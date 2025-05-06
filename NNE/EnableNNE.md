## How to check NNE is enabled?
```
select network_service_banner from v$session_connect_info where sid in (select distinct sid from v$mystat);
```
## How to enable NNE?
```
As to be done in SQLNET.ora
cd $ORACLE_HOME/network/admin
SQLNET.ENCRYPTION.SERVER=REQUIRED
SQLNET.ENCRYPTION_TYPES_SERVER=(AES256)               (helps to encrypt in transit data over network)
SQLNET.CRYPTO_CHECKSUM_SERVER=REQUIRED                (helps to maintain data intigrity)
SQLNET.CRYPTO_CHECKSUM_TYPES_SERVER=(SHA1)


SQLNET.ENCRYPTION_SERVER=REQUIRED
SQLNET.CRYPTO_CHECKSUM_SERVER=REQUIRED
SQLNET.ENCRYPTION_TYPES_SERVER=(AES256,AES192,AES128)
SQLNET.CRYPTO_CHECKSUM_TYPES_SERVER=(SHA256,SHA384,SHA512,SHA1)
SQLNET.ENCRYPTION_CLIENT=REQUIRED
SQLNET.CRYPTO_CHECKSUM_CLIENT=REQUIRED
SQLNET.ENCRYPTION_TYPES_CLIENT=(AES256,AES192,AES128)
SQLNET.CRYPTO_CHECKSUM_TYPES_CLIENT=(SHA256,SHA384,SHA512,SHA1)
SQLNET.EXPIRE_TIME=10

sqlplus sys@tns as sysdba
select network_service_banner from v$session_connect_info where sid in (select distinct sid from v$mystat);
```

## Inspect Network trafic after enabling NNE.
```
Take a new session-
ip addr show           => list network interfaces
tcpdump -i lo -A port 1521

-i -> interface
-A  -> ASSCI format

sqlplus sys@pdb1 as sysdba
select * from hr.employees;
```

## scripts
```
[oracle@chakra ~]$ cat banner
#!/bin/bash

sqlplus -s / as sysdba <<EOF
set heading off
set feedback off
select network_service_banner from v\$session_connect_info where sid in (select distinct sid from v\$mystat);
EXIT

#!/bin/bash
[oracle@chakra ~]$ cat tcpsql
sqlplus -s system/"ReddY__321"@"198.168.0.14:1521/pdb1.demopub.demo.oraclevcn.com" <<EOF
set heading off
set feedback off
set lines 300
select name from v\$datafile;
EXIT
EOF

[oracle@chakra ~]$ cat nic
#!/bin/bash
ip addr show
```


