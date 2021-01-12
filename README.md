# psend

Utility to construct and send packets for network daemon testing

## Quick start

The `psend.py` Python program reads a file (by default `psend.txt`) and builds a network packet
and then sends it to a network host on a specified port. It can optionally wait for a response
packet and display the bytes in the response packet.

For example create a `psend.txt` file with the following content:

```
host 10.1.1.13
port 69
0x0001 'file' 0 'octet' 0
show
send
receive
```

Change the IPx4 address `10.1.1.13` to the IP address of a TFTP server
on your network.

Now run:

```
python psend.txt
```

You might well get output similar to:

```
> 0000 : 00 01 66 69 6C 65 00 6F 63 74 65 74 00             ??file?octet?
< 0000 : 00 05 00 01 46 69 6C 65 20 6E 6F 74 20 66 6F 75    ????File not fou
< 0010 : 6E 64 00                                           nd?
```

What has happened here is that a TFTP read request for a file called `file` to be transferred in
binary format has been sent to a host with IP address `10.1.1.5` on the well known TCP/IP port
number `69` for TFTP requests. The response packet indicates that the file called `file` was
not found on the TFTP server.

The output packet is shown as:

```
> 0000 : 00 01 66 69 6C 65 00 6F 63 74 65 74 00             ??file?octet?
```

and the response packet is show as:

```
< 0000 : 00 05 00 01 46 69 6C 65 20 6E 6F 74 20 66 6F 75    ????File not fou
< 0010 : 6E 64 00                                           nd?
```




## Prerequsites

You will need:

+ UNIX/Linux or Windows
+ Python 3 (tested on version 3.7.2)

## Command line option `-f` / `--file`

The optional command line option `--file` (short form `-f`) can be used to specify a
different packet specification file. For example if the packet specification is in a file called
`px2firmware.txt` then run the `psend.py` program as follows:

```
python psend.py --file px2firmware.txt
```

or with the short form:

```
python psend.py -f px2firmware.txt
```




----------------------------------------------------------------

End of README.md - sversion 0.1.0, fversion 002, 12-january-2021
