# Go, Golang

# Types and type conversion

```
var v interface{} = 2.3
t := fmt.Sprintf("%T", v)
fmt.Println(fmt.Sprintf("Value: %T", v))
fmt.Println("Type: ",t)
fmt.Println(fmt.Sprintf("Type of value type: %T", t))

switch f := v.(type) {
case float64:
    fmt.Println("float64:", f)
default:
    fmt.Println(f)
}
```
