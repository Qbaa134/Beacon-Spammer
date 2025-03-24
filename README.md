![Projekt bez nazwy](https://github.com/user-attachments/assets/c55a62b6-598a-4503-94cc-8d73c1f7a948)
# 📡 Projekt Beacon Spammer 🚀
Cześć! 👋 Witam Was w projekcie **Beacon Spammer**, który pozwala na generowanie fałszywych sieci Wi-Fi (SSID) za pomocą mikrokontrolera ESP8266. To narzędzie może być użyteczne w różnych scenariuszach, takich jak testowanie bezpieczeństwa sieci Wi-Fi 🔐, badanie zachowań urządzeń bezprzewodowych 🧑‍💻, czy po prostu eksperymentowanie z technologią 💡.

# W najnowszej wersji skryptu jest również Deauther!

> [!WARNING]
> To narzędzie jest przeznaczone do celów edukacyjnych i testowania własnych sieci. Nie używaj go nielegalnie na cudzych sieciach.

# **NOWOŚĆ!**
## **Teraz można wgrać szybciej skrypt [z oficjalnej strony projektu](https://qbaa134.github.io/Beacon-Spammer).**


## 🎯 Cel projektu

Celem tego projektu jest stworzenie narzędzia, które pozwala na emulowanie sieci Wi-Fi, wysyłając regularnie pakiety beacon z fałszywymi SSID. Każdy pakiet beacon symuluje prawdziwą sieć Wi-Fi, co sprawia, że urządzenia w pobliżu wykrywają "nową" sieć. 🌍

Możesz skonfigurować prefiks SSID, który będzie dodawany do każdej wysyłanej sieci. Dzięki temu możesz łatwo generować dużą liczbę różnych SSID, które będą widoczne na innych urządzeniach w zasięgu. 📱💻
### W przyszłści będzie możliwość wykorzystania w projekcie ekranu `OLED`, przycisków oraz bedzie implementacvja innych funkcji hakerskich!

## 📦 Wymagania


![image](https://github.com/user-attachments/assets/6d378cec-3d35-4e42-a325-15104f413880)
Aby uruchomić skrypt będziesz potrzebował:
- Mikrokontroler ESP8266 (np. NodeMCU, Wemos D1 Mini):
- **Środowisko Arduino IDE** z wgranym odpowiednim środowiskiem dla ESP8266 lub [stronę projektu](https://qbaa134.github.io/Beacon-Spammer)
- Kabel USB do połączenia mikrokontrolera z komputerem
- (Opcjonalnie) Dodatkowe biblioteki Arduino

### Opcjonalne części:
- Li Po akumulator (najlepiej 1000mAh)
- Moduł Tp4056
- Dioda RGB K851264
- Kondensator 10uF
- Kabelki i przewody
- Mini Switch SPDT
- Przetwornica Mini Step Up 3,7V -> 5V
- (Opcjonalnie dioda Shottky)

## 🔌 Podłączenie
![Tekst akapitu (2)](https://github.com/user-attachments/assets/6b8b0966-31f0-4986-8b04-8d0c86dcdeed)


| **Źródło**        | **Cel**          |
|-------------------|------------------|
| Li Po +           | Tp4056 B+        |
| Li Po -           | Tp4056 B-        |
| Tp4056 OUT +      | Switch           |
| Tp4056 OUT -      | Step Up -        |
| Switch            | Step Up +        |
| Step Up +         | 10uF             |
| Step Up -         | 10uF             |
| Step Up OUT +     | 5V              |
| Step Up OUT -     | G                |
| RGB GND           | G                |
| RGB R             | D5               |
| RGB B             | D7               |
| RGB G             | D6               |

Kolory diody:
- Czerwony: Brak aktywności
- Niebieski: Klient podłączony do AP
- Zielony: Trwa transmisja pakietów / Atak Rozpoczęty

## Instalacja
## Arduino IDE
1. **Zainstaluj Arduino IDE**: Jeśli jeszcze go nie masz, pobierz i zainstaluj Arduino IDE z [oficjalnej strony](https://www.arduino.cc/en/software).
   
2. **Skonfiguruj ESP8266 w Arduino IDE**:
   - Otwórz Arduino IDE.
   - Wybierz `Plik` → `Preferencje` i w polu "Dodatkowe menedżery URL dla płytek" dodaj adres: `http://arduino.esp8266.com/stable/package_esp8266com_index.json`.
   - Wybierz `Narzędzia` → `Płytka` → `Płytki menedżer`, wyszukaj `ESP8266` i zainstaluj odpowiednią wersję.
   
3. **Załaduj kod do ESP8266**: Skopiuj kod projektu do nowego szkicu w Arduino IDE i załaduj go do swojego mikrokontrolera ESP8266.

4. **Monitoruj dane na serial monitorze**: Po wgraniu programu możesz monitorować proces generowania pakietów SSID za pomocą `Serial Monitor` w Arduino IDE.

## Pliki bin
1. W przeglądarce na komputerze wejdź na [stronę projektu](https://qbaa134.github.io/Beacon-Spammer), a następnie wybierz wersję oprogramowania.
   - Wersja klasyczna z zaimplementowanymi w kodzie nazwami sieci.
   - Wersja  z interfejsem sieciowym, przez który wpisujemy nazwy sieci.
2. Kliknij `Connect`, przejdź dalej i wgraj plik.

# Wersja z Interfejserm sieciowym
1. Po wgraniu oprogramowania połącz się z wifi `beacon` wpisując hasło `password`.
2. W przeglądarce wpisz adres IP Esp8266, czyli `192.168.4.1.` lub [kliknij w link](http://192.168.4.1/).
3. Wpisz 100 SSID sieci i kliknij `Zielony Przycisk`.
4. Wejdź do [serial monitora](https://qbaa134.github.io/esp-tool/) i połacz się z Esp8266.
![image](https://github.com/user-attachments/assets/c70ba991-65eb-4a4b-bf80-91f123b81345)

- `SSID_name`
- `SSID_name`
- `SSID_name`  
- `SSID_name`
- `itd.`

## Wpisywanie tego samego SSID
Aby sieci były takie same trzeba dodać specjalny znak na końcu SSID.
- `siećx`  
- `siećx` (zawiera ukryty znak po nazwie)
- `siećx` (dwa ukryte znaki)
- `siećx` (trzy ukryte znaki)
- `siećx` (cztery ukryte znaki)
- `itd.`

1.Skopiuj znak Zero-Width Space:

`  `← tutaj jest zero-width space (U+200B)

To wygląda jak "pusta linia", ale znak tam jest. Wklej go na końcu SSID, ile razy chcesz.

2.Możesz go wpisać za pomocą kombinacji:

Alt + 8203 (na klawiaturze numerycznej)

Te dwa sposoby dodadzą U+200B w miejscu kursora.
## Wersja z RGB
Wersja z RGB jest taka sama jak wersja z interfejsem sieciowym, ale do Esp podłączamy diodę, która w zależności od wykonywanej funkcji świeci na dany kolor.

# ⚠️ESP8266 Deauther⚠️

## Co to jest Deauther?

Deauther to specjalistyczne oprogramowanie, które działa na mikrokontrolerze ESP8266 (lub ESP32) i pozwala na przeprowadzanie testów sieci Wi-Fi poprzez wysyłanie pakietów deautoryzacyjnych (deauthentication) oraz disassociacyjnych (disassociation). Głównym celem jest edukacja i testowanie zabezpieczeń sieci bezprzewodowych. Projekt ten jest popularny w środowisku hakerów etycznych oraz pentesterów.

# Instalacja Deauthera
1. W przeglądarce na komputerze wejdź na [stronę projektu](https://qbaa134.github.io/Beacon-Spammer), a następnie wybierz punkt z Deautherem w nazwie.
   - WiFi Deauther (ESP8266).
2. Kliknij `Connect`, przejdź dalej i wgraj plik.
3. Po wgraniu Deauther rozłącza urządzenia od wszystkich dostępnych sieci.
### Uwaga! Używaj skryptu tylko i wyłącznie na własnych sieciach!

## Jak działa Deauther?

Deauther korzysta z możliwości ESP8266 do monitorowania i wysyłania ramek w sieci Wi-Fi. Zasada działania opiera się na lukach w standardzie 802.11, który pozwala na przesyłanie niezaszyfrowanych ramek sterujących — w tym właśnie ramek deauth i disassoc. 

- **Deauthentication** — pakiet informuje klienta, że został nieautoryzowany z siecią. Klient przestaje być połączony z routerem.
- **Disassociation** — pakiet mówi klientowi, że połączenie z punktem dostępowym zostało zerwane. Klient nie zrywa pełnego połączenia, ale musi przejść ponowną negocjację połączenia.


### Legalność i ostrzeżenie

Deauther jest narzędziem edukacyjnym. Używanie go bez zgody właściciela sieci jest nielegalne i może prowadzić do konsekwencji prawnych. Celem tego projektu jest zwiększanie świadomości o bezpieczeństwie Wi-Fi.

Gotowy na dalsze modyfikacje, np. sekcję o konfiguracji?


## ⚙️ Jak działa Beacon Spammer?

Projekt bazuje na wykorzystywaniu funkcji ESP8266 do emulowania sieci Wi-Fi poprzez wysyłanie specjalnie sformatowanych pakietów beacon. Pakiety te zawierają informacje o SSID (nazwie sieci), które będą widoczne dla urządzeń w zasięgu.
## Wszystkie informacje poniżej dotyczą pliku `.ino`
### Struktura pakietu beacon 

Pakiety beacon zawierają różne informacje, w tym:

- **Adres MAC urządzenia**: Unikalny identyfikator sprzętu, który jest wykorzystywany przez sieci Wi-Fi.
- **SSID**: Nazwa sieci Wi-Fi, która jest prezentowana urządzeniom w pobliżu.
- **Wersja WPA/WPA2**: Określenie, jaki typ zabezpieczeń jest używany w danej sieci (opcjonalnie).

Każdy z tych elementów może być zmieniany, co daje ogromne możliwości manipulacji w tym, co urządzenia widzą w swoich listach dostępnych sieci.

### Generowanie SSID

W tym projekcie SSID są generowane dynamicznie, a ich nazwy zaczynają się od określonego prefiksu. Na przykład, jeżeli ustawisz prefiks na `MyFakeSSID_`, wygenerowane SSID mogą wyglądać tak:

- `MyFakeSSID_1`
- `MyFakeSSID_2`
- `MyFakeSSID_3`
- itd.
<img src="https://github.com/user-attachments/assets/221b3a9a-a3d4-42a1-ae6d-21971daa90ac" alt="Opis obrazu" width="400"/>

Dzięki temu łatwo możesz tworzyć wiele sieci o różnych nazwach, co przydaje się w testach bezpieczeństwa.

## 🛠️ Konfiguracja

### Zmiana prefiksu SSID

Aby zmienić prefiks SSID (czyli nazwę generowanych sieci), wystarczy edytować/dodać zmienną w kodzie:

```cpp
"twojasieć\n";
```

Możesz zamienić `"twojasieć"` na dowolny ciąg znaków, który będzie początkiem nazw sieci.

### WPA2

W projekcie zaimplementowano możliwość włączenia/wyłączenia trybu WPA2. Jeśli chcesz, aby twoje sieci były "zabezpieczone" przy pomocy WPA2, ustaw zmienną `wpa2` na `true`:

```cpp
const bool wpa2 = true;  // Tryb WPA2
```

Jeśli chcesz, aby sieci były "otwarte" (bez szyfrowania), ustaw ją na `false`.

### Randomizacja adresu MAC

Adresy MAC generowane są losowo za pomocą funkcji `randomMac()`, co pozwala na emulowanie różnych urządzeń. Pierwszy bajt adresu MAC jest ustawiony na `0x02`, co oznacza, że adres jest lokalnie zarządzany (przeznaczony dla urządzeń, które generują losowe adresy MAC).

```cpp
void randomMac() {
  macAddr[0] = 0x02; // Unicast, lokalnie zarządzany
  for (int i = 1; i < 6; i++) {
     macAddr[i] = random(256);
  }
}
```

## 📊 Monitorowanie

Podczas działania programu na `Serial Monitor` możesz śledzić, jakie SSID zostały wygenerowane, a także informacje o statusie wysyłania pakietów. Jest to szczególnie pomocne, jeśli chcesz debugować swój kod lub sprawdzić, jak wygląda wydajność generowania SSID.

## 🧰 Przykłady użycia

### Testowanie sieci Wi-Fi

Możesz użyć tego projektu do testowania, jak różne urządzenia reagują na wiele dostępnych sieci Wi-Fi. Dzięki temu dowiesz się, jak systemy operacyjne (np. Android, Windows) wykrywają i sortują sieci, a także czy są w stanie rozpoznać fałszywe SSID.

## 📦 Obudowa
Jeśli masz Wemos D1 mini, możesz wydrukować dedykowaną obudowę, korzystając z pliku w formacie **.3mf**. Dzięki temu Twoje urządzenie będzie lepiej chronione i estetycznie wykończone.
![image](https://github.com/user-attachments/assets/a028a3a8-ed1c-46cb-9f28-6c569c86478f)

## 🚀 Przyszłościowe Rozwinięcia

- **Wsparcie WPA3** - Implementacja generowania beaconów ze wsparciem najnowszego standardu zabezpieczeń  
- **Tryb Stealth** - Losowe odstępy czasowe między pakietami dla uniknięcia wykrycia  
- **Dynamiczna zmiana kanałów** - Automatyczne skanowanie i wybór optymalnych kanałów WiFi  
- **Deauthentication Attack** - Integracja funkcji wysyłania pakietów deauth  
- **Geofencing** - Auto-wyłączanie transmisji w oparciu o lokalizację GPS  
- **Advanced SSID Spoofing** - Generowanie realistycznych nazw SSID na podstawie otoczenia  
- **Statystyki w czasie rzeczywistym** - Wizualizacja danych w formie wykresów na interfejsie web  
- **Wsparcie Enterprise WiFi** - Emulacja sieci korporacyjnych z autentykacją 802.1X  
- **Energy Saving Mode** - Optymalizacja zużycia energii dla pracy bateryjnej  
- **Multi-AP Synchronization** - Koordynacja wielu urządzeń do tworzenia złożonych scenariuszy  
- **AI-Powered Patterns** - Generowanie ruchu sieciowego z wykorzystaniem modeli ML  
- **Captive Portal Integration** - Tworzenie interaktywnych portali przechwytujących  
- **Bluetooth Low Energy Spoofing** - Rozszerzenie z połączeniem ESP 32 o emulację urządzeń BLE  
- **Wsparcie OpenWRT** - Portowanie rozwiązania na routery z customowym firmware  
- **RF Shielding Analytics** - Monitorowanie skuteczności maskowania sygnału  
- **Cross-Platform Client** - Dedykowana aplikacja mobilna do zarządzania urządzeniem  

## 🌟 Podsumowanie

**Beacon Spammer** to świetne narzędzie do eksperymentowania z technologią Wi-Fi, testowania bezpieczeństwa sieci, a także zabawy z mikrokontrolerami. Dzięki prostocie i elastyczności w konfiguracji możesz dostosować projekt do swoich potrzeb i zrealizować ciekawe projekty związane z sieciami bezprzewodowymi.

Jeśli masz pytania lub sugestie dotyczące projektu, śmiało się nimi podziel! 🚀
