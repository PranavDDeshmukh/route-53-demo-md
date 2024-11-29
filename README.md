# AWS Route 53 Routing Policy
### AWS Route 53 routing policy determines how AWS would respond to the DNS queries and provides multiple routing policy options.

## 1:Simple Routing Policy
- Simple routing policy is a simple round-robin policy and can be applied when there is a single resource doing the function for the domain e.g. web server that serves content for the website.
- Simple routing helps configure standard DNS records, with no special Route 53 routing such as weighted or latency.
- Route 53 responds to the DNS queries based on the values in the resource record set e.g. IP address in an A record.
- Simple routing does not allow the creation of multiple records with the same name and type, but multiple values can be specified in the same record, such as multiple IP addresses.

## 2:Weighted Routing Policy
- Weighted routing policy helps route traffic to different resources in specified proportions (weights) e.g., 75% to one server and 25% to the other during a pilot release
- Weights can be assigned between any number from 0 to 255 inclusive.
- Weighted routing policy can be applied when there are multiple resources that perform the same function e.g., webservers serving the same site
- Weighted resource record sets allow associating multiple resources with a single DNS name.
- To create a group of weighted resource record sets, two or more resource record sets can be created that has the same combination of DNS name and type, and each resource record set is assigned a unique identifier and a relative weight.

## 3:Latency-based Routing (LBR) Policy
- Latency-based Routing Policy helps respond to the DNS query based on which data center gives the user the lowest network latency.
- Latency-based routing policy can be used when there are multiple resources performing the same function and Route 53 needs to be configured to respond to the DNS queries with the resources that provide the fastest response with the lowest latency.
- A latency resource record set can be created for the EC2 resource in each region that hosts the application. When Route 53 receives a query for the corresponding domain, it selects the latency resource record set for the EC2 region that gives the user the lowest latency. Route 53 then responds with the value associated with that resource record set for e.g., you might have web servers for example.com in the EC2 data centers in Ireland and in Tokyo. When a user browses example.com from Singapore, Route 53 will pick up the data center (Tokyo) which has the lowest latency from the user’s location
- Latency between hosts on the Internet can change over time as a result of changes in network connectivity and routing. Latency-based routing is based on latency measurements performed over a period of time, and the measurements reflect these changes for e.g. if the latency from the user in Singapore to Ireland improves, the user can be routed to Ireland
- Latency-based routing cannot guarantee users from the same geographic will be served from the same location for any compliance reason

## 4:Failover Routing Policy
- Failover routing policy allows active-passive failover configuration, in which one resource (primary) takes all traffic when it’s healthy and the other resource (secondary) takes all traffic when the first isn’t healthy.
- Route 53 health checking agents will monitor each location/endpoint of the application to determine its availability.
- Failover routing policy is applicable for Public hosted zones only.

## 5:Geolocation Routing Policy
- Geolocation routing policy helps respond to DNS queries based on the geographic location of the users i.e. location from which the DNS queries originate.
- Geolocation works by mapping IP addresses to locations, which might not be mapped to an exact geographic location.
- A default resource record set can be created to handle these queries and also the ones which do not have an explicit record set created.
