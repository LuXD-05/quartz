### Database

**Container used to store info** managed by the information system and contains files (saved on mass memory) logically organized to represent reality.

###### Types

- **Small** db: stored on a <u>file system</u>,
- **Large** db: hosted on <u>pc clusters or cloud storage</u>.

###### Actions

These are: search, retrieve, edit, delete... data.

### Tables

Db are organized in **tables**, lists of <u>rows</u> and <u>columns</u>.

##### Record

(<u>Row</u>), a **meaningful and consistent way to combine info about something**.

##### Field

(<u>Column</u>), a **single item of info, one that appears in every record**.

### Keys

An attribute used to **sort/identify data**; they give meaning to data.

##### Types

- **Primary (PK)**: <u>specific choice of a minimal set of fields that uniquely identifies a row</u> in a relation,
- **Alternate (AK)**: candidate key to be primary, but isn’t,
- **Foreign (FK)**: <u>refers to the PK of another table</u>.

### Schema

**Structure of a db**, or a **set of integrity constraints** imposed on a db (they ensure compatibility). The **schema** <u>doesn’t vary in time</u>.

### Instance

Collection of **info stored** in the db **at** a certain **moment**/instance **of time** (*snapshot* of the db). The **instance** does <u>vary in time</u>.

### Data models

Data structures to manage and interrogate dbs. **They classify databases**.

##### Non-Relational db models

- **Hierarchical**: data arranged in a <u>tree-like structure</u>. Nodes = entities, Arcs = relations. Rigidity: redundancy.
- **Flat-file**: data organized into a <u>single table</u> (*spreadsheets*).
- **Network/reticular**: organizes data in a <u>graph</u>. Access through several paths. Complex, no redundancy.
- **Object oriented**: data stored as <u>objects</u> belonging to classes.

##### Relational db models

**Simple and effective** (better represent reality), data in tables/files in fields and records. They use **SQL** (*Structured Query Language*) for queries.

### DBMS

It’s a **sw** system that **stores and organizes data** other than **retrieving data for apps**. Main features:

###### Data normalization

< risk, < data duplication (redundancy) and < chance of anomalies or inconsistencies.

###### User-defined constraints

Users can define constraints (rules) to prevent accidental damage to the db by authorized users.

###### Security protocols

Protects the integrity of db, data and records with encryption, user authentication and authorization.

###### Backups

Copy of the db data in case of loss or corruption by any mean. Used to reconstruct dbs.

###### Data structuring

DBMS allows users to define clear and hierarchical structures to organize information.

### Abstraction layers

Simplified representation of a db in the form of written description of diagram. 3 levels:

###### External/application level

Exposed to users and devs. Describes data as it’s seen. Provides tools for db operations (modify and see data).

###### Logical level

Describes all the items of interest of the app and offers detailed descriptions about records of data.

###### Internal/physical level

Used to store data. Implements the logical level.

##### Type of info stored in db

Ex: e-commerce app

- **Customer data**: emails, passwords, preferences…
- **Business data**: products colors, prices, ratings…
- **Relationship data**: location of store with specific product…

### A good db design

Principles of db design:

1) **Redundancy** (duplicated data) **is bad** (> wasted space & > error chance)
2) **Correctness and completeness of information** is important. If <u>not</u>, = <u>misinformation</u> (unintentional, <u>disinformation</u> = intentional).

A good db design, therefore:

- Divides info in subject-based tables (< redundancy),
- Gives access and information to join tables data together as needed,
- Ensures accuracy and integrity of info,
- Satisfies data processing and reporting needs.

### Database application

Sw whose purpose is retrieving (+ insert, update, delete…) info in/from a db. It facilitates simultaneous queries from multiple users (since mid-1990s, common to build db apps with web interface).

### Types of db apps

There are also dbs for homes & small businesses, like Access, Oracle, SQL Server, MySQL…

###### Accounting apps

Used for **financial data**. Record liabilities, inventory, transactions between customers and suppliers… (Microsoft Money)

###### CRM apps

Manages **relations of a business with clients** + marketing, sales, support for clients… goal: > sales, < costs… (Bitrix24?)

###### Web apps

**Websites as db apps**. Can incorporate db functions of accounting/CRM apps (Office 365 suite?).

