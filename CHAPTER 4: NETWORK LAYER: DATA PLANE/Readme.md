# CHAPTER 4: THE NETWORK LAYER: DATA PLANE

## NETWORK LAYER OVERVIEW


1. THE NETWORK LAYER - WHERE IS IT?

    Check all of the statements below about where (in the network) the network layer is implemented that are true.

    - [ ] The network layer is implemented in Ethernet switches in a local area network. (False, Ethernet switches operate at the data link layer, not the network layer)

    - [x] The network layer is implemented in hosts at the network's edge. (True, hosts at the network's edge, such as computers and servers, do implement the network layer)

    - [ ] The network layer is implemented in wired Internet-connected devices but not wireless Internet-connected devices. (False, the network layer is implemented in both wired and wireless Internet-connected devices)

    - [x] The network layer is implemented in routers in the network core. (True, routers operate at the network layer)

2. FORWARDING VERSUS ROUTING. 
    
    Consider the travel analogy discussed in the textbook - some actions we take on a trip correspond to forwarding and other actions we take on a trip correspond to routing.  Which of the following travel actions below correspond to forwarding? The other travel actions that you don't select below then correspond to routing.  

    - [ ] A car takes highway 80 between New York and Chicago, rather than highway 87 to Albany and from there take Interstate 90 to Chicago.

    - [ ] A climber decides to take the South Col Route to the top of Mt Everest rather than the Northeast Ridge route.

    - [x] A car waits at light and then turns left at the intersection.

    - [x] A car stops at an intersection to “gas-up” and take a “bathroom break”

    - [ ] A traveler decides to fly to Sydney through Singapore rather that Dubai.

    - [x] A car takes the 3rd exit from a roundabout.

3. THE CONTROL PLANE VERSUS THE DATA PLANE
    
    For each of the actions below, select those actions below that are primarily in the network-layer data plane. The other actions that you don't select below then correspond to control-plane actions.  

    - [x] Moving an arriving datagram from a router’s input port to output port

    - [x] Looking up address bits in an arriving datagram header in the forwarding table.

    - [ ] Monitoring and managing the configuration and performance of an network device.

    - [ ] Computing the contents of the forwarding table.

    - [x] Dropping a datagram due to a congested (full) output buffer. 

4. WHAT TYPE OF CONTROL PLANE?

    We've seen that there are two approaches towards implementing the network control plane - a per-router control-plane approach and a software-defined networking (SDN) control-plane approach.  Which of the following actions occur in a per-router control-plane approach? The other actions that you don't select below then correspond to actions in an SDN control plane.  

    - [x] A router exchanges messages with another router, indicating the cost for it (the sending router) to reach a destination host.

    - [x] Routers send information about their incoming and outgoing links to other routers in the network.

    - [ ] A control agent in router receives a complete forwarding table, which it installs and
    uses to locally control datagram forwarding.

    - [ ] All routers in the network send information about their incoming and outgoing links to a logically centralized controller.

5. BEST EFFORT SERVICE.

    Which of the following quality-of-service guarantees are part of the Internet’s best-effort service model? Check all that apply.
 
    - [ ] Guaranteed delivery from sending host to receiving host.

    - [ ] In-order datagram payload delivery to the transport layer of those datagrams arriving to the receiving host.

    - [ ] A guaranteed minimum bandwidth is provided to a source-to-destination flow of packets

    - [ ] Guaranteed delivery time from sending host to receiving host.

    - [x] None of the other services listed here are part of the best-effort service model. Evidently, best-effort service really means no guarantees at all!

## Whats Inside a Router?

1. WHAT'S INSIDE A ROUTER?

    Match the names of the principal router components (A,B,C,D below) with their function and whether they are in the network-layer data plane or control plane.

    ![Alt text](https://gaia.cs.umass.edu/kurose_ross/LMS/images/Chapter_4_KC/KC4.2a.jpg)

    - **A**:  input ports, operating primarily in the data plane

    - **B**:  the switching fabric, operating primarily in the data plane.

    - **C**:  output ports, operating primarily in the data plane.

    - **D**:  the routing processor, operating primarily in the control plane.


2. WHERE DOES DESTINATION ADDRESS LOOKUP HAPPEN?

    Where in a router is the destination IP address looked up in a forwarding table to determine the appropriate output port to which the datagram should be directed?

    - [ ] Within the routing processor.


    - [x] At the input port where a packet arrives.

    - [ ] At the output port leading to the next hop towards the destination.

    - [ ] Within the switching fabric. 

3. WHERE DOES "MATCH+ACTION" HAPPEN?

    Where in a router does "match plus action" happen to determine the appropriate output port to which the arriving datagram should be directed?

    - [ ] Within the routing processor.

    - [x] At the input port where a packet arrives.

    - [ ] Within the switching fabric.

    - [ ] At the output port leading to the next hop towards the destination.

3. LONGEST PREFIX MATCHING.

    Consider the following forwarding table below. Indicate the output to link interface to which a datagram with the destination addresses below will be forwarded under longest prefix matching. (Note: The list of addresses is ordered below. If two addresses map to the same output link interface, map the first of these two addresses to the first  instance of that link interface.)

    ![Alt text](https://gaia.cs.umass.edu/kurose_ross/LMS/images/Chapter_4_KC/longest_prefix_match_a.jpg)

   **QUESTION LIST:**
    
        11001000 00010111 00010010 10101101: 
        - This is the first destination address in the list that maps to output port 0.

        11001000 00010111 00011000 00001101: 
        - This is the first destination address in the list that maps to output port 1.

        11001000 00010111 00011001 11001101:
        - This is the first destination address in the list that maps to output port 2.

        10001000 11100000 00011000 00001101:
        - This is the first destination address in the list that maps to output port 3.

        11001000 00010111 00011000 11001111:
        - This is the second destination address in the list that maps to output port 1.

        11001000 00010111 00010001 01010101:
        - This is the second destination address in the list that maps to output port 0.

        11001000 00010111 00011101 01101101:
        - This is the second destination address in the list that maps to output port 2.

5. PACKET DROPPING.

Suppose a datagram is switched through the switching fabric and arrives to its appropriate output to find that there are no free buffers.  In this case:

- [x] The packet will either be dropped or another packet will be removed (lost) from the buffer to make room for this packet, depending on policy.  But the packet will definitely not be be sent back to the input port.

- [ ] The packet will be dropped (lost).

- [ ] The packet will be sent back to the input port.

- [ ] Another packet will be removed (lost) from the buffer to make room for this packet.

6. HOL BLOCKING.

    What is meant by Head of the Line (HOL) blocking?

    - [x] A queued datagram waiting for service at the front of a queue prevents other datagrams in queue from moving forward in the queue.

    - [ ] A queued datagram receiving service at the front of a queue prevents other datagrams in queue from receiving service.

    - [ ] In a block error code, the first bytes of the code indicate the type of coding being used.

7. PACKET SCHEDULING (SCENARIO 1, FCFS).

    Consider the pattern of red and green packet arrivals to a router’s output port queue, shown below. Suppose each packet takes one time slot to be transmitted, and can only begin transmission at the beginning of a time slot after its arrival.  Indicate the sequence of departing packet numbers (at t = 1, 2, 3, 4, 5, 7, 8) under FCFS scheduling. 
    
    Give your answer as 7 ordered digits (each corresponding to the packet number of a departing packet), with a single space between each digit, and no spaces before the first or after the last digit, e.g., in a form like 7 6 5 4 3 2 1).

    ![Alt text](https://gaia.cs.umass.edu/kurose_ross/LMS/images/Chapter_4_KC/output_queue_scheduling_1.png)


    - 1 2 3 4 5 6 7

8. PACKET SCHEDULING (SCENARIO 2, PRIORITY).

    Consider the pattern of red and green packet arrivals to a router’s output port queue, shown below. Suppose each packet takes one time slot to be transmitted, and can only begin transmission at the beginning of a time slot after its arrival.  Indicate the sequence of departing packet numbers (at t = 1, 2, 3, 4, 5, 7, 8) under priority scheduling, where red packets have higher priority.

    Give your answer as 7 ordered digits (each corresponding to the packet number of a departing packet), with a single space between each digit, and no spaces before the first or after the last digit, e.g., in a form like 7 6 5 4 3 2 1).

    ![Alt text](https://gaia.cs.umass.edu/kurose_ross/LMS/images/Chapter_4_KC/output_queue_scheduling_2.png)

    - 1 2 4 3 5 6 7

## The Internet Protocol

1. WHAT IS THE INTERNET PROTOCOL?

    What are the principal components of the IPv4 protocol (check all that apply)?

    - [x] Packet handling conventions at routers (e.g., segmentation/reassembly)

    - [x] IPv4 addressing conventions.

    - [x] IPv4 datagram format.

    - [ ] ICMP (Internet Control Message Protocol)

    - [ ] Routing algorithms and protocols like OSPF and BGP.

    - [ ] SDN controller protocols.

2. THE IPV4 HEADER.

    Match each of the following fields in the IP header with its description, function or use.

    QUESTION LIST:

    - Version field
        - This field contains the IP protocol version number.

    - Type-of-service field
        - This field contains ECN and differentiated service bits.

    - Fragmentation offset field
        - This field is used for datagram fragmentation/reassembly.

    - Time-to-live field
        - The value in this field is decremented at each router; when it reaches zero, the packet must be dropped.

    - Header checksum field
        - This field contains the Internet checksum of this datagram's header fields.

    - Upper layer field
        - This field contains the "protocol number" for the transport-layer protocol to which this datagram's payload will be demultiplexed - UDP or TCP, for example.

    - Payload/data field
        - This field contains a UDP or TCP segment, for example.

    - Datagram length field.
        - This field indicates the total number of bytes in datagram.

3. WHAT IS AN IP ADDRESS ACTUALLY ASSOCIATED WITH?

    Which of the following statements is true regarding an IP address? (Zero, one or more of the following statements is true).

    - [ ] It is not necessary for a device using the IP protocol to actually have an IP address associated with it.

    - [x] If a host has more than one interface, then it has more that one IP address at which it can be reached.

    - [x] An IP address is associated with an interface.

    - [x] If a router has more than one interface, then it has more that one IP address at which it can be reached.

4. WHAT IS A SUBNET?

    What is meant by an IP subnet? (Check zero, one or more of the following characteristics of an IP subnet).

    - [ ] A set of devices that always have a common first 16 bits in their IP address.
    - [x] A set of devices that have a common set of leading high order bits in their IP address.
    - [x] A set of device interfaces that can physically reach each other without passing through an intervening router.
    - [ ] A set of devices all manufactured by the same equipment maker/vendor.

5. SUBNETTING(A).

    Consider the three subnets in the diagram below.

    ![Alt text](https://gaia.cs.umass.edu/kurose_ross/LMS/images/Chapter_4_KC/subnetting_1.jpg)

    What is the maximum # of interfaces in the 223.1.2/24 network?

    - [ ] 2**32
    - [ ] There's no a priori limit on the number of interfaces in this subnet.
    - [ ] Two hosts, as shown in the figure.
    - [x] 256
    - [ ] 128

6. What is the maximum # of interfaces in the 223.1.3/29 network?

    - [ ] 2**32
    - [ ] 128
    - [ ] There's no a priori limit on the number of interfaces in this subnet.
    - [x] 8
    - [ ] Three hosts, as shown in the figure.

7. Which of the following addresses can not be used by an interface in the 223.1.3/29 network? Check all that apply.

    - [x] 223.1.2.6
    - [ ] 223.1.3.6
    - [x] 223.1.3.16
    - [ ] 223.1.3.2
    - [x] 223.1.3.28

8. What is meant by saying that DHCP is a "plug and play" protocol?

    - [ ] The host needs to "plug" (by wire or wirelessly) into the local network in order to access ("play" in) the Internet
    
    - [ ] The network provides an Ethernet jack for a host's Ethernet adapter.
    
    - [x] No manual configuration is needed for the host to join the network.

9. DHCP REQUEST MESSAGE. 

    Which of the following statements about a DHCP request message are true (check all that are true). Hint: check out Figure 4.24 in the 7th and 8th edition of our textbook.


- [x] A DHCP request message may contain the IP address that the client will use.

- [ ] A DHCP request message is optional in the DHCP protocol.

- [ ] A DHCP request message is sent from a DHCP server to a DHCP client.

- [ ] The transaction ID in a DCHP request message is used to associate this message with previous messages sent by this client.

- [x] The transaction ID in a DHCP request message will be used to associate this message with future DHCP messages sent from, or to, this client.

- [x] A DHCP request message is sent broadcast, using the 255.255.255.255 IP destination address.

10. IPV4 VERSUS IPV6. 

    Which of the following fields occur ONLY in the IPv6 datagram header (i.e., appear in the IPv6 header but not in the IPv4 header)?  Check all that apply.

    - [x] The flow label field.

    - [ ] The header checksum field.

    - [ ] The time-to-live (or hop limit) field.

    - [ ] The upper layer protocol (or next header) field.

    - [ ] The options field.

    - [ ] The IP version number field.

    - [x] 128-bit source and destination IP addresses.

    - [ ] The header length field.

11. PURPOSE OF DHCP. 

    What is the purpose of the Dynamic Host Configuration Protocol?

    - [x] To obtain an IP address for a host attaching to an IP network.
    - [ ] To configure the set of available open ports (and hence well-known services) for a server.
    - [ ] To get the 48-bit link-layer MAC address associated with a network-layer IP address.
    - [ ] To configure the interface speed to be used, for hardware like Ethernet, which can be used at different speeds.


## Generalized Forwarding

1. Destination-based forwarding, which we studied in section 4.2, is a specific instance of match+action and generalized forwarding. Select the phrase below which best completes the following sentence:

    "In destination-based forwarding, ..."

    - [x] ... after matching on the destination IP address in the datagram header, the action taken is to forward the datagram to the output port associated with that destination IP address.

2. Which of the following match+actions can be taken in the generalized OpenFlow 1.0 match+action paradigm that we studied in Section 4.4? Check all that apply.

    - [x]... after matching on the destination IP address in the datagram header, the action taken is to decide whether or not to drop that datagram.

    - [x]... after matching on the destination IP address in the datagram header, the action taken is to forward the datagram to the output port associated with that destination IP address.

    - [x]... after matching on the source and destination IP address in the datagram header, the action taken is to forward the datagram to the output port associated with that source and destination IP address pair.

    - [x]... after matching on the 48-bit link-layer destination MAC address, the action taken is to forward the datagram to the output port associated with that link-layer address.

    - [x]... after matching on the port number in the segment's header, the action taken is to decide whether or not to drop that datagram containing that segment.

    - [x]... after matching on the port number in the segment's header, the action taken is to forward the datagram to the output port associated with that destination IP address.

3. Which of the following fields in the frame/datagram/segment/application-layer message can be matched in OpenFlow 1.0? Check all that apply.

    - [x] Source and/or destination port number

    - [x] Upper layer protocol field

    - [x] IP type-of-service field

    - [x] IP destination address

    - [x] IP source address

4. MATCH+ACTION IN OPENFLOW 1.0.

    Consider the figure below that shows the generalized forwarding table in a router.  Recall that a * represents a wildcard value. Now consider an arriving datagram with the IP source and destination address fields indicated below.  For each source/destination IP address pair, indicate which rule is matched. Note: assume that a rule that is earlier in the table takes priority over a rule that is later in the table and that a datagram that matches none of the table entries is dropped.

    ![Alt text](https://gaia.cs.umass.edu/kurose_ross/LMS/images/Chapter_4_KC/openflow_fig_1.jpg)

    **QUESTION LIST:**

    Source: 1.2.56.32 Destination:128.116.40.186
    - Rule 2, with action _drop_
    
    Source: 65.92.15.27 Destination: 3.4.65.76
    - Rule 1, with action _forward(2)_

    Source: 10.1.2.3 Destination: 7.8.9.2
    - Rule 3, with action _send to controller_

    Source: 10.1.34.56 Destination: 54.72.29.90
    - No match to any rule.


5. CRAFTING NETWORK-WIDE FORWARDING USING FLOW TABLES.

    Consider the network below.  We want to specify the match+action rules at s3 so that only the following network-wide behavior is allowed:

    traffic from 128.119/16 and destined to 137.220/16 is forwarded on the direct link from s3 to s1;
    traffic from 128.119/16 and destined to 67.56/16 is forwarded on the direct link from s3 to s2;
    incoming traffic via port 2 or 3, and destined to 128.119/16 is forwarded to 128.119/16 via local port 1. 

    No other forwarding should be allowed.  In particular s3 should not forward traffic arriving from 137.220/16 and destined for 67.56/16 and vice versa.

    From the list of match+action rules below, select the rules to include in s3's flow table to implement this forwarding behavior. Assume that if a packet arrives and finds no matching rule, it is dropped.

    ![Alt text](https://gaia.cs.umass.edu/kurose_ross/LMS/images/Chapter_4_KC/openflow_fig_2.jpg)

    - [x] Input port: 2; Dest: 128.119/16 Action: forward(1)

    - [x] Input port:1 ; Dest: 137.220/16 Action: forward(2)

    - [x] Input port: 3; Dest: 128.119/16 Action: forward(1)

    - [x] Input port: 1; Dest: 67.56/16 Action: forward(3)

6. CRAFTING NETWORK-WIDE FORWARDING USING FLOW TABLES (MORE).

    Consider the network below.  We want to specify the match+action rules at s3 so that s3 acts only as a relay for traffic between 137.220/16 and 67.56/16.  In particular s3 should not accept/forward and traffic to/from 128.119/16.

    From the list of match+action rules below, select the rules to include in s3's flow table to implement this forwarding behavior. Assume that if a packet arrives and finds no matching rule, it is dropped.

    - [x] Input port: 2; Dest: 67.56/16 Action: forward(3)

    - [x] Input port: 3; Dest: 137.220/16 Action: forward(2)

5. GENERALIZED FORWARDING.  

    What is meant by generalized forwarding (as opposed to destination-based forwarding) in a router or switch?

    - [x] Any of several actions (including drop (block), forward to a given interface, or duplicate-and-forward) can be made based on the contents of one or more packet header fields.


## Middleboxes and Summary

1. WHAT'S A "MIDDLEBOX"?  

    Which of the following network devices can be thought of as a "middlebox"? Check all that apply.

    - [x] HTTP load balancer

    - [x] HTTP cache

    - [x] Network Address Translation box

2. THE "THIN WAIST" OF THE INTERNET.

    What protocol (or protocols) constitutes the "thin waist" of the Internet protocol stack? Check all that apply.

    - [x] IP

3. THE END-TO-END PRINCIPLE.

    Which of the statements below are true statements regarding  the "end-to-end principle"? Check all that apply.

    - [x] The end-to-end argument advocates placing functionality at the network edge because some functionality cannot be completely and correctly implemented in the network, and so needs to be placed at the edge in any case, making in-network implementation redundant.

    - [x] The end-to-end argument allows that some redundant functionality might be placed both in-network and at the network edge in order to enhance performance.

4. THE INTERNET HOURGLASS.  

    What is meant when it is said that the Internet has an “hourglass” architecture? See the picture below if you are unfamiliar with an "hourglass".

    - [x] The Internet protocol stack has a “thin waist” in the middle, like an hourglass.  The Internet Protocol (IP) is the only network-layer protocol in the middle layer of the stack.  Every other layer has multiple protocols at that layer.

5. FEDERAL REGULATION AND THE INTERNET.  

    In the US, which of the following services has been regulated by the Federal Communications Commission (FCC) going back into the 20th century?

    - [x] Telecommunication services.
    