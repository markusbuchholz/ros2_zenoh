# ROS 2 with Zenoh RMW


## Problems with DDS in ROS 2:
 - Complex Setup and Configuration: DDS in ROS 2 requires detailed configuration and setup, often involving complex environment variables and ```XML``` configuration files.
 
- Unreliable Performance in Flaky Networks: DDS relies heavily on the stability of the network. In environments with unstable or unreliable networks (such as flaky Wi-Fi), DDS can struggle to maintain reliable communication between nodes. Messages may not get through, and topics can disappear unexpectedly, leading to unreliable system performance.

- Network Overload and Interference: DDS can generate significant network traffic, which may lead to network flooding, especially in environments with multiple nodes or high-frequency messaging. 

- Limited Flexibility for Different Communication Needs: DDS was primarily designed for local network communication, making it less flexible for scenarios that require communication across different networks, such as over the internet or in cloud-based applications. It does not natively support more complex or distributed communication patterns without significant configuration.

## How Zenoh Can Help:

- Simplified Configuration and Setup: Zenoh offers a more straightforward setup process compared to DDS, reducing the need for complex configuration files and environment settings.

- Enhanced Network Resilience: Zenoh is designed to handle unreliable networks more effectively than DDS. It uses a ```router-based``` architecture that can better manage message delivery and maintain communication even when network conditions are unstable or when nodes are distributed across different networks.

- Efficient Communication and Reduced Network Load: Zenoh reduces network load by facilitating direct communication between nodes when possible and using routers for initial discovery and coordination. This approach helps prevent the network flooding and interference issues commonly associated with DDS, leading to more efficient and reliable communication.

 - Greater Flexibility for Distributed and Cloud-Based Applications: Zenoh is built to support both local and internet-based communications, making it ideal for cloud-based or geographically distributed systems. It allows for secure communication over the internet without requiring a VPN, providing a flexible solution for modern robotic applications that need to operate across different networks and locations.

 - Support for Non-DDS Communication Protocols: Zenoh is not limited to DDS protocols, providing greater flexibility in choosing communication mechanisms that best suit the application's needs. This makes it a versatile option for various scenarios, from local peer-to-peer communications to cloud-based setups.


## Build

```bash

sudo ./build.sh

```


## Run

```bash

sudo ./run.sh

```

## Links

- [zenoh-plugin](https://github.com/eclipse-zenoh/zenoh-plugin-ros2dds)
- [Zenoh documentation](https://zenoh.io/)
- [No more broken comms!](https://www.youtube.com/watch?v=fS0_rbQ6KKA&t=2s)
