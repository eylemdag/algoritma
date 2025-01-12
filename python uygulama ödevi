def kullanici_girisi(prompt, kontrol, hata_mesaji):
    while True:
        try:
            deger = int(input(prompt))
            if kontrol(deger):
                return deger
            else:
                print(hata_mesaji)
        except ValueError:
            print(hata_mesaji)


ciktilar = []
konut_sayisi = 0
birinci_kademe_konut_sayisi = 0
ikinci_kademe_konut_sayisi = 0
ucuncu_kademe_konut_sayisi = 0
isyeri_sayisi = 0
birinci_kademe_isyeri_sayisi = 0
ikinci_kademe_isyeri_sayisi = 0
kamu_kurumu_sayisi = 0
trustik_tesis_sayisi = 0
konut_toplam_gun =  0
konut_toplam_su = 0
while True:
    # Abone tipi girişi
    abone_tipi = kullanici_girisi(
        "Abone tipini girin (1-4 arasında bir sayı olmalı): ",
        lambda x: 1 <= x <= 4,
        "Geçersiz giriş! Lütfen 1-4 (dahil) arası bir tam sayı giriniz."
    )

    # İlk sayaç girişi
    onceki_sayac = kullanici_girisi(
        "İlk sayaç değerini giriniz: ",
        lambda x: x >= 0,
        "Geçersiz giriş! Lütfen 0'dan büyük bir değer giriniz."
    )

    # Son sayaç girişi
    sonraki_sayac = kullanici_girisi(
        "Son sayaç değerini giriniz: ",
        lambda x: x >= onceki_sayac,
        "Geçersiz giriş! Önceki sayaçtan büyük veya eşit bir değer giriniz."
    )

    # Gün sayısı girişi
    gun_sayisi = kullanici_girisi(
        "Gün sayısını giriniz: ",
        lambda x: x > 0,
        "Geçersiz giriş! Gün sayısı 0'dan büyük olmalı!"
    )
    
    su_kullanim_miktari = sonraki_sayac - onceki_sayac
    
    if abone_tipi == 1:
        abone_adi = "Konut"
        konut_sayisi += 1
        konut_toplam_gun += gun_sayisi
        konut_toplam_su += sonraki_sayac-onceki_sayac
        atik_su_ucreti = su_kullanim_miktari * 1.91
        if su_kullanim_miktari <= ((13 * gun_sayisi) / 30):
            kullanim_fatura = su_kullanim_miktari * 2.24
            birinci_kademe_konut_sayisi += 1
        elif su_kullanim_miktari <= (20 * (gun_sayisi / 30)):
            kullanim_fatura = (13 * (gun_sayisi / 30)) * 2.24 + (su_kullanim_miktari - (13 * (gun_sayisi / 30))) * 5.78
            ikinci_kademe_konut_sayisi += 1
        else:
            kullanim_fatura = (13 * (gun_sayisi / 30) * 2.24) + ((7 * (gun_sayisi / 30)) * 5.78) + (su_kullanim_miktari - (20 * (gun_sayisi / 30))) * 9.33
            ucuncu_kademe_konut_sayisi += 1
    elif abone_tipi == 2:
        abone_adi = "İşyeri"
        isyeri_sayisi += 1
        atik_su_ucreti = su_kullanim_miktari * 3.79
        
        if su_kullanim_miktari <= (10 * (gun_sayisi / 30)):
            kullanim_fatura = su_kullanim_miktari * 7.71
            birinci_kademe_isyeri_sayisi += 1
        else:
            kullanim_fatura = ((10 * (gun_sayisi / 30)) * 7.71) + ((su_kullanim_miktari - (10 * (gun_sayisi / 30))) * 8.88)
            ikinci_kademe_isyeri_sayisi += 1
            
    elif abone_tipi == 3:
        abone_adi = "Kamu Kurumu"
        kamu_kurumu_sayisi += 1
        atik_su_ucreti = su_kullanim_miktari * 2.56
        kullanim_fatura = su_kullanim_miktari * 6.64
    
    else:
        abone_adi = "Trustik Tesis"
        trustik_tesis_sayisi += 1
        atik_su_ucreti = su_kullanim_miktari * 1.91
        kullanim_fatura = su_kullanim_miktari * 5.78
    
    kdv_tutari =  (atik_su_ucreti + kullanim_fatura) * 8 / 100
    toplam_fatura = kdv_tutari + atik_su_ucreti + kullanim_fatura
    
    ciktilar.append({
        "Abone Tipi": abone_adi,
        "Su Tüketim Miktarı (m³)": f"{su_kullanim_miktari:.2f} m³",
        "Gün Sayısı": gun_sayisi,
        "Su Tüketim Ücreti (₺)": round(kullanim_fatura, 2),
        "Atık Su Ücreti (₺)": round(atik_su_ucreti, 2),
        "KDV (₺)": round(kdv_tutari, 2),
        "Fatura Tutarı (₺)": round(toplam_fatura, 2)
    })
    
    # Son aboneye ait çıktıyı gösterme
    print("\nSon Abone Bilgileri:")
    print(f"{'Abone Tipi Kodu:':<20} {abone_tipi}")
    print(f"{'İlk Sayaç:':<20} {onceki_sayac}")
    print(f"{'Son Sayaç:':<20} {sonraki_sayac}")
    print(f"{'Gün Sayısı:':<20} {gun_sayisi}")
    print("\nSon Çıktılar:")
    print(f"{'Abone Tipi':<20} {'Su Tüketim Miktarı (m³)':<25} {'Su Tüketim Ücreti (₺)':<25} {'Atık Su Ücreti (₺)':<20} {'KDV (₺)':<15} {'Fatura Tutarı (₺)':<20}")
    print("-" * 127)
    print(f"{abone_adi:<20} {f'{su_kullanim_miktari:.2f} m³':<25} {round(kullanim_fatura, 2):<25} {round(atik_su_ucreti, 2):<20} {round(kdv_tutari, 2):<15} {round(toplam_fatura, 2):<20}")

    # Kullanıcıya başka abone girip girmeyeceği sorusu
    cevap = input("\nBaşka abone var mı? (E/e: Evet, H/h: Hayır): ").strip().lower()
    
    if cevap == 'h':
        print("Program sonlandırılıyor.")
        
        # Tüm çıktıların gösterilmesi
        print("\nTüm Çıktılar:")
        print(f"{'Abone Tipi':<20} {'Su Tüketim Miktarı (m³)':<25} {'Su Tüketim Ücreti (₺)':<25} {'Atık Su Ücreti (₺)':<20} {'KDV (₺)':<15} {'Fatura Tutarı (₺)':<20}")
        print("-" * 120)
        for c in ciktilar:
            print(f"{c['Abone Tipi']:<20} {c['Su Tüketim Miktarı (m³)']:<25} {c['Su Tüketim Ücreti (₺)']:<25} {c['Atık Su Ücreti (₺)']:<20} {c['KDV (₺)']:<15} {c['Fatura Tutarı (₺)']:<20}")
        print("\n")
        
        
        if konut_sayisi > 0:
            yuzde = (birinci_kademe_konut_sayisi / konut_sayisi) * 100
        else:
            yuzde = 0
            
        if isyeri_sayisi > 0:
            yuzde2 = (ikinci_kademe_isyeri_sayisi / isyeri_sayisi) * 100
        else:
            yuzde2 = 0
        
        toplam_atik_su_ucreti = 0
        toplam_kdv = 0
        konut_en_fazla_gunluk_ortalama_dizi = []
        toplam_konut_su_tuketim = 0
        toplam_isyeri_su_tuketim = 0
        toplam_kamu_kurumu_su_tuketim = 0
        toplam_trustik_tesis_su_tuketim = 0
        su_tuketim_ucreti_en_fazla = 0
        su_tuketim_ucreti_en_fazla_abone_tipi = ""
        su_tuketim_ucreti_en_fazla_su_tuketim = ""
        atik_su_ucreti_en_fazla = 0
        atik_su_ucreti_en_fazla_abone_tipi = ""
        atik_su_ucreti_en_fazla_su_tuketim = ""
        
        konut_toplam_su_tuketim_ucreti = 0
        isyeri_toplam_su_tuketim_ucreti = 0
        kamu_kurumu_toplam_su_tuketim_ucreti = 0
        trustik_tesis_toplam_su_tuketim_ucreti = 0
        
        konut_gunluk_ortalama = []
        isyeri_gunluk_ortalama = []
        kamu_kurumu_gunluk_ortalama = []
        trustik_tesis_gunluk_ortalama = []

        
        for cikti in ciktilar:
            toplam_atik_su_ucreti += cikti["Atık Su Ücreti (₺)"]
            toplam_kdv += cikti["KDV (₺)"]
            
            if atik_su_ucreti_en_fazla < cikti["Atık Su Ücreti (₺)"]:
                atik_su_ucreti_en_fazla = cikti["Atık Su Ücreti (₺)"]
                atik_su_ucreti_en_fazla_abone_tipi = cikti["Abone Tipi"]
                atik_su_ucreti_en_fazla_su_tuketim = cikti["Su Tüketim Miktarı (m³)"]
            
            if su_tuketim_ucreti_en_fazla < cikti["Su Tüketim Ücreti (₺)"]:
                su_tuketim_ucreti_en_fazla = cikti["Su Tüketim Ücreti (₺)"]
                su_tuketim_ucreti_en_fazla_abone_tipi = cikti["Abone Tipi"]
                su_tuketim_ucreti_en_fazla_su_tuketim = cikti["Su Tüketim Miktarı (m³)"]
                
            if cikti["Abone Tipi"] == "Konut":
                toplam_konut_su_tuketim += float(cikti["Su Tüketim Miktarı (m³)"].split()[0])
                konut_toplam_su_tuketim_ucreti += cikti['Su Tüketim Ücreti (₺)']
                
                gunluk_ortalama = float(cikti["Su Tüketim Miktarı (m³)"].split()[0]) / cikti["Gün Sayısı"]
                konut_gunluk_ortalama.append(gunluk_ortalama)
                konut_en_fazla_gunluk_ortalama_dizi.append(gunluk_ortalama)
                
            elif cikti["Abone Tipi"] == "İşyeri":
                toplam_isyeri_su_tuketim += float(cikti["Su Tüketim Miktarı (m³)"].split()[0])
                isyeri_toplam_su_tuketim_ucreti += cikti['Su Tüketim Ücreti (₺)']
                
                gunluk_ortalama = float(cikti["Su Tüketim Miktarı (m³)"].split()[0]) / cikti["Gün Sayısı"]
                isyeri_gunluk_ortalama.append(gunluk_ortalama)
            elif cikti["Abone Tipi"] == "Kamu Kurumu":
                toplam_kamu_kurumu_su_tuketim += float(cikti["Su Tüketim Miktarı (m³)"].split()[0])
                kamu_kurumu_toplam_su_tuketim_ucreti += cikti['Su Tüketim Ücreti (₺)']
                
                gunluk_ortalama = float(cikti["Su Tüketim Miktarı (m³)"].split()[0]) / cikti["Gün Sayısı"]
                kamu_kurumu_gunluk_ortalama.append(gunluk_ortalama)
            else :
                toplam_trustik_tesis_su_tuketim += float(cikti["Su Tüketim Miktarı (m³)"].split()[0])
                trustik_tesis_toplam_su_tuketim_ucreti += cikti['Su Tüketim Ücreti (₺)']
                
                gunluk_ortalama = float(cikti["Su Tüketim Miktarı (m³)"].split()[0]) / cikti["Gün Sayısı"]
                trustik_tesis_gunluk_ortalama.append(gunluk_ortalama)
        
        
        konut_gunluk_ortalama_max = konut_toplam_su/konut_toplam_gun
        isyeri_gunluk_ortalama_max = max(isyeri_gunluk_ortalama, default=0)
        kamu_kurumu_gunluk_ortalama_max = max(kamu_kurumu_gunluk_ortalama, default=0)
        trustik_tesis_gunluk_ortalama_max = max(trustik_tesis_gunluk_ortalama, default=0)
        
        konut_en_fazla_gunluk_ortalama = max(konut_en_fazla_gunluk_ortalama_dizi, default=0)
        toplam_su_tuketim = toplam_konut_su_tuketim + toplam_isyeri_su_tuketim + toplam_kamu_kurumu_su_tuketim + toplam_trustik_tesis_su_tuketim
        toplam_su_tuketim_ucreti = trustik_tesis_toplam_su_tuketim_ucreti + kamu_kurumu_toplam_su_tuketim_ucreti + isyeri_toplam_su_tuketim_ucreti + konut_toplam_su_tuketim_ucreti
        
        toplam_abone_sayisi = konut_sayisi + isyeri_sayisi + kamu_kurumu_sayisi + trustik_tesis_sayisi
        konut_yuzde = (konut_sayisi / toplam_abone_sayisi) * 100
        isyeri_yuzde = (isyeri_sayisi / toplam_abone_sayisi) * 100
        kamu_kurumu_yuzde = (kamu_kurumu_sayisi / toplam_abone_sayisi) * 100
        trustik_tesis_yuzde = (trustik_tesis_sayisi / toplam_abone_sayisi) * 100
       
        
        print(f"1) Abone Tipi      Abone Say  Yüzde   Günlük Ort Tük")
        print(f"    Konut           {konut_sayisi}          % {konut_yuzde:.2f}    {konut_gunluk_ortalama_max:.2f} ton")
        print(f"    İşyeri          {isyeri_sayisi}          % {isyeri_yuzde:.2f}    {isyeri_gunluk_ortalama_max:.2f} ton")
        print(f"    Kamu Kurumu     {kamu_kurumu_sayisi}      % {kamu_kurumu_yuzde:.2f}    {kamu_kurumu_gunluk_ortalama_max:.2f} ton")
        print(f"    Turistik Tesis  {trustik_tesis_sayisi}     % {trustik_tesis_yuzde:.2f}    {trustik_tesis_gunluk_ortalama_max:.2f} ton")
                
        print(f"\n2) Aylık su tüketim miktarı, 1. kademeyi aşmayan konut abonelerinin:")
        print(f"   Sayısı: {birinci_kademe_konut_sayisi}")
        print(f"   Yüzdesi: %{round(yuzde, 2)}")
        
        print(f"\n3) Aylık su tüketim miktarı, 1. kademeyi aşan işyeri abonelerinin: ")
        print(f"   Sayısı: {ikinci_kademe_isyeri_sayisi}")
        print(f"   Yüzdesi: %{round(yuzde2, 2)}")
        
        print(f"\n4) Günlük ortalama su tüketim miktarı en yüksek olan konut tipi abonenin günlük ortalama su tüketim miktarı: {konut_en_fazla_gunluk_ortalama}")
        
        print(f"\n5) Aylık su tüketim ücreti en yüksek olan abonenin:")
        print(f"{'Abone Tipi:':<35} {su_tuketim_ucreti_en_fazla_abone_tipi}")
        print(f"{'Aylık Su Tüketim Miktarı (ton):':<35} {float(su_tuketim_ucreti_en_fazla_su_tuketim.split()[0]):.2f}")
        print(f"{'Ödediği Aylık Su Tüketim Ücreti (₺):':<35} {su_tuketim_ucreti_en_fazla:.2f}")
        
        print(f"\n6) Aylık atık su ücreti en yüksek olan abonenin: ")
        print(f"{'Abone Tipi:':<35} {atik_su_ucreti_en_fazla_abone_tipi}")
        print(f"{'Aylık Su Tüketim Miktarı (ton):':<35} {float(atik_su_ucreti_en_fazla_su_tuketim.split()[0]):.2f}")
        print(f"{'Ödediği Aylık Atık Su Ücreti (₺):':<35} {atik_su_ucreti_en_fazla:.2f}")
        
        print(f"\n7) Toplam Su Tüketimleri:")
        print(f"{'Konut Tüketimi (m³)':<30} {toplam_konut_su_tuketim:.2f} ton")
        print(f"{'İşyeri Tüketimi (m³)':<30} {toplam_isyeri_su_tuketim:.2f} ton")
        print(f"{'Kamu Kurumu Tüketimi (m³)':<30} {toplam_kamu_kurumu_su_tuketim:.2f} ton")
        print(f"{'Turistik Tesis Tüketimi (m³)':<30} {toplam_trustik_tesis_su_tuketim:.2f} ton")
        print(f"{'Toplam Tüketim':<30} {toplam_su_tuketim:.2f} ton")
        
        # Abone tiplerinin su tüketim ücretleri
        print(f"\n8) Toplam Su Tüketim Ücretleri:")
        print(f"1) Konut toplam su tüketim ücreti: {konut_toplam_su_tuketim_ucreti:.2f} TL")
        print(f"2) İşyeri toplam su tüketim ücreti: {isyeri_toplam_su_tuketim_ucreti:.2f} TL")
        print(f"3) Kamu Kurumu toplam su tüketim ücreti: {kamu_kurumu_toplam_su_tuketim_ucreti:.2f} TL")
        print(f"4) Turistik Tesis toplam su tüketim ücreti: {trustik_tesis_toplam_su_tuketim_ucreti:.2f} TL")
        print(f"{'Toplam Tüketim':<30} {toplam_su_tuketim_ucreti:.2f} TL")


        print(f"\n9) Tüm abonelerden elde edilen aylık toplam atık su ücreti: {round(toplam_atik_su_ucreti, 2)} ₺")
        print(f"\n10) Devlete ödenen aylık toplam KDV tutarı: {round(toplam_kdv, 2)} ₺")
        
        break
    elif cevap != 'e':
        print("Geçersiz cevap! Lütfen E/e ya da H/h giriniz.")
