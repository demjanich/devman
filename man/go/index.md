# Go, Golang

## Types and Type Conversion

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

## Comma Ok Idiom

```
var timeZone = map[string]int{
    "UTC": 0 * 60 * 60,
    "EST": -5 * 60 * 60,
    "CST": -6 * 60 * 60,
    "MST": -7 * 60 * 60,
    "PST": -8 * 60 * 60,
}

if seconds, ok := timeZone["PST"]; ok {
    return seconds
}
```
