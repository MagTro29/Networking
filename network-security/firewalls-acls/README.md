# Access Control Lists (ACLs) – Standard vs Extended

This lab documents the configuration and verification of **Access Control
Lists (ACLs)** to control traffic flow within a routed network.

ACLs are used to permit or deny traffic based on defined criteria and are a
fundamental security and traffic-filtering mechanism in enterprise networks.

## Goal
- Understand the difference between standard and extended ACLs
- Apply ACLs to control traffic between network segments
- Verify correct traffic filtering without breaking connectivity

## ACL Types

### Standard ACLs
- Filter traffic **based only on source IP address**
- Less granular control
- Typically placed **close to the destination**

### Extended ACLs
- Filter traffic based on:
  - Source IP
  - Destination IP
  - Protocol (IP, TCP, UDP, ICMP)
  - Source and destination ports
- Much more granular
- Typically placed **close to the source**

## Scenario (Example)
- VLAN 10: Users
- VLAN 20: Admin
- VLAN 30: Servers
- Requirement:
  - Users (VLAN 10) can access servers (VLAN 30) on HTTP/HTTPS
  - Users cannot access Admin VLAN (VLAN 20)
  - Admin VLAN has full access

## Steps Performed (High Level)
1. Identified traffic flows that should be permitted or denied.
2. Designed ACL logic before applying any configuration.
3. Implemented a **standard ACL** to demonstrate source-based filtering.
4. Implemented an **extended ACL** to control traffic by protocol and port.
5. Applied ACLs to the correct interface and direction (inbound/outbound).
6. Verified behaviour using ping and application-based testing.

## Placement & Direction
- Incorrect ACL placement can unintentionally block legitimate traffic.
- Extended ACLs were applied **inbound near the source VLAN**.
- Direction (in vs out) was chosen based on where traffic should be filtered.

## Verification Checklist
- `show access-lists` confirms ACL entries and match counters
- `show ip interface` confirms ACL is applied to the correct interface
- Ping tests:
  - Allowed traffic succeeds
  - Denied traffic fails as expected
- If issues occur:
  - Check ACL order (top-down processing)
  - Check implicit deny at the end
  - Verify interface and direction

## What I Learned
- Extended ACLs provide precise control and should be preferred in most cases.
- Planning ACL logic before configuration prevents accidental outages.
- ACL order and placement are critical for correct behaviour.
