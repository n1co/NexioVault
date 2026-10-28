```python
#!/usr/bin/env python3

import random, time
from datetime import datetime, timedelta

hosts = ["web01.example.local", "db01.example.local"]
usernames = ["root","admin","test","ubuntu","ec2-user"]
attacker_ips = ["203.0.113.5","198.51.100.23","192.0.2.45"]
reasons = [
    "Failed password for invalid user {user} from {ip} port {port} ssh2",
    "Failed password for {user} from {ip} port {port} ssh2",
    "Invalid user {user} from {ip}",
    "Disconnected from authenticating user {user} {ip} port {port}"
]

start = datetime.now() - timedelta(minutes=30)
lines = []
for i in range(600):  # 600 lignes sur ~30 minutes
    ts = start + timedelta(seconds=i*3 + random.randint(0,2))
    host = random.choice(hosts)
    ip = random.choice(attacker_ips)
    user = random.choice(usernames)
    port = random.randint(1024,65535)
    reason = random.choice(reasons).format(user=user, ip=ip, port=port)
    line = ts.strftime("%b %d %H:%M:%S") + f" {host} sshd[{1000 + (i%50)}]: {reason}"
    lines.append(line)

with open("auth_bruteforce.log", "a") as f:
    f.write("\n".join(lines))

print("Fichier auth_bruteforce.log généré (600 lignes).")

```

```
index=* sourcetype=access-too_small | rex field=_raw "(?ms)^(?P<field_ip>[^ ]+)[^\\[\\n]*\\[(?P<field_date>[^\\]]+)(?:[^ \\n]* ){2}(?P<field_url>/[a-z]+)[^\"\\n]*\"\\s+(?P<field_status>\\d+)\\s+(?P<field_requestsize>\\d+)\\s+\"\\-\"\\s+\"(?P<field_useragent>[^\"]+)" offset_field=_extracted_fields_bounds
```