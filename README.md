# apex-cheat-sheet

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

###Process Row of <Table>
- Automatic Row processing 
- Provide ID

### reset page
- clear session state
  - when button pressed delete

### close dialog
- when REQUST in CREATE SAVE DELETE

###Test

