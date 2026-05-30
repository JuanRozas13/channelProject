# Atualização do Sistema Debian Server 13.4.0 no VirtualBox

#Autor: JF Tech<br>
#Projeto: Infraestrutura de Rede com VirtualBox<br>
#Sistema Operacional: Debian Server 13.4.0<br>
#Ambiente: Máquina Virtual no Oracle VM VirtualBox<br>
#Objetivo: Atualização inicial do sistema após a instalação<br>
#Documentação: Atualização do Debian Server<br>
#Versão: 0.01<br>
#Data de criação: 23/05/2026<br>

**OBSERVAÇÃO IMPORTANTE:** esta documentação faz parte do projeto de infraestrutura criado em ambiente virtual. Neste momento o foco é somente atualizar o Debian Server após a instalação no VirtualBox. Configurações de OpenSSH, firewall, usuários, serviços de rede e hardening serão tratadas em documentos próprios.

## Informações da Documentação

| Item | Descrição |
| --- | --- |
| Sistema Operacional | Debian Server 13.4.0 |
| Ambiente | Oracle VM VirtualBox |
| Tipo de instalação | Servidor Debian em máquina virtual |
| Objetivo | Atualizar o sistema após a instalação |
| Público |inscritos do canal e pessoas estudando infraestrutura |
| Nível | Iniciante a intermediário |

## Sobre Esta Etapa do Projeto

Após instalar o Debian Server no VirtualBox, o primeiro procedimento recomendado é atualizar o sistema operacional.

Essa etapa é importante porque a imagem ISO usada na instalação pode não conter todos os pacotes mais recentes. Mesmo quando a instalação é nova, os repositórios oficiais podem ter recebido correções de segurança, atualizações de estabilidade e novas versões de pacotes.

Nesta documentação serão executadas as seguintes atividades:

- verificar informações básicas do Debian;
- validar conectividade de rede;
- atualizar a lista de pacotes;
- verificar pacotes disponíveis para atualização;
- atualizar o sistema;
- remover pacotes desnecessários;
- validar o sistema após a atualização;
- registrar a atualização feita na VM.

## Cenário do Projeto

O projeto utiliza máquinas virtuais para simular uma infraestrutura de rede.

| Componente | Função | Observação |
| --- | --- | --- |
| Linux Mint | Sistema host | Computador físico que executa o VirtualBox |
| VirtualBox | Plataforma de virtualização | Responsável por criar e executar as VMs |
| Debian Server 13.4.0 | Servidor Linux | VM que será atualizada nesta documentação |

Exemplo de nome para a VM:

```text
srv-debian01
```

Exemplo de uso futuro deste servidor:

```text
Servidor base para serviços de infraestrutura, acesso remoto, firewall, banco de dados ou aplicações internas.
```

## Por Que Atualizar o Debian Após a Instalação

Atualizar o sistema logo depois da instalação ajuda a garantir:

- correções de segurança;
- pacotes mais recentes;
- melhor compatibilidade com serviços que serão instalados depois;
- correção de falhas conhecidas;
- estabilidade do ambiente;
- base mais confiável para continuar o projeto.

Em ambientes reais, manter servidores atualizados é uma prática essencial de administração de sistemas.

## Antes de Começar

Antes de executar os comandos, confirme os pontos abaixo:

- o Debian Server foi instalado com sucesso;
- a máquina virtual está ligada;
- você consegue fazer login no sistema;
- o usuário possui permissão administrativa com `sudo`;
- a placa de rede da VM está configurada corretamente no VirtualBox;
- o servidor possui acesso à internet;
- foi criado um snapshot da VM antes das alterações.

**OBSERVAÇÃO IMPORTANTE:** em ambiente de laboratório, sempre que uma etapa importante for iniciada, crie um snapshot no VirtualBox. Assim, se algo der errado, será possível voltar ao estado anterior da máquina virtual.

## 01 - Verificando Informações do Sistema

O primeiro passo é verificar se o sistema instalado é realmente o Debian esperado.

```bash
cat /etc/debian_version
```

Esse comando mostra a versão do Debian instalada.

Também é possível visualizar informações mais completas com:

```bash
hostnamectl
```

Esse comando mostra dados como:

- hostname do servidor;
- sistema operacional;
- kernel em uso;
- arquitetura;
- tipo de virtualização.

## 02 - Verificando o Usuário Atual

Para verificar qual usuário está logado no sistema:

```bash
whoami
```

Para confirmar se o usuário possui permissão de `sudo`, execute:

```bash
sudo -v
```

Se o comando não retornar erro, o usuário possui permissão administrativa.

**OBSERVAÇÃO IMPORTANTE:** caso o usuário não esteja no grupo `sudo`, será necessário acessar com o usuário `root` ou adicionar o usuário ao grupo correto. Esse procedimento deve ser documentado separadamente.

## 03 - Verificando o Nome do Servidor

Para consultar o hostname atual:

```bash
hostname
```

Para consultar informações completas:

```bash
hostnamectl
```

Exemplo recomendado para laboratório:

```text
srv-debian01
```

**OBSERVAÇÃO:** a padronização de nomes ajuda a organizar a infraestrutura, principalmente quando o projeto crescer e possuir vários servidores.

## 04 - Verificando Configuração de Rede

Antes de atualizar o sistema, confirme se a VM possui endereço IP.

```bash
ip addr
```

Verifique também a rota padrão:

```bash
ip route
```

A rota padrão indica por onde o Debian acessa outras redes, incluindo a internet.

## 05 - Testando Conectividade com a Internet

Teste primeiro a conectividade usando um endereço IP público:

```bash
ping -c 4 8.8.8.8
```

Se esse teste funcionar, significa que existe comunicação com a internet.

Depois teste a resolução de nomes DNS:

```bash
ping -c 4 deb.debian.org
```

Se o primeiro teste funcionar e o segundo falhar, o problema provavelmente está relacionado ao DNS.

## 06 - Atualizando a Lista de Repositórios

Antes de instalar ou atualizar pacotes, é necessário atualizar a lista de pacotes disponíveis nos repositórios.

```bash
sudo apt update
```

Esse comando consulta os repositórios configurados no Debian e atualiza a base local de pacotes.

**OBSERVAÇÃO IMPORTANTE:** o comando `apt update` não atualiza os programas instalados. Ele apenas atualiza a lista de pacotes disponíveis.

## 07 - Verificando Pacotes Disponíveis para Atualização

Para listar os pacotes que possuem atualização disponível:

```bash
apt list --upgradable
```

Esse comando ajuda a visualizar o que será atualizado antes de aplicar as alterações.

## 08 - Atualizando os Pacotes Instalados

Para atualizar os pacotes já instalados no Debian:

```bash
sudo apt upgrade
```

O sistema exibirá um resumo com:

- quantidade de pacotes que serão atualizados;
- pacotes que serão mantidos;
- espaço em disco necessário;
- confirmação antes de continuar.

Quando for solicitado, confirme a operação digitando:

```text
S
```

ou:

```text
Y
```

A letra pode variar conforme o idioma do sistema.

## 09 - Atualização Completa do Sistema

Em alguns casos, o Debian pode precisar instalar novos pacotes ou remover pacotes antigos para concluir uma atualização.

Para isso, use:

```bash
sudo apt full-upgrade
```

**OBSERVAÇÃO IMPORTANTE:** o `full-upgrade` pode remover pacotes quando necessário para resolver dependências. Em servidores de produção, esse comando deve ser usado com atenção. No laboratório, ele é útil para deixar o sistema totalmente atualizado.

## 10 - Removendo Pacotes Desnecessários

Depois da atualização, alguns pacotes podem não ser mais necessários.

Para remover dependências antigas:

```bash
sudo apt autoremove
```

Para limpar arquivos antigos baixados pelo gerenciador de pacotes:

```bash
sudo apt autoclean
```

Esses comandos ajudam a manter o sistema mais limpo.

## 11 - Verificando se o Sistema Precisa Reiniciar

Após uma atualização, principalmente quando envolve kernel ou bibliotecas importantes, pode ser necessário reiniciar o servidor.

Verifique se existe indicação de reinicialização:

```bash
ls /var/run/reboot-required
```

Se o arquivo existir, reinicie a máquina:

```bash
sudo reboot
```

**OBSERVAÇÃO:** caso o comando `ls /var/run/reboot-required` retorne erro informando que o arquivo não existe, significa que o sistema não sinalizou necessidade obrigatória de reinicialização.

## 12 - Validando o Sistema Após a Atualização

Depois do reboot, faça login novamente no Debian e valide o sistema.

Verificar a versão do Debian:

```bash
cat /etc/debian_version
```

Verificar informações do sistema:

```bash
hostnamectl
```

Verificar endereço IP:

```bash
ip addr
```

Verificar rota padrão:

```bash
ip route
```

Testar internet:

```bash
ping -c 4 8.8.8.8
```

Testar DNS:

```bash
ping -c 4 deb.debian.org
```

## 13 - Verificando Serviços com Falha

Para verificar se existe algum serviço com erro:

```bash
systemctl --failed
```

Se nenhum serviço estiver com falha, o sistema exibirá uma lista vazia ou uma mensagem informando que não existem unidades com erro.

Para visualizar todos os serviços ativos:

```bash
systemctl list-units --type=service --state=running
```

## 14 - Verificando Espaço em Disco

Para conferir o uso do disco:

```bash
df -h
```

Esse comando mostra as partições montadas e o espaço usado em cada uma.

Para verificar o tamanho de diretórios principais:

```bash
sudo du -sh /var /home /tmp
```

## 15 - Verificando Memória RAM

Para consultar o uso da memória:

```bash
free -h
```

Esse comando mostra:

- memória total;
- memória usada;
- memória livre;
- memória disponível;
- uso de swap.

## 16 - Verificando Kernel em Uso

Para verificar a versão do kernel carregado:

```bash
uname -r
```

Esse comando é útil após atualizações que envolvem o kernel do sistema.

## 17 - Fluxo Resumido da Atualização

O fluxo abaixo resume os principais comandos usados nesta documentação.

```bash
cat /etc/debian_version
hostnamectl
ip addr
ip route
ping -c 4 8.8.8.8
ping -c 4 deb.debian.org
sudo apt update
apt list --upgradable
sudo apt upgrade
sudo apt full-upgrade
sudo apt autoremove
sudo apt autoclean
sudo reboot
```

Depois do reinício:

```bash
hostnamectl
systemctl --failed
df -h
free -h
uname -r
ping -c 4 deb.debian.org
```

## 18 - Registro da Atualização

Use a tabela abaixo para documentar a atualização feita no servidor.

| Data | Servidor | Responsável | Versão Debian | Resultado |
| --- | --- | --- | --- | --- |
| 23/05/2026 | srv-debian01 |  | Debian Server 13.4.0 |  |

## 19 - Checklist da Aula

- [ ] Debian Server instalado no VirtualBox
- [ ] Login realizado com sucesso
- [ ] Snapshot criado antes da atualização
- [ ] Conectividade com IP público testada
- [ ] Resolução DNS testada
- [ ] Lista de pacotes atualizada
- [ ] Pacotes atualizáveis verificados
- [ ] Sistema atualizado
- [ ] Pacotes desnecessários removidos
- [ ] Servidor reiniciado, se necessário
- [ ] Serviços com falha verificados
- [ ] Disco verificado
- [ ] Memória verificada
- [ ] Kernel verificado
- [ ] Atualização registrada na documentação

## 20 - Problemas Comuns

### Sem Internet na VM

Verifique:

- se a placa de rede está habilitada no VirtualBox;
- se o modo de rede está configurado corretamente;
- se o Debian recebeu IP;
- se existe rota padrão;
- se o host físico possui internet.

Comandos úteis:

```bash
ip addr
ip route
ping -c 4 8.8.8.8
```

### DNS Não Resolve Nomes

Se o ping para `8.8.8.8` funcionar, mas o ping para `deb.debian.org` falhar, verifique a configuração de DNS.

Comando útil:

```bash
cat /etc/resolv.conf
```

### Pacotes Não Atualizam

Verifique se os repositórios estão acessíveis:

```bash
sudo apt update
```

Se aparecerem erros, leia a mensagem exibida no terminal. Ela normalmente indica se o problema está na rede, DNS, repositório ou data/hora do sistema.

### Sistema Pede Reinicialização

Se o sistema solicitar reinicialização após atualizar, execute:

```bash
sudo reboot
```

Após o reboot, valide novamente os serviços e a conectividade.

## 21 - Boas Práticas

- criar snapshot antes de grandes alterações;
- manter o sistema atualizado;
- documentar comandos executados;
- registrar data e responsável pela alteração;
- validar rede antes e depois da atualização;
- evitar instalar pacotes desnecessários;
- reiniciar o servidor quando o sistema solicitar;
- manter nomes de servidores padronizados.

## 22 - Próxima Etapa do Projeto

Após atualizar o Debian Server, o próximo passo recomendado é preparar o servidor para administração remota.

Essa próxima documentação poderá abordar:

- instalação do OpenSSH Server;
- verificação do serviço SSH;
- configuração de acesso remoto;
- segurança inicial do SSH;
- acesso pelo Linux Mint;
- acesso pelo Windows PowerShell;
- acesso pelo PuTTY;
- boas práticas de administração remota.

## Referências

- Debian: https://www.debian.org/
- Debian Packages: https://packages.debian.org/
- Debian Security: https://www.debian.org/security/
- Manual do APT: https://manpages.debian.org/apt
- Oracle VM VirtualBox: https://www.virtualbox.org/
