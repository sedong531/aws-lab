# 05 WAF

## 1. WAF 구성

- 외부에서 들어오는 웹 요청에 대해 애플리케이션 계층의 보안 통제를 적용하기 위해 AWS WAF를 구성하였다.

- Web ACL을 생성하여 웹 요청을 검사하고, 정의된 Rule에 따라 요청을 허용하거나 차단하도록 구성하였다.


## 2. Web ACL 및 Managed Rule

- Web ACL에 AWS Managed Rule Group을 적용하여 일반적인 웹 공격과 SQL Injection 패턴을 탐지·차단하도록 구성하였다.

- 적용한 Managed Rule Group은 다음과 같다.

| Rule Group | 역할 |
| --- | --- |
| AWSManagedRulesCommonRuleSet | 일반적인 웹 공격 패턴 탐지 및 차단 |
| AWSManagedRulesSQLiRuleSet | SQL Injection 공격 패턴 탐지 및 차단 |


## 3. ALB 연동

- WAF Web ACL을 Application Load Balancer(ALB)에 연결하여 외부 HTTP 요청이 웹 서버에 전달되기 전에 WAF Rule을 적용받도록 구성하였다.

- 정상 요청은 ALB를 통해 Target Group으로 전달되고, Rule에 의해 탐지된 요청은 WAF에서 차단하도록 구성하였다.


## 4. 대표 화면

### Web ACL
<src img="../images/5_WAF/web_acl.png" alt="" width="900">



### Web ACL에 적용된 Rules
<src img="../images/5_WAF/web_acl_rule.png" alt="" width="900">