---
title: "OLTP Design notes"
date: 2020-04-11
tags: [oltp, conceptual schema, logical schema, physical schema, db]
---


# How to design an OLTP database

The path to designing an OLTP database goes through three different stages:
![alt text](/images/oltp/oltp1.png)

## The Conceptual Model
![alt text](/images/oltp/conceptual_model.png)

- A ‘Computer Independent Model’ (CIM)
- Identifies business concepts (or ‘Business Objects’) and their relationships. No attribute and no primary key specified here.
- Data Architects and Business Architects work here

## The Logical Model
![alt text](/images/oltp/logical_model.png)

- A ‘Platform Independent Model’ (PIM)
- A design of data structures to support the CIM but not designed for any particular platform. Features of a logical data model include:
    - Includes all entities and relationships among them.
    - All attributes for each entity are specified.
    - The primary key for each entity is specified.
    - Foreign keys (keys identifying the relationship between different entities) are specified.
    - Normalization occurs at this level.
- Data Modellers, Systems Analysts and Business Analysts work here

The basis for an ideal data model is formed from 3 ideas:
- Entities: concepts important to the business about which they wish to hold data and information
- Attributes: the pieces of data held about each concept (entity)
- Associations: important facts in the domain that tie entities together in a significant way

## The Physical Model
![alt text](/images/oltp/physical_model.png)

- A ‘Platform Specific Model’ (PSM)
- Interprets the PIM as it will be built in the database – generally as a schema. Features of a physical data model include:
    - Specification all tables and columns.
    - Foreign keys are used to identify relationships between tables.
    - Denormalization may occur based on user requirements.
    - Physical considerations may cause the physical data model to be quite different from the logical data model.
    - Physical data model will be different for different RDBMS. For example, data type for a column may be different between MySQL and SQL Server.
- DBAs and Developers work here

The steps for physical data model design are as follows:
1. Convert entities into tables.
2. Convert relationships into foreign keys.
3. Convert attributes into columns.
4. Modify the physical data model based on physical constraints / requirements.
