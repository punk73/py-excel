
after review current document, what we need to do is :

- create master data. including :
    - Master model for convert MA to Mecha Models.
    - Model Group for Arrange Line and Model.
    - Master Line data include Man Power, Capacity, Model.
    - Master data stock.
    - Master month and line for PMC Requirement. // ini nanti. katanya bakal ada solusi buat upload ke tops.


- implement max logic:
    - basically, we need to maximize the amount of production based on time and line_process available.

    - Recap MA : jumlah requirement per model. setelah compare dengan current stock.
        - input     : 
            - SKE
            - nagano
            - soundmax
            - service part
            - jein internal
            - data stock
        - outputnya :
            - MA requirement. ( kolom nya kita tentukan nanti )

    - convert MA To Mecha amount (we need to consider the scale. apakah selalu 1:1 atau tidak)
        - input : 
            - MA requirement. (hasil dari process 1)
            - Master model for convert MA to Mecha Models.
        - output: mecha_requirement. (kolom: mecha model, qty, start_date)
            dari ario, 1 model MA itu belongsTo 1 model mecha.
                jadi disini bisa jadi 10 model MA jadi 5 model mecha. karena mungkin model MA
                punya mecha yg sama.

    - assign amount to specific line and time. 
        - ( harus dipastikan apakah ada semacam sentuhan manual pada proses ini )
        - (juga harus dipastikan apakah logic nya common atau ada beberapa jenis. misalnya: oem atau bukan dsb )
        - hal yg harus diperhatikan :
            - Line Availability.
            - Line Capacity.
            - Re-arrange edited schedules
            - schedule data sebelumnya. ketika harus consider data sebelumnya.
        
        input : 
            - Master Line data include Man Power, Capacity, Model.
            - mecha_requirement

        output :
            - created schedule.txt


- create schedule.txt
    - kita harus sepakati format hasilnya harus seperti apa. biar tidak ada kebingungan.
    - txt ini dibuat untuk diupload atau untuk dibaca.

<!-- another step -->
    create automation to input to tops.

=====================================================================
- sf92 = schedule tops;
- mecha harus running sebelum MA. jumlah waktunya beda2. ( dengan start_date yg sudah dikurangi tentunya dr tanggal running MA )
- output dari txt nya itu sf92 juga. tapi dengan tambahan data Mecha.
- data email adalah data demand juga. tapi bukan dari tops. melainkan dari planning yg lain.
tiap member, punya format yg berbeda. ada process yg harus dilakukan untuk memformat data masukan tsb.
- program tidak tahu preferensi personal pic. jadi bisa jadi akan assign ke line yg berbeda.
- apakah text file yg di generate jg harus menghitung ulang stock ?

==================================================================================
target kita 13-01-2021 adalah punya file input dan output yang lengkap.
yaitu :
    - sf92, ske model, oem model + data stock => MA Requirement.
    - MA Requirement + Master model for convert MA to Mecha Models. => Mecha Requirement
    - Mecha Requirement + Master Line data include Man Power, Capacity, Model. = schedule.txt
==================================================================================================

order via email meliputi :
- SKE
- nagano
- soundmax
- service part
- jein internal

kalau  butuh data refer ke :
\\svrfile\DEPARTMENT\planning\Sharing\B_SCHEDULER\MECHA
=================================================================================================

stock : 

data yang di generate wajib konsisten. based on data data yang diinput.


kita harus tentukan start_date, dan max end date.

hari pertama 90% ini harus dipikirkan ada 