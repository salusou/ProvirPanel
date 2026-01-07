# Provir Cloud Panel v1.0.0 - Release Notes

## 🚀 Funcionalidades Principais

### 🔐 Sistema de Autenticação
- Autenticação JWT com roles (admin, dev, viewer)
- Criação automática de usuário admin padrão
- Gestão de usuários e alteração de senhas
- Rotas protegidas no frontend

### 📊 Dashboard e Métricas
- Monitoramento em tempo real via WebSocket
- Métricas de CPU, RAM e Disco com gráficos
- Contagem de containers Docker ativos
- Lista de processos por uso de recursos
- Informações de sistema (uptime, hostname)

### 🖥️ Terminal Web
- Terminal remoto via Socket.io
- Múltiplas abas de terminal
- Autocomplete de comandos e arquivos
- Controle de permissões por usuário
- Histórico de comandos

### 🐳 Gerenciamento Docker
- **Serviços Docker**: Sistema completo de templates pré-configurados
- **Templates Disponíveis**: Node.js, Nginx, PostgreSQL, MySQL, Redis, pgAdmin
- **Projetos Exemplo**: Criação automática de código de exemplo para desenvolvimento
- **Gerenciamento de Containers**: Start, stop, restart, remoção e logs em tempo real
- **Redes Docker**: Configuração de networks (bridge, host, custom)
- **Validação de Portas**: Verificação automática de disponibilidade
- **pgAdmin Integration**: Instalação automática com PostgreSQL

### 📁 Gerenciador de Arquivos
- Interface estilo VS Code
- Editor Monaco com syntax highlighting
- Upload/download de arquivos
- Preview de imagens, PDFs e mídia
- Criação, renomeação e movimentação de arquivos
- Navegação em árvore de diretórios

### 🌐 Gestão de Rotas/Domínios
- **Proxy Manager**: Sistema de roteamento por paths
- **Configuração Nginx**: Geração automática de configuração
- **Domínio Base**: Suporte a subdomínio único (ex: portal.exbonus.com.br)
- **Paths Dinâmicos**: Criação de rotas como /app, /api para serviços
- **SSL Ready**: Configuração preparada para certificados

### ⚙️ CI/CD Básico
- Integração com Git (pull, build, restart)
- Webhooks para deploy automático
- Sistema de rollback
- Suporte a PM2 e Docker

## 🛠️ Melhorias Técnicas

### Backend
- **Detecção Robusta de Portas**: Uso de `lsof` para verificação real de portas ocupadas
- **Templates de Projeto**: Sistema modular para criação de exemplos de código
- **Validação de Serviços**: Prevenção de nomes duplicados e validação de configurações
- **Métricas Docker**: Integração com dockerode para contagem de containers
- **Proxy Reverso**: Geração automática de configuração Nginx

### Frontend
- **Visual Aprimorado**: Gradientes, melhor tipografia e espaçamento
- **Logo Integration**: Suporte a logo personalizada nos componentes
- **Modais Responsivos**: Interfaces modernas para criação e edição
- **Validação em Tempo Real**: Feedback imediato para formulários
- **Estado Consistente**: Gerenciamento de estado otimizado

### Instaladores
- **Multiplataforma**: Linux (Debian/Ubuntu, RHEL/CentOS, SUSE), macOS
- **Detecção Automática**: Identificação de distribuição e gerenciador de pacotes
- **Configuração Completa**: Setup automático de PostgreSQL, Docker, PM2
- **SSL Self-Signed**: Geração automática de certificados para desenvolvimento

## 📦 Estrutura do Projeto

```
provirpanel/
├── backend/
│   ├── src/
│   │   ├── services/
│   │   │   ├── DockerManager.js
│   │   │   ├── ProjectTemplateManager.js
│   │   │   ├── CloudflareManager.js (ProxyManager)
│   │   │   └── MetricsCollector.js
│   │   ├── routes/
│   │   │   ├── docker.js
│   │   │   ├── domains.js
│   │   │   └── metrics.js
│   │   └── config/
│   └── .env.example
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── DockerPanel.jsx
│   │   │   ├── DomainsPanel.jsx
│   │   │   └── Dashboard.jsx
│   │   └── assets/
│   │       └── logo.png
├── install.sh
├── install-macos.sh
└── README.md
```

## 🔧 Configuração

### Variáveis de Ambiente
```env
PORT=3000
DATABASE_URL=postgres://user:password@localhost:5432/provirpanel
JWT_SECRET=your-secure-secret
CLOUDPAINEL_PROJECTS_DIR=/home/provirpanel/projects
PROXY_BASE_URL=portal.exbonus.com.br
```

### Instalação Rápida
```bash
# Linux
curl -fsSL https://raw.githubusercontent.com/ProvirCloud/provirpanel/main/install.sh | bash

# macOS
curl -fsSL https://raw.githubusercontent.com/ProvirCloud/provirpanel/main/install-macos.sh | bash
```

## 🎯 Próximos Passos

- [ ] Validação de webhooks GitHub/GitLab
- [ ] Sistema de permissões granulares
- [ ] Auditoria de comandos e logs estruturados
- [ ] Testes automatizados (API e UI)
- [ ] Suporte a múltiplos domínios base
- [ ] Integração com Let's Encrypt

---

**Tecnologias**: Node.js, React, PostgreSQL, Docker, Socket.io, Nginx, PM2