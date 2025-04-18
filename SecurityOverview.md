Major security threats
Think like a hacker

1) Malware (Software intentianally designed to cause damage to a computer/network)
2) Insider threat (People working in your organization)
3) Human error
4) SQL Injection (Malicius SQL code for backend database to access information that is not intended to be displayed) where 1=1(always true)
5) Overloaded data (Data without as per context)
6) DDOS attach (distributed denial of service), network is flooded with so much mallisious trafic as it can't communicate. starts spaning
   many connections. Lagitimate connections will be haulted.

What is MSA?
Maximum Security Architecture.

What we need to secure?
Data and its users.

Steps
1) Assess security posture of database (DBSTAT, Data discovery, privilege analysis (bypass alerts))

2) Detect using (Activity Auditing/Monitoring, Audit vault, database firewall(examinse the SQLs to prevent SQL injection)
   Learn Oracle unified auditing available since 12c
   Audit vault and DB firewall combined into one component.

3) Prevent using (Encryption and key vault, Data Masking, Data redaction, Database vault).

Data
Crypto toolkit
Virtual private database
Label Security
Real application security

Users
Password, PKI, kerberos, Radius Proxy users, Password profiles, Oracle & Active directory


Difference between data masking and data reduction.
In masking we are updating records or changing data
Data reduction is we hide the sensitive data such as credit card number piror to displaying to users at runtime.
Without changing the actual data.

