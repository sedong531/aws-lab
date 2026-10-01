# 1. 로그/감사 계열 : Cloud Trail / VPC Flow Logs / Access Log(미구현)



# 2. 탐지 계열 : GuardDuty



# 3. 상태/취약점 점검 계열 : Inpector




# 4. 차단/예방 계열 : WAF / 방화벽 / IPS 등




VPC
Subnet
Internet Gateway
Route Table
Security Group

EC2
AMI
Launch Template
Auto Scaling Group
Application Load Balancer
Target Group

RDS
S3

IAM
CloudTrail
CloudWatch
VPC Flow Logs
AWS WAF
Secrets Manager


GuardDuty 미구현

SSM / Inspector / Macie / Security Hub / IDS,IPS대용이름머더라



---

# 1. 인프라스트럭처.md
EC2
RDS
S3
Auto Scaling (Launch Template, AMI도 여기일듯. 타겟그룹도 여기인가)
-> 각 항목별 구축 내용 / 주요 설정 / 검증

# 2. 네트워크.md
VPC
Public / Private Subnet
Route Table
IGW
ALB 
-> 네트워크 흐름, 연결성 검증
NAT 추가 했음 private -> NAT -> 인터넷

# 3. 접근 제어.md
Security Group
IAM
세큐리티 매니저
-> 접근 범위 / 권한 구조, 허용차단 검증

# 4. 웹 보안.md
HTTPS
AWS WAF
-> 적용 정책, 정상 요청/차단 요청 검증

# 5. 로깅 모니터링.md
CloudTrail
CloudWatch
VPC Flow Logs
-> 로그 수집 위치, 실제 이벤트/로그 생성 확인




웹서비스가 어떤 구조로 배치되었는가

외부 요청이 어디를 거쳐 어디까지 가는가

보안/로그 서비스가 주변에서 어떻게 붙는가





메인경로

Internet - WAF - ALB - EC2 - EC2 - RDS


네트워크 구조
VPC (영역은?)
- Public Subnet a, b
- Private Subnet a, b

접근/보안
Security Group
IAM Role
Secrets Manager

로그/모니터링
CloudWatch
CloudTrail
VPC Flow Logs
S3






s3, Secrets manager, CloudTrail, CloudWatch, VPC Flow Logs
-> 넣기.



IAM, Security Group -> 상세문서로 빼기??


1) CloudTrail -> S3

2) S