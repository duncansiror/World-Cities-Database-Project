# Create a database user 

First, enter MySQL while logged in as root user `mysql -p`.

<img width="408" height="88" alt="mysql_p" src="https://github.com/user-attachments/assets/c85279bd-b243-4d68-97ff-5df7ade80f56" /></br>

Create database user with the following syntax: `CREATE USER 'username'@'localhost';` This user must already exist as a Linux user.

<img width="752" height="86" alt="createuser" src="https://github.com/user-attachments/assets/3a4ef584-3bd0-4ca0-957d-5e1b87cd4e54" /><br/>

Grant the user a password: `ALTER USER 'username'@'localhost' IDENTIFIED BY 'Password';`

<img width="1134" height="88" alt="alteruser" src="https://github.com/user-attachments/assets/96103251-daae-4d11-914e-8514e31c2953" /><br/>

Grant new user full access to all databases and all tables associated with given databases: `GRANT ALL PRIVILEGES ON *.* TO 'username'@'localhost' WITH GRANT OPTION;

<img width="1274" height="86" alt="grant" src="https://github.com/user-attachments/assets/9ca50d61-1d6f-42f3-8105-61b2d911ca31" /><br/>


