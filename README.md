[![Build Status](https://travis-ci.org/taganaka/SpeedTest.svg?branch=master)](https://travis-ci.org/taganaka/SpeedTest)

# SpeedTest++

Yet another unofficial speedtest.net client cli interface

It supports the new (undocumented) raw TCP protocol for better accuracy.

## Features

1. Best server discovery based on speed and distance from you.

2. Line type discovery to select the best test profile based on your line speed.

3. Aggressive multi-threading program in order to saturate your bandwidth quickly.

4. Test supported: Ping / Jitter / Download speed / Upload speed / Packet loss (UDP).

5. Provide a URL to the speedtest.net share results image using option --share

## Installation

### Requirements

1. A modern C++ compiler
2. cmake
3. libcurl
4. libssl
5. libxml2

### On Mac OS X

```
$ brew install cmake
$ cd cmake_build
$ cmake -DCMAKE_BUILD_TYPE=Release ..
$ make install
```

### On Ubuntu/Debian

```
$ sudo apt-get install build-essential libcurl4-openssl-dev libxml2-dev libssl-dev cmake
$ git clone https://github.com/taganaka/SpeedTest
$ cd SpeedTest
$ cmake -DCMAKE_BUILD_TYPE=Release .
$ sudo make install
```

### On OpenSuse

```
$ sudo zypper install cmake gcc-c++ libcurl-devel libxml2-devel libopenssl-devel git
$ git clone https://github.com/taganaka/SpeedTest
$ cd SpeedTest
$ cmake -DCMAKE_BUILD_TYPE=Release .
$ sudo make install
```

## IP lookup API key (ipapi.is)

SpeedTest++ uses [ipapi.is](https://ipapi.is/) to find your public IP and location.
Anonymous requests are heavily rate limited, which shows up as
`Unable to retrieve your IP info. Try again later`. A free API key
(1000 requests/day) avoids this. The key is taken from the first of:

1. `--ipapi-key KEY`
2. `--ipapi-key-file PATH` (first non-empty line of the file)
3. the `IPAPI_KEY` environment variable
4. `~/.config/SpeedTest/ipapi.key`, if it exists

A key file is preferable to `--ipapi-key` for scheduled runs, since command-line
arguments are visible to other users in `ps`.

## Usage

```
$ ./SpeedTest --help
SpeedTest++ version 1.15
Speedtest.net command line interface
Info: https://github.com/taganaka/SpeedTest
Fixed: https://github.com/gglluukk/SpeedTest
Author: Francesco Laurita <francesco.laurita@gmail.com>

Usage: ./SpeedTest  [--latency] [--quality] [--download] [--upload] [--share] [--help]
      [--test-server host:port] [--output verbose|text|json]
      [--ipapi-key KEY | --ipapi-key-file PATH]
optional arguments:
  --help                      Show this message and exit
  --latency                   Perform latency test only
  --quality                   Perform quality test only. It includes latency test
  --download                  Perform download test only. It includes latency test
  --upload                    Perform upload test only. It includes latency test
  --share                     Generate and provide a URL to the speedtest.net share results image
  --insecure                  Skip SSL certificate verify (Useful for Embedded devices)
  --test-server host:port     Run speed test against a specific server
  --quality-server host:port  Run line quality test against a specific server
  --output verbose|text|json  Set output type. Default: verbose
  --ipapi-key KEY             ipapi.is API key used for the IP/location lookup
  --ipapi-key-file PATH       Read the ipapi.is API key from a file
                              (also: $IPAPI_KEY, or ~/.config/SpeedTest/ipapi.key)
$
```

See [IP lookup API key (ipapi.is)](#ip-lookup-api-key-ipapiis) for how the API key is resolved.

## License

SpeedTest++ is available as open source program under the terms of the [MIT License](http://opensource.org/licenses/MIT).
