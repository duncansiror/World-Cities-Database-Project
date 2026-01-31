# Import CSV into database 

Here, I will explain the steps of obtaining the CSV file, transferring it to the server, formatting the file, and importing into the database. 

## Obtain CSV

Download the CSV file from [Simple Maps](https://simplemaps.com/data/world-cities). The basic, free version will  be sufficient for this project. 

<img width="2344" height="1644" alt="simplemaps" src="https://github.com/user-attachments/assets/1a8ed9c7-27d1-4708-8a5c-07707c0bbe11" /></br>

This is what the CSV should look like: 

<img width="1562" height="694" alt="worldcitiescsv" src="https://github.com/user-attachments/assets/2a4a3cbe-5288-4354-8975-2bbe383322fc" /></br>

Install FileZilla and connect to the server with the same credentials as when using SSH.

<img width="3024" height="1572" alt="filezilla" src="https://github.com/user-attachments/assets/c6b24238-b813-4ebb-9841-75b62abe6b5a" />
As you can see by the status and the listing, the transfer was successful. It is also visible from the terminal.

<img width="352" height="132" alt="verifycsv" src="https://github.com/user-attachments/assets/9c876f2b-987c-4676-ad7f-890f6aa098a9" /><br/>

## Create database and table

Return to the server terminal and access MySQL with the previously created user. Create the database with `CREATE DATABASE mydb;`

<img width="596" height="82" alt="createdb" src="https://github.com/user-attachments/assets/cb441d9b-1907-4764-b162-d8828ef03277" /><br/>

Enter the database and create the table: `use mydb; DROP TABLE IF EXISTS worldcities;   CREATE TABLE worldcities (      city VARCHAR(120),  city_ascii VARCHAR(120), lat FLOAT,  lng FLOAT,  country VARCHAR(120),  iso2 VARCHAR(2),  iso3 VARCHAR(3),  admin_name VARCHAR(120), capital VARCHAR(7), population FLOAT, id VARCHAR(10))   CHARACTER SET=utf8mb4;` The columns of the table must match the colummns of the CSV file. A character set of utf8mb4 is used in order not to lose characters. MySQL utf8 uses a maximum of three bytes and cannot store four-byte unicode characters. 

## Format and move CSV

Create a new version of your CSV file without fieldnames (only data rows), replace all empty stringss with \N (to denote NULL) and move it into a directory that mysql has the privileges to open.

`tail -n +2 worldcities.csv >| worldcities_noheader.csv && \
sed -i -e 's/""/"\\N"/g' worldcities_noheader.csv   && \
sudo mv -f worldcities_noheader.csv /var/lib/mysql-files/worldcities.csv`
<br/>

Now, import the CSV: 

`mysqlimport --fields-optionally-enclosed-by='"' --fields-terminated-by=',' --lines-terminated-by='\r\n' --user=root -p mydb /var/lib/mysql-files/worldcities.csv`

Finally, ensure that the import worked. Access the database (`use mydb;`) and enter the following select statement: 

`SELECT * FROM worldcities WHERE country="Japan" LIMIT 10;`

<img width="1702" height="508" alt="select" src="https://github.com/user-attachments/assets/f424d798-cca8-4f4e-b592-b0d6cf789373" /><br/>

Success!

