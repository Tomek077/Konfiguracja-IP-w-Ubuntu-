### Lekcja: Konfiguracja IP w Ubuntu za pomocą terminala oraz podstawowa obsługa menedżera plików MC

#### **Cel lekcji:**
- Zrozumienie podstawowej konfiguracji sieciowej w systemie Ubuntu przy użyciu terminala.
- Poznanie i opanowanie podstawowej obsługi menedżera plików Midnight Commander (MC).

#### **Materiały potrzebne:**
- Komputer z zainstalowanym systemem Ubuntu (preferowana wersja 20.04 lub nowsza).
- Dostęp do terminala.
- Połączenie internetowe (opcjonalnie, do instalacji MC).

---

### **Część 1: Konfiguracja IP w Ubuntu za pomocą terminala**

#### **1.1 Wprowadzenie do konfiguracji sieciowej w Ubuntu**
Ubuntu używa narzędzia `Netplan` do zarządzania konfiguracją sieciową. Pliki konfiguracyjne Netplan znajdują się w katalogu `/etc/netplan/`.

#### **1.2 Sprawdzenie obecnej konfiguracji sieciowej**

1. Otwórz terminal (`Ctrl + Alt + T`).
2. Wpisz poniższe polecenie, aby wyświetlić aktualną konfigurację sieci:

   ```bash
   ip addr show
   ```

   Lub

   ```bash
   ifconfig
   ```

   **Uwaga:** Jeśli `ifconfig` nie jest zainstalowany, możesz go zainstalować za pomocą:

   ```bash
   sudo apt update
   sudo apt install net-tools
   ```

#### **1.3 Konfiguracja statycznego adresu IP**

1. **Otwórz plik konfiguracyjny Netplan:**

   Pliki zazwyczaj znajdują się w `/etc/netplan/`. Możesz wyświetlić zawartość katalogu:

   ```bash
   ls /etc/netplan/
   ```

   Załóżmy, że plik nazywa się `01-netcfg.yaml`. Otwórz go za pomocą edytora tekstu `nano`:

   ```bash
   sudo nano /etc/netplan/01-netcfg.yaml
   ```

2. **Przykładowa konfiguracja dla statycznego IP:**

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
   ```

   - **enp3s0** – nazwa interfejsu sieciowego. Możesz sprawdzić swoją nazwę interfejsu za pomocą `ip addr show`.
   - **addresses** – przypisany statyczny adres IP wraz z maską sieciową.
   - **gateway4** – adres bramy domyślnej.
   - **nameservers** – adresy serwerów DNS.

3. **Zastosowanie zmian:**

   Po zapisaniu pliku (w `nano` naciśnij `Ctrl + O`, potem `Enter`, a następnie `Ctrl + X`), zastosuj konfigurację:

   ```bash
   sudo netplan apply
   ```

4. **Weryfikacja:**

   Sprawdź, czy nowa konfiguracja została zastosowana:

   ```bash
   ip addr show
   ```

   Lub

   ```bash
   ifconfig
   ```

#### **1.4 Konfiguracja dynamicznego adresu IP (DHCP)**

1. **Otwórz plik konfiguracyjny Netplan:**

   ```bash
   sudo nano /etc/netplan/01-netcfg.yaml
   ```

2. **Przykładowa konfiguracja dla DHCP:**

   ```yaml
   network:
     version: 2
     renderer: networkd
     ethernets:
       enp3s0:
         dhcp4: yes
   ```

3. **Zastosowanie zmian:**

   ```bash
   sudo netplan apply
   ```

4. **Weryfikacja:**

   ```bash
   ip addr show
   ```

---

### **Część 2: Menedżer plików Midnight Commander (MC)**

#### **2.1 Wprowadzenie do MC**
Midnight Commander (MC) to dwupanelowy menedżer plików działający w trybie tekstowym. Umożliwia łatwe zarządzanie plikami i katalogami za pomocą klawiatury.

#### **2.2 Instalacja MC**

1. **Sprawdź, czy MC jest już zainstalowany:**

   ```bash
   mc --version
   ```

2. **Jeśli nie jest zainstalowany, zainstaluj go:**

   ```bash
   sudo apt update
   sudo apt install mc
   ```

#### **2.3 Uruchomienie MC**

W terminalu wpisz:

```bash
mc
```

Powinien uruchomić się interfejs MC z dwoma panelami.

#### **2.4 Podstawowe operacje w MC**

- **Nawigacja:**
  - **Strzałki:** Poruszanie się po plikach i katalogach.
  - **Enter:** Wejście do wybranego katalogu lub otwarie pliku.
  - **Backspace:** Powrót do poprzedniego katalogu.

- **Operacje na plikach:**
  - **F5 (Copy):** Kopiowanie wybranego pliku/katalogu.
  - **F6 (Move/Rename):** Przenoszenie lub zmiana nazwy pliku/katalogu.
  - **F7 (Mkdir):** Tworzenie nowego katalogu.
  - **F8 (Delete):** Usuwanie wybranego pliku/katalogu.

- **Wyszukiwanie plików:**
  - Naciśnij `Ctrl + \` aby rozpocząć wyszukiwanie plików.

- **Podgląd plików:**
  - Zaznacz plik i naciśnij `F3` aby go wyświetlić.
  - Naciśnij `F4` aby edytować plik za pomocą wbudowanego edytora.

- **Zamykanie MC:**
  - Naciśnij `F10`.

#### **2.5 Przykładowe zadania z MC**

1. **Kopiowanie pliku:**
   - Przejdź do katalogu źródłowego.
   - Wybierz plik za pomocą strzałek.
   - Naciśnij `F5`.
   - Wybierz katalog docelowy i potwierdź.

2. **Tworzenie nowego katalogu:**
   - Przejdź do miejsca, gdzie chcesz utworzyć katalog.
   - Naciśnij `F7`.
   - Wprowadź nazwę katalogu i potwierdź.

3. **Usuwanie pliku:**
   - Wybierz plik.
   - Naciśnij `F8`.
   - Potwierdź usunięcie.

---

### **Podsumowanie**

W tej lekcji nauczyliśmy się, jak konfigurować adres IP w systemie Ubuntu za pomocą terminala, korzystając z narzędzia Netplan. Ponadto, poznaliśmy podstawową obsługę menedżera plików Midnight Commander, który umożliwia efektywne zarządzanie plikami i katalogami w środowisku tekstowym.

#### **Zadania domowe:**
1. Skonfiguruj statyczny adres IP na swoim systemie Ubuntu.
2. Przećwicz podstawowe operacje w MC: kopiowanie, przenoszenie, tworzenie i usuwanie plików/katalogów.
3. Zgłoś ewentualne problemy napotkane podczas wykonywania zadań.

#### **Dodatkowe zasoby:**
- [Oficjalna dokumentacja Netplan](https://netplan.io/)
- [Man page dla MC](https://linux.die.net/man/1/mc)

---
