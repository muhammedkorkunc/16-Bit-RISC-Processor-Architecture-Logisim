cat << 'EOF' > README.md

# 💻 16-Bit RISC Processor Architecture in Logisim

### 5-Aşamalı Veri Yolu (Pipelined/Single-Cycle Datapath) 16-Bit İşlemci Tasarımı

Bu depo; Fatih Sultan Mehmet Vakıf Üniversitesi Bilgisayar Mühendisliği **Bilgisayar Mimarisi ve Organizasyonu (Computer Organization & Architecture)** dersi kapsamında Logisim simülatöründe sıfırdan tasarlanan **16-Bit RISC İşlemci** devre modelini (`.circ`) ve mimari analiz raporunu barındırır.

---

## 🛠️ Mimari Birimler & Veri Yolu Aşamaları

İşlemci, klasik beş aşamalı RISC yapısına uygun olarak tasarlanmıştır:

1. **Instruction Fetch (IF):** Program Sayacı (PC) ve Komut Belleği (Instruction Memory / RAM). Komutlar sırayla çekilir ve $PC + 1$ adresi hesaplanır.
2. **Instruction Decode (ID):** 16-bit komut formatındaki Opcode (5 bit), Hedef Yazmaç (DestReg - 3 bit), Kaynak Yazmaç (SrcReg - 3 bit) ve Immediate/Offset (5 bit) alanlarının çözümlenmesi ve 8 adet 16-bit genel amaçlı yazmacın ($R_0 - R_7$) denetimi.
3. **Execute (EX - ALU):** Aritmetik ve Mantık Birimi; çıkarma (`SUBI`) ve bit düzeyinde mantıksal VEYA (`ORI`) işlemlerini yürütür.
4. **Data Memory (MEM):** Veri Belleği; `STR` bellek yazma komutunda hesaplanan efektif adrese verinin kaydedilmesini sağlar.
5. **Write Back (WB):** ALU veya bellekten gelen sonucun ilgili hedef yazmaca geri yazılması.

---

## 📑 Desteklenen Özel Komut Kümesi

| Komut      | Sözdizimi (Syntax)      | Format (Bit Dağılımı)              | İşlem & Açıklama                                                 |
| :--------- | :---------------------- | :--------------------------------- | :--------------------------------------------------------------- |
| **`SUBI`** | `SUBI X1, X2, #imm`     | `[Opcode:5][Rd:3][Rn:3][Imm:5]`    | $X_1 = X_2 - \text{imm}$ (Sabit ile çıkarma)                     |
| **`ORI`**  | `ORI X3, X4, #imm`      | `[Opcode:5][Rd:3][Rn:3][Imm:5]`    | $X_3 = X_4 \lor \text{imm}$ (Bitwise OR)                         |
| **`STR`**  | `STR X0, [X6, #offset]` | `[Opcode:5][Rt:3][Rn:3][Offset:5]` | $\text{Mem}[X_6 + \text{offset}] = X_0$ (Belleğe yazma)          |
| **`BNE`**  | `BNE X1, X2, #label`    | `[Opcode:5][R1:3][R2:3][Label:5]`  | $X_1 \neq X_2 \implies PC = PC + \text{label}$ (Şartlı dallanma) |

---

## 🔒 Copyright & License / Telif Hakkı Bildirimi

Bu devre tasarımı, şematik çizimler ve proje raporu **Proprietary (Tescilli / Tüm Hakları Saklıdır)** lisansına tabidir.

```text
Copyright (c) 2026 Muhammed Emin Korkunç. All Rights Reserved.

Bu projedeki tüm Logisim devre blokları, kontrol ünitesi tasarımları,
ALU mimarisi ve rapor içerikleri Muhammed Emin Korkunç'a aittir.
Yazarın açık yazılı izni olmaksızın kısmen veya tamamen kopyalanması,
üzerinde değişiklik yapılması veya ticari/akademik amaçla izinsiz kullanımı kesinlikle yasaktır.

👨‍💻 Geliştirici / Author
Muhammed Emin Korkunç

GitHub: @muhammedkorkunc

LinkedIn: Muhammed Emin Korkunç

Email: muhammedemin.korkunc@gmail.com
```
