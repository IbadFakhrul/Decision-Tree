# DECISION TREE

**A. Pengertian**

Decisison Tree atau dalam Bahasa Indonesia disebut sebagai pohon keputusan merupakan suatu metode pengambilan keputusan yang menyusun setiap opsi menjadi bentuk yang bercabang. Pohon keputusan membangun model klasifikasi atau regresi dalam bentuk struktur pohon.

Metode ini memiliki 3 komponen yaitu akar, ranting, dan daun. Tiap komponennya terdiri dari 2 atau lebih cabang, dan atribut yang memiliki nilai *Information Gain* tertinggilah yang nantinya akan menjadi akar.

**B. Kode Program Python**

1. Pertama-tama import library pandas untuk memasukkan data.

   ```
   import pandas as pd
   df = pd.read_csv('https://raw.githubusercontent.com/plotly/datasets/master/iris-data.csv')
   ```

2. Lalu definisikan nilai X dan Y yang nantinya akan digunakan untuk split data menjadi training dan testing. 'iloc' digunakan untuk menyeleksi data pada lokasi tertentu saja, iloc[:,:4] pada variabel X untuk memuat 4 kolom pertama, dan iloc[:,4] pada variabel y untuk kolom terakhir atau kolom ke-5 (mulai dari 0). Variabel X digunakan untuk memuat kolom "sepal length, sepal width,petal length,petal width", sedangkan variabel y untuk memuat kolom "class".

   ```
   X = df.iloc[:,0:4]
   y = df.iloc[:,4]
   ```

3. Import library dari sklearn model_selction berupa train_test_split, untuk memisah data di atas menjadi 2 bagian yaitu data training dan data testing dengan perbandingan 80:20. X_train adalah data training dari variabel X tadi sedangkan X_test adalah data testing, sama halnya dengan y_train dan y_test. Di dalam train_test_split terdapat X dan y untuk memanggil variabel di atas, test_size untuk menentukan seberapa banyak data yang digunakan untuk testing, dalam hal ini adalah 0.2 atau 20%, random_state digunakan untuk mengacak data awal.

   ```
   from sklearn.model_selection import train_test_split
   
   X_train, X_test, y_train, y_test = train_test_split(X,y, test_size=0.2, random_state=10)
   ```

4. Import tree dari library sklearn. Panggil DecisionTreeClassifier() dari tree karena data ini adalah data klasifikasi, lalu masukkan data training ke dalam variabel 'model'. Untuk memprediksi kelas dari sample (data training).

   ```
   from sklearn import tree
   
   model = tree.DecisionTreeClassifier()
   model = model.fit(X_train, y_train)
   
   hasil_prediksi = model.predict(X_test)
   ```

5. Import accuracy_score dari library sklearn metrics. accuracy_score sendiri digunakan untuk menghitung akurasi atau ketepatan berdasarkan data yang telah diuji sebelumnya, dengan hasil_prediksi dan y_test debagai parameter dihasilkanlah akurasi dari kasus ini yaitu 96.67%

   ```
   from sklearn.metrics import accuracy_score
   
   accuracy = accuracy_score(hasil_prediksi, y_test)*100
   print('Akurasi: ' + str(round(accuracy, 2)) + '%')
   
   >>Akurasi: 96.67%
   ```

6. Untuk menamilkan gambar tree dari data

   ```
   tree.plot_tree(model)
   ```

**C. Perbandingan Antara Decision Tree, Naive Bayes, Dan K-NN**

Dengan menggunakan data dan cara yang sama, hasil yang dikeluarkan oleh algoritma Decision Tree, Naive Bayes, dan K-NN adalah,

- Decision Tree: 96.67%
- Naive Bayes:  100.0%
- K-NN: 96.67%

Jadi dapat disimpulkan bahwa jika menggunakan data-data di atas maka hasil yang terbaik dengan akurasi tertinggi adalah dari algoritma Naive Bayes.
