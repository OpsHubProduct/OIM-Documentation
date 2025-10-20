## Description

<code class="expression">space.vars.SITENAME</code> provides installation options with these 5 types of databases: HSQL, MYSQL, MS SQL, ORACLE, PostgreSQL. Among these, which one is our recommended database for <code class="expression">space.vars.SITENAME</code> installation?

## Solution

If <code class="expression">space.vars.SITENAME</code> is being installed for POC (Proof of Concept) purpose or no other database server is available, then HSQL can be used as this is the in-built database provided by <code class="expression">space.vars.SITENAME</code>. But if <code class="expression">space.vars.SITENAME</code> is going to be used for production purpose, then HSQL is not recommended as it is not scalable. One of the below database options can be used for installation:

1. MySQL  
2. MS SQL / Azure SQL  
3. Oracle  
4. PostgreSQL  

For database related pre-requisites, please refer to [Database Prerequisites](../../../getting-started/prerequisites.md#database-prerequisites).

