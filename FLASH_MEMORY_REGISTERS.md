## 1. FLASH Access Control Register (FLASH_ACR)

* **Adres Ofseti:** 0x00
* **Amacı :** Flash erişim sürelerini ve hızlandırma özelliklerini (prefetch, cache) kontrol eder.

| Bit | Adı | Açıklama |
|--|--|--|
| 12 | **DCRST** (Data Cache Reset) | Veri önbelleğini sıfırlamak için kullanılır. **1** yazıldığında veri önbelleği temizlenir. (Önceden devre dışı bırakılmış olması gerekir.) |
| 11 | **ICRST** (Instruction Cache Reset) | Komut önbelleğini sıfırlamak için kullanılır. **1** yazıldığında komut önbelleği temizlenir. (Önceden devre dışı bırakılmış olması gerekir.) |
| 10 | **DCEN** (Data Cache Enable) | Veri önbelleğini açar/kapatır. **1** yapılırsa veri önbelleği aktif olur. |
| 9 | **ICEN** (Instruction Cache Enable) | Komut önbelleğini açar/kapatır. **1** yapılırsa komut önbelleği aktif olur. | 
| 8 | **PRFTEN** (Prefetch Enable) | Flash bellekten gelen verileri önceden getirme mekanizmasını açar. **1** yapılırsa prefetch açılır. |
| 3:0 | **LATENCY** | CPU saat hızına göre Flash erişim gecikmesini belirler. Daha yüksek hızlarda çalışırken wait-state (bekleme döngüsü) eklenmesi gerekir. |

* **Kullanım :** CPU saat frekansına bağlı olarak wait - state ayarlanır. Prefetch, veri ve komut cache kullanımı etkinleştirilebilir.


------------------------------------------------------------------------------------------------------------------------------------------------------------

## 2. FLASH Key Register (FLASH_KEYR)

* **Adres Ofseti :** 0x04
* **Amacı :** Flash konrtol register'ını (FLASH_CR) açarak, programlama ve silme işlemlerine izin verir.

| Bit | Adı | Açıklama |
|--|--|--|
| 31:0 | **FKEYR** | FLASH_CR register'ını açmak için sırasıyla **0x45670123** ve **0xCDEF89AB** değerlerinin yazılması gerekir. |

* **Kullanım :** Flash'ı programlamak veya silmek için önce bu register üzerinden kilidin açılması gerekir.

------------------------------------------------------------------------------------------------------------------------------------------------------------

## 3. FLASH Option Key Register (FLASH_OPTKEYR)

* **Adres Ofseti :** 0x08
* **Amacı :** Kullanıcı yapılandırma (option byte) sektörüne erişim sağlar.

| Bit | Adı | Açıklama |
|--|--|--|
| 31:0 | **OPTKEYR** | FLASH_OPTCR register'ını açmak için sırasıyla **0x08192A3B** ve **0x4C5D6E7F** yazılması gerekir.

* **Kullanım :** Kullanıcı yapılandırma seçeneklerini değiştirmek için bu register aracılığıyla kilidin açılması gerekir.

------------------------------------------------------------------------------------------------------------------------------------------------------------

## 4. FLASH Status Register (FLASH_SR)

* **Adres Ofseti :** 0x0C
* **Amacı :** Flash işlemlerinin durumunu gösterir ve hata bilgisi verir.

| Bit | Adı | Açıklama |
|--|--|--|
| 16 | **BSY** | Flash bellekte işlem olup olmadığını gösterir. **1** ise Flash meşgul, **0** ise işlem tamamlanmış. |
| 8 | **RDERR** | Okuma koruması (PCROP) etkinleştirilmiş bir bölgeye erişildiğinde **1** olur |
| 7 | **PGSERR** | Programlama sırasında geçersiz bir işlem yapılmışsa **1** olur. |
| 6 | **PGPERR** | Programlama sırasında boyut uyuşmazlığı varsa **1** olur. |
| 5 | **PGAERR** | Programlama hizalama hatası oluştuğunda **1** olur. |
| 4 | **WRPERR** | Yazma koruması olan bir bölgeye yazılmaya çalıştığında **1** olur. | 
| 1 | **OPERR** | Geçersiz bir Flash işlemi yapıldığında **1** olur. | 
| 0 | **EOP** | Flash işlemi başarıyla tamamlandıysa 1 olur. |

* **Kullanım :** Flash işlemleri öncesi ve sonrası hatalar ve işlemlerin tamamlanıp tamamlanmadığını kontrol etmek için kullanılır.

------------------------------------------------------------------------------------------------------------------------------------------------------------

## 5. FLASH Control Register (FLASH_CR)

* **Adres Ofseti :** 0x10
* **Amacı :** Flash programlama ve silme işlemlerini yönetir.

| Bit | Adı | Açıklama |
|--|--|--|
| 31 | **LOCK** | Flash kontrol register'ını kilitler. Açmak için **FLASH_KEYR** register'ına anahtar yazılmalı. |
| 25 | **ERRIE** | Hata oluştuğunda kesme (interrupt) oluşturulmasını sağlar. |
| 24 | **EOPIE** | İşlem tamamlandığında kesme oluşturulmasını sağlar. |
| 16 | **STRT** | Flash silme işlemini başlatır. |
| 9:8 | **PSIZE** | Programlama yapılacak veri büyüklüğünü belirler : 00 = 8-bit, 01 = 16-bit, 10 = 32-bit, 11 = 64-bit |
| 6:3 | **SNB** | Silinecek sektörün numarasını belirler. |
| 2 | **MER** | Tüm Flash belleği silmek için kullanılır. |
| 1 | **SER** | Seçili sektörü silmek için kullanılır. |
| 0 | **PG** | Flash yazma işlemini başlatır. |

* **Kullanım :** Flash programlama veya silme işlemi yapmak için bu register kullanılır.

------------------------------------------------------------------------------------------------------------------------------------------------------------

## 6. FLASH Option Control Register (FLASH_OPTCR)

* **Adres Ofseti :** 0x14
* **Amacı :** Kullanıcı seçeneklerini (option bytes) değiştirmek için kullanılır.

| Bit | Adı | Açıklama |
|--|--|--|
| 31 | **SPRMOD** | Koruma modunu seçer. **0** = Yazma koruması, **1** = PCROP koruması. |
| 23:16 | **nWRP** | Yazma koruması etkin olan sektörleri belirler. |
| 15:8 | **RDP** | Okuma koruma seviyesini belirler. **0xAA** = Kapalı, **0xCC** = Seviye 2, diğerleri = Seviye 1. |
| 7:5 | **USER** | Kullanıcı yapılandırmalarını içerir. |
| 3:2 | **BOR_LEV** | Brown-out reset (BOR) seviyesini belirler. | 

* **Kullanım :** Okuma ve yazma koruması gibi güvenlik önlemlerini yapılandırmak için kullanılır.

------------------------------------------------------------------------------------------------------------------------------------------------------------

## GENEL ÖZET

* **FLASH_ACR :** Flash erişimini hızlandırma ve wait-state ayarları.
* **FLASH_KEYR :** Flash kontrol register'ının kilidini açma.
* **FLASH_OPTKEYR :** Option byte değişikliklerini açma.
* **FLASH_SR :** Flash işlemlerinin durumu ve hataları.
* **FLASH_CR :** Flash programlama ve silme işlemlerini başlatma.
* **FLASH_OPTCR :** Okuma/yazma koruması gibi güvenlik ayarları.

* **Bu registerlar sayesinde STM32 mikrodenetleyicinin Flash belleği verimli bir şekilde yönetilebilir.**






























































                        
      



