# Develop OData ABAP Service with CREATE_ENTITY( ) method

Create_Entity( ) method is used to Insert Data.

Create_Entity( ) method contains 2 important parameters:-
1. io_data_provider: _will accept input record_
2. er_entity: _will send output record_

### Code:- 

We "REDEFINE" the <entity_set>_CREATE_ENTITY( ) method of DataProvider Extension Class ( DPC_EXT ) Class

```
Data : wa Type ZCL_Z630AM_ODATAWITHBA_MPC=>TS_EMP.

IO_DATA_PROVIDER->READ_ENTRY_DATA( IMPORTING  ES_DATA  = wa ).

INSERT into ZUSERINFO values wa.

commit WORK.
```




