---
title: "CREATE INDEX Statement (Microsoft Access SQL)"
  
  
manager: soliver
ms.date: 3/9/2015
ms.audience: Developer
 
f1_keywords:
- jetsql40.chm5277562
  
localization_priority: Normal
ms.assetid: c5919ef4-a08d-df06-7078-5331adbcb45c
description: "Creates a new index on an existing table."
---

# CREATE INDEX Statement (Microsoft Access SQL)

Creates a new index on an existing table.
  
> [!NOTE]
> For non-Microsoft Access atabse engine databases, the Microsoft Access database engine does not support the use of CREATE INDEX (except to create a pseudo index on an ODBC linked table) or any of the data definition language (DDL) statements. Use the DAO Create methods instead. For more information see the Remarks section. 
  
## Syntax

CREATE [ UNIQUE ] INDEX  *index*  ON  *table*  (  *field*  [ASC|DESC][,  *field*  [ASC|DESC], …]) [WITH { PRIMARY | DISALLOW NULL | IGNORE NULL }] 
  
The CREATE INDEX statement has these parts:
  
|**Part**|**Description**|
|:-----|:-----|
| *index*  <br/> |The name of the index to be created.  <br/> |
| *table*  <br/> |The name of the existing table that will contain the index.  <br/> |
| *field*  <br/> |The name of the field or fields to be indexed. To create a single-field index, list the field name in parentheses following the table name. To create a multiple-field index, list the name of each field to be included in the index. To create descending indexes, use the DESC reserved word; otherwise, indexes are assumed to be ascending.  <br/> |
   
## Remarks

To prohibit duplicate values in the indexed field or fields of different records, use the UNIQUE reserved word.
  
In the optional WITH clause you can enforce data validation rules. You can:
  
- Prohibit Null entries in the indexed field or fields of new records by using the DISALLOW NULL option.
    
- Prevent records with **Null** values in the indexed field or fields from being included in the index by using the IGNORE NULL option. 
    
- Designate the indexed field or fields as the primary key by using the PRIMARY reserved word. This implies that the key is unique, so you can omit the UNIQUE reserved word.
    
You can use CREATE INDEX to create a pseudo index on a linked table in an ODBC data source, such as Microsoft® SQL Server™, that does not already have an index. You do not need permission or access to the remote server to create a pseudo index, and the remote database is unaware of and unaffected by the pseudo index. You use the same syntax for both linked and native tables. Creating a pseudo-index on a table that would ordinarily be read-only can be especially useful.
  
You can also use the [ALTER TABLE](alter-table-statement-microsoft-access-sql.md) statement to add a single- or multiple-field index to a table, and you can use the ALTER TABLE statement or the [DROP](drop-statement-microsoft-access-sql.md) statement to remove an index created with ALTER TABLE or CREATE INDEX. 
  
> [!NOTE]
> Do not use the PRIMARY reserved word when you create a new index on a table that already has a primary key; if you do, an error occurs. 
  
## Example

This example creates an index consisting of the fields Home Phone and Extension in the Employees table.
  
```
Sub CreateIndexX1() 
 
    Dim dbs As Database 
 
    ' Modify this line to include the path to Northwind 
    ' on your computer. 
    Set dbs = OpenDatabase("Northwind.mdb") 
 
    ' Create the NewIndex index on the Employees table. 
    dbs.Execute "CREATE INDEX NewIndex ON Employees " _ 
        &amp; "(HomePhone, Extension);" 
 
    dbs.Close 
 
End Sub 

```

This example creates an index on the Customers table using the CustomerID field. No two records can have the same data in the CustomerID field, and no Null values are allowed.
  
```
Sub CreateIndexX2() 
 
    Dim dbs As Database 
 
    ' Modify this line to include the path to Northwind 
    ' on your computer. 
    Set dbs = OpenDatabase("Northwind.mdb") 
 
    ' Create a unique index, CustID, on the  
    ' CustomerID field. 
    dbs.Execute "CREATE UNIQUE INDEX CustID " _ 
        &amp; "ON Customers (CustomerID) " _ 
        &amp; "WITH DISALLOW NULL;" 
 
    dbs.Close 
 
End Sub 

```

