# Developing OData ABAP Service using GET_EXPANDED_ENTITY( ) method

GET_EXPANDED_ENTITY( ) method : _is used to Fetch a single Header Record along with Corresponding Item records._

This method contains 2 important parameters:-
1. it_key_tab  : _To accept Input Key Field Value_
2. er_entity   : _To Send Output Header Record along with Corresponding Items Records_

### Steps:-

ZUSERINFO ( Table which contains  Header Records )

ZUSERDETAILS ( Table which contains Item Records )


1. Open Your OData Service Project under SEGW tcode
2. Under Data Model , create Entity Type & Entity Set  with ABAP Structure ( ZUSERINFO ) ( Userid is the Key field )
3.  Data Model, create Entity TYpe & Entity Set with ABAP Structure ( ZUSERDETAILS ) ( Userid is the Key field )
4. Create Association,  Maintain Referential Constraint , Create Association Set:-
    - **Creating Association**
        - Expand Data Model Folder -> Right Click on "Associations"  Folder - > click on Create option
        - Configure  Association Name  = Association
        - configure Priniciple  Entity Type  = USERHEADER with Cardinality ( 1 )
        - configure  Dependent Entity Type = USERITEMS   with Cardinality ( 0-N )
        - Configure Navigation property  =  NP_ON_USERID
        - click next
    - **Maintain Referential Constraint**
        - left side  -> Configure   Userid   For ( USERHEADER  )
        - right side -> Configure  Userid  For ( USERITEMS )
        - click next
    - **Create Association Set**
        - Provide AssociationSet Name  = AssociationSet
        - left side  ->configure Principle Entity Set = USERHEADERSet
        - right side -> Configure Dependent Entity Set = USERITEMSSet
        - click Finish
5. Generate Runtime Artifacts 


REDEFINE GET_EXPANDED_ENTITY( ) method of Data Provider Extension Class ( DPC_EXT ).


```
data: begin of str_exp.
        include type zcl_z8amhiodataproj_01_mpc=>ts_userheader.
        data: NP_ON_USERID type zcl_z8amhiodataproj_01_mpc=>tt_useritems,
      end of str_exp.

data: ls_expand like str_exp,
      ls_useritems type zcl_z8amhiodataproj_01_mpc=>ts_useritems.

data: it_userheader   type table of ZUSERINFO,
      it_useritems    type table of ZUSERDETAILS,
      wa_userheader   like line of it_userheader,
      wa_useritems    like line of it_useritems.

data:wa_key_tab TYPE /IWBEP/S_MGW_NAME_VALUE_PAIR.

constants: lc_expand_tech_clause type string value 'NP_ON_USERID'.


Read Table it_key_tab into wa_key_tab index 1.

select * from ZUSERINFO into corresponding fields of table it_userheader WHERE Userid = wa_key_tab-value.

select * from ZUSERDETAILS into table it_useritems WHERE Userid = wa_key_tab-value.

loop at it_userheader into wa_userheader.
     move-corresponding wa_userheader to ls_expand .

    loop at it_useritems into wa_useritems where Userid = wa_userheader-Userid.
        move-corresponding wa_useritems to ls_useritems.
        append ls_useritems to ls_expand-np_on_userid.
        clear ls_useritems.
    endloop.

endloop.

copy_data_to_ref( EXPORTING is_data = ls_expand
                  changing  cr_data = er_entity ).


insert lc_expand_tech_clause into table et_expanded_tech_clauses.

```

#### Testing :-

/sap/opu/odata/SAP/Z8AMHIODATAPROJECT1_SRV/USERHEADERSet(Userid='1001')?$expand=NP_ON_USERID

/sap/opu/odata/SAP/Z8AMHIODATAPROJECT1_SRV/USERHEADERSet(Userid='1002')?$expand=NP_ON_USERID

/sap/opu/odata/SAP/Z8AMHIODATAPROJECT1_SRV/USERHEADERSet(Userid='1001')?$expand=NP_ON_USERID&$format=json
