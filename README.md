# The Quaoar Case

This document summarizes the **Black Box Penetration Testing** activity conducted on the vulnerable virtual machine *Quaoar*. The analysis was carried out as a project for the **Penetration Testing and Ethical Hacking (PTEH)** course (Academic Year 2025/2026).

## Analysis Summary

The goal of the analysis was to simulate a real-world attack starting with zero knowledge of the target infrastructure. The objective was to identify architectural weaknesses, exploit them to gain access, and finally escalate privileges to achieve full system compromise (root).

The entire *Kill Chain* exploited a series of severe misconfigurations, highlighting a total lack of basic *hardening* practices:

1. **Enumeration and Vulnerability Mapping:** A **WordPress** installation exposed on the network was identified.
2. **Target Exploitation:** Access to the CMS administration panel was achieved using default credentials (`admin:admin`).
3. **Remote Code Execution (RCE):** By leveraging the active *Theme Editor* feature in WordPress, a malicious payload (PHP Reverse Shell) was injected into the `header.php` file. This provided initial access to the machine with limited privileges (`www-data`).
4. **Privilege Escalation:** During system exploration (Post-Exploitation), cleartext passwords were found in web configuration files. Due to the critical practice of *password reuse*, the database password (`rootpassword!`) was also the password for the system `root` account, allowing full acquisition of maximum privileges.

## Remediation

The primary recommendations resulting from the test include:
- Prompt removal of default credentials and application of strict password policies (absolute prohibition of password reuse between DB and system).
- CMS Hardening (disabling the *Theme Editor* via `wp-config.php`).
- Systematic updating and patching of obsolete services exposed by the machine.
- Disabling direct SSH access for the root user.

---

**Author:**  
Choaib Goumri (Student ID: NF22500223)  
*University of Salerno - Department of Computer Science (DINF)*
