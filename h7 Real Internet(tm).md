# x)

 
 
 
 
## 	 First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS (https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/)

Tero Karvisen (19.9.2017) kirjoittamasa artikkelissa ohjeistetaan miten konfiguroidaan uusi yksityinen virtuaali- ja nimipalvelin.

   * Salasanojen pitää olla aina vahvoja, vaikka niitä käyttäisikin vain lyhyen aikaa
   * Ensimmäistä kertaa kirjautuessa virtuaalipalvelimelle kirjaudutaan sisään juurikäyttäjänä
   * Ennen kuin palomuurin laittaa päälle, on siihen tehtävä aukko ssh:lle
   * On tärkeää luoda itselleen uusi käyttäjä ja antaa sille sudo-oikeudet
   * Uuden käyttäjän luonnin jälkeen voi estää juurikäyttäjänä kirjautumisen
   * Pakettien ja käyttöjärjestelmän pitäminen ajantasalla on tärkeää tietoturvan kannalta
   * Uusille julkisille palvelimille on tehtävä aukko palomuuriin
   * Eri nimipalvelimien tarjoajilta voi vuokrata nimiä esitettäväksi IP-osoitteen sijasta

  
   
 # H7
 Harjoituksen tarkoituksena on vuokrata oma virtuaalipalvelin ja sen konfiguroiminen manuaalisti, asentaa weppipalvelin ja etsiä merkkejä murtautumisyrityksistä. Tein harjoituksen omalla pöytäkoneella 08.02.2023-09.02.2023.
 

 
 
### Laitteisto
 
* Käyttöjärjestelmä	Microsoft Windows 10 Enterprise LTSC 64 bit
* Prosessori i5-6600
* RAM 16 GB
* Virtuaaliohjelmisto : Oracle VM VirtualBox
* Virtuaalikoneen käyttöjärjestelmä: Debian-live-11.6.0-amd64-xfce+nonfree.iso
* Virtuaalipalvelin: Linode Nanode 1 GB





## Virtuaali palvelimen vuokraus Linodesta (https://www.linode.com/)

Aluksi loin käyttäjätunnuksen Linoden palveluun ja lisäsin maksukortin. Tämän jälkeen loin uuden virtuaalipalvelimen 'create Linode' kohdasta.

![Add file: Upload](/ss/h61.PNG)
    
Valitsin käyttöjärjestelmäksi Debian 11:sta ja alueeksi Frankfurt, DE (eu-central). Virtuaalipalvelimeksi valitsin Nanode 1 GB:n.  
  
![Add file: Upload](/ss/h62.PNG)  


      

## Uuuden virtuaalipalvelimen käyttöönotto  (21:15)

Aloitin harjoituksen yrittämällä yhdistää virtuaalipalvelimeen komennolla 

    $ ssh root@194.233.167.186
    
Mutta sain viestin, että ssh-komentoa ei löydy. Yritin käynnisttää ssh:n uudestaan komennolla 

    $ sudo systemctl restart ssh
    
Mutta kyseistä palvelua ei ilmeisesti löydy. Kokeilin vielä tarkistaa ssh:n version komennolla

    $ ssh -v
    
Mutta sain viestin, että ssh-komentoa ei löydy.

![Add file: Upload](/ss/h63.PNG) 


Etsittyä netistä löysin mahdollisen ratkaisun ja päätin kokeilla asentaa ssh:n tämän ohjeen mukaan (https://www.cyberciti.biz/faq/debian-linux-install-openssh-sshd-server/) Käyttämällä komentoja 

    $ apt-get update
    
   ja
   
    $ apt-get install openssh-server

Sain seuraavan error-viestin 

![Add file: Upload](/ss/h64.PNG) 

Löysin netistä mahdollisen tavan vapauttaa muistia (https://askubuntu.com/questions/178909/not-enough-space-in-var-cache-apt-archivesVapautin) poistamalla kaikki paketit jota ei ole asennettu. Käyttäen komentoa

    $ sudo apt-get autoclean

Sain vapautettua muistia ja asennettua openssh-serverin.

Varmistin vielä, että ssh-palvelu on päällä komennoilla

    $ sudo systemctl restart ssh
    
    
    $ sudo systemctl status ssh
    
 ![Add file: Upload](/ss/h65.PNG)    
 
 Ssh näyttäisi olevan käynnissä. Seuraavaksi yritin yhdistää uudestaa virtuaalipalvelimeen komennolla
 
    $ ssh root@194.233.167.186
    
   
 Pääsin sisään syötettyäni Linodeen luomani salasanan. Seuraavaksi päivitin paketit ja asensin palomuurin komnennoilla
 
    
    $ sudo apt-get update
    
    $ sudo apt-get install ufw
  
  Seuraavaksi loin palomuuriin reiän ssh:lle ja sen jälkeen laitoin palomuurin päälle komennoilla
  
    $ sudo ufw allow 22/tcp
    
    $ sudo ufw enable
    
  ![Add file: Upload](/ss/h66.PNG)    
    

Seuraavaksi loin uuden käyttäjän ja annoin sille oikeuksia kommennoilla 

    $ sudo adduser roi
    $ sudo adduser roi sudo
    $ sudo adduser roi adm
    
    
Kokeilin kirjautua uudella käyttäjällä eri terminaalissa komennolla

    $ ssh roi@IP-osoite
    
  Ja pääsin sisään. Seuraavaksi lukitsin juurikäyttäjän salasanan komenolla
  
    $ sudo usermod --lock root
    
 Tämän jälkeen kävin muokkaamassa muokkaamassa ssh:n konfiguraatio tiedostoa ja poistin juurikäyttäjänä kirjautumisen käytöstä komennolla
 
    $ sudoedit /etc/ssh/sshd_config
    
Ja muuttamalla kohtaa PermitRootLogin yes -> no
   
  ![Add file: Upload](/ss/h67.PNG) 
   

Tämän jälkeen käynnistin ssh:n uudestaan komennolla 

    $ sudo systemctl restart ssh
   
Seuraavaksi kirjauduin sisään uudella käyttäjällä komennolla

     $ ssh roi@IP-osoite
 
 Sitten vielä päivitin ja asensin uusimmat paketit komennoilla 
 
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
   
   
 Seuraavaksi vaihdoin Apachen esimerkkisivun komennolla
 
    $ echo Hello | sudo tee /var/www/html/index.html
    
    
   ![Add file: Upload](/ss/h670.PNG)  
    
   
 Tämän jälkeen tein palomuuriin uudestaan reiän komennolla 
 
      $ sudo ufw allow 80/tcp
      
Kävin selaimessa tosiella laitteella tarkistamassa muutokset ja testisivu latautui


   ![Add file: Upload](/ss/h671.PNG)  
   
## Murtautumisyritykset (0:08)

Kävin tutkimassa /var/log/auth.log:sta merkkejä murtautumisyrityksistä komennolla

    $ sudo less /var/log/auth.log
   
 ![Add file: Upload](/ss/h673.PNG)  
 
Näyttäisi siltä että monta eri käyttäjää on yrittänyt sisään virtuaalipalvelimeen, mutta todennus on epäonnistunut. Kävin myös katsomassa /var/log/apache2/access.log:ia komennolla
 
    $ sudo less /var/log/apache2/access.log
    
Mutta en löytänyt sieltä mitään omaan silmään hälyyttävää.

 ## Lopuksi 
 
 Tässä harjoituksessa vuokrasin virtuaalipalvelimen ja konfiguroin sen manuaalisesti. Asensin myös webbipalvelimen ja tutkin murtautumisyrityksiä. Ongelmia tuotti ssh:n puuttuminen ja muistin loppuminen. 
 
 
## Lähteet

Linux Palvelimet 2023 alkukevät, Tero Karvinen (https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)

First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS, Tero Karvinen - 19.9.2017 (https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/)

How to install OpenSSH server on Debian Linux 9/10/11, Vivek Gite - 29.3.2022 (https://www.cyberciti.biz/faq/debian-linux-install-openssh-sshd-server/)

Not enough space in /var/cache/apt/archives/ (https://askubuntu.com/questions/178909/not-enough-space-in-var-cache-apt-archives)



#### Tehnyt Roi Partanen 08.02.2023-09.02.2023
