# Import CSV into database 

Here, I will explain the steps of obtaining the CSV file, transferring it to the server, formatting the file, and importing into the database. 

## Obtain CSV

Download the CSV file from [Simple Maps](https://simplemaps.com/data/world-cities). The basic, free version will  be sufficient for this project. 

<img width="2344" height="1644" alt="simplemaps" src="https://github.com/user-attachments/assets/1a8ed9c7-27d1-4708-8a5c-07707c0bbe11" /></br>

This is what the CSV should look like: 

<img width="1562" height="694" alt="worldcitiescsv" src="https://github.com/user-attachments/assets/2a4a3cbe-5288-4354-8975-2bbe383322fc" /></br>

Install FileZilla and connect to the server with the same credentials as when using SSH.

<img width="3024" height="1572" alt="filezilla" src="https://github.com/user-attachments/assets/c6b24238-b813-4ebb-9841-75b62abe6b5a" />
As you can see by the status and the listing, the transfer was successful. 

Return to the server terminal and access MySQL with the previously created user. Create the database.  
