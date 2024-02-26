# HOW TO START PSQL IN UBUNTU 
Type the commands : 
- `> sudo -i -u postgres`
- `> psql`

# HOW TO MODIFY USER PASSWORD 
- `> ALTER USER user_name WITH PASSWORD 'new_password';`

# HOW TO ADD A SUPERUSER
- `CREATE ROLE 'username' WITH LOGIN SUPERUSER PASSWORD 'password';`

# HOW TO CHANGE DATABASE OWNER
- `ALTER DATABASE database_name OWNER TO new_owner;`

