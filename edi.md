# Egzamin dyplomowy - ogólne

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

* przewody +, -, SDA, SCL
* podłączenie wielu urządzeń do tych samych 2 linii
* jeden master reszta slave
* każdy slave ma unikalny adres (arbitraż adresowy)
* max ~3 Mbps
* zasięg do kilku metrów


## Zasada działania, właściwości i zastosowania wybranych elementów systemu
## optoelektronicznego (źródła, modulatory, detektory).

Systemy optoelektroniczne
Systemy optoelektroniczne to układy wykorzystujące światło (fale elektromagnetyczne w zakresie widzialnym, podczerwieni lub ultrafioletu) do przesyłania, przetwarzania lub detekcji informacji. Kluczowymi elementami takich systemów są:

Źródła światła (np. diody LED, lasery).
Modulatory (zmieniające właściwości światła w czasie).
Detektory światła (np. fotodiody, fotopowielacze).
1. Źródła światła
Zasada działania
Źródła światła generują promieniowanie elektromagnetyczne w wyniku procesów fizycznych, takich jak:

Emisja spontaniczna (np. w diodach LED).
Emisja wymuszona (np. w laserach).
Rodzaje źródeł światła:
Diody LED (Light Emitting Diodes):
Wytwarzają światło w wyniku rekombinacji nośników ładunku (elektronów i dziur) w półprzewodniku.
Emitują światło w zakresie widzialnym, podczerwonym lub ultrafioletowym.
Lasery:
Generują światło spójne (o jednej długości fali) dzięki zjawisku emisji wymuszonej.
Wykorzystują rezonator optyczny do wzmacniania światła.
Właściwości źródeł światła:
Długość fali: Określa kolor światła (np. światło widzialne, podczerwień).
Spójność: Wysoka w przypadku laserów, niska w diodach LED.
Moc promieniowania: Zależy od zastosowania (np. lasery wysokiej mocy dla komunikacji światłowodowej).
Zastosowania:
Diody LED: Oświetlenie, wskaźniki, ekrany.
Lasery: Komunikacja światłowodowa, obróbka materiałów, medycyna (np. laseroterapia), skanery kodów kreskowych.
2. Modulatory światła
Zasada działania
Modulatory zmieniają właściwości światła, takie jak:

Amplituda (jasność).
Częstotliwość.
Faza.
Polaryzacja.
Zmiany te są stosowane do kodowania informacji w wiązce świetlnej.

Rodzaje modulatorów:
Modulatory elektrooptyczne:
Wykorzystują efekt Pockelsa lub Kerra, gdzie zastosowane pole elektryczne zmienia współczynnik załamania światła w materiale.
Modulatory akustooptyczne:
Fala akustyczna w materiale zmienia współczynnik załamania światła, co prowadzi do modulacji.
Modulatory termooptyczne:
Zmiana temperatury powoduje zmiany współczynnika załamania światła.
Właściwości:
Prędkość modulacji: Określa, jak szybko można zmieniać parametry światła (ważne w komunikacji optycznej).
Czułość: Zdolność do efektywnego modulowania światła przy niskiej energii sterującej.
Zastosowania:
Komunikacja światłowodowa (np. modulacja amplitudy światła w transmisji danych).
Laserowe systemy pomiarowe (np. LIDAR).
Projekcja obrazów (np. w wyświetlaczach holograficznych).
3. Detektory światła
Zasada działania
Detektory konwertują energię świetlną na sygnał elektryczny, dzięki zjawiskom takim jak:

Efekt fotoelektryczny: Światło uwalnia elektrony z materiału.
Efekt fotowoltaiczny: Światło generuje napięcie w półprzewodniku.
Rodzaje detektorów:
Fotodiody:
Wytwarzają prąd elektryczny proporcjonalny do natężenia padającego światła.
Typy:
PIN: szerokie pasmo częstotliwości.
APD (Avalanche Photodiode): wysoka czułość.
Fotopowielacze:
Wzmacniają sygnały świetlne dzięki wielokrotnemu pomnażaniu elektronów.
Bardzo czułe, stosowane w pomiarach słabego światła.
Czujniki CCD i CMOS:
Konwertują światło na sygnał cyfrowy w kamerach i aparatach.
Właściwości:
Czułość spektralna: Zakres długości fal, na które reaguje detektor.
Prędkość odpowiedzi: Jak szybko detektor reaguje na zmiany światła.
Zakres dynamiczny: Zakres natężeń światła, które może zarejestrować.
Zastosowania:
Fotodiody: Komunikacja światłowodowa, czujniki optyczne.
Fotopowielacze: Detektory cząstek, spektroskopia, astronomia.
Czujniki CCD/CMOS: Kamery, obrazowanie medyczne.
Przykład działania systemu optoelektronicznego
Komunikacja światłowodowa:

Źródło światła: Laser generuje światło podczerwone, które jest nośnikiem informacji.
Modulator: Koduje dane (np. modulacja amplitudy lub fazy).
Detektor: Na drugim końcu światłowodu fotodioda odbiera światło i przekształca je w sygnał elektryczny.


## Architektury procesorów rdzeniowych mikrokontrolerów

Architektury procesorów rdzeniowych mikrokontrolerów
Architektura rdzenia procesora mikrokontrolera określa sposób organizacji jego komponentów (np. jednostki obliczeniowej, pamięci, magistral). Wpływa ona na wydajność, funkcjonalność i zastosowania mikrokontrolera. Istnieje kilka kluczowych typów architektur stosowanych w mikrokontrolerach.

1. Podział architektur procesorów rdzeniowych
RISC (Reduced Instruction Set Computer)

Zmniejszony zestaw instrukcji, zoptymalizowany pod kątem szybkości i efektywności.
Przykłady: ARM Cortex-M, AVR.
CISC (Complex Instruction Set Computer)

Rozbudowany zestaw instrukcji, pozwalający na wykonywanie złożonych operacji w jednej instrukcji.
Przykłady: x86, niektóre architektury DSP.
Harvard vs. von Neumann:

Harvard: Oddzielne magistrale danych i instrukcji (np. AVR, ARM Cortex-M).
von Neumann: Wspólna magistrala dla danych i instrukcji (np. 8051, PIC w starszych wersjach).
Architektury specjalizowane:

Wykorzystujące DSP (Digital Signal Processing) lub inne zoptymalizowane jednostki obliczeniowe do określonych zadań (np. przetwarzanie sygnałów).
Przykłady: ARM Cortex-M4F (z jednostką FPU), dsPIC.
2. Najpopularniejsze architektury rdzeni mikrokontrolerów
ARM Cortex-M
Architektura: RISC, Harvard.
Cechy:
Niskie zużycie energii.
Duża moc obliczeniowa przy zachowaniu prostoty programowania.
Obsługa 32-bitowych instrukcji.
Rodziny:
Cortex-M0/M0+: Najprostsze, energooszczędne, tanie.
Cortex-M3: Większa moc obliczeniowa, bardziej złożone aplikacje.
Cortex-M4/M7: Obsługa DSP i jednostek FPU (przetwarzanie sygnałów, aplikacje multimedialne).
Zastosowania: IoT, automatyka przemysłowa, urządzenia medyczne, systemy wbudowane.
AVR (Atmel, obecnie Microchip)
Architektura: RISC, Harvard.
Cechy:
8-bitowe rejestry, prosty zestaw instrukcji.
Wysoka efektywność w prostych aplikacjach.
Rodziny:
ATmega: Ogólnego przeznaczenia (np. Arduino).
ATtiny: Miniaturowe aplikacje.
Zastosowania: Małe systemy wbudowane, urządzenia niskobudżetowe.
8051 (Intel, obecnie wiele producentów)
Architektura: CISC, von Neumann.
Cechy:
8-bitowy procesor.
Rozbudowana rodzina instrukcji.
Stosunkowo niska wydajność w porównaniu do nowoczesnych mikrokontrolerów.
Zastosowania: Starsze systemy wbudowane, systemy przemysłowe.
PIC (Microchip)
Architektura: RISC, Harvard.
Cechy:
Szeroka gama produktów (od prostych do zaawansowanych mikrokontrolerów).
Modularność i elastyczność.
Rodziny:
PIC10/12/16: Proste aplikacje.
PIC18: Zaawansowane aplikacje 8-bitowe.
dsPIC: Wbudowane DSP dla przetwarzania sygnałów.
Zastosowania: Elektronika konsumencka, automatyka.
RISC-V
Architektura: RISC, Harvard.
Cechy:
Otwarta, darmowa architektura, którą można dostosowywać do własnych potrzeb.
Nowoczesna i elastyczna.
Zastosowania: Aplikacje IoT, badania naukowe, rozwój nowych technologii.
3. Kluczowe właściwości architektur rdzeni mikrokontrolerów
Cechy	RISC	CISC
Zestaw instrukcji	Prosty, niewielka liczba instrukcji	Rozbudowany, złożone instrukcje
Prędkość działania	Wysoka (krótkie instrukcje, 1 cykl)	Wolniejsza w porównaniu do RISC
Zużycie energii	Mniejsze	Większe
Koszt implementacji	Niski	Wyższy
Zastosowania	Systemy wbudowane, IoT, automatyka	Rozbudowane systemy obliczeniowe
4. Przykład zastosowania – ARM Cortex-M4
Architektura:
Harvard RISC, 32-bitowa.
Zawiera jednostkę DSP i FPU.
Zastosowanie:
Przetwarzanie sygnałów: Analiza danych z czujników w systemach medycznych.
IoT: Zbieranie i przesyłanie danych do chmury.
Multimedia: Sterowanie urządzeniami audio. 
Dlaczego ARM Cortex-M4?
Wysoka moc obliczeniowa przy niskim zużyciu energii.
Wszechstronność dzięki DSP i FPU.
Podsumowanie
Architektury rdzeni mikrokontrolerów różnią się pod względem zestawu instrukcji, organizacji pamięci i wydajności. RISC (np. ARM Cortex-M) dominuje w nowoczesnych zastosowaniach, zapewniając wysoką wydajność i energooszczędność. CISC (np. 8051) jest stosowany w starszych systemach i specyficznych aplikacjach. Wybór architektury zależy od wymagań aplikacji, takich jak moc obliczeniowa, złożoność systemu, koszt i zużycie energii.


## W jaki sposób można zrealizować w zakresie b.w.cz. czystą reaktancję?

Zdecyduj, czego potrzebujesz:
Pojemności? Zakończ linię otwarto.
Indukcyjności? Zakończ linię zwarciem.
Dopasuj długość linii transmisyjnej:
Krótka linia (𝑙≪𝜆) da czystą reaktancję.
Gotowe! Linia transmisyjna teraz działa jak kondensator lub cewka w zakresie 
b.w.cz., bez efektów pasożytniczych.


## Do czego służy strojnik pojedynczy i jaka jest jego zasada działania?

odchodzi z boku głównej linii transmisyjnej. Używa się go do dopasowania 
impedancji, żeby sygnał mógł płynąć bez odbić i strat mocy.
Odcinek przewodu (czyli strojnik) ma określoną długość, np. 𝜆/4 lub krótszą. 
Na jego końcu jest zwarcie lub otwarty koniec, co pozwala tworzyć efekt „cewki”
(indukcyjność) albo „kondensatora” (pojemność). Gdy go podłączysz bocznie do 
głównej linii transmisyjnej, zmienia całkowitą impedancję widzianą przez 
nadajnik, żeby pasowała do impedancji obciążenia (np. anteny). W linii 
transmisyjnej fale odbijają się od zakończenia (zwarty/otwarty koniec). Odbite 
fale tworzą rezonans w zależności od długości strojnika i częstotliwości 
sygnału. Wzdłuż długości strojnika impedancja się zmienia, ponieważ fala 
„przemieszcza się” po linii i zmienia fazę.

na wykresie schmidta się przemieszcza parametrem d (od obciążenia) i l 
(strojnika) transformując impedancję

## Omów ramy stosowania rachunku wskazów w analizie obwodów i niekonkurencyjność
## rachunku operatorowego Laplace’a w tych ramach.

Dzięki wskazom, prawa Kirchhoffa można zapisać jako równania algebraiczne w 
dziedzinie zespolonej. Prąd lub napięcie sinusoidalne cos(ωt+ϕ) reprezentuje 
się jako liczby zespolone. Każdy element obwodu ma reprezentację w dziedzinie 
zespolonej:

* Rezystor: 𝑍𝑅 = 𝑅
* Cewka: 𝑍𝐿=jωL
* Kondensator: 𝑍𝐶=1/𝑗𝜔𝐶

1. Obwody w stanie przejściowym:
    * Rachunek Laplace’a: Działa w stanach przejściowych i dla dowolnych 
      przebiegów sygnałów, w tym impulsowych czy nieregularnych. 
    * Rachunek wskazów: Nie nadaje się do analizy stanów przejściowych, działa 
      tylko w stanie ustalonym.
2. Dowolne przebiegi sygnałów:
    * Rachunek Laplace’a: Obsługuje sygnały o dowolnym kształcie, dzięki czemu 
      pozwala analizować złożone przebiegi czasowe.
    * Rachunek wskazów: Ogranicza się do sinusoidalnych sygnałów o stałej 
      częstotliwości.
3. Skomplikowane obwody:
    * Rachunek Laplace’a: Radzi sobie z bardziej skomplikowanymi układami 
      nieliniowymi i czasowo-zmiennymi.
    * Rachunek wskazów: Ograniczony do liniowych obwodów o stałych parametrach.
4. Prostota analizy:
    * Rachunek wskazów: Jest łatwiejszy do zrozumienia i stosowania w prostych 
      przypadkach.
    * Rachunek Laplace’a: Jest bardziej złożony, ale ma szersze możliwości.

## Sformułuj i zapisz w postaci ogólnej prawa Kirchhoffa oraz podaj własne 
## przykłady ilustrujące treść tych praw.

1. Pierwsze prawo Kirchhoffa – Prawo prądów (KCL):
    Suma algebraiczna prądów wpływających do węzła w obwodzie elektrycznym jest 
    równa sumie prądów wypływających z tego węzła. W węźle nie gromadzi się 
    ładunek.

2. Drugie prawo Kirchhoffa – Prawo napięć (KVL)
    Suma algebraiczna napięć w oczku (zamkniętej pętli) obwodu elektrycznego 
    jest równa zeru. Energia przekazywana przez źródła napięcia w oczku jest 
    równa energii zużywanej na elementach obwodu.

# Egzamin dyplomowy - Telekomunikacja

## Omów problem analizy i syntezy zasobów w sieci telekomunikacyjnej.

### Analiza zasobóow

Celem analizy jest:
* Zrozumienie aktualnego stanu sieci.
* Identyfikacja potencjalnych problemów, takich jak przeciążenie, wąskie 
  gardła, czy niewykorzystane zasoby.

Problemy analizy zasobów:
* **Przeciążenie sieci**
  Gdy zasoby sieci (np. przepustowość) są niewystarczające, pojawiają się 
  opóźnienia, utrata pakietów i degradacja jakości usług (QoS).
* **Wąskie gardła**
  Lokalizacje w sieci, gdzie przepustowość jest znacznie niższa niż w 
  pozostałych częściach, co prowadzi do spowolnienia transmisji.
* **Niewykorzystane zasoby**
  Zbyt wiele nadmiarowych zasobów może prowadzić do marnotrawstwa, co zwiększa 
  koszty operacyjne.
* **Zmienne obciążenie**
  Sieci telekomunikacyjne mają nieregularne obciążenia w czasie (np. godziny 
  szczytu), co utrudnia efektywne planowanie.
* **Integracja nowych technologii**
  Przejście na nowe technologie, takie jak 5G, wymaga analizy istniejących 
  zasobów i planowania ich modernizacji.

Kluczowe metody analizy zasobów:
* Analiza ruchu sieciowego
* Symulacje
* Pomiar QoS
* Analiza danych historycznych

### Synteza zasobów

Synteza obejmuje:
* Planowanie nowych połączeń, węzłów i ścieżek.
* Rozdzielanie zasobów w celu optymalizacji kosztów i wydajności.

Problemy syntezy zasobów: 
* **Efektywne przydzielanie zasobów**
  Jak rozdzielić przepustowość, pasmo częstotliwości, czy moce obliczeniowe w 
  sposób optymalny między różne usługi i użytkowników.
* **Minimalizacja kosztów**
  Synteza zasobów musi uwzględniać optymalizację kosztów operacyjnych i 
  inwestycyjnych.
* **Zapewnienie jakości usług (QoS)**
  Wymaga spełnienia parametrów, takich jak opóźnienie, jitter, dostępność, i 
  przepustowość dla różnych aplikacji.
* **Skalowalność sieci**
  Projektowanie sieci musi uwzględniać możliwość łatwej rozbudowy w przyszłości
  , np. przy wzroście liczby użytkowników lub wdrożeniu nowych technologii.
* **Zarządzanie ryzykiem**
  Synteza musi uwzględniać redundancję i mechanizmy awaryjne, które zabezpieczą
  działanie sieci w przypadku awarii.

Kluczowe metody syntezy zasobów:
* Optymalizacja ścieżek routingu
* Przydział zasobów pasma
* Mechanizmy zarządzania ruchem
* Redundancja i planowanie awaryjne
* Wirtualizacja sieci

---

## Scharakteryzuj architektury wspierające realizację sieci IP QoS.

1. Best-Effort (Podejście bez gwarancji QoS)
Standardowe podejście w sieciach IP, w którym wszystkie pakiety są traktowane 
jednakowo. Brak priorytetyzacji lub gwarancji jakości transmisji.

* Zalety: Prosta implementacja, brak dodatkowych kosztów.
* Wady: Nieodpowiednia dla aplikacji wymagających niskich opóźnień i 
  gwarantowanej przepustowości (np. VoIP, wideo strumieniowe).
* Zastosowania: E-mail, przeglądanie WWW.

2. Integrated Services (IntServ)
Architektura oparta na rezerwacji zasobów wzdłuż ścieżki przesyłania danych.
Wykorzystuje protokół RSVP (Resource Reservation Protocol) do rezerwacji 
zasobów w routerach.

* Rezerwacja zasobów: Każdy strumień danych musi zarezerwować wymagane zasoby 
  (np. przepustowość, bufory).
* Gwarantowana QoS: Zapewnia parametry jakości transmisji dla indywidualnych 
  połączeń.
* Wady: Niska skalowalność, duże obciążenie routerów przez konieczność 
  przechowywania stanu każdego połączenia.
* Zastosowania: Aplikacje wymagające gwarantowanej jakości, np. 
  wideokonferencje, transmisje w czasie rzeczywistym.

3. Differentiated Services (DiffServ)
Architektura oparta na klasyfikacji ruchu i przypisywaniu priorytetów.
Każdy pakiet jest oznaczany w nagłówku IP polem DSCP (Differentiated Services 
Code Point), które określa jego klasę usług.

* Klasy usług: Ruch jest grupowany w klasy, np. wysoki priorytet dla VoIP, 
  niski dla e-mail.
* Elastyczność: Mechanizmy QoS są realizowane w routerach na podstawie klas, 
  bez przechowywania stanu połączeń.
* Wady: Brak ścisłych gwarancji jakości, tylko względne priorytety.
* Zastosowania: Sieci korporacyjne i ISP obsługujące ruch mieszany (VoIP, 
  wideo, dane).

4. Multiprotocol Label Switching (MPLS)
Architektura, która umożliwia tworzenie wirtualnych ścieżek (Label-Switched 
Paths, LSP) w sieci, zapewniając lepsze zarządzanie ruchem. Pakiety są 
kierowane na podstawie etykiet MPLS, a nie adresów IP.

* QoS na poziomie ścieżki: Możliwość definiowania tras o określonych 
  parametrach jakości.
* Efektywność: Szybsze przesyłanie pakietów dzięki etykietom zamiast analizy 
  nagłówka IP.
* Wady: Złożoność konfiguracji i wdrożenia.
* Zastosowania: Sieci operatorów telekomunikacyjnych, transmisje o wysokiej 
  niezawodności.

5. Traffic Engineering (TE) z SDN i NFV
Nowoczesne podejście wykorzystujące Software-Defined Networking (SDN) i Network
Function Virtualization (NFV). SDN umożliwia centralne zarządzanie ruchem 
sieciowym, a NFV pozwala na elastyczne wdrażanie funkcji sieciowych.

* Centralne sterowanie: Dynamiczne przydzielanie zasobów i kierowanie ruchem na
  podstawie aktualnych warunków w sieci.
* Wysoka elastyczność: Możliwość adaptacji do zmieniających się wymagań QoS.
* Wady: Wymaga nowoczesnej infrastruktury i protokołów.
* Zastosowania: Sieci 5G, IoT, chmura obliczeniowa.


Podsumowanie
* Best-Effort: Brak QoS, ale prostota i niskie koszty.
* IntServ: Gwarantowana QoS, ale ograniczona skalowalność.
* DiffServ: Priorytetyzacja ruchu i dobra skalowalność, ale bez pełnych 
  gwarancji.
* MPLS: Efektywne zarządzanie ruchem z QoS na poziomie ścieżki.
* SDN/NFV: Nowoczesne i elastyczne podejście, odpowiednie dla dynamicznych 
  sieci.

Każda architektura ma swoje zalety i wady, a wybór zależy od wymagań aplikacji 
i środowiska sieciowego. W praktyce stosuje się często hybrydowe podejścia, 
które łączą elementy kilku architektur.

---

## Przedstaw bilans energetyczny i scharakteryzuj jego znaczenie przy projektowaniu łącza
## radiowego.

### Elementy bilansu energetycznego

* **Moc nadajnika Pt**
    * Moc wyjściowa generowana przez nadajnik.
    * Wpływa na zasięg i jakość sygnału.

* **Zysk anteny nadawczej Gt**
    * Zdolność anteny nadawczej do skupienia energii w określonym kierunku.
    * Wyrażana w decybelach izotropowych (

* **Straty w linii transmisyjnej nadajnika Lt**
    * Straty energii na kablach i złączach między nadajnikiem a anteną.

* **Tłumienie propagacyjne Lp**
    * Straty mocy sygnału w wyniku propagacji przez powietrze.

* **Zysk anteny odbiorczej Gr**
    * Zdolność anteny odbiorczej do skupienia energii z określonego kierunku.

* **Straty w linii transmisyjnej odbiorczej Lr**
    * Straty mocy na kablach i złączach między anteną odbiorczą a odbiornikiem.

* **Czułość odbiornika Sr**
    * Minimalna moc sygnału wymagana przez odbiornik do poprawnego dekodowania 
      danych.

### Równanie bilansu energetycznego

    **Pr = Pt + Gt − Lt − Lp + Gr − Lr** 

### Znaczenie bilansu energetycznego przy projektowaniu łącza radiowego

* **Zapewnienie niezawodności łącza**:
    * Analiza bilansu energetycznego pozwala przewidzieć, czy sygnał 
    docierający do odbiornika będzie wystarczająco silny do poprawnego odbioru.
* **Określenie wymagań sprzętowych**:
    * Umożliwia dobór odpowiednich anten (o odpowiednich zyskach), nadajników 
    (o odpowiedniej mocy) i odbiorników (o wymaganej czułości).
* **Uwzględnienie tłumienia propagacyjnego**:
    * Pozwala na oszacowanie wpływu odległości, przeszkód (np. budynków, drzew)
    a także warunków atmosferycznych na jakość łącza.
* **Optymalizacja kosztów**:
    * Poprawne wyliczenie bilansu energetycznego zapobiega nadmiarowym wydatkom
    na sprzęt o niepotrzebnie dużej mocy czy wysokich parametrach.
* **Rezerwa energetyczna (margines łącza)**:
    * Przy projektowaniu dodaje się margines bezpieczeństwa, aby zrekompensować 
    nieprzewidziane zmiany, takie jak zakłócenia czy starzenie się sprzętu.


## System komórkowy GSM, architektura, podstawowe parametry i rodzaje usług.

### Architektura systemu GSM

* A. Stacja bazowa (Base Station Subsystem, BSS):
    * Stacja bazowa (Base Transceiver Station, BTS):
        * Fizyczna infrastruktura odpowiedzialna za transmisję sygnałów 
        radiowych.
        * Obsługuje interfejs radiowy z urządzeniami mobilnymi (MS).
        * BTS komunikuje się z wieloma urządzeniami jednocześnie.
    * Sterownik stacji bazowych (Base Station Controller, BSC):
        * Zarządza wieloma BTS-ami.
        * Odpowiada za przydział zasobów radiowych, handover (przełączanie 
        połączeń) i kontrolę mocy.

* B. Sieć i centrum przełączania (Network and Switching Subsystem, NSS):
    * Mobilna centrala przełączania (Mobile Switching Center, MSC):
        * Odpowiada za zestawianie, kierowanie i rozłączanie połączeń.
        * Zarządza komunikacją między użytkownikami w tej samej sieci i z 
        innymi sieciami.
    * Rejestry baz danych:
        * HLR (Home Location Register): Przechowuje dane abonenta, np. numer 
        telefonu, subskrypcje usług.
        * VLR (Visitor Location Register): Tymczasowa baza danych dla abonentów
        przebywających w obszarze kontrolowanym przez MSC.
        * AUC (Authentication Center): Przechowuje dane autoryzacyjne, 
        zapewniając bezpieczeństwo.
        * EIR (Equipment Identity Register): Zawiera listę legalnych urządzeń, 
        identyfikowanych za pomocą IMEI.

* C. Podsystem operacyjny i zarządzania (OSS):
    Zarządza całą siecią, monitoruje jej wydajność, konfigurację i stan 
    urządzeń.

2. Podstawowe parametry GSM
    * Pasmo częstotliwości:
        * 900 MHz: 890–915 MHz (uplink), 935–960 MHz (downlink).
        * 1800 MHz: 1710–1785 MHz (uplink), 1805–1880 MHz (downlink).

    * Podział pasma (Multiple Access):
        * FDMA (Frequency Division Multiple Access): Podział pasma na kanały 
        częstotliwościowe.
        * TDMA (Time Division Multiple Access): Podział każdego kanału na 
        szczeliny czasowe.

    * Przepustowość kanału:
        * 200 kHz (kanał częstotliwościowy).
        * 8 szczelin czasowych na kanał (każda szczelina umożliwia jedno 
        połączenie).

    * Prędkość transmisji danych:
        * Standardowy GSM: Do 9,6 kbps.
        * Rozszerzenia (GPRS/EDGE): Do 384 kbps (EDGE).

    * Zasięg komórki:
        * Od kilkuset metrów (mikrokomórki) do 35 km (makrokomórki).

    * Czas trwania ramki TDMA:
        * 4,615 ms, co odpowiada jednej ramce dla 8 szczelin czasowych.

    * Kodowanie:
        * Wykorzystuje się kodowanie kanałowe dla ochrony przed błędami 
        transmisji.

3. Rodzaje usług GSM

* A. Usługi telekomunikacyjne (Bearer Services):
    * Usługi głosowe: Standardowe połączenia telefoniczne.
    * Usługi danych: Modemowe połączenia z sieciami, takimi jak Internet.
    * Faks: Transmisja faksów przez sieć GSM.

* B. Usługi dodatkowe (Supplementary Services):
    * Przekierowanie połączeń.
    * Trzymanie połączeń w zawieszeniu.
    * Konferencje trójstronne.
    * Ukrywanie numeru (CLIR – Calling Line Identification Restriction).

* C. Usługi wiadomości (Short Message Services, SMS):
    * Wysyłanie i odbieranie wiadomości tekstowych (maks. 160 znaków w jednej 
    wiadomości).
    * Rozszerzone o MMS (Multimedia Messaging Service) w późniejszych wersjach 
    GSM.

* D. Usługi przesyłania pakietów (GPRS/EDGE):
    * Transmisja danych w trybie pakietowym.
    * Wykorzystywana do przeglądania Internetu, poczty elektronicznej itp.
    * EDGE (Enhanced Data Rates for GSM Evolution):
    * Rozszerzenie GPRS, zapewniające wyższe prędkości transmisji danych.

4. Znaczenie systemu GSM
    * Globalny zasięg:
    * Bezpieczeństwo:
        * Zabezpieczenia takie jak autoryzacja, szyfrowanie transmisji 
        chronią dane użytkowników.
    * Elastyczność:
        * Możliwość wdrażania nowych usług, takich jak GPRS czy EDGE, bez 
        konieczności wymiany całej infrastruktury.
    * Efektywność:
        * Dzięki TDMA i FDMA możliwe jest jednoczesne obsługiwanie wielu 
        użytkowników na ograniczonym paśmie częstotliwości.



## Filtry cyfrowe o skończonej i o nieskończonej odpowiedzi impulsowej.

1. Filtry FIR (Finite Impulse Response)
Charakterystyka:
Odpowiedź impulsowa filtra FIR ma skończoną długość. Oznacza to, że po podaniu 
impulsu na wejście, odpowiedź filtra wygasa po określonej liczbie próbek.
Oparte na splotach dyskretnych. Wyjście jest liniową kombinacją bieżących i 
wcześniejszych wartości wejściowych.

Cechy:
* Stabilność:
    * Zawsze stabilne, ponieważ nie zawierają elementów sprzężenia zwrotnego.
* Odpowiedź liniowa w fazie:
    * Mogą być zaprojektowane tak, aby zapewniały liniową charakterystykę fazową 
    (ważne w aplikacjach audio i komunikacyjnych).
* Złożoność obliczeniowa:
    Dłuższe filtry wymagają więcej obliczeń, co zwiększa złożoność.

Zastosowania:
* Filtry dolnoprzepustowe, pasmowe i górnoprzepustowe o liniowej charakterystyce 
fazowej. 
* Aplikacje wymagające wysokiej stabilności, np. w audio czy systemach kontroli.


2. Filtry IIR (Infinite Impulse Response)
Charakterystyka:
Odpowiedź impulsowa filtra IIR jest nieskończona, ponieważ zawiera sprzężenie 
zwrotne. Oznacza to, że po podaniu impulsu na wejście, odpowiedź teoretycznie 
nigdy nie wygasa.
Oparte na równaniach różnicowych z elementami sprzężenia zwrotnego.

Cechy:
* Stabilność:
    * Może być niestabilne, jeśli bieguny funkcji przenoszenia znajdują się poza 
    jednostkowym okręgiem w dziedzinie z.
* Efektywność obliczeniowa:
    * Krótsza odpowiedź impulsowa w porównaniu do FIR dla podobnej 
    charakterystyki częstotliwościowej.
* Charakterystyka fazowa:
    * Zwykle nieliniowa, co może być problematyczne w niektórych aplikacjach.

Zastosowania:
* Filtry o stromych zboczach, np. w telekomunikacji, przetwarzaniu sygnałów 
radarowych. 

---


## Zasada działania i rodzaje sztucznych sieci neuronowych.

### Zasada działania sztucznych sieci neuronowych

1. Neuron sztuczny (podstawowy element):

Neuron jest podstawową jednostką obliczeniową w sieci neuronowej. Działa w kilku krokach:

* Wejście: Przyjmuje zestaw wartości wejściowych, z których każda jest mnożona przez wagę 

* Suma ważona: 
    * Oblicza sumę ważoną wejść, gdzie b to parametr zwany biasem, który 
    przesuwa funkcję aktywacji.

* Funkcja aktywacji:
    * Wynik przechodzi przez funkcję aktywacji, która decyduje, czy neuron 
    zostanie "pobudzony" i jaki sygnał wyśle dalej. Typowe funkcje aktywacji to
        * Sigmoidalna 
        * ReLU 
        * Tanh

2. Warstwy w sieci:

* Warstwa wejściowa: 
    * Otrzymuje dane wejściowe.
* Warstwy ukryte
    * Przetwarzają dane wejściowe, wykonując złożone obliczenia.
* Warstwa wyjściowa
    * Zwraca wynik, np. klasyfikację lub wartość liczbową.

3. Uczenie sieci:

Uczenie sieci polega na dostosowywaniu wag i biasów, aby minimalizować różnicę 
między wynikami sieci a oczekiwanymi wynikami. Proces ten obejmuje:

* Funkcję kosztu
    * Określa różnicę między wynikiem sieci a rzeczywistą wartością (np. 
    funkcja błędu średniokwadratowego, funkcja entropii krzyżowej).
* Optymalizację 
    * Algorytmy takie jak backpropagation i gradient descent są używane 
    do minimalizowania funkcji kosztu przez aktualizację wag.


4. Sieci rekurencyjne (Recurrent Neural Networks, RNN):

Potrafią przetwarzać dane sekwencyjne, np. teksty, dźwięk, dane czasowe.
* Cechy: 
    * Wykorzystują mechanizmy pamięci do uwzględniania wcześniejszych elementów 
    sekwencji.
* Zastosowania
    * Przetwarzanie języka naturalnego (NLP), analiza danych czasowych, 
    tłumaczenie maszynowe.

6. Sieci generatywne (Generative Adversarial Networks, GAN):

Składają się z dwóch sieci:

* Generator: Tworzy dane.
* Dyskryminator: Rozróżnia dane prawdziwe od wygenerowanych.

Zastosowania: 
* Tworzenie obrazów, deepfake, generowanie danych.
