# go-tomcat-mgmt-scanner

[![baby-gopher](https://raw.githubusercontent.com/drnic/babygopher-site/gh-pages/images/babygopher-logo-small.png)](http://www.babygopher.org)

A simple scanner to find and brute force tomcat manager logins.

This is just a toy project to learn and get used to golang, feedback is appreciated!

Current project version: 1.0 

# About

A simple brute force scanner that tries to identify tomcat manager applications. If such a manager is found, it tries to find valid login credentials by trying common combinations.
The initial wordlists for credential brute forcing are those from Metasploit. The scanner supports userpass files containing `<user>:<password>` entries and files containing solely usernames or passwords which are tried in every possible combination. **There is currently no logic to check if found applications are actually Tomcat manager login pages**. This means that the scanner may also be used to brute force any HTTP auth.

# Build

```
$ go get -u https://github.com/edermi/go-tomcat-mgmt-scanner
$ make # builds for some architectures/platforms and drops binaries to build/

# or

$ env GOOS=linux GOARCH=arm GOARM=7 go build # Raspberry Pi
$ env GOOS=windows GOARCH=amd64 go build # x64 Windows
$ env GOOS=linux GOARCH=amd64 go build # x64 linux
$ ....
```

# Run

```
./go-tomcat-mgmt-scanner -help
Usage of ./go-tomcat-mgmt-scanner:
  -concurrency uint
    	Concurrent Goroutines to use. Due to kernel limitations on linux, it should not be more than 'ulimit -n / 7'. (default 100)
  -debug
    	Enable debugging output.
  -managerpath string
    	Manager path. (default "/manager/html")
  -ports string
    	Comma separated list of target ports. (default "8080,8443,80,443,8000,8888")
  -randomize
    	Randomize the order that IP:Port is accessed. (default true)
  -target string
    	The target network range in CIDR notation, e.g. 10.10.10.0/24
```

# License

See LICENSE. User and password lists are taken from Metasploit project which are licensed BSD 3-clause.

# DISCLAIMER

The usual stuff. Don't do bad things and only use it against targets you are permitted to attack. You are on your own if something breaks.