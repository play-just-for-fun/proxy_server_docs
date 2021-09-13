Basic architecture
---

###**Terms:**
- **VPN Admin** - **pc** with installed admin panel. This panel need for control **vpn agents**
- **VPN Agent (Gateway)** - **pc** that do all work for tunneling your devices. It acts as a router for your end devices.
Separate subnetwork created. Addresses in this range will be such as _10.1.0.10,10.1.0.240,etc_. 
- **Aggregation switch** - this switch need for aggregate **access switches** to single **vpn agent** network.
- **Access switch** - your end devices will be connected to this switch.
- **Caching server** - PC that acts as http cache server for your end devices.
- **End device** - device that connected to gateway. It can be pc,console etc.
- *portN* - ethernet port of switch/router/pc. N is a port number. For vpn agent port1 its mean first network card (connected to your primary network)
and port2 is second network card (connected to aggregate switch or access switch).

----


##### Top network architecture diagram
<!-- generated by mermaid compile action - START -->
![~mermaid diagram 1~](/.resources/docs_basics-md-1.svg)
<details>
  <summary>Mermaid markup</summary>

```mermaid
graph TB
subgraph -
WAN-->A
A[Your main router]-->|port2->port1| E[VPN admin]
A-->|port3->port1| B[VPN Agent 1]
A-->|port4->port1|D[VPN Agent ...]

end
```

</details>
<!-- generated by mermaid compile action - END -->
*Next you can use one of configuration*

## Configuration 1

*For small deployments lower than 40 end devices*

You connect  **access switch** to **vpn agent**.
Your end devices will be connected to **access switch** ports. **Cache server** is optional
<!-- generated by mermaid compile action - START -->
![~mermaid diagram 2~](/.resources/docs_basics-md-2.svg)
<details>
  <summary>Mermaid markup</summary>

```mermaid
graph TB
subgraph - 

B[VPN Agent]-->|port2->port1|swB1[Access switch 1]
swB1-->|port2|Cache1[Cache server]

swB1-->|port3|PC
swB1-->|port4|Dev1[Device 1]
swB1-->|port5|Dev2[Device 2]
swB1-->|portN|Dev3[Device n]


end
```

</details>
<!-- generated by mermaid compile action - END -->

## Configuration 2

*For medium or large deployments greater than 40 end devices*

You connect **aggregation switch** to **vpn agent**. Then you connect **access switches** to your **aggregate switch**.
Your end devices except **caching server** will be connected to **access switch** ports
<!-- generated by mermaid compile action - START -->
![~mermaid diagram 3~](/.resources/docs_basics-md-3.svg)
<details>
  <summary>Mermaid markup</summary>

```mermaid
graph TB
subgraph - 
B[VPN Agent]-->|port2->port1|AG1[Aggregation switch]
AG1-->|port2->port1|swB1[Access switch 1]
AG1-->|port3->port1|swB2[Access switch 2]
AG1-->|port4->port1|swB3[Access switch n]
AG1-->|port5->port1|Cache1[Cache server]

swB1-->|portN|PC1
swB1-->|portN|Dev1[Device 1]
swB1-->|portN|Dev2[Device 2]
swB1-->|portN|Dev3[Device n]

swB2-->|portN|PC2
swB2-->|portN|Dev12[Device 1]
swB2-->|portN|Dev22[Device 2]
swB2-->|portN|Dev32[Device n]

end
```

</details>
<!-- generated by mermaid compile action - END -->