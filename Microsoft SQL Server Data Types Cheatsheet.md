#### String types

|Data type|Description|Maximum size|
|---|---|---|
|char(n)|Fixed width character string with `n` is the number of characters to store.  <br>Non-Unicode data.|8,000 characters|
|varchar(n)|Variable width character string with `n` is the number of characters to store.  <br>Non-Unicode data.|8,000 characters|
|varchar(max)|Variable width character string with maximum number of characters is 2GB.  <br>Non-Unicode data.|1,073,741,824 characters|
|text|Variable width character string.  <br>Non-Unicode data.|2GB of text data|
|nchar(n)|Fixed width character string with `n` is the number of characters to store.  <br>Unicode data.|4,000 characters|
|nvarchar(n)|Variable width character string with `n` is the number of characters to store.  <br>Unicode data.|4,000 characters|
|nvarchar(max)|Variable width character string with maximum number of characters is 2GB.  <br>Unicode data.|536,870,912 characters|
|ntext|Variable width character string.  <br>Unicode data.|2GB of text data|
|binary(n)|Fixed width binary string.|8,000 bytes|
|varbinary|Variable width binary string.|8,000 bytes|
|varbinary(max)|Variable width binary string.|2GB|
|image|Variable width binary string.|2GB|

---

#### Number types

|Data type|Description|Storage|
|---|---|---|
|bit|0, 1, or NULL||
|tinyint|From 0 to 255|1 byte|
|smallint|From -32,768 to 32,767|2 bytes|
|int|From -2,147,483,648 to 2,147,483,647|4 bytes|
|bigint|From -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807|8 bytes|
|decimal(p,s)|Fixed precision and scale numbers.  <br>`p` defaults to 18, if not specified.  <br>`s` defaults to 0, if not specified.|5-17 bytes|
|dec(p,s)|Fixed precision and scale numbers.  <br>`p` defaults to 18, if not specified.  <br>`s` defaults to 0, if not specified.|5-17 bytes|
|numeric(p,s)|Fixed precision and scale numbers.  <br>`p` defaults to 18, if not specified.  <br>`s` defaults to 0, if not specified.|5-17 bytes|
|smallmoney|From -214,748.3648 to 214,748.3647|4 bytes|
|money|From -922,337,203,685,477.5808 to 922,337,203,685,477.5807|8 bytes|
|float(n)|Floating point number data from -1.79E + 308 to 1.79E + 308  <br>`n` default to 53, if not specified.|4 or 8 bytes|
|real|Equivalent to float(24)|4 bytes|

---

#### Date data types:

| Data type|Description Storage| |
|---|---|---|
|datetime|From January 1, 1753 to December 31, 9999|8 bytes|
|datetime2|From January 1, 0001 to December 31, 9999|6-8 bytes|
|smalldatetime|From January 1, 1900 to June 6, 2079|4 bytes|
|date|Store a date only.  <br>From January 1, 0001 to December 31, 9999|3 bytes|
|time|Store a time only.  <br>From 00:00:00.0000000 to 23:59:59.9999999|3-5 bytes|
|datetimeoffset|From January 1, 0001 to December 31, 9999.  <br>Time zone offset range from -14:00 to +14:00.|8-10 bytes|
|timestamp|Stores a unique number that gets updated every time a row gets created or modified. The timestamp value is based upon an internal clock and does not correspond to real time. Each table may have only one timestamp variable.||

---

#### Some other types:

|Data type|Description|
|---|---|
|sql_variant|Stores up to 8,000 bytes of data of various data types, except text, ntext, and timestamp|
|uniqueidentifier|Stores a globally unique identifier (GUID)|
|xml|Stores XML formatted data. Maximum 2GB|
|cursor|Stores a reference to a cursor used for database operations|
|table|Stores a result-set for later processing|


>You may have seen Transact-SQL code that passes strings around using an N prefix. This denotes that the subsequent string is in Unicode (the N actually stands for National language character set). Which means that you are passing an NCHAR, NVARCHAR or NTEXT value, as opposed to CHAR, VARCHAR or TEXT.


