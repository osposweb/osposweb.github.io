1) Downlaod and Install Wamp or Xampp
2) Download and Install **composer, node.js, grunt-cli**
3) Downlaod the "opensourcepos-master.zip" (~3mb) and extract it to www or htdocs directory
4) Open command prompt in "opensourcepos-master" directory and run the following commands.
   - composer install
   - npm install
   - grunt --force
5) Create/locate a new mysql database to install open source point of sale into
6) Execute the file database/database.sql to create the tables needed
7) Modify application/config/database.php and modify credentials if needed to connect to your database
8) Go to your point of sale install public dir via the browser
LOGIN using
username: admin
password: pointofsale