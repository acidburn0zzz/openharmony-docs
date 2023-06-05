# Overview of Distributed Application Data Synchronization


## When to Use

The distributed application data synchronization allows the data of an application to be synchronized with other devices that are connected to form a Virtual Device. This feature enables seamless synchronization, modification, and query of use application data across trusted devices.

For example, when data is added, deleted, or modified for an application on a device, the same application on another device can obtain the updated data. You can use this feature in the distributed Gallery, Notepad, Contacts, and File Manager. 

For details about how to subscribe to database change notifications between different applications, see [Sharing Application Data with Other Applications](share-device-data-across-apps-overview.md).

The data storage modes vary depending on the lifecycle of data to be synchronized:

- Temporary data has a short lifecycle and is usually stored in memory. For example, distributed data objects are recommended for process data generated by game applications.

- Persistent data has a long lifecycle and needs to be stored in databases. You can use RDB stores or KV stores based on data characteristics and relationships. For example, RDB stores are recommended for storing Gallery attribute information, such as albums, covers, and images, and KV stores are recommended for storing Gallery image thumbnails.


## Basic Concepts

In a distributed scenario, cross-device collaboration demands consistent data between the devices in the same network.


The data consistency can be classified into the following types:


- Strong consistency: When data is inserted, deleted, or modified on a device, other devices in the same network can obtain the updates eventually, but may not immediately.

- Weak consistency: When data is added, deleted, or modified on a device, other devices in the same network may or may not obtain the updates. The data on these devices may be inconsistent after a certain period of time.

- Eventual consistency: When data is added, deleted, or modified on a device, other devices in the same network may not obtain the updates immediately. However, data on these devices will become consistent after a certain period of time.


Strong consistency has high requirements on distributed data management and may be used in distributed server deployment. Because mobile devices are not always online and there is no central node, the cross-device application data synchronization supports eventual consistency only.


## Access Control Mechanism in Cross-Device Synchronization

When data is synchronized across devices, access control is performed based on the device level and data security label. For details, see [Access Control Mechanism in Cross-Device Synchronization](access-control-by-device-and-data-level.md#access-control-mechanism-in-cross-device-synchronization).