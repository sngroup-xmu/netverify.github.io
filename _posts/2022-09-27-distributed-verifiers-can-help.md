---
layout: post
title: TBD
authors: [A,B,C,D,E,F]
categories: [overview, research, network, verification]
image: 
tags: []
---

TODO: overview

## Issues of centralized DPV

Despite the substantial progress in accelerating DPV, existing tools use a centralized architecture, which lacks the scalability needed for deployment in large networks. Specifically, they use a centralized server to collect the data plane from each network device and verify the requirement. Such a design is unscalable in nature: (1) it requires a management network to provide reliable connections between the server and network devices, which is hard to build itself; (2) it introduces a long control path, which includes sending device data planes to the server, performing verification at the server, and sending corresponding action instructions from the server back to devices, leading to the slow response to network errors and finally affecting network availability; (3) the server becomes the performance bottleneck and the single point of failure of DPV tools, it is mainly because larger network requires verifiers with stronger operational capability. To scale up DPV, Libra [[1]](#Libra) partitions the data plane into disjoint packet spaces and uses MapReduce to achieve parallel verification in a cluster; Azure RCDC [[2]](#RCDC) partitions the data plane by device to verify the availability of all shortest paths with a higher level of parallelization in a cluster. However, both are still centralized designs with the limitations above, and RCDC can only verify that particular requirement.

![A (cluster of) server(s) as a centralized verifier](C:\Users\31139\Desktop\centralizedDPV.png)

## The challenges of scaling DPV via distributed

TODO

## Design(TBD)

TODO

## Example 

TODO

## Summary

Current DPV tools employ a centralized architecture, however, this design faces scalability issues in large networks, such as maintaining a reliable, low-latency management network, performance bottleneck, and single point of failure. To tackle the scalability challenge of DPV, we design Coral, a distributed DPV framework to achieve scalable DPV by decomposing verification to lightweight on-device counting tasks. Coral consists of (1) a declarative specification language,(2) a verification planner decomposing global verification into lightweight on-device counting tasks, and (3) a distributed verification messaging(DVM) protocol that enables efficient and distributed computing among on-device verifiers. Extensive experiments demonstrate the benefits and feasibility of Coral. 

## References

 <a name="Libra"></a>[1] H. Zeng, S. Zhang, F. Ye, V. Jeyakumar, M. Ju, J. Liu, N. McKeown, and A. Vahdat. Libra: Divide and conquer to verify forwarding tables in huge networks. In 11th USENIX Symposium on Networked Systems Design and Implementation (NSDI), pages 87–99, 2014.

<a name="RCDC"></a>[2] K. Jayaraman, N. Bjørner, J. Padhye, A. Agrawal, A. Bhargava, P.-A. C. Bissonnette, S. Foster, A. Helwer, M. Kasten, I. Lee, et al.
Validating datacenters at scale. In Proceedings of the ACM Special Interest Group on Data Communication, pages 200–213. 2019.
