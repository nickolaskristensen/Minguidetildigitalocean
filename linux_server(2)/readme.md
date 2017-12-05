# Guide til oprettelsen af en webserver

## Opret droplet
1) www.digitalocean.com/login - (RTS mail + kode).

2) Opret(Create) Droplet.

3) Under distributions vælges: CentOS version: 6.9 x32.

<img src="img/distribution.png">

4) Vælg størrelse: $5/mo (512mb/1 CPU, 20GB/SSD disk, 1000GB/transfer).

<img src="img/Size.png">

5) Vælg Datacenter region: Eksempelvis: Amsterdam(2, 3).

<img src="img/datacenter.png">

6) Vælg et Host navn: Eksempelvis: 'Test'.

7) Efter udførelsen af disse kriterier trykkes på 'create'-knappen og en mail vil blive sendt med oplysninger til at oprette en webserver med PuTTy værktøjet. (Droplet Navn, IP-adresse, Username & kodeord).

<img src="img/mail.png">

----

## PuTTy

Oprettelsen af en webserver foregår med puTTy-værktøjet.

## 1) Åben PuTTy og indtast IP-adressen, som blev tilsendt fra digital ocean ved oprettelsen af 'dropletten'.

<img src="img/putty_start.png">

Tryk på 'Open'-knappen.

## 2) Login

- Indtast brugernavn (root)
- Indtast kode (link fra digitalocean)

Kopier koden, højreklik og tryk enter. Herefter vil den spørge om UNIX password, hvor der skal højreklikkes igen og trykkes enter. Derefter anmoder den om at ændre passwordet.

## 3) Installer Nano

Installer Nano ved at indtaste følgene sætning:
- yum install nano

Efter installationen vil den spørge om dette er ok, hvor der tastes 'y'(yes).

## 4) Installer MySQL

Installer Nano ved at indtaste følgene sætning:
- yum install mysql-server

Efter installationen vil den spørge om dette er ok, hvor der tastes 'y'(yes).

(Der kan indtastes: nano test, for at lave en kommentar)

Start og stop:

Der kan også indtastes: service mysqld start/stop/restart - for at starte, stoppe eller genstarte serveren.

Konfigurer MySQL:

Indtast: sudo /usr/bin/mysql_secure_installation

Enter current password for root (enter for none): indtast kode + enter

## 5) Installer Node.js

- yum install epel-release + y(yes)
- yum install nodejs + y(yes)
- yum install npm + y(yes)
- npm install -g n

Tjek version af node ved at indtaste: node -v

Installer ny version (opdater), ved at indtaste:
- n lts
- n

## 6) Genstart server/droplet(digital ocean.com)
- Tryk på 'ON'-knappen, så den står på 'OFF'
- Tryk på den igen, så den står på 'ON' igen.
- Luk putty ned og åben en ny putty terminal.

Indtast root + det nye kodeord.
Tjek om den har opdateret den nye version (node -v) skal være: v8.9.1

## 7) Installer PM2
(PM2 er en process manager til Node.js applikationer.)

Indtast: npm install -g pm2

Indtast kode (Kør pm2 ved startup): pm2 startup
Remove init script via: pm2 unstartup systemv

## 8) Installer Git

Installation: 
- yum install git

Konfiguration:
- git config --global user.name "Nickolas Kristensen"
- git config --global user.email "53708@RTS-365.dk"

Tjek Konfiguration:
- nano ~/.gitconfig

## 9) Opret et nøglesæt til at logge ind på GitHub

Opret nøglesæt:

- ssh-keygen -t rsa (tryk herefter enter 3 gange ved dette):

- a) Enter file in which to save the key (/root/.ssh/id_rsa): - enter
- b) Enter passphrase (empty for no passphrase): - enter
- c) Enter same passphrase again: - enter

Åbn den offentlige nøgle:

- nano ~/.ssh/id_rsa.pub
- cat ~/.ssh/id_rsa.pub

så kommer dette ud:
ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAu3kZ2lp/Fvw49If7GPGMGFRVrtAL+97vDn3QKpcaXn15MD9gq5PNgYUKddRX0FBdX78SGDVzQcOL9Krot1Pv8IqP1nzohSrRev2Tfg49v5k73XU39RGFXEt7n6+TJxzMbnQqyU6RWVqnd1fduGGWVwRd+gLbsOmsATdcLD7UtcKhIaE0F88HhwpSE14vKS6FzlMbGCQuHcBqxGNetZy05PTv+Oy5s88B8MMO7MJSXmVMvTMOXhfGnqBkCRfJuaC3e2/R7J1XCcIdNdMBUDat38UUuvre6EjxLAouIngz5glfkt2nvZD+SbhTKDYSs91eGIkGIBatBvwiEPyICISdLQ== root@TEST

Kopier dette output (af den offentlige nøgle) til: 
GitHub -> Settings -> SSH and GPG keys -> New SSH key -> Indsæt.
(Nu kender min webserver og min github hinanden)

Indtast: clear (så der bliver ryddet op)

## 10) Opret en mappe til din applikation

opret bibliotek/ direktory: indtast: 
- mkdir www

Indtast: 
- ls -l (for at se om der ligger noget)

Naviger ind i mappen: Indtast:
- cd ~/www

## 11) Klon dit repository fra GitHub

git clone git@github.com:brugernavn/repository ---
TAG FRANKS - github.com/frankgoldmann
vælg: webserver73
fork den til min egen profil (Nu har du den)
Gå ind i den og videre ind i package.json filen og tryk på blyanten i højre hjørne for at redigere:
ændre franks navne til dit eget: nickolaskristensen

- git clone git@github.com:nickolaskristensen/webserver73
- cd webserver73 (tilgå repository)
- ls -l (Se hvad der ligger i repository)
- npm install

node app.js

(og når du har en opdatering, skal du lave et pull)

Skal man pull (hvis man har lavet ændringer på github):

git pull git@github.com:nickolaskristensen/webserver73

------------

# Opsætning af mysql på linux-box

1) Indtast: mysql -p + kode

2) Giv root brugeren lov til at logge ind fra andre adresser end localhost, dette gøre ved at indtaste:

GRANT ALL ON *.* TO 'root'@'%' (GRANT ALL ON stjerne punktum stjerne TO)
(Betyder: alle databaser og alle tabeller)

3) Angiv kodeord til rootbrugeren: 

SET PASSWORD FOR 'root'@'%' = PASSWORD('1234');

4) For at komme ud i hjemmemappen skriv: quit;

5) Start MySQL Workbench - Tryk på MySQL Localhost connection, findes den ikke så opret den ved at trykke på (+). Kald den localhost og gem.

6) Vælg den ønskede database som ønskes eksporteret.

7) Tryk ”Server” og tryk ”Data Export” Vælg databasen.
Herefter trykkes der på 'Start Export'.

8) Gå til den mappe hvor du eksportede databasen til, her kan du nu se dine dumps. Alle dine tabeller ligger her som SQL filer.

9) Nu vil vi importere filerne over på vores linux maskine. (Workbench)

10) Opret en ny forbindelse ved trykke på '+' ikonet.

11) Indsæt den IP-adresse, som blev sendt via mail, fra digitalocean. Tryk herefter på OK-knappen.

12) Dobbeltklik på den nye forbindelse og indtast kodeordet (1234).
 
13) Klik på ”Create new schema” øverst.

14) Angiv navn til databasen og herefter på 'Apply'-knappen.

15) Tryk derefter på 'Server' og herefter på 'Data import'.

16) Tryk på knappen for at finde mappen, som hedder 'Dumps/...' og begynd herefter import.













