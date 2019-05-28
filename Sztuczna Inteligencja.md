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
