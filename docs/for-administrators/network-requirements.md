# Network Requirements

**Purpose:** Define source-restricted network requirements for Delinea discovery and Windows breakglass management.  
**Audience:** Network engineers, firewall administrators, Windows engineers, and PAM administrators.

## Approved source identities

The following on-premises and cloud Discovery Engine sources are approved at the network level:

| Source IP |
|---|
| `10.122.84.93` |
| `10.122.84.94` |
| `10.122.84.95` |
| `10.122.128.87` |
| `10.122.128.88` |
| `10.46.158.68` |
| `10.46.158.69` |

## Discovery Engine hostnames

| Hostname | Role |
|---|---|
| `gotsvw12243` | Discovery Engine |
| `gotsvw12244` | Discovery Engine |
| `gotsvw12245` | Discovery Engine |
| `gotsvw12299` | Discovery Engine |
| `gotsvw12300` | Discovery Engine |
| `closvw1979` | Cloud Discovery Engine |
| `closvw1982` | Cloud Discovery Engine |

> [!IMPORTANT]
> TBC: Hostname-to-IP mappings are not confirmed. Validate them through DNS, CMDB, or IPAM before firewall implementation.
> Owner: Infrastructure, DNS, and network teams

## Supplied firewall matrix

| Function | Protocol | Port | Remote scope |
|---|---|---:|---|
| RPC Endpoint Mapper | TCP | 135 | Approved Discovery Engine IPs only |
| SMB / Microsoft-DS | TCP/UDP | 445 | Approved Discovery Engine IPs only |
| Dynamic RPC | TCP/UDP | 49152-65535 | Approved Discovery Engine IPs only |
| NetBIOS discovery | UDP | 137-138 | Approved Discovery Engine IPs only |
| WinNT ADSI provider | TCP | 139 | Approved Discovery Engine IPs only |

**Required policy:** Domain profile, Allow action, approved source IP scope only.

## Items requiring validation

> [!IMPORTANT]
> TBC: UDP 445, UDP dynamic RPC, NetBIOS 137-139, exact dynamic RPC range, traffic direction, and host versus network firewall ownership.
> Owner: Network and Windows infrastructure teams

Do not implement unrestricted remote scope or broad public or internal address ranges.

## Discovery connectivity prerequisites

1. Resolve the assigned Discovery Engine hostname to the approved source IP.
2. Confirm route and packet flow through the relevant firewall zones.
3. Confirm Windows firewall Domain profile application.
4. Confirm host and network firewall direction match the approved implementation.
5. Confirm DNS and AD connectivity from the assigned Discovery Engine.
6. Test only the required ports and source addresses.

## Validation procedure

1. Document the source hostname and source IP used for the test.
2. Capture current route and firewall evidence.
3. From the assigned Discovery Engine, test RPC, SMB, and any approved discovery protocols against a test server.
4. Record success or failure for each protocol.
5. Attempt a denied test from an unapproved source if safely authorized.
6. Confirm that no excessive source scope or alternate route exists.
7. Attach evidence to the change record.

## Rollback

1. Remove or disable newly created temporary rules only after approval.
2. Restore the exact prior host and network firewall configuration.
3. Revalidate discovery and unrelated system connectivity.
4. Preserve the change and rollback evidence.

## Stop conditions

Stop implementation and escalate when:

- A hostname cannot be mapped to an approved IP.
- A required source or destination is unknown.
- The supplied traffic direction conflicts with the environment.
- A rule would require a broad or unrestricted remote scope.
- Existing firewall policy conflicts cannot be identified.

## Source and validation status

**Confirmed:** Approved source IPs, engine hostnames, supplied port matrix, Domain profile policy, and source restriction requirement.  
**TBC:** Hostname mapping, exact protocol use, traffic direction, exact RPC range, and host/network firewall split.
