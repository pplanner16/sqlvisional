# Technical Design
## Design principles
- platform independant
- client server
- most processing logic and data stored in database
## Flow
- front end posts command
- HTTP server calls CGI program
- CGI program executes SQL statement on database
- CGI program queries the result on database
- CGI program outputs html including query result
- HTTP server returns output to client
### Commands
- import table
- SQL statement
## Front end HTTP client
- web browser
## Server
- HTTP server
- SQL database
- CGI program
## CGI program
- wrapper for database
- builds and executes new statement if no result row returned from last statement
- unit tests
- import table
### writeprocess(sql statement from front end)
    printf(process(sql statement from front end))
### process(sql statement from front end, htmloutput)
    append htmlpagetop table to htmloutput
    execute ssffe on DB
    if error
	append error to htmloutput
    else
	while no rows are returned
	    recursively search for subsequent SQL statement
### runtests
    query testcase
    while still more rows
        check (process(testcases.client request) = testcases.Expected result)
### tables
#### testcases
- SQL statement - client request
- SQL statement - Expected result
#### subsequent_queries
- id
- parent id
- statement pattern
- query statement
##### default entries
- insert_table_name, '', sql to extract table from insert statement 
- update_table_name, '', sql to extract table from update statement 
- delete_table_name, '', sql to extract table from delete statement 
- '', '', 'select * from table_name limit 10'
#### htmlpage
- top
- bottom
