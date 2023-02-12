
   
 # H8
 Harjoituksen tarkoituksena on vuokrata oma domainnimi NameCheapista ja asettaa se osoittamaan tehtävässä h7 luotuun virtuaalipalvelimeen. Tutkin myös domainnimeä host- ja dig-komennoilla. Tein harjoituksen omalla pöytäkoneella 12.02.2023-13.02.2023.
 

 
 
### Laitteisto
 
* Käyttöjärjestelmä	Microsoft Windows 10 Enterprise LTSC 64 bit
* Prosessori i5-6600
* RAM 16 GB
* Virtuaaliohjelmisto : Oracle VM VirtualBox
* Virtuaalikoneen käyttöjärjestelmä: Debian-live-11.6.0-amd64-xfce+nonfree.iso
* Virtuaalipalvelin: Linode Nanode 1 GB





## Domainnimen vuokraaminen NameCheapista (https://www.namecheap.com/) (23:07)

Aluksi tarkastin haluamani domainnimen "www.roipartanen.com" saatavuuden. 

![Add file: Upload](/ss/h81.PNG)
    
Nimi oli saatavilla. Seuraavaksi siirryin luomaan käyttäjätilin.

Luotuani käyttäjätilin ja vuokrtattuani domainnimen siirryin käyttäjän dashboardiin ja sieltä domain listin kautta muokkaamaan vuokraamaani domainia.
  
![Add file: Upload](/ss/h82.PNG)  

Kohdassa 'advanced DNS' lisäsin 'Add new record' kohdasta kaksi uutta A-record tyyppistä hostia ja yhdistin ne luomani virtuaalipalvelimen IP-osoitteeseen.

![Add file: Upload](/ss/h83.PNG)  

Hostien '@' ja 'www' pitäisi taata, että roipartanen.com ja www.roipartanen.com toimivat. Luotuani hostit tarkistin selaimesta molempien toimivuuden.

![Add file: Upload](/ss/h84.PNG)  

 ![Add file: Upload](/ss/h85.PNG)       
 
 Molemmat hostit toimivat.

## Domainnimen tutkiminen käyttäen dig- ja host-komentoa (23:33)


Aloitin harjoituksen käyttämällä komentoa 

        $ dig roipartanen.com
        
Mutta sain viestin, että kyseistä komentoa ei löydy.

![Add file: Upload](/ss/h86.PNG)  

Kokeilin vielä komentoa
    
        $ man dig
        
ja sain viestin, että kyseistä komennosta ei ollut manuaalia. Googlettamalla löysin komennon, millä asentaa dig-työkalu (https://linuxhint.com/install-dig-debian-11/). 

Asensin digin käyttäen komentoa

         $ sudo apt-get install -y dnsutils
 
Seuraavaksi siirryin tarkastelemaan luomaani sivustoa komennolla 
 
         $ dig roipartanen.com

![Add file: Upload](/ss/h87.PNG)  



    


 ## Lopuksi 
 
 Tässä harjoituksessa vuokrasin virtuaalipalvelimen ja konfiguroin sen manuaalisesti. Asensin myös webbipalvelimen ja tutkin murtautumisyrityksiä. Ongelmia tuotti ssh:n puuttuminen ja muistin loppuminen. 
 
 
## Lähteet

Linux Palvelimet 2023 alkukevät, Tero Karvinen (https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)

Install DIG on Debian 11, David Adams (https://linuxhint.com/install-dig-debian-11/)





#### Tehnyt Roi Partanen 12.02.2023-13.02.2023
