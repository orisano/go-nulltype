# go-nulltype

Nullable types friendly to json.Encoder, json.Decoder, database/sql, fmt.Stringer.

## Usage

```go
import "github.com/mattn/go-nulltype"

type User struct {
	Name	nulltype.NullString `json:"name"`
}
```

### friendly to Stringer

```go
var user User
fmt.Println(user.Name) // nil

user.Name.Set("Bob")
fmt.Println(user.Name) // Bob

user.Name.Value()
fmt.Println(user.Name.Value() == "Bob") // true

user.Name.Reset()
fmt.Println(user.Name) // nil
```

### friendly to json.MarshalJSON

```go
var user User
json.NewEncoder(os.Stdout).Encode(user) // {"name": nil}

user.Name.Set("Bob")
json.NewEncoder(os.Stdout).Encode(user) // {"name": "Bob"}
```

### friendly to json.UnmarshalJSON

```go
var user User
s := `{"name": "Bob"}`
json.NewDecoder(strings.NewReader(s)).Decode(&user)
fmt.Println(user.Name) // Bob

s = `{"name": null}`
json.NewDecoder(strings.NewReader(s)).Decode(&user)
fmt.Println(user.Name) // nil
```

## Installation

```
go get github.com/mattn/go-nullable
```

## License

MIT

## Author

Yasuhiro Matsumoto