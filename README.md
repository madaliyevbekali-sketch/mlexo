# LEXO — Ma’muriy huquq test sayti

Bitta fayldan iborat statik sayt (`index.html`). Server yoki o‘rnatish talab qilinmaydi.

**Muallif:** M.Bekali

## Imkoniyatlar

- Bosh sahifada **LEXO**; **Ma’muriy huquq** bo‘limiga alohida tugma orqali kiriladi
- Faqat **talabalar ro‘yxatidagi** ism va familiya bilan kirish mumkin (5 ta noto‘g‘ri urinishdan keyin 30 soniya kutish)
- To‘g‘ri kirgan talaba **o‘z profiliga** tushadi (ism-familiya, savollar soni, vaqt, oxirgi natija). Test shu yerdagi **"Testni boshlash"** tugmasi bilan boshlanadi
- **Fan haqida** sahifasi (profildan va menyudan ochiladi)
- Test paytidan tashqari hamma sahifada **"Bosh sahifa"** tugmasi ko‘rinib turadi
- 15 ta murakkab test, har bir savolning o‘z bali bor (jami 21.8 ball), **15 daqiqa** vaqt. Vaqt tugasa o‘quvchi yutqazadi va testdan chiqariladi
- Saytdan yoki oynadan chiqib ketgan vaqt va necha marta chiqqani hisoblanadi
- Natija **75% dan yuqori** bo‘lsa, natijadan oldin maxsus tabrik effekti ko‘rsatiladi
- Natijani nusxalash: matn ichiga **bir martalik tasdiq kodi** qo‘shiladi
- **Natijani tekshirish** bo‘limi (o‘qituvchi uchun) kirish kodi bilan himoyalangan; kod to‘g‘ri kiritilgach, tasdiq kodini tekshiradi

## Natijani tekshirish kodini o‘zgartirish

Kirish kodi `index.html` ichida ochiq matn emas, hash ko‘rinishida saqlanadi (`GATE_HASH`). Yangi kod uchun (kichik harflarda yozing):

```
python3 -c "import hashlib;print(hashlib.sha256(b'LEXO-GATE-2026|YANGIKOD').hexdigest())"
```

Chiqqan qiymatni `index.html` dagi `const GATE_HASH='...'` o‘rniga qo‘ying. Katta-kichik harf va tutuq belgilari e’tiborga olinmaydi.

## Talabalar ro‘yxatini yangilash

Ismlar `index.html` ichida ochiq matn emas, hash ko‘rinishida saqlanadi (`const STUDENTS = [...]`).
Excel faylidan yangi ro‘yxat yaratish:

```
pip install openpyxl
python3 tools/hash_students.py talabalar_royxati.xlsx
```

Chiqqan `const STUDENTS = [ ... ];` blokini `index.html` dagi eskisi o‘rniga qo‘ying.
Excel formati: B ustunida `FAMILIYA ISM OTASINING ISMI` (birinchi so‘z familiya, ikkinchisi ism).
Tekshiruvda katta-kichik harf va tutuq belgilari (`'`, `’`, `‘`) e’tiborga olinmaydi.

## Sozlamalar (`index.html` ichida)

| Nom | Vazifasi |
| --- | --- |
| `TIME_LIMIT_MIN` | test vaqti, daqiqada (hozir `15`) |
| `Q[...].w` | savolning bali |
| `Q[...].c` | to‘g‘ri javob: `0`=A, `1`=B, `2`=C, `3`=D |
| `pct>75` (`finish` funksiyasida) | tabrik effekti chegarasi |

## 🎮 Bamboozle (sinfdagi o‘yin moduli)

Bamboozle **shu `index.html` faylning ichida** (alohida fayl yo‘q). Bosh sahifadagi **🎮 BAMBOOZLE** tugmasi (yoki menyudagi havola) uni to‘liq ekranli bo‘lim sifatida ochadi; to‘g‘ridan-to‘g‘ri ochish uchun manzil oxiriga `#bamboozle` qo‘shing. Barcha CSS klasslari `.bamboozle-` prefiksi bilan, shuning uchun asosiy sayt bilan to‘qnashmaydi. Kod `index.html` oxiridagi "BAMBOOZLE — JavaScript" blokida.

- **BEKALI CODE** bilan kiriladi (noto‘g‘ri bo‘lsa: `Invalid Bekali Code`). Kodni o‘zgartirish: shu blok boshidagi `const BEKALI_CODE = 'BEKALI';`
- 1–5 ta jamoa, jamoa nomlari, har bir jamoaga rang va ikonka; scoreboard doim ko‘rinib turadi
- 4 × 5 = 20 ta karta; ichida 14 ta savol + 6 ta yashirin maxsus karta (soni sozlanadi; maxsus kartalar ochilmaguncha ko‘rinmaydi)
- 20 ta savol `QUESTIONS` ro‘yxatida (savol, javob, ball)
- Maxsus kartalar: 🎁 BONUS, 💥 DOUBLE, 🔥 TRIPLE, ➕ EXTRA, ➖ LOSE, 💰 STEAL, 🎲 RANDOM, 🔄 SWAP
- To‘g‘ri/noto‘g‘ri, ixtiyoriy minus ball, savol ballini qo‘lda tanlash, taymer (10/20/30/45/60/OFF)
- O‘qituvchi paneli: Add/Remove Points, Bonus, Steal, Swap, Next Team, **Undo** (oxirgi 40 amal), Pause, End Game; Game History
- Reset, Fullscreen, ovoz ON/OFF (ovozlar brauzerning o‘zida yaratiladi), konfetti bilan g‘olib e’loni
- Klaviatura: `F` fullscreen · `R` tasodifiy karta · `Esc` oynani yopish · `Space` (Show Answer / Next Team / Resume) · `Enter` tasdiqlash
- Holat `localStorage` da saqlanadi: sahifa yangilansa o‘yin davom ettirish mumkin (kod qayta so‘raladi)

**Logo:** `assets/lexon-logo.png` fayliga joylang (yo‘l `LOGO_URL` o‘zgaruvchisida). Fayl bo‘lmasa, zaxira "LEXON" belgisi ko‘rinadi.

**Eslatma:** BEKALI CODE haqiqiy autentifikatsiya emas. Kod fayl ichida turadi, bu faqat sinfdagi o‘yinga kirish uchun oddiy to‘siq.

## Profil, "Fan haqida" va "Natijani tekshirish"

- Ro‘yxatdagi talaba ism-familiyasini to‘g‘ri yozgach, **o‘z profiliga** kiradi. Test avtomatik boshlanmaydi: profildagi **Testni boshlash** tugmasi bosilgandan keyin boshlanadi
- Profilda **Fan haqida**, **Bosh sahifa** va **Testni boshlash** tugmalari bor; **Profildan chiqish** orqali boshqa talaba kirishi mumkin
- **Fan haqida** sahifasida fan bo‘yicha qisqa ma’lumot yozilgan (bosh sahifadan ham, profildan ham ochiladi)
- Barcha sahifalarda **Bosh sahifa** tugmasi ko‘rinib turadi. Faqat test ishlash paytida (va tabrik effekti vaqtida) ko‘rinmaydi
- **Natijani tekshirish** bo‘limiga kirishdan oldin kirish kodi so‘raladi (hozirgi kod: `Bekali`, katta-kichik harf farqi yo‘q). Kod saytda ochiq matn emas, hash ko‘rinishida saqlanadi

### Kirish kodini almashtirish

```
python3 -c "import hashlib;print(hashlib.sha256(('LEXO-GATE-2026|'+input('Yangi kod: ').lower().strip()).encode()).hexdigest())"
```

Chiqqan qiymatni `index.html` dagi `GATE_HASH='...'` o‘rniga qo‘ying. Eslatma: kod tekshiruvi ham brauzer ichida ishlaydi, shuning uchun bu oddiy to‘siq, to‘liq himoya emas.

## Tasdiq kodi haqida muhim eslatma

Kod natija ma’lumotlariga (ism, foiz, ball, vaqt, sana, tasodifiy son) bog‘langan va imzolangan, shuning uchun matn qo‘lda o‘zgartirilsa, tekshiruv buni aniqlaydi. Lekin sayt to‘liq brauzerda ishlagani uchun imzo kaliti kod ichida turadi. Dasturlashni biladigan odam uni topib, soxta kod yasashi mumkin. To‘liq himoya uchun natijalar serverda saqlanishi va tekshirilishi kerak.

## GitHub Pages orqali e’lon qilish

1. GitHub’da yangi **Public** repozitoriy yarating.
2. Shu papkadagi barcha fayllarni yuklang.
3. **Settings → Pages → Deploy from a branch → `main` / `(root)` → Save**.
4. 1–2 daqiqadan keyin sayt `https://FOYDALANUVCHI.github.io/REPO-NOMI/` manzilida ochiladi.
