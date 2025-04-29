# Monitoramento de Links com n8n e Telegram

Este repositório contém um tutorial para o canal Código Fonte TV que mostra como criar uma automação com n8n para verificar periodicamente o status de uma lista de URLs e enviar alertas via Telegram quando algum link estiver fora do ar.

**Assista ao vídeo tutorial:** https://youtu.be/UDWEAMwS7rg

## 🔧 Pré-requisitos

- Docker
- Docker Compose
- Conta e Bot no Telegram (Token)
- Chat ID do Telegram para receber alertas

## 🚀 Instalação

1. Clone este repositório:

   ```bash
   git clone <URL do repositório>
   cd <nome-do-diretório>
   ```

2. Copie o arquivo de exemplo `.env` e preencha as variáveis:

   ```bash
   cp sample.env .env
   ```

   Edite o `.env` com:

   - `DOMAIN_NAME`: seu domínio (ex: codigofonte.tv)
   - `SUBDOMAIN`: subdomínio para acesso ao n8n (ex: n8n)
   - `GENERIC_TIMEZONE`: fuso horário (ex: America/Sao_Paulo)

3. Edite o arquivo `data/meus-links.txt` e adicione as URLs que deseja monitorar (uma URL por linha).

## ⚙️ Configurando o n8n

1. Inicie os serviços:

   ```bash
   docker-compose up -d
   ```

2. Acesse o painel do n8n em `http://localhost:5678` (ou `https://<SUBDOMAIN>.<DOMAIN_NAME>` se configurado).

3. Crie uma credencial do tipo **Telegram**:

   - Token: fornecido pelo @BotFather
   - Nome da credencial: `Telegram account` (deve coincidir com o nome usado no workflow)

4. Importe o workflow:

   - Clique em **+** > **Importar** > **Importar de arquivo**
   - Selecione `workflows/check-links-telegram.json`

5. Salve e **ative** o workflow.

## 📝 Estrutura do Projeto

```
.
├── docker-compose.yml              # Definição do serviço n8n
├── sample.env                      # Exemplo de variáveis de ambiente
├── data/
│   └── meus-links.txt              # Arquivo com as URLs a monitorar
└── workflows/
    └── check-links-telegram.json   # Workflow exportado do n8n
```

## 📊 Uso

- O workflow é executado a cada minuto (configurado no node Cron).
- Se algum link retornar `statusCode` diferente de 200, uma mensagem de alerta é enviada para o chat do Telegram configurado.
- Logs podem ser visualizados com:

  ```bash
  docker-compose logs -f n8n
  ```

## 🌐 Hospedagem Recomendada

Para um ambiente de produção mais estável e seguro, recomendamos hospedar o n8n em um VPS da Hostinger.

- A Hostinger tem um plano de VPS já com o n8n pré-instalado, facilitando a configuração.
- Aproveite **nosso desconto** em qualquer plano de VPS usando o cupom `CODIGOFONTE` no checkout.
- Link: https://codigofonte.click/hostingern8n

## 🤝 Contribuições

Contribuições são bem-vindas! Abra uma issue ou envie um pull request.

---

Feito com ❤️ pelo Código Fonte TV.
