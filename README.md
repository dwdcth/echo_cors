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

When request options,Access-Control-Allow-Origin will dynamic change 
```
Access-Control-Allow-Credentials →true
Access-Control-Allow-Methods →GET,HEAD,PUT,PATCH,POST,DELETE
Access-Control-Allow-Origin →http://localhost:1323
```

becouse cors only allow req below:
- application/x-www-form-urlencoded
- multipart/form-data
- text/plain

When you use json in ajax,you should change it.If you use axios,you can do:
```
const Axios = axios.create({
    headers: {
        'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8'
    },
    withCredentials: true
});


Axios.interceptors.request.use(
    config => {
        if (config.method === 'post' || config.method === 'put') {
            if (config.data) {
                var queryString = Object.keys(config.data)
                    .map(key => {
                        return encodeURIComponent(key) + '=' + encodeURIComponent(config.data[key]);
                    })
                    .join('&');
                config.data = queryString;
            }
            return config;
        }
        return config;
    },
    error => {
        return Promise.reject(error);
    }
);
```
