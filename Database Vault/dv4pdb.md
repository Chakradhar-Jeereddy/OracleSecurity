## Pluggable Database (PDB1) 

# Connect as Admin to PDB1
```
Alter session set container=pdb1;
```
# Verify if Label Security and Database Vault are Installed & Configured
```
SELECT * FROM SYS.DBA_DV_STATUS;
SELECT * FROM DBA_OLS_STATUS;
```
# Select Data from HR Schema
```
create schema from $ORACLE_HOME/demo/schema/human_resources/hr_main.sql
select EMPLOYEE_ID,FIRST_NAME,LAST_NAME,SALARY from hr.employees ;
```
# Configure Database Vault
```
BEGIN
CONFIGURE_DV (
 dvowner_uname => 'c##dv_owner',
 dvacctmgr_uname => 'c##dv_acctmgr');
END;
/
```
# Connect as DV Owner User( c##dv_owner)
```
connect c##dv_owner@192.168.1.12:1521/pdb1
EXEC DBMS_MACADM.ENABLE_DV;
```
# Restart the Pluggable Database 
```
Alter pluggable database pdb1 close;
Alter pluggable database pdb1 open;
```
# Verify if Label Security and Database Vault are Installed & Configured
```
SELECT * FROM SYS.DBA_DV_STATUS;
SELECT * FROM DBA_OLS_STATUS;
```






