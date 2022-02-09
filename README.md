
# Quicklog

A quick-and-dirty logger for python that's extensible by design.

## Installation

### Pip (recommended)

```bash
$ pip install coderkearns_quicklog
```

### Git

```bash
$ git clone https://github.com/coderkearns/quicklog.git
$ mv quicklog/coderkearns_quicklog .
$ rm -rf quicklog
```

## API Reference

### BaseLogger

In [`base.py`](base.py). Extensible but unusable on its own. All other loggers should extend this class and implement a `log(level, *args)` method.

#### `BaseLogger.get_level(level_name)`

Gets a level number from the given name.

```python
BaseLogger.get_level("ERROR") # => 3
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `level_name`   | `str` | **Required**. The name of the level. |

#### `BaseLogger.get_level_name(self, level)`

Gets a level name given its number.

```python
BaseLogger.get_level_name(3) # => "ERROR"
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `level`   | `int` | **Required**. The number of the level. |

#### `__init__(level=1)`

```python
logger = BaseLogger(level)
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `level`   | `int|string` | **Optional**, default `1`. The level to show. Can be the level's number or the level's name. |

#### `set_level(level)`

Changes the minimum level to log to `level`

```python
logger = BaseLogger(1) # INFO
logger.set_level(0) # DEBUG
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `level`   | `int` | **Required**. The level to show. |

#### `debug(*args)`

Logs a *DEBUG* level message.

```python
logger.debug("some debug") # [DEBUG] some debug
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `*args`   | `any` | The values to log. |

#### `info(*args)`

Logs a *INFO* level message.

```python
logger.info("some info") # [INFO] some info
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `*args`   | `any` | The values to log. |

#### `warning(*args)`

Logs a *WARNING* level message.

```python
logger.warning("some warning") # [WARNING] some warning
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `*args`   | `any` | The values to log. |

#### `error(*args)`

Logs a *ERROR* level message.

```python
logger.error("some error") # [ERROR] some error
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `*args`   | `any` | The values to log. |

#### `critical(*args)`

Logs a *CRITICAL* level message.

```python
logger.critical("some critical") # [CRITICAL] some critical
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `*args`   | `any` | The values to log. |

#### `fatal(*args)`

Logs a *FATAL* level message.

```python
logger.fatal("some fatal") # [FATAL] some fatal
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `*args`   | `any` | The values to log. |

### FileLogger

In [`file.py`](file.py). Stores it's logs in a file.

#### `__init__(path, level=1)`

Creates a new FileLogger for the given path.

```python
file_logger = FileLogger("./filelogs.log", "ERROR")
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `path`   | `str` | The path to the log file. It it does not exist, create it. |

#### `log(level, *args)`

Appends a log the the log file.

Formatted as `[<level_name>] <args>`

#### `open()`

Opens the file at the given path.

#### `close()`

Closes the file at the given path.

### MemoryLogger

In [`memory.py`](memory.py). Stores it's logs in a list.

#### `log(level, *args)`

Adds a log to the internal list.

Formatted as `["<level_name>", <args>]`

#### `get_logs()`

Returns a list with all the logs in the format `[level_name, *args]`

```python
memory_logger.debug("a")
memory_logger.error("b", 1)

memory_logger.get_logs()
# => [["DEBUG", "a"], ["ERROR", "b", 1]]
```

### StdoutLogger

In [`stdout.py`](stdout.py). Logs to the stdout using `print()`.

#### `log(level, *args)`

Prints a log to the stdout.

Formatted as `[<level_name>] <args>`


## License

[MIT](https://choosealicense.com/licenses/mit/)
