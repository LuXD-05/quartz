---
public: true
edited_seconds: 10
modified_at: 02/04/2024 11:14:33
---
Cloud Computing

Is the on-demand availability & delivery of resources (computing, storage capacity…) as services to end users. Cloud computing shares resources on-demand using a pay-as-you-go model.

Large clouds often distribute functions over multiple locations, called datacenters.

Characteristics

-      **On-demand self-service** --> resources are required automatically when needed without human interaction,

-      **Broad network access** --> resources are available over internet and accessed through client platforms,

-      **Resource pooling** --> the provider’s **resources** are **pooled** to serve **multiple consumers** (dynamically assigned to each),

-      **Rapid elasticity** --> capabilities are elastically provided and released (sometimes automatically).

-      **Measured service** --> cloud systems **auto control/optimize** **resource use** by **measuring**/**monitoring** user’s **activity**.

IaaS

Refers to **physical/virtual machines** (run as **guests** by the **hypervisor**) offered **on-demand** (so > capabilities + < invest on hw).

Clients are able to **deploy** & **run** **sw** (like OS and apps). The client doesn’t manage the cloud infrastructure, but **controls**:

-      OS,

-      Storage,

-      Deployed applications,

-      (Maybe limited control of networking components like firewalls…)

Why use IaaS?

So, you **won't have to buy & manage** the **hw**. [IaaS is billed on a **utility computing basis** (cost = n° of resources allocated)].

PaaS

Refers to a pc platform including: OS, programming environment, db & web server. With this devs can deploy and run sw on a cloud platform without having to buy & manage the underlying hw & sw. The client doesn’t manage the cloud infrastructure + network, servers, OS or storage, but **controls**:

-      Deployed applications,

-      Data,

-      (Maybe configuration settings for the application-hosting environment).

SaaS

Apps are installed & running in the cloud, & are accessible from various client devices through a browser/interface.

The client doesn’t manage the cloud infrastructure or the platform (network, servers, OS, storage…), but **controls**:

-      The used application (not its capabilities, but its **results**/**outputs**),

-      (Maybe limited user-specific configuration settings).

With SaaS the client doesn’t need to install the application; and SaaS is often referred as on-demand service and usually priced on a pay-per-use basis or with a subscription fee.

Public Cloud Computing

A **multi-tenant environment** in which **servers** **shares** the same **resources** as others tenants in cloud (usually pay-as-you-go).

Cloud services are “**public**” when delivered over the public internet & can be free or paid (with subscription).

Few differences between public & private cloud, but **security concerns** increase as services are shared by multiple users.

With a public cloud, all sw and hw and other infrastructure are owned and managed by the cloud provider

In a public cloud you share the same hw, storage & network with other cloud "tenants" & access service with browser.

Public cloud deployments often provide: webmail, online office apps, storage, testing and dev environments.

Advantages

-      Low costs --> no need to buy hw or sw, you pay only for the service that you use,

-      No maintenance --> service providers provide maintenance,

-      Near unlimited scalability --> on-demand resources are available to meet your business needs,

-      High reliability --> vast network of services ensures against failures.

Private Cloud Computing

Is a single-tenant environment that:

-      Is dedicated to a single client/company (so it’s customizable & maintained on a private network),

-      Is hosted & managed internally (on-site) or by an external 3rd-party (outsourced),

-      (Hw is dedicated, so client always pays a fixed amount).

Private clouds are often user by government agencies, financial institutions or other companies which need enhanced control over their environment

Advantages

-      More **flexibility** --> the organization can customize its cloud environment,

-      More **control** --> higher privacy, because resources are not shared (outside of the company),

-      More **scalability** --> more scalability than on-premise (in sede) infrastructures.

Hybrid Cloud Computing

A cloud that combines on-premise infrastructure (private cloud) with a public cloud; allowing data sharing between the 2.

Hybrid cloud is evolving to include edge workloads. By moving workloads to the edges (closer to the devices where data resides) devices spend less time communicating = < latency and ability to operate reliably in extended offline periods.

Benefits

Hybrid cloud **benefits**: > flexibility, > deployment options, security, compliance, > value from existing infrastructure.

In case of overflows (too much info to process), hybrid cloud seamlessly scales up the on-premises infrastructure with the public cloud to handle the situation (without giving third party datacenters access to data).

Hence companies can run certain workloads in the cloud while keeping highly sensitive data in their own datacenter.

Advantages

-      Control --> org can maintain a private infrastructure for sensitive data & workloads that need low latency,

-      Flexibility --> additional resources in the public cloud can be used when needed,

-      Cost-effectiveness --> since public cloud can be scaled up, only the needed extra computing power is paid,

-      Ease --> the migration isn’t overwhelming because it can be done gradually over time.

Public, Private or Hybrid?

There's no one type of cloud computing that's right for everyone.

Different cloud computing models, types and services have evolved to meet the rapidly changing tech needs of orgs.