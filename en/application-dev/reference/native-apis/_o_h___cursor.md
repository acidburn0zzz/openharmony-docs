# OH_Cursor


## Overview

Defines a result set.

It provides APIs to access the result set obtained by querying the RDB store.

**Since**

10

**Related Modules**

[RDB](_r_d_b.md)


## Summary


### Member Variables

| Name| Description|
| -------- | -------- |
| [id](_r_d_b.md) | Unique identifier of the **OH_Cursor** struct.|
| [getColumnCount](_r_d_b.md#getcolumncount) | Pointer to the function used to obtain the number of columns in the result set.|
| [getColumnType](_r_d_b.md#getcolumntype) | Pointer to the function used to obtain the column type based on the specified column index.|
| [getColumnIndex](_r_d_b.md#getcolumnindex) | Pointer to the function used to obtain the column index based on the specified column name.|
| [getColumnName](_r_d_b.md#getcolumnname) | Pointer to the function used to obtain the column name based on the specified column index.|
| [getRowCount](_r_d_b.md#getrowcount) | Pointer to the function used to obtain the number of rows in the result set.|
| [goToNextRow](_r_d_b.md#gotonextrow) | Pointer to the function used to go to the next row of the result set.|
| [getSize](_r_d_b.md#getsize) | Pointer to the function used to obtain information about the memory required when the column data type in the result set is **BLOB** or **TEXT**.|
| [getText](_r_d_b.md#gettext) | Pointer to the function used to obtain the value in the form of a string based on the specified column and the current row.|
| [getInt64](_r_d_b.md#getint64) | Pointer to the function used to obtain the value of the int64_t type based on the specified column and the current row.|
| [getReal](_r_d_b.md#getreal) | Pointer to the function used to obtain the value of the double type based on the specified column and the current row.|
| [getBlob](_r_d_b.md#getblob) | Pointer to the function used to obtain the value in the form of a byte array based on the specified column and the current row.|
| [isNull](_r_d_b.md#isnull-12) | Pointer to the function used to check whether the value in the specified column is null.|
| [close](_r_d_b.md#close) | Pointer to the function used to close a result set.|
