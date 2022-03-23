# rbldnsd
This is a rbldnsd dockerfile that will allow you to configure environmental variables for 'ZONE', 'TYPE' and 'OPTONS'

Where environment Variables could be:
ZONE=blocklist.example.com
TYPE=ip4set
OPTIONS=-e -t 5m

Running this container from Docker could look like

docker run -it --rm -e ZONE=my-blocklist.example.com -e TYPE=ip4set -e VARIABLES="-e -t 5m" -v /some/folder/path/rbldnsd:/var/lib/rbldnsd/:ro smck83/rbldnsd-combined

This image looks for ANY file in /var/lib/rbldnsd that contains a '-' e.g. sample-com and passes it into the ENTRYPOINT

e.g. by running the above, the ENTRYPOINT would look like this where sample-com has been discovered via $(ls /var/lib/rbldnsd/| grep - | tr -s '\n' ',' | rev | cut -c 2- | rev)
/usr/sbin/rbldnsd -b 0.0.0.0 -n -e -t 5m blocklist.example.com:ip4set:sample-com
