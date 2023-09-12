## N-prefix

You may have seen Transact-SQL code that passes strings around using an N prefix. This denotes that the subsequent string is in Unicode (the N actually stands for National language character set). Which means that you are passing an NCHAR, NVARCHAR or NTEXT value, as opposed to CHAR, VARCHAR or TEXT.
## OUTPUT
In SQL, `OUTPUT` is a clause used in some SQL statements, such as `INSERT`, `UPDATE`, and `DELETE`, to return specific data from the affected rows after the statement has executed. The `OUTPUT` clause allows you to retrieve values from the rows that were inserted, updated, or deleted by the statement.

When you see `OUTPUT 1`, it typically means that you want to return a single value from the affected row. The `1` here is often used as a placeholder to indicate that you are interested in some value from the row, but the specific value is not specified in the `OUTPUT` clause itself.
