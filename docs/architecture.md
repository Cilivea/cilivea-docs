![architecture flowchart](/resources/cilivea_architecture_flowchart.svg)
The architecture is segmented into two parts, the local devices and the remote devices.

# Block
The blocks are the fundamental datapoints of a system. These can be sensors like temperature, light, sound, humidity, etc, or actuators like motors, lights, heaters etc.
A block is normally just a single datapoint, however, a complex datatype that maps multiple blocks into a structure can also be defined.
For more info about blocks, see [here](./blocks.md)

# Gateway
The gateway is responsible for all setup, security, and communication with blocks. The protocol used between gateway and block is not in this spec, as this is up for individual implementation.

The gateway must implement a [CIL/GW client](./CIL_GW.md).

# Edge
The edge is comprised of two parts, a data link layer (called data aggregator in the chart), and an automation API.
The data links purpose is simply to provide an entry point that the gateway can send and receive values, whilst the automation API authenticates events from the automation servers, and sends live data to the datastore server. This is the edge's security layer agains an attack from the automation server and local API.

The edge must implement a [CIL/GW server](./CIL_GW.md).
The edge must implement a [CIL/AU server](./CIL_AU.md).
The edge must implement a [CIL/DB client](./CIL_DB.md).

# Datastore
The datastores have the responsibility of storing data of the sensors, be that historical telemetry data, or simply the last updated values of the blocks.

This is the first service that includes a cloud sync option. If the datastore is configured for it, the datastore may be synced with a cloud datastore. This is explained in the [SYNC/DB](./SYNC_DB.md) spec.

Note that if the cloud connection disappears, the system will still continue to function in real-time.

The local datastore must implement a [CIL/DB server](./CIL_DB.md)
The local datastore must implement a [CIL/DS server](./CIL_DS.md)
The local datastore must implement a [CIL/AS client](./CIL_AS.md)
The local datastore may implement a [SYNC/DB client](./SYNC_DB.md)

# Automation server
The automation server stores and executes automation scripts.

The automation server includes a cloud syc option, similar to above. This is in the [SYNC/AU](./SYNC_AU.md) spec.

The local automation server must implement a [CIL/AS server](./CIL_AS.md)
The local automation server must implement a [CIL/AUSYNC server](./CIL_AUSYNC.md)
The local automation server must implement a [CIL/AU client](./CIL_AU.md)
The local automation server may implement a [SYNC/AU client](./SYNC_AU.md)

# Authenticated API
This is the public-facing API for the framework. The API serves as a secured access point to interact with block devices, and automations.

The API must implement a [CIL/AUSYNC client](./CIL_AUSYNC.md)
The API must implement a [CIL/DS client](./CIL_DS.md)
The API must implement a [CIL/US client](./CIL_US.md)
The API must implement a [CIL/RT server](./CIL_RT.md)
The API must implement a [CIL/PL server](./CIL_PL.md)


# User store
This is the database that stores user information, such as usernames, contact info, etc.

The user store includes a cloud sync option. This is in the [SYNC/US](./SYNC_US.md) spec.

The user store must implement a [CIL/US server](./CIL_US.md)
The user store may implement a [SYNC/US client](./SYNC_US.md)

# GUI
This is the final step for reaching the client. This is the part that hosts the dashboards. How dashboards are stored is implementation specific, as the goal is a unified communication protocol and structure.

The GUI must implement a [CIL/RT client](./CIL_RT.md)
The GUI must implement a [CIL/PL client](./CIL_PL.md)