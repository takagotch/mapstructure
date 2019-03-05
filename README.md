### mapstructure
---
https://github.com/mitchellh/mapstructure

```go
type Person struct {
  Name string
  Age int
  Emails []string
  Extra map[string]string
}

input := map[string]interface{} {
  "name": "Mitchell",
  "age": 91,
  "emails": []string{"one", "two", "three"},
  "extra": map[string]string{
    "twitter": "mitchelh",
  },
}

var result Person
err := Decode(input, &result)
if err != nil {
  panic(err)
}

fmt.Printf("%#v", result)















```

```
go get github.com/mitchelh/mapstructure
```

```
{
  "type": "person",
  "name": "Mitchell"
}
```


