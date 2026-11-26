# PAM 2.0 Infrastructure Architecture

## Purpose

This document describes the physical deployment topology of the PAM 2.0 platform, including web servers, databases, RabbitMQ clusters, Distributed Engines, load balancing components, and high availability design.

## Infrastructure Overview

The Delinea PAM platform is deployed across:

- Primary Datacenter (GOT)
- Secondary / DR Datacenter (Cloud)
- Manufacturing DMZ (vccmfg.net)
- F5 Global and Local Load Balancing Layer

## Physical Topology

```mermaid
flowchart TB
    User[PAM User]
    GLB[pam.volvocars.net]

    subgraph Primary Datacenter (GOT)
        WEB1[WEB1]
        WEB2[WEB2]
        DB1[DB1]
        DB2[DB2]
        AOAG[DB-AOAG]
        MQ1[MQ1]
        MQ2[MQ2]
        MQ3[MQ3]
        DE1[DE1]
    end

    subgraph DR Datacenter (Cloud)
        WEB3[WEB3]
        WEB4[WEB4]
        DB3[DB3]
        MQ4[MQ4]
        MQ5[MQ5]
        MQ6[MQ6]
        DE2[DE2]
    end

    subgraph DMZ
        DE3[DE3]
        DE4[DE4]
    end

    User --> GLB
```

# Infrastructure Inventory

## Primary Datacenter (GOT)

### Database Layer

| Reference | FQDN | IP Address | Component |
|------------|------------|------------|------------|
| DB1 | gotsvw12236.got.volvocars.net | 10.122.84.78 | Database Server |
| DB2 | gotsvw12238.got.volvocars.net | 10.122.84.100 | Database Server |
| DB-AOAG | gotsvw12236vc.got.volvocars.net | 10.122.84.98 | SQL Always On Availability Group Listener |
| DB-WSFC | gotsvw12238vc.got.volvocars.net | 10.122.84.101 | Windows Server Failover Cluster |

### Web Tier

| Reference | FQDN | IP Address | Component |
|------------|------------|------------|------------|
| WEB1 | gotsvw12243.got.volvocars.net | 10.122.84.93 | Delinea Web Server |
| WEB2 | gotsvw12244.got.volvocars.net | 10.122.84.94 | Delinea Web Server |

### RabbitMQ Layer

| Reference | FQDN | IP Address | Component |
|------------|------------|------------|------------|
| MQ1 | gotsvw12303.got.volvocars.net | TBD | RabbitMQ Node |
| MQ2 | gotsvw12304.got.volvocars.net | TBD | RabbitMQ Node |
| MQ3 | gotsvw12252.got.volvocars.net | 10.122.84.34 | RabbitMQ Node |

### Distributed Engine Layer

| Reference | FQDN | IP Address | Component |
|------------|------------|------------|------------|
| DE1 | gotsvw12245.got.volvocars.net | 10.122.84.95 | Distributed Engine |

---

## Secondary / DR Datacenter (Cloud)

### Database Layer

| Reference | FQDN | IP Address | Component |
|------------|------------|------------|------------|
| DB3 | closvw1985.cloud.volvocars.net | 10.46.158.74 | Database Server |

### Web Tier

| Reference | FQDN | IP Address | Component |
|------------|------------|------------|------------|
| WEB3 | closvw1979.cloud.volvocars.net | 10.46.158.68 | Delinea Web Server |
| WEB4 | closvw1982.cloud.volvocars.net | 10.46.158.69 | Delinea Web Server |

### RabbitMQ Layer

| Reference | FQDN | IP Address | Component |
|------------|------------|------------|------------|
| MQ4 | closvw1981.cloud.volvocars.net | 10.46.158.70 | RabbitMQ Node |
| MQ5 | closvw1983.cloud.volvocars.net | 10.46.158.72 | RabbitMQ Node |
| MQ6 | closvw1984.cloud.volvocars.net | 10.46.158.73 | RabbitMQ Node |

### Distributed Engine Layer

| Reference | FQDN | IP Address | Component |
|------------|------------|------------|------------|
| DE2 | closvw1980.cloud.volvocars.net | 10.46.158.71 | Distributed Engine |

---

## Manufacturing DMZ Environment (vccmfg.net)

### Distributed Engine Layer

| Reference | FQDN | IP Address | Component |
|------------|------------|------------|------------|
| DE3 | gotsvw12299.vccmfg.net | 10.122.128.87 | Distributed Engine |
| DE4 | gotsvw12300.vccmfg.net | 10.122.128.88 | Distributed Engine |

---

## Load Balancing Layer

### Global Traffic Managers

| Reference | FQDN | IP Address | Function |
|------------|------------|------------|------------|
| GLB1 | pam.volvocars.net | 10.40.140.159 | Global Traffic Manager (User Access) |
| GLB2 | pam-mq.volvocars.net | TBD | Global Traffic Manager (RabbitMQ) |

### Local Traffic Managers

| Reference | FQDN | IP Address | Function |
|------------|------------|------------|------------|
| LLB1 | pam-site1.volvocars.net | 10.40.140.157 | Primary Site Web Load Balancer |
| LLB2 | pam-site2.volvocars.net | 10.40.140.156 | DR Site Web Load Balancer |
| LLB3 | pam-mq-site1.volvocars.net | 10.40.138.69 | Primary Site RabbitMQ Load Balancer |
| LLB4 | pam-mq-site2.volvocars.net | TBD | DR Site RabbitMQ Load Balancer |

---

# Infrastructure Summary

| Layer | Components |
|---------|---------|
| Global Load Balancing | GLB1, GLB2 |
| Local Load Balancing | LLB1, LLB2, LLB3, LLB4 |
| Web Tier | WEB1, WEB2, WEB3, WEB4 |
| Database Tier | DB1, DB2, DB3 |
| SQL Availability | DB-AOAG, DB-WSFC |
| RabbitMQ Cluster | MQ1, MQ2, MQ3, MQ4, MQ5, MQ6 |
| Distributed Engines | DE1, DE2, DE3, DE4 |

---

# Infrastructure Capacity Summary

| Component Type | Quantity |
|----------------|----------|
| Web Servers | 4 |
| Database Servers | 3 |
| SQL Cluster Services | 2 |
| RabbitMQ Servers | 6 |
| Distributed Engines | 4 |
| Global Load Balancers | 2 |
| Local Load Balancers | 4 |
| Total Managed PAM Infrastructure Nodes | 25 |

