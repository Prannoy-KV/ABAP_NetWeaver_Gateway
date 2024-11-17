#  Download  Data/Records into  ExcelSheet via OData Service

Make sure that  GET_ENTITYSet( ) of  UserSet  is implemented. There is no extra coding required, we can download just by adding **_$format=xlsx_** in URL

---

#### Testing 
open Gateway Client 
  
Select GET option
Select  EntitySets ( for Ex :  UserSet )  
Select  ADD URI option  (  $format=xlsx )

Execute the service with below URL syntax

/sap/opu/odata/SAP/Z7AM_CRUD_ODATAPROJECT_SRV/UserSet?$format=xlsx

Check the output/response in browser  ( To view the downloaded data in Excel Sheet format  )


