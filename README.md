# golang 1.22 feature with http mux

```golang
package main

import (
	"fmt"
	"net/http"
)

func main() {
	fmt.Println("Building RESTful APIs in Go1.22!")

	mux := http.NewServeMux()

	mux.HandleFunc("GET /comment", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintf(w, "resturn all commments\n")
	})
	mux.HandleFunc("GET /comment/{id}", func(w http.ResponseWriter, r *http.Request) {
		id := r.PathValue("id")
		fmt.Fprintf(w, "resturn a single commment with id: %s\n", id)
	})

	mux.HandleFunc("POST /comment", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintf(w, "post a new commment\n")
	})

	if err := http.ListenAndServe(":8000", mux); err != nil {
		fmt.Println(err.Error())
	}
}
```

## compare with previous handle 

1. just use a http method declare syntax to specify which http method to handle

no need to parse the http method anymore

2. with path parser to handle path parameter