# Termux-Tool

Framework ofensivo de **reconocimiento, OSINT, escaneo y análisis de seguridad**,
escrito **100% en Python de la biblioteca estándar**. Sin dependencias `pip`, sin
root y **sin binarios externos**: los protocolos (DNS, WHOIS, TCP, TLS, HTTP) están
implementados a mano con `socket`, `ssl` y `urllib`.

Pensado para funcionar al **100% en Termux (Android)** y también en **Kali/Debian**.

<p align="center">
  <img src="assets/termux-tool-logo.jpg" alt="Termux Tool" width="400">
</p>

---

## Características

- **47 herramientas** repartidas en 5 categorías.
- **Script central** (`termux-tool.py`) que orquesta los módulos, que viven separados en `modules/`.
- Tema de color **naranja/rojo** con ANSI 256 y ASCII art de murciélago (silueta real convertida a bloques Unicode).
- **Cero dependencias externas** → no pelea con el gestor de paquetes de Termux.
- **Sin root**: el escaneo usa TCP `connect()` (no SYN raw), el DNS es cliente UDP.
- Multihilo (`concurrent.futures`) para escaneos rápidos.

---

## Instalación

### Termux (Android)
```bash
pkg install python git -y
git clone https://github.com/nostraxiten/Termux-Tool
cd Termux-Tool
python termux-tool.py
```

### Kali / Debian
```bash
sudo apt install python3 -y
cd Termux-Tool
python3 termux-tool.py
```

O simplemente:
```bash
bash install.sh
```

---

## Uso

Lanza el menú central:
```bash
python termux-tool.py
```

Cada módulo también se puede ejecutar suelto:
```bash
python modules/osint.py
python modules/active.py
```

Navegas con números; `0` vuelve atrás o sale. `Ctrl+C` corta la herramienta actual
sin cerrar el framework.

---

## Estructura

```
Termux-Tool/
├── termux-tool.py        # launcher central
├── core/
│   ├── banner.py         # paleta de color + ASCII art
│   ├── ui.py             # menús y salida
│   └── net.py            # HTTP, DNS propio (UDP), WHOIS, sockets
├── modules/
│   ├── osint.py          # OSINT & recon
│   ├── passive.py        # escaneo pasivo
│   ├── active.py         # escaneo activo / agresivo
│   ├── analysis.py       # análisis seguridad & red
│   └── basictools.py     # utilidades básicas
├── data/
│   ├── subdomains.txt    # wordlist subdominios
│   └── dirs.txt          # wordlist rutas web
├── install.sh
├── requirements.txt      # (vacío: todo es stdlib)
└── README.md
```

---

## Catálogo de herramientas

**OSINT & Reconocimiento**
1. IP / Host Info (geolocalización, ISP, ASN)
2. WHOIS (recursivo vía IANA, socket puerto 43)
3. Registros DNS (resolver propio: A, AAAA, MX, NS, TXT, SOA, CNAME)
4. Reverse DNS (PTR)
5. Certificado SSL/TLS (emisor, validez, SANs, versión/cipher)
6. GitHub OSINT (perfil + repos + lenguajes)
7. Wayback Machine (URLs archivadas)
8. Fingerprint HTTP / detección de tecnologías
9. Phone Info offline (E.164, código de país)
10. Username OSINT (presencia en ~18 redes)

**Escaneo Pasivo**
1. DNS Enum (registros + hostnames comunes)
2. Subdominios vía crt.sh (Certificate Transparency)
3. robots.txt & sitemap.xml
4. security.txt
5. Auditoría de cabeceras de seguridad (con nota A–F)
6. Análisis de cookies (Secure/HttpOnly/SameSite)
7. Email harvester
8. Detección de CMS por rutas
9. Meta info del HTML (generator, comentarios)

**Escaneo Activo / Agresivo**
1. Escaneo rápido (top ~50 puertos)
2. Escaneo de rango de puertos
3. Banner grabbing
4. Barrido de red / host sweep (TCP ping)
5. Directory bruteforce
6. Subdomain bruteforce
7. HTTP methods
8. Web crawler
9. VHost scan
10. Detección de servicios

**Análisis Seguridad & Red**
1. Info de red local (IP salida, gateway, IP pública)
2. IP pública + geo
3. Fortaleza de contraseña (entropía)
4. Generador de contraseñas (secrets)
5. Generador de hashes (md5→blake2b)
6. Identificador de hash
7. Encoder/Decoder (base64/hex/url/rot13)
8. Test de conectividad TCP
9. HTTP status / uptime
10. TCP latency (ping por TCP)

**Toolkit Seguridad Básica**
1. MAC aleatoria
2. Tokens / UUID
3. Hash de fichero
4. Entropía de texto (Shannon)
5. Cifrados clásicos (Caesar/XOR/ROT13)
6. Generador de wordlist
7. Generador de User-Agents
8. Calculadora de subred (CIDR)

---

## Aviso legal

Esta herramienta es para **auditar sistemas propios o con autorización explícita**,
y para aprendizaje. Escanear infraestructura de terceros sin permiso puede ser ilegal.
El uso que hagas es tu responsabilidad.

---

*by [@nostraxiten](https://github.com/nostraxiten)*
