---
layout: post
title: PDW - Currently Assign User Permissions
categories: code
comments: true
---

## Introduction

Let us jump right in, the first thing that we need to know is that the APS/PDW is not like a normal SQL Server instance. It does look and feel like one, but it has its own little quirks. One of the big ones is that it is not as straight forward to see current assigned User Permissions as what one would expect.

## Code Snippet

```sql
SELECT	DPUsers.name AS UserName, 
		permission_name,	
		object_name(major_id) AS ObjectName
FROM sys.database_permissions AS DP 
JOIN sys.database_principals AS DPUsers ON DP.grantee_principal_id = DPUsers.principal_id 
WHERE DPUsers.name not like '##%' 
AND DPUsers.name not like 'NT SERVICE%' 
AND DPUsers.name not like 'NT AUTHORITY%' 
AND DPUsers.name != 'public' 
and DPUsers.name not like 'l_cert%' 
```

## Review

The above code snippet will return you with the Username, The Granted Permission and the ObjectName if only granted on a specific object.

## External Links

[https://www.microsoft.com/en-us/sql-server/analytics-platform-system](https://www.microsoft.com/en-us/sql-server/analytics-platform-system)

[https://docs.microsoft.com/en-us/sql/analytics-platform-system/parallel-data-warehouse-overview?view=aps-pdw-2016-au7](https://docs.microsoft.com/en-us/sql/analytics-platform-system/parallel-data-warehouse-overview?view=aps-pdw-2016-au7)

[https://docs.microsoft.com/en-us/sql/analytics-platform-system/pdw-permissions?view=aps-pdw-2016-au7](https://docs.microsoft.com/en-us/sql/analytics-platform-system/pdw-permissions?view=aps-pdw-2016-au7)

[https://saurabhsinhainblogs.blogspot.com/2016/01/frequently-used-sql-server-pdw-parallel.html](https://saurabhsinhainblogs.blogspot.com/2016/01/frequently-used-sql-server-pdw-parallel.htm)


{% include post_footer.html %}
