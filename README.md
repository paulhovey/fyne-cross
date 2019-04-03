# Fyne Cross Compile Docker Image

This repo contains a Dockerfile for building an image which is used to cross compile [Fyne](https://fyne.io) applications. 

Built on top of [golang-cross](https://hub.docker.com/r/dockercore/golang-cross/), it includes the MinGW compiler for windows, and an OSX SDK, along the Fyne requirements.

Build the image locally using ```docker-compose build linux```

## Usage

Requires a project using go mod support to be in ```src/``` directory.

Cross compiling build can be done using the commands below:

### linux

    docker-compose run --rm linux

### osx

    docker run --rm -ti -v $GOPATH:/go -w /go/src/fyne-example \
        -e CGO_ENABLED=1 -e GOOS=darwin -e CC=o32-clang \
        lucor/fyne-cross \
        bash -c "go get -v ./...; go build -o fyne-example-osx"

### windows

    docker run --rm -ti -v $GOPATH:/go -w /go/src/fyne-example \
        -e CGO_ENABLED=1 -e GOOS=windows -e CC=x86_64-w64-mingw32-gcc \
        lucor/fyne-cross \
        bash -c "go get -v ./...; go build -o fyne-example-windows.exe"
