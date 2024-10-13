---
title: "Parse and Filter Nuclei Json"
author: "John Coleman"
date: "2024-09-28"
tags: 
     - howto
     - nuclei
---

# Create a csv with select fields

Show only template-id, severity, host, matched-at. Exclude info and low severity.

```
jq -r '
    # Print the header
    "template-id,severity,host,matched-at",
    # Extract and transform the data to CSV format
    (.[] | select(.info.severity != "info" and .info.severity != "low") | [
        .["template-id"], 
        .info.severity, 
        .host,
        .["matched-at"]
    ] | @csv)
' nuclei_http.json
```
```
template-id,severity,host,matched-at
"CVE-2018-11784","medium","1.2.3.4","http://1.2.3.4//interact.sh"
"open-redirect-generic","medium","5.6.7.8","http://5.6.7.8///%6f%61%73%74%2e%6d%65"
"generic-j2ee-lfi","high","3.4.5.6","http://3.4.5.6/WEB-INF/web.xml"
```
