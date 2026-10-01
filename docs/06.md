RDS
mysql로 만듦.



IAM
aws-lab-admin 사용자 만듬
aws-lab-admins 그룹 (policy는 administrator) 만듬


S3
Bucket 만들었음




CloudTrail
어... 쉽게 만들었고.. S3만 기본으로 지정한거를 우리가 만든거로 바꿧고, log file validation을 켜서 cloudtrail 로그 무결성 검증 기능을 활성화시켰음.

CloudWatch
cpu threshold 80% 이상이 5분간격으로 두번이상 반복되면 
sedong531@gmail.com 메일이 오도록 설정함.

대시보드도 만들었음. 커스텀으루. 
EC2와 관련된거 3개랑 RDS관련된거 3개 넣어놧음.


























9/28 저녘 기준
앞으로 추가로 구현할 것.






EC2를 추가하고, ALB로 고가용성/부하분산 직접 구현
-> 1번 포폴에서 고가용성/부하분산은 구현되지 않았었음. 이걸 여기선 쉽게 ㄱㄱ가능.

AWS WAF
-> ALB 앞에 붙여 웹 공격 필터링.

Auto Scaling
-> 부하에 따라 EC2 대수 증감.
-> 1번 포폴에서 고가용성/부하분산을 클라우드에 의한 탄력성으로 해결하는 모습 보여주기 가능.

VPC Flow Logs 또는 GuardDuty
-> 네트워크/위협 탐지 쪽 보완. IDS/IPS를 일부 보완하는 느낌.

CloudWatch Logs Agent
-> EC2의 Apache 로그를 CloudWatch로 보내 운영 로그까지 통합.





///

[핵심]
ALB + EC2 2대
Auto Scaling
AWS WAF

[보안 보강]
SSM Session Manager  ← ★ 추가 추천
Secrets Manager
VPC Flow Logs / GuardDuty
CloudWatch Logs Agent

[시간 남으면]
Inspector
AWS Config
ACM + HTTPS
Security Hub







////////////
WAF , Secret Manager , VPC Flow Logs , GuardDuty






EC2 Instance에서 create image로 web 이미지 만들었음.
images에서 AMIs에 나옴.



WAF 완료
아마존 코어룰셋 + 데이터베이스 룰만 넣어놨음.

403뜨는거 확인했음


VPC Flow Logs
만들었음. S3 버켓이 아니라 CloudWatch로 보내기로 함.


Secret Manager
비밀번호, API 키, DB 접속정보 같은 민감정보를 안전하게 보관하는 저장소

예를들어, 웹서버에서 RDS로 접속하는 가장 단순한 구현은 코드나 설정파일에 
DB_HOST = ...
DB_USER = admin
DB_PASSWOR = password

이렇게 하는 방식인데, 소스코드가 직접 유출되거나 설정파일이 노출되거나, GitHub에 운영상의 실수로 올라가면 비밀번호가 전부 털리게 됨.

Secrets Manager를 쓰면?
EC2/애플리케이션 -> Secrets Manager에 비밀번호 요청 -> IAM 권한 확인 -> 비밀값 반환 -> RDS 접속

즉, EC2/애플리케이션은 비밀번호를 Secrets manager에 요청해서 잠시 받아와 메모리에서 사용후 바로 버리는 방식.




mysql -h aws-lab-rds01.c7oewga4aq5t.ap-northeast-2.rds.amazonaws.com -P 3306 -u admin -p
비밀번호 : awslab01

Database : aws_lab
user : 'testuser'@'%'
SELECT, INSERT, DELETE 만 있음.





SECRET=$(aws secretsmanager get-secret-value --secret-id aws-lab-rds-secret --region ap-northeast-2 --query SecretString --output text)
DB_HOST=$(echo "$SECRET" | jq -r '.host')
DB_USER=$(echo "$SECRET" | jq -r '.username')
DB_PASS=$(echo "$SECRET" | jq -r '.password')
DB_PORT=$(echo "$SECRET" | jq -r '.port')

 MYSQL_PWD="$DB_PASS" mysql -h "$DB_HOST" -P "$DB_PORT" -u "$DB_USER"
접속되는지 확인 완료.

EC2 안에 쉘스크립트로
~/connect-rds.sh 
저장했음. 
MYSQL_PWD="$DB_... 이것만 하면 됨.












