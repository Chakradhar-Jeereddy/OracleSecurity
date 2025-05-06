# Create a new Tablespace 
```
SQL> create tablespace userstab datafile '+DATA' size 1G;
```
# Install Sample HR Schema in this Tablespace
```
@?/demo/schema/human_resources/hr_main.sql 
```
# Perform a strings command and view the data
```
strings /opt/oracle/oradata/XE/XEPDB1/userstab01.dbf
```
# Create an entry in sqlnet.ora file
```
ENCRYPTION_WALLET_LOCATION =
 (SOURCE = (METHOD = FILE)
 (METHOD_DATA =
 (DIRECTORY = /opt/oracle/wallet)
 )
 )
```
# Create the keystore
```
ADMINISTER KEY MANAGEMENT CREATE KEYSTORE '/opt/oracle/wallet' IDENTIFIED BY oracle12;
```
# Check the Wallet Directory
```
ls -ltr /opt/oracle/wallet
```
# Open the Keystore
```
ADMINISTER KEY MANAGEMENT SET KEYSTORE OPEN IDENTIFIED BY oracle12
```
# Open the Keystore
```
ADMINISTER KEY MANAGEMENT SET KEYSTORE OPEN IDENTIFIED BY oracle12
```
# Set the Master Encryption Key (always the keystore password)
```
ADMINISTER KEY MANAGEMENT SET KEY IDENTIFIED BY oracle12 with backup;
```
# Check the Wallet Directory
```
ls -ltr /opt/oracle/wallet
```
# Verify if the Wallet has been opened in CDB Database
```
select con_id,WRL_TYPE,wallet_type,STATUS,KEYSTORE_MODE from V$encryption_wallet;
````






