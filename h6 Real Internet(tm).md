# x)

 
 
 
 
## 	 Apache Software Foundation 2023: Getting Started (https://httpd.apache.org/docs/2.4/getting-started.html)

Artikkelin tarkoituksena on toimia pohjustuksena Apachen HTTP-palvelimien ja nettisivujen toimintaan.

   * Osoitteet verkossa ilmoitetaan URL:n avulla
   * Asiakasohjelmaa (esim. nettiselain) käytetään yhdistämään palvelimeen
   * Yhdistääkseen palvelimelle asiakasohjelman täytyy ensin yhdistää palvelimen nimi ja IP-osoite
   * Virtual Hostien avulla pystyy ylläpitämään monia eri sivuja samalla palvelimella
   * Apachen palvelin konfiguroidaan tekstitiedostojen avulla
   * Lokit auttavat vianmäärityksessä ja korjauksessa

## Apache Software Foundation 2023: Name-based Virtual Host Support (https://httpd.apache.org/docs/current/vhosts/name-based.html)
   Artikkelin tarkoituksena on kertoa milloin ja miten käyttää nimipohjaisia virtual hosteja.
   
   * Virtual hostit voivat olla IP-osoitepohjaisia tai nimipohjaisia
   * IP-pohjaiset virtual hostit tarvitsevat jokaiselle hostille oman IP-osoitteen
   * Nimipohjaiset virtual hostit ovat yksinkertaisempia ja helpottavat vähäisten IP-osoitteiden kysyntää käyttämällä samaa IP-osoitetta eri hosteille.
   * Nimipohjainen virtual host ilmoitetaan muodossa  <VirtualHost *:80> ja sen alapuolelle määritetään ServerNamen avulla, mihin hostiin yhdistetään 
   * ServerAlias komennolla voi määrittää useampi osoite samalla palvelimelle
   * DocumentRoot-direktiivi kertoo missä hostin tiedostot sijaitsevat järjestelmässä
   
   
   
 # H6
 Harjoituksen tarkoituksena on vuokrata oma virtuaalipalvelin ja laittaa sen astukset kuntoon, asentaa weppipalvelin ja etsiä merkkejä murtautumisyrityksistä. Tein harjoituksen omalla pöytäkoneella 08.02.2023.
 

 
 
### Laitteisto
 
* Käyttöjärjestelmä	Microsoft Windows 10 Enterprise LTSC 64 bit
* Prosessori i5-6600
* RAM 16 GB
* Virtuaaliohjelmisto : Oracle VM VirtualBox
* Virtuaalikoneen käyttöjärjestelmä: Debian-live-11.6.0-amd64-xfce+nonfree.iso





## Virtuaali palvelimen vuokraus Linodesta (https://www.linode.com/)

Aluksi loin käyttäjätunnuksen Linoden palveluun ja lisäsin maksukortin. Tämän jälkeen loin uuden virtuaalipalvelimen 'create Linode' kohdasta.

![Add file: Upload](/ss/h61.PNG)
    
Valitsin käyttöjärjestelmäksi Debian 11:sta ja alueeksi Frankfurt, DE (eu-central). Virtuaalipalvelimeksi valitsin Nanode 1 GB:n.  
  
![Add file: Upload](/ss/h62.PNG)  


      

## Uuuden virtuaalipalvelimen käyttöönotto  (21:15

Aloitin harjoituksen yrittämällä yhdistää virtuaalipalvelimeen komennolla 

    $ ssh root@IP-osoite
    
Mutta sain viestin, että ssh-komentoa ei löydy. Yritin käynnisttää ssh:n uudestaan komennolla 

    $ sudo systemctl restart ssh
    
Mutta kyseistä palvelua ei ilmeisesti löydy. Kokeilin vielä tarkistaa ssh:n version komennolla

    $ ssh -v
    
Mutta sain viestin, että ssh-komentoa ei löydy.

![Add file: Upload](/ss/h63.PNG) 


Etsityä netitä löysin mahdollisen ratkaisun ja päätin kokeilla asentaa ssh:n tämän ohjeen mukaan (https://www.cyberciti.biz/faq/debian-linux-install-openssh-sshd-server/) Käyttämällä komentoja 

    $ apt-get update
    
   ja
   
    $ apt-get install openssh-server

Sain seuraavan error-viestin 

![Add file: Upload](/ss/h64.PNG) 

Löysin netistä mahdollisen tavan vapauttaa muistia (https://askubuntu.com/questions/178909/not-enough-space-in-var-cache-apt-archivesVapautin) poistamalla kaikki paketit jota ei ole asennettu komennolla

    $ sudo apt-get autoclean

Komento onnistui ja sain asennettua openssh-serverin.

Varmistin vielä, että ssh-palvelu on päällä komennoilla

    $ sudo systemctl restart ssh
    
    $ sudo systemctl status ssh
    
 ![Add file: Upload](/ss/h65.PNG)    
 
 Ssh näyttäisi olevan käynnissä. Seuraavaksi yritin yhdistää uudestaa virtuaalipalvelimeen komennolla
 
    $ ssh root@IP-osoite
    
   
 Pääsin sisään syötettyäni Linodeen luomani salasanan. Seuraavaksi päivin paketit ja asensin palomuurin komnennoilla
 
    
    $ sudo apt-get update
    
    $ sudo apt-get install ufw
  
  Seuraavaksi loin palomuuriin reiän ssh:lle ja laitoin palomuurin päälle komennoilla
  
    $ sudo ufw allow 22/tcp
    
    $ sudo ufw enable
    
  ![Add file: Upload](/ss/h66.PNG)    
    

Seuraavaksi loin uuden käyttäjän ja annoin sille oikeuksia kommennoilla 

    $ sudo adduser roi
    $ sudo adduser roi sudo
    $ sudo adduser roi adm
    
    
Kokeilin kirjautua uudella käyttäjällä eri terminaalissa komennolla

    $ ssh roi@IP-osoite
    
  Ja pääsin sisään. Seuraavaksi lukitsin root-käyttäjän komenolla
  
    $ sudo usermod --lock root
    
 Tämän jälkeen kävin muokkaamassa muokkaamassa ssh:n konfiguraatio tiedostoa ja poistin root kirjautumisin käytöstä komennolla
 
    $ sudoedit /etc/ssh/sshd_config
    
Ja muuttamalla kohtaa PermitRootLogin yes -> no
   
  ![Add file: Upload](/ss/h67.PNG) 
   

Tämän jälkeen käynnistin ssh:n uudestaan komennolla 

    $ sudo systemctl restart ssh
   
Seuraavaksi kirjauduin sisään uudella käyttäjällä komennolla

     $ ssh roi@IP-osoite
 
 Sitten päivitin ja asensin uusimmat paketit komennoilla 
 
     $ sudo apt-get update
     $ sudo apt-get upgrade
     
## Apache-palvelimen asentaminen virtuaalipalvelimelle (22:27)

  Asensin Apache-palvelimen kommenoilla 
  
      $ sudo apt-get update
      $ sudo apt-get install apache2
      
  Tein palomuuriin reiän Apachelle komennolla
  
       $ sudo ufw allow 80/tcp
       
  ja käynnistin Apache-palvelimen komennolla
  
       $ sudo systemctl start apache2
       
   Tarkistin, että Apache on käynnissä komennoilla 
    
       $ sudo systemctl status apache2 
       $ curl 'localhost'
       
   ![Add file: Upload](/ss/h68.PNG)  
   
   Apachen esimerkkisivu latautui.
   
   ![Add file: Upload](/ss/h69.PNG)  
   
   
   
  Kokeilin seuraavaksi käynnistää Apache-serverin uudestaan komennolla 
  
    $ sudo systemctl restart apache2
    
  Ja sain seuraavan viestin
   
   ![Add file: Upload](/ss/ss6.2.PNG)  
      
 
   
 Kävin vielä selaimessa osoitteessa 'localhost' ja sain seuraavan viestin
  
  
   ![Add file: Upload](/ss/ss6.3.PNG)  
   
   
   Seuraavaksi menin katsomaan Apachen konfiguraatio testiä komennolla
   
     $ cd /usr/sbin/
     
 ja
 
    $ sudo apache2ctl configtest
    
Sain seuraavanlaisen viestin

![Add file: Upload](/ss/ss6.4.PNG)
 
mikä viittaisi syntaksivirheeseen, 'frontpage.conf' sivulla, minkä johdosta konfiguraatio testi epäonnistui.

Kävin myös tutkimassa Apachen virhelokin viitä viimeisintä viestiä kommenolla 

    $ sudo tail -5 /var/log/apache2/error.log
    
 jaa sain seuraavat lokit
   
![Add file: Upload](/ss/ss6.6.PNG)

Viimeisimmässä lokissa näkyi ensin päivämäärä ja kellon aika oikeassa muodossa. Seuraavaksi lokissa oli listattu tapahtuman tyyppi (tässä tapauksessa ilmoitus). Seuraavaksi lokissa oli listattu thread- ja prosessi-id:t (TID ja PID). Seuraavaksi loki kertoo, että ohjelma on saanut pyynnön sulkeutua. 

Sitä ennen olevissa lokeissa näkyy ensin päivämäärä ja kellon aika oikeassa muodossa. Seuraavaksi lokissa oli listattu tapahtuman tyyppi (tässä tapauksessa error-viesti) Seuraavaksi lokeissa oli listattu thread- ja prosessi-id:t (TID ja PID). Näiden jälkeen oli listattu asiakasohjelma ja sen jälkeen  viesti 'client denied by server configuration', minkä jälkeen hakemistopolku.

Viestit 'client denied by configuration'  viittaisi ongelmaan Apachen konfiguraatiossa, joka estää pääsyä käsiksi hakemistoon. Mikä johtaa sitten ohjelman sulkeutumiseen.

Testasin vielä, että ongelma ratkaistiin ja lokit olivat oikeassa

Muokkasin frontpage.conf-tiedostoa komennolla

    $ sudoedit /etc/apache2/sites-available/frontpage.conf

ja poistin kirjoitusvirheen sanasta 'Directory'.

![Add file: Upload](/ss/ss6.7.PNG)

Käynnistin Apachen uudestaan kommennolla

    $ sudo systemctl restart apache2

Seuraavaksi tein Apachen konfiguraatio testin komennoilla

   
     $ cd /usr/sbin/
     
 ja
 
    $ sudo apache2ctl configtest
    
    
   ![Add file: Upload](/ss/ss6.8.PNG)   
   
  Syntaksi oli OK.
 
 Kävin myös katsomassa Apachen virhelokin viimeisintä viestiä kommennolla
 
    $ sudo tail -1 /var/log/apache2/error.log
    
  ![Add file: Upload](/ss/ss6.10.PNG)  
  
 Ensiksi lokissa näkyi päivämäärä ja kellon aika oikeassa muodossa. Seuraavaksi lokissa oli listattu tapahtuman tyyppi (tässä tapauksessa ilmoitus). Seuraavaksi lokissa oli listattu thread- ja prosessi-id:t (TID ja PID). Loki kertoo, että komentoa  
  
    $ /usr/sbin/apache2
    
  oli käytetty aloittamaan säiettä. Aikaisempi virhe ei ollut siis toistunut käynnistäessä Apachea uudestaan.
 

  
  Tein vielä testin kommennolla
  
      $ curl 'localhost'
      
 Ja sivusto toimi.
 
 ![Add file: Upload](/ss/ss6.9.PNG)  


 ## Lopuksi 
 
 Tässä harjoituksessa tutustuin syvemmin Apache-palvelimeen ja harjoittelin Apachen etusivun muuttamista. Harjoittelin myös Apachen vianmääritystä.
 
 
## Lähteet



New Default Website with Apache2, Tero Karvinen - 16.2.2016 (https://terokarvinen.com/2016/new-default-website-with-apache2-show-your-homepage-at-top-of-example-com-no-tilde/)

Linux Palvelimet 2023 alkukevät, Tero Karvinen (https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)

First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS, Tero Karvinen - 19.11.2017 (https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/)


#### Tehnyt Roi Partanen 08.02.2023
