Query 1: Brute Force

index=security EventCode=4625 
| stats count by user, src_ip 
| sort -count

Query 2: Phishing URL Check

index=proxy "bit.ly" OR "tinyurl"
| table _time, user, url

Query 3: Data Exfiltration Check

index=firewall 
| stats sum(bytes) by dest_ip 
| sort -sum(bytes)
