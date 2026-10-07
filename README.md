
# Autonomiczny Stochastyczny Odstraszacz Ptaków

## 1. Zalozenia i Architektura Systemu

**Cel**: Urządzenie zostało zaprojektowane w celu odstraszania ptaków w sadach orzechowych. Składa się z 3 części: 3 ogniw LiIon, płytki stochastycznego sterowania sygnałem oraz płytki do generacji dźwięku określonej częstotliwości. 

![](docs/BlockDiagram.png)

W danym folderze GitHub mieści się projekt płytki stochastycznego sterowania oraz jej opis.

Metoda pracy:

1.   Dioda Zenera pracująca w stanie przebicia lawinowego wytwarza analogowy szum biały o losowych wahaniach napięcia.   
2.  Sygnał szumu jest wzmacniany przez wzmacniacz operacyjny TL072 i przekształcany przez komparator LM393 na ciąg logicznych impulsów, trafiających na wejście danych $D$ przerzutnika HEF4013B.
3. Timer 1 generuje krótkie impulsy co 5 minut.
Timer 2  generuje krótkie impulsy co 5 secund.
4. Oba przebiegi są sumowane bramką diodową OR i podawane na wejście zegarowe $CLK$ przerzutnika.
5. Wyjście proste $Q$ steruje wejściem resetującym Timera 2. 
 6. Wyjście zanegowane $\overline{Q}$ steruje bramką tranzystora P-MOSFET, który steruje zasilaniem płytki generacji dzwięku.
 
Jako efekt cykl pracy charakteryzuje sie losowym zalaczaniem w odstepach bedacych wielokrotnoscia 5 minut (np. 5, 10, 15 min) na czas trwania bedacy wielokrotnoscia 10 sekund (10, 20, 30 s).


# 2. Realizacja

Rezultat symulacji w LTSPICE: ![](docs/Simulation.png)

Projekt obudowy w FreeCAD: ![](docs/FreeCAD.png)

Zdjęcia:![](docs/BlocDiagram.png) 

Demonstracja:

