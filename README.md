# GZIP gin's middleware

[![Build Status](https://travis-ci.org/hubsync/gzip.svg)](https://travis-ci.org/hubsync/gzip)
[![codecov](https://codecov.io/gh/hubsync/gzip/branch/master/graph/badge.svg)](https://codecov.io/gh/hubsync/gzip)
[![Go Report Card](https://goreportcard.com/badge/github.com/hubsync/gzip)](https://goreportcard.com/report/github.com/hubsync/gzip)
[![GoDoc](https://godoc.org/github.com/hubsync/gzip?status.svg)](https://godoc.org/github.com/hubsync/gzip)
[![Join the chat at https://gitter.im/gin-gonic/gin](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/gin-gonic/gin)

Gin middleware to enable `GZIP` support.

## Usage

Download and install it:

```sh
go get github.com/hubsync/gzip
```

Import it in your code:

```go
import "github.com/hubsync/gzip"
```

Canonical example:

```go
package main

import (
	"fmt"
	"net/http"
	"time"

	"github.com/hubsync/gzip"
	"github.com/gin-gonic/gin"
)

func main() {
	r := gin.Default()
	r.Use(gzip.Gzip(gzip.DefaultCompression))
	r.GET("/ping", func(c *gin.Context) {
		c.String(http.StatusOK, "pong "+fmt.Sprint(time.Now().Unix()))
	})

	// Listen and Server in 0.0.0.0:8080
	r.Run(":8080")
}
```

Customized Excluded Extensions

```go
package main

import (
	"fmt"
	"net/http"
	"time"

	"github.com/hubsync/gzip"
	"github.com/gin-gonic/gin"
)

func main() {
	r := gin.Default()
	r.Use(gzip.Gzip(gzip.DefaultCompression, gzip.WithExcludedExtensions([]string{".pdf", ".mp4"})))
	r.GET("/ping", func(c *gin.Context) {
		c.String(http.StatusOK, "pong "+fmt.Sprint(time.Now().Unix()))
	})

	// Listen and Server in 0.0.0.0:8080
	r.Run(":8080")
}
```

Customized Excluded Paths

```go
package main

import (
	"fmt"
	"net/http"
	"time"

	"github.com/hubsync/gzip"
	"github.com/gin-gonic/gin"
)

func main() {
	r := gin.Default()
	r.Use(gzip.Gzip(gzip.DefaultCompression, gzip.WithExcludedPaths([]string{"/api/"})))
	r.GET("/ping", func(c *gin.Context) {
		c.String(http.StatusOK, "pong "+fmt.Sprint(time.Now().Unix()))
	})

	// Listen and Server in 0.0.0.0:8080
	r.Run(":8080")
}
```
