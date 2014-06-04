dns-scripts
===========

### About

Collections of script for managing DNS zone files:

- drev - Generate DNS reverse zone records

### drev

Generate DNS reverse zone records suitable for inclusion in complete
zone file with SOA record.

Usage:

        drev -i IN -o OUT -n NET
         -i IN     input zone
         -o OUT    output reverse zone
         -n NET    network range to filter

Example:

        drev -i example.com -o 168.192.in-addr.arpa.auto -n 192.168.0.0/16
		drev -i example.com -o 0.0.d.f.ip6.arpa.auto -n fd00::/8

Include generated reverse record file like this:

        $TTL 1D
        @       IN      SOA     ns.example.com.    hostmaster.example.com. (
                                2014060403      ; serial
                                1H              ; refresh
                                15              ; update retry
                                14D             ; expiry
                                12H             ; minimum
                                )
        @               IN      NS      ns
        ns              IN      A       192.168.0.100
        $INCLUDE 168.192.in-addr.arpa.auto
