# Technical Design
## Design principles
- platform independant
- stand alone / client server / peer to peer
- most processing logic and data stored in database
## Flow
- front end posts command
- HTTP server calls CGI program
- CGI program executes SQL statement on database
- CGI program queries the result on database
- CGI program outputs html including query result
- HTTP server returns output to client
## Front end HTTP client
- web browser
## Server
- HTTP server
- SQL database
- CGI program
## CGI program
- wrapper for database
- build new statement if no result row returned from last statement
- unit tests
### writeprocess(sql statement from front end)
    printf(process(sql statement from front end))
### process(sql statement from front end, htmloutput)
    append htmlpagetop table to htmloutput
    execute ssffe on DB
    if error
	append error to htmloutput
    else
	while no rows are returned
	    build new SQL statement based on last executed statement
	    execute new SQL statement
        append rows to htmloutput
    append htmlpagebottom table to htmloutput
### buildnewsql(last sql statement)
    extract table name and main statement
    query defaultqueries  
### runtests
    query testcase
    while still more rows
        check (process(testcases.client request) = testcases.Expected result)
### tables
#### testcases
- SQL statement - client request
- SQL statement - Expected result
#### defaultqeueries
- statement name (insert, update, delete)
- table name
- query statement
##### default entries
- insert_table_name, '', sql to extract table from insert statement 
- update_table_name, '', sql to extract table from update statement 
- delete_table_name, '', sql to extract table from delete statement 
- '', '', 'select * from table_name limit 10'
#### htmlpage
- top
- bottom
