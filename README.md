# Cybersecurity - Brute Force ☠️
Simulando um Ataque de Brute Force de Senhas com Medusa e Kali Linux

## 1º PASSO - Identificando vulnerabilidades 👁️

#### Descubra o seu IP e a Máscara de Rede:
> $ ip a

Procure algo como 192.168.145.36/24.

• **Seu IP**: 192.168.145.36  
• **Sua Notação CIDR**: /24  
• **Sua Faixa de Rede**: 192.168.145.0/24

// Determine a Faixa de Escaneamento a partir da sua Notação CIDR, neste caso **/24**.

#### Use o "nmap" para Escaneamento Rápido

> $ nmap -sn 192.168.145.0/24

**Exemplo de Saída Esperada**:
```
Starting Nmap 7.93 ( https://nmap.org ) at 2025-00-00 10:00 -03
Nmap scan report for 192.168.145.1     ← ROTEADOR/GATEWAY
Host is up (0.0031s latency).
MAC Address: 00:1A:2B:3C:4D:5E
Nmap scan report for 192.168.145.13    ← SEU DISPOSITIVO
Host is up (0.0001s latency).
MAC Address: 0A:1B:2C:3D:4E:5F
Nmap scan report for 192.168.145.20
Host is up (0.0055s latency).
MAC Address: A1:B2:C3:D4:E5:F6
Nmap scan report for 192.168.145.13    ← DISPOSITIVO DO ALVO 👾
Host is up (0.0092s latency).
MAC Address: F1:E2:D3:C4:B5:A6
Nmap scan report for 192.168.145.101
Host is up (0.0118s latency).
MAC Address: 11:22:33:44:55:66
Nmap done: ... scanned in 2.50 seconds
```
## 2º PASSO - Explorando vulnerabilidades 👨‍💻

#### Primeiro vamos testar as conexões e portas abertas do IP do Alvo (192.168.145.13)

> $ ping -c 3 192.168.145.13

Onde:  
**-c** → count (contagem) | **3**  → quantidade de pings

#### Testando conexão bem-sucedida, vamos verificar as portas abertas:

> $ nmap -sV -p **21,22,80,445,139** 192.168.145.13

Onde:  
**nmpa** (mapear) **-sV** (Verificação de Serviço) **-p** (Porta)  

**21** → Porta do Protocolo FTP  
**22** → Porta do Protocolo SSH  
**80** → Porta do Protocolo HTTP  
**445** → Porta do Protocolo TCP  
**139** → Antiga Porta do Protocolo TCP/IP, também associada ao Protocolo SMB  

... **Fique à vonta para testar outras portas** ...

**Exemplo de Saída Esperada**:
```
PORT       STATE      SERVICE          VERSION
21/tcp     open       ftp              vsftcp 2.3.4
22/tcp     open       ssh              OpenSSH 4.7p1 Debain...
Service detection performed. Please report any incorrect results
at http://nmap.org/submit/.
Nmap done: 1 IP adress (1 host up) scanned in 24.71seconds
```

