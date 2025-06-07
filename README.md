# Program Komnum
Nama: Azmii Maulawiy Said  
NRP: 5053241024  
Kelompok: R10    
## Newton's Divided Difference Interpolation

Implementasi metode **Newton Interpolation** menggunakan bahasa Python untuk menghitung nilai estimasi dari sebuah fungsi berdasarkan titik-titik data yang sudah diketahui.

## Cara Kerja

Program ini menggunakan **Newton’s Divided Difference Method**, yang membangun sebuah polinomial untuk memperkirakan nilai suatu fungsi di antara titik-titik yang diketahui.

## Struktur Kelas

### `class NewtonInterpolation`

Kelas ini berfungsi untuk:
- Menyimpan titik data `x` dan `f(x)`
- Membangun tabel divided difference
- Menghitung nilai estimasi fungsi menggunakan Newton Polynomial

### Konstruktor
```python
def __init__(self, x, fx)
```

### Method Calculate(target_x)
Fungsi ini digunakan untuk menghitung nilai pendekatan dari fungsi di titik `target_x` menggunakan polinomial Newton hingga orde ke-3.

```python
def Calculate(self, target_x):
        self.__FirstOrde()
        self.__SecondOrde()
        self.__ThirdOrde()

        x0 = self.x[0]
        x1 = self.x[1]
        x2 = self.x[2]

        b0 = self.divided_diff[0][0]
        b1 = self.divided_diff[0][1]
        b2 = self.divided_diff[0][2]
        b3 = self.divided_diff[0][3]

        result = b0
        result += b1 * (target_x - x0)
        result += b2 * (target_x - x0) * (target_x - x1)
        result += b3 * (target_x - x0) * (target_x - x1) * (target_x - x2)

        return round(result, 2)
```
**Langkah-Langkah:**  
1. Memanggil method `__FirstOrde()` untuk mencari orde 1, `__SecondOrde()` untul mencari orde 2, dan `__ThirdOrde()` untu mencari orde 3.
2. Mengambil koefisien `x0`, `x1`, dan `x2` dari array `x`.
3. Lalu mengambil koefisien `b0`, `b1`, `b2`, dan `b3` dari array `divided_diff`.
4. Menghitung hasil menggunakan rumus Interpolasi Newton:
   ``` text
   P(x) = b0 + b1(x−x0) + b2(x−x0)(x−x1) + b3(x−x0)(x−x1)(x−x2)
5. Mengembalikan hasil yang sudah dibulatkan ke dua desimal.  

### Method __FirstOrde()
Menghitung pembagi selisih orde pertama (linear divided difference).  
``` python
def __FirstOrde(self):
        print("Orde 1:")
        for i in range(self.n - 1):
            self.divided_diff[i][1] = round(((self.divided_diff[i + 1][0] - self.divided_diff[i][0]) / (self.x[i + 1] - self.x[i])), 2)
            print(f"F[X{i + 1}, X{i}]: {self.divided_diff[i][1]:.2f}")
        print()
```
- Disimpan di kolom pertama tabel `divided_diff`
- Hasilnya dicetak ke konsol

### Method __SecondOrde()
Menghitung pembagi selisih orde kedua (quadratic divided difference).
``` python
def __SecondOrde(self):
        print("Orde 2:")
        for i in range(self.n - 2):
            self.divided_diff[i][2] = round(((self.divided_diff[i + 1][1] - self.divided_diff[i][1]) / (self.x[i + 2] - self.x[i])), 2)
            print(f"F[X{i + 2}, X{i + 1}, X{i}]: {self.divided_diff[i][2]:.2f}")
        print()
```
- Disimpan di kolom kedua dari tabel `divided_diff`
- Hasilnya dicetak ke konsol

### Method __ThirdOrde()
Menghitung pembagi selisih orde ketiga.
```python
def __ThirdOrde(self):
        print("Orde 3:")
        for i in range(self.n - 3):
            self.divided_diff[i][3] = round(((self.divided_diff[i + 1][2] - self.divided_diff[i][2]) / (self.x[i + 3] - self.x[i])), 2)
            print(f"F[X{i+3}, X{i+2}, X{i+1}, X{i}]: {self.divided_diff[i][3]:.2f}")
        print()
```
- Disimpan di kolom ketiga dari tabel `divided_diff`
- Hasilnya dicetak ke konsol
