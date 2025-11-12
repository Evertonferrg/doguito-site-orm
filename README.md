# 🐶 Doguito API

Aplicação Node.js que fornece endpoints para gerenciamento de clientes e integração com banco de dados Oracle Cloud.  
Desenvolvido como parte do projeto **Doguito Site ORM**, com deploy automatizado via **systemd** no Oracle Cloud Infrastructure (OCI).

---
<img width="1431" height="598" alt="Captura de tela 2025-11-12 170610" src="https://github.com/user-attachments/assets/b098b4c4-ef0c-40a9-bd70-f89d4a9acb3d" />

acesso : http://163.176.131.17/telas/lista_cliente.html

## 🚀 Tecnologias Utilizadas

- **Node.js** (v18+)
- **Express.js**
- **Oracle Database (ATP / Autonomous DB)**
- **oracledb** (driver oficial da Oracle)
- **systemd** (para execução automática da API)
- **Linux Oracle Cloud Instance (OCI)**

---

## 📂 Estrutura do Projeto

doguito-site-orm/
│
├── bin/
│ └── www # Ponto de entrada da aplicação
├── public/ # Arquivos estáticos (HTML, CSS, JS)
├── routes/ # Definição das rotas (ex: clientes.js)
├── service/ # Serviços e conexão com o banco
├── app.js # Configuração principal do Express
├── package.json # Dependências do projeto
└── README.md # Este arquivo

yaml
Copiar código

---

## ⚙️ Variáveis de Ambiente

A aplicação utiliza três variáveis principais para conectar ao banco Oracle:

| Variável | Descrição | Exemplo |
|-----------|------------|---------|
| `DB_USER` | Usuário do banco Oracle | `admin` |
| `DB_PASSWORD` | Senha do usuário | `Doguito12345` |
| `CONNECT_STRING` | String de conexão do Oracle | `doguitodb_high` |

> Estas variáveis estão configuradas no arquivo do serviço systemd:  
> `/etc/systemd/system/doguito-site.service`

---

## 🖥️ Execução Manual

Você pode executar o servidor manualmente com:

```bash
node ./bin/www
Depois, acesse no navegador:

👉 http://localhost:3000
ou
👉 http://<seu-IP-público>:3000

🔄 Execução Automática (Systemd)
O serviço foi configurado para iniciar automaticamente no boot.

Arquivo de serviço:
/etc/systemd/system/doguito-site.service

ini
Copiar código
[Unit]
Description=Doguito API Service
After=network.target

[Service]
Environment=DB_USER=admin
Environment=DB_PASSWORD=Doguito12345
Environment=CONNECT_STRING=doguitodb_high
WorkingDirectory=/home/opc/doguito-site-orm
ExecStart=/usr/bin/node /home/opc/doguito-site-orm/bin/www
Restart=always
RestartSec=10
StandardOutput=journal
StandardError=journal
User=opc

[Install]
WantedBy=multi-user.target
Comandos úteis:
bash
Copiar código
sudo systemctl daemon-reload          # Recarregar configurações
sudo systemctl start doguito-site     # Iniciar o serviço
sudo systemctl stop doguito-site      # Parar o serviço
sudo systemctl status doguito-site    # Ver status do serviço
sudo systemctl enable doguito-site    # Ativar no boot
sudo journalctl -u doguito-site -f    # Ver logs em tempo real
📡 Endpoints Principais
Método	Rota	Descrição
GET	/clientes	Lista todos os clientes
POST	/clientes	Cadastra um novo cliente
PUT	/clientes/:id	Atualiza um cliente existente
DELETE	/clientes/:id	Remove um cliente

🧩 Dependências
Para instalar as dependências do projeto:

bash
Copiar código
npm install
🧠 Solução de Problemas
Erro ORA-24415
“Missing or null username.”

Verifique se as variáveis DB_USER, DB_PASSWORD e CONNECT_STRING estão configuradas corretamente no serviço systemd.

Recarregue o daemon e reinicie o serviço:

bash
Copiar código
sudo systemctl daemon-reload
sudo systemctl restart doguito-site
🧾 Licença
Este projeto é de uso educacional aprendido no curso Alura e está sob a licença MIT.

✍️ Autor
Everton Guedes


yaml
Copiar código
