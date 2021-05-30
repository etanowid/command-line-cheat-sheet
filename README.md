# COMMAND LINE CHEAT SHEET

# local (mac)
### ssh into UCI openlab<br/>
`ssh <UCINetID>@openlab.ics.uci.edu`<br/>
<br/>

### ssh into AWS<br/>
`ssh -i "<pemFileName>" ubuntu@<blahblah>`<br/>
ex:<br/>
`ssh -i "cs122b.pem" ubuntu@blah.us-east-2.compute.amazonaws.com`<br/>
<br/>

### compile (gcc) and run C code  (in ics openlab) <br/>
cd to the project directory<br/>
`gcc file.c -o file` 	<br/>
`./file`<br/>
<br/>

### compile (clang) and run C++ code (in ics openlab)<br/>
cd to the project directory<br/>
`clang++ *.cpp -o obj` <br/>
`./obj`<br/>
<br/>

### transfer file local -> remote<br/>
1. using sftp <br/>
`sftp> <UCINetID>@openlab.ics.uci.edu`<br/>
`sftp> lcd <directoryName>` 	ex: `sftp> lcd Documents`<br/>
`sftp> put <fileName>`		ex: `sftp> put file.c`<br/>

2. using scp <br/>
`scp -i <pemFileName> <fileName> ubuntu@ec2BLAHBLAH:/home/ubuntu/<fileName>`<br/>
ex:<br/>
`scp -i cs122b.pem moviedb.sql ubuntu@ec2BLAHBLAH:/home/ubuntu/moviedb.sql`<br/>
<br/>

### make file executable<br/>
`chmod +x <fileName>`<br/>
ex: <br/>
`chmod +x apache-tomcat-9.0.44/bin/catalina.sh`<br/>
<br/>

### MySQL stuff<br/>
1. settings -> MySQL -> Start MySQL Server -> click path in gray above -> bin (copy this MySQL bin's path)
2. `cd <binpath>`
3. `./mysql -u root -p`<br/>
<br/>

### allow MySQL logging<br/>
1. By default, MySQL doesn't enable logging. To enable<br/>
`shell> mysql -u root -p`<br/>
`mysql> SET GLOBAL general_log = 'ON';`
2. find the MySQL file log file and its path:<br/>
`shell> mysql -u root -p -se "SHOW VARIABLES" | grep -e log_error -e general_log -e slow_query_log -e datadir`
3. copy the file for general_log_file line <br/>
ex: `general_log_file	/usr/local/mysql/data/dhcp-v044-069.log`
4. Monitor the ".log" files under this folder. Command using "tail":<br/>
`shell> sudo tail -f /usr/local/mysql/data/dhcp-v044-069.log`<br/>
<br/>
<br/>


# remote/linux (aws ubuntu ec2 instance)
### remove file<br/>
`rm <file>`<br/>
<br/>

### make a directory<br/>
`mkdir <directoryName>`<br/>
<br/>

### remove directory<br/>
`sudo rm -r <directoryName>`<br/>
<br/>

### copy file<br/>
creates a copy of the firstFile.txt file and renames the new file to secondFile.txt <br/>
`cp firstFile.txt secondFile.txt`<br/>
creates a copy of the firstFile.txt file and renames the new file to secondFile.txt and moves it to otherDirectory <br/>
`cp firstFile.txt /otherDirectory/secondFile.txt`<br/>
<br/>

### move file<br/>
move file: `mv <source> <destination>`<br/>
rename file: `mv originalName.txt newName.txt`<br/>
ex:<br/>
`mv file.txt /home/ubuntu`<br/>
<br/>

### open and edit a file<br/>
`vi file.txt`<br/>
to edit: type `i` 	<br/>
if done: press `esc`<br/>
save and quit: type `:wq` <br/>
<br/>

### download file using url<br/>
`wget <url>`<br/>
<br/>

### MySQL stuff<br/>
connect to mysql root <br/>
`mysql -u root -p` 	<br/>
<br/>
create new user called 'mytestuser' and grant privileges<br/>
`mysql> CREATE user mytestuser@localhost IDENTIFIED by ‘password’;`<br/>
`mysql> GRANT ALL PRIVILEGES ON * . * TO 'mytestuser'@'localhost'; `<br/>
<br/>
change password of 'mytestuser'<br/>
`mysql> ALTER user mytestuser@localhost IDENTIFIED by ‘newpassword’;`<br/>
<br/>
create table by running 'moviedb.sql' file<br/>
`shell> mysql -u mytestuser -p < moviedb.sql`<br/>
<br/>
populate the moviedb table by running 'movie-data.sql' file<br/>
`shell> mysql -u mytestuser -p --database=moviedb < /home/ubuntu/movie-data.sql`<br/>
<br/>
make copy/backup of a table<br/>
`insert into employees_backup select * from employees;`<br/>
<br/>
<br/>
### maven <br/>
(cd to project directory)<br/>
to compile and build war file<br/>
`mvn compile`<br/>
`mvn package`<br/>
or to remove war file <br/>
`mvn clean package`<br/>
<br/>
to run a stand-alone file in the project (ex. class name = VerifyPassword)v]<br/>
`mvn compile`<br/>
`mvn exec:java -Dexec.cleanupDaemonThreads=false -Dexec.mainClass="VerifyPassword"`<br/>
