+++
title = "*postgresql"
author = ["PENG Kui"]
draft = false
+++

## postgresql {#postgresql}


### setup {#setup}

`sudo apt-get install postgresql`
predefined user: `postgres`, no auth
predefined roles: many, mostly are used to auth `privileged`
predefined database: `postgres`, `template0`, `template1`
configure file location: `/etc/postgresql/12/main/postgresql.conf`


### login {#login}

`sudo service postgresql restart` to start postgresql server
`sudo su - postgres`
`psql`


### command {#command}


#### help {#help}

`\?` for all help
 `\h` list all available command
`\h Command` for sql command detail help
`\h create user`
`\h create db`
`\i filename` to run cmd from file


#### query {#query}

`\s` show history command
`\l` list database
`\du` list roles/users
`\dxxx` list many other info in database
`\conninfo` list current connect information
`SELECT current_database();`  list current_database
`\c database_name` change database
`\dn` list schema
`select nspname from pg_catalog.pg_namespace` list all schema in current db
`select * from information_schema.tables where table_name = 'name'` list tables
`SELECT typname from pg_catalog.pg_type where typname ~ '^_';` use regexp eg.


#### privileg {#privileg}

change password `\password`
change privileg `alter role <name> with <privileg>`
change current_user `set role <name>`, unable to change session_user(need relogin)
assign database privileg to user `GRANT all privileges on database <db> to <role>`
make a database public for all user/role:
`GRANT ALL ON DATABASE test TO public;`


#### ADC {#adc}

add
delete
change


#### sql language {#sql-language}


### config in emacs {#config-in-emacs}


### coding style {#coding-style}

<https://www.postgresql.org/docs/12/source.html>


### key concept {#key-concept}

role
: no user, group concept, user/group are implement by role

schema
: 1.  information_schema
        provide view
    2.  pg_catalog
        system schema, contain all psql system information

types
: -   Boolean(bool), Enum, Bit, bytea
    -   Character(char, varchar, text)
    -   -   integer(smallint=int2, int=int4, int8, serial)
        -   float(float&lt;n=4,8&gt;,realor, numberic)
    -   time(date,time,timestamp,interval)
    -   uuid(uuid)
    -   array([])
    -   json(json, jsonb)
    -   hstore(hash pair)
    -   network address(inet,maciddr), inet is ipv4 address
    -   geometric object(box, line, point, lseg, polygon)
    -   money(money)
    -   CREATE TYPE xxx

functions
:
