# Configure Transparent Database Encryption (TDE)
## Setup TDE in Pluggable Database

# Connect to pdb database xepdb1
```
Alter session set container=xepdb1;
```
# Open the Keystore & Create a Master Encryption Key for PDB
```
ADMINISTER KEY MANAGEMENT SET KEYSTORE OPEN IDENTIFIED BY oracle12 ;
ADMINISTER KEY MANAGEMENT SET KEY IDENTIFIED BY oracle12 with backup;
```
# Verify if the Wallet has been opened in PDB 
```
select con_id, WRL_TYPE,wallet_type,STATUS,KEYSTORE_MODE from V$encryption_wallet;
```
# Create a new Encrypted Tablespace
```
create tablespace userstab_enc datafile '/opt/oracle/oradata/XE/XEPDB1/userstab_enc_01.dbf' size 1G encryption using 'AES256' default storage (encrypt) ;
```
# Install Sample HR Schema in this Encrypted Tablespace
```
@?/demo/schema/human_resources/hr_main.sql 
```
# Run the strings command
```
alter system flush buffer_cache;
strings /u01/app/oracle/oradata/TESTDB/pdb_stats/userstab_enc_01.dbf
select	con_id,	WRL_TYPE,wallet_type,STATUS,KEYSTORE_MODE	from	V$encryption_wallet;
create	tablespace	testpdb2	datafile	size	1G	encryption	using	'AES256'	default	storage	(encrypt)	;
dbcli		list-databases
dbcli	update-tdekey	-i	dbbc28ad-c235-476b-9da5-37498911b118	-n	PDB2	-p Oracle1234##
```



