# 🧠 Nettverk – Grunnleggende om IP-adresser og nettverksklasser

## 📡 Innstillinger på nettverkskortet
Når du kobler en PC til et nettverk, trenger nettverkskortet disse innstillingene:

- **IP-adresse**: Identifiserer enheten på nettverket. Består av:
  - **Nettverks-ID** (felles for alle i samme nettverk)
  - **Klient-ID** (unik for hver enhet)
- **Nettverksmaske**: Bestemmer hvilken del av IP-en som er nettverk og hvilken som er klient.
- **Default Gateway**: Ruterens adresse – brukes for å nå andre nettverk, f.eks. internett.
- **DNS-server**: Oversetter domenenavn (f.eks. `google.com`) til IP-adresser.

---

## 📘 Eksempel: IP 192.168.1.1
**Desimal til binær konvertering:**
- Oktett 1: 192 = `11000000`
- Oktett 2: 168 = `10101000`
- Oktett 3: 1 = `00000001`
- Oktett 4: 1 = `00000001`

---

## 🧬 IP-Klasser (Legacy-klassifisering)
> Brukes sjelden direkte i moderne nettverk, men viktig å kunne.

### Klasse A – Store nettverk
- **Binær start**: `0XXXXXXX`
- **Desimalområde**: `0.0.0.0 – 127.255.255.255`
- **Standard nettverksmaske**: `255.0.0.0` eller `/8`

### Klasse B – Mellomstore nettverk
- **Binær start**: `10XXXXXX`
- **Desimalområde**: `128.0.0.0 – 191.255.255.255`
- **Standard nettverksmaske**: `255.255.0.0` eller `/16`

### Klasse C – Små nettverk
- **Binær start**: `110XXXXX`
- **Desimalområde**: `192.0.0.0 – 223.255.255.255`
- **Standard nettverksmaske**: `255.255.255.0` eller `/24`

### Klasse D – Multicast
- **Binær start**: `1110XXXX`
- **Desimalområde**: `224.0.0.0 – 239.255.255.255`
- **Bruk**: Multicast-grupper (ikke vanlig ruting)
- **Ingen nettverksmaske**

### Klasse E – Eksperimentell
- **Binær start**: `1111XXXX`
- **Desimalområde**: `240.0.0.0 – 255.255.255.255`
- **Bruk**: Reserved for forskning/testing
- **Ingen nettverksmaske**

---

## ⚙️ Bitvis AND – Hvordan subnett fungerer
For å finne nettverksdelen av en IP-adresse, brukes en **bitvis AND** mellom IP og nettverksmaske:

**Eksempel:**
```
IP:              192.168.1.10   → 11000000.10101000.00000001.00001010
Nettverksmaske:  255.255.255.0 → 11111111.11111111.11111111.00000000
---------------------------------------------------------------
Nettverks-ID:                    → 11000000.10101000.00000001.00000000
                             = 192.168.1.0
```

---

## 📏 CIDR-notasjon (Classless Inter-Domain Routing)
Skrives som `/X` der X er antall bits satt til `1` i nettverksmasken.

| CIDR | Nettverksmaske     | Antall adresser |
|------|--------------------|------------------|
| /8   | 255.0.0.0          | 16 777 216       |
| /16  | 255.255.0.0        | 65 536           |
| /24  | 255.255.255.0      | 256              |
| /32  | 255.255.255.255    | 1 (1 IP)         |

- **/24** er vanlig i lokale nettverk (LAN)
- **/32** brukes for én spesifikk IP, f.eks. i brannmurregler

