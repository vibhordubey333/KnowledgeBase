1. Compiling with flags
     ```
     env GOOS=linux GOARCH=amd64 go build -o output/main

     we are setting the environment variable

    GOOS=linux, implying build the executable for linux OS
    GOARCH=amd64, implying that the executable is build for execution in amd64 cpu architechture
    -o <path/file> is the output file name

     ```
