
 
 ### x)
 Tero Karvisen sivuilla https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited löytyy katsaus Linuxin käyttöjärjestelmän eri komentoihin ja ominaisuuksiin.
 
 Huomioita:
 * Linuxissa ollaan aina hakemiston sisällä
* Pico ja Nano ovat hyviä tekstieditoreita
* Linuxiin asennetaan ohjelmistoa pakettien avulla
 
 # Komentaja Pingviini
 Harjoituksen tarkoituksena on tutustua Linuxin eri komentoihin ja hakemistoihin ja harjoitella niiden käyttöä. Tein harjoituksen omalla pöytäkoneella 22.01.2023
 

 
 
### Laitteisto
 
* Käyttöjärjestelmä	Microsoft Windows 10 Enterprise LTSC 64 bit
* Prosessori i5-6600
* RAM 16 GB
* Virtuaaliohjelmisto : Oracle VM VirtualBox
* Virtuaalikoneen käyttöjärjestelmä: Debian-live-11.6.0-amd64-xfce+nonfree.iso





## Aloitin harjoituksen kello 11:08 asentamalla micro editorin


       $ sudo apt-get update
       
  Komennolla ja salasanan syöttämällä sain haettua saatavilla olevat päivitykset

      $ apt-cache show micro
      
   Komennolla sain löydettyä micro editorin

     $ sudo apt-get -y install micro
     
  Komennolla sain asennettua micro tekstieditorin
     

 ## Seuraavaksi tutkin virtuaalikoneen ominaisuuksia (11:27)
 
  Hyödyntämällä viime tehtävän komentoja asensin LSHW ohjelman, jonka avulla pystyy tutkimaan käyttöjärjestelmän ominaisuuksia
  
     $ sudo lshw -short -sanitize
     
  Komennolla käynnistin lshw ohjelman ja listasin virtuaalikoneen ominaisuudet
  
  
![Add file: Upload](/ss/LSHW.PNG)
  
  
  Listauksessa näkyy, kuinka olin antanut virtuaalikoneelle 5 GB RAMia ja että virtuaalikone pyörii samalla prosessorilla, kuin pöytäkoneeni.
  
  ## Seuraavaksi asensin itselleni kolme mieluisaa komentorivi ohjelmaa (11:49)
  
  Valitisin ohjelmiksi cmatrix, cowsay ja sl
  
    $ sudo apt-get install cmatrix cowsay sl
    
  Komennolla asensin kaikki kolme ohjelmaa yhtäaikaa
  
     cmatrix
     cowsay "hello"
     sl
     
Komennoilla pääsin testaamaan eri ohjelmia

![Add file: Upload](/ss/cmatrix.PNG)

![Add file: Upload](/ss/cowsay.PNG)

![Add file: Upload](/ss/sl.PNG)



## Seuraavaksi tutustuin tärkeimpiin kansioihin ja tiedostoihin Linux-käyttöjärjestelmässä (12:08)
    cd /
   
   
   Komennolla sain esiin juurihakemiston, jonka sisältä töytyy kaikki tiedostot
   
    ls 
    
   Komento listaa tiedostot ja hakemistot valitussa hakemistossa
   
   ![Add file: Upload](/ss/root.PNG)
   
    cd /home/
  
   Komennolla pääsin kotihakemistoon, josta löytyy kaikki käyttäjät. Minun tapauksessa vain oma käyttäjäni.
   
   ![Add file: Upload](/ss/home.PNG)
   
   
    cd /home/r01
  
    
   Komennoilla pääsin oman käyttäjän hakemistoon
   
   ![Add file: Upload](/ss/r01.PNG)
   
    cd /etc/
    
   Komenolla pääsin järjestelmän asetuksiin
   
   ![Add file: Upload](/ss/etc.PNG)
   
    cd /media/
   
  Komennolla pääsin siirrettävien tallenusvälineiden hakemistoon
  
  ![Add file: Upload](/ss/media.PNG)
  
    cd /var/log/
    
   Komenolla pääsin tarkastelemaan koko järjestelmän lokeja
   
  
 ![Add file: Upload](/ss/log.PNG)
  
  
 ## Grepin testaus 13:01
 
 Aloitin tarkistamalla, että minulla on grep käytössä ja sen jälkeen luomalla uuden kansion ja sinne tekstiä nano-editorilla käyttäen komentoja
 
    grep
    $ mkdir testigrep
    nano hello
   
 ![Add file: Upload](/ss/onkogrep.PNG)    

    



 
    grep -c "Hello" hello
    
   Komenolla hain lainaismerkkien sisällä olevan sanan lukumäärää kansiossa "hello"
   
   
![Add file: Upload](/ss/montagrep.PNG)

    grep -v "Hello" hello
    
   Komennolla sain haettua kaikki sanat jotka eivät vastanneet lainausmerkkien sisällä olevaa sanaa
   
  
 ![Add file: Upload](/ss/greptasma.PNG)
 
 
    grep --color "Hello" hello
    
 Värjäsin kaikki Hello sanat kyseisessä tiedostossa
 
 ![Add file: Upload](/ss/grepvari.PNG)
 
 
 ## Lopuksi (13:43)
 
 Tässä harjoituksessa opettelin Debian-käyttöjärjestelmän ohjelmistojen ja hakemistojen käyttöä. Vastaan ei tullut ongelmatapauksia.
 
## Lähteet

Linux Palvelimet 2023 alkukevät, Tero Karvinen (https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)

Command Line Basics Revisited, Tero Karvinen - 2020-02-03 (https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited)

How To Use grep Command In Linux / UNIX With Practical Examples,  Vivek Gite - 20.1.2023 (https://www.cyberciti.biz/faq/howto-use-grep-command-in-linux-unix/)

11 Fun Linux Command-Line Programs You Should Try When Bored, Deepesh Sharma - 1.11.2022 (https://www.makeuseof.com/fun-linux-command-line-programs/)

UNIX Basic commands: grep (https://www.techonthenet.com/unix/basic/grep.php)



#### Tehnyt Roi Partanen 23.1.2023
 
 
 
   
  
  
    
  
  
   
   
   
   
   
   
   



