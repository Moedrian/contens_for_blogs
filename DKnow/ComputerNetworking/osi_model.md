# Open Systems Interconnection Model

## Layers

<center><pre>
+--------------------+-------------------+--------------+
| Application Layer  |                   |              |
+--------------------+                   |              |
| Presentation Layer | Data              |              |
+--------------------+                   | Host Layers  |
| Session Layer      |                   |              |
+--------------------+-------------------+              |
| Transport Layer    | Segment, Datagram |              |
+--------------------+-------------------+--------------+
| Network Layer      | Packet            |              |
+--------------------+-------------------+              |
| Data Link Layer    | Frame             | Media Layers |
+--------------------+-------------------+              |
| Physical Layer     | Symbol            |              |
+--------------------+-------------------+--------------+
</pre></center>

---

### 1. Physical Layer

#### 1.1 Role

> Actual physical connection between the devices. When receiving data, this layer will get the signal received and convert it into bits then send them to Data Link Layer.

#### 1.2 The form of information

What is transmitted in this layer is **bit**, i.e.

<center><pre>
+----+----+----+
|0011|0100|1001|
+----+----+----+
</pre></center>

#### 1.3 The functions of Physical Layer

| Function | Explanation |
|:---|:---|
| Bit Synchronization | Bit level synchronization between  sender and receiver via a clock. |
| Bit Rate Control | Transmission rate i.e. the number of bits sent/received per second. |
| Physical Topologies | The way in which the different devices/nodes arranged in a network, i.e. bus, star or mesh topology. |
| Transmission Mode | The way in which data flows between the two connected devices. Simplex, half-duplex and full-duplex |

#### 1.4 Examples
Hub, Repeater, Modem, Cables are all in the Physical layer. Check those jargons [here](../Jargon/osi_jargon.md).

### 2. Data Link Layer

#### 2.1 Role

> The data link layer provides node-to-node data transfer—a link between two directly connected nodes.

> It detects and possibly corrects errors that may occur in the physical layer. 
> It defines the protocol to establish and terminate a connection between two physically connected devices.
> It also defines the protocol for flow control between them.

And it has two sublayers:

* Medium Access Control (MAC) layer
  > responsible for controlling how devices in a network gain access to a medium and permission to transmit data
* Logical Link Control (LLC) layer
  > responsible for identifying and encapsulating network layer protocols, and controls error checking and frame synchronization

#### 2.2 The form of information

Frame.

> In the OSI model of computer networking, a frame is the protocol data unit at the data link layer. Frames are the result of the final layer of encapsulation before the data is transmitted over the physical layer.

> A frame is "the unit of transmission in a link layer protocol, and consists of a link layer header followed by a packet." Each frame is separated from the next by an interframe gap.

> A frame is a series of bits generally composed of frame synchronization bits, the packet payload, and a frame check sequence.

#### 2.3 The functions of Data Link Layer

| Function | Explanation |
|:---|:---|
| Framing | It provides a way for sender to transmit a set of bits that are meaningful to the receiver. It is implemented by special bit patterns in the beginning and the end of the frame. |
| Physical Addressing | DLL adds MAC addresses of sender and/or receiver in the header of each frame. |
| Error Control | DLL detects and retransmit damaged or lost frames using mechanism built inside the layer. |
| Flow Control | The data rate *must* be constant between sender and receiver. Flow control coordinates the amount of data on both two sides. |
| Access Control | Suppose there's a single channel shared by multi devices, the MAC sublayer helps determine which device has control over the single channel at a given time. |

#### 2.4 Examples

Switches, Bridges.

### 3. Network Layer

#### 3.1 Role

> The network layer provides the functional and procedural means of transferring variable length data sequences (called packets) from one node to another connected in "different networks".

>  It also takes care of packet routing i.e. selection of the shortest path to transmit the packet, from the number of routes available. The sender & receiver’s IP address are placed in the header by network layer.

#### 3.2 Functions of Network Layer

| Function | Explanation |
|:---|:---|
| Routing | The Network Layer determines which route is suitable from source to destination. |
| Logical Addressing | The Network Layer maintains an address scheme to identify devices on internetwork uniquely. |

#### 3.3 The form of information

Packet. A packet consists of control information and user data, which is also known as payload.

#### 3.4 Examples

Routers.

---

### 4. Transport Layer

#### 4.1 Role

End to End delivery of the complete message. Transport layer also provides the acknowledgement of the successful data transmission and re-transmits the data if an error is found.

#### 4.2 Functions of Transport Layer

| Function | Explanation |
|:---|:---|
| Segmentation and Desegmentation (Reassembly) | This layer accepts the message from Session Layer then breaks message into small units. The destination station within this layer will reassembly these units. |
| Service Point Addressing | To deliver the message to correct process. |

#### 4.3 The form of information

Segment.

#### 4.4 Examples

The Transmission Control Protocol (TCP) and the User Datagram Protocol are commonly categorized as layer-4 protocols within OSI.

---

### 5. Session Layer

#### 5.1 Role

* Connection establishment 
* Maintenance of sessions
* Authentication
* Security Assurance

#### 5.2 The functions of Session Layer

| Function | Explanation |
|:---|:---|
| Session establishment, maintenance and termination | This layer allow the two processes to establish, use and terminate a connection.
| Synchronization | This layer allows a process to add checkpoints which are considered as synchronization points into the data to identify the error so that the integrity of data can be kept. |
| Dialog Controller | To allow two systems start a simplex, half-duplex or full-duplex connection. |

#### 5.3 Examples

Application environments that use Remote Procedure Calls (RPC).

### 6. Presentation Layer

#### 6.1 Role

The data from Application Layer is extracted here and manipulated as per the required format to transmit over the network.

#### 6.2 The functions of Presentation Layer

| Function | Explanation |
|:---|:---|
| Translation | E.g. ASCII to EBCDIC |
| Encryption/Decryption | E.g. Base64, Sha1, etc |
| Compression/Extraction | To reduces the number of bits. |

### 7. Application Layer

#### 7.1 Role

To produce the data.

#### 7.2 The functions of Application Layer

* Network Virtual Terminal
* FTAM-File transfer access and management
* Mail Services
* Directory Services

#### 7.3 Examples

Browsers, Messengers, etc.

## Reference

[Computer Network | Layers of OSI Model](https://www.geeksforgeeks.org/layers-osi-model/)