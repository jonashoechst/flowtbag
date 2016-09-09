## License

Copyright 2011 Daniel Arndt

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

Author: 
    Daniel Arndt <danielarndt@gmail.com> (http://dan.arndt.ca)

## Purpose

The purpose of this program is to calculate flow statistics from a given 
capture file. Flowtbag was designed with offline processing as the primary
focus.

## Requirements

To run the executable, you will need libpcap installed. On a debian based
system, the following command will install the appropriate library:

    apt-get install libpcap

Other distributions will likely have a similar package name.

To compile from source, you'll need a Go compiler, libpcap headers, and
gopcap.

### Go compiler:

Please see http://golang.org/doc/install.html

### libpcap headers:

On a debian based system, you can execute the following command:

    apt-get install libpcap-dev

Other distributions will likely have a similar package name. It is
important that if you are compiling the program from source, you install
the developement headers.

## Compilation

Once libpcap is installed, `go` will install the necessary go dependencies. Just
build and install using go.

   go get github.com/danielarndt/flowtbag

## Usage

The program's usage is currently left undocumented due to the rapidly
changing functionality of the program in its early stages. However, if you
run flowtbag, the currently implemented options should be displayed. A
typical use case might look something like:

    $ ./flowtbag test.cap > test.out

## Output

Flowtbag currently has two seperate channels for output. To stdout, a stream
of comma seperated values is output. Line by line, these represent the flows
in the capture. The features output are given, in order, in section 4.1. The
second output channel is stderr. This is where reports, as well as any
debugging information is displayed. This allows the user to redirect output
to a text file, and still receive updates as the program runs. The setup for
output is likely to change in future versions of Flowtbag when a better
system is designed.

### Features

    srcip STRING                source IPv4 (sent SYN) 
    srcport NUMERIC             source port
    dstip STRING                destination IPv4
    dstport NUMERIC             destination Port 
    proto NUMERIC               protocol in IP Header: 6: TCP, 17: UDP
    total_fpackets NUMERIC      forward packets count
    total_fvolume NUMERIC       forward packets volume
    total_bpackets NUMERIC      back packets count
    total_bvolume NUMERIC       back packets sum
    min_fpktl NUMERIC           forward packets length: min
    mean_fpktl NUMERIC          forward packets length: mean
    max_fpktl NUMERIC           forward packets length: max
    std_fpktl NUMERIC           forward packets length: standard deviation
    min_bpktl NUMERIC           back packets length: min
    mean_bpktl NUMERIC          back packets length: mean
    max_bpktl NUMERIC           back packets length: max
    std_bpktl NUMERIC           back packets length: standard deviation
    min_fiat NUMERIC            send interarrival time: min
    mean_fiat NUMERIC           send interarrival time: mean
    max_fiat NUMERIC            send interarrival time: max
    std_fiat NUMERIC            send interarrival time: standard deviation
    min_biat NUMERIC            received inter arrival time: min
    mean_biat NUMERIC           received inter arrival time: mean
    max_biat NUMERIC            received inter arrival time: max
    std_biat NUMERIC            received inter arrival time: standard deviation
    duration NUMERIC            connection duration (syn to fin)
    min_active NUMERIC          active connection phases: min
    mean_active NUMERIC         active connection phases: mean
    max_active NUMERIC          active connection phases: max
    std_active NUMERIC          active connection phases: standard deviation
    min_idle NUMERIC            idle connection phases: min
    mean_idle NUMERIC           idle connection phases: mean
    max_idle NUMERIC            idle connection phases: max
    std_idle NUMERIC            idle connection phases: standard deviation
    sflow_fpackets NUMERIC      forward subflows mean packet count 
    sflow_fbytes NUMERIC        forward subflows mean packet bytes 
    sflow_bpackets NUMERIC      back subflows mean packet count 
    sflow_bbytes NUMERIC        back subflows mean packet bytes 
    fpsh_cnt NUMERIC            forward push (PSH) count
    bpsh_cnt NUMERIC            back push count
    furg_cnt NUMERIC            forward urgent (URG) count
    burg_cnt NUMERIC            back urgent count
    total_fhlen NUMERIC         forward packets volume (summed header length)
    total_bhlen NUMERIC         back packets volume (summed header length)
    dscp NUMERIC                differentiated services field
