# Simple-Network-topology
below is a simple networking connection for Netcore Ltd
# Netcore Ltd Network Topology and Connectivity Testing

A Cisco Packet Tracer networking project that models a small organisation, **Netcore Ltd**, with separate IT, Sales, and HR departmental networks. The project documents the network layout, sample endpoint configuration, router startup, and basic connectivity checks, including a successful ping to the server and HTTP access to the hosted Netcore Ltd webpage.

> **Project type:** Networking lab / cybersecurity fundamentals  
> **Tool:** Cisco Packet Tracer  
> **Focus areas:** Network topology, IPv4 addressing, routing concepts, connectivity testing, and test documentation

## Table of Contents

- [Project Overview](#project-overview)
- [Objectives](#objectives)
- [Network Design](#network-design)
- [Addressing and Endpoint Configuration](#addressing-and-endpoint-configuration)
- [Services and Connectivity](#services-and-connectivity)
- [Testing and Evidence](#testing-and-evidence)
- [Test Matrix](#test-matrix)
- [How to Reproduce the Lab](#how-to-reproduce-the-lab)
- [Security and GRC Learning Points](#security-and-grc-learning-points)
- [Limitations and Next Steps](#limitations-and-next-steps)
- [Skills Demonstrated](#skills-demonstrated)

## Project Overview

This lab represents a simple departmental network. A central router connects three departmental segments:

- **IT:** A switch connects the IT endpoints and a server.
- **Sales:** A switch connects the Sales endpoints.
- **HR:** A switch connects the HR endpoints.

The submitted evidence includes the topology in Packet Tracer, a sample PC IP configuration, the router's Cisco IOS startup screen, a successful browser request to the Netcore Ltd webpage, a successful ping to the server, and a table of intended test cases.

The project is an introductory network configuration and verification exercise. It is also a useful foundation for exploring how network segmentation, access controls, service availability, and test evidence support security and governance objectives.

## Objectives

1. Represent separate IT, Sales, and HR departmental networks in Cisco Packet Tracer.
2. Connect departmental switches and endpoints through a central router.
3. Configure and inspect endpoint IPv4 network settings.
4. Verify basic connectivity to the server using ICMP ping.
5. demonstrate HTTP access to a webpage hosted for Netcore Ltd.
6. Document expected network and service test outcomes.

## Network Design

The logical topology follows a hub-and-spoke layout, with the router at the centre.

```text
                         +------------------+
                         |     Router0      |
                         +------------------+
                           /       |       \
                          /        |        \
                 +-----------+ +-----------+ +-----------+
                 | IT Switch | |Sales Switch| | HR Switch |
                 +-----------+ +-----------+ +-----------+
                   /   |   \       /   \         /   \
              Server  PC0  PC1   PC2   PC3     PC4   PC5
```

**Topology notes**

- Each department has its own switch and connected endpoints.
- The IT segment also contains the server.
- The central router provides the intended path between departmental networks.
- The diagram shows the logical connections; it does not, by itself, prove that every interdepartmental route or access-control policy has been fully configured and tested.

## Addressing and Endpoint Configuration

The submitted PC configuration screenshot shows the following values for **PC1**:

| Setting | Value |
|---|---|
| IPv4 address | `192.168.10.5` |
| Subnet mask | `255.255.255.0` |
| Default gateway | `192.168.10.1` |
| DNS server | `192.168.10.2` |

These values place PC1 in the `192.168.10.0/24` IPv4 subnet. The gateway and DNS values are recorded as shown in the project evidence.

The screenshot has the **DHCP** option selected while displaying these IPv4 values. Therefore, the README does not assume that the values were manually assigned as a static configuration.

### Addressing details to document in a future revision

For a more complete network handover, add a full IP plan showing each router interface, departmental subnet, switch management address (if used), server address, DHCP scope (if used), and DNS configuration. The supplied evidence does not provide a complete address table for all devices.

## Services and Connectivity

### HTTP

The Packet Tracer browser screenshot shows PC1 accessing `http://netcore.com` and displaying the **Netcore Ltd** webpage. This is evidence of successful HTTP access from that endpoint in the simulation.

### ICMP ping

The command prompt screenshot shows PC0 pinging `192.168.10.2`. The displayed results are:

- Packets sent: 4
- Packets received: 4
- Packets lost: 0
- Packet loss: 0%

This confirms successful ICMP reachability from PC0 to `192.168.10.2` at the time of the test. The project identifies this address as the server/DNS address in the sample PC configuration, although the supplied evidence does not show the server's own configuration screen.

### FTP and access-control expectations

The test matrix lists FTP as an expected permitted service from Sales and HR to IT. It also lists a test in which Sales-to-IT ping is expected to be blocked. These are **expected outcomes in the submitted test plan**, not confirmed results in the screenshots supplied. They should be verified in Packet Tracer before being described as implemented or passed.

## Testing and Evidence

The project evidence supports the following status summary:

| Check | Evidence in the assignment | Status |
|---|---|---|
| Network topology | Packet Tracer topology screenshot | Documented |
| PC1 IPv4 settings | PC configuration screenshot | Documented |
| Router startup | Cisco IOS CLI startup screenshot | Documented |
| PC0 to `192.168.10.2` ping | Four replies, 0% packet loss | Successful in the captured test |
| PC1 HTTP access to `http://netcore.com` | Netcore Ltd page displayed in browser | Successful in the captured test |
| Department-to-department ping tests | Listed in the test matrix | Expected outcomes documented; execution evidence not supplied |
| Sales-to-IT ping restriction | Listed as expected to be blocked | Expected outcome documented; execution evidence not supplied |
| Sales/HR HTTP and FTP access to IT | Listed as expected to be allowed | Expected outcomes documented; execution evidence not supplied |

### Suggested evidence to add

For a stronger portfolio presentation, include screenshots of:

- Successful and unsuccessful pings for every test in the matrix.
- Router interface addressing and routing configuration.
- Any ACLs used to permit or block specific traffic.
- Successful HTTP and FTP tests from the required departments.
- The server's IP configuration and enabled services.
- A completed test-results table showing actual result, pass/fail status, date, and notes.

## Test Matrix

The following cases reproduce the expected outcomes in the submitted assignment. They should not be treated as passed until the corresponding tests have been run and evidence captured.

| ID | Test | Expected outcome in assignment |
|---|---|---|
| T01 | IT → Sales ping | Success |
| T02 | IT → HR ping | Success |
| T03 | HR → IT ping | Success |
| T04 | HR → Sales ping | Success |
| T05 | Sales → HR ping | Success |
| T06 | Sales → IT ping | Blocked |
| T07 | Sales → IT HTTP | Allowed |
| T08 | Sales → IT FTP | Allowed |
| T09 | HR → IT HTTP | Allowed |
| T10 | HR → IT FTP | Allowed |

### Test execution recommendations

For each case, record the source device, destination device or service, command or action, expected result, actual result, pass/fail status, and screenshot or evidence reference. If traffic is intentionally blocked, record the policy responsible for the restriction and verify that the permitted services continue to work.

## How to Reproduce the Lab

1. Open the project in Cisco Packet Tracer. If the `.pkt` file is included in this repository, open that file; otherwise recreate the topology from the diagram.
2. Add one router, three departmental switches, the IT server, and the endpoint PCs shown in the topology.
3. Connect each department's switch to the router and connect the department's endpoints to its switch.
4. Configure router interfaces and endpoint IP settings to match the addressing plan used by the lab.
5. Configure the server and enable the services required for the tests, including HTTP and FTP if those tests are in scope.
6. Verify the routing and any access-control rules needed to achieve the test matrix.
7. Run each test and record the actual result. Do not mark a test as passed solely because its expected outcome is listed.
8. Capture screenshots and update the test matrix with the observed outcomes.

**Reproducibility note:** The supplied assignment document contains screenshots and expected test cases. It does not establish that the editable Packet Tracer `.pkt` file is included with this README. Add the `.pkt` file to the repository if you are able to share it and want others to reproduce the simulation.

## Security and GRC Learning Points

This lab provides a practical starting point for connecting network engineering work with Governance, Risk, and Compliance (GRC) concepts.

- **Segmentation:** Separate departmental networks can support least-privilege access when combined with correctly configured routing and access-control rules.
- **Access control:** The test plan distinguishes between traffic that should be allowed and traffic that should be blocked. The implemented rules should be reviewed and tested against those requirements.
- **Verification and evidence:** Screenshots and recorded outcomes help demonstrate what was tested, what succeeded, and what remains unverified.
- **Requirements traceability:** Mapping each test to a documented expected result makes it easier to identify gaps between requirements and implementation.
- **Change and configuration management:** Keeping the Packet Tracer file, addressing plan, router configuration, and test evidence under version control can help make changes traceable.
- **Risk awareness:** A successful ping or HTTP request alone does not establish that the network is secure. Security also depends on access rules, service configuration, authentication, patching, monitoring, and other controls that are outside the scope of the supplied evidence.

These are learning points drawn from the design and test plan; the assignment does not claim a formal security audit, compliance certification, or full GRC assessment.

## Limitations and Next Steps

The current submission is a concise simulation record. The following additions would make it more complete:

1. Include the original Packet Tracer `.pkt` file, if available and appropriate to share.
2. Publish a full IP addressing table and router interface configuration.
3. Add the configuration for any ACLs or other rules used to restrict traffic.
4. Execute and capture every test in the test matrix.
5. Record actual results separately from expected results.
6. Add a short network risk assessment covering unauthorised access, unnecessary exposed services, and inadequate segmentation.
7. Document the intended business reason for each permitted or blocked connection.

## Skills Demonstrated

- Cisco Packet Tracer topology design
- Basic IPv4 addressing concepts
- Router, switch, endpoint, and server network concepts
- ICMP ping and connectivity verification
- HTTP service testing
- Test-case documentation and evidence capture
- Introductory network segmentation and access-control concepts
- GRC-oriented thinking about requirements, control expectations, and verification

## Project Evidence

The original assignment contains screenshots of the network topology, PC configuration, router CLI startup, HTTP webpage access, successful ping, and the expected test matrix. Add these screenshots to a repository folder such as `docs/images/` if you want the README to display them directly. Update the image links after adding the files.

---

*Portfolio note: This project demonstrates foundational networking practice using a simulated environment. Test outcomes are described according to the evidence supplied, and expected results are not presented as verified results unless a successful test is shown.*

