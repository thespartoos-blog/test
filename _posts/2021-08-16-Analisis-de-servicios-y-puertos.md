---
layout: post
title: Host and Port Discovery
author: thespartoos
categories: [ Articulo ]
image: assets/images/Analisis-de-servicios-y-puertos/nmap.jpg
beforetoc: "Aquí puedes aprender como enumerar puertos y como descubrir hosts activos en red utilizando una serie de utilidades, algunas diseñadas y otras son creadas manualmente por tí"
toc: no
---

**BIENVENIDOS A MI PRIMER POST**
---
<br>
Aquí puedes aprender como enumerar puertos y como descubrir hosts activos en 
red utilizando una serie de utilidades, algunas diseñadas y otras son creadas 
manualmente por ti

- 1 - PUERTOS
- 2 - HOSTS

## 1 - PORTSCAN MANUAL

```bash
#!/bin/bash

function ctrl_c(){
	echo -e "\n\n[!] Saliendo....\n"
	tput cnorm; exit 1
}

# Ctrl+C

trap ctrl_c INT
tput civis

for port in $(seq 1 65535); do
	timeout 1 bash -c "echo '' > /dev/tcp/IP/$port" 2>/dev/null && echo "[+] Puerto $port - ABIERTO" &
done; wait
tput cnorm
```

## 1 - Puertos NMAP

- Modo --> agresivo y ruidoso ⚠️  `nmap -p- --open -T5 -v -n [IP]`
- Modo --> Rápido enviando 5000 p/s 💨 `nmap -sS --min-rate 5000 -p- --open -vvv -n -Pn [IP]`
- Modo --> Enumerar servicio y versión 🔥 `nmap -sC -sV -p22,80,443 [IP]`

## 2 - HOST DISCOVERY

```javascript
#!/bin/bash

function ctrl_c(){
	echo -e "\n\n[!] Saliendo....\n"
	tput cnorm; exit 1
}

# Ctrl+C
trap ctrl_c INT

tput civis
for host in $(seq 1 254); do
	timeout 5 bash -c "ping -c 1 192.168.1.$host &>/dev/null " && echo "[+] HOST 192.168.1.$host - ACTIVO" &
done; wait
tput cnorm
```
## 2 - HOST NMAP

```bash
nmap -sP 192.168.1.0/24
```
```bash
nmap -sn 192.168.1.0/24
```
