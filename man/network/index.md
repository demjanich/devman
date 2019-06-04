# Curl

## Verbose 

When we are testing, it’s a good idea to set the verbose mode on:

```curl -v http://www.example.com/```

As a result, the commands would provide helpful information such as the resolved IP address, the port we are trying to connect to and the headers.

## Output

By default, curl outputs the response body to standard output. Optionally, we can provide the output option to save to a file:

```curl -o out.json http://www.example.com/index.html```

## GET

```curl -v http://localhost:8080/example.html```

## POST

Use the data option.

```curl -d 'id=9&name=baeldung' http://localhost:8080/test```

or, pass a file containing the request body to the data option like this:

```
curl -d @request.json -H "Content-Type: application/json" 
  http://localhost:8080/test
```

## PUT

```
curl -d @request.json -H 'Content-Type: application/json' 
  -X PUT http://localhost:8080/test
```

## DELETE

Use DELETE by using the -X option:

```curl -X DELETE http://localhost:8080/foo/9```

## Custom Headers

We can replace the default headers or add our own headers. For instance, to change the Host header, we do this:

```
curl -H "Host: com.baeldung" http://example.com/
```

To switch off the User-Agent header, we put in an empty value:

```curl -H "User-Agent:" http://example.com/```

The most usual scenario while testing is changing the Content-Type and Accept header. We’d just have to prefix each header with the -H option:

```
curl -d @request.json -H "Content-Type: application/json" 
  -H "Accept: application/json" http://localhost:8080/foo/new
```

