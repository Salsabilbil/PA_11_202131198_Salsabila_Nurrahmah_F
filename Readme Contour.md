
# Contour Image

## Materi Terkait: 
### - Deteksi Tepi Tujuan 
Operasi deteksi tepi adalah meningkatkan penampakan garis batas suatu daerah atau objek  di  dalam  citra. Operator gradien pertama yang digunakan untuk mendeteksi tepi di dalam citra, yaitu operator gradien selisih terpusat, operator Sobel, operator Prewitt,  operator Roberts operator Canny(Munir, 2004). 

### - Ekstrasi Kontur
Menurut pedro dalam jurnal a computational geometry of contour extractionpada  tahun  2009,  kontur  adalah garis batas dari bentuk geometris dalam gambar digital. Algoritma ekstrasi kontur tahapan pertama adalah preprocessinguntuk mengestrak satu set point berorientasi dari input gambar. Tahap kedua menentukan kontur diantara    titik yang berorientasi menggunakan geometri.(Tejada, 2009).

### - Kontur
• Pendeteksi tepi menghasilkan citra tepi yang berupa citra biner

• Pixel-pixel tepi berwarna putih, sedangkan pixel bukan-tepi berwarna hitam.

• Rangkaian pixel-pixel tepi yang membentuk batas daerah (region
boundary) disebut kontur

• Kontur dapat terbuka atau tertutup

• Kontur tertutup berkoresponden dengan batas yang mengelililingi suatu daerah (region).

• Pixel-pixel di dalam daerah tertutup dapat ditemukan dengan algoritma pengisian (filling algorithm).

• Batas daerah berguna untuk mendeskripsikan bentuk objek dalam tahap analisis citra (misalnya untuk mengenali objek).

• Kontur terbuka dapat berupa fragmen garis atau bagian dari batas daerah yang tidak membentuk sirkuit

### - Representasi Kontur
• Representasi kontur dapat berupa senarai tepi (edge list) atau berupa kurva.

• Senarai tepi merupakan himpunan terurut pixel-pixel tepi.

• Representasi kontur ke dalam kurva merupakan representasi dalam bentuk persamaan. Misalnya, rangkaian pixel tepi yang membentuk garis dapat
direpresentasikan hanya dengan sebuah persamaan garis lurus.

• Representasi semacam ini menyederhanakan perhitungan selanjutnya seperti arah dan panjang garis

### - Kode Rantai
• Kode rantai (chain code)adalah notasi untuk mengkodekan senarai tepi yang membentuk batas daerah.

• Kode rantai menspesifikasikan arah setiap pixel tepi di dalam senarai tepi. Arah yang digunakan adalah 4 arah mata angin atau 8 arah mata angin.

• Dimulai dari sebuah pixel tepi dan searah jarum jam, arah setiap pixel tepi yang membentuk batas objek dikodekan dengan salah satu dari empat atau delapan kode rantai.

• Kode rantai merepresentasikan batas objek dengan koordinat pixel tepi pertama
lalu diikuti dengan senarai kode rantai

### - Transformasi Hough
• Kurva yang merepresentasikan kontur dicari dengan teknik pencocokan kurva (curve fitting).

• Ada dua macam teknik pencocakan kurva: interpolasi dan penghampiran (approximation).

• Interpolasi kurva adalah mencari kurva yang melalui semua pixel tepi.

• Penghampiran kurva dengan mencari kurva yang paling dekat melalui pixel-pixel tepi, tetapi tidak perlu melalui semua pixel tersebut.

• Transformasi Hough adalah teknik untuk menghampiri kurva parameterik (garis, lingkaran, elips, dll).

• Transformasi Hough menspesifikasikan kurva dalam bentuk parametrik. Kurva dinyatakan sebagai bentuk parametrik (x(u), y(u)) dari parameter u.

• Transformasi Hough menggunakan mekanisme voting untuk mengestimasi nilai parameter.

• Setiap titik di kurva menyumbang suara untuk beberapa kombinasi parameter. Parameter yang memperoleh suara terbanyak terpilih sebagai pemenang

## Penjelasan Progam
### - [ln 1] Import Library
Berikut ini penjelasan library yang digunakan :
- 'os' adalah library untuk melakukan operasi terkait sistem operasi, seperti mengakses file dan direktori.
- 'cv2' adalah library OpenCV (Open Source Computer Vision) yang digunakan untuk pemrosesan gambar dan komputer vision.
- numpy adalah library yang digunakan untuk melakukan operasi numerik dan manipulasi array multidimensi.
- 'pandas' adalah library yang digunakan untuk melakukan analisis dan manipulasi data terstruktur, khususnya dalam bentuk DataFrame.
- matplotlib.pyplot adalah library yang digunakan untuk membuat visualisasi data dalam bentuk grafik dan plot.
# 
### - [ln 2] Membaca / memuat sebuah gambar
- Program tersebut menggunakan library OpenCV (cv2) untuk membaca atau memuat sebuah gambar dengan nama file "kipas.jpg".
- Baris kode cv2.imread('kipas.jpg') mengambil gambar dengan nama "kipas.jpg" dari direktori yang sama dengan program Python yang sedang dijalankan. Fungsi imread() digunakan untuk membaca file gambar dan mengembalikan representasi matriks dari gambar tersebut.
# 
### - [ln 3] Display rgb images
Kode berikutnya melakukan beberapa langkah pemrosesan gambar dan menggunakan library matplotlib untuk menampilkan gambar tersebut.
- cv2.cvtColor(img, cv2.COLOR_BGR2RGB): Pada baris ini, fungsi cvtColor() digunakan untuk mengubah format warna gambar dari BGR (Blue-Green-Red) ke RGB (Red-Green-Blue). Hasilnya disimpan kembali ke variabel img.

- copy_img = img.copy(): Baris ini membuat salinan gambar yang telah diubah format warnanya. Ini dilakukan untuk mempertahankan gambar asli yang akan digunakan untuk pemrosesan selanjutnya, sementara copy_img akan digunakan untuk ditampilkan dengan matplotlib.

- plt.imshow(img): Baris ini menggunakan fungsi imshow() dari library matplotlib untuk menampilkan gambar yang telah diubah format warnanya (img). Digunakan untuk membuka jendela baru yang menampilkan gambar tersebut.

Pada tahap ini, gambar telah berhasil ditampilkan menggunakan matplotlib dan Anda dapat melihatnya dalam jendela grafik yang terbuka. Jika ada langkah selanjutnya dalam program ini atau jika Anda memiliki pertanyaan lebih lanjut, silakan beri tahu saya.
# 
### - [ln 4] Processing images
- lower = np.array([30,30,30]) dan higher = np.array([250,250,250]): Dua variabel ini mendefinisikan batas bawah dan batas atas untuk melakukan segmentasi warna pada gambar. Rentang warna yang ditentukan dalam kode ini adalah [30, 30, 30] untuk batas bawah dan [250, 250, 250] untuk batas atas. Ini berarti kita ingin mengambil piksel yang memiliki nilai warna antara batas bawah dan batas atas ini.

- mask = cv2.inRange(img,lower,higher): Fungsi inRange() digunakan untuk membuat masker (mask) biner dari gambar berdasarkan rentang warna yang ditentukan. Masker biner ini akan memiliki piksel yang bernilai 255 (putih) di area di mana piksel gambar asli berada di dalam rentang warna yang ditentukan, dan akan memiliki piksel yang bernilai 0 (hitam) di area lainnya.

- plt.imshow(mask,'gray'): Baris ini menggunakan fungsi imshow() dari matplotlib untuk menampilkan masker biner (mask) dengan skala warna keabuan ('gray'). Dengan menggunakan skala warna keabuan, area yang sesuai dengan rentang warna yang ditentukan akan ditampilkan sebagai putih, sementara area lainnya akan ditampilkan sebagai hitam.

Pada tahap ini, gambar hasil masker biner akan ditampilkan dalam jendela grafik yang terbuka. Anda dapat melihat area di mana warna gambar asli berada di dalam rentang warna yang ditentukan ditampilkan sebagai putih, sedangkan area lainnya ditampilkan sebagai hitam


# 
### - [ln 5&6] 
- cv2.inRange(img, lower, higher): Fungsi ini digunakan untuk membuat sebuah mask (masker) dari gambar (img) berdasarkan batasan nilai warna yang ditentukan. Masker ini akan memfilter piksel-piksel dalam gambar berdasarkan nilai warna yang berada di antara lower (batas bawah) dan higher (batas atas). Hasilnya adalah gambar biner, di mana piksel-piksel yang berada di dalam rentang warna akan menjadi putih, sedangkan piksel-piksel di luar rentang warna akan menjadi hitam.

- plt.imshow(mask, 'gray'): Fungsi ini digunakan untuk menampilkan gambar hasil masker yang telah dibuat. 'gray' adalah argumen opsional yang menentukan bahwa gambar yang ditampilkan dalam skala keabuan (grayscale).

# 
### - [ln 7] Finds the contour (borderline) of the detected object in the binary mask
- cont, _ = cv2.findContours(mask, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_NONE): Fungsi findContours() digunakan untuk menemukan kontur dalam gambar biner (mask). Kontur adalah garis tepi yang mengelilingi objek yang terdeteksi dalam gambar. Fungsi ini mengambil tiga parameter: gambar biner, mode retrieval (cv2.RETR_EXTERNAL), dan metode approksimasi kontur (cv2.CHAIN_APPROX_NONE).

- Parameter cv2.RETR_EXTERNAL untuk menentukan mode retrieval kontur, yang berarti hanya kontur eksternal yang akan ditemukan (kontur terluar objek). Kontur internal atau lubang dalam objek tidak akan diikutsertakan.

- Parameter cv2.CHAIN_APPROX_NONE menentukan metode approksimasi kontur, yang berarti hasil dari fungsi findContours() akan menyimpan kontur-kontur yang ditemukan dalam variabel cont. Namun, kita juga mendapatkan variabel _ yang tidak digunakan dalam program ini.

# 
### - [ln 8] Created an empty image using the NumPy and OpenCV libraries
- blank_image = np.zeros((1500,1500,3), np.uint8): Baris ini menggunakan fungsi zeros() dari NumPy untuk membuat matriks dengan dimensi 1500x1500 dan tiga saluran warna (RGB). Parameter np.uint8 menentukan tipe data yang digunakan untuk matriks, yaitu unsigned 8-bit integer.

- blank_image[:,0:1500//2] = (255,255,255): Baris ini mengatur nilai piksel pada setengah kiri gambar (0 hingga 750 kolom) menjadi putih (255, 255, 255). Dalam format warna RGB, nilai (255, 255, 255) mewakili warna putih.

- blank_image[:,1500//2:1500] = (255,255,255): Baris ini mengatur nilai piksel pada setengah kanan gambar (750 hingga 1500 kolom) menjadi putih (255, 255, 255).

# 
### - [ln 9] draw the contours found in the blank image.
- contour = cv2.drawContours(blank_image, cont, -1, 255, 0): Fungsi drawContours() digunakan untuk menggambar kontur pada gambar kosong (blank_image). Parameter yang digunakan adalah:
- blank_image: Gambar kosong yang akan digambar konturnya.
- cont: Variabel yang berisi kontur-kontur yang telah ditemukan sebelumnya.
- -1: Indeks kontur yang ingin digambar. Jika nilainya -1, semua kontur yang ditemukan akan digambar.
- 255: Warna kontur. Nilai 255 mewakili warna putih dalam format RGB.
- 0: Ketebalan garis kontur. Dalam hal ini, ketebalan garis kontur adalah 0, yang berarti kontur akan diisi solid dengan warna yang telah ditentukan.
Hasil dari fungsi drawContours() akan disimpan dalam variabel contour. Gambar tersebut sekarang akan memiliki garis tepi kontur yang tergambar di atasnya.
# 
### - [ln 10] rotates the contour image by 180 degrees, and then uses matplotlib to display the result.
- contour = cv2.rotate(contour, cv2.ROTATE_180): Fungsi rotate() digunakan untuk memutar gambar kontur (contour) sebesar 180 derajat. Parameter - cv2.ROTATE_180 menunjukkan bahwa rotasi yang dilakukan adalah sebesar 180 derajat.
- plt.imshow(contour): Baris ini menggunakan fungsi imshow() dari matplotlib untuk menampilkan gambar kontur yang telah diputar. Gambar kontur akan ditampilkan dalam jendela grafik yang terbuka.
# 
### - [ln 11 & 12] draw the contours found in the original drawing.
Pada tahap ini, gambar kontur yang telah diputar sebesar 180 derajat akan ditampilkan menggunakan matplotlib.
- cont_img = cv2.drawContours(img, cont, -1, 255, 10): Fungsi drawContours() digunakan untuk menggambar kontur pada gambar asli (img). Parameter yang digunakan adalah:
- img: Gambar asli pada which kontur akan digambar.
- cont: Variabel yang berisi kontur-kontur yang telah ditemukan sebelumnya.
- -1: Indeks kontur yang ingin digambar. Jika nilainya -1, semua kontur yang ditemukan akan digambar.
- 255: Warna kontur. Nilai 255 mewakili warna putih dalam format RGB.
- 10: Ketebalan garis kontur. Dalam hal ini, ketebalan garis kontur adalah 10, sehingga kontur akan digambar dengan ketebalan 10 piksel.
- to show contours images : plt.imshow(cont_img)
# 
### - [ln 13&14] calculate the area of ​​each contour found, and then choose the contour with the largest area.
- c = max(cont, key=cv2.contourArea): Baris ini menggunakan fungsi max() untuk mencari kontur dengan luas terbesar dari semua kontur yang ditemukan dalam variabel cont. Fungsi max() menggunakan argumen key untuk membandingkan kontur berdasarkan luasnya.
- cont: Variabel yang berisi kontur-kontur yang telah ditemukan sebelumnya.
- cv2.contourArea: Fungsi contourArea() digunakan untuk menghitung luas kontur.
- key=cv2.contourArea: Argumen key digunakan untuk menentukan kriteria perbandingan dalam pencarian kontur terbesar berdasarkan luasnya.
Hasilnya, kontur dengan luas terbesar akan disimpan dalam variabel c.
# 
### - [ln 14] get the bounding box of the contour
- x, y, w, h = cv2.boundingRect(c): Fungsi boundingRect() digunakan untuk menghitung kotak pembatas (bounding box) dari kontur c, yang merupakan kontur dengan luas terbesar yang telah dipilih sebelumnya.
- c: Kontur dengan luas terbesar yang telah dipilih sebelumnya.
- x: Koordinat X dari pojok kiri atas kotak pembatas.
- y: Koordinat Y dari pojok kiri atas kotak pembatas.
- w: Lebar (width) kotak pembatas.
- h: Tinggi (height) kotak pembatas.
# 
### - [ln 14] get the bounding box of the contour
- cv2.rectangle(img, (x, y), (x+w, y+h), (255, 255, 255), 5): Fungsi rectangle() digunakan untuk menggambar kotak pada gambar asli (img) dengan parameter berikut:
- img: Gambar asli pada mana kotak akan digambar.
- (x, y): Koordinat titik pojok kiri atas dari kotak pembatas.
- (x+w, y+h): Koordinat titik pojok kanan bawah dari kotak pembatas.
- (255, 255, 255): Warna kotak. Dalam format RGB, nilai (255, 255, 255) mewakili warna putih.
- 5: Ketebalan garis kotak.
- 0: Tipe garis kotak. Dalam hal ini, tipe garis kotak adalah 0, yang berarti garis kotak solid.
# 
### - [ln 16] use cropping to obtain a cropped image based on the bounding box of the original image.
- cropped_image = copy_img[y:y+h, x:x+w]: Baris ini menggunakan potongan (slicing) untuk memperoleh bagian gambar yang terpotong dari gambar asli (copy_img) dengan parameter berikut:
- [y:y+h]: Rentang baris (y) untuk memotong gambar, mulai dari y sampai y+h.
- [x:x+w]: Rentang kolom (x) untuk memotong gambar, mulai dari x sampai x+w.
Hasilnya, cropped_image akan berisi gambar yang merupakan potongan dari gambar asli berdasarkan kotak pembatas yang dihitung sebelumnya
# 
### - [ln 17] display the three final images
- plt.figure(figsize=(20,4)): Fungsi figure() digunakan untuk membuat sebuah jendela grafik baru dengan ukuran yang ditentukan. Parameter figsize=(20,4) menentukan lebar dan tinggi jendela grafik dalam satuan inchi.

- plt.subplot(1,3,1), plt.imshow(copy_img): Fungsi subplot() digunakan untuk membuat subplot pertama dalam jendela grafik. Parameter (1,3,1) menunjukkan bahwa jendela grafik akan memiliki 1 baris, 3 kolom, dan subplot pertama. Fungsi imshow() digunakan untuk menampilkan gambar copy_img pada subplot ini.

- plt.subplot(1,3,2), plt.imshow(contour): Fungsi subplot() digunakan untuk membuat subplot kedua dalam jendela grafik. Parameter (1,3,2) menunjukkan bahwa jendela grafik akan memiliki 1 baris, 3 kolom, dan subplot kedua. Fungsi imshow() digunakan untuk menampilkan gambar contour pada subplot ini.

- plt.subplot(1,3,3), plt.imshow(cont_img): Fungsi subplot() digunakan untuk membuat subplot ketiga dalam jendela grafik. Parameter (1,3,3) menunjukkan bahwa jendela grafik akan memiliki 1 baris, 3 kolom, dan subplot ketiga. Fungsi imshow() digunakan untuk menampilkan gambar cont_img pada subplot ini.

- Hasilnya, jendela grafik akan menampilkan tiga gambar dalam tata letak yang horizontal. Subplot pertama menampilkan gambar copy_img, subplot kedua menampilkan gambar contour, dan subplot ketiga menampilkan gambar cont_img.




## Sumber lain 
- http://jurnal.unidha.ac.id/index.php/jteksis/article/view/358
- https://ejournal.unsrat.ac.id/index.php/JIS/article/view/2057
- https://informatika.stei.itb.ac.id/~rinaldi.munir/Citra/2019-2020/14-Kontur.pdf