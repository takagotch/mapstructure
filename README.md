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

type Family struct {
  City string
}
type Person struct {
  Family `mapstructure:",squash`
  Location `mapstructure:",squash"`
  FirstName string
}

input := map[string]interface{}{
  "FirstName": "Mitchell",
  "LastName": "Hashimoto",
  "City": "San Francisco"
}

var result Person
err := Decode(input, &result)
if err != nil {
  panic(err)
}

fmt.Printf("%s %s, %s", result.FirstName, result.LastName, result.City)


type Person struct {
  Name string
  Age int
  Emails []string
  Extra map[string]string
}

input := map[string]interface{} {
  "name": 123,
  "age": "bad value",
  "emails": []int{1, 2, 3},
}

var result Person
err := Decode(input, &result)
if err == nil {
  panic("should have an error")
}

fmt.Println(err.Error())


type Person struct {
  Name string
  Age int
}

input := map[string]interface{} {
  "name": "Mitchell",
  "age": 91,
  "email": "foo@bar.com",
}

var md Metadata
var result Person
config := &DecoderConfig{
  Metadata: &md,
  Result: &result,
}

decoder, err := NewDecoder(config)
if err != nil {
  panic(err)
}

if err := decoder.Decode(input); err != nil {
  panic(err)
}

fmt.Printf("Unused keys: %#v", md.Unused)

type Person struct {
  Name string `mapstructure:"person_name"`
  Age int `mapstructure:"person_age"`
}

input := map[string]interface{} {
  "person_name": "Mitchell",
  "person_age": 91,
}

var result Person
err := Decode(input, &result)
if err != nil {
  panic(err)
}

fmt.Printf("%#v", result)


type Person struct {
  Name string
  Age int
  Emails []string
}

input := map[string]interface{} {
  "name": 123,
  "age": "42",
  "emails": map[string]interface{}{},
}

var result Person
config := &DecoderConfig{
  WeaklyTypedIntput: true,
  Result: &result,
}

decoder, err := NewDecoder(config)
if err != nil {
  panic(err)
}

err = decoder.Decode(input)
if err != nil {
  panic(err)
}

fmt.Printf("%#v", result)


func DecodeHookExec(
  raw DecodeHookFunc,
  from reflect.Type, to reflect.Type,
  data interface{}) (interface{}, error)
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


