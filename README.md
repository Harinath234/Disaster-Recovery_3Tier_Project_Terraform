🚀 Disaster Recovery 3-Tier Architecture using Terraform (AWS)

This project demonstrates a production-grade 3-tier architecture with Disaster Recovery (DR) on AWS using Terraform.

It is designed to ensure high availability, fault tolerance, and business continuity using a multi-region failover architecture with DNS-based traffic routing.

🏗️ Architecture Overview

This solution follows a 3-tier architecture pattern:

🔹 Web Layer (Frontend)

EC2 instances behind Application Load Balancer (ALB)

Public access via Route53

Auto Scaling enabled

🔹 Application Layer (Backend)

Private EC2 instances

Internal communication via backend ALB

Handles business logic

🔹 Database Layer

Primary RDS (MySQL) in us-east-1 (N. Virginia)

Cross-region Read Replica in us-west-2 (Oregon)

🌍 Multi-Region Disaster Recovery Design
Component	Primary (us-east-1)	Secondary (us-west-2)
VPC	✅	✅
ALB	✅	✅
EC2 (ASG)	✅	✅
RDS	Primary	Read Replica
AMI Backup	❌	✅
Route53	Primary Routing	Failover Target
🌐 Route53 Failover Strategy (Key Highlight 🔥)

This architecture uses DNS-based failover routing:

Primary traffic goes to N. Virginia (us-east-1)

Secondary region (Oregon - us-west-2) acts as standby

In case of failure, Route53 redirects traffic automatically

🔁 Traffic Flow

User hits application domain

Route53 routes traffic to Primary ALB (us-east-1)

If health check fails:
👉 Traffic is redirected to
