# AWS WAF

<aside>
💡 일반적인 웹 공격으로부터 웹앱, API를 보호하는 웹 애플리케이션 방화벽

</aside>

- cross-site scripting or SQL injection 공격 방어
- 특정 IP 주소로부터 오는 request를 block or allow

### WAF + ALB in VPC

- WAF + ALB
- web ACL에 있는 규칙에 따라 Geographic 조건에 따라 request를 허용/제한
- `geo match conditions` : WAF가 접근을 허용할 국가를 선택할 수 있음