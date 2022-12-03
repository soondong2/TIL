# Today I Learned - 2022/12/03 Sat

# Daily Leads and Partners
- 출처 : https://leetcode.com/problems/daily-leads-and-partners/
- 난이도 : Easy
<br>

## 풀이
```sql
SELECT
    date_id,
    make_name,
    COUNT(DISTINCT(lead_id)) AS unique_leads,
    COUNT(DISTINCT(partner_id)) AS unique_partners
FROM DailySales
GROUP BY date_id, make_name;
```
