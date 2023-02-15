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

Luotuani käyttäjätilin ja vuokrattuani domainnimen siirryin käyttäjän dashboardiin ja sieltä domain listin kautta muokkaamaan vuokraamaani domainia.
  
![Add file: Upload](/ss/h82.PNG)  

Kohdassa 'advanced DNS' lisäsin 'Add new record' kohdasta kaksi uutta A-record tyyppistä hostia ja yhdistin ne luomani virtuaalipalvelimen IP-osoitteeseen.

![Add file: Upload](/ss/h83.PNG)  

Hostien '@' ja 'www' pitäisi taata, että molemmat osoitemuodot roipartanen.com ja www.roipartanen.com toimivat. Luotuani hostit tarkistin selaimesta molempien toimivuuden.

![Add file: Upload](/ss/h84.PNG)  

 ![Add file: Upload](/ss/h85.PNG)       
 
 Molemmat hostit toimivat.

## Domainnimen tutkiminen käyttäen dig- ja host-komentoa (23:33-0:44)


Aloitin harjoituksen käyttämällä komentoa 

        $ dig roipartanen.com
        
Mutta sain viestin, että kyseistä komentoa ei löydy.

![Add file: Upload](/ss/h86.PNG)  

Kokeilin vielä komentoa
    
        $ man dig
        
ja sain viestin, että kyseistä komennosta ei ollut manuaalia. Googlettamalla löysin komennon, millä asentaa dig-työkalu (https://linuxhint.com/install-dig-debian-11/). 

Asensin digin käyttäen komentoja

         $ sudo apt-get update

         $ sudo apt-get install -y dnsutils
 
Seuraavaksi siirryin tarkastelemaan luomaani sivustoa komennolla 
 
         $ dig roipartanen.com

![Add file: Upload](/ss/h87.PNG)  

Ensimmäinen kappale kertoo Dig-työkalun version ja mihin osoitteeseen sitä on käytetty. Kappaleessa myös kerrotaan, mikä operaatio on tehty, tässä tapauksessa kysely (QUERY), onnistuiko kyseinen operaatio (onnistui=NOERROR) ja operaation id. Tämän jälkeen on määritelty vastausmuoto erillaisten binäärimuuttujien (flags) avulla.

OPT PSEUDOSECTION kertoo mikä EDNS versio on käytössä (EDNS0), siihen liittyvät binäärimuuttujat (flags) ja pyyntöä kantavan UDP paketin koko.

Kysymys kohdassa (Question section) Kerrotaan mihin osoitteeseen kysely on suoritettu.

Vastaus kohdassa (Answer section) kerrotaan ensin haettu sivu ja sen jälkeen 'TTL', eli kuinka pitkään kestää ennen kuin data päivittyy. 'IN' kertoo, että tein internet kyselyn ja 'A' kertoo minkälaisesta recordista oli kyse (tässä tapauksessa A-record). Rivin lopussa näkyy vielä haetun sivun IP-osoite.
Query time kertoo, kuinka kauan vastauksen saamisessa kesti (tässä tapauksessa 20 millisekunttia). 'When' kertoo milloin kysely on tehty ja 'MSG size' kertoo kuinka suuri kyselyn vastaus oli (60 tavua).



Tämän jälkeen tarkastelin vielä sivustoa host komennolla

      $ host roipartanen.com
      
Ja sain seuraavan tuloksen

![Add file: Upload](/ss/h88.PNG)  

Ensiksi työkalu kertoo sivuston ja siihen liitetyn IP-osoitteen (194.233.167.186).
Seuraavaksi työkalu ilmeisesti kertoo minkä palvelimien kautta sähköpostien uudelleenohjaus tapahtuu jos se on otettu käyttöön. 








 ## Lopuksi 
 
 Tässä harjoituksessa vuokrasin oman domainnimen ja yhdistin sen aikaisemmin luomaani virtuaalipalvelimeen. Harjoittelin myös dig- ja host-työkalun käyttöä.
 
 
## Lähteet

Linux Palvelimet 2023 alkukevät, Tero Karvinen (https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)

Install DIG on Debian 11, David Adams (https://linuxhint.com/install-dig-debian-11/)

What does OPT PSEUDOSECTION mean in `dig` response? (https://serverfault.com/questions/1018425/what-does-opt-pseudosection-mean-in-dig-response)




#### Tehnyt Roi Partanen 12.02.2023-13.02.2023
