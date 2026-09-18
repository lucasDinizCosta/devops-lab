# 📘 FASE 1 — Linux + Fundamentos de Infraestrutura
**Período:** Outubro/2026

> **Objetivo da fase:** Não precisa virar administrador Linux.
> Você precisa conseguir **operar uma aplicação Linux sem depender de tutorial para cada problema**.

---

## Índice

1. [Shell](#1-shell)
2. [Processos](#2-processos)
3. [Serviços](#3-serviços)
4. [Arquivos e Permissões](#4-arquivos-e-permissões)
5. [Networking](#5-networking)
6. [SSH](#6-ssh)
7. [🎯 Entregável da Fase](#-entregável-da-fase)

---

## 1. Shell

O shell é a sua interface direta com o sistema operacional. Dominar os comandos básicos é o que separa "ficar preso" de "resolver rápido".

### Comandos essenciais

| Comando | O que faz | Exemplo |
|---|---|---|
| `cd` | Navega entre diretórios | `cd /var/log` |
| `ls` | Lista arquivos e pastas | `ls -la` (lista tudo, com detalhes) |
| `cp` | Copia arquivos/pastas | `cp app.js app.js.bak` |
| `mv` | Move ou renomeia | `mv config.old.json config.json` |
| `rm` | Remove arquivos/pastas | `rm -rf node_modules` |
| `mkdir` | Cria diretório | `mkdir -p src/utils` |
| `cat` | Mostra conteúdo de um arquivo | `cat .env` |
| `less` | Visualiza arquivo grande com paginação | `less app.log` |
| `grep` | Busca padrões em texto | `grep "ERROR" app.log` |
| `find` | Busca arquivos no sistema | `find / -name "*.log"` |
| `head` | Mostra as primeiras linhas | `head -n 20 app.log` |
| `tail` | Mostra as últimas linhas | `tail -f app.log` (acompanha em tempo real) |
| `sort` | Ordena linhas | `sort nomes.txt` |
| `uniq` | Remove duplicadas (linhas adjacentes) | `sort ips.txt \| uniq -c` |
| `awk` | Processa texto por colunas | `awk '{print $1}' access.log` |
| `sed` | Substitui texto | `sed 's/dev/prod/g' config.txt` |
| `curl` | Faz requisições HTTP | `curl -I https://api.exemplo.com` |
| `wget` | Baixa arquivos da web | `wget https://exemplo.com/arquivo.tar.gz` |

### Operadores principais

| Operador | O que faz | Exemplo |
|---|---|---|
| `\|` (pipe) | Envia a saída de um comando como entrada de outro | `cat app.log \| grep ERROR` |
| `>` | Redireciona saída, **sobrescrevendo** o arquivo | `echo "log iniciado" > status.txt` |
| `>>` | Redireciona saída, **acrescentando** ao arquivo | `echo "novo evento" >> status.txt` |
| `&&` | Executa o próximo comando **somente se o anterior deu certo** | `npm install && npm start` |
| `;` | Executa comandos em sequência, **independente do resultado** | `cd /app ; ls` |

### Exemplo de aplicação prática

Encontrar os últimos 50 erros de um log de aplicação:

```bash
cat app.log | grep ERROR | tail -50
```

Outro exemplo combinando conceitos — contar quantas vezes cada IP aparece em um log de acesso, do maior para o menor:

```bash
awk '{print $1}' access.log | sort | uniq -c | sort -nr
```

Verificar se uma API está no ar antes de continuar um script de deploy:

```bash
curl -sf https://api.exemplo.com/health && echo "API OK" && ./deploy.sh
```

---

## 2. Processos

Toda aplicação rodando em Linux é um **processo**. Entender processos é essencial para saber se sua aplicação está viva, travada, consumindo recursos demais, ou simplesmente não existe.

### Comandos essenciais

| Comando | O que faz | Exemplo |
|---|---|---|
| `ps` | Lista processos em execução | `ps aux \| grep node` |
| `top` | Monitor de processos em tempo real | `top` |
| `htop` | Versão mais amigável do `top` (interativa) | `htop` |
| `kill` | Envia um sinal para encerrar um processo pelo PID | `kill 4521` |
| `killall` | Encerra processos pelo nome | `killall node` |

### Conceitos-chave

- **PID (Process ID):** número único que identifica um processo em execução.
- **Processo:** uma instância de um programa rodando.
- **Thread:** uma "linha de execução" dentro de um processo — vários threads podem rodar dentro do mesmo processo, compartilhando memória.
- **Daemon:** processo que roda em segundo plano, geralmente iniciado no boot, sem interação direta com o usuário (ex: `nginx`, `sshd`).
- **Foreground/Background:** um processo em *foreground* ocupa o terminal; em *background* (`&`) libera o terminal para outros comandos.
- **Sinais:** mensagens enviadas para processos pedindo alguma ação (parar, reiniciar, etc).
- **SIGTERM:** pede para o processo encerrar **de forma graciosa** (ele pode salvar estado, fechar conexões).
- **SIGKILL:** força o encerramento **imediato**, sem chance do processo reagir.

### Exemplo de aplicação prática

Descobrir se sua aplicação Node está rodando e pegar o PID dela:

```bash
ps aux | grep node
```

Encerrar a aplicação de forma graciosa (permite que ela finalize requisições em andamento):

```bash
kill 4521
```

Se ela não responder ao `SIGTERM`, forçar o encerramento:

```bash
kill -9 4521
```

Rodar uma aplicação em background e continuar usando o terminal:

```bash
node app.js &
```

---

## 3. Serviços

Em produção, você raramente sobe uma aplicação digitando `node app.js` manualmente. Você configura um **serviço** gerenciado pelo `systemd`, que garante que a aplicação suba no boot, reinicie se cair, e tenha logs centralizados.

### Comandos essenciais

| Comando | O que faz | Exemplo |
|---|---|---|
| `systemctl` | Gerencia serviços (start, stop, restart, status) | `systemctl status meu-app` |
| `journalctl` | Consulta logs do systemd | `journalctl -u meu-app -f` |

### Conceito-chave: a cadeia de responsabilidade

```
systemd
    ↓
service
    ↓
processo
```

O `systemd` é o "gerente" do sistema. Ele controla os **services** (unidades de configuração que dizem como e quando rodar algo), e cada service, quando ativado, sobe um **processo** real na memória.

### Exemplo de aplicação prática

Verificar o status de uma aplicação rodando como serviço:

```bash
systemctl status meu-app
```

Reiniciar o serviço depois de um deploy:

```bash
sudo systemctl restart meu-app
```

Acompanhar os logs em tempo real (muito parecido com `tail -f`):

```bash
journalctl -u meu-app -f
```

Isso será muito útil quando você estiver investigando aplicações em **EC2**: ao invés de perguntar "por que minha aplicação caiu?", você vai direto no `journalctl` e vê a causa raiz.

---

## 4. Arquivos e Permissões

Um dos erros mais comuns em produção é "Permission denied". Entender permissões evita perder horas com isso.

### Comandos essenciais

| Comando | O que faz | Exemplo |
|---|---|---|
| `chmod` | Altera permissões de um arquivo/pasta | `chmod +x deploy.sh` |
| `chown` | Altera o dono de um arquivo | `chown ubuntu:ubuntu app.js` |
| `chgrp` | Altera o grupo de um arquivo | `chgrp deploy app.js` |

### Conceitos-chave

- **rwx:** read (ler), write (escrever), execute (executar) — as três permissões básicas.
- **owner:** o dono do arquivo.
- **group:** o grupo associado ao arquivo.
- **others:** todos os outros usuários do sistema.

Cada arquivo tem permissões separadas para essas três categorias, por exemplo:

```
-rwxr-xr--
```

Lido como: owner pode ler/escrever/executar, group pode ler/executar, others só pode ler.

### `sudo`

Permite executar um comando como outro usuário (geralmente `root`), quando você tem permissão para isso. É a diferença entre "não consigo fazer isso" e "posso fazer isso temporariamente, com privilégio elevado".

### Exemplo de aplicação prática

Tornar um script executável:

```bash
chmod +x deploy.sh
./deploy.sh
```

Corrigir o dono de um arquivo copiado como root para o usuário da aplicação:

```bash
sudo chown ubuntu:ubuntu /var/www/app/config.json
```

Editar um arquivo de configuração do sistema que exige privilégio de root:

```bash
sudo nano /etc/nginx/nginx.conf
```

---

## 5. Networking

Aqui começa uma parte importante. Sua aplicação pode estar perfeita e ainda assim ser inacessível — e o motivo quase sempre está na rede.

### Conceitos-chave

- **IP:** endereço que identifica uma máquina na rede.
- **Port:** "porta" onde um serviço específico escuta (ex: 80 para HTTP, 443 para HTTPS, 22 para SSH).
- **TCP:** protocolo de transporte confiável, com confirmação de entrega (usado por HTTP, SSH, etc).
- **UDP:** protocolo de transporte mais rápido, mas sem garantia de entrega (usado em streaming, DNS, jogos).
- **DNS:** sistema que traduz nomes de domínio (ex: `google.com`) em endereços IP.
- **HTTP/HTTPS:** protocolos de comunicação web, sendo o HTTPS a versão criptografada.
- **SSH:** protocolo para acesso remoto seguro a outra máquina.

### Ferramentas essenciais

| Comando | O que faz | Exemplo |
|---|---|---|
| `ping` | Testa se um host está acessível na rede | `ping 8.8.8.8` |
| `curl` | Faz requisições e testa respostas de serviços | `curl -v http://localhost:3000` |
| `ss` | Lista conexões e portas abertas (substitui o `netstat`) | `ss -tulpn` |
| `netstat` | Lista conexões de rede (mais antigo, ainda muito usado) | `netstat -tulpn` |
| `dig` | Consulta registros DNS | `dig exemplo.com` |
| `nslookup` | Consulta DNS (alternativa mais simples ao `dig`) | `nslookup exemplo.com` |
| `traceroute` | Mostra o caminho (saltos de rede) até um host | `traceroute exemplo.com` |

### A pergunta que você precisa saber responder

> "Minha aplicação está rodando, mas ninguém consegue acessá-la. Como descubro por quê?"

Você precisa conseguir investigar — e não apenas reiniciar a aplicação na esperança de que resolva.

### Exemplo de aplicação prática — roteiro de investigação

1. **A aplicação está de fato rodando?**
   ```bash
   ps aux | grep node
   ```

2. **Em qual porta ela está escutando?**
   ```bash
   ss -tulpn | grep node
   ```

3. **Ela responde localmente, na própria máquina?**
   ```bash
   curl -v http://localhost:3000
   ```
   Se funcionar localmente mas não externamente, o problema é de rede/firewall, não da aplicação.

4. **A porta está liberada externamente?** (verifique o Security Group na AWS, ou `iptables`/`ufw` localmente)

5. **O DNS está resolvendo corretamente?**
   ```bash
   dig meuapp.com
   ```

6. **Existe um problema de rota até o servidor?**
   ```bash
   traceroute meuapp.com
   ```

Esse roteiro — de dentro para fora — é o que transforma "não sei o que houve" em "identifiquei o problema em 2 minutos".

---

## 6. SSH

SSH é a porta de entrada para qualquer servidor remoto. Sem isso, você não acessa sua EC2, não faz deploy, não investiga nada.

### Comandos essenciais

| Comando | O que faz | Exemplo |
|---|---|---|
| `ssh` | Conecta a uma máquina remota | `ssh -i chave.pem ubuntu@54.23.11.9` |
| `scp` | Copia arquivos entre máquinas via SSH | `scp -i chave.pem app.js ubuntu@54.23.11.9:/home/ubuntu/` |

### A cadeia de acesso

```
seu computador
      ↓ SSH
     EC2
      ↓
   Linux
      ↓
   Node.js
```

Você usa SSH para "entrar" na EC2. Uma vez dentro, você está operando o Linux daquela máquina — e é dentro dele que sua aplicação Node.js está rodando.

### Exemplo de aplicação prática

Conectar a uma instância EC2 usando uma chave privada:

```bash
ssh -i minha-chave.pem ubuntu@54.23.11.9
```

Copiar um arquivo local para o servidor remoto:

```bash
scp -i minha-chave.pem ./dist/app.js ubuntu@54.23.11.9:/home/ubuntu/app/
```

Executar um comando remoto sem precisar abrir uma sessão interativa:

```bash
ssh -i minha-chave.pem ubuntu@54.23.11.9 "systemctl restart meu-app"
```

---

## 🎯 Entregável da Fase

Criar uma pequena aplicação com a seguinte arquitetura:

```
Node API
   ↓
Linux
   ↓
PostgreSQL
```

Rodando em uma **VM Linux** (ex: EC2).

### Checklist de habilidades a validar

Ao final desta fase, você deve conseguir, sem depender de tutorial:

- [ ] Iniciar/parar a aplicação
- [ ] Encontrar o processo da aplicação (PID, uso de recursos)
- [ ] Descobrir em qual porta a aplicação está escutando
- [ ] Consultar logs da aplicação (via `journalctl` ou arquivo de log)
- [ ] Verificar consumo de CPU/RAM (`top`/`htop`)
- [ ] Verificar conectividade de rede (a aplicação está acessível externamente?)
- [ ] Investigar um erro do zero, sem saber de antemão qual é a causa
- [ ] Configurar usuário e permissões corretamente para rodar a aplicação com segurança

> Se você concluir esse checklist sem precisar buscar "como fazer X no Linux" no Google, a Fase 1 está completa.