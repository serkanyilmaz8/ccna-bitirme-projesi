# 🌐 Kurumsal Ağ Tasarımı ve Uygulaması (CCNA Bitirme Projesi)
<img width="1423" height="463" alt="bitirme-projesi-resim" src="https://github.com/user-attachments/assets/72343866-081c-4232-b5cc-b5d77e8b4411" />


Bu proje, **Cisco Packet Tracer** kullanılarak tasarlanmış; Merkez (BİM) ve iki şube (A Blok, B Blok) yapısından oluşan kapsamlı bir kurumsal ağ simülasyonudur. Proje; anahtarlama (switching), yönlendirme (routing), kablosuz ağ (wireless), güvenlik ve servis yapılandırmalarını içermektedir.

---

## 🚀 Proje Özellikleri

Bu topolojide aşağıdaki ağ teknolojileri ve protokolleri aktif olarak yapılandırılmış ve test edilmiştir:

### 🔗 Layer 2 (Switching)
* **VLAN & Trunking:** Departmanlar (Yönetim, Personel, Misafir) için mantıksal ağ ayrımı.
* **VTP (VLAN Trunking Protocol):** VLAN'ların merkezi olarak yönetilmesi ve dağıtılması.
* **STP (Spanning Tree Protocol):** Döngüleri engellemek için Root Bridge (PAŞA Switch) optimizasyonları.
* **EtherChannel:** Bant genişliği artırımı ve yedeklilik (BİM Omurga - Kat1 arası LACP/PAgP).
* **Port Security:** İzinsiz erişimleri engellemek için port bazlı MAC adresi sabitleme (Sticky & Restrict modları).

### 🛣️ Layer 3 (Routing)
* **OSPF (Open Shortest Path First):** Bloklar arası dinamik yönlendirme (Area 0 - Backbone).
* **Router-on-a-Stick:** Tek bir fiziksel arayüz üzerinden VLAN'lar arası yönlendirme (Inter-VLAN Routing).
* **DHCP Relay (IP Helper):** Şubelerdeki istemcilerin Merkezdeki (BİM) DHCP sunucusundan otomatik IP alması.

### 📡 Wireless (Kablosuz Ağ)
* **WLC (Wireless LAN Controller):** A Blok, B Blok ve BİM için ayrı WLC 2504 yapılandırması.
* **Lightweight APs (LAP):** WLC tarafından yönetilen "Thin" Access Point mimarisi.
* **SSID & Security:** WPA2-PSK Enterprise güvenliği ile çoklu SSID yayını (Yönetim, Personel, Misafir) ve VLAN eşleştirmeleri.

### 🛡️ Güvenlik ve Servisler
* **ACL (Access Control Lists):** Misafir VLAN'larının, hassas Yönetim (MGMT) ağlarına erişiminin kısıtlanması.
* **Syslog:** Tüm router ve switch loglarının merkezi bir sunucuda toplanması (Debugging seviyesinde).
* **TFTP:** Cihazların `running-config` dosyalarının yedeklenmesi.
* **SSH:** Cihazlara güvenli uzaktan yönetim erişimi (Telnet yerine şifreli bağlantı).

---

## 📊 IP ve VLAN Planlaması

Ağ yapısı, hiyerarşik bir düzen içinde aşağıdaki şemaya göre adreslenmiştir:

| Blok | VLAN ID | VLAN Adı | Alt Ağ (Subnet) |
| :--- | :---: | :--- | :--- |
| **A Blok** | `10` | Yonetim-A | 192.168.10.0/24 |
| | `11` | Personel-A | 192.168.11.0/24 |
| | `12` | Misafir-A | 192.168.12.0/24 |
| | `19` | MGMT (WLC/AP) | 192.168.19.0/24 |
| **BİM** | `20` | Server Farm | 192.168.20.0/24 |
| | `21` | DHCP-TFTP | 192.168.21.0/24 |
| | `22` | Bim-Wifi | 192.168.22.0/24 |
| | `29` | MGMT | 192.168.29.0/24 |
| **B Blok** | `30` | Yonetim-B | 192.168.30.0/24 |
| | `31` | Personel-B | 192.168.31.0/24 |
| | `32` | Misafir-B | 192.168.32.0/24 |
| | `39` | MGMT (WLC/AP) | 192.168.39.0/24 |

---

## 🔑 Erişim Bilgileri (Credentials)

Simülasyonu test etmek ve cihazlara erişmek için aşağıdaki giriş bilgilerini kullanabilirsiniz:

### Router ve Switch (CLI)
```text
Username      : sinan
Password      : cisco
Enable Secret : cisco
