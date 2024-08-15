---
layout:     post
title:      Creating a Cross-Platform Command-Line Application in Go
subtitle:   A Simple Guide
date:       2024-08-15
author:     ontheeway01
header-img: img/post-bg-cook.jpg
catalog: true
tags: 
    - GOARCH
    - GOOS
---


Go's standard library provides a rich set of packages that abstract away most of the platform-specific differences, allowing developers to write code that compiles and runs with minimal changes on different operating systems.

In this guide, we'll create a simple "Hello, World!" command-line application that runs on both Windows and Linux. This example will demonstrate the basics of writing cross-platform Go code and building executables for different operating systems.


### Step 0: Setting Up Your Environment

Ensure you have Go installed on your machine. You can download and install Go from the official website: <https://golang.org/dl/>.

### Step 1: Understand Platforms
let's first understand what types of platforms Go can build for and how Go associates these platforms with the environment variables GOOS and GOARCH.

The Go tool has a command that can print out the list of platforms that Go can build for. This list changes with every new Go release, so the combinations discussed here might be different in another version of Go. At the time of writing this tutorial, the Go release version is 1.13.

To find the applicable platforms, execute the following command:

```bash
go tool dist list
```

You will receive output similar to this:

```plaintext
aix/ppc64        freebsd/amd64   linux/mipsle   openbsd/386
android/386      freebsd/arm     linux/ppc64    openbsd/amd64
android/amd64    illumos/amd64   linux/ppc64le  openbsd/arm
android/arm      js/wasm         linux/s390x    openbsd/arm64
android/arm64    linux/386       nacl/386       plan9/386
darwin/386       linux/amd64     nacl/amd64p32  plan9/amd64
darwin/amd64     linux/arm       nacl/arm       plan9/arm
darwin/arm       linux/arm64     netbsd/386     solaris/amd64
darwin/arm64     linux/mips      netbsd/amd64   windows/386
dragonfly/amd64  linux/mips64    netbsd/arm     windows/amd64
freebsd/386      linux/mips64le  netbsd/arm64   windows/arm
```

The output is a list of key-value pairs separated by slashes. 
1. The first part of the key-value pair, before the slash, is the operating system. In Go, these operating systems will be the values of the environment variable **GOOS**, representing Go Operation System.
2. The second part, after the slash, is the architecture. As mentioned earlier, these are all possible values for the environment variable **GOARCH**.

### Step 2: Creating Your Application

1. **Create a new directory** for your project and navigate into it:
   ```bash
   mkdir hello
   cd hello
   ```

2. **Create a new Go file** named `main.go`:
   ```bash
   touch main.go
   ```

3. **Edit `main.go`** with your favorite text editor or IDE and add the following code:

   ```go
   package main

   import (
       "fmt"
       "os"
   )

   func main() {
       // Detect the operating system
       if os.Getenv("GOOS") == "windows" {
           fmt.Println("Hello, Windows!")
       } else {
           fmt.Println("Hello, World!")
       }
   }
   ```

   This code checks the `GOOS` environment variable to determine the operating system. While not strictly necessary for writing cross-platform code, it demonstrates how to conditionally execute code based on the platform.

### Step 3: Building and Running Your Application

1. **Build your application** for different platforms. Open a terminal or command prompt and run the following commands:

   - For Windows:
     ```bash
     GOOS=windows GOARCH=amd64 go build -o hello.windows.exe main.go
     ```

   - For Linux:
     ```bash
     GOOS=linux GOARCH=amd64 go build -o hello.linux main.go
     ```

   These commands set the `GOOS` and `GOARCH` environment variables to specify the target operating system and architecture, then build the application.

2. **Run your application** on each platform by executing the appropriate binary:

   - On Windows, run:
     ```bash
     ./hello.windows.exe
     ```

   - On Linux, run:
     ```bash
     ./hello.linux
     ```

### Conclusion

You have now created a simple cross-platform command-line application in Go. By leveraging Go's standard library and conditional compilation techniques, you can write code that runs seamlessly on multiple operating systems. Remember, Go's philosophy emphasizes portability, so most Go code will work across platforms with little to no modification.
