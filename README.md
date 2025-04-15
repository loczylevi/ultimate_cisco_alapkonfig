# ultimate_cisco_alapkonfig

```bash


en
conf t 

! Hosztnév és domain
hostname R1
ip domain-name wmszki.hu

! Felhasználó és jelszó
username admin privilege 15 secret class    ! privilege 15: Ez határozza meg a felhasználó jogosultsági szintjét. privilege 15: A legmagasabb jogosultsági szint
username admin password 1234
username admin secret 1234                  ! titkositott jelszó (running configban nem látod)

! Enable secret
enable secret Exam2025                     ! Az enable secret Exam2025 parancs egy titkosított jelszót állít be magyarul jelszot kérsz ha beirod hogy "en" [privilegizált mód]
enable password 1234

! Console port védelem
line con 0
login local                          ! login local azt mondja a routernek vagy switch-nek, hogy: ”Felhasználónevet és jelszót is fog kérni.
exec-timeout 5 0                    ! Ez a parancs azt szabályozza, mennyi ideig marad aktív egy inaktív konzolkapcsolat, mielőtt automatikusan kijelentkeztet.[percek][másodpercek]
logging synchronous                 ! Ez a parancs azt szabályozza, hogy hogyan viselkedjen a rendszer, amikor közben üzenetet ír ki (pl. hiba, link változás), miközben te épp gépelsz.
exit


! VTY vonalak SSH-val, Telnet tiltása
line vty 0 15
transport input ssh
login local
exit


! SSH beállítás
crypto key generate rsa
1024
crypto key generate rsa modulus 1024   ??? ez müködik?
ip ssh version 2

! titkositás
service password-encryption

! bannerek
banner motd #sigma boy#
banner login #mind megbukunk let's gooo#
banner exec #skibidi#

! túl cicomázott, barokkos bannerek

banner motd #
+---------------------------------------+
|  ILLETÉKTELEN HOZZÁFÉRÉS TILOS!       |
|  Minden tevékenység naplózásra kerül. |
+---------------------------------------+
#

banner login ^C     
________________________________________
|  ILLETÉKTELEN HOZZÁFÉRÉS TILOS!       |
|  BELÉPÉS CSAK JOGOSULT SZEMÉLYEKNEK.  |
|  MINDEN TEVÉKENYSÉG NAPLÓZVA VAN.     |
_________________________________________
^C

banner exec ^C
Sikeres belépés! Kellemes munkát kívánunk.
^C

! ftp user
ip ftp username 1234
ip ftp password 1234

no ip domain-lookup

! Mentés
end
copy running-config startup-config 
wr



```
