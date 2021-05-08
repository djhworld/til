+++
title = "Golang Snippets"

date = 2021-05-08

[taxonomies]
tags = ["golang"]
+++

Just some snippets I regularly refer to 

Reading from Stdin

```go
package main

 import (
   "bufio"
   "fmt"
   "os"
 )

 func main() {
   scanner := bufio.NewScanner(os.Stdin)
   for scanner.Scan() {
     fmt.Println(scanner.Text()) // Println will add back the final '\n'
   }
   if err := scanner.Err(); err != nil {
     fmt.Fprintln(os.Stderr, "reading standard input:", err)
   }
 }
```

Simple web server

```go
package main

import (
    "fmt"
    "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hi there, I love %s!", r.URL.Path[1:])
 }

func main() {
    http.HandleFunc("/", handler)
    http.ListenAndServe(":8080", nil)
}
```

Deserialising JSON

```go
package main

import (
  "encoding/json"
  "fmt"
)

func main() {
  var jsonBlob = []byte(`[
    {"Name": "Platypus", "Order": "Monotremata"},
    {"Name": "Quoll",    "Order": "Dasyuromorphia"}
  ]`)
  type Animal struct {
    Name  string
    Order string
  }
  var animals []Animal
  err := json.Unmarshal(jsonBlob, &animals)
  if err != nil {
    fmt.Println("error:", err)
  }
  fmt.Printf("%+v", animals)
}
```

Partition a list by batch size

```go
func min(a, b int) int {
    if a <= b {
        return a
    }
    return b
}

for i := 0; i < len(records); i += 500 {
        batch := records[i:min(i+500, len(records))]
        fmt.Println("Submitting batch of", len(batch), "records")
    }
```


Use TLS cert in http request

```go
cert, err := tls.LoadX509KeyPair("<CERT>", "<KEY>")
       if err != nil {
               fmt.Println("Failed", err)
               return
       }
       tr := &http.Transport{
               TLSClientConfig: &tls.Config{
                       Certificates: []tls.Certificate{cert},
               },
       }
       client := &http.Client{Transport: tr}
       client.Get("endpoint")
```


Sorting a slice of things using an anonymous function

```go
var myslice [][]byte
...
sort.Slice(myslice, func(i, j int) bool {
    return bytes.Compare(myslice[i], myslice[j]) < 0
})
```


