# ROTEIRO - VÍDEO 01: APRESENTAÇÃO DO PROJETO
## Canal: [Seu Canal]
**Data de Gravação:** [data]  
**Duração Estimada:** 8-10 minutos  
**Tema:** Apresentação da Infraestrutura de Rede com VMs em VirtualBox

---

## 🎯 OBJETIVO DO VÍDEO
Apresentar ao espectador a topologia de rede que será construída ao longo da série, explicando como cada componente funciona e se comunica.

---

## 📋 ROTEIRO DETALHADO

### **[ABERTURA - 0:00 a 0:30]**

**[Fala/Apresentação pessoal]**

"Oi, tudo bem? Meu nome é [seu nome] e bem-vindo ao meu canal!

Neste vídeo, vou apresentar um projeto completo de infraestrutura de rede que estou desenvolvendo durante meu curso técnico em TI.

Esse projeto vai servir para você entender como funciona uma rede corporativa **real**, com servidores, firewalls e clientes se comunicando.

Vou mostrar tudo isso na prática usando **máquinas virtuais no VirtualBox**. Então, se você quer aprender como funcionam redes, não perca nenhum vídeo desta série!"

---

### **[CONTEXTO - 0:30 a 1:30]**

**[Explicação do aprendizado]**

"Estou cursando Técnico em TI e, até agora, aprendi:

- ✅ Montagem e manutenção de computadores
- ✅ Planejamento e instalação de redes locais
- ✅ Simulação de redes com Packet Tracer
- ✅ Configuração de sistemas Windows e Linux
- ✅ Administração de servidores

Agora chegou a hora de **colocar tudo em prática** de forma integrada. Meu objetivo com este canal não é necessariamente ensinar vocês, mas sim **mostrar na prática** como essas tecnologias funcionam juntas em um cenário real.

Vou usar máquinas virtuais no VirtualBox para recriar um ambiente que você pode encontrar em uma pequena ou média empresa."

---

### **[APRESENTAÇÃO DA TOPOLOGIA - 1:30 a 5:00]**

**[Mostre o diagrama enquanto explica. Se não tiver diagrama, descreva detalhadamente]**

#### **Visão Geral da Infraestrutura:**

"O projeto consiste em **4 máquinas virtuais** trabalhando juntas:

---

#### **1️⃣ DEBIAN - FIREWALL/ROUTER (Servidor 1)**

**Função:** Gerenciar o acesso à internet e proteger a rede interna

**Configuração:**
- 2 placas de rede:
  - **Placa 1 (Externa):** Recebe a internet do computador host
  - **Placa 2 (Interna):** Conecta à rede privada interna
  
**O que faz:**
- Funciona como um roteador
- Controla o tráfego de dados
- Protege a rede interna com regras de firewall
- Compartilha a internet recebida para a rede interna

---

#### **2️⃣ WINDOWS SERVER 2012 (Servidor 2)**

**Função:** Distribuir recursos e gerenciar a rede interna

**Configuração:**
- 1 placa de rede: Conectada à rede interna (recebe internet do Debian/Firewall)

**O que faz:**
- Distribui endereços IP automaticamente para os outros computadores (DHCP)
- Gerencia a rede interna
- Atua como servidor central da infraestrutura
- Implementa Active Directory para autenticação e gerenciamento de usuários
- Aplica políticas de grupo (GPOs) para controle de configurações

---

#### **3️⃣ DEBIAN - SERVIDOR DE BANCO DE DADOS (Servidor 3)**

**Função:** Armazenar e gerenciar dados da aplicação

**Configuração:**
- 1 placa de rede: Conectada à rede interna
- Recebe IP automático do Windows Server via DHCP

**O que faz:**
- Executa um serviço de banco de dados
- Armazena informações importantes
- Responde às requisições dos clientes

---

#### **4️⃣ WINDOWS 10 PRO (Cliente)**

**Função:** Simular um computador de usuário

**Configuração:**
- 1 placa de rede: Conectada à rede interna
- Recebe IP automático do Windows Server via DHCP

**O que faz:**
- Acessa os serviços da rede
- Se conecta ao servidor de banco de dados
- Representa o "usuário final" da rede

---

### **[FLUXO DE COMUNICAÇÃO - 5:00 a 7:00]**

**[Explique como os dados fluem]**

"Vamos entender como as máquinas se comunicam:

**Passo 1 - Recebimento de Internet:**
O Debian Firewall recebe a conexão de internet do computador host e a coloca na rede interna.

**Passo 2 - Distribuição de IPs:**
O Windows Server 2012 está constantemente disponível para distribuir endereços IP (via DHCP) para qualquer máquina que se conecte à rede.

**Passo 3 - Configuração Automática:**
O Debian DBA e o Windows 10 Pro, ao se conectarem, recebem automaticamente um IP do Windows Server.

**Passo 4 - Comunicação:**
Com os IPs configurados, todas as máquinas podem se comunicar:
- Windows 10 → Debian DBA: Solicita dados
- Debian DBA → Windows 10: Responde com dados
- Tudo passa pelo Debian Firewall para sair/entrar da rede

**Resultado:**
Uma rede funcional, segura e bem organizada!"

---

### **[OBJETIVOS DA SÉRIE - 7:00 a 8:00]**

**[Explique o que será feito nos próximos vídeos]**

"Quais serão os proximos objetivos:

1. ✅ **Vídeo 02:** Instalação das VMs e configuração inicial do VirtualBox
2. ✅ **Vídeo 03:** Configuração do Debian Firewall (roteamento e NAT)
3. ✅ **Vídeo 04:** Configuração do Windows Server 2012 (DHCP e roles)
4. ✅ **Vídeo 05:** Configuração do Debian DBA (banco de dados)
5. ✅ **Vídeo 06:** Configuração do Windows 10 Pro (cliente)
6. ✅ **Vídeo 07:** Testes de comunicação entre as máquinas
7. ✅ **Vídeo 08:** Implementação de segurança no Firewall
8. ✅ **Vídeo 09:** Troubleshooting e dicas práticas

Cada vídeo será focado em um aspecto específico, com passo a passo detalhado."

---

### **[ENCERRAMENTO - 8:00 a 8:30]**

**[Chamada para ação]**

"Se você quer aprender como construir uma infraestrutura de rede real, inscreva-se no canal e ative as notificações para não perder nenhum vídeo!

Se você tiver dúvidas ou sugestões, deixe um comentário abaixo. Vou responder com prazer.

Nos vemos no próximo vídeo! Até mais! 👋"

---

## 📊 VISUAL/RECURSOS RECOMENDADOS

**Durante a Explicação, Mostre:**
- [ ] Um diagrama da topologia (pode ser feito no Paint, Lucidchart, ou até desenhado)
- [ ] Screenshots do VirtualBox mostrando as VMs (opcional, mas recomendado)
- [ ] Animações ou transições entre cada componente

**Sugestão de Diagrama ASCII (para colocar uma imagem no vídeo):**

```
┌─────────────────────────────────────────────────┐
│           Linux Mint 22.3 HOST (Internet)       │
└────────────┬────────────────────────────────────┘
             │
    ┌────────▼────────┐
    │  DEBIAN FIREWALL│
    │  (2 Placas NIC) │
    │  ┌────┬────┐    │ 192.168.10.1
    │  │Eth0│Eth1│    │
    └──┬─┬┼──────┘────┘
       │ │└─────────────────┐
       │ │                  │
    ┌──┘ └─────────────────────────────┐
    │                                  │
    │    REDE INTERNA (192.168.10.0)   │
    │                                  │
┌───▼────────────┐ ┌───────────────┐ ┌──▼────────────────┐
│ WINDOWS SERVER │ │ DEBIAN DBA    │ │ WINDOWS 10 PRO    │
│  2012 (DHCP)   │ │  (Cliente)    │ │   (Cliente)       │
│  192.168.10.10 │ │ 192.168.10.20 │ │   IP: Auto        │
└────────────────┘ └───────────────┘ └───────────────────┘
```

---

## 💡 DICAS DE GRAVAÇÃO

- [ ] **Fale claro e devagar:** Seu público pode não ser técnico
- [ ] **Use cursor destacado:** Para apontar elementos na tela
- [ ] **Faça pausas:** Para o espectador processar as informações
- [ ] **Mostre enquanto explica:** Não fale apenas, visualize também
- [ ] **Use legendas/texto na tela:** Para reforçar conceitos importantes
- [ ] **Mantenha tom profissional mas acessível:** Não seja muito formal, seja amigável

---

## 🎬 CHECKLIST ANTES DE GRAVAR

- [ ] Roteiro memorizado ou bem ensaiado
- [ ] VirtualBox aberto e VMs visíveis
- [ ] Microfone testado e em bom nível
- [ ] Luz ambiente adequada
- [ ] Tela do computador bem organizada
- [ ] Diagrama ou imagens prontas para mostrar
- [ ] Background limpo ou blurred (se for câmera)
- [ ] Tempo de gravação cronometrado

---

## 🎙️ SCRIPT ALTERNATIVO (Mais Formal)

Se preferir algo mais focado e direto, use este:

**Abertura:** "Olá, sou [seu nome]. Neste vídeo, vou apresentar um projeto prático de infraestrutura de rede que envolve firewall, servidores e clientes se comunicando através de máquinas virtuais."

**Desenvolvimento:** [Use a mesma estrutura acima]

**Encerramento:** "Inscreva-se para acompanhar os próximos episódios. Obrigado!"

---

**Versão do Documento:** 1.0  
**Última Atualização:** 21/04/2026
