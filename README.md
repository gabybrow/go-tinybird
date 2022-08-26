# Go-Tinybird

A [Tinybird](https://www.tinybird.co/) module for Go. Why need this module? It provides an easy and standard way of getting data through the Tinybird API.

## Features

- Lightweight and fast.
- Native Go implementation. No C-bindings, just pure Go
- Connection pooling for HTTP.
- Allow [NDJSON](http://ndjson.org/) between tinybird and this module.
- Parallelize HTTP requests.

## Requirements

Go 1.13 or higher. We aim to support the 3 latest versions of Go.

## Installation

Simple install the package to your $GOPATH with the go tool from shell:

```bash
go get -u github.com/the-hotels-network/go-tinybird
```

Make sure Git is installed on your machine and in your system's PATH.

## Quickstart

```
package main

import (
	"fmt"
	"net/http"
	"net/url"
	"os"

	"github.com/the-hotels-network/go-tinybird"
)

func main() {
	params := url.Values{}
	params.Add("start_date", "2022-05-01")
	params.Add("end_date", "2022-05-30")
	params.Add("property_id", "1234")

	req := tinybird.Request{
		Method: http.MethodGet,
		Pipe: tinybird.Pipe{
			Name:       "tinybird_endpoint",
			Parameters: params,
			Workspace: tinybird.Workspace{
				Token: "token-demo",
			},
		},
	}

	err := req.Execute()
	if err != nil {
		fmt.Println(err)
		os.Exit(1)
	}

	res := req.Response
	fmt.Println("Status:", res.Status)
	fmt.Println("Error:", res.Error)
	fmt.Println("Data:", res.Data)
}
```

To see more examples, please go to [this directory](https://github.com/the-hotels-network/go-tinybird/tree/main/example).

## Run the test

```
make tests
```
