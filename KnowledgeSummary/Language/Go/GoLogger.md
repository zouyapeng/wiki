## Go Base Logger

### Base Example

```go
package main
import (
    "log"      
)
func init(){
    log.SetPrefix("LOG: ")
    log.SetFlags(log.Ldate | log.Lmicroseconds | log.Llongfile)
    log.Println("init started")
}
func main() {
// Println writes to the standard logger.
    log.Println("main started")

// Fatalln is Println() followed by a call to os.Exit(1)
    log.Fatalln("fatal message")

// Panicln is Println() followed by a call to panic()
    log.Panicln("panic message")
}
```

### File Example

```go
package main
import (
        "log"
        "os"
)

func main() {
        //create your file with desired read/write permissions
        f, err := os.OpenFile("filename", os.O_WRONLY|os.O_CREATE|os.O_APPEND, 0644)
        if err != nil {
                log.Fatal(err)
        }   
        //defer to close when you're done with it, not because you think it's idiomatic!
        defer f.Close()
        //set output of logs to f
        log.SetOutput(f)
        //test case
        log.Println("check to make sure it works")
}
```

### Advanced Example

```go
package main

import (
    "io"
    "io/ioutil"
    "log"
    "os"
)

var (
    Info    *log.Logger
    Warning *log.Logger
    Error   *log.Logger
)

func init() {
    Info = log.New(os.Stdout,
        "INFO: ",
        log.Ldate|log.Ltime|log.Lshortfile)

    Warning = log.New(os.Stdout,
        "WARNING: ",
        log.Ldate|log.Ltime|log.Lshortfile)

    Error = log.New(os.Stderr,
        "ERROR: ",
        log.Ldate|log.Ltime|log.Lshortfile)
}

func main() {
    Info.Println("Special Information")
    Warning.Println("There is something you need to know about")
    Error.Println("Something has failed")
}
```



## Go Advanced Logger\(github.com/Sirupsen/logrus\)

### Base example

```go
package main
import (
  log "github.com/Sirupsen/logrus"
  "github.com/logmatic/logmatic-go"
)
func main() {
    // use JSONFormatter
    log.SetFormatter(&logmatic.JSONFormatter{})
    // log an event as usual with logrus
    log.WithFields(log.Fields{"string": "foo", "int": 1, "float": 1.1 }).Info("My first ssl event from golang")
}
```

Rotating Example

```go
package main
import (
  log "github.com/Sirupsen/logrus"
  "gopkg.in/natefinch/lumberjack.v2"
)

func init(){
    log.SetOutput(&lumberjack.Logger{
	Filename:   "Rotating.log",
	MaxSize:    10, // megabytes
	MaxBackups: 5,
	MaxAge:     1, // days
	Compress:   false,
    })
    
    log.SetFormatter(
        &log.TextFormatter{
            TimestampFormat: "2006-01-02 15:04:05",
	    FullTimestamp:   true,
	    DisableColors:   false,
	}
    )
    
    log.SetLevel(log.InfoLevel)
}

func main() {
    // log an event as usual with logrus
    log.WithFields(log.Fields{"string": "foo", "int": 1, "float": 1.1 }).Info("My first ssl event from golang")
}
```



