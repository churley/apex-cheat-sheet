# apex-cheat-sheet

## Processing

### Get PK
```
begin 
    if :P10_ID is null then
        select "#OWNER#"."EAC_GROUP_SEQ".nextval
          into :P10_ID
          from sys.dual;
    end if;
end;
```
