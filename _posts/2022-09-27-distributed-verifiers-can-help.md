---
layout: post
title: TBD
authors: [A,B,C,D,E,F]
categories: [overview, research, network, verification]
image: 
tags: []
---

There has been a long line of research on both data plane verification (DPV) and control plane verification (CPV). In this work, we mainly focus on data plane verification, because data plane is the ground truth of network, in other words,  it can detect a wider range of network errors by checking the actual data plane at the network devices. However, current data plane verification tools employ a centralized architecture, where a server collects the data planes of all devices and verifies them.  This design faces scalability issues in large networks, such as maintaining a reliable, low-latency management network, performance bottleneck and single point of failure. 

In this article, we propose Coral, a distributed, on-device DPV framework, to tackle the scalability challenge of DPV, allowing to achieve scalable DPV under various settings, with little overhead on commodity network devices.



## Issues of centralized DPV

Existing tools use a centralized architecture, which lacks the scalability needed for deployment in large networks. Specifically, they use a centralized server to collect the data plane from each network device and verify the requirement. Such a design is unscalable in nature: (1) it requires a management network to provide reliable connections between the server and network devices, which is hard to build itself; (2) it introduces a long control path, which includes sending device data planes to the server, performing verification at the server, and sending corresponding action instructions from the server back to devices, leading to the slow response to network errors and finally affecting network availability; (3) the server becomes the performance bottleneck and the single point of failure of DPV tools, it is mainly because larger network requires verifiers with stronger operational capability. To scale up DPV, Libra [[1]](#Libra) partitions the data plane into disjoint packet spaces and uses MapReduce to achieve parallel verification in a cluster; Azure RCDC [[2]](#RCDC) partitions the data plane by device to verify the availability of all shortest paths with a higher level of parallelization in a cluster. However, both are still centralized designs with the limitations above, and RCDC can only verify that particular requirement.

![A (cluster of) server(s) as a centralized verifier](C:\Users\31139\Desktop\centralizedDPV.png)

## The challenges of scaling DPV via distributed

TODO

## Design(TBD)

TODO

## Example 

TODO

## Summary

Current DPV tools employ a centralized architecture, however, this design faces scalability issues in large networks, such as maintaining a reliable, low-latency management network, performance bottleneck, and single point of failure. To tackle the scalability challenge of DPV, we design Coral, a distributed DPV framework to achieve scalable DPV by decomposing verification to lightweight on-device counting tasks. Coral consists of (1) a declarative specification language,(2) a verification planner decomposing global verification into lightweight on-device counting tasks, and (3) a distributed verification messaging(DVM) protocol that enables efficient and distributed computing among on-device verifiers. Extensive experiments demonstrate the benefits and feasibility of Coral. 
		
There's a lot more to learn about this topic, and in future blog posts, we will explore some of them. (1)Some studies investigate the verification of stateful DP (e.g., middleboxes)[[3]](#middleboxes) and programmable DP (e.g., P4 [[4]](#P4) ) . Studying how to extend Coral to verify stateful and programmable DP would be an interesting future work. (2) Coral chooses BDD [[5]](#BDD) to represent packets for its efficiency. Recent data structures (e.g.,ddNF [[6]](#ddNF) and PEC [[7]](#PEC)) may have better performance and benefit Coral. We leave this as future work.

## References

 <a name="Libra"></a>[1] H. Zeng, S. Zhang, F. Ye, V. Jeyakumar, M. Ju, J. Liu, N. McKeown, and A. Vahdat. Libra: Divide and conquer to verify forwarding tables in huge networks. In 11th USENIX Symposium on Networked Systems Design and Implementation (NSDI), pages 87–99, 2014.

<a name="RCDC"></a>[2] K. Jayaraman, N. Bjørner, J. Padhye, A. Agrawal, A. Bhargava, P.-A. C. Bissonnette, S. Foster, A. Helwer, M. Kasten, I. Lee, et al.
Validating datacenters at scale. In Proceedings of the ACM Special Interest Group on Data Communication, pages 200–213. 2019.

<a name="middleboxes"></a>[3] Aurojit Panda, Ori Lahav, Katerina Argyraki, Mooly Sagiv, and Scott Shenker. Verifying reachability in networks with mutable datapaths. In 14th USENIX symposium on networked systems design and implementation(NSDI), pages 699–718, 2017.
		
<a name="P4"></a>[4] Pat Bosshart, Dan Daly, Glen Gibb, Martin Izzard, NickMcKeown, Jennifer Rexford, Cole Schlesinger, Dan Talayco, Amin Vahdat, George Varghese, et al. P4:Programming protocol-independent packet processors.ACM SIGCOMM Computer Communication Review,44(3):87–95, 2014.
		
<a name="BDD"></a>[5] Randal E Bryant. Graph-based algorithms for boolean function manipulation. Computers, IEEE Transactions on, 100(8):677–691, 1986.
		
<a name="ddNF"></a>[6] Nikolaj Bjørner, Garvit Juniwal, Ratul Mahajan, Sanjit A Seshia, and George Varghese. Ddnf: An efficient data structure for header spaces. In Haifa Verification Conference, pages 49–64. Springer, 2016.
		
<a name="PEC"></a>[7] Alex Horn, Ali Kheradmand, and Mukul R Prasad. A precise and expressive lattice-theoretical framework for efficient network verification. In 2019 IEEE 27th In- ternational Conference on Network Protocols (ICNP),pages 1–12. IEEE, 2019.

