# @ohos.data.dataShareResultSet (DataShare Result Set)

The **DataShareResultSet** module provides APIs for accessing the result set obtained from the database. You can access the values in the specified rows or the value of the specified data type.

> **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>
> The APIs provided by this module are system APIs.


## Modules to Import

```ts
import DataShareResultSet from '@ohos.data.DataShareResultSet';
```

## Usage

You can call [query()](js-apis-data-dataShare.md#query) to obtain the **DataShareResultSet** object.

```ts
import dataShare from '@ohos.data.dataShare';
import dataSharePredicates from '@ohos.data.dataSharePredicates'

let dataShareHelper;
let uri = ("datashare:///com.samples.datasharetest.DataShare");
await dataShare.createDataShareHelper(this.context, uri, (err, data) => {
	if (err != undefined) {
        console.error("createDataShareHelper fail, error message : " + err);
    } else {
        console.info("createDataShareHelper end, data : " + data);
        dataShareHelper = data;
    }
});

let columns = ["*"];
let da = new dataSharePredicates.DataSharePredicates();
let resultSet;
da.equalTo("name", "ZhangSan");
dataShareHelper.query(uri, da, columns).then((data) => {
    console.info("query end, data : " + data);
    resultSet = data;
}).catch((err) => {
	console.error("query fail, error message : " + err);
});
```

## DataShareResultSet
Provides methods for accessing the result sets generated by querying the database.

### Attributes

**System capability**: SystemCapability.DistributedDataManager.DataShare.Core

| Name       | Type     | Mandatory| Description                    |
| ----------- | ------------- | ---- | ------------------------ |
| columnNames | Array&lt;string&gt; | Yes  | Names of all columns in the result set.  |
| columnCount | number        | Yes  | Number of columns in the result set.        |
| rowCount    | number        | Yes  | Number of rows in the result set.        |
| isClosed    | boolean       | Yes  | Whether the result set is closed.|

### goToFirstRow

goToFirstRow(): boolean

Moves to the first row of the result set.

**System capability**: SystemCapability.DistributedDataManager.DataShare.Core

**Return value**

| Type   | Description                                         |
| :------ | --------------------------------------------- |
| boolean | Returns **true** if the operation is successful; returns **false** otherwise.|

**Example**

```ts
let isGoTOFirstRow = resultSet.goToFirstRow();
console.info('resultSet.goToFirstRow: ' + isGoTOFirstRow);
```

### goToLastRow

goToLastRow(): boolean

Moves to the last row of the result set.

**System capability**: SystemCapability.DistributedDataManager.DataShare.Core

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Returns **true** if the operation is successful; returns **false** otherwise.|

**Example**

```ts
let isGoToLastRow = resultSet.goToLastRow();
console.info('resultSet.goToLastRow: ' + isGoToLastRow);
```

### goToNextRow

goToNextRow(): boolean

Moves to the next row in the result set.

**System capability**: SystemCapability.DistributedDataManager.DataShare.Core

**Return value**

| Type   | Description                                         |
| ------- | --------------------------------------------- |
| boolean | Returns **true** if the operation is successful; returns **false** otherwise.|

**Example**

```ts
let isGoToNextRow = resultSet.goToNextRow();
console.info('resultSet.goToNextRow: ' + isGoToNextRow);
```

### goToPreviousRow

goToPreviousRow(): boolean

Moves to the previous row in the result set.

**System capability**: SystemCapability.DistributedDataManager.DataShare.Core

**Return value**

| Type   | Description                                         |
| ------- | --------------------------------------------- |
| boolean | Returns **true** if the operation is successful; returns **false** otherwise.|

**Example**

```ts
let isGoToPreviousRow = resultSet.goToPreviousRow();
console.info('resultSet.goToPreviousRow: ' + isGoToPreviousRow);
```

### goTo

goTo(offset:number): boolean

Moves based on the specified offset.

**System capability**: SystemCapability.DistributedDataManager.DataShare.Core

**Parameters**

| **Name**| **Type**| **Mandatory**| Description                                                        |
| ---------- | -------- | -------- | ------------------------------------------------------------ |
| offset     | number   | Yes      | Offset relative to the current position. A negative value means to move backward, and a positive value means to move forward.|

**Return value**

| Type   | Description                                         |
| ------- | --------------------------------------------- |
| boolean | Returns **true** if the operation is successful; returns **false** otherwise.|

**Example**

```ts
let goToNum = 1;
let isGoTo = resultSet.goTo(goToNum);
console.info('resultSet.goTo: ' + isGoTo);
```

### goToRow

goToRow(position: number): boolean

Moves to the specified row in the result set.

**System capability**: SystemCapability.DistributedDataManager.DataShare.Core

**Parameters**

| **Name**| **Type**| **Mandatory**| Description                    |
| ---------- | -------- | -------- | ------------------------ |
| position   | number   | Yes      | Destination position to move to.|

**Return value**

| Type   | Description                                         |
| ------- | --------------------------------------------- |
| boolean | Returns **true** if the operation is successful; returns **false** otherwise.|

**Example**

```ts
let goToRowNum = 2;
let isGoToRow = resultSet.goToRow(goToRowNum);
console.info('resultSet.goToRow: ' + isGoToRow);
```

### getBlob

getBlob(columnIndex: number): Uint8Array

Obtains the value in the form of a byte array based on the specified column and the current row.

**System capability**: SystemCapability.DistributedDataManager.DataShare.Core

**Parameters**

| **Name** | **Type**| **Mandatory**| Description                   |
| ----------- | -------- | -------- | ----------------------- |
| columnIndex | number   | Yes      | Index of the target column, starting from 0.|

**Return value**

| Type      | Description                            |
| ---------- | -------------------------------- |
| Uint8Array | Value obtained.|

**Example**

```ts
let columnIndex = 1;
let goToFirstRow = resultSet.goToFirstRow();
let getBlob = resultSet.getBlob(columnIndex);
console.info('resultSet.getBlob: ' + getBlob);
```

### getString

getString(columnIndex: number): string

Obtains the value in the form of a string based on the specified column and the current row.

**System capability**: SystemCapability.DistributedDataManager.DataShare.Core

**Parameters**

| **Name** | **Type**| **Mandatory**| Description                   |
| ----------- | -------- | -------- | ----------------------- |
| columnIndex | number   | Yes      | Index of the target column, starting from 0.|

**Return value**

| Type  | Description                        |
| ------ | ---------------------------- |
| string | Value obtained.|

**Example**

```ts
let columnIndex = 1;
let goToFirstRow = resultSet.goToFirstRow();
let getString = resultSet.getString(columnIndex);
console.info('resultSet.getString: ' + getString);
```

### getLong

getLong(columnIndex: number): number

Obtains the value in the form of a long integer based on the specified column and the current row.

**System capability**: SystemCapability.DistributedDataManager.DataShare.Core

**Parameters**

| **Name** | **Type**| **Mandatory**| Description                   |
| ----------- | -------- | -------- | ----------------------- |
| columnIndex | number   | Yes      | Index of the target column, starting from 0.|

**Return value**

| Type  | Description                      |
| ------ | -------------------------- |
| number | Value obtained.|

**Example**

```ts
let columnIndex = 1;
let goToFirstRow = resultSet.goToFirstRow();
let getLong = resultSet.getLong(columnIndex);
console.info('resultSet.getLong: ' + getLong);
```

### getDouble

getDouble(columnIndex: number): number

Obtains the value in the form of a double-precision floating-point number based on the specified column and the current row.

**System capability**: SystemCapability.DistributedDataManager.DataShare.Core

**Parameters**

| **Name** | **Type**| **Mandatory**| Description                   |
| ----------- | -------- | -------- | ----------------------- |
| columnIndex | number   | Yes      | Index of the target column, starting from 0.|

**Return value**

| Type  | Description                        |
| ------ | ---------------------------- |
| number | Value obtained.|

**Example**

```ts
let columnIndex = 1;
let goToFirstRow = resultSet.goToFirstRow();
let getDouble = resultSet.getDouble(columnIndex);
console.info('resultSet.getDouble: ' + getDouble);
```

### close

close(): void

Closes this result set.

**System capability**: SystemCapability.DistributedDataManager.DataShare.Core

**Example**

```ts
resultSet.close();
```

### getColumnIndex

getColumnIndex(columnName: string): number

Obtains the column index based on the column name.

**System capability**: SystemCapability.DistributedDataManager.DataShare.Core

**Parameters**

| **Name**| **Type**| **Mandatory**| Description                      |
| ---------- | -------- | -------- | -------------------------- |
| columnName | string   | Yes      | Column name.|

**Return value**

| Type  | Description              |
| ------ | ------------------ |
| number | Column index obtained.|

**Example**

```ts
let ColumnName = "name";
let getColumnIndex = resultSet.getColumnIndex(ColumnName);
console.info('resultSet.getColumnIndex: ' + getColumnIndex);
```

### getColumnName

getColumnName(columnIndex: number): string

Obtains the column name based on the column index.

**System capability**: SystemCapability.DistributedDataManager.DataShare.Core

**Parameters**

| **Name** | **Type**| **Mandatory**| Description                      |
| ----------- | -------- | -------- | -------------------------- |
| columnIndex | number   | Yes      | Column index.|

**Return value**

| Type  | Description              |
| ------ | ------------------ |
| string | Column name obtained.|

**Example**

```ts
let columnIndex = 1;
let getColumnName = resultSet.getColumnName(columnIndex);
console.info('resultSet.getColumnName: ' + getColumnName);
```

### getDataType

getDataType(columnIndex: number): DataType

Obtains the data type based on the specified column index.

**System capability**: SystemCapability.DistributedDataManager.DataShare.Core

**Parameters**

| **Name** | **Type**| **Mandatory**| Description                      |
| ----------- | -------- | -------- | -------------------------- |
| columnIndex | number   | Yes      | Column index.|

**Return value**

| Type                 | Description              |
| --------------------- | ------------------ |
| [DataType](#datatype) | Data type obtained.|

**Example**

```ts
let columnIndex = 1;
let getDataType = resultSet.getDataType(columnIndex);
console.info('resultSet.getDataType: ' + getDataType);
```

## DataType

Enumerates the data types.

**System capability**: SystemCapability.DistributedDataManager.DataShare.Core

| Name       | Value| Description                |
| ----------- | ------ | -------------------- |
| TYPE_NULL   | 0      | Null.    |
| TYPE_LONG   | 1      | Long integer.  |
| TYPE_DOUBLE | 2      | Double-precision floating-point number.|
| TYPE_STRING | 3      | String.|
| TYPE_BLOB   | 4      | Byte array.|
