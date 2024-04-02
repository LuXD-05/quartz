---
public: true
edited_seconds: 20
modified_at: 02/04/2024 11:14:51
---
Database

**Container used to store information** managed by the information system (efficient = no redundancy, effective = fast).

It contains files (saved on mass memory) logically organized to represent reality.

-      **Small** db --> stored on a **file system**,

-      **Large** db --> hosted on **pc clusters** or **cloud storage**.

Actions

-      Search data,

-      Retrieve data (generate reports),

-      Edit/delete data…

Tables

Db are organized in **tables**, **lists of rows and columns**.

Record (row)

**Meaningful and consistent way to combine information about something**.

Field (column)

**Single item of information, one that appears in every record**. (Key field --> holds unique data that identifies the record)

Keys

An **attribute used to sort/identify data**; they give meaning to data.

-      **Primary (PK)** --> **specific choice of a minimal set of fields that uniquely identifies a row** in a relation,

-      **Alternate (AK)** --> candidate key to be primary, but isn’t,

-      **Foreign (FK)** --> **refers to the PK of another table**.

Schema

**Structure** (in formal language) **of a db**, or, a **set of integrity constraints imposed on a db** (they ensure compatibility).

The **schema doesn’t vary in time**.

Instance

**Collection of information stored in the db at a certain moment/instance of time** (**snapshot** of the db).

The **instance does vary in time**.

Data models

Data structures to manage and interrogate dbs. **They classify databases**.

Non-Relational db models:

-      **Hierarchical** --> data arranged in a **tree-like structure**. **Nodes** = entities, **Arcs** = relations. Rigidity: **redundancy**.

-      **Flat-file** --> data organized into a **single table** (**spreadsheets**).

-      **Network/reticular** --> organizes data in a **graph**. Access through **several paths**. **Complex**, **no redundancy**.

-      **Object oriented** --> data stored as **objects belonging to classes**.

Relational db models:

Simple and effective (better represent reality), data in tables/files in fields and records.

SQL (Structured Query Language)

Language used for queries.

DBMS

It’s a **software** system that **stores and organizes data** other than **retrieving data for apps**. Main features:

Data normalization

**< risk, <** data duplication (**redundancy**) & **< chance of** anomalies or **inconsistencies**.

User-defined constraints

Users can define **constraints** (rules) to prevent accidental damage to the db by authorized users.

Security protocols

Protects the **integrity of db**, data and records with **encryption**, user **auth**entication and authorization.

Backups

**Copy of the db data in case of loss or corruption** by any mean. Used to reconstruct dbs.

Data structuring

DBMS allows users to define clear and **hierarchical structures** to organize information.

Abstraction layers

Simplified representation of a db in the form of written description of diagram. 3 levels:

External/application level

Exposed to users and devs. Describes data as it’s seen. Provides tools for db operations (modify and see data).

Logical level

Describes all the items of interest of the app and offers detailed descriptions about records of data.

Internal/physical level

Used to store data. Implements the logical level.

Type of information stored in a db

Ex: e-commerce app

-      Customer data --> emails, passwords, preferences…

-      Business data --> products colors, prices, ratings…

-      Relationship data --> location of store with specific product…

A good db design

Principle guide db design:

1)    **Redundancy** (duplicated data) **is bad** (> wasted space & > error chance)

2)    **Correctness and completeness of information** is important. If **not**, = **misinformation** (unintentional, dis… = intentional).

A good db design, therefore:

-      Divides info in subject-based tables (< redundancy),

-      Gives access and information to join tables data together as needed,

-      Ensures accuracy and integrity of info,

-      Satisfies data processing and reporting needs.

Database application

**Program whose purpose is retrieving** (**& insert, update, delete…**) **information from a db**. It facilitates **simultaneous** **queries** from **multiple** **users** (since mid-1990s, common to build db apps with web interface).

Users POV

There are also dbs for homes & small businesses, like **Access, Oracle, SQL Server, MySQL**…

Accounting apps

Used for financial data. Record liabilities, inventory, transactions between customers and suppliers…

CRM apps

Manages relations of a business with clients + marketing, sales, support for clients… goal: > sales, < costs…

Web apps

Websites as db apps. Can incorporate db functions of accounting/CRM apps.