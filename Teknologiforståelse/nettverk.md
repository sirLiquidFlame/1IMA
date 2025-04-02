# 🧠 Nettverk – Grunnleggende om IP-adresser og nettverksklasser

## 📡 Innstillinger på nettverkskortet
Når du kobler en PC til et nettverk, trenger nettverkskortet disse innstillingene:

- **IP-adresse**: Identifiserer enheten på nettverket. Består av:
  - **Nettverks-ID** (felles for alle i samme nettverk)
  - **Klient-ID** (unik for hver enhet)
- **Nettverksmaske**: Bestemmer hvilken del av IP-en som er nettverk og hvilken som er klient.
- **Default Gateway**: Ruterens adresse – brukes for å nå andre nettverk, f.eks. internett.
- **DNS-server**: Oversetter domenenavn (f.eks. `google.com`) til IP-adresser.
- **MAC-adresse**: Maskinvareadresse som er unik for hvert nettverkskort. Brukes for identifikasjon på datalink-laget.

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

---

## 🛠️ Andre viktige nettverksbegreper

### DHCP (Dynamic Host Configuration Protocol)
- Automatisk tildeling av IP-adresse, gateway og DNS til klienter.
- Brukes i de fleste hjemmenettverk via ruteren.
- Prosess:
  1. **DHCP Discover**: Klienten sender forespørsel (broadcast).
  2. **DHCP Offer**: Server svarer med forslag til IP.
  3. **DHCP Request**: Klienten aksepterer IP-en.
  4. **DHCP Acknowledge**: Server bekrefter og tildeler IP-en.

### NAT (Network Address Translation)
- Oversetter private IP-adresser (f.eks. 192.168.x.x) til en offentlig IP på internett.
- Gjør at flere enheter kan dele samme offentlige IP.

### Private IP-adresser
Brukes internt i nettverk, ikke rutbare på internett.
- **Klasse A**: 10.0.0.0 – 10.255.255.255
- **Klasse B**: 172.16.0.0 – 172.31.255.255
- **Klasse C**: 192.168.0.0 – 192.168.255.255

### Ping og ICMP
- Ping brukes for å teste om en annen enhet er tilgjengelig på nettverket.
- Bruker ICMP-protokollen for å sende "echo request" og motta "echo reply".

### ARP (Address Resolution Protocol)
- Brukes for å finne MAC-adressen til en IP-adresse i samme nettverk.
- Viktig i lokal kommunikasjon på Ethernet.

### Subnett og subnetting
- Deler et stort nettverk i mindre, mer oversiktlige deler.
- Viktig for økt sikkerhet, ytelse og struktur i større nettverk.

### TCP vs UDP
- Begge er transportprotokoller som brukes til å sende data over IP-nettverk.

#### TCP (Transmission Control Protocol):
- **Tilkoblingsbasert**: Oppretter en forbindelse før data sendes.
- **Pålitelig**: Sikrer at data kommer frem, i riktig rekkefølge, og uten tap.
- **Brukes av**: HTTP/HTTPS, FTP, SSH, e-post (SMTP, IMAP, POP3)

#### UDP (User Datagram Protocol):
- **Tilkoblingsløs**: Ingen håndtrykk eller bekreftelse.
- **Raskere, men upålitelig**: Ingen garanti for levering eller rekkefølge.
- **Brukes av**: D
