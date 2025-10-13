---
{"dg-publish":true,"permalink":"/notes/organize-resource-pkm-app-nb/","title":"Nb","tags":["source.app"]}
---


## Setup github sync

Remote:

```bash
mkdir nb
git init --bare nb/personal.git
git init --bare nb/work.git
```

Local:

```bash
nb notebook add personal
nb notebook add work
nb personal:remote set user@domain.com:/home/user/nb/personal.git
nb work:remote set user@domain.com:/home/user/nb/work/git.
```bash
