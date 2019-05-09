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
