# JWT

A JWT plugin for gin, iris, go-frame, beego, go-zero, go-chassis, go-kit and other frameworks

## **Note**  
> This project is forked from [dobyte/jwt](https://github.com/dobyte/jwt). The original version did not support `ParserOption`, so modifications have been made to add this feature.  
> 本项目基于 [dobyte/jwt](https://github.com/dobyte/jwt) ，因原版不支持 `ParserOption`，因此进行了相关修改。


## Use

Download and install
```shell
go get github.com/hylio1127/jwt
```



Demo

```go
package main

import (
	"fmt"
	"log"
	"github.com/hylio1127/jwt"
)

func main() {
	auth, err := jwt.NewJWT(
		jwt.WithIssuer("backend"),
		jwt.WithSignAlgorithm(jwt.HS256),
		jwt.WithSecretKey("secret"),
		jwt.WithValidDuration(3600),
		jwt.WithLookupLocations("header:Authorization"),
		jwt.WithIdentityKey("uid"),
	)
	if err != nil {
		log.Fatal("create jwt instance failed:" + err.Error())
    }

	token, err := auth.GenerateToken(jwt.Payload{
		"uid":     1,
		"account": "hylio",
	})
	if err != nil {
		log.Fatal("Generate token failed:" + err.Error())
	}

	fmt.Println(token)
}
```

