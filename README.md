# echo_cors

```go get github.com/dwdcth/echo_cors```

```
package main

import (
	"github.com/dwdcth/echo_cors"
	"github.com/labstack/echo"
	"net/http"

)
func main() {
	e := echo.New()
	e.Use(echo_cors.CORSWithConfig(echo_cors.CORSConfig{AllowCredentials: true, AllowAllHost:true}))
	e.GET("/", func(c echo.Context) error {
		return c.String(http.StatusOK, "Hello, World!")
	})
	e.Logger.Fatal(e.Start(":1323"))
}
```

when request options,Access-Control-Allow-Origin will dynamic change 
```
Access-Control-Allow-Credentials →true
Access-Control-Allow-Methods →GET,HEAD,PUT,PATCH,POST,DELETE
Access-Control-Allow-Origin →http://localhost:1323
```