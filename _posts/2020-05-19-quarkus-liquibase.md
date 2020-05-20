---
title: Quarkus - Liquibase
---

Liquibase is an open source tool for database schema change management.

## In pom.xml, add the following dependencies
```xml
    <!-- Hibernate ORM specific dependencies -->
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-hibernate-orm</artifactId>
    </dependency>
    
    <!-- Liquibase specific dependencies -->
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-liquibase</artifactId>
    </dependency>

    <!-- JDBC driver dependencies -->
    <dependency>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-jdbc-postgresql</artifactId>
    </dependency>

```
# configure data source in application.property
```
# configure your datasource
quarkus.datasource.db-kind=postgresql
quarkus.datasource.username=sarah
quarkus.datasource.password=connor
quarkus.datasource.jdbc.url=jdbc:postgresql://localhost:5432/mydatabase
```

## add your changeLog to the src/main/resources/db/changeLog.xml file as you usually do with Liquibase
```


<?xml version="1.1" encoding="UTF-8" standalone="no"?>
<databaseChangeLog xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
    xmlns:ext="http://www.liquibase.org/xml/ns/dbchangelog-ext"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog-ext
    http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-ext.xsd
    http://www.liquibase.org/xml/ns/dbchangelog
    http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-3.5.xsd">

    <changeSet author="quarkus" id="1">
        <createTable tableName="quarkus">
            <column name="ID" type="VARCHAR(255)">
                <constraints nullable="false"/>
            </column>
            <column name="NAME" type="VARCHAR(255)"/>
        </createTable>
    </changeSet>
</databaseChangeLog>

```

## activate the migrate-at-start option to migrate the schema automatically
```
# Liquibase minimal config properties
quarkus.liquibase.migrate-at-start=true

# Liquibase optional config properties
# quarkus.liquibase.change-log=db/changeLog.xml
# quarkus.liquibase.validate-on-migrate=true
# quarkus.liquibase.clean-at-start=false
# quarkus.liquibase.database-change-log-lock-table-name=DATABASECHANGELOGLOCK
# quarkus.liquibase.database-change-log-table-name=DATABASECHANGELOG
# quarkus.liquibase.contexts=Context1,Context2
# quarkus.liquibase.labels=Label1,Label2
# quarkus.liquibase.default-catalog-name=DefaultCatalog
# quarkus.liquibase.default-schema-name=DefaultSchema
# quarkus.liquibase.liquibase-catalog-name=liquibaseCatalog
# quarkus.liquibase.liquibase-schema-name=liquibaseSchema
# quarkus.liquibase.liquibase-tablespace-name=liquibaseSpace
```

