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

sqlplus sys@tns as sysdba
select network_service_banner from v$session_connect_info where sid in (select distinct sid from v$mystat);
```

## Inspect Network trafic after enabling NNE.
```
ip addr show           => list network interfaces
tcpdump -i lo -A port 1521

-i -> interface
-A  -> ASSCI format
```
