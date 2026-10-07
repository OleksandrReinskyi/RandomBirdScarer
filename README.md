
# Autonomiczny Stochastyczny Odstraszacz Ptaków

## 1. Założenia i Architektura Systemu

**Cel:** Urządzenie zostało zaprojektowane do ochrony upraw w sadach orzechowych przed ptakami. Konstrukcja eliminuje zjawisko przyzwyczajania się szkodników do powtarzalnego dźwięku dzięki zastosowaniu losowości.

System składa się z trzech głównych modułów:
1. **Moduł zasilania:** Pakiet 3 ogniw Li-Ion 3.7V
2. **Płytka stochastycznego kontrolera:** Układ analogowo-cyfrowy generujący losowe interwały załączania płytki generatora dźwięku.
3. **Płytka generatora dźwięku:** Układ wytwarzający falę prostokątną o częstotliwości 2,1–2,9 kHz na glośniku

![Schemat blokowy systemu](docs/BlockDiagram.png)

W tym repozytorium znajduje się projekt schematu ideowego, obwodu drukowanego (KiCad) oraz dokumentacja płytki stochastycznego kontrolera.

---

### Zasada działania sterownika:

1. **Źródło losowości:** Dioda Zenera pracująca w stanie przebicia lawinowego generuje analogowy szum biały.
2. **Wzmocnienie i formowanie impulsów:** Niewielkie fluktuacje szumu są wzmacniane przez wzmacniacz operacyjny TL072 (wzmocnienie $A_u \approx 511$), a następnie przekształcane przez komparator LM393 na  ciąg impulsów, podawany na wejście danych $D$ przerzutnika typu D (HEF4013B).
3. **Baza czasowa:**
   * **Timer 1:** Generuje krótkie impulsy co 5 minut.
   * **Timer 2:** Odpowiada za taktowanie krótkich cykli dźwięku (co ok. 5–10 sekund)
4. **Próbkowanie (Bramka OR + CLK):** Przebiegi z obu timerów są podawane przez diodową bramkę logiczną OR na wejście zegarowe $CLK$ przerzutnika.
5. **Pętla decyzyjna:** Wyjście proste $Q$ steruje wejściem zerowania ($RESET$) Timera 2, decydując o zakończeniu lub wydłużeniu cyklu odstraszania.
6. **Stopień mocy:** Wyjście zanegowane $\overline{Q}$ steruje bramką tranzystora P-MOSFET, który załącza napięcie zasilania dla płytki generacji dźwięku.

**Efekt końcowy:** Urządzenie załącza się w nieprzewidywalnych odstępach czasu będących losową wielokrotnością 5 minut (np. 5, 10, 15 min...) na losowy czas trwania będący wielokrotnością 10 sekund (np. 10, 20, 30 s...), co redukuję adaptację ptaków do sygnału.

---

## 2. Realizacja Sprzętowa i Weryfikacja

### Wyniki symulacji (LTspice)
![Symulacja układu w LTspice](docs/Simulation.png)

### Obudowa (FreeCAD)
Obudowa przystosowana do druku 3D z komorą na ogniwa oraz uchwytami montażowymi na drzewa:
![Projekt obudowy w FreeCAD](docs/FreeCAD.png)

### Zmontowany prototyp
![Zmontowane urządzenie](docs/Prototype.png)

### Demonstracja wideo
*(Tutaj wstaw link do YouTube/wideo lub plik GIF prezentujący działanie prototypu)*

| ![](docs/1.png) | ![](docs/2.png) |
|--|--|
|![](docs/3.png)  | ![](docs/4.png) |

