# Network Management Overview

Network management functions include:

- [HTTP data request](http-request.md): Initiates a data request through HTTP.
- [WebSocket connection](websocket-connection.md): Establishes a bidirectional connection between the server and client through WebSocket.
- [Socket connection](socket-connection.md): Transmits data through Socket.
- [Network sharing](net-sharing.md): Shares a device's Internet connection with other connected devices by means of Wi-Fi hotspot, Bluetooth, and USB sharing, and queries the network sharing state and shared mobile data volume.
- [Ethernet connection](net-ethernet.md): Provides wired network capabilities, which allow you to set the IP address, subnet mask, gateway, and Domain Name System (DNS) server of a wired network.
- [Network connection management](net-connection-manager.md): Provides basic network management capabilities, including management of Wi-Fi/cellular/Ethernet connection priorities, network quality evaluation, subscription to network connection status changes, query of network connection information, and DNS resolution.
- [mDNS management](net-mdns.md): provides Multicast DNS (mDNS) management capabilities, such as adding, removing, discovering, and resolving local services on a LAN.

## Constraints

To use the functions of the network management module, you must obtain the permissions listed in the following table.

| Permission                          | Description                                  |
| -------------------------------- | -------------------------------------- |
| ohos.permission.GET_NETWORK_INFO | Allows an application to obtain the network connection information.                    |
| ohos.permission.SET_NETWORK_INFO | Allows an application to modify the network connection state.                    |
| ohos.permission.INTERNET         | Allows an application to open network sockets to connect to the network.|
