# apex-cheat-sheet

## Collections

# Populate Collections
```
declare
    l_rowxml varchar2(4000);
begin
if apex_collection.collection_exists( 'EMPCollection') = TRUE then
    --
    apex_collection.delete_collection(
        p_collection_name => 'EMPCollection' );
end if;
--
apex_collection.create_collection_from_query2(
    p_collection_name => 'EMPCollection',
    p_query           => 'select empno, sal, comm, deptno, null, hiredate, null, null, null, null, ename, job, mgr, ''O'' original_flag from eba_demo_cs_emp order by ename',
    p_generate_md5    => 'YES');
--
for c1 in (select n001 empno, seq_id
             from apex_collections
            where collection_name = 'EMPCOLLECTION'
           order by seq_id) loop
    
    l_rowxml := dbms_xmlgen.getxml( 'select * from eba_demo_cs_emp where empno = ' || c1.empno );
    apex_collection.update_member_attribute( 
        p_collection_name => 'EMPCollection',
        p_seq             => c1.seq_id,
        p_xmltype_number  => 1,
        p_xmltype_value   => XMLType(l_rowxml));
end loop;
--
commit;
end;
```

## Request
Request can be what you name the button or the following value based on operation:
- CREATE
- SAVE
- DELETE

## Processing
- get pk
- process row
- reset page
- close dialog

### Get PK
When Button Pressed: CREATE
```
begin 
    if :P10_ID is null then
        select "#OWNER#"."EAC_GROUP_SEQ".nextval
          into :P10_ID
          from sys.dual;
    end if;
end;
```

### Process Row of <Table>
- Automatic Row processing 
- Provide ID

### reset page
- clear session state
  - when button pressed delete

### close dialog
- when REQUST in CREATE SAVE DELETE

### Dialog Closed
- Dymaic action on region to refresh
  - event: Dialog closed
