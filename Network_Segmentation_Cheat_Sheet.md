# Network segmentation Cheat Sheet

## Introduction

Network segmentation is the core of multi-layer defense in depth for modern services. Segmentation allows you to slow down an attacker if he cannot implement attacks such as:
 - SQL-injections, see [SQL Injection Prevention Cheat Sheet](https://github.com/OWASP/CheatSheetSeries/blob/master/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.md)
 - compromise of workstations of employees with elevated privileges
 - compromise of another server in the perimeter of the organization
 - compromise of the target service through the compromise of the LDAP directory, DNS server, and other corporate site published on the Internet

The main goal of this cheat sheet is to show the basics of network segmentation to effectively counter attacks by building a secure and maximally isolated service network architecture.

Segmentation will avoid the following situations:
- executing arbitrary commands on a public web server (NginX, Apache, Internet Information Service) prevents an attacker from gaining direct access to the database
- having unauthorized access to the database server, an attacker cannot access CnC on the Internet

## Schematic symbols

Elements used in network diagrams:

![Schematic symbols](https://github.com/sergiomarotco/OWASP_Draft/blob/main/Assets/Network_Segmentation_Cheat_Sheet_Schematic_symbols.jpg)

Crossing the border of the rectangle means crossing the firewall:
![Traffic passes through two firewalls](https://github.com/sergiomarotco/OWASP_Draft/blob/main/Assets/Network_Segmentation_Cheat_Sheet_firewall_1.jpg)

In the image above, traffic passes through two firewalls with the names FW1 and FW2

![Traffic passes through one firewall](https://github.com/sergiomarotco/OWASP_Draft/blob/main/Assets/Network_Segmentation_Cheat_Sheet_firewall_2.jpg)

In the image above, traffic passes through one firewall, behind which there are two VLANs

Further, the schemes do not contain firewall icons so as not to overload the schemes

## Three-layer network architecture
By default, developed information systems should consist of at least three components:
1. [FRONTEND](https://github.com/sergiomarotco/OWASP_Draft/blob/main/Network_Segmentation_Cheat_Sheet.md#FRONTEND)
2. [MIDDLEWARE](https://github.com/sergiomarotco/OWASP_Draft/blob/main/Network_Segmentation_Cheat_Sheet.md#MIDDLEWARE)
3. [BACKEND](https://github.com/sergiomarotco/OWASP_Draft/blob/main/Network_Segmentation_Cheat_Sheet.md#BACKEND)

### FRONTEND
FRONTEND - A frontend is a set of segments with the following network elements:
- balancer
- application layer firewall
- web server
- web cache

![FRONTEND](https://github.com/sergiomarotco/OWASP_Draft/blob/main/Assets/Network_Segmentation_Cheat_Sheet_FRONTEND.jpg)

### MIDDLEWARE
MIDDLEWARE - a set of segments to accommodate the following network elements:
- web applications that implement the logic of the information system (processing requests from clients, other services of the company and external services; execution of requests)
- authorization services
- analytics services
- message queues
- stream processing platform

![MIDDLEWARE](https://github.com/sergiomarotco/OWASP_Draft/blob/main/Assets/Network_Segmentation_Cheat_Sheet_MIDDLEWARE.jpg)

### BACKEND
BACKEND - a set of network segments to accommodate the following network elements:
- SQL database
- LDAP directory (Domain controller)
- storage of cryptographic keys
- file-server

![BACKEND](https://github.com/sergiomarotco/OWASP_Draft/blob/main/Assets/Network_Segmentation_Cheat_Sheet_BACKEND.jpg)

### Example of Three-layer network architecture
![BACKEND](https://github.com/sergiomarotco/OWASP_Draft/blob/main/Assets/Network_Segmentation_Cheat_Sheet_TIER_Example.jpg)
The following example shows an organization's local network. The organization is called "Сontoso".

The edge firewall contains 2 VLANs of **FRONTED** secuirity zone:
- DMZ Inbound - a segment for hosting services and applications accessible from the Internet, they must be protected by WAF
- DMZ Outgoing - a segment for hosting services that are inaccessible from the Internet, but have access to external networks (the firewall does not contain any rules for allowing traffic from external networks)

The internal firewall contains 4 VLANs:
- **MIDDLEWARE** security zone contains only one VLAN with name APPLICATIONS - a segment designed to host information system applications that interact with each other (interservice communication) and interact with other services
- **BACKEND** security zone contains:
   - segment DATABASES - a segment designed to delimit various databases of an automated system
   - AD SERVICES - segment designed to host various Active Directory services, in the example only one server with a domain controller Contoso.com is shown
   - LOGS - segment, designed to host servers with logs, servers centrally store application logs of an automated system.
