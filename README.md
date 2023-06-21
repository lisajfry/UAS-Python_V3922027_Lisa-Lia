# UAS-Python_V3922027_Lisa-Lia

PENJELASAN SCRIPT SCRAPPING:
//import modul
import requests
import csv
import os

//perintah masukkan keyword
BANDO = input('Masukkan keyword: ')
//untuk menyimpan file csv ke directori hasilscrapping yang telah dibuat
directory = 'hasilscrapping'
file_path = os.path.join(directory, '{}.csv'.format(key))

//untuk memeriksa directory
if not os.path.exists(directory):
    os.makedirs(directory)

//masukkan url api dari web
url = 'https://api.bukalapak.com/multistrategy-products'
count = 0

//membuka file & mengatur header untuk file csv
with open(file_path, 'w', newline='') as file:
    write = csv.writer(file)
    header = ['nama', 'harga', 'toko']
    write.writerow(header)

//tambahkan halaman yang akan di scrapping
    for page in range(1, 2):
//inputkan parameter dari halaman web yang dipilih
        parameter = {
            'keywords': BANDO,
            'limit': 50,
            'offset': (page - 1) * 50,
            'facet': 'True',
            'page': page,
            'access_token': 'eyJhbGciOiJSUzI1NiIsImtpZCI6ImFjY291bnRzLmp3dC5hY2Nlc3MtdG9rZW4iLCJ0eXAiOiJKV1QifQ.eyJpc3MiOiJodHRwczovL2FjY291bnRzLmJ1a2FsYXBhay5jb20vIiwic3ViIjoiMjMxZDRhODY5MDVmMGYyNjJjNWUwM2ZjIiwiYXVkIjpbImh0dHBzOi8vYWNjb3VudHMuYnVrYWxhcGFrLmNvbSIsImh0dHBzOi8vYXBpLmJ1a2FsYXBhay5jb20iLCJodHRwczovL2FwaS5zZXJ2ZXJtaXRyYS5jb20iXSwiZXhwIjoxNjg3MzUzMjQzLCJuYmYiOjE2ODczNDQ4NDMsImlhdCI6MTY4NzM0NDg0MywianRpIjoiOXAzb0RjUXhBN3ppN0ZiaGJ5VzlrdyIsImNsaWVudF9pZCI6IjIzMWQ0YTg2OTA1ZjBmMjYyYzVlMDNmYyIsInNjb3BlIjoicHVibGljIn0.jXHuQZe83ZO-3FZu141qzcVKXM90hth1xV08qepwHqEwEXhI_safW9UHM76c1F0m4kL-ez_FC8ANRxewqrPbjJc_Q1NJP9o8reLwwktXjzDacEpbb0jubu0Pl0VBCCcJ-gslBqYNWVXUuXgDXKVtq-doZH0dz4TVedkx1KLFaaogtCLKMwQ6AsOOyqWheCqzwjU7oYTKYddT6VeK22HvzvBFLTXaJNZOH1i6ijTldfumhcpUY5pjXwks9DzRCljI-ggkYznpOUhw_Wu9R2H2OaQnX4hmpJoOyKdxyGiOe_reUQ8LV0pBrNVq5qKjRzTmDLhMTMOOmtv6j062ERKrTw'
        }

    //get ke api dan tambahkan .json untuk merespon 
        r = requests.get(url, params=parameter).json()
        products = r['data']

    //looping berisi nama, harga, dan toko
        for p in products:
            nama = p['name']
            harga = p['price']
            toko = p['store']
            count += 1
            print('No:', count, 'Name:', nama, 'Price:', harga, 'Store:', toko)
    //menuliskan informasi produk ke csv
            write.writerow([nama, harga, toko])


PENJELASAN SCRIPT GRAFIK:
1. Scatter Plot:
//import modul
import pandas as pd
import matplotlib.pyplot as plt

//membaca file csv 
data = pd.read_csv("C:/Users/Penti Anggraini/bukalapak/hasilscrapping/BANDO.csv")

//pilih data yang diablim dari isi file csv
plt.scatter(data['nama'], data['harga'])

//bentuk scatter plot
plt.title("Scatter Plot")

//sumbu x
plt.xlabel('nama')
//sumbu y
plt.ylabel('harga')

//tampilkan
plt.show()

2. Pie Chart:
//import modul
import pandas as pd
import matplotlib.pyplot as plt

//untuk membaca file csv
data = pd.read_csv("C:/Users/Penti Anggraini/bukalapak/hasilscrapping/BANDO.csv")

//menghitung jmlh kemunculan kategori di kolom nama
kategori_counts = data['nama'].value_counts()

//jumlah kategori yang diambil
top5_kategori = kategori_counts.head(5)

//membuat pie chart
plt.pie(top5_kategori, labels=top5_kategori.index, autopct='%1.1f%%')

//judul
plt.title('Pie Chart Top 5 Kategori Nama Bando')

//menampilkan
plt.show()
