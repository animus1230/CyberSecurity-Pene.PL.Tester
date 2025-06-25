📄 Raport z maszyn Hack The Box – Portfolio 

Cześć! entuzjasta cyberbezpieczeństwa, który już zdobył flagi na kilku maszynach w Hack The Box. Poniżej przedstawiam zestawienie maszyn, które potrafię samodzielnie „złamać”, opis zadań oraz użyte techniki/komendy. Raport jest krótki, czytelny i przygotowany tak, żeby każdy mógł go skopiować i wkleić.


---

1. Meow (miauczeć) 🐾

Opis maszyny: „Meow” to maszyna z serii Starting Point o poziomie trudności Very Easy. Głównym zadaniem jest uwierzytelnienie przez Telnet i odczytanie pliku z flagą.

Zadania:

1. Połączenie do maszyny (ping).


2. Skanowanie portów przy pomocy nmap -p- -sV <IP>.


3. Wykrycie otwartego portu 23 (Telnet).


4. Połączenie przez Telnet:



telnet <IP>

5. Logowanie jako root (brak hasła lub puste hasło).


6. Odczytanie flagi:



ls
cat flag.txt

Wykorzystane komendy:

ping <IP>

nmap -p- -sV <IP>

telnet <IP>

ls, cat flag.txt


Efekt: Zdobycie flagi root. 🎉


---

2. Fawn (płowy) 🌾

Opis maszyny: „Fawn” to Very Easy Linux Box, wprowadzający do protokołu FTP i prostego uwierzytelnienia anonimo w sesji.

Zadania:

1. Połączenie (ping) i skan nmap -sV <IP> – wykrycie portu 21 (FTP).


2. Połączenie do FTP jako anonymous:



ftp <IP>
login: anonymous

3. Przejście do katalogu, pobranie pliku flag.txt:



ls
get flag.txt

Wykorzystane komendy:

ping <IP>

nmap -sV <IP>

ftp <IP>, ls, get flag.txt


Efekt: Zdobycie flagi user. 🎉


---

3. Dancing (taniec) 💃

Opis maszyny: „Dancing” to Very Easy Windows Box, wprowadzający do protokołu SMB. Celem jest zalogowanie się jako anonimowy użytkownik do udziału SMB i odczytanie flagi.

Zadania:

1. Połączenie (ping) i skan nmap -sV -p 139,445 <IP> – porty SMB.


2. Listowanie udziałów SMB:



smbclient -L //<IP>

3. Połączenie do udziału np. WorkShares:



smbclient //<IP>/WorkShares

login: (enter jako pusty lub anonymous)
4. Nawigacja do katalogu użytkownika i pobranie flag.txt:

cd <UserFolder>
get flag.txt

Wykorzystane komendy:

ping <IP>

nmap -sV -p 139,445 <IP>

smbclient -L //<IP>

smbclient //<IP>/WorkShares

cd, get flag.txt (wewnątrz smbclient)


Efekt: Zdobycie flagi user. 🎉


---

4. Redeemer (odkupiciel) ✨

Opis maszyny: „Redeemer” to Very Easy Linux Box – usługa Redis. Trzeba połączyć się do bazy Redis i wyciągnąć flagę z odpowiedniego klucza.

Zadania:

1. Połączenie (ping) i skan nmap -sV <IP> – port 6379 (Redis).


2. Połączenie do Redis:



redis-cli -h <IP> -p 6379

3. Wykonanie komendy w Redis, np.:



KEYS *
GET <nazwa_klucza_z_flaga>

4. Zapisanie flagi.



Wykorzystane komendy:

ping <IP>

nmap -sV <IP>

redis-cli -h <IP> -p 6379

KEYS *, GET <key>


Efekt: Zdobycie flagi user. 🎉


---

5. Explosion (eksplozja) 💥

Opis maszyny: „Explosion” to Very Easy Windows Box – wprowadzenie do RDP. Należy połączyć się przez RDP, znaleźć lokalizację flagi i odczytać ją.

Zadania:

1. Połączenie (ping) i skan nmap -sV <IP> – port 3389 (RDP).


2. Łączenie przez xfreerdp:



xfreerdp /v:<IP> /u:<UserName> /p:<Password>

(w Starting Point często podane zadania: dane logowania użytkownika).
3. Po zalogowaniu otworzenie przeglądarki albo eksploratora plików, znalezienie pliku flag.txt (np. na pulpicie).
4. Odczytanie zawartości flagi.

Wykorzystane komendy:

ping <IP>

nmap -sV <IP>

xfreerdp /v:<IP> /u:<UserName> /p:<Password>


Efekt: Zdobycie flagi user. 🎉


---

6. Ignition (zapłon wstępny) 🚀

Opis maszyny: „Ignition” to Very Easy Linux Box. Trzeba odpowiedzieć na kilka pytań dotyczących HTTP, plików systemowych i panelu admina Magento.

Zadania:

1. Połączenie (ping) i skan nmap -sV <IP> – port 80 (HTTP).


2. Odwiedzenie strony w przeglądarce:



http://ignition.htb/

3. Odpowiedź na pytanie o kod statusu HTTP (200) oraz wersję serwera.


4. Sprawdzenie pliku /etc/hosts – lokalna mapa DNS.


5. Bruteforce katalogów (np. gobuster dir -u http://ignition.htb/ -w /usr/share/wordlists/raft-small-words.txt).


6. Znalezienie panelu admina Magento:



http://ignition.htb/admin

7. Logowanie do panelu admina (użycie słabej, popularnej kombinacji np. admin:qwerty123).


8. Zapisanie flagi root (podana w zadaniach do Submit Root flag).



Wykorzystane komendy:

ping <IP>

nmap -sV <IP>

vim /etc/hosts (ew. cat /etc/hosts)

gobuster dir -u http://ignition.htb/ -w /usr/share/wordlists/raft-small-words.txt

Przeglądarka: http://ignition.htb/admin


Efekt: Zdobycie flagi root. 🎉


---

Podsumowanie 🚀

Wszystkie wyżej wymienione maszyny udało mi się samodzielnie rozwiązać i zdobyć flagi.

Użyte protokoły i narzędzia: ICMP (ping), Nmap, Telnet, FTP, SMB (smbclient), Redis (redis-cli), RDP (xfreerdp), HTTP (gobuster, przeglądarka).

Z każdej maszyny zdobyłem flagę user, a w przypadku Ignition – flagę root.



---

Kilka słów o mnie 🤓💡
 pasjonatem pentestingu i szybko przyswajam wiedzę.

Szukam praktyk – jestem głodny wiedzy i chcę rozwijać się w realnym środowisku.

Posiadam już doświadczenie w środowiskach typu HTB i potrafię samodzielnie przeprowadzić podstawowe ataki sieciowe.

Mam talent do szybkiego uczenia się nowych technologii i narzędzi.



---

Dziękuję za przeczytanie!
Chętnie podejmę się kolejnych wyzwań, praktyk i projektów w dziedzinie cyberbezpieczeństwa.  Powiedz mi czy takie coś mogę napisać w raporcie to wszystko tak razem połączyć mogę

