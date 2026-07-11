# Analisis-Trafico-Inseguro-Telnet-Wireshark
Análisis de tráfico de red con Wireshark sobre el protocolo Telnet en un entorno controlado. Se documenta la captura y el análisis de una sesión de autenticación, demostrando la transmisión de credenciales sin cifrado y los riesgos asociados. Incluye evidencia, metodología, observaciones técnicas y conclusiones.


# Technical Report

## Executive Summary

A packet capture containing 897 network packets was analyzed to evaluate the behavior of the Telnet protocol during a remote authentication process.

Traffic inspection confirmed the establishment of a TCP session between the client (192.168.1.92) and the Cisco IOS switch (192.168.1.244) over TCP port 23.

Session reconstruction performed through Wireshark's **Follow TCP Stream** feature confirmed that authentication credentials were transmitted in clear text.

This behavior represents a significant security weakness because any actor capable of intercepting network traffic could recover authentication data without requiring cryptographic attacks.

---

## Scope

The assessment covers the following activities:

* Packet inspection
* TCP session analysis
* Telnet authentication
* Stream reconstruction
* Security assessment

---

## Evidence Summary

| Evidence      | Value                                |
| ------------- | ------------------------------------ |
| Capture File  | analisis-telnet-no-encriptado.pcapng |
| Tool          | Wireshark                            |
| Protocol      | Telnet                               |
| Transport     | TCP                                  |
| Port          | 23                                   |
| Client        | 192.168.1.92                         |
| Server        | 192.168.1.244                        |
| Device        | Cisco IOS Switch                     |
| Total Packets | 897                                  |

---

## Methodology

The packet capture was imported into Wireshark for inspection.

Traffic associated with TCP port 23 was isolated to identify the Telnet communication between both hosts.

After validating the TCP session establishment, the conversation was reconstructed using **Follow TCP Stream** to inspect the authentication exchange.

The reconstructed stream confirmed that the username and password configured exclusively for this laboratory were transmitted without encryption.

---

## Technical Analysis

The network capture shows a successful TCP session established between the client workstation and the Cisco IOS switch.

Packet analysis confirms the expected TCP connection sequence followed by a Telnet authentication.

Unlike secure remote administration protocols such as SSH, Telnet does not provide confidentiality for transmitted information.

As a consequence, authentication credentials remain visible within the packet capture and can be reconstructed directly from the TCP stream.

---

## Findings

### Finding 01

**Title**

Cleartext Transmission of Authentication Credentials

**Severity**

High

**Description**

The Telnet protocol transmitted authentication credentials without applying any encryption mechanism.

Credential visibility was confirmed through TCP Stream reconstruction.

**Impact**

An attacker with access to the communication channel could recover authentication credentials and potentially gain unauthorized administrative access.

---

### Finding 02

**Title**

Use of Legacy Remote Administration Protocol

**Severity**

Medium

**Description**

The analyzed device accepts Telnet connections for remote administration.

Legacy protocols lacking encryption increase the attack surface and should not be used in production environments.

---

## Risk Assessment

| Category        | Assessment  |
| --------------- | ----------- |
| Confidentiality | High Risk   |
| Integrity       | Medium Risk |
| Availability    | Low Risk    |

---

## Recommendations

* Disable Telnet on network devices.
* Enable SSH version 2 exclusively.
* Restrict administrative access through ACLs.
* Monitor TCP port 23 activity.
* Remove legacy management protocols from production environments.
* Periodically audit remote administration services.

---

## Conclusion

The assessment confirms that Telnet authentication exposes credentials in clear text during network transmission.

Although the analyzed credentials were fictitious and used exclusively in a controlled laboratory, the captured traffic demonstrates why Telnet is considered an insecure protocol for remote administration.

The results obtained during this assessment reinforce the importance of encrypted management protocols and illustrate how packet analysis can be used to identify security weaknesses during network forensic investigations.




