Topics to be covered for System Design
1. CAP theorem
  In a distributed computer system, you can only support two of the following guarantees:

  Consistency - Every read receives the most recent write or an error
  Availability - Every request receives a response, without guarantee that it contains the most recent version of the information
  Partition Tolerance - The system continues to operate despite arbitrary partitioning due to network failures
  Networks aren't reliable, so you'll need to support partition tolerance. You'll need to make a software tradeoff between consistency and availability.

   http://ksat.me/a-plain-english-introduction-to-cap-theorem, https://www.youtube.com/watch?v=k-Yaq8AHlFA&ab_channel=DistributedSystemsCourse

  Consistency patterns
    With multiple copies of the same data, we are faced with options on how to synchronize them so clients have a consistent view of the data. 
    Recall the definition of consistency from the CAP theorem - Every read receives the most recent write or an error.
    
    Weak consistency
    After a write, reads may or may not see it. A best effort approach is taken. Example Video Call or chat
    Eventual consistency
    After a write, reads will eventually see it (typically within milliseconds). Data is replicated asynchronously.
    This approach is seen in systems such as DNS and email. Eventual consistency works well in highly available systems.
    Strong consistency
    After a write, reads will see it. Data is replicated synchronously.
    This approach is seen in file systems and RDBMSes. Strong consistency works well in systems that need transactions.

  Availability patterns
    There are two complementary patterns to support high availability: fail-over and replication.
    Fail-over
      Active-passive
        With active-passive fail-over, heartbeats are sent between the active and the passive server on standby. 
        If the heartbeat is interrupted, the passive server takes over the active's IP address and resumes service.  
        Only the active server handles traffic. Active-passive failover can also be referred to as master-slave failover.

      Active-active
        In active-active, both servers are managing traffic, spreading the load between them.
        If the servers are public-facing, the DNS would need to know about the public IPs of both servers.
        If the servers are internal-facing, application logic would need to know about both servers.
        Active-active failover can also be referred to as master-master failover.
    
    Replication
      Master-slave 
      master-master

2. Vertical scaling vs Horizontal scaling
   https://www.cloudzero.com/blog/horizontal-vs-vertical-scaling/#:~:text=While%20horizontal%20scaling%20refers%20to,%2C%20storage%2C%20or%20network%20speed.

3. Performance vs scalability
   A service is scalable if it results in increased performance in a manner proportional to resources added. Generally, increasing performance means serving more units of work, but it can also be to handle larger units of work, such as when datasets grow.1

Another way to look at performance vs scalability:
If you have a performance problem, your system is slow for a single user.
If you have a scalability problem, your system is fast for a single user but slow under heavy load.

4. Latency vs throughput
  Latency is the time to perform some action or to produce some result.
  Throughput is the number of such actions or results per unit of time.
  
  Generally, you should aim for maximal throughput with acceptable latency.
  https://community.cadence.com/cadence_blogs_8/b/fv/posts/understanding-latency-vs-throughput

5. Load balancing
  A load balancer is a software or hardware device that keeps any one server from becoming overloaded.
  A load balancing algorithm is the logic that a load balancer uses to distribute network traffic between servers.

    Dynamic load balancing algorithms
     Least connection: Checks which servers have the fewest connections open at the time and sends traffic to those servers.
     Weighted least connection: Gives administrators the ability to assign different weights to each server, assuming that some servers can handle more connections than others.
     Weighted response time: Averages the response time of each server, and combines that with the number of connections each server has open to determine where to send traffic.
       By sending traffic to the servers with the quickest response time, the algorithm ensures faster service for users.
     Resource-based: Distributes load based on what resources each server has available at the time.
       Specialized software (called an "agent") running on each server measures that server's available CPU and memory,
       and the load balancer queries the agent before distributing traffic to that server.

    Static load balancing algorithms
     Round robin: Round robin load balancing distributes traffic to a list of servers in rotation using the Domain Name System (DNS).
       An authoritative nameserver will have a list of different A records for a domain and provides a different one in response to each DNS query.
     Weighted round robin: Allows an administrator to assign different weights to each server.
       Servers deemed able to handle more traffic will receive slightly more. Weighting can be configured within DNS records.
     IP hash: Combines incoming traffic's source and destination IP addresses and uses a mathematical function to convert it into a hash.
       Based on the hash, the connection is assigned to a specific server.

6. Database replication
   https://estuary.dev/data-replication-strategies/

7. Database Sharding vs. partitioning
   https://planetscale.com/learn/articles/sharding-vs-partitioning-whats-the-difference
   https://www.mongodb.com/basics/sharding

8. How DNS works
    https://cloudinfrastructureservices.co.uk/what-is-dns-hierarchy/

9. How CDN Works
    https://www.imperva.com/learn/performance/what-is-cdn-how-it-works
