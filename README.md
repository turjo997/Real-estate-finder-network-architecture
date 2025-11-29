
# Real Estate Finder - Network Architecture

A network architecture for a platform that will serve as a real estate finder. People will come and search for houses, bid on them, chat with the buyer/seller. The platform will fetch data from many 3rd party services for different countries and cities.

## Assumptions

### 1. High availability is mandatory
The platform must survive the failure of a single Availability Zone or even an entire Region.

### 2. A secondary Region is required for failover
If Region A goes down, Region B must take over with minimal downtime.

### 3. Applications require separation of concerns
Web tier must stay public and app tier must be private for security and compliance.

### 5. Databases require both local HA and cross-region failover
Hence: primary + standby (same region) and replication across regions.

### 6. Outbound internet access from private subnets must be controlled
NAT Gateways in public subnets serve this purpose.

### 7. On-premise offices must connect securely
This requires both:

Client-to-Site VPN for developers/ remote workers

Site-to-Site VPN for the office router

### 8. The platform must be reachable via a custom domain name
Route 53 manages DNS in both Regions.

### 9. Autoscaling is required for unpredictable traffic patterns
Load balancers must distribute traffic across EC2 instances automatically.

### 10. Security boundaries must be strict
Public resources are only for load balancing and NAT and everything else stays in private subnets.

