## Table of Contents
- [Views](#Views)
	- [Syntax](#Syntax)
	- [Rules](#Rules)
- [PLSQL](#PL/SQL)
	- [Records](#Records)
	- [Cursors](#Cursors)
	- [Stored Procedures](#Stored%20Procedures)
	- [Functions](#Functions)
	- [Triggers](#Triggers)
- [Query Optimization](#Query%20Optimization)
	- [Indexes](#Indexes)

## Views
Basically just a query with a name

### Syntax
[More info](LO8/8.1%20Views)

```sql
CREATE [OR REPLACE] VIEW viewName [ ( aliases for columns ) ] AS
	SELECT statement [WITH ( READ ONLY | CHECK OPTION ) ];
```

Use *`OR REPLACE`* if you want to replace an existing view with a new `SELECT` statement
Provide aliases for columns

**`WITH READ ONLY`** means only selects are allowed against the view
- updates, inserts, and deletes aren't allowed

**`WITH CHECK OPTION`** means the user can insert, update, and delete but only those rows that are available in the view
- without the check option, the user could create a row that would not appear in the view

*Naming columns*
- Can give names to use for the columns in a list after the view name
- Can also use column aliases in `SELECT` statement

### Rules
[More Info](LO8/8.2%20Modifying%20Data%20through%20Views)

A view is not updateable if it has any of the following items in the select clause

*`DISTINCT`*

An *Aggregate* or *analytical* function (`SUM`, `MAX`, etc.)
- Single row functions don't break this rule (you just can't update those fields)

*`GROUP BY`*, *`ORDER BY`*, or *`HAVING`* clause

References to more than one table (`FROM` clause, subquery, `UNION`, etc.)
- Oracle and many systems support updateable join views, with restrictions
	- Can only update one base table through the view at most
	- Must have at least one key preserved table

References to a view that is read only or non-updateable

**Bottom line: for a view to be updateable, the DBMS must be able to trace any row or column back to it's row or column in the source table**

## PL/SQL

### Records
[More Info](LO9/9.1%20PSQL#Records)

#### Syntax
```sql
TYPE record_type_name IS RECORD
	(first_col_name column_datatype[, second_col_name column_datatype, ... ]);
```
To base the record on a table existing in your database
```sql
col_name table_name.column_name%type;
```

#### Passing values to/from a Record
```sql
record_name.col_name := value;
```
Can also do it with `SELECT`
```sql
SELECT col1, col2
	INTO record_name.col_name1, record_name.col_name2
	FROM table_name
	[WHERE clause];
```

**A record can only have on row of data selected into it (Use a `WHERE` clause)**

### Cursors
[More Info](LO9/9.1%20PSQL#Cursors)

#### Syntax Example
```sql
DECLARE
    -- copy title table row type
    title_rec title%ROWTYPE;
    -- Declare a cursor taht will get the expensive books
    CURSOR title_cur (price_in) IS
        SELECT * FROM Title WHERE price > price_in; -- query isn't executed yet

BEGIN
    -- CURSOR select query is run on Open
    OPEN title_cur(&EnterANumber); -- Note IF you know you will GET exactly one ROW, it's easier IF you just SELECT INTO a RECORD
    LOOP
        EXIT WHEN title_cur%NOTFOUND;
    
        FETCH title_cu INTO title_rec;
    
        DBMS_OUTPUT.PUT_LINE(title_rec.title || ' ' || title_rec.price);
        
    END LOOP;
    CLOSE title_cur; -- END processing ON CURSOR/ RELEASE resources
    
END;
```

### Stored Procedures
[More Info](LO9/9.2%20Stored%20Procedures)

are a type of **Named Block**
can take in parameters but never returns a value (like a void method in C#/Java)

#### Syntax
```sql
CREATE [OR REPLACE] PROCEDURE proc_name [ (list of parameters)]
IS
	-- Declaration section
BEGIN
	-- Execution section
EXCEPTION
	-- Exception section
END;
```

##### Parameters
*IN*
- Most common
- Can be referenced by the procedure but can't change it
- default

*OUT*
- The parameter can't be referenced by the value but can be overwritten

*IN OUT*
- pass by reference
- Can both be referenced and overwritten

##### Execution
```SQL
EXECUTE [or EXEC] procedureName;
-- Or
procedureName;
```

### Functions
[More Info](LO9/9.3%20Functions)

Similar to **procedures**, but must always return a value (can't be void)

#### Syntax
```SQL
CREATE [OR REPLACE] FUNCTION [Parameters]
	RETURN return_datatype
IS
	-- Declaration Section
BEGIN
	-- Execution section
EXCEPTION
	-- Exception section
END;
```

##### Execution
*Assign result to a variable*
```sql
employee_name := employer_details_func;
```

### Triggers
[More Info](LO9/9.4%20Triggers)

Block that is triggered to fire when a condition is met
*Row-level*: Triggered for each row changed (Ex. deleting 10 rows triggers it 10 times)
*Statement-level*: Triggered for the statement as a whole

#### Syntax
```sql
CREATE [OR REPLACE] TRIGGER trigger_name
	{BEFORE | AFTER | INSTEAD OF }
	{INSERT [OR] | UPDATE [OR] | DELETE }
	{ OF col_name }
	ON table_name
	[REFERENCING OLD AS o NEW AS n]
	[FOR EACH ROW]
	WHEN (condition)

DECLARE

BEGIN
	-- SQL Statements

END;
```

**`INSTEAD OF`** is only used for views
- Lets you get around certain views being read only?
- `BEFORE` and `AFTER` can't be used on a view

**`OLD`** and **`NEW`**
- By default you can reference the values as *`:old.column_name`* or *`:new.column_name`*
- Reference names can be changed from old/new to any other user-defined name
- `OLD` can't be used in `INSERT` triggers
- `NEW` can't be used in `DELETE` triggers
- Both can be used in `UPDATE` triggers

**`FOR EACH ROW`** makes it a *row level trigger*

#### Information about existing triggers
This view stores info about header and body of the trigger
```sql
SELECT * FROM USER_TRIGGERS WHERE trigger_name = 'Before Update Stat_product';
```

## Query Optimization
[Basics of Query Optimization](LO10/10.1%20Query%20Optimization#Basics%20of%20Query%20Optimization)

### Indexes
[More Info](LO10/10.1%20Query%20Optimization)

**A logical pointer to a physical location**

#### Syntax
```SQL
CREATE [ UNIQUE | BITMAP ] INDEX index_name 
	ON table_name ({ column_name | column_expressions } [ ASC | DESC ] [, ...])
	[ various storage attributes ];
```

**`BITMAP`** - Works best for columns with a small set of possible values (Ex. only 3 or 4)
**`UNIQUE`** - Prevents duplication

#### `Explan.sql`
```sql
SELECT
  id ||
  DECODE(id, 0, '', LPAD(' ', 2*(level - 1))) || ' ' ||
  operation || ' ' ||
  options || ' ' ||
  object_name || ' ' ||
  object_type || ' ' ||
  DECODE(cost, NULL, '', 'Cost = ' || position)
AS execution_plan
FROM plan_table
CONNECT BY PRIOR id = parent_id
AND statement_id = '&v_statement_id'
START WITH id = 0
AND statement_id = '&v_statement_id';
```
