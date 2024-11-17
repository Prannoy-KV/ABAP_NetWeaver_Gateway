# Various DPC Methods and it's important Parameters

1. \<EntitySet>_Get_Entity( ):- _Is used to fetch a single record based on input Key Field(s)._
    
    | Parameter | Functionality |
    | ------ | ------ |
    | it_key_tab | Accepts input Key Field Value(s) |
    | er_entity | Sends single output record |

2. \<EntitySet>_Get_EntitySet( ):- _Is used to fetch N Number of record(s) based on Input(s)
._

    | Parameter | Functionality |
    | ------ | ------ |
    | iv_filter_string | Accepts input Value(s) |
    | iv_search_string | Accepts input Value(s) |
    | it_filter_select_options | Accepts input Value(s) |
    | io_tech_request_context | Sends output record(s) |

3. \<EntitySet>_Create_Entity( ):- _Is used to Insert Data._

    | Parameter | Functionality |
    | ------ | ------ |
    | io_data_provider | Accepts input record values(s) |
    | er_entity | Sends output record |

4. \<EntitySet>_Update_Entity( ):- _Is used to Update Data._

    | Parameter | Functionality |
    | ------ | ------ |
    | it_key_tab | Accepts input Key Field Value(s) |
    | io_data_provider | Accepts input record values(s) |
    | er_entity | Sends output record |

5. \<EntitySet>_Delete_Entity( ):- _Is used to Delete Data._

    | Parameter | Functionality |
    | ------ | ------ |
    | it_key_tab | Accepts input Key Field Value(s) |
    | set_header(key/value) | Sends output message |

6. Update_Stream( ):- _Is used to Upload File Content._

    | Parameter | Functionality |
    | ------ | ------ |
    | it_key_tab | Accepts input Key Field Value(s) |
    | is_media_resource | Accepts Input File Content & Input File Type |

7. Get_Stream( ):- _Is used to Download File Content._

    | Parameter | Functionality |
    | ------ | ------ |
    | it_key_tab | Accepts input Key Field Value(s) |
    | er_stream | Sends output File Content & Output File Type |

8. Execute_Action:- _Is generic and can be used for INSERT and SELECT functionality._

    | Parameter | Functionality |
    | ------ | ------ |
    | iv_action_name | Captures the name of the action triggered |
    | it_parameter | Accepts input value(s) |
    | er_data | Sends output data |

9. Get_Expanded_Entity:- _Is used to fetch a single Header data and its corresponding item data._

    | Parameter | Functionality |
    | ------ | ------ |
    | it_key_tab | Accepts input Value(s) |
    | io_tech_request_Context  | Accepts input value(s) |
    | io_expand | Accepts input value(s) |
    | er_entity | Sends output data |
    | et_expanded_tech_clauses | Sends output data ( Header + it's Item ) |

10. Get_Expanded_EntitySet:- _Is used to fetch Header data and its corresponding items data._

    | Parameter | Functionality |
    | ------ | ------ |
    | it_key_tab | Accepts input Value(s) |
    | iv_filter_string  | Accepts input value(s) |
    | iv_search_string | Accepts input value(s) |
    | io_tech_request_context | Accepts input value(s) |
    | it_filter_select_options | Accepts input value(s) |
    | er_entityset | Sends output data |
    | et_expanded_tech_clauses | Sends output data ( Header + it's Items ) |

