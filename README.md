# bwcalc

Network bandwidth/throughput calculator

## Description

Calculate the estimated duration required to move an arbitrary amount of data
given a particular network speed, latency, window size, and MTU.

It should be noted that these will be theoretical minimum durations as it
does not take into account things such as application overhead.

## Usage

    usage: bwcalc [-h] [--data-size BYTES] [--speed LINK_SPEED] [--upload]
                  [--rtt MILLISECONDS] [--mtu BYTES] [--l2-overhead BYTES]
                  [--l3-overhead BYTES] [--rwnd RWND]
    
    Network throughput calculator
    
    optional arguments:
      -h, --help           show this help message and exit
      --data-size BYTES    Size of the data to be transferred
      --speed LINK_SPEED   Link speed of the network [default: 1Gb]
      --upload             Specify that this is an upload (uses tcp_wmem instead
                           of tcp_rmem for rwnd)
      --rtt MILLISECONDS   Round Trip Time (RTT) in milliseconds [default: 10]
      --mtu BYTES          MTU of the path [default: 1500]
      --l2-overhead BYTES  L1/L2 frame overhead in bytes [default: 38]
      --l3-overhead BYTES  L3 TCP/IP overhead in bytes [default: 40]
      --rwnd RWND          TCP window (RWND) size in bytes [default: None]


### --rwnd

The window size will be determined from the local system if --rwnd is not
specified.  This will be combined with --upload to determine if we need
the value from tcp_rmem or tcp_wmem.  This is useful when trying to 
estimate the throughput from a specific system.

### --l3-overhead

This is the size in bytes of the TCP/IP headers.  The default is 40, which
is the typical TCP/IP frame without any additional options.
