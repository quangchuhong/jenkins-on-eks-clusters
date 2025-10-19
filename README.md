[Users]
  │
  ▼ HTTPS/SSL
[Application Load Balancer (ALB)] → Health Check, SSL Termination
  │
  ▼
[Amazon EKS Cluster]
  ├── [Jenkins Controller Pod (Single Instance)] → Deploy trên một AZ
  │    ├── [Persistent Volume (EBS)] → Local storage cho /var/jenkins_home (config, plugins, jobs)
  │    └── [IAM Role (IRSA)] → Truy cập AWS resources (ECR, S3, v.v.)
  │
  ├── [Jenkins Agent Pods (Dynamic Scaling)] → Chạy trên nhiều AZ
  │    ├── [Kubernetes Pod Templates] → Cấu hình agent theo nhu cầu
  │    └── [IAM Role (IRSA)] → Truy cập AWS resources (ECR, S3, v.v.)
  │
  ▼
[Amazon ECR] → Lưu trữ Docker images cho Jenkins agents
  │
  ▼
[Amazon S3] → Lưu trữ build artifacts và logs
  │
  ▼
[Backup & Monitoring]
  ├── AWS Backup (EBS, S3)
  └── Prometheus/Grafana → Giám sát hiệu năng
