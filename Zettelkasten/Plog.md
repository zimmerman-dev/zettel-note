 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚7:49 pm  📆 Tue Sep 2
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: Plog
`plog`  is a third-party logger, and while there are many options, PLOG is great because it's simple, well-documented, and easy to integrate for beginners.
1. **Copy the source** - Simply copy the `plog` directory into your source tree
```bash
.                           <-- root of your solution
├── README.md
└── src
    ├── 3rd-party           <-- directory for all 3rd-party dependencies
    │   └── plog            <-- plog is copied there
    │       ├── include     <-- add this to your include search path
    │       │   └── plog
    │       ├── LICENSE
    │       └── README.md
    ├── proj1
    └── proj2  
```

2. **Git submodule** - Add `plog` as a git submodule to keep it up to date and track its version:
```bash
git submodule add https://github.com/SergiusTheBest/plog.git src/3rd-party/plog
git commit -m "Add plog as a submodule"	   
```

3. **Cmake Integration** - You can add `plog` directly to your build:
```text
add_subdirectory(3rd-party/plog) # Adds plog to your CMake project

add_executable(myproj main.cpp)
target_link_libraries(myproj plog::plog) # Links and sets include path
```
### 🔹 Step 1: Adding includes
At first your project needs to know about `plog`. For that you have to:

1. Add `plog/include` to the project include paths
2. Add `#include <plog/Log.h>` into your cpp/h files (if you have precompiled headers it is a good place to add this include there)
### 🔹 Step 2: Initialization
To use plog, you must initialize the logger by including the appropriate header and calling the corresponding `plog::init` overload:

```c
Logger& init(Severity maxSeverity, ...
```

`maxSeverity` is the logger severity upper limit. Log messages with a severity value higher (less severe) than the limit are dropped.

Plog defines the following severity levels:

```c
enum Severity
{
    none = 0,
    fatal = 1,
    error = 2,
    warning = 3,
    info = 4,
    debug = 5,
    verbose = 6
};
```

> **Note** Messages with severity level `none` will always be printed.

Plog provides several convenient initializer functions to simplify logger setup for common use cases. These initializers configure the logger with typical appenders and formatters, so you can get started quickly without manually specifying all template parameters.
####  RollingFileInitializer
Use this when you want to log to a file with automatic rolling (rotation) based on size and count. Add `#include <plog/Initializers/RollingFileInitializer.h>` and call `init`:

```c
Logger& init(Severity maxSeverity, const util::nchar* fileName, size_t maxFileSize = 0, int maxFiles = 0);
```

- The log format is determined by the file extension:
    - `.csv` → [CSV format](https://github.com/SergiusTheBest/plog#csvformatter)
    - anything else → [TXT format](https://github.com/SergiusTheBest/plog#txtformatter)
- You can override the format by specifying a formatter as a template parameter, e.g. `plog::init<plog::CsvFormatter>(...)`.
- Rolling is controlled by `maxFileSize` (bytes) and `maxFiles` (number of files to keep). If either is zero, rolling is disabled.

Example:

```c
#include <plog/Log.h>
#include <plog/Initializers/RollingFileInitializer.h>

plog::init(plog::warning, "c:\\logs\\log.csv", 1000000, 5);
```

Here the logger is initialized to write all messages with up to warning severity to a file in csv format. Maximum log file size is set to 1'000'000 bytes and 5 log files are kept.
####  ConsoleInitializer
Use this to log to the console (stdout or stderr) with color output. Add `#include <plog/Initializers/ConsoleInitializer.h>` and call `init`:

```c
Logger& init(Severity maxSeverity, OutputStream outputStream)
```

- By default it uses [TXT format](https://github.com/SergiusTheBest/plog#txtformatter) but it can be overriden by specifying a formatter as a template parameter, e.g. `plog::init<plog::CsvFormatter>(...)`.
- `outputStream` chooses the output stream: `plog::streamStdOut` or `plog::streamStdErr`.

Example:

```c
#include <plog/Log.h>
#include <plog/Initializers/ConsoleInitializer.h>

plog::init<plog::TxtFormatter>(plog::error, plog::streamStdErr); // logs error and above to stderr
```

####  Manual initialization (Init.h)
For advanced or custom setups add `#include <plog/Init.h>` and call `init`:

```c
Logger& init(Severity maxSeverity = none, IAppender* appender = NULL);
```

You must construct and manage the appender yourself.

Example:

```c
#include <plog/Log.h>
#include <plog/Init.h>

static plog::ConsoleAppender<plog::TxtFormatter> appender;
plog::init(plog::info, &appender); // logs info and above to the specified appender
```

> **Note** See [Custom initialization](https://github.com/SergiusTheBest/plog#custom-initialization) for advanced usage.

### 🔹Step 3: Logging

[](https://github.com/SergiusTheBest/plog#step-3-logging)

Logging is performed with the help of special macros. A log message is constructed using stream output operators `<<`. Thus it is type-safe and extendable in contrast to a format string output.

### 🔹 Basic logging macros
This is the most used type of logging macros. They do unconditional logging.

#### Long macros:
```c
PLOG_VERBOSE << "verbose";
PLOG_DEBUG << "debug";
PLOG_INFO << "info";
PLOG_WARNING << "warning";
PLOG_ERROR << "error";
PLOG_FATAL << "fatal";
PLOG_NONE << "none";
```

#### Short macros:
```c
PLOGV << "verbose";
PLOGD << "debug";
PLOGI << "info";
PLOGW << "warning";
PLOGE << "error";
PLOGF << "fatal";
PLOGN << "none";
```

#### Function-style macros:
```c
PLOG(severity) << "msg";
```

### 🔹 Conditional logging macros
These macros are used to do conditional logging. They accept a condition as a parameter and perform logging if the condition is true.
#### Long macros:
```c
PLOG_VERBOSE_IF(cond) << "verbose";
PLOG_DEBUG_IF(cond) << "debug";
PLOG_INFO_IF(cond) << "info";
PLOG_WARNING_IF(cond) << "warning";
PLOG_ERROR_IF(cond) << "error";
PLOG_FATAL_IF(cond) << "fatal";
PLOG_NONE_IF(cond) << "none";
```

#### Short macros:
```c
PLOGV_IF(cond) << "verbose";
PLOGD_IF(cond) << "debug";
PLOGI_IF(cond) << "info";
PLOGW_IF(cond) << "warning";
PLOGE_IF(cond) << "error";
PLOGF_IF(cond) << "fatal";
PLOGN_IF(cond) << "none";
```

#### Function-style macros:
```c
PLOG_IF(severity, cond) << "msg";
```

### 🔹 Logger severity checker
In some cases there is a need to perform a group of actions depending on the current logger severity level. There is a special macro for that. It helps to minimize performance penalty when the logger is inactive.

```c
IF_PLOG(severity)
```

Sample:

```c
IF_PLOG(plog::debug) // we want to execute the following statements only at debug severity (and higher)
{
    for (int i = 0; i < vec.size(); ++i)
    {
        PLOGD << "vec[" << i << "]: " << vec[i];
    }
}
```
