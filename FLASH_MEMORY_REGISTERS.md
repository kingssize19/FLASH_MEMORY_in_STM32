## 1. FLASH Access Control Register (FLASH_ACR)

* **Adres Ofseti:** 0x00
* **Amacı :** Flash erişim sürelerini ve hızlandırma özelliklerini (prefetch, cache) kontrol eder.

| Bit | Adı | Açıklama |
|--|--|--|
| 12 | **DCRST** (Data Cache Reset) | Veri önbelleğini sıfırlamak için kullanılır. 1 yazıldığında veri önbelleği temizlenir. (Önceden devre dışı bırakılmış olması gerekir.) |
| 11 | **ICRST** (Instruction Cache Reset) | Komut önbelleğini sıfırlamak için kullanılır. 1 yazıldığında komut önbelleği temizlenir. (Önceden devre dışı bırakılmış olması gerekir.) |
| 10 | **DCEN** (Data Cache Enable) | Veri önbelleğini açar/kapatır. 1 yapılırsa veri önbelleği aktif olur. |
| 9 | **ICEN** (Instruction Cache Enable) | Komut önbelleğini açar/kapatır. 1 yapılırsa komut önbelleği aktif olur. | 
| 8 | **PRFTEN** (Prefetch Enable) | Flash bellekten gelen verileri önceden getirme mekanizmasını açar. 1 yapılırsa prefetch açılır. |
| 3:0 | **LATENCY** | CPU saat hızına göre Flash erişim gecikmesini belirler. Daha yüksek hızlarda çalışırken wait-state (bekleme döngüsü) eklenmesi gerekir. |

* **Kullanım :** CPU saat frekansına bağlı olarak wait - state ayarlanır. Prefetch, veri ve komut cache kullanımı etkinleştirilebilir.


------------------------------------------------------------------------------------------------------------------------------------------------------------




                        
      



