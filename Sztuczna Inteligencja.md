𝕶𝖔𝖗𝖇𝖎𝖙𝖈𝖍
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

