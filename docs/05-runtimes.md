---
title: Runtimes
---

Up supports a number of interpreted languages, and virtually any language which can be compiled to a binary such as Golang. Up does its best to provide idiomatic and useful out-of-the-box experiences tailored to each language. Currently first-class support is provided for:

- Python
- Golang
- Node.js
- Crystal
- Java
- Static sites

## Node.js

When a `package.json` file is detected, Node.js is the assumed runtime. By default the latest version supported by Lambda is used (6.10). If you'd like to deploy other versions of Node you may want to consider using the [Node binaries](https://github.com/apex/up-examples/tree/master/oss/node-8).

The `build` hook becomes:

```
$ npm run build
```

The server run by the proxy becomes:

```
$ npm start
```

## Python

When requirements.txt is present the build command becomes:

```
$ mkdir -p .pypath/ && pip install -r requirements.txt -t .pypath/
```

The server run by the proxy becomes:

```
$ python app.py
```

## Golang

When a `main.go` file is detected, Golang is the assumed runtime.

The `build` hook becomes:

```
$ GOOS=linux GOARCH=amd64 go build -o server *.go
```

The `clean` hook becomes:

```
$ rm server
```

## Crystal

When a `main.cr` file is detected, Crystal is the assumed runtime. Note that this runtime requires Docker to be installed.

The `build` hook becomes:

```
$ docker run --rm -v $(PWD):/src -w /src tjholowaychuk/up-crystal crystal build --link-flags -static -o server main.cr
```

The `clean` hook becomes:

```
$ rm server
```

## Java

When a `build.gradle` file is detected, Gradle is assumed, otherwise if `pom.xml` is found then Maven is used.

## Static

When an `index.html` file is detected the project is assumed to be static.
