#Over View of Database Management

**Definition (Database):**  A laarge and persistent collection of (more or les similar) pieces of information organized in a way that facilitates efficient retrieval and modifcation

**Definition (Database Managment System (DMBS)):** A programm (or set of progams) that manages details related to storage and access of a database

**Definition (Schema):** A description of the data interface to the database (how the data is organized)
1. External Schema (view): What the application progaams and user see. May differ for different users of the same database.
2. Conceptual Schema: description of the logicl structure of all data in the database.
3. Physical/internal schema: description of physical aspects (selection of files, devices, stroage algorithms)

**Definition (Instance):** A database instance is a database (real data) that conforms to a given schema. 
- A schema can have many instances

**Data Independence**: Applications do not access data directly but, rather through an abstract data model provided by the DBMS

Two kinds of data independence

* Physical: applications immune to changes in storage structures
* Logical: applications immune to changes in data organizations

**Data Definition Language DDL**
for specifying schemas
* may have different DDLS for external schema, conceptual schema, internal schema
* informaion is sotred in the data dictionary or catalog
* granting privileges - sometimes separated as Datal Control Languages (DCL)

**Data Manipulation Language (DML)**
for specifying queries and updates
* navigational (procedural)
* non-navigational (Declarative)

**Definition (Transaction)**
An application-specified atomic and durable unit of work

Properties of transactions ensured by the DBMS(ACID)
Atomic: A transaction occurs entirely, or not at all
Consistency: each transaction preserves the consistsency of the database
Isolated: concurrent transactions do not interfer with each other
Durable: once completed, a transaction's changes are permanent
