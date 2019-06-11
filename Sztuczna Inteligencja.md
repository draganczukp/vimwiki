# Egzamin
25 czerwca (wtorek) 10:00 115 A-2\
4 września (środa) 10:00 115 A-2

# 𝕶𝖔𝖗𝖇𝖎𝖙𝖈𝖍
# Przykłady użycia
## Sprawdzanie parzystości
### Dane wejściowe
$\vec{u}$ - $n$-elementowy wektor składający się z 0 i 1
### Dane wyjściowe
$1$, jeśli liczba jedynek jest nieparzysta,\
$0$ w przeciwnym przypadku
### Struktura sieci
Dwuwarstwowa sieć jednokierunkowa z $n$ wejść i jednym wyjściu
### Zbiór danych uczących
Udowodniono, że dla wektora o rozmiarze $n$ składającego się z $0$ i $1$ wystarczy zbiór danych
uczących o wielkości $2^n$.

$
{u,z} = \begin{bmatrix}
1 & 0 &0&0&|1\\
1&1&0&0&|0\\
0&1&1&1&|1\\
\vdots&\vdots&\vdots&\vdots&\vdots
\end{bmatrix}
$

## Kompresja
Zadanie kompresji danych polega na zmniejszeniu ilości informacji przechowywanych lub
transmitowanych przy zachowaniu możliwości jej pełnego odtworzenia (dekompresji). Mamy kompresję
stratną i bez stratną. Przykładem kompresji bez stratnej może być drzewo Huffmana
### Dane wejściowe
$n$-elementowy wektor $\vec{u}$
### Dane wyjściowe
$n$-elementowy wektor $\vec{y}$
### Struktura sieci
Trójwarstwowa sieć jednokierunkowa

$i=1,2,...,n$ - Indeksy wejściowe\
$j=1,2,...,n$ - Indeksy wyjściowe\
$k=1,2,...,q; q \leq n$ - Indeksy warstwy ukrytej

### Zestaw uczący
$\{\vec{u}^\mu,\vec{u}^\mu\}, \mu=1,2...P$

Na etapie uczenia metodą propagacji wstecznej wyznaczane są wartości wag $w_{ik}$ oraz ${v_kj}$ że
sieć taka po nauczeniu może być rozdzielona na dwie części, lewa to kompresor, a prawa to
dekompresor. Tak zrealizowana kompresja danych jest kompresją stratną, gdyż algorytm uczenia
(propagacja wsteczna) nie daje możliwości zakończenia procesu uczenia w skończonym czasie z
błędem zerowym.

## Zastosowanie sieci neuronowej do wyznaczenia macierzy odwrotnej
Załóżmy, że jest dana macierz kwadratowa $A$ rzędu $n$ ($dim A=(n\times n)$). Należy zaprojektować
sieć neuronową obliczającą macierz odwrotną $B = A^{-1}$.\
$B*A=I$

Załóżmy, że mamy wektor $\vec{x}=[x_1, x_2, ..., x_n]$

$B*A=I/*x$

$BAx=x \Rightarrow BAx-x=0$

$E=\frac{1}{2} ||BAx-x||^2_2$

$||x||_2 = \sqrt{\displaystyle\sum_{i=1}^nx_i^2}$

Zauważmy, że wektor $\vec{x}$ pełni podwójną rolę. Jest wektorem uczącym, czyli wejściem do
sieci. Pełni też rolę wektora zadanego.

### Zestaw uczący
$\{x^\mu,x^\mu\}, \mu=1,2...P$

# Jakieś zadanie
$f_0$ - stan normalny\
$f_1$ - pęknięcie\
$f_2$ - uszkodzenie pompy\
$f_3$ - zarastanie

Sygnały wejściowe:
${P,T,Q}$

Wyjścia:
$f_0,f_1,f_2,f_3$ o wartości $0$ lub $1$\
$1$ - poprawne\
$0$ - niepoprawne

```
graph LR;
P-->net["Sieć neuronowa"]
T-->net
Q-->net
net-->f_0
net-->f_1
net-->f_2
net-->f_3
```
## Struktura sieci
3 warstwowa
## Zestaw uczący
$
f_0= \begin{Bmatrix}
100& 70& 200 &|1\\
95& 78& 250 &|1\\
\vdots &&&|1\\
93& 71& 210 &|1
\end{Bmatrix}
$

$
f_1=\begin{Bmatrix}
70&40&300&|1 \\
20&45&200&|1\\
\cdots&&&|1
\end{Bmatrix}
$

$f_3=\begin{Bmatrix}
\cdots
\end{Bmatrix}
$

$f_4=\begin{Bmatrix}
\cdots
\end{Bmatrix}
$

# Logika rozmyta i zastosowania
| logika klasyczna                 | logika rozmyta         |
| -                                | -                      |
| Coś albo jest w zbiorze albo nie | Może należeć częściowo |

## Zastosowanie logiki rozmytej w diagnostyce obiektów technicznych

```
graph LR;
u-->obiekt
u-->model
obiekt-->|y|o(( ))
model-->|y_u|o
o-->w[r=y-y_u]
```
$r$- sygnał residuum

$r = \begin{cases}
1 \text{ - gdy nie przekroczony} \\
0 \text{ - gdy przekroczony}
\end{cases}$

### Rozmyta ocena wartości residuum
Każdemu residuum $N$ przyporządkować można zmienną opisującą wyniki testu. W najgorszym przypadku
zbiór posiada 2 wyniki, pozytywny i negatywny. 

### Reguły wnioskowania rozmytego
$R_0$ Jeżeli $S_1=P$ i $S_j=P$ to wszystko jest OK\
$R_k$ Jeżeli $S_1 = N$ i $S_j = P$ to np. Uszkodzenie $f_k$

### Rozmyte wnioskowanie
Analiza zestawu reguł

#### Rozmyta struktura diagnostyki
```
graph LR;
residuum==>rozm[Blok rozmywania]
rozm==>wn[Blok wnioskowania]
wn==>diagnoza
```
$\{f_1, 0.8\}$ lub $\{f_3, 0.3\}$\
$\{f_0, 1\}$

## Struktura układu sterowania rozmytego

```
graph LR;
a>"Sygnał rzeczywisty"]==>rozm[Blok rozmywania]
rozm==>bp[Blok przetwarzania]
bp==>bw[Blok wyostrzania]
bw==>s>Sterowanie]
```

# Sieci neuronowe
## Nauczanie be nauczyciela (nienadzorowane)

```
graph LR;
u1-->sn
u2-->sn
un-->sn
sn-->y1
sn-->y2
sn-->yn
```
#### Zestaw uczący
$\{u^\mu\}$

Dotychczas przyjmowano, że cel uczenia był określony i nauczanie sieci sprowadzało się do realizacji
tego celu. W nauczaniu bez nauczyciela (nienadzorowanym) kategorie celu są rozwijane przez sieć.
Taki sposób nauczania rozszerza możliwości sztucznych sieci neuronowych do zadań rozpoznawania
obrazów, kiedy klasyfikacje celu są nieznane

## Nauczanie konkursowe - model Rumelharta-Zipsera (model R-Z)
Model R-Z jest siecią klasyfikującą obrazy z jedną warstwą neuronów przetwarzających, które
konkurują każdy z każdym. Dla sieci pokazywany jest zbiór obrazów uczących, ale nie ma podanego celu
dla tych obrazów wyjściowych. Sieć taka organizuje obrazy uczące w zbiory klas samodzielnie. Model
R-Z jest prostym schematem i ma małe praktyczne zastosowanie, ale ma zalety pozwalające na
ilustracje wybranych głównych cech nauczania konkursowego

```
graph LR;
u1-->j1((j1))
u1-->j2
u1-->jn
u2-->j1
u2-->j2((j2))
u2-->jn
un-->j1
un-->j2
un-->jn((jn))
j1-->y1
j2-->y2
jn-->yn

```
### Uwagi
1. Warstwy wejściowe i konkursowe są całkowicie połączone (każdy $i$ty węzeł jest połączony z każdym
$j$tym węzłem)
2. Wagi $W_{i,j}$ posiadają ograniczone wartości $[0,1]$ a ich suma jest równa 1, $0 < W_{ij} < 1,
   \displaystyle\sum_{i=1}^{m}w_{ij} =1$
3. Używa się kwantowania sygnałów wejściowych i wyjściowych

### Zestaw uczący
$\{u^\mu\}, \mu = 1,2,...,P$

### Algorytm uczenia
1. Eksperyment: podaj obraz z zestawu uczącego $u^\mu$ i wyznacz potencjał membranowy dla
   poszczególnych wyjść. $\phi_j=\displaystyle\sum_{i=1}^m w_{ij} u_i$
2. Analiza: polega na przyjęciu algorytmu/pojęcia "zwycięzca bierze wszystko". W danym przypadku
   zasada ta pozwala na wyznaczenie zwycięzcy $\phi_j^z$, który posiada największą wartość
   potencjału
3. Konsumpcja zwycięstwa. Zwycięzcy przydzielane jest wyjście $+1$, a pozostałym $0$. Po określeniu
   zwycięzcy wagi połączeń łączących węzeł zwycięzcy są uaktualniane według algorytmu:
$\Delta_{ij}^\mu = \alpha(\frac{u_i^\mu}{q}-W_{ij}) = \alpha q^{-1}u_i^\mu - \alpha W_{ij}$\
Gdzie:\
$\alpha$- $(0<\alpha\leq1), \alpha=0.01 - 0.3$\
$q$- liczba węzłów w warstwie wejściowej, które posiadają wartości $+1$

Aby reguła była spełniona, należy sprawdzić warunek\
$\displaystyle\sum_{i=1}^m\Delta W_{ij} = \alpha q^{-1}\displaystyle\sum_i^\mu u_i^\mu -
\alpha\displaystyle\sum_{i-1}^\mu W_{ij} = 0$

## Przykład
### Struktura
3 wejścia $(u_1, u_2, u_3$), 2 wyjścia ($A, B$)
### Obrazy uczące
$u^1 = (1 0 1)P_1$\
$u^2 = (1 0 0)P_2$\
$u^3 = (0 1 0)P_3$\
$u^4 = (0 1 1)P_4$

### Wyniki
W wyniku uzyskujemy:\
$P_1(101) \rightarrow A$\
$P_2(100) \rightarrow A$\
$P_3(010) \rightarrow B$\
$P_3(011) \rightarrow B$

|       | $P_1$ | $P_2$ | $P_3$ | $P_4$ |
| -     | -     | -     | -     | -     |
| $P_1$ |  0    |   1   |   3   |  2    |
| $P_2$ |   1   |  0    |   2   |  3    |
| $P_3$ |   3   |   2   |     0 |  1    |
| $P_4$ |   2   |   3   |    1  |  0    |

## Sieci ze współzawodnictwem poprzez eliminacje
Dotychczas węzeł zwycięzca w modelu R-Z był określany poprzez wybór zewnętrzny, to jest węzeł z
największym potencjałem membranowym $\phi_j$. Alternatywną procedurą jest procedura zezwalająca na
eliminacje jednego przez drugiego, czyli w danym przypadku zwycięzcą jest węzeł który wyeliminował
wszystkie pozostałe, lecz sam pozostaje aktywny.

# Sieć Kohonena
Sieć konkursowa, która organizuje topologiczne odwzorowanie pokazujące rzeczywiste związki pomiędzy
obrazami prezentowanymi jako wejścia do sieci
## Uwagi
Sygnały wejściowe $u_i$ mają wartości ciągłe z przedziału $[0-1]$
## Algorytm działania sieci
1. Wyznaczyć dobre $\vec{u}$ - Eksperyment
2. Obliczyć odległość pomiędzy obrazem wejściowym a wagami  
   $d_i=\sqrt{\displaystyle\sum_j(u_i-w_{ij})^2}$
3. Wybór zwycięzcy dla którego $d_i$ jest najmniejsze
4. Wybierz sąsiedztwo otaczające węzeł zwycięzcy  
	$n_c$- zbiór węzłów w sąsiedztwie zwycięzcy
5. Uaktualnić wszystkie wagi w sąsiedztwie zwycięzcy $c(w_{ij})$  
   $\Delta w_{ij}^c = \alpha (u_i - w_{ij}^c)$  
   $w_{ij} = w_{ij}+\Delta w_{ij}^c$  
   $0.2 < \alpha < 0.5$  
Z podanej reguły uczenia wynika, że wagi $w_{ij}$ w otoczeniu zwycięzcy są modyfikowane w taki
sposób, aby ich wartości zbliżały się do wartości obrazu wejściowego. Zwycięzca $c$, który
najbardziej prawdopodobnie może zwyciężyć współzawodnictwo powinien obrazy podobne do $u_i$ mieć w
pewnej sekwencji
6. Iteracyjne obliczanie współczynnika $\alpha$

$
\alpha = \alpha_0 (0.2-0.5)\\
\alpha_t = \alpha_0(1-\frac{t}{T})
$  

Gdzie  $t$ - bieżący krok, $T$ - ogólna liczba kroków
7. Analiza rozmiaru sąsiedztwa $n_c$, na początku powinno być duże, a w procesie uczenia
   iteracyjnie pomniejszane  

## Algorytm uogólniony
1. Wyznaczyć zwycięzce i jego sąsiadów
2. Korekta wag, aby poprawić dopasowanie wag do obrazu
3. Korekta (stopniowe zmniejszanie) współczynnika $\alpha$ i rozmiaru sąsiedztwa

## Przykład
Zbiór danych z dwoma atrybutami: wiek i dochód (znormalizowane). Należy użyć sieci Kohonena o
rozmiarach $2\times2$, aby odkryć ukryte grupy w zbiorze danych

### Dane
$\{\vec{u}^\mu\}=$
| lp. | wiek           | dochód          | opis                           |
| -   | -              | -               | -                              |
| 1   | $u_{11} = 0.8$ | $u_{1,2} = 0.8$ | Osoby starsze z dużym dochodem |
| 2   | $u_{21} = 0.8$ | $u_{2,2} = 0.1$ | Osoby starsze z małym dochodem |
| 3   | $u_{31} = 0.2$ | $u_{3,2} = 0.9$ | Osoby młodsze z dużym dochodem |
| 4   | $u_{41} = 0.1$ | $u_{4,2} = 0.1$ | Osoby młodsze z małym dochodem |

### Sieć
4 neurony wyjściowe $1,2,3,4$, 2 wejściowe $\{\text{wiek}, \text{dochód}\}$\
Ze względu na mały rozmiar sieci, można przyjąć promień sąsiedztwa $0$\
$\alpha=0.5$

#### Wagi
$
w_{11}=0.9,
w_{21}=0.8,
w_{12}=0.9,
w_{22}=0.2,\\
w_{13}=0.1,
w_{23}=0.8,
w_{14}=0.1,
w_{24}=0.2
$
### Uczenie
1. Obraz wejściowy nr. 1 $u_1=(0.8, 0.8)$

## Przykład zastosowania sieci Kohonena do budowy klasyfikatora uszkodzeń rurociągu przesyłu medium
### Wejścia:
$p,q,T,V$
### Scenariusze (wyjścia)
- $f_0$ - stan prawidłowy
- $f_1$ - pęknięcie
- $f_2$ - zarastanie
- $f_3$ - inne

### Zbiór uczący
$\{\vec{u}\}, \vec{u} = [p,q,T,v]^T$  
$\{\vec{u^\mu}\}, \mu = 1,2,3...$

$\vec{u}^{f_0}= \begin{bmatrix}
200&150&30&20\\
\vdots & \vdots & \vdots &\vdots
\end{bmatrix}$
