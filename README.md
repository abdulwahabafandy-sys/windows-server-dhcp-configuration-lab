# Windows Server 2022 — DHCP Server Configuration & Lease Verification

**Hands-on Windows infrastructure lab | Hyper-V · Windows Server 2022 · DHCP · DNS settings · IPv4 networking**

> Configured the Windows Server DHCP role, deployed an IPv4 scope, enabled automatic Windows client addressing, and verified a successful DHCP lease from both the client and server.

[**View the lab report with all seven screenshots (PDF)**](Report.pdf)

## Lab overview

The goal was to configure a Windows Server 2022 domain controller to distribute IPv4 network settings automatically to a Windows client on an isolated Hyper-V lab network. After creating and activating the DHCP scope, I set the client to obtain its IP and DNS settings automatically, renewed the lease, and verified the assigned address in both `ipconfig /all` and the DHCP server's **Address Leases** view.

### Architecture

```text
          Hyper-V private/internal lab network
                    192.168.20.0/24
                           |
             Windows Server 2022 / DHCP
                   192.168.20.10
                Domain: Exam.local
                           |
                    Windows client
             DHCP-assigned: 192.168.20.101
```

| Setting | Configuration |
|---|---|
| DHCP server | `192.168.20.10/24` |
| DHCP scope | `ExamScope` |
| Scope address range | `192.168.20.100–192.168.20.200` |
| DNS server setting | `192.168.20.10` |
| Client address observed | `192.168.20.101` |
| Environment | Windows Server 2022 + Windows client on Hyper-V |

## What I accomplished

1. Configured the Windows Server with a static IPv4 address and installed DHCP Server and management tools.
2. Created and activated an IPv4 DHCP scope for the lab subnet.
3. Configured the Windows client to obtain its IPv4 and DNS server addresses automatically.
4. Used `ipconfig /release`, `ipconfig /renew`, and `ipconfig /all` to refresh and verify the lease.
5. Confirmed the issued client address from DHCP Manager's **Address Leases** list.
6. Documented problems involving VM network connectivity, inactive scopes, DNS settings, and stale leases.

## Evidence and results

The report includes **seven screenshots** covering the server's static configuration, DHCP role installation, scope boundaries, scope activation, automatic client addressing, client lease output, and the matching server-side lease record.

**Result:** The Windows client received `192.168.20.101`, and DHCP Manager showed the same address assigned within the active scope. This demonstrates successful DHCP lease allocation—not merely installation of the server role.

## Tools and skills

**Tools:** Windows Server 2022, Hyper-V, Windows PowerShell, DHCP Manager, Windows client network settings.

**Demonstrated skills:** DHCP scope administration, IPv4 subnet configuration, client/server networking, lease verification, and troubleshooting Windows networking services.

## Limitations and notes

- The original report documents router option `192.168.20.1`, while the client screenshot appears to show `192.168.20.10` as the default gateway. This mismatch should be checked in a follow-up exercise. It does not invalidate the observed DHCP lease.
- Evidence establishes DHCP lease allocation; it does not independently demonstrate successful external routing or complete DNS resolution.
- This is an isolated **educational lab**, not a production deployment.

## Full lab report

[Download **Report.pdf** — 8 pages, seven screenshots, validation and troubleshooting](Report.pdf)