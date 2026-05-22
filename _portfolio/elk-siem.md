---
layout: single
title: "SIEM Dashboard with ELK Stack"
excerpt: "Configured Elasticsearch, Logstash, and Kibana to aggregate firewall and auth logs, with custom alerts for anomaly detection."
date: 2023-11-05
type: blue-team
featured: true
author_profile: false
tags:
  - ELK Stack
  - Kibana
  - Logstash
  - SIEM
  - Log Analysis
header:
  teaser: /assets/images/projects/elk.png
---

## Overview

Set up a home-lab SIEM using the ELK Stack (Elasticsearch, Logstash, Kibana) to centralise logs from multiple sources and detect suspicious activity through custom dashboards and alert rules.

## Architecture

```
[pfSense Firewall] ──┐
[Ubuntu Server]    ──┼──► Logstash ──► Elasticsearch ──► Kibana
[Windows 10 VM]    ──┘
```

## Log Sources

| Source | Log Type |
|--------|---------|
| pfSense | Firewall allow/deny events |
| Ubuntu Server | SSH auth logs (`/var/log/auth.log`) |
| Windows 10 VM | Windows Event Logs (Security) |
| Apache | Web server access and error logs |

## What I Built

### Custom Kibana Dashboards

- **SSH Brute Force Monitor** — shows failed login attempts grouped by source IP and time
- **Firewall Traffic Overview** — top blocked IPs, ports, and countries
- **Authentication Timeline** — successful vs failed logins per hour

### Logstash Pipeline (example)

```ruby
input {
  file {
    path => "/var/log/auth.log"
    type => "ssh"
  }
}

filter {
  grok {
    match => { "message" => "%{SSHFAILED}" }
  }
  geoip {
    source => "src_ip"
  }
}

output {
  elasticsearch {
    hosts => ["localhost:9200"]
    index => "ssh-logs-%{+YYYY.MM.dd}"
  }
}
```

### Alert Rules

- 5+ failed SSH logins from same IP within 60 seconds → alert
- New admin account created on Windows VM → alert
- Outbound connection to known malicious IP → alert

## Results

- Caught a simulated brute-force attack in under 30 seconds
- Visualised traffic patterns across all three machines in one dashboard
- Reduced alert noise by 60% after tuning grok filters

## What I learned

- Log normalisation and grok pattern writing
- Elasticsearch index management and retention policies
- Building actionable dashboards vs noisy dashboards

## Source

[View on GitHub](https://github.com/yourusername/elk-siem-lab)
