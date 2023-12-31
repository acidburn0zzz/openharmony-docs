# Persisting RDB Store Data


## When to Use

A relational database (RDB) store is used to store data in complex relational models, such as the student information including names, student IDs, and scores of each subject, or employee information including names, employee IDs, and positions, based on SQLite. The data is more complex than key-value (KV) pairs due to strict mappings. You can use **RelationalStore** to implement persistence of this type of data.


## Basic Concepts

- **Predicates**: A representation of the property or feature of a data entity, or the relationship between data entities. It is used to define operation conditions.

- **ResultSet**: a set of query results, which allows access to the required data in flexible modes.


## Working Principles

**RelationalStore** provides APIs for applications to perform data operations. With SQLite as the underlying persistent storage engine, **RelationalStore** provides SQLite database features, including transactions, indexes, views, triggers, foreign keys, parameterized queries, prepared SQL statements, and more.

**Figure 1** Working mechanism
 
![relationStore_local](figures/relationStore_local.jpg)


## Constraints

- The default logging mode is Write Ahead Log (WAL), and the default flushing mode is **FULL** mode.

- An RDB store can be connected to a maximum of four connection pools for user read operations.

- To ensure data accuracy, only one write operation is allowed at a time.

- Once an application is uninstalled, related database files and temporary files on the device are automatically deleted.


## Available APIs

The following table lists the APIs used for RDB data persistence. Most of the APIs are executed asynchronously, using a callback or promise to return the result. The following table uses the callback-based APIs as an example. For more information about the APIs, see [RDB Store](../reference/apis/js-apis-data-relationalStore.md).

| API| Description| 
| -------- | -------- |
| getRdbStore(context: Context, config: StoreConfig, callback: AsyncCallback&lt;RdbStore&gt;): void | Obtains a **RdbStore** instance to implement RDB store operations. You can set **RdbStore** parameters based on actual requirements and use **RdbStore** APIs to perform data operations.| 
| executeSql(sql: string, bindArgs: Array&lt;ValueType&gt;, callback: AsyncCallback&lt;void&gt;):void | Executes an SQL statement that contains specified arguments but returns no value.| 
| insert(table: string, values: ValuesBucket, callback: AsyncCallback&lt;number&gt;):void | Inserts a row of data into a table.| 
| update(values: ValuesBucket, predicates: RdbPredicates, callback: AsyncCallback&lt;number&gt;):void | Updates data in the RDB store based on the specified **RdbPredicates** instance.| 
| delete(predicates: RdbPredicates, callback: AsyncCallback&lt;number&gt;):void | Deletes data from the RDB store based on the specified **RdbPredicates** instance.| 
| query(predicates: RdbPredicates, columns: Array&lt;string&gt;, callback: AsyncCallback&lt;ResultSet&gt;):void | Queries data in the RDB store based on specified conditions.| 
| deleteRdbStore(context: Context, name: string, callback: AsyncCallback&lt;void&gt;): void | Deletes an RDB store.| 


## How to Develop

1. Obtain an **RdbStore** instance.<br> Example:

   Stage model:
     
   ```js
   import relationalStore from '@ohos.data.relationalStore'; // Import the module.
   import UIAbility from '@ohos.app.ability.UIAbility';

   class EntryAbility extends UIAbility {
     onWindowStageCreate(windowStage) {
       const STORE_CONFIG = {
         name: 'RdbTest.db', // Database file name.
         securityLevel: relationalStore.SecurityLevel.S1 // Database security level.
       };

       // The current RDB store version is 3, and the table structure is EMPLOYEE (NAME, AGE, SALARY, CODES).
       const SQL_CREATE_TABLE ='CREATE TABLE IF NOT EXISTS EMPLOYEE (ID INTEGER PRIMARY KEY AUTOINCREMENT, NAME TEXT NOT NULL, AGE INTEGER, SALARY REAL, CODES BLOB)'; // SQL statement for creating a data table.

       relationalStore.getRdbStore(this.context, STORE_CONFIG, (err, store) => {
         if (err) {
           console.error(`Failed to get RdbStore. Code:${err.code}, message:${err.message}`);
           return;
         }
         console.info(`Succeeded in getting RdbStore.`);

        // When the RDB store is created, the default version is 0.
        if (store.version == 0) {
          store.executeSql(SQL_CREATE_TABLE); // Create a data table.
          // Set the RDB store version, which must be an integer greater than 0.
          store.version = 3;
        }

        // If the RDB store version is not 0 and does not match the current version, upgrade or downgrade the RDB store.
        // For example, upgrade the RDB store from version 1 to version 2.
        if (store.version != 3 && store.version == 1) {
          // Upgrade the RDB store from version 1 to version 2, and change the table structure from EMPLOYEE (NAME, SALARY, CODES, ADDRESS) to EMPLOYEE (NAME, AGE, SALARY, CODES, ADDRESS).
          store.executeSql("ALTER TABLE EMPLOYEE ADD COLUMN AGE INTEGER", null);
          store.version = 2;
        }

        // For example, upgrade the RDB store from version 2 to version 3.
        if (store.version != 3 && store.version == 2) {
          // Upgrade the RDB store from version 2 to version 3, and change the table structure from EMPLOYEE (NAME, AGE, SALARY, CODES, ADDRESS) to EMPLOYEE (NAME, AGE, SALARY, CODES).
          store.executeSql("ALTER TABLE EMPLOYEE DROP COLUMN ADDRESS TEXT", null);
          store.version = 3;
        }

         // Perform operations such as adding, deleting, modifying, and querying data in the RDB store.

       });
     }
   }
   ```

   FA model:

     
   ```js
   import relationalStore from '@ohos.data.relationalStore'; // Import the module.
   import featureAbility from '@ohos.ability.featureAbility';
   
   // Obtain the context.
   let context = featureAbility.getContext();
   
   const STORE_CONFIG = {
     name: 'RdbTest.db', // Database file name.
     securityLevel: relationalStore.SecurityLevel.S1 // Database security level.
   };

   // The RDB store version is 3, and the table structure is EMPLOYEE (NAME, AGE, SALARY, CODES).
   const SQL_CREATE_TABLE ='CREATE TABLE IF NOT EXISTS EMPLOYEE (ID INTEGER PRIMARY KEY AUTOINCREMENT, NAME TEXT NOT NULL, AGE INTEGER, SALARY REAL, CODES BLOB)'; // SQL statement for creating a data table.

   relationalStore.getRdbStore(context, STORE_CONFIG, (err, store) => {
     if (err) {
       console.error(`Failed to get RdbStore. Code:${err.code}, message:${err.message}`);
       return;
     }
     console.info(`Succeeded in getting RdbStore.`);

     // When the RDB store is created, the default version is 0.
     if (store.version == 0) {
        store.executeSql(SQL_CREATE_TABLE); // Create a data table.
        // Set the RDB store version, which must be an integer greater than 0.
        store.version = 3;
     }

     // If the RDB store version is not 0 and does not match the current version, upgrade or downgrade the RDB store.
     // For example, upgrade the RDB store from version 1 to version 2.
     if (store.version != 3 && store.version == 1) {
        // Upgrade the RDB store from version 1 to version 2, and change the table structure from EMPLOYEE (NAME, SALARY, CODES, ADDRESS) to EMPLOYEE (NAME, AGE, SALARY, CODES, ADDRESS).
        store.executeSql("ALTER TABLE EMPLOYEE ADD COLUMN AGE INTEGER", null);
        store.version = 2;
     }

     // For example, upgrade the RDB store from version 2 to version 3.
     if (store.version != 3 && store.version == 2) {
        // Upgrade the RDB store from version 2 to version 3, and change the table structure from EMPLOYEE (NAME, AGE, SALARY, CODES, ADDRESS) to EMPLOYEE (NAME, AGE, SALARY, CODES).
        store.executeSql("ALTER TABLE EMPLOYEE DROP COLUMN ADDRESS TEXT", null);
        store.version = 3;
     }
   
     // Perform operations such as adding, deleting, modifying, and querying data in the RDB store.
   
   });
   ```

   > **NOTE**
   >
   > - The RDB store created by an application varies with the context. Multiple RDB stores are created for the same database name with different application contexts. For example, each UIAbility has its own context.
   > 
   > - When an application calls **getRdbStore()** to obtain an RDB store instance for the first time, the corresponding database file is generated in the application sandbox. If you want to move the files of an RDB store to another place for view, you must also move the temporary files with finename extensions **-wal** or **-shm** in the same directory. Once an application is uninstalled, the database files and temporary files generated by the application on the device are also removed.

2. Use **insert()** to insert data to the RDB store. Example:
     
   ```js
   const valueBucket = {
     'NAME': 'Lisa',
     'AGE': 18,
     'SALARY': 100.5,
     'CODES': new Uint8Array([1, 2, 3, 4, 5])
   };
   store.insert('EMPLOYEE', valueBucket, (err, rowId) => {
     if (err) {
       console.error(`Failed to insert data. Code:${err.code}, message:${err.message}`);
       return;
     }
     console.info(`Succeeded in inserting data. rowId:${rowId}`);
   })
   ```

   > **NOTE**
   >
   > **RelationalStore** does not provide explicit flush operations for data persistence. Data inserted by **insert()** is stored in files persistently.

3. Modify or delete data based on the specified **Predicates** instance.

   Use **update()** to modify data and **delete()** to delete data. 

   Example:

   ```js
   // Modify data.
   const valueBucket = {
     'NAME': 'Rose',
     'AGE': 22,
     'SALARY': 200.5,
     'CODES': new Uint8Array([1, 2, 3, 4, 5])
   };
   let predicates = new relationalStore.RdbPredicates('EMPLOYEE'); // Create predicates for the table named EMPLOYEE.
   predicates.equalTo('NAME', 'Lisa'); // Modify the data of Lisa in the EMPLOYEE table to the specified data.
   store.update(valueBucket, predicates, (err, rows) => {
     if (err) {
       console.error(`Failed to update data. Code:${err.code}, message:${err.message}`);
       return;
     }
     console.info(`Succeeded in updating data. row count: ${rows}`);
   })
   
   // Delete data.
   let predicates = new relationalStore.RdbPredicates('EMPLOYEE');
   predicates.equalTo('NAME', 'Lisa');
   store.delete(predicates, (err, rows) => {
     if (err) {
       console.error(`Failed to delete data. Code:${err.code}, message:${err.message}`);
       return;
     }
     console.info(`Delete rows: ${rows}`);
   })
   ```

4. Query data based on the conditions specified by **Predicates**.

   Use **query()** to query data. The data obtained is returned in a **ResultSet** object. 

   Example:

   ```js
   let predicates = new relationalStore.RdbPredicates('EMPLOYEE');
   predicates.equalTo('NAME', 'Rose');
   store.query(predicates, ['ID', 'NAME', 'AGE', 'SALARY'], (err, resultSet) => {
     if (err) {
       console.error(`Failed to query data. Code:${err.code}, message:${err.message}`);
       return;
     }
     console.info(`ResultSet column names: ${resultSet.columnNames}, column count: ${resultSet.columnCount}`);
     // resultSet is a cursor of a data set. By default, the cursor points to the -1st record. Valid data starts from 0.
     while (resultSet.goToNextRow()) {
       const id = resultSet.getLong(resultSet.getColumnIndex("ID"));
       const name = resultSet.getString(resultSet.getColumnIndex("NAME"));
       const age = resultSet.getLong(resultSet.getColumnIndex("AGE"));
       const salary = resultSet.getDouble(resultSet.getColumnIndex("SALARY"));
       console.info(`id=${id}, name=${name}, age=${age}, salary=${salary}`);
     }
     // Release the data set memory.
     resultSet.close();
   })
   ```

   > **NOTE**
   >
   > Use **close()** to close the **ResultSet** that is no longer used in a timely manner so that the memory allocated can be released.

5. Delete the RDB store.

   Use **deleteRdbStore()** to delete the RDB store and related database files. 

   Example:

   Stage model:

     
   ```js
   import UIAbility from '@ohos.app.ability.UIAbility';
   
   class EntryAbility extends UIAbility {
     onWindowStageCreate(windowStage) {
       relationalStore.deleteRdbStore(this.context, 'RdbTest.db', (err) => {
         if (err) {
           console.error(`Failed to delete RdbStore. Code:${err.code}, message:${err.message}`);
           return;
         }
         console.info('Succeeded in deleting RdbStore.');
       });
     }
   }
   ```

   FA model:

     
   ```js
   import featureAbility from '@ohos.ability.featureAbility';
   
   // Obtain the context.
   let context = featureAbility.getContext();
   
   relationalStore.deleteRdbStore(context, 'RdbTest.db', (err) => {
     if (err) {
       console.error(`Failed to delete RdbStore. Code:${err.code}, message:${err.message}`);
       return;
     }
     console.info('Succeeded in deleting RdbStore.');
   });
   ```
