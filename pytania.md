# **Pytania kierunkowe**
## 1. Widmo sygnału analogowego (podstawowo-pasmowego i pasmowego) a twierdzenie o próbkowaniu.
Widmo sygnału jest to reprezentacja sygnału w dziedzinie częstotliwości, wyznaczana najczęściej z transformacji Fouriera. Aby sygnał był użyteczny w technice cyfrowj musi zostać zdyskretyzowany, a więc konieczne jest jego spróbkowanie oraz kwantyzacja, a widmo wyznacza się wtedy z DFT (w praktyce FFT).

Próbkowanie jest procesem konwersji sygnału analogowego (o czasie ciągłym) do postaci próbek pobieranych w rónomiernych odstępach czasu (zwanych okresem próbkowania T).

Twierdzenie Nyquista o próbkowaniu sygnału mówi nam, że jeżeli sygnał analogowy x<sub>a</sub>(t) jest ograniczony pasmowo (ma ograniczoną pasmowo transformatę Fouriera) to sygnał może być bezbłędnie i jednoznacznie zrekonstruowany na podstawie ciągu równomiernie rozłożonych próbek:

<div style="text-align: center;"> x[n]=x<sub>a</sub>(*n*T<sub>S</sub>), *n*∈I </div>
jeżeli:
<div style="text-align: center;">F<sub>S</sub>=1/T<sub>S</sub>≥2F<sub>max</sub> </div>
F<sub>S</sub> - częstotliwość próbkowania,

F<sub>max</sub> - częstotliwość górna sygnału,

Częstotliwość Nyquista - połowa F<sub>S</sub>


Z właściwości transformaty Fouriera wiadomo, że widmo sygnału dyskretnego jest okresowe (co f<sub>s</sub> się powtarza). A więc jeżeli się próbkuje sygnał z częstotliwocią niższą od częstotliwości Nyquista zajdzie zjawisko aliasingu i wynikowo widma zaczną na siebie zachodzić.

Sygnał analogowy podstawowo-pasmowy jest sygnałem ograniczonym pasmowo o widmie ulokowanym wokół częstotliwości zerowej. Widmo w funkcji częstotliwości:
![obrazek](1.1.PNG)

A więc żeby spróbkować sygnał podstawowo-pasmowy wystarczy zastosować twierdzenie Nyquista o próbkowaniu sygnałów.

Sygnał pasmowy jest to sygnał o ograniczonym widmie ulokowanym wokół częstotliwości +f.
Widmo w funkcji częstotliwości:
![obrazek](1.2.PNG)

Zastosowania twierdzenia Nyquista o próbkowaniu sygnałów dla tego sygnału jest nieefektywne. W przypadku takich sygnałów możliwe jest takie dobranie szybkości próbkowania mniejszej od szybkości Nyquista, które zapewnia zachowanie nie zniekształconego widma sygnału przesuniętego jedynie w dziedzinie częstotliwości i w niektórych przypadkach widmie odwróconym w częstotliwości. Wynika to z faktu, że podczas podpróbkowania zachodzi zjawisko aliasingu, czyli sygnały "podszywają się" pod sygnały o innych częstotliwościach. Takie próbkowanie sygnału nazywa się podpróbkowaniem.

Różnica względem twierdzenia o próbkowaniu Nyquista jest taka, że:
<div style="text-align: center;"> F<sub>S</sub>>2B </div>
B - pasmo sygnału

Dodatkowo F<sub>S</sub> nie może być dowolne, występują dopuszczalne pasma próbkowania. W wyniku podpróbkowania w dopuszczalnych pasmach próbkowania uzyskuje się widmo odwrócone w częstotliwości bądź widmo bez odwrócenia. Jeśli do podpróbkowania zostanie wybrana częstotliwość spoza dopuszczalnego pasma to zajdzie zachodzeni się na siebie widm sygnału.

Jak dobrać F<sub>S</sub> nie znając wzorów, które wyznaczają dopuszczalne pasma próbkowania:
    Jeżeli pasmo B mieści się całkowitą ilość razy w częstotliwości f<sub>H</sub> (iloraz f<sub>H</sub>/B jest liczbą naturalną), to minimalną szybkością próbkowania przy której nie zajdą zniekształcenia jest f<sub>S</sub>=2B

Jeżeli jednak pasmo B nie mieści się całkowitą liczbę razy w f<sub>H</sub> (iloraz f<sub>H</sub>/B nie jest liczbą naturalną), to wartość B należy zwiększyć do takiej najbliższej wartości B', która mieści się całkowitą ilość razy w f<sub>H</sub>. Wtedy minimalną szybkością próbkowania, przy której nie zajdą zniekształcenia aliasowe to f<sub>S</sub>=2B'. W ten sposób "ogony" replik nie tylko nie nachodzą na siebie, ale istnieje również zapas równy 2(B'-B).

## 2. Widmo sygnału dyskretnego i transformacje (DTFT, DFT, FFT) służące do obliczania tego widma oraz powiązania tych transformat.
## 3. Twierdzenia Schannona i ich interpretacje.
## 4. Usługi w sieci telekomunikacyjnej - klasyfikacja, charakterystyki, jakość usług.
## 5. Narysuj schemat blokowy i omów działanie łącza radiowego.
## 6. Omów podstawowe parametry elektryczne anteny.
## 7. Budowa i właściwości wzmacniaczy tranzystorowych.
## 8. Porównanie budowy, właściwości i zastosowań układów FPGA, CPLD.
## 9. Omów relacyjny model danych.
## 10. Wymień interfejsy przewodowe stosowane w systemach czujnikowych i omów jeden szczegółowo.
## 11. Zasada działania, właściwości i zastosowania wybranych elementów systemu optoelektronicznego (źródła, modulatory, detektory).
## 12. Architektury procesorów rdzeniowych mikrokontrolerów.
## 13. W jaki sposób można zrealizować w zakresie b. w. cz. czystą reaktancję?
## 14. Do czego służy strojnik pojedynczy i jaka jest jego zasada działania?
## 15. Omów ramy stosowania rachunku wskazów w analizie obwodów i niekonkurencyjności rachunku Laplace'a w tych ramach.
## 16. Sformułuj i zapisz w postaci ogólnej prawa Kirchoffa oraz podaj własne przykłady ilustrujące treść tych praw.

# **Pytania dla Telekomunikacji**
## 1. Omów problem analizy i syntezy zasobów w sieci telekomunikacyjnej.
## 2. Scharakteryzuj architektury wspierające realizację sieci IP QoS.
## 3. Przedstaw bilands energetyczny i scharakteryzuj jego znaczenie przy projektowaniu łącza radiowego.
## 4. System komórkowy GSM, architektura, podstawowe parametry i rodzaje usług.
## 5. Filtry cyfrowe o skończonej i o nieskończonej odpowiedzi impulsowej.
## 6. Zasada działania i rodzaje sztucznych sieci neuronowych.
## 7. Przedstaw zasadę pracy systemów echolokacyjnych i zdefiniuj ich podstawowe parametry eksploatacyjne.
## 8. Omów budowę, właściwości i zastosowania wielowiązkowych systemów echolokacyjnych.

# **Pytania dla Systemów Wbudowanych Czasu Rzeczywistego**
## 1. Wymień 3 główne typy silników krokowych i scharakteryzuj jeden z nich.
## 2. Wymień i scharakteryzuj elementy urządzenia wykonawczego.
## 3. Opisz cechy szczególne wyróżniające procesory sygnałowe.
## 4. Opisz typy systemów czasu rzeczywistego.
## 5. Wyjaśnij pojęcie systemu wbudowanego (ang. embedded system).
## 6. Narażenia zagrażające aparaturze z komputerami wbudowanymi - rodzaje, główne źródła, sposoby przeciwdziałania.
## 7. Zasady rozprowadzania zasilania obwodów w aparaturze z komputerami wbudowanymi - odsprzęganie, filtracja zakłóceń.
## 8. Automatyczne regulacje w układach z otoczenia komputerów wbudowanych - rodzaje, cele stosowania, sposoby realizacji.
## 9. Funkcje elementów systemu operacyjnego Linux dla systemu wbudowanego: toolchain, bootloader, jądro, system plików.
## 10. Opisz metory pomiarowe stosowane w radarze meteorologicznym.