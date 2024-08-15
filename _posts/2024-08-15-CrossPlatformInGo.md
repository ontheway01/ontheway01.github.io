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

### Step 1: Setting Up Your Environment

Ensure you have Go installed on your machine. You can download and install Go from the official website: <https://golang.org/dl/>.

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
