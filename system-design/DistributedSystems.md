# Distributed Systems

### Summary

- [Definition](#definition)
    - [Advantages](#advantages)
    - [Issues](#issues)
- [Decentralized vs Distributed](#decentralized-vs-distributed)
- [Cloud vs Distributed Systems](#cloud-vs-distributed-systems)


### Definition

- A **collection of computers**, autonomous but working interdependently to form a single machine for the end-user.
- One shared state, operate concurrently.
- Able to fail independently without damaging the whole system (like *microservices*).
- Linked by a **network** to share information, communicate, and exchange information easily.

The user must be able to communicate with any machine without knowing it is only one machine. 
Most applications today use some form of a distributed database and must account for their *homogenous* or *heterogenous* nature.

**Homogenous distributed database**

- Each system shares the database management system and data model.
- Easier to manage by adding nodes. 

**Heterogeneous distributed database**

- Each system has different data models or varied database management systems, using gateways to translate data between nodes.

<br>

> An important part of distributed systems is the **CAP theorem** : a distributed data store cannot simultaneously be **consistent**, **available**, and **partition tolerant** (*see related document*).


### Advantages

- **Scalability** : Unlocks horizontal scalability.
- **Modular growth** : No limit in scalability capacity.
- **Fault tolerance**.
- **Cost effectiveness** : Initial cost higher than traditional system, but because of scalability, quickly becomes more cost effective.
- **Low latency** : Users can have a node in multiple locations, so traffic will hit the closet node.
- **Efficiency** : Breaks complex data into smaller pieces.
- **Parallelism**.


### Issues

- **Failure Handling** : Some components fail while others continue to function.Advantage to prevent large-scale failures, but also leads to more complexity troubleshooting and debugging.
- **Concurrency**.
- **Security** : Sharing data across multiple nodes increases risk. The network has to be secured, and users must be able to safely access replicated data across multiple locations.
- **Higher initial infrastructure costs** : Additional systems, processes, conception implied.

<br>

---


### Decentralized vs Distributed

**Distributed** > One entity (team/company) owns all the nodes.

**Decentralized** > Distributed on a technical level, usually not owned by a single entity. Harder to manage, as you cannot manage all the participants.

---


### Cloud vs Distributed Systems

The cloud offers some advantages over hardware distributed systems :

- More cost effective.
- Access to storage, servers, and databases from the internet.

However, the cloud is less flexible as the infrastructure is decentralized.
