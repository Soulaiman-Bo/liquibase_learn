

Here's a **README** file containing a list of essential Liquibase commands for managing your PostgreSQL database in Docker:

---

# Liquibase Command List

This README provides a list of essential Liquibase commands to help manage a PostgreSQL database within a Dockerized environment. Each command includes a description and example usage.


## Prerequisites

Before running Liquibase commands in this directory, ensure you have the following setup:

1. **Java Installation**:  
   Liquibase requires Java. Install Java if it's not already available:

   ```bash
   sudo apt update
   sudo apt install default-jdk -y
   ```

2. **Liquibase Installation**:  
   Download and install Liquibase from [Liquibase Downloads](https://www.liquibase.org/download).

3. **PostgreSQL JDBC Driver**:
   - The `postgresql-42.6.0.jar` file in this directory is the PostgreSQL JDBC driver required for Liquibase to connect to a PostgreSQL database. Ensure this file is in the same directory as Liquibase.

4. **Docker and Docker Compose**:
   - Ensure Docker and Docker Compose are installed, as `compose.yml` will be used to run the PostgreSQL database in a Docker container.

5. **Liquibase Properties Configuration**:
   - Verify that `liquibase.properties` is configured with the correct details to connect to the Dockerized PostgreSQL database. Here’s a sample configuration based on your setup:

     ```properties
     changeLogFile=changelog.yaml
     driver=org.postgresql.Driver
     url=jdbc:postgresql://localhost:5432/mydb
     username=myuser
     password=mypassword
     ```

6. **Docker Compose Setup**:
   - Use `compose.yml` to start your PostgreSQL database in Docker:

     ```bash
     docker-compose -f compose.yml up -d
     ```

7. **Changelog Files**:
   - The `changelog.yaml` file acts as the main changelog, and it should include or reference additional changesets (e.g., `changeLog_1.yaml`, `changeLog_2.yaml`, etc.) that define specific database changes.

After completing these prerequisites, you should be ready to run Liquibase commands for database management.



## Liquibase Command List

### 1. Update Command
Applies the changes from your changelog file to the database.

```bash
liquibase --classpath=./postgresql-42.6.0.jar update
```

### 2. Drop All Objects
Removes all database objects (e.g., tables, views, stored procedures). **Use with caution in non-development environments.**

```bash
liquibase --classpath=./postgresql-42.6.0.jar dropAll
```

### 3. Generate Changelog
Creates a changelog file based on the current state of the database. This is useful for generating an initial schema snapshot.

```bash
liquibase --classpath=./postgresql-42.6.0.jar generateChangeLog
```

### 4. Rollback Command
Rolls back the last set of changes or a specific set of changes based on tags or dates.

- Roll back the last changeset:

  ```bash
  liquibase --classpath=./postgresql-42.6.0.jar rollbackCount 1
  ```

- Roll back to a specific tag:

  ```bash
  liquibase --classpath=./postgresql-42.6.0.jar rollback <tag_name>
  ```

### 5. Status Command
Displays which changesets have not been applied to the database.

```bash
liquibase --classpath=./postgresql-42.6.0.jar status
```

### 6. Update SQL Command
Generates the SQL commands for an update without applying them, allowing you to review changes.

```bash
liquibase --classpath=./postgresql-42.6.0.jar updateSQL
```

### 7. Clear Checksums
Clears all checksums in the `DATABASECHANGELOG` table. Use this if you encounter checksum errors after modifying a changelog.

```bash
liquibase --classpath=./postgresql-42.6.0.jar clearCheckSums
```


### 8. Summary

```bash
liquibase --classpath=./postgresql-42.6.0.jar history 

liquibase --classpath=./postgresql-42.6.0.jar status 

liquibase --classpath=./postgresql-42.6.0.jar validate 

liquibase --classpath=./postgresql-42.6.0.jar update 

liquibase --classpath=./postgresql-42.6.0.jar rollback 1 

liquibase --classpath=./postgresql-42.6.0.jar rollback count  1 

liquibase --classpath=./postgresql-42.6.0.jar updateSQL
```
