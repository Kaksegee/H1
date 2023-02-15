
# x) Esimerkki Palvelusta

Esimerkkinä voisi toimia suoratoistopalvelu. Hyötyinä voisi olla palvelun nopeus ja laatu.



# H9
 Harjoituksen tarkoituksena on asentaa PostgreSQL ja harjoitella datan luomista, lukemista, päivittämistä ja poistoa.

 
 
### Laitteisto
 
* Käyttöjärjestelmä	Microsoft Windows 10 Enterprise LTSC 64 bit
* Prosessori i5-6600
* RAM 16 GB
* Virtuaaliohjelmisto : Oracle VM VirtualBox
* Virtuaalikoneen käyttöjärjestelmä: Debian-live-11.6.0-amd64-xfce+nonfree.iso
* Virtuaalipalvelin: Linode Nanode 1 GB





## PostgreSQL:n asentaminen ja testaaminen (0:00-0:55)

Alotin harjoituksen asentamalla PostgreSQL:n kommeoilla:

    $ sudo apt-get update
    $ sudo apt-get -y install postgresql
    
Tämän jälkeen käynnistin postgreSQL:n komennolla:

    $ sudo systemctl start postgresql
    
Seuraavaksi loin uuden tietokannan ja lisäsin käyttäjän kommenoilla:

    $ sudo -u postgres createdb r01p4r
    $ sudo -u postgres createuser r01p4r
  
![Add file: Upload](/ss/h91.PNG)

  Seuraavaksi testasin postgreSQL:n toimivuuden komennolla:
   
    $ psql
  
  ![Add file: Upload](/ss/h92.PNG)
  
  PostgreSQL toimii.
     
   

## CRUD (0:13)

Siirryin PostgreSQL:ään komenolla

    $ psql
    
 Ja loin uuden taulukon komennolla
  
    r01p4r=> CREATE TABLE students (id SERIAL PRIMARY KEY, name VARCHAR(200));
    
   ![Add file: Upload](/ss/h93.PNG)  
    
Avasin taulukon näkymiin komennolla

    r01p4r=> \d students
    
![Add file: Upload](/ss/h94.PNG)  

Seuraavaksi lisäsin taulukkoon nimiä käyttäen komentoja

    
    r01p4r=> INSERT INTO students(name) VALUES ('Sami');
    r01p4r=> INSERT INTO students(name) VALUES ('Lotta');
    r01p4r=> INSERT INTO students(name) VALUES ('Roi');
    
Tarkistin nimien lisäämisen komennolla

    r01p4r=> SELECT * FROM students;
    
 
![Add file: Upload](/ss/h95.PNG)  


Seuraavaksi päivitin yhtä taulukon nimeä komennolla

    r01p4r=> UPDATE students SET name='Roi Moi' WHERE name='Roi';
    
 Tarkistin nimen päivittämistä komennolla

    r01p4r=> select * from students;

![Add file: Upload](/ss/h96.PNG)  


   Seuraavaksi poistin nimen 'Sami' taulukosta students komennolla
   
      r01p4r=> DELETE FROM students WHERE name='Sami';
      
  Tarkistin nimen ppoistoa komennolla

    r01p4r=> select * from students;
    
   ![Add file: Upload](/ss/h97.PNG)  
    
    
    
    

      
   





 ## Lopuksi 
 
 Tässä harjoituksessa asensin PostgreSQL:n ja harjoittelin datan luomista, lukemista, päivittämistä ja poistoa.
 
 
## Lähteet

Linux Palvelimet 2023 alkukevät, Tero Karvinen (https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)

Install PostgreSQL on Ubuntu – New user and database in 3 commands, Tero Karvinen - 3.3.2016 (https://terokarvinen.com/2016/03/03/install-postgresql-on-ubuntu-new-user-and-database-in-3-commands/)

PostgreSQL Install and One Table Database – SQL CRUD tutorial for Ubuntu, Tero Karvinen - 5.3.2016 (https://terokarvinen.com/2016/03/05/postgresql-install-and-one-table-database-sql-crud-tutorial-for-ubuntu/)




#### Tehnyt Roi Partanen 16.2.2023
