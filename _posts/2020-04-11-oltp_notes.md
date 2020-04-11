---
title: "OLTP database notes"
date: 2020-04-11
tags: [oltp, db]
---


# OLTP databases

An OLTP system is a common data processing system characterized via a specific data usage that is different from data warehouse environments. Classic examples of OLTP systems are order entry, retail sales, and financial transaction systems etc.

Main characteristics of OLTP systems are:
- Short response time
- Small transactions
- High concurrency
- Large user populations
- High availability
- Etc.

## Common considerations when designing an OLTP database

### Performance
The goal here is to minimize latency and process transactions in milliseconds. Are you looking at a high transaction rate like a busy web site or low use like a small company HR system? Will your users be doing many updates/inserts or is it mainly read only?

### Availability
The ability to keep going, even if one or more nodes in the system fail or are temporarily disconnected from the network. Do you need 24x7, 16x5 or other uptime, 24x7 is much harder to do as you have no down time for maintenance? Do you need to look at enterprise cluster with hot fail over, or just normal hosting?

### Scalability
The ability to incrementally scale to massive data volumes and transaction velocity. How many users, what are the usage patterns (peak load or evenly distributed)? How big is the DB going to go? If it's really big you'll have to design your tables to take account of that and/or partition. Do you need to look at enterprise cluster with hot fail over, or just normal hosting?

### Consistency
To provide consistent, accurate results — particularly in the event of network failures or in high concurrency transactions where users are trying to access the same data at the same time. For example, an online auction website can have hundreds of thousands (if not millions) of users accessing data on its website at the same time.


### Durability
To ensure changes once committed are not lost.

### Backup & Archiving
- Online or offline backups
- Size of backups
- Incremental vs dump
- Archiving strategy

### Security
Is security a big issue - are you handling personal details, or financial data. Or is it just a product catalogue. Do you need to setup passwords, permissions and views.
