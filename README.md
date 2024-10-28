### **Lekcja: Podstawy Obsługi Menedżera Plików Midnight Commander (MC) oraz Konfiguracja IP dla Dwóch Kart Sieciowych w Ubuntu przy użyciu MC**

---

#### **Cel lekcji:**
- **Poznanie i opanowanie podstawowej obsługi menedżera plików Midnight Commander (MC).**
- **Nauczenie się konfigurowania adresów IP dla dwóch kart sieciowych w systemie Ubuntu za pomocą terminala, wykorzystując MC do zarządzania plikami konfiguracyjnymi.**

#### **Materiały potrzebne:**
- Komputer z zainstalowanym systemem Ubuntu (preferowana wersja 20.04 lub nowsza).
- Dostęp do terminala.
- Zainstalowany menedżer plików Midnight Commander (MC).
- Połączenie internetowe (opcjonalnie, do instalacji MC).

---

### **Część 1: Instalacja i Podstawowa Obsługa Menedżera Plików Midnight Commander (MC)**

#### **1.1. Co to jest Midnight Commander?**
**Midnight Commander (MC)** to dwupanelowy menedżer plików działający w trybie tekstowym (terminalowym). Umożliwia łatwe zarządzanie plikami i katalogami za pomocą klawiatury, co jest szczególnie przydatne na serwerach lub w środowiskach bez interfejsu graficznego.

**Główne cechy MC:**
- Dwupanelowy interfejs ułatwiający porównywanie i przenoszenie plików między katalogami.
- Wbudowany edytor tekstu (mcedit) do przeglądania i edycji plików.
- Obsługa skrótów klawiszowych przyspieszających pracę.
- Integracja z systemem plików, archiwami, FTP i innymi zasobami.

#### **1.2. Instalacja Midnight Commander (MC)**

1. **Sprawdzenie, czy MC jest już zainstalowany:**

   Otwórz terminal i wpisz:
   
   ```bash
   mc --version
   ```
   
   - Jeśli MC jest zainstalowany, zobaczysz informację o wersji.
   - Jeśli nie jest zainstalowany, przejdź do instalacji.

2. **Instalacja MC:**

   W terminalu wpisz następujące polecenia:
   
   ```bash
   sudo apt update
   sudo apt install mc
   ```
   
   - Potwierdź instalację, wpisując `y`, gdy zostaniesz o to poproszony.

#### **1.3. Uruchomienie Midnight Commander (MC)**

Aby uruchomić MC, wpisz w terminalu:
   
```bash
mc
```
   
Po chwili powinien uruchomić się interfejs MC z dwoma panelami oraz paskiem menu na górze.

#### **1.4. Podstawowy Interfejs MC**

Interfejs MC składa się z:
- **Dwóch paneli:** Każdy panel wyświetla zawartość innego katalogu, co ułatwia porównywanie i przenoszenie plików.
- **Paska menu:** Znajduje się na górze i wyświetla dostępne polecenia oraz skróty klawiszowe.
- **Paska statusu:** Na dole wyświetla informacje o aktualnie wybranym pliku/katalogu oraz dostępnych poleceniach.

#### **1.5. Nawigacja w MC**

**Poruszanie się po plikach i katalogach:**
- **Strzałki góra/dół:** Przemieszczanie się między plikami i katalogami.
- **Strzałki lewo/prawo:** Przełączanie między panelami.
- **Enter:** Wejście do wybranego katalogu lub otwarie pliku.
- **Backspace:** Powrót do poprzedniego katalogu.
- **Home:** Przejście do katalogu głównego użytkownika.
- **End:** Przejście do korzenia systemu plików (`/`).

**Zmiana widoku:**
- **Tab:** Przełączanie aktywnego panelu.

#### **1.6. Podstawowe Operacje w MC**

**Kopiowanie pliku/katalogu:**
1. Przejdź do katalogu źródłowego w jednym z paneli.
2. Wybierz plik/katalog za pomocą strzałek.
3. Naciśnij `F5` (Copy).
4. Wybierz katalog docelowy w drugim panelu.
5. Potwierdź operację, naciskając `Enter`.

**Przenoszenie/Renamowanie pliku/katalogu:**
1. Wybierz plik/katalog.
2. Naciśnij `F6` (Move/Rename).
3. Wprowadź nową ścieżkę lub nazwę i potwierdź `Enter`.

**Usuwanie pliku/katalogu:**
1. Wybierz plik/katalog.
2. Naciśnij `F8` (Delete).
3. Potwierdź usunięcie.

**Tworzenie nowego katalogu:**
1. Przejdź do miejsca, gdzie chcesz utworzyć katalog.
2. Naciśnij `F7` (Mkdir).
3. Wprowadź nazwę nowego katalogu i potwierdź `Enter`.

**Przeglądanie plików:**
- Naciśnij `F3` aby wyświetlić zawartość pliku (podgląd).
- Naciśnij `F4` aby edytować plik za pomocą wbudowanego edytora (`mcedit`).

---

### **Część 2: Konfiguracja Adresów IP dla Dwóch Kart Sieciowych w Ubuntu przy użyciu MC**

#### **2.1. Wprowadzenie do Konfiguracji Sieciowej w Ubuntu**

Ubuntu używa narzędzia `Netplan` do zarządzania konfiguracją sieciową. Pliki konfiguracyjne Netplan znajdują się w katalogu `/etc/netplan/`. W tym tutorialu użyjemy MC do nawigacji i edycji tych plików, aby skonfigurować dwie karty sieciowe.

#### **2.2. Identyfikacja Kart Sieciowych**

Przed przystąpieniem do konfiguracji, musimy zidentyfikować nazwy interfejsów sieciowych.

1. **Otwórz terminal i uruchom MC:**

   ```bash
   mc
   ```

2. **Sprawdzenie nazw interfejsów sieciowych:**

   W terminalu (poza MC) wpisz:
   
   ```bash
   ip addr show
   ```
   
   Przykładowy wynik może wyglądać tak:
   
   ```
   2: enp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
       inet 192.168.1.100/24 brd 192.168.1.255 scope global enp3s0
          valid_lft forever preferred_lft forever
   3: enp4s0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default qlen 1000
   ```

   W tym przykładzie mamy dwie karty sieciowe:
   - `enp3s0`
   - `enp4s0`

#### **2.3. Konfiguracja Statycznych Adresów IP dla Dwóch Kart Sieciowych za pomocą MC**

1. **Otwórz plik konfiguracyjny Netplan w MC:**

   - W panelu MC, nawiguj do katalogu `/etc/netplan/`.
   - Znajdź plik konfiguracyjny Netplan, np. `01-netcfg.yaml`.
   - Wybierz plik i naciśnij `F4`, aby otworzyć go w edytorze `mcedit`.

2. **Edytuj plik konfiguracyjny:**

   Wprowadź następującą konfigurację, dostosowując nazwy interfejsów i adresy IP do swoich potrzeb:

   ```yaml
   network:
     version: 2
     renderer: networkd
     ethernets:
       enp3s0:
         dhcp4: no
         addresses:
           - 192.168.1.100/24
         gateway4: 192.168.1.1
         nameservers:
           addresses:
             - 8.8.8.8
             - 8.8.4.4
       enp4s0:
         dhcp4: no
         addresses:
           - 10.0.0.100/24
         gateway4: 10.0.0.1
         nameservers:
           addresses:
             - 1.1.1.1
             - 1.0.0.1
   ```

   **Wyjaśnienie konfiguracji:**
   - **enp3s0:**
     - **dhcp4:** Wyłączone (`no`) dla statycznego IP.
     - **addresses:** Przypisany statyczny adres IP (`192.168.1.100/24`).
     - **gateway4:** Adres bramy domyślnej (`192.168.1.1`).
     - **nameservers:** Serwery DNS (`8.8.8.8`, `8.8.4.4`).

   - **enp4s0:**
     - **dhcp4:** Wyłączone (`no`) dla statycznego IP.
     - **addresses:** Przypisany statyczny adres IP (`10.0.0.100/24`).
     - **gateway4:** Adres bramy domyślnej (`10.0.0.1`).
     - **nameservers:** Serwery DNS (`1.1.1.1`, `1.0.0.1`).

   **Uwaga:**
   - **Gateway:** Zazwyczaj tylko jedna karta sieciowa powinna mieć skonfigurowaną bramę domyślną. Jeśli obie karty mają bramy, może to prowadzić do konfliktów routingu.
   - **Jeśli potrzebujesz tylko jednej bramy domyślnej:** Usuń `gateway4` z jednej z kart.

3. **Zapisz i zamknij plik:**

   - W `mcedit` naciśnij `F2`, aby zapisać zmiany.
   - Następnie naciśnij `F10`, aby wyjść z edytora.

4. **Zastosowanie zmian Netplan:**

   W terminalu (poza MC) wpisz:

   ```bash
   sudo netplan apply
   ```

   Jeśli wystąpią błędy w konfiguracji, Netplan poinformuje Cię o nich. Upewnij się, że plik YAML jest poprawnie sformatowany (prawidłowe wcięcia są kluczowe).

5. **Weryfikacja Nowej Konfiguracji:**

   - Sprawdź, czy nowe adresy IP zostały przypisane:

     ```bash
     ip addr show
     ```

   - Upewnij się, że obie karty sieciowe są aktywne i mają przypisane odpowiednie adresy IP.

#### **2.4. Konfiguracja Dynamicznych Adresów IP (DHCP) dla Dwóch Kart Sieciowych za pomocą MC**

Jeżeli chcesz, aby obie karty sieciowe korzystały z DHCP (dynamicznego przydzielania adresów IP), wykonaj następujące kroki:

1. **Otwórz plik konfiguracyjny Netplan w MC:**

   - W panelu MC, nawiguj do katalogu `/etc/netplan/`.
   - Znajdź plik konfiguracyjny Netplan, np. `01-netcfg.yaml`.
   - Wybierz plik i naciśnij `F4`, aby otworzyć go w edytorze `mcedit`.

2. **Edytuj plik konfiguracyjny dla DHCP:**

   Zmień zawartość na:

   ```yaml
   network:
     version: 2
     renderer: networkd
     ethernets:
       enp3s0:
         dhcp4: yes
       enp4s0:
         dhcp4: yes
   ```

   **Uwaga:** Jeśli tylko jedna z kart ma mieć bramę domyślną, skonfiguruj `gateway4` tylko dla tej karty.

3. **Zapisz i zamknij plik:**

   - W `mcedit` naciśnij `F2`, aby zapisać zmiany.
   - Następnie naciśnij `F10`, aby wyjść z edytora.

4. **Zastosowanie zmian Netplan:**

   W terminalu (poza MC) wpisz:

   ```bash
   sudo netplan apply
   ```

5. **Weryfikacja Nowej Konfiguracji:**

   - Sprawdź, czy system uzyskał dynamiczne adresy IP:

     ```bash
     ip addr show
     ```

   - Upewnij się, że obie karty sieciowe mają przypisane adresy IP z DHCP.

---

### **Część 3: Przykładowe Zadania Praktyczne**

#### **3.1. Zadanie 1: Kopiowanie Pliku za pomocą MC**

1. Uruchom MC (`mc`).
2. W lewym panelu przejdź do katalogu zawierającego plik `dokument.txt`.
3. Wybierz `dokument.txt` za pomocą strzałek.
4. Naciśnij `F5` (Copy).
5. W prawym panelu przejdź do katalogu docelowego, np. `Backup`.
6. Potwierdź kopiowanie, naciskając `Enter`.

#### **3.2. Zadanie 2: Edytowanie Pliku Konfiguracyjnego Netplan**

1. Uruchom MC (`mc`).
2. Przejdź do katalogu `/etc/netplan/`.
3. Wybierz plik konfiguracyjny (np. `01-netcfg.yaml`) i naciśnij `F4`, aby otworzyć go w `mcedit`.
4. Dokonaj niezbędnych zmian (np. dodaj drugą kartę sieciową lub zmień adresy IP).
5. Zapisz zmiany (`F2`) i zamknij edytor (`F10`).
6. W terminalu poza MC wpisz `sudo netplan apply`, aby zastosować zmiany.

#### **3.3. Zadanie 3: Tworzenie Nowego Katalogu i Przenoszenie Plików**

1. Uruchom MC (`mc`).
2. W jednym z paneli przejdź do katalogu `Dokumenty`.
3. Naciśnij `F7` (Mkdir) i utwórz nowy katalog o nazwie `Nowy_Katalog`.
4. Przejdź do katalogu źródłowego zawierającego plik `praca.docx`.
5. Wybierz `praca.docx` i naciśnij `F6` (Move/Rename).
6. Przejdź do `Nowy_Katalog` w drugim panelu i potwierdź przeniesienie.

#### **3.4. Zadanie 4: Usuwanie Niepotrzebnego Pliku**

1. Uruchom MC (`mc`).
2. Przejdź do katalogu zawierającego plik `stary_plik.log`.
3. Wybierz `stary_plik.log` za pomocą strzałek.
4. Naciśnij `F8` (Delete).
5. Potwierdź usunięcie, wpisując `y` lub naciskając `Enter`.

#### **3.5. Zadanie 5: Konfiguracja Drugiej Karty Sieciowej**

1. Uruchom MC (`mc`).
2. Przejdź do katalogu `/etc/netplan/`.
3. Otwórz plik konfiguracyjny Netplan (`01-netcfg.yaml`) za pomocą `F4`.
4. Dodaj konfigurację dla drugiej karty sieciowej (jeśli jeszcze nie jest dodana). Przykład:

   ```yaml
   network:
     version: 2
     renderer: networkd
     ethernets:
       enp3s0:
         dhcp4: no
         addresses:
           - 192.168.1.100/24
         gateway4: 192.168.1.1
         nameservers:
           addresses:
             - 8.8.8.8
             - 8.8.4.4
       enp4s0:
         dhcp4: no
         addresses:
           - 10.0.0.100/24
         gateway4: 10.0.0.1
         nameservers:
           addresses:
             - 1.1.1.1
             - 1.0.0.1
   ```

5. Zapisz zmiany (`F2`) i zamknij edytor (`F10`).
6. W terminalu poza MC wpisz `sudo netplan apply`, aby zastosować zmiany.
7. Sprawdź, czy obie karty sieciowe mają przypisane adresy IP:

   ```bash
   ip addr show
   ```

---

### **Część 4: Dodatkowe Funkcje i Konfiguracja MC**

#### **4.1. Wyszukiwanie Plików**

1. Uruchom MC (`mc`).
2. Naciśnij `Ctrl + \`, aby otworzyć okno wyszukiwania.
3. Wprowadź nazwę pliku lub wzorzec wyszukiwania.
4. Potwierdź `Enter`, aby rozpocząć wyszukiwanie.

#### **4.2. Konfiguracja MC**

MC oferuje wiele opcji konfiguracyjnych, które można dostosować do własnych potrzeb.

1. **Dostęp do ustawień:**
   - Naciśnij `F9`, aby otworzyć pasek menu.
   - Przejdź do `Options` za pomocą strzałek i wybierz `Configuration`.

2. **Dostępne opcje:**
   - **Start-up:** Ustawienia dotyczące wyglądu i zachowania MC podczas uruchamiania.
   - **Panel options:** Konfiguracja wyglądu i funkcji paneli.
   - **Layout:** Zmiana układu interfejsu.
   - **Display bits:** Ustawienia dotyczące wyświetlania informacji o plikach.

3. **Zapisywanie ustawień:**
   - Po dokonaniu zmian, wybierz `Save`, aby zapisać konfigurację.

#### **4.3. Podgląd i Edycja Plików**

- **Podgląd pliku:**
  - Wybierz plik i naciśnij `F3`, aby zobaczyć jego zawartość.

- **Edycja pliku:**
  - Wybierz plik i naciśnij `F4`, aby otworzyć go w wbudowanym edytorze `mcedit`.

---

### **Część 5: Podsumowanie i Zadania Domowe**

#### **Podsumowanie:**

W tej lekcji nauczyliśmy się:
- Jak zainstalować i uruchomić menedżer plików Midnight Commander (MC).
- Podstawowych operacji w MC, takich jak kopiowanie, przenoszenie, usuwanie oraz tworzenie katalogów.
- Jak nawigować i edytować pliki konfiguracyjne Netplan za pomocą MC.
- Konfigurować statyczne i dynamiczne adresy IP dla dwóch kart sieciowych w Ubuntu, wykorzystując MC do zarządzania plikami konfiguracyjnymi.

#### **Zadania domowe:**

1. **Konfiguracja IP:**
   - Skonfiguruj statyczne adresy IP dla obu kart sieciowych na swoim systemie Ubuntu, używając MC do edycji plików Netplan.
   - Zmień konfigurację na dynamiczne adresy IP (DHCP) i zweryfikuj działanie.

2. **Praktyka z MC:**
   - Wykonaj opisane w zadaniach praktycznych operacje: kopiowanie, przenoszenie, usuwanie oraz tworzenie katalogów.
   - Stwórz własne zadania, takie jak przeglądanie plików, wyszukiwanie i edycja dokumentów.

3. **Eksperymentowanie z konfiguracją MC:**
   - Dostosuj ustawienia MC, zmieniając wygląd panelów, skróty klawiszowe lub inne dostępne opcje.
   - Sprawdź, jak różne ustawienia wpływają na pracę w MC.

4. **Raportowanie:**
   - Zgłoś ewentualne problemy napotkane podczas wykonywania zadań.
   - Opisz, które funkcje MC okazały się najbardziej przydatne i dlaczego.

#### **Dodatkowe Zasoby:**

- **Oficjalna Dokumentacja MC:** [Midnight Commander](https://midnight-commander.org/)
- **Man Page dla MC:** W terminalu wpisz `man mc`, aby otworzyć podręcznik użytkownika.
- **Społeczność i Wsparcie:**
  - Fora dyskusyjne Linux: [Ubuntu Forums](https://ubuntuforums.org/)
  - GitHub MC: [Midnight Commander na GitHub](https://github.com/MidnightCommander/mc)
- **Dokumentacja Netplan:** [Netplan.io](https://netplan.io/)

---

### **Dodatkowe Wskazówki:**

- **Bezpieczeństwo:** Przy edycji plików konfiguracyjnych zawsze wykonuj kopię zapasową oryginalnych plików. Możesz to zrobić w MC, kopiując plik przed wprowadzeniem zmian.

  ```bash
  sudo cp /etc/netplan/01-netcfg.yaml /etc/netplan/01-netcfg.yaml.bak
  ```

- **Używanie Skrótów Klawiszowych:** Nauka skrótów klawiszowych MC może znacznie przyspieszyć pracę. Zapoznaj się z pełną listą dostępnych skrótów w dokumentacji MC.

- **Eksperymentowanie:** Nie bój się eksperymentować z różnymi funkcjami MC i konfiguracjami sieci. Praktyka jest kluczem do opanowania tych narzędzi.

---

Jeśli masz dodatkowe pytania lub potrzebujesz bardziej zaawansowanych instrukcji dotyczących Midnight Commander lub konfiguracji sieci w Ubuntu, śmiało pytaj!
