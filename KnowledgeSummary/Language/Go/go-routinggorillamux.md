## Routing \(using gorilla/mux\)

### example

```go
package main

import (
	"fmt"
	"net/http"

	"github.com/gorilla/mux"
)

func main() {
	r := mux.NewRouter()
	r.HandleFunc("/books/{title}/page/{page}", func(w http.ResponseWriter, r *http.Request) {
		vars := mux.Vars(r)
		title := vars["title"]
		page := vars["page"]

		fmt.Fprintf(w, "You've requested the book: %s on page %s\n", title, page)
	})

	http.ListenAndServe(":80", r)
}
```

### Features of the`gorilla/mux`Router

#### Methods

Restrict the request handler to specific HTTP methods.

```Golang
r.HandleFunc("/books/{title}", CreateBook).Methods("POST")
r.HandleFunc("/books/{title}", ReadBook).Methods("GET")
r.HandleFunc("/books/{title}", UpdateBook).Methods("PUT")
r.HandleFunc("/books/{title}", DeleteBook).Methods("DELETE")
```

#### Hostnames & Subdomains

Restrict the request handler to specific hostnames or subdomains.

```Golang
r.HandleFunc("/books/{title}", BookHandler).Host("www.mybookstore.com")
```

#### Schemes

Restrict the request handler to http/https.

```Golang
r.HandleFunc("/secure", SecureHandler).Schemes("https")
r.HandleFunc("/insecure", InsecureHandler).Schemes("http")
```

#### Path Prefixes & Subrouters

```Golang
bookrouter := r.PathPrefix("/books").Subrouter()
bookrouter.HandleFunc("/", AllBooks)
bookrouter.HandleFunc("/{title}", GetBook)
```



Reference：

[Routing \(using gorilla/mux\)](https://gowebexamples.com/routes-using-gorilla-mux/)

