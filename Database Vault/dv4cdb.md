# Verify if Label Security and Database Vault are Installed & Configured
```
col DESCRIPTION format a40
set lines 900
SELECT * FROM SYS.DBA_DV_STATUS;
SELECT * FROM DBA_OLS_STATUS;
```
# Create new Users for Database Vault
```
GRANT CREATE SESSION, SET CONTAINER TO c##dv_owner IDENTIFIED BY ORacle1234## CONTAINER = ALL;
GRANT CREATE SESSION, SET CONTAINER TO c##dv_acctmgr IDENTIFIED BY ORacle1234## CONTAINER = ALL;
```
# Configure Database Vault (Connect as root admin)
```
BEGIN
CONFIGURE_DV (
 dvowner_uname => 'c##dv_owner',
 dvacctmgr_uname => 'c##dv_acctmgr',
 force_local_dvowner => FALSE);
END;
/
exec CONFIGURE_DV('c##dv_owner','c##dv_acctmgr');
```
# Recompile Invalid Objects
```
@?/rdbms/admin/utlrp.sql
```

# Connect to root as DV Owner User( c##dv_owner)
```
EXEC DBMS_MACADM.ENABLE_DV;
```
# Restart the 
```
SQL> conn / as sysdba
Shutdown immediate
Startup
```
# Verify if Label Security and Database Vault are Installed & Configured
```
SELECT * FROM SYS.DBA_DV_STATUS;
SELECT * FROM DBA_OLS_STATUS;
```
















