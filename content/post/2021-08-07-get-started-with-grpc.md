---
title: Get started with gRPC
date: 2021-08-07
tags: [grpc, go]
---

<!-- ToC -->
<!--  - Introduction to gRPC -->
<!--  - Benefits -->
<!--  - Four types of API in gRPC -->
<!--  - Installation for gRPC-Go -->
<!--  - Generate code -->
<!--  - gRPC Boilerplate code -->

gRPC is a Remote Procedure Call (RPC) framework defined on
[grpc.io](https://grpc.io) as:

> gRPC is a modern open source high performance Remote Procedure Call
> (RPC) framework that can run in any environment. It can efficiently
> connect services in and across data centers with pluggable support
> for load balancing, tracing, health checking and authentication. It
> is also applicable in last mile of distributed computing to connect
> devices, mobile applications and browsers to backend services.

gRPC is the framework for microservices exchanging information over
the network. Unlike REST API, gRPC uses protocol buffers for
representing data.

gRPC and protocol buffer has benefits over the REST:

- Binary format data transfer through the wire.
- Uses HTTP/2 protocol, [Compare HTTP/1.1 vs HTTP/2
  performance](https://imagekit.io/blog/http2-vs-http1-performance/).
- Language independent, supports 11 programming languages.
- Supports bidirectional streaming.

There are four type of gRPC APIs:

  1. Unary
  2. Server streaming
  3. Client streaming
  4. Bidirectional streaming

We will discuss about using gRPC protocol in Go language in this blog
post. But the gRPC is programming language agnostic protocol (fully?
not sure yet).

## Install gRPC-Go

You must install following binaries on your machine, and they should
be executable in your project directory.  Add path to the `$PATH`
system variable, if you are using GNU Linux OS.

  1. [Go](https://golang.org/doc/install)
  2. [protoc](https://grpc.io/docs/protoc-installation/)
  3. Go plugins for the protocol compiler:
     - [protoc-gen-go](https://pkg.go.dev/google.golang.org/protobuf/cmd/protoc-gen-go)
     - [protoc-gen-go-grpc](https://pkg.go.dev/google.golang.org/grpc/cmd/protoc-gen-go-grpc)
     
The following versions are installed on my machine at a time of
writing this post:

```
$ go version
go version go1.16.5 linux/amd64

$ protoc --version
libprotoc 3.17.3

$ protoc-gen-go --version
protoc-gen-go v1.27.1

$ protoc-gen-go-grpc --version
protoc-gen-go-grpc 1.1.0
```

To install `grpc-go` package, run following command in project
directory:

```
go get -u google.golang.org/grpc
```

Installing gRPC Go binaries is a one time procedure. That's it, we are
ready to generate gRPC Go code.

## Generate code

Let's consider following proto buffer file as an example:

```
// greet.proto

syntax = "proto3";

package greetpb;
option go_package="github.com/akshay196/grpc-demo/greetpb";

message GreetRequest {
  string name = 1;
}

message GreetResponse {
  string result = 1;
}

service GreetService{
  rpc Greet(GreetRequest) returns (GreetResponse) {};
}
```

go_package is the "greetpb" package path containing .proto file and
generated pb and gRPC code files.

There is single rpc service `Greet` defined in the above code. It
requests `GreetRequest` message and response with `GreetResponse`
message.

To generate code run following command:

```
protoc --go_out=. --go_opt=paths=source_relative \
       --go-grpc_out=. --go-grpc_opt=paths=source_relative \
       path/to/greet.proto
```

It generates files named 'greet.pb.go' and 'greet_grpc.pb.go' in the
directory containing 'greet.proto' file.

Every time you change something in .proto file, execute this command
to generate code.


## Use generated code in our project

```go
// server.go

// Import go_package which is 'greetpb' as defined in the proto file.

type srv struct {
    // implement GreetService service.
}

// Greet rpc handler accepts GreetRequest and returns GreetResponse
func (*srv) Greet(c context.Context, req *greetpb.GreetRequest) (*greetpb.GreetResponse, error) {
    // Logic
    return res, nil
}

func main() {
    lis, err := net.Listen("tcp", "0.0.0.0:50051")
    
    // Create a gRPC server
    s := grpc.NewServer()

    // Register a service.
    // srv is the server API for "GreetService" service.
    greetpb.RegisterGreetServiceServer(s, &srv{})
    
    // Serve accepts incoming connections on a listener lis.
    err := s.Serve(lis)
}
```

Now let's understand the gRPC client code:

```go
// client.go

func main() {
    // Create a client connection.
    // Default grpc runs with SSL connection.
    cc, err := grpc.Dial("serverAddress:50051", grpc.WithInsecure)
    defer cc.Close()
    
    c := greetpb.NewGreetServiceClient(cc)
    
    // Create request data
    req := &greetpb.GreetRequest{
        Name: "John",
    }
    
    // Call Greet rpc service.
    // res is the response from the gRPC server in GreetResponse format.
    res, err := c.Greet(context.Background(), req)
    
    // check whether error nil or not.
    
    fmt.Printf("Response from Greet: %s", res.Result)
}
```

Try running server and client written in different language.
