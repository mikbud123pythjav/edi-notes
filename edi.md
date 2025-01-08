# Egzamin dyplomowy

## Widmo sygnału analogowego (podstawowo-pasmowego i pasmowego) a twierdzenie o
## próbkowaniu

Każdy sygnał analogowy można zapisać jako sumę sinusoid o różnej amplitudzie  i
częstotliwości, taką reprezentację nazywamy widmem sygnału. Żeby zdyskretyzować
ciągły w czasie sygnał analogowy w celu cyfrowego przetwarzania, należy go 
spróbkować. Aby uzyskać pełną reprezentację analogowego sygnału i później go 
wiernie odtworzyć, częstotliwość próbkowania (odpowiadająca stałym odstępom 
pomiędzy każdym pomiarem sygnału) musi być conajmniej dwukrotnie większa od 
najwyższej częstotliwości występującej w oryginalnym sygnale. W przeciwnym 
wypadku dochodzi do aliasingu, czyli częstotliwości powyżej fs odbijają się
w spróbkowanym sygnale jako niższe częstotliwości.

Sygnał podstawowo-pasmowy to taki, którego widmo koncentruje się wokół 
częstotliwości zerowej i rozciąga się od f=0 do fmax, np. audio od ok. 20Hz
do 20kHz. 

Sygnał pasmowy nie zawiera składowych w pobliżu f=0 lecz zawiera się w 
określonym paśmie od f1 do f2, np. sygnał radiowy.

Różnica polega na tym, że w sygnale podstawowo-pasmowym aliasing jest 
problemem, bo wyższe składowe odbijają się od fs i nakładają na składowe 
wewnątrz pasma [f=0; fs] więc trzeba go próbkować z dwukrotnie większą fs od
fmax, a w sygnale pasmowym ten sam aliasing może być narzędziem, ponieważ w 
paśmie [0; fs] nie ma żadnych składowych. Dzięki temu można wykorzystać 
aliasing, aby poodbijać sobie wszystkie składowe sygnału o wysokim paśmie do 
wewnątrz niskiego pasma. Można więc próbkować go z niższą częstotliwością, 
pamiętając jedynie aby fs było 2x większe od B, aby wiernie odwzorować 
wszystkie składowe oraz pamiętając o ile należy przesunąć wszystkie składowe
aby uzyskać faktyczne widmo próbkowanego sygnału.


## DTFT, DFT, FFT

* DTFT - dla sygnału dyskretnego, ciągłego w dziedzinie częstotliwości
    * wynik w zakresie od -pi do pi, odpowiada jednemu pełnemu okresowi
      sygnału dyskretnego
    * widmo X(e^jw)

* DFT - dla sygnału dyskretnego w czasie i częstotliwości, stosowany w 
  praktyce, gdzie liczba próbek i możliwych poziomów jest skończona
    * wynik okresowy z okresem N
    * próbkuje widmo X(e^jw) w N-równomiernie rozmieszczonych punktach

* FFT - efektywna implementacja DFT minimalizująca złożoność obliczeniową
  (O(NlogN) zamiast O(N^2))


## Tor radiowy

* Nadajnik
  Generuje informację którą chcemy nadać
* Koder i kompresor sygnału
  Kompresuje i zapisuję informację za pomocą wybranego kodowania kanałowego
* Modulator
  Pozyskuje z generatora częstotliwość nośną i moduluje ją używając sygnału
  informacyjnego
* Filtry kształtujące
  Odfiltrowują zakłócenia wykraczające poza przydzielone pasmo
* Wzmacniacz mocy
  Wzmacnia sygnał nadając mu moc potrzebną do wysterowania anteny
* Tuner, dopasowanie anteny
  Zapewnia dopasowanie do impedancji anteny
* Antena nadawcza
  Przekształca sygnał na fale elektromagnetyczne

* Tor radiowy
  Wprowadza tłumienie, szum, zakłócenia, dodaje propagację wielotorową

* Antena odbiorcza
  Przekształca nadchodzące fale elektromagnetyczne w sygnał
* Tuner, dopasowanie
  j/w
* Wzmacniacz niskoszumowy
  Wzmacnia odzyskany sygnał, dodając jak najmniej szumów
* Filtr pasmowy
  j/w
* Demodulator
  Ponownie oddziela sygnał informacyjny od częstotliwości nośnej
* Regenerator sygnału
  Wzmacnia i regeneruje zdemodulowany sygnał informacyjny
* Dekoder i dekompresor
  Odczytuje pierwotną informację z kodowania kanałowego
* Odbiornik
  Obsługuje odebraną informację


## Parametry elektryczne anteny

* Zysk
* Impedancja
  Stosunek napięcia do prądu na zaciskach anteny; zazwyczaj 50 lub 75 Ohm;
  musi być dopasowana do linii zasilającej aby nie tracić mocy na odbicia 
  sygnału
* Kierunkowość
* Szerokość wiązki
* Pasmo
* F/B ratio
* Sprawność
* Polaryzacja
    * liniowa
    * kołowa
    * eliptyczna
* Współczynnik fali stojącej
    * od 1 (idealne dopasowanie) do nieskończoności (całkowite odbicie sygnału)

## Budowa i właściwości wzmacniaczy tranzystorowych

### Budowa

* element aktywny
    * tranzystor BJT sterowany prądem bazowym
    * tranzystor FET sterowany napięciem na bramce

* obwody 
    * układ polaryzacji - zapewnia odpowiednie napięcia/prądy na wejściu 
      tranzystora aby działał w liniowym zakresie
    * obciążenie wyjściowe - rezystor, cewka, kondensator lub inny element 
      który odbiera sygnał

* sprzężegnie
    * kondensatory sprzęgające izolują różne stopnie wzmacniacza, 
      przepuszczając jedynie sygnały zmienne


### Właściwości

* wzmocnienie A
* impedancja wejściowa i wyjściowa
* pasmo przenoszenia
* liniowość
* sprawność energetyczna
* szumy własne


### Konfiguracje

* Wspólnego emitera
    * wysokie wzmocnienie
    * średnia Zin
    * odwraca fazę
    * wysoka Zout

* Wspólnej bazy
    * wysokie A
    * bardzo niska Zin
    * wysoka Zout
    * nie odwraca fazy

* Wspólnego kolektora
    * A bliskie 1
    * bardzo wysoka Zin
    * bardzo niska Zout
    * nie odwraca fazy
    * wzmacnia jedynie prąd


## FPGA i CPLD

### Właściwości

* FPGA
    * dynamiczna programowalność (RAM)
    * duża gęstość logiczna - 100k bloków logicznych
    * architektura rozproszona - programowalne połączenia między blokami
    * wyższa częstotliwość pracy
    * większe zużycie energii, wymaga zasilania dla podtrzymania konfiguracji
    * wyższy koszt, bardziej złożone układy
    * wydajność operacyjna bardzo wysoka

* CPLD 
    * trwała programowalność (flash/EEPROM)
    * mała gęstość logiczna - kilkadziesiąt k makrokomórek
    * architektura centralna - sztywne połączenia 
    * niższa częstotliwość pracy
    * mniejsze zużycie energii, trwała konfiguracja, bardziej energooszczędne
    * niższy koszt, prostsze układy, mniej bramek
    * wydajność operacyjna dobra dla prostych i średnio-złożonych aplikacji, 
      takich jak dekodery logiczne

### Zastosowania

* FPGA
    * prototypowanie procesorów i mikroprocesorów
    * złożone DSP
    * akceleracja obliczeń
    * systemy wideo
    * obsługa wysokiej przepustowości np 5G, eth 100G

* CPLD
    * dekodery, liczniki, rejestry, kontrolery czasowe
    * sterowniki automatyki
    * aplikacje zasilane z baterii
    * kontrola urządzeń wbudowanych

## Relacyjny model danych

Podstawowe pojęcia w relacyjnym modelu danych:

* Relacja
    * Matematycznie jest to zbiór uporządkowanych krotek (wierszy).
    * W kontekście baz danych, relacja jest reprezentowana jako tabela.
* Atrybut
    * Kolumna w tabeli, reprezentująca pojedynczą cechę danych.
    * Każdy atrybut ma określony typ danych (np. tekst, liczba, data).
* Krotka
    * Wiersz w tabeli, reprezentujący pojedynczy rekord (instancję danych).
* Schemat relacji
    * Definicja struktury relacji, czyli zbiór nazw atrybutów i ich typów 
    danych.
* Klucz główny (Primary Key)
    * Atrybut (lub zestaw atrybutów), który jednoznacznie identyfikuje każdą 
      krotkę w relacji.
    * Przykład: W tabeli "Pracownicy" kluczem głównym może być numer PESEL.
* Klucz obcy (Foreign Key)
    * Atrybut w jednej relacji, który odwołuje się do klucza głównego w innej 
      relacji, tworząc powiązanie między tabelami.


## Wymień interfejsy przewodowe stosowane w systemach czujnikowych i omów jeden
## szczegółowo.

### Interfejsy przewodowe:

* I²C (Inter-Integrated Circuit)
* SPI (Serial Peripheral Interface)
* UART (Universal Asynchronous Receiver-Transmitter)
* 1-Wire
* CAN (Controller Area Network)
* Ethernet
* RS-232 / RS-485
* Modbus
* USB (Universal Serial Bus)

### I²C - szczegółowo


