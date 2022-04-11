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
