# HOW TO START PSQL IN UBUNTU 
Type the commands : 
- `> sudo -i -u postgres`
- `> psql`

# SEE WHICH USER IS CONNECTED
- `> \conninfo`

# LIST ALL USERS AND THER ROLES
- `> \du`

# LIST ALL DATABASES
- `> \l`

 
# HOW TO MODIFY USER PASSWORD 
- `> ALTER USER user_name WITH PASSWORD 'new_password';`

# HOW TO ADD A SUPERUSER
- `CREATE ROLE username WITH LOGIN SUPERUSER PASSWORD 'password';`

# HOW TO CREATE A DATABASE
- `> CREATE DATABASE database_name;`

# HOW TO CHANGE DATABASE OWNER
- `ALTER DATABASE database_name OWNER TO new_owner;`

# HOW TO CONNECT TO A DATABASE
- `psql -h localhost -U username -d mydatabase`