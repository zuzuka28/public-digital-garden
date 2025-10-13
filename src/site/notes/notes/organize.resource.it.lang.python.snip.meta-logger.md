---
{"dg-publish":true,"permalink":"/notes/organize.resource.it.lang.python.snip.meta-logger/","title":"Meta Logger"}
---


```py
import abc
import enum
import logging
import os


class LogLevel(int, enum.Enum):
    DEBUG = logging.DEBUG
    INFO = logging.INFO
    WARN = logging.WARN
    ERROR = logging.ERROR
    FATAL = logging.FATAL


def get_log_level() -> LogLevel:
    env_log_level = os.getenv("LOG_LEVEL")
    if env_log_level is None:
        env_log_level = "DEBUG"
    env_log_level = env_log_level.upper()

    try:
        level = getattr(LogLevel, env_log_level)
    except AttributeError:
        print(f"Unknown log-level in 'LOG_LEVEL' envar: {env_log_level}")
        return exit(1)
    return level


def get_new_logger(logger_name: str, log_level: LogLevel) -> logging.Logger:
    logger = logging.getLogger(name=logger_name)
    logger.setLevel(log_level)
    # Формат лога
    s_format = logging.Formatter(
        fmt="%(asctime)s.%(msecs)03d  %(levelname)-8s [%(name)s] - %(message)s",
        datefmt="%Y-%m-%d %H:%M:%S",
    )
    s_handler = logging.StreamHandler()
    s_handler.setFormatter(s_format)
    logger.addHandler(s_handler)
    return logger


class LogConsoleMixinMeta(abc.ABCMeta):
    LOG_LEVEL: LogLevel = get_log_level()
    logger: logging.Logger

    def __new__(mcs, name, bases, attrs):
        cls = super(LogConsoleMixinMeta, mcs).__new__(mcs, name, bases, attrs)
        cls.logger = get_new_logger(logger_name=name, log_level=mcs.LOG_LEVEL)
        return cls


class LogConsoleMixin:
    LOG_LEVEL: LogLevel = get_log_level()

    def __init__(self):
        self.logger = get_new_logger(
            logger_name=self.__class__.__name__, log_level=self.LOG_LEVEL
        )
```