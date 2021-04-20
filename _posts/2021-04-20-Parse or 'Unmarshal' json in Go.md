## Prerequisites

- Import `encoding/json`

First is to create a struct

```go
type Payload struct {
  Name      string    `json:"name"`
  Email     string    `json:"email"`
  Addresses []string  `json:"addresses"`
  Desc      string    `json:"desc"`
}
```

After you get from the file or fetch from the endpoint, do:

```go
response, err := http.DefaultClient.Do(request)

if err != nil {
  log.Printf("Could not make a request - %v", err)
}
byteValue, _ := ioutil.ReadAll(response.Body)

var payload model.Payload
json.Unmarshal([]byte(byteValue), &payload)

```

And that's that.
