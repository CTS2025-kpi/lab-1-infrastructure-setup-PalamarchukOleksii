# 8. Calculate monthly budget for lab 2, assuming there will be only 2 shards.

**Region:** Europe (Frankfurt)  
**Estimated Monthly Cost:** ~$130/month

| Component | Quantity | Unit Price | Monthly Cost | Calculation Notes |
|-----------|----------|------------|--------------|-------------------|
| **VPC** | 1 | Free | $0 | VPC itself has no charge |
| **Subnets** | 4 (2 public, 2 private) | Free | $0 | No charge for subnet creation |
| **Internet Gateway (IGW)** | 1 | Free | $0 | No charge for IGW itself, only data transfer |
| **IAM Users/Roles/Policies** | ~5 | Free | $0 | IAM service is always free |
| **EC2 Instances (t3.small)** | 3 | ~$15/instance | ~$45 | 730 hours × $0.0208/hour × 3 instances |
| **NAT Gateway** | 1 | ~$33 base | ~$33 | 730 hours × $0.045/hour + data processing |
| **EBS Storage (gp3)** | 90 GB | $0.08/GB | ~$7 | 30 GB per instance × 3 instances |
| **EBS Snapshots** | Daily | varies | ~$20 | 2 snapshots/day × 3 GB × 30 days × $0.05/GB |
| **Data Transfer OUT** | 10 GB | $0.09/GB | ~$1 | Outbound internet traffic |
| **Data Transfer Intra-Region** | 15 GB | $0.01/GB | ~$0.15 | Cross-AZ traffic between services |
| **Application Load Balancer** | 1 | ~$22 | ~$22 | $16.43 fixed + ~$2-5 LCU charges |
| **CloudWatch Metrics** | 20 | $0.30/metric | ~$3 | 10 free + 10 paid custom metrics |
| **CloudWatch Logs** | 2 GB | varies | ~$0.50 | First 5 GB ingestion free, storage $0.03/GB |
| **CloudWatch Alarms** | 3 | free | $0 | First 10 alarms included in free tier |
| | | **TOTAL:** | **~$130** | |

## Notes

- **Free AWS Components:** VPC, Subnets, IGW, Route Tables, Security Groups, IAM (all management)
- **EC2:** Using 1-year reserved instances saves ~30% vs on-demand
- **NAT Gateway:** Most expensive single component; required for private subnets internet access
- **Snapshots:** Can reduce frequency to save ~$15/month
- **ALB:** Optional - can skip and save $22/month by using direct IPs
- **Free tier:** CloudWatch, data transfer (first 100 GB OUT), and basic monitoring included