---
copyright:
  years: 2014, 2018
lastupdated: "2017-11-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# MySQL Optimization/Repair Information

## How MySQL Uses Memory 
The following are some of the ways that the mysqld server uses memory, and associated mysqld variable names.
* [Memory Use MySQL 5.0 ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://dev.mysql.com/doc/refman/5.0/en/memory-use.html){: new_window}
* [Memory Use MySQL 4.1 ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://dev.mysql.com/doc/refman/4.1/en/memory-use.html){: new_window}

## MySQL Optimization covers the following items:
- Optimization Overview
- Optimizing SELECT and Other Statements
- Locking Issues
- Optimizing Database Structure
- Optimizing the MySQL Server
- Disk Issues

[Optimization MySQL 5.0 ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://dev.mysql.com/doc/refman/5.0/en/optimization.html){: new_window}
[Optimization MySQL 4.1 ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://dev.mysql.com/doc/refman/4.1/en/optimization.html){: new_window}

## MySQL Server Variables - SQL layer or Storage Engine specific.
The following links list some of the more common variables.
[Go to article 1 ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.mysqlperformanceblog.com/2006/06/08/mysql-server-variables-sql-layer-or-storage-engine-specific/){: new_window}
[Go to article 2 ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://forge.mysql.com/wiki/ServerVariables){: new_window}

## Optimizing the mysqld variables by Ian Gilfillan
See this article on MySQL optimization, including some guidelines on setting mysqld server variable.
(key_buffer_size, Query cache variables, table_cache, sort_buffer, etc..)
[Go to article ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.databasejournal.com/features/mysql/article.php/3367871){: new_window}

## Repairing Database Corruption in MySQL by Ian Gilfillan
Table corruption is rare when you use {{site.data.keyword.mysql}}. However, it helps to know how to fix the problem when it occurs.
[Go to article ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.databasejournal.com/features/mysql/article.php/3300511){: new_window}

## Optimizing MySQL: Queries and Indexes by Ian Gilfillan
<!--The database is too slow. Queries are queuing up, backlogs growing, users being refused connection. Management is ready to spend millions on "upgrading" to some other system, when the problem is really that MySQL is simply not being used properly. Badly defined or non-existent indexes are one of the primary reasons for poor performance, and fixing these can often lead to phenomenal improvements.-->
[Go to article ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.databasejournal.com/features/mysql/article.php/1382791){: new_window}

[Other {{site.data.keyword.mysql}} articles by Ian Gilfillan ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.databasejournal.com/article.php/1474351){: new_window}
