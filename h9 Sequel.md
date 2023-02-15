
x) Esimerkki Palvelusta

Esimerkkinä voisi toimia 



# H9
 Harjoituksen tarkoituksena on vuokrata oma domainnimi NameCheapista ja asettaa se osoittamaan tehtävässä h7 luotuun virtuaalipalvelimeen. Tutkin myös domainnimeä host- ja dig-komennoilla. Tein harjoituksen omalla pöytäkoneella 12.02.2023-13.02.2023.
 

 
 
### Laitteisto
 
* Käyttöjärjestelmä	Microsoft Windows 10 Enterprise LTSC 64 bit
* Prosessori i5-6600
* RAM 16 GB
* Virtuaaliohjelmisto : Oracle VM VirtualBox
* Virtuaalikoneen käyttöjärjestelmä: Debian-live-11.6.0-amd64-xfce+nonfree.iso
* Virtuaalipalvelin: Linode Nanode 1 GB





## PostgreSQL:n asentaminen ja testaaminen (0:00)

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

    r01p4r> \d students
    
![Add file: Upload](/ss/h94.PNG)  
     








 ## Lopuksi 
 
 Tässä harjoituksessa vuokrasin oman domainnimen ja yhdistin sen aikaisemmin luomaani virtuaalipalvelimeen. Harjoittelin myös dig- ja host-työkalun käyttöä.
 
 
## Lähteet

Linux Palvelimet 2023 alkukevät, Tero Karvinen (https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)

Install PostgreSQL on Ubuntu – New user and database in 3 commands, Tero Karvinen - 3.3.2016 (https://terokarvinen.com/2016/03/03/install-postgresql-on-ubuntu-new-user-and-database-in-3-commands/)

PostgreSQL Install and One Table Database – SQL CRUD tutorial for Ubuntu, Tero Karvinen - 5.3.2016 (PostgreSQL Install and One Table Database – SQL CRUD tutorial for Ubuntu)




#### Tehnyt Roi Partanen 16.2.2023
