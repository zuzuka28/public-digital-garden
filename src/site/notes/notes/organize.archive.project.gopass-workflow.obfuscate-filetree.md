---
{"dg-publish":true,"permalink":"/notes/organize.archive.project.gopass-workflow.obfuscate-filetree/","title":"Obfuscate Filetree"}
---


[[notes/organize.resource.it.lang.shell\|notes/organize.resource.it.lang.shell]] скрипт для обсускации файловой иерархии

Пример использования 

---

```bash
#!/usr/bin/env bash
#
# utility for flattening and folder structure obfuscation


#######################################
# obfuscate_secret - obfuscates string with hash256func
# Globals:
#   hash256func
# Arguments:
#   1 - path to secret to be obfuscated
# Outputs:
#   1 - hash with prefix secret-
#######################################
function obfuscate_secret() {
  sourceSecret=$1
  obfuscatedSecret=$(echo -n "$sourceSecret" | eval "$hash256func" | cut -d' ' -f1)
  echo "secret-${obfuscatedSecret}"
}

#######################################
# decript_secrets_index - decript secrets index
# Globals:
#   secrets_index_file
# Outputs:
#   decript secrets index
#######################################
function decript_secrets_index () {
  if ! [ -f "$secrets_index_file" ]; then
    return
  fi

  age -d -i "$identities" "$secrets_index_file" > "$secrets_root_dir/tmp" \
    && mv "$secrets_root_dir/tmp" "$secrets_index_file"
}

#######################################
# encript_secrets_index - encript secrets index
# Globals:
#   secrets_index_file
# Outputs:
#   encript  secrets index
#######################################
function encript_secrets_index () {
  if ! [ -f "$secrets_index_file" ]; then
    return
  fi

  age -e -r "$(cat "$recipiens")" "$secrets_index_file" > "$secrets_root_dir/tmp" \
    && mv "$secrets_root_dir/tmp" "$secrets_index_file"
}

#######################################
# load_secrets_index - loads secrets index file to memory
# Globals:
#   secrets_index_file
#   secrets_index
# Outputs:
#   fills secrets_index variable with pairs from secrets_index_file
#######################################
function load_secrets_index() {
  if ! [ -f "$secrets_index_file" ]; then
    return
  fi

  while IFS= read -r line; do
    local hash
    local path
    hash=$(echo "$line" | jq -r '.hash')
    path=$(echo "$line" | jq -r '.path')
    secrets_index["$hash"]="$path"
  done < <(jq -c '.[]' "$secrets_index_file")
}


#######################################
# unset_unused_secrets_from_index - unset secrets not presented in secrets vault
# Globals:
#   secrets_index
#   secrets_root_dir
# Outputs:
#   removes secrets from secrets_index if no such files in secrets_root_dir
#######################################
function unset_unused_secrets_from_index() {
  for fname in "${!secrets_index[@]}"; do
    if [ ! -f "$secrets_root_dir/$fname" ]; then
      unset 'secrets_index[$fname]'
    fi
  done
}

#######################################
# obfuscate_secrets_vault - obfuscate filenames and flatten filestructure of secrets vault
# Globals:
#   secrets_index
#   secrets_root_dir
# Outputs:
#   obfuscate filenames and flatten filestructure of secrets vault
#######################################
function obfuscate_secrets_vault() {
  secretPathRe="^.*(secret-[0-9a-f]{64})$"

  while IFS= read -r -d '' path; do
    if [[notes/$path =~ $secretPathRe]]; then # add already obfuscated files to index
      matched_part=${BASH_REMATCH[1]}
      if [[ ! ${secrets_index[$matched_part]} ]]; then
        secrets_index[$matched_part]=$path
      fi
    elif [ ! -d "$path" ]; then # or obfuscate and move to root (flatten filestructure)
      nn=$(obfuscate_secret "$path")
      mv "$path" "$secrets_root_dir/$nn"
      secrets_index[$nn]=$path
    fi
  done < <(find "$secrets_root_dir" -mindepth 1 -print0)

  find "$secrets_root_dir" -depth -type d -exec rmdir {} + 2>/dev/null
}


#######################################
# save_secrets_index - saves secrets index to file in json format
# Globals:
#   secrets_index
#   secrets_index_file
# Outputs:
#   write [{"hash":"", "path":""}] to secrets_index_file
#######################################
function save_secrets_index() {
  entries="["
  for h in "${!secrets_index[@]}"; do
    p=${secrets_index[$h]}
    entries+="$(printf '{"hash":"%s","path":"%s"},' "$h" "${p/#$secrets_root_dir}")"
  done
  entries=${entries%,}
  entries+="]"
  echo "$entries" | jq -c '.' >"$secrets_index_file"
}

#######################################
# build_secrets_tree - restores folder tree from secrets index
# Globals:
#   secrets_index
#   secrets_root_dir
# Outputs:
#   restores folder tree from secrets index
#######################################
function build_secrets_tree() {
  for h in "${!secrets_index[@]}"; do
    p=${secrets_index[$h]}
    mkdir -p "$secrets_root_dir/$(dirname "$p")" \
      && mv "$secrets_root_dir/$h" "$secrets_root_dir/$p"
  done
}

if ((BASH_VERSINFO[0] < 4)); then
  echo "Sorry, you need at least bash-4.0 to run this script." >&2; exit 1;
fi

if ! [ -x "$(command -v jq)" ]; then
  echo 'Error: jq is not installed.' >&2
  exit 1
fi

if ! [ -x "$(command -v age)" ]; then
  echo 'Error: age is not installed.' >&2
  exit 1
fi

if [[notes/"$OSTYPE" == "linux-gnu"*]]; then
  hash256func=sha256sum
elif [[notes/"$OSTYPE" == "darwin"*]]; then
  hash256func="shasum -a 256"
fi

secrets_root_dir=""
secrets_index_file=""
action=""
action_encript="encript"
action_decript="decript"

recipiens="$HOME/.local/share/gopass/stores/root/.age-recipients"
identities="$HOME/.config/gopass/age/identities"

while getopts ":edi:r:" option; do
  case $option in
    r)
      secrets_root_dir="$OPTARG"
      ;;
    i)
      secrets_index_file="$secrets_root_dir/$OPTARG"
      ;;
    e)
      action="$action_encript"
      ;;
    d)
      action="$action_decript"
      ;;
    *)
      echo "Usage: $0 [-r vault dirname] [-i secrets index file] [-e encript secrets] [-d decript secrets]"
      exit 1
      ;;
  esac
done

if [ -z "$secrets_root_dir" ]; then
  echo "Must specify dir to obfuscate - [-r vault dirname]"
  exit 1
fi

if [ -z "$secrets_index_file" ]; then
  secrets_index_file="$secrets_root_dir/index"
fi

if [ -z "$action" ]; then
  echo "Must select action - [-e encript secrets] [-d decript secrets]"
  exit 1
fi

echo "$action"

if [ "$action" = "$action_decript" ]; then
  if ! [ -f "$secrets_index_file" ]; then
    echo "Can't decript files by not existing index file"
    exit 1
  fi
fi

declare -A secrets_index

if [ "$action" = "$action_encript" ]; then
  load_secrets_index
  unset_unused_secrets_from_index
  obfuscate_secrets_vault
  save_secrets_index
  encript_secrets_index
fi


if [ "$action" = "$action_decript" ]; then
  decript_secrets_index
  load_secrets_index
  unset_unused_secrets_from_index
  build_secrets_tree
fi
```