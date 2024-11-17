# Develop OData ABAP Service with GET_ENTITY( ) method

Get_Entity( ) method is used to send a single record.

 Get_Entity( ) method contains 2 important parameters:
 1. it_key_tab: will accept Input Key Field Value(s).
 2. er_entity: will send output record.

In order to create a workarea which deals with Input Key Field we use a standard Structure `/IWBEP/S_MGW_NAME_VALUE_PAIR`.<br>
`/IWBEP/S_MGW_NAME_VALUE_PAIR` contains 2 options
1. NAME  (  Name of Key Field )
2. VALUE ( Value of Key Field )

In order to create a Internal table which deals with Input Key Field we use a standard Table Type `/IWBEP/T_MGW_NAME_VALUE_PAIR`

### Code:- 

We "REDEFINE" the <entity_set>_GET_ENTITY( ) method of DataProvider Extension Class ( DPC_EXT ) Class

Note:- In this example Userid and Firstname are key fields.

```
Data  : wa_key_tab1  TYPE /IWBEP/S_MGW_NAME_VALUE_PAIR.
Data  : wa_key_tab2  TYPE /IWBEP/S_MGW_NAME_VALUE_PAIR.    

"At index 1 we have key-value pair of Userid.
"At index 2 we have key-value pair of Firstname.
"Indexes depends on the URL's used to Query( see below URL )
Read Table  it_key_tab  into  wa_key_tab1  index 1. 
Read Table  it_key_tab  into  wa_key_tab2  index 2. 
    
Select single * from ZUSERINFO into
    CORRESPONDING FIELDS OF ER_ENTITY
    where Userid  =  WA_KEY_TAB1-VALUE
    and
    Firstname = WA_KEY_TAB2-VALUE.
```

open Service Maintainence<br>
open Gateway Client

**Note to Clean cache:- Select metadata  -> cleanup cache from Both Systems -> Continue**

now you can test the service with GET option Under Gateway Client with below url

`/sap/opu/odata/SAP/Z630AM_ODATAWITHBAPI_SRV/UserSet(Userid='1001',Firstname='VIJAY')`

