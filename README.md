# ========== Data Nasabah Bank BTW ===========

# List Data Nasabah
# 5 kolom : No.Rekening, Nama Lengkap, Domisili, Tipe Tabungan, Tahun Lahir
# Akan banyak menggunakan try, except, else (check suatu blok kode dan mengatasi errornya)

import sys
from tkinter import N

ListNasabah = [
              ['12345321','Andriyansyah ','Jakarta  ','Gold',1980],
              ['54321543','Novita Melati','Tangerang','Silver',1985],
              ['02198123','Rizki Saputra','Karawang ','Platinum',1981],
              ['03200045','Agus Suhendi ','Bandung  ','Silver',2000],
              ['00000001','Saputra Rizki','Tangerang','Silver',2022]
             ] 


# Function cari index dari sublist di dalam list dengan input no. rekening
def findIndex(NoNasabah):
    for i in range(len(ListNasabah)):
        try:
            j = ListNasabah[i].index(NoNasabah)
            return i
        except:
            pass    

# Function kembali ke Menu Utama
def back_menu_utama(function):
    back = input('\nKembali ke Menu Utama? [Y/N]: ').upper()

    if back == 'Y':
        menu_utama()

    elif back == 'N':
        function()

    else:
        print('\n**Input yang anda masukkan salah!**\n')
        function()

# Function Menu Utama 
def menu_utama():

    print(f'''
====== Data Base Nasabah Bank BTW ======\n
Menu Utama:
1. List Data Nasabah
2. Menambahkan Data Nasabah
3. Mengubah Data Nasabah
4. Menghapus Data Nasabah
5. Exit
    ''')

    pilihan_menu = input('Silahkan Pilih Menu [1-5]: ')

    if pilihan_menu == '1':
        read_data()

    elif pilihan_menu == '2':
        create_data()

    elif pilihan_menu == '3':
        update_data()

    elif pilihan_menu == '4':
        delete_data()

    elif pilihan_menu == '5':
        yakin = input('Yakin ingin keluar? [Y/N]: ').upper()
        if yakin == 'Y':
            print('\n== Terima Kasih ==\n')
            sys.exit()
        elif yakin == 'N':
            menu_utama()
        else:
            print('\n**Input yang anda masukkan salah!**')
            menu_utama() 

    else:
        print('\n**Input yang anda masukkan salah!**\n')
        menu_utama()        


# Function Read Data
def read_data():

    while True:

        # Print list menu read
        print('''
====== List Data Nasabah ======\n
1. List Seluruh Data
2. Report Data Tertentu
3. Kembali ke Menu Utama''')

        sub_read_input = input('\nSilahkan Pilih Sub Menu Read Data [1-3]: ')

        # Jika input 1, maka akan print semua data
        if sub_read_input == '1':
            if len(ListNasabah) == 0:    # Menghitung isi list, jika = 0 maka tidak ada data
                print('\n***** Tidak ada data nasabah di database *****\n')

            else:       # Jika ada data menampilkan semua isi list
                print('====== List Seluruh Data Nasabah ======\n')
                print('No. Rekening\t| Nama Lengkap\t\t| Domisili\t\t| Tipe Tabungan\t| Tahun Lahir')

                for i in range(len(ListNasabah)):
                    print(f'{ListNasabah[i][0]}\t| {ListNasabah[i][1]}\t\t| {ListNasabah[i][2]}\t\t| {ListNasabah[i][3]}  \t| {ListNasabah[i][4]}')

        # Jika input 2, maka akan print hanya data yang dipilih saja   
        elif sub_read_input == '2':
            NoNasabah = input('\nMasukkan No. Rekening: ').upper()
            print(f'\nData Nasabah dengan Nomor: {NoNasabah}\n')

            try:         # mencoba mencari no pasien di dalam list pasien
                x = findIndex(NoNasabah)

            except:     # kalau tidak ada / error
                print(f'\n==== {NoNasabah} tidak ada di list Data Nasabah ====')

            else:
                print(f'No. Rekening : {ListNasabah[x][0]} | Nama Lengkap: {ListNasabah[x][1]} | Domisili: {ListNasabah[x][2]} | Tipe Tabungan: {ListNasabah[x][3]} | Tahun Lahir: {ListNasabah[x][4]}')    


        # Jika input 3, maka akan kembali ke menu utama atau kembali ke menu read
        elif sub_read_input == '3':
            back_menu_utama(read_data)
            pass

        # Jika memasukkan input lain akan kembali ke menu read
        else:
            print('\n**Input yang anda masukkan salah!**\n')
            pass


# Function Create Data
def create_data():

    while True:

        # Print menu create data
        print('''
====== Menambah Data Nasabah ======\n
1. Tambah Data Nasabah
2. Kembali ke Menu Utama''')

        sub_create_input = input('\nSilahkan Pilih Sub Menu Create Data [1-2]: ')

        # Jika input 1, maka akan mencari dan menambah data
        if sub_create_input == '1':
            NoNasabah = input('\nMasukkan No. Rekening: ').upper()

            try:    # Ketika ditemukan indexnya akan mengembalikan print
                findIndex(NoNasabah) >= 0

            except:     # Ketika tidak ada index, maka akan diberikan input dibawah
                print('\nNomor Nasabah Belum Ada, Masukkan Detail Nasabah Dibawah:\n')
                Nama_Lengkap = input('Masukkan Nama Lengkap: ').capitalize()
                Domisili = input('Masukkan Domisili: ').capitalize()
                Tipe_Tabungan = input('Masukkan Gender Tipe Tabungan: ').capitalize()
                Tahun_Lahir = int(input('Masukkan Tahun Lahir: '))
                noPas = '0' + str(len(ListNasabah)) + str(Tahun_Lahir) + Nama_Lengkap[0].upper() + Tipe_Tabungan[0].upper()

                while True: # Untuk mengkonfirmasi apakah benar data ingin disimpan
                    confirm = input(f'Simpan data? [Y/N]: ').upper()

                    if confirm == 'Y':
                        ListNasabah.append([NoNasabah,Nama_Lengkap,Domisili,Tipe_Tabungan,Tahun_Lahir])
                        print('\n== Data Telah Tersimpan ==')
                        break

                    elif confirm == 'N':
                        create_data()

                    else:
                        confirm

            else:
                print(f'\n *** Nasabah dengan nomor {NoNasabah} sudah ada ***')


        # Jika input 2, maka akan kembali ke menu utama
        elif sub_create_input == '2':
            back_menu_utama(create_data)
            pass

        # Jika memasukkan input lain akan kembali ke menu read
        else:
            print('\n**Input yang anda masukkan salah!**\n')
            pass


# Function Update Data:
def update_data():

    while True:

        # Print menu update data
        print('''
====== Mengubah Data Nasabah ======\n
1. Ubah Data Nasabah
2. Kembali ke Menu Utama''')

        sub_update_input = input('\nSilahkan Pilih Sub Menu Ubah Data [1-2]: ')

        # Jika input 1, maka akan mencari no. pasien dan tanya update data
        if sub_update_input == '1':
            NoNasabah = input('\nMasukkan No. Rekening: ').upper()

            # Function untuk mengubah data dilist dengan input judul kolom
            def ubah(kolom):
                edit = input(f'Masukkan {kolom} baru: ').title()
                list_kolom = ['No. Rekening','Nama Lengkap','Domisili','Tipe Tabungan','Tahun Lahir']

                # Untuk mengkonfirmasi apakah benar data ingin disimpan
                confirm = input(f'\nUbah data? [Y/N]: ').upper()

                if confirm == 'Y':
                    ListNasabah[x][list_kolom.index(kolom)] = edit
                    print('\nPerubahan Data Telah Tersimpan\n')

                elif confirm == 'N':
                    update_data()

                else:
                    print('\n**Input yang anda masukkan salah!**\n')
                    update_data()                


            try:    # Ketika ditemukan indexnya akan mengembalikan tanya update
                x = findIndex(NoNasabah)

            except:     # jika no pasien tidak ditemukan dalam list nasabah
                print(f'\n**** {NoNasabah} tidak ada di list Data Pasien ****')
                update_data()

            else:    
                print(f'No. Rekening : {ListNasabah[x][0]} | Nama Lengkap: {ListNasabah[x][1]} | Domisili: {ListNasabah[x][2]} | Tipe Tabungan: {ListNasabah[x][3]} | Tahun Lahir: {ListNasabah[x][4]}')

                update_input = input('\nLanjut mengubah data? [Y/N]: ').upper()

                if update_input == 'Y':
                    kolom_input = input('Masukkan kolom yang ingin diubah (Kecuali No. Rekening): ').title()
                    if kolom_input == 'No. Rekening':
                        print("\n *** No. Rekening tidak bisa diubah ***")
                        update_data()
                    else:
                        ubah(kolom_input)   # fungsi ubah

                elif update_input == 'N':
                    update_data()

                else:
                    print('\n**Input yang anda masukkan salah!**\n')
                    pass  

        # Jika input 2, maka akan kembali ke menu utama            
        elif sub_update_input == '2':
            back_menu_utama(update_data)
            pass

        # Jika memasukkan input lain akan kembali ke menu read
        else:
            print('\n**Input yang anda masukkan salah!**\n')
            pass

# Function Delete Data:
def delete_data():

    while True:

        # Print menu delete data
        print('''
====== Menghapus Data Nasabah ======\n
1. Hapus Data Nasabah
2. Kembali ke Menu Utama''')

        sub_delete_input = input('\nSilahkan Pilih Sub Menu Ubah Data [1-2]: ')

        # Jika 1, maka tanya no pasien yang akan dihapus datanya
        if sub_delete_input == '1':
            NoNasabah = input('\nMasukkan No. Rekening: ').upper()

            try:    # Ketika ditemukan indexnya akan mengembalikan tanya delete
                x = findIndex(NoNasabah)


            except:     # jika no pasien tidak ditemukan dalam list nasabah
                print(f'\n**** {NoNasabah} tidak ada di list Data Nasabah ****')
                delete_data()   

            else:
                print(f'No. Rekening : {ListNasabah[x][0]} | Nama Lengkap: {ListNasabah[x][1]} | Domisisli: {ListNasabah[x][2]} | Tipe Tabungan: {ListNasabah[x][3]} | Tahun Lahir: {ListNasabah[x][4]}')

                delete_input = input('\nLanjut hapus data? [Y/N]: ').upper()  

                if delete_input == 'Y':
                    del ListNasabah[x]
                    print('\n** Data berhasil dihapus **')

                elif delete_input == 'N':
                    delete_data()

                else:
                    print('\n**Input yang anda masukkan salah!**\n')
                    pass  

        # Jika input 2, maka akan kembali ke menu utama            
        elif sub_delete_input == '2':
            back_menu_utama(delete_data)
            pass

        # Jika memasukkan input lain akan kembali ke menu read
        else:
            print('\n**Input yang anda masukkan salah!**\n')
            pass        

menu_utama()
