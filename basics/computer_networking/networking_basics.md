# Computer Networking

This section is used to list some important concepts and commands on computer networking.

## Switching and Routing

* Switch: Switch can only enable communication within a network, which means it can receive packets from a host on the network and deliver it to other systems within the same network.
* Routing: A router helps connect two networks together.
* Gateway: Gateway is a door to th outside world, to the other networks or to the Internet. 

## DNS
* Name Resolution: Translating host names to IP addresses, i.e. process of associating names and IP addresses.
* DNS Server: Domain Name system server which translates domain names into IP addresses.
* Record Types

| Record Type | web-server | Example   | Comments   |
| :-------:   | :---:      | :-------: |  :-------: |
| A      | web-server     | 192.168.1.1 | Stores IP addresses to hostnames |
| AAAA   | web-server     | 2001:xx:xx:xx| Stores IPv6 addresses to host names |
| CNAME  | food.web-server | eat.web-server,hungry.web-server | mapping one name to another name |

## Private IP addreses, NAT, Public IP addresses
###  Private IP address: It is not routable on the Internet.
* 10.0.0.0 to 10.255.255.255
* 172.16.00 to 172.31.255.255
* 192.168.0.0 to 192.168.255.255
### NAT: Network Address Translation. It take a private IP address and translate it to a public IP address.
### Public IP address: It is routable on the Internet.

## Important Commands

* ping: ping can be used to test DNS resolution. For example, ping www.google.com.
* nslookup: query a host name from a DNS server. For example, nslookup www.google.com.
* dig: Another useful tool to list DNS name resolution.
* curl: It stands for "Client URL". curl is a command line tool that enables data transfer over various network protocols.
    * -v: Makes curl verbose during the operation
    ```
    curl -v https://example.com 
    ```
    * -k: Allow curl to work with insecure connections. This option makes curl skip the verification step and proceed without checking.
    ```
    curl -k https://example.com 
    ```
    * -H: Specify an additional header to be sent in the HTTP request. 
      ```
      curl -H "X-First-Name: abc" https://example.com 
      ```
    * Obtain only headers.
    ```
    curl -I https://example.com 
    ```
    * -x or --proxy: Use the specified proxy.
    ```
    curl --proxy http://proxy.example https://example.com
    ```
* nc: Netcat command is a command-line utility for reading and writing data between two computer networks. 
    * The basic syntax for the nc command is:
    ```
    nc [<options>] <host> <port>
    ```
    * some important options are below.
        * -v: Sets verbosity level.
        * -z: Report connection status without establishing a connection.

## References
* https://curl.se/docs/manpage.html
* https://everything.curl.dev/cmdline/options
* https://phoenixnap.com/kb/curl-command
* https://www.computerhope.com/unix/nc.htm
* https://phoenixnap.com/kb/nc-command