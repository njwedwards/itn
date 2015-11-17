---
title: Postgres readonly access
author: nedwards
layout: post
categories:
  - Postgres
tags:
  - Postgres
---
Having used MySQL quite a bit in the past. I have been used to being able to setup a read only user for a database. In PostgreSQL things work a bit differently. In order to allow read only access you need to assign SELECT access on each table to a role.

The following seems to work.

**Login to database**

psql database

**Create readonly role**

CREATE ROLE readonly;

**Create readonly\_for\_database.sh**

This will grant select access on every table.

    
    #!/bin/sh
    
    tables=$(psql database -A -t -c "SELECT table_name FROM information_schema.tables  
    WHERE table_schema = 'public';")
    
    for table in $tables
    do
    echo "Granting select to readonly on $table"
    psql database -c "GRANT SELECT ON $table to readonly;"
    done
    
    

**Grant readonly role to existing user**

GRANT readonly TO existinguser;

Once this is done you will be able to give users read only access to the database.
