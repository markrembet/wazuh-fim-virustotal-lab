# Home Lab Wazuh — FIM + VirusTotal + Active Response

[![Wazuh](https://img.shields.io/badge/Wazuh-4.14.x-blue)](https://wazuh.com)
[![Lab](https://img.shields.io/badge/Type-Home%20Lab-success)]()
[![Focus](https://img.shields.io/badge/Focus-FIM%20%7C%20Threat%20Intel%20%7C%20Active%20Response-orange)]()

Dokumentasi laboratorium keamanan siber untuk demonstrasi **File Integrity Monitoring (FIM)**, integrasi **VirusTotal**, dan **Active Response** otomatis menggunakan platform open-source **Wazuh**.

> Lab ini dirancang untuk pembelajaran dan portfolio praktik SIEM, endpoint detection, dan threat intelligence integration.

---

## Tujuan Lab

Setelah mengikuti panduan ini, Anda dapat:

- Menginstal Wazuh Manager + Dashboard via OVA VirtualBox
- Mendeploy dan memverifikasi Wazuh Agent (Linux)
- Mengonfigurasi FIM (syscheck) real-time pada direktori target
- Mengintegrasikan VirusTotal API untuk analisis reputasi file
- Membangun script Active Response yang menghapus file berbahaya secara otomatis
- Melakukan pengujian end-to-end dengan file uji EICAR

## Skills yang Ditunjukkan

| Area | Detail |
|------|--------|
| SIEM & Detection | Wazuh Manager, Agent, Dashboard |
| File Integrity | syscheck realtime, check_all |
| Threat Intelligence | VirusTotal API integration |
| Response Automation | Active Response script (bash + jq) |
| System Admin | Linux service, permission, networking |
| Dokumentasi | Technical writing untuk portfolio |

## Arsitektur Singkat

```
┌─────────────────────────┐          ┌──────────────────────────┐
│   Wazuh Server (OVA)    │◄────────►│   Wazuh Agent (Linux)    │
│  Manager + Indexer +    │  1514/tcp│  FIM: /home/.../Downloads│
│  Dashboard              │          │  Script: remove-threat.sh│
│  IP: 192.168.100.119    │          │                          │
└─────────────────────────┘          └──────────────────────────┘
         │
         │ hash → VirusTotal API
         ▼
   Alert rule 87105 → Active Response → File dihapus
```

## Struktur Repositori yang Disarankan

```
wazuh-fim-virustotal-lab/
├── README.md                          # File ini
├── docs/
│   └── Wazuh-Home-Lab-FIM-VirusTotal-Guide.pdf
```

## Cara Menjalankan Lab (Ringkas)

1. **Import OVA** Wazuh ke VirtualBox → start → login `wazuh-user` / `wazuh`
2. **Login Dashboard** → `admin` / `admin` → Deploy new agent
3. **Install agent** di VM Linux → enable & start service
4. **Konfigurasi FIM** (via Group atau ossec.conf) pada `/home/wazuh/Downloads`
5. **Tambah integrasi VirusTotal** di manager (`ossec.conf`) + restart
6. **Pasang script** `remove-threat.sh` di agent + daftarkan Active Response di manager
7. **Uji** dengan file EICAR → amati event FIM + Threat Hunting + penghapusan otomatis

Panduan lengkap langkah-demi-langkah tersedia di:

- [PDF Guide](docs/Wazuh-Home-Lab-FIM-VirusTotal-Guide.pdf)
- [DOCX Guide](docs/Wazuh-Home-Lab-FIM-VirusTotal-Guide.docx) *(jika Anda menyertakan)*

## Keamanan

- Segera ganti password default
- Jangan commit **API key VirusTotal** ke repositori
- Permission `777` hanya untuk lab; produksi harus lebih ketat
- Gunakan **EICAR** untuk pengujian, bukan malware nyata

## Referensi

- [Wazuh Documentation](https://documentation.wazuh.com)
- [VirusTotal API](https://docs.virustotal.com)
- [EICAR Test File](https://www.eicar.org)
- [Wazuh GitHub](https://github.com/wazuh/wazuh)

## Lisensi

Konten dokumentasi lab ini dapat digunakan untuk keperluan pembelajaran dan portfolio.  
Wazuh sendiri berlisensi GPLv2. Hormati Terms of Service VirusTotal saat menggunakan API.

---

**Happy learning & stay secure.**
