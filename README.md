# 📡 Projekt Beacon Spammer 🚀
Cześć! 👋 Witam Was w projekcie **Beacon Spammer**, który pozwala na generowanie fałszywych sieci Wi-Fi (SSID) za pomocą mikrokontrolera ESP8266. To narzędzie może być użyteczne w różnych scenariuszach, takich jak testowanie bezpieczeństwa sieci Wi-Fi 🔐, badanie zachowań urządzeń bezprzewodowych 🧑‍💻, czy po prostu eksperymentowanie z technologią 💡.

# **NOWOŚĆ!**
## **Teraz można wgrać szybciej skrypt [ze strony projektu](https://qbaa134.github.io/Beacon-Spammer).**


## 🎯 Cel projektu

Celem tego projektu jest stworzenie narzędzia, które pozwala na emulowanie sieci Wi-Fi, wysyłając regularnie pakiety beacon z fałszywymi SSID. Każdy pakiet beacon symuluje prawdziwą sieć Wi-Fi, co sprawia, że urządzenia w pobliżu wykrywają "nową" sieć. 🌍

Możesz skonfigurować prefiks SSID, który będzie dodawany do każdej wysyłanej sieci. Dzięki temu możesz łatwo generować dużą liczbę różnych SSID, które będą widoczne na innych urządzeniach w zasięgu. 📱💻

## 📦 Wymagania

Aby uruchomić projekt, będziesz potrzebował:
- Mikrokontroler ESP8266** (np. NodeMCU, Wemos D1 Mini):
![image](https://github.com/user-attachments/assets/6d378cec-3d35-4e42-a325-15104f413880)
- **Środowisko Arduino IDE** z wgranym odpowiednim środowiskiem dla ESP8266
- Kabel USB do połączenia mikrokontrolera z komputerem
- (Opcjonalnie) Dodatkowe biblioteki Arduino

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

## ⚙️ Jak to działa?

Projekt bazuje na wykorzystywaniu funkcji ESP8266 do emulowania sieci Wi-Fi poprzez wysyłanie specjalnie sformatowanych pakietów beacon. Pakiety te zawierają informacje o SSID (nazwie sieci), które będą widoczne dla urządzeń w zasięgu.

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

### Symulacja ataków

Fake SSID Generator może być użyty do symulacji ataków typu "Evil Twin", gdzie tworzysz fałszywą sieć, która ma ten sam SSID, co prawdziwa sieć, aby podszyć się pod nią. Takie techniki są stosowane w testach penetracyjnych, aby sprawdzić, jak dobrze chronione są sieci bezprzewodowe.

### Monitorowanie sieci

Możesz również wykorzystać projekt do monitorowania, które urządzenia są widoczne w twojej okolicy, emulując sieci z różnymi SSID. Może to być pomocne w analizach bezpieczeństwa Wi-Fi lub po prostu w eksperymentach związanych z technologią sieciową.

## 📦 Obudowa
Jeśli masz Wemos D1 mini, możesz wydrukować dedykowaną obudowę, korzystając z pliku w formacie **.3mf**. Dzięki temu Twoje urządzenie będzie lepiej chronione i estetycznie wykończone.
![image](https://github.com/user-attachments/assets/a028a3a8-ed1c-46cb-9f28-6c569c86478f)

## 🌟 Podsumowanie

**Beacon Spammer** to świetne narzędzie do eksperymentowania z technologią Wi-Fi, testowania bezpieczeństwa sieci, a także zabawy z mikrokontrolerami. Dzięki prostocie i elastyczności w konfiguracji możesz dostosować projekt do swoich potrzeb i zrealizować ciekawe projekty związane z sieciami bezprzewodowymi.

Jeśli masz pytania lub sugestie dotyczące projektu, śmiało się nimi podziel! 🚀
