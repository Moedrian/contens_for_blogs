# Open Systems Interconnection

## Layers

<pre>
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
</pre>

---
### 1. Physical Layer

Actual physical connection between the devices.

The form of information in this layer is **bit**, i.e.

<pre>
+----+----+----+
|0011|0100|1001|
+----+----+----+
</pre>

When receiving data, this layer will get the signal received and convert it into bits then send them to Data Link Layer.

The functions of Physical Layers are:

| Name | Explanation |
|:---|:---|
| Bit Synchronization | Bit level synchronization between  sender and receiver via a clock. |
| Bit Rate Control | Transmission rate i.e. the number of bits sent/received per second. |
| Physical Topologies | The way in which the different devices/nodes arranged in a network, i.e. bus, star or mesh topology. |
| Transmission Mode | The way in which data flows between the two connected devices. Simplex, half-duplex and full-duplex |

Hub, Repeater, Modem, Cables, etc. Check those jargons [here](../Jargon/osi_jargon.md).

### 2. Data Link Layer

Node to node delivery of message.

### 3. Network Layer
---
### 4. Transport Layer
---
### 5. Session Layer
### 6. Presentation Layer
### 7. Application Layer

## Reference

[Computer Network | Layers of OSI Model](https://www.geeksforgeeks.org/layers-osi-model/)