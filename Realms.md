# Select Data from HR Schema
```
select * from hr.employees;
```
# Connect to root as DV Owner User( c##dv_owner_root)
```
connect c##dv_owner_root@pdb1
```
# Create a Realm on HR Schema
```
BEGIN
DBMS_MACADM.CREATE_REALM(
 realm_name => 'HR_REALM',
 description => 'Realm for HR Schema',
 enabled => DBMS_MACUTL.G_YES,
 audit_options => DBMS_MACUTL.G_REALM_AUDIT_FAIL +
DBMS_MACUTL.G_REALM_AUDIT_SUCCESS);
END;
/

BEGIN
DBMS_MACADM.ADD_OBJECT_TO_REALM(
 realm_name => 'HR_REALM',
 object_owner => 'HR',
 object_name => '%',
object_type => '%');
END;
/
```
# Select Data from HR Schema
```
select * from hr.employees;
```


# Exporting Data in Database Vault Enabled Environment
# Export 
```
expdp system@pdb1 schemas=HR
```

# Connect to root as DV Owner User( c##dv_owner_root)
```
Connect c##dv_owner_root@pdb1
```

# Authorize Export 
```
SQL> EXEC DBMS_MACADM.AUTHORIZE_DATAPUMP_USER('SYSTEM');
PL/SQL procedure successfully completed.
```

# Export 
```
expdp system@pdb1 schemas=HR
```

# Creating a user
```
SQL>alter session set container=pdb1;
SQL>
SQL> create user scott identified by tiger;
create user scott identified by tiger
*
ERROR at line 1:
ORA-01031: insufficient privileges
```

# The right user to allow this (c##_dv_acctmgr)
```
sqlplus c##dv_acctmgr_root@pdb1
SQL> create user scott identified by ORacle1234##;
User created.
```

