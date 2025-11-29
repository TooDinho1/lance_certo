# 🎥 Lance Certo — Plataforma Inteligente de Captura e Compartilhamento de Momentos Esportivos

[![Status](https://img.shields.io/badge/status-em%20desenvolvimento-yellow)]()
[![Python](https://img.shields.io/badge/python-3.10%2B-blue)]()
[![Django](https://img.shields.io/badge/django-5.2-green)]()
[![React](https://img.shields.io/badge/react-19.1-blue)]()
[![OpenCV](https://img.shields.io/badge/OpenCV-4.x-red)]()

> **Projeto Interdisciplinar de Extensão II — SETREM**  
> Desenvolvido por alunos de Engenharia de Computação

---

## 📝 Sobre o Projeto

O **Lance Certo** é uma plataforma completa que democratiza o acesso à tecnologia de captura e compartilhamento de momentos esportivos. Combinando um sistema de gravação inteligente com uma rede social integrada, a solução permite que atletas amadores e comunitários capturem, editem e compartilhem seus melhores momentos de forma simples e acessível.

### 🎯 Problema Identificado

Registrar e compartilhar os melhores momentos de uma partida esportiva ainda é um desafio em ambientes **amadores e comunitários**:
- 📹 Gravações longas que desperdiçam espaço
- ✂️ Necessidade de edição manual complexa
- 💰 Equipamentos caros e inacessíveis
- 🔄 Falta de plataforma integrada para compartilhamento

### 💡 Nossa Solução

Uma plataforma web moderna que integra:
- **Captura Inteligente**: Grave continuamente e salve apenas os últimos 60 segundos ao pressionar um botão na tela de Captura
- **Rede Social**: Compartilhe, curta e descubra momentos incríveis de outros atletas
- **Interface Intuitiva**: Design responsivo e fácil de usar
- **Baixo Custo**: Funciona com equipamentos acessíveis (notebook + webcam)

---

## ✨ Funcionalidades

### 🎬 Sistema de Captura
- ✅ Gravação contínua com buffer circular de 60 segundos
- ✅ Captura via webcam ou tela do computador
- ✅ Salvamento instantâneo de clipes ao pressionar botão
- ✅ Múltiplos clipes por sessão de gravação
- ✅ Preview em tempo real
- ✅ Compressão otimizada (H.264/WebM)

### 🌐 Rede Social
- ✅ Feed de momentos com filtros e ordenação
- ✅ Sistema de curtidas e visualizações
- ✅ Tags e categorias (Futebol, Basquete, Vôlei, etc.)
- ✅ Perfil de usuário com estatísticas
- ✅ Busca inteligente de momentos
- ✅ Player de vídeo integrado
- ✅ Sugestões de vídeos relacionados
- ✅ Paginação otimizada

### 👤 Perfil e Personalização
- ✅ Avatar e biografia personalizável
- ✅ Estatísticas de visualizações e curtidas
- ✅ Gerenciamento de momentos publicados
- ✅ Edição e exclusão de conteúdo próprio

### 🔐 Autenticação
- ✅ Sistema de login/registro seguro
- ✅ Sessões com Django Session Authentication
- ✅ Proteção CSRF
- ✅ Autorização baseada em permissões

---

## 🏗️ Arquitetura

### 📊 Diagrama de Componentes

```
┌─────────────────────────────────────────────────────────┐
│                    FRONTEND (React)                     │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌─────────┐  │
│  │   Home   │  │ Capture  │  │  Profile │  │  Video  │  │
│  └──────────┘  └──────────┘  └──────────┘  └─────────┘  │
│         │              │              │            │    │
│         └──────────────┴──────────────┴────────────┘    │
│                        │                                │
│                    API Client                           │
└─────────────────────────────────────────────────────────┘
                           │
                      HTTPS/REST
                           │
┌─────────────────────────────────────────────────────────┐
│                 BACKEND (Django REST)                   │
│  ┌──────────────────┐      ┌──────────────────┐         │
│  │  Auth Endpoints  │      │ Momentos Endpoints│        │
│  └──────────────────┘      └──────────────────┘         │
│           │                         │                   │
│  ┌────────┴─────────────────────────┴────────┐          │
│  │         Business Logic Layer               │         │
│  │  • Serializers  • Views  • Permissions    │          │
│  └────────┬─────────────────────────┬────────┘          │
│           │                         │                   │
│  ┌────────┴────────┐      ┌────────┴────────┐           │
│  │  User Model     │      │  Momento Model  │           │
│  │                 │      │  • Likes        │           │
│  │  • Usuario      │      │  • Tags         │           │
│  └─────────────────┘      │  • Comentarios  │           │
│                            └─────────────────┘          │
└─────────────────────────────────────────────────────────┘
                           │
                      PostgreSQL
```

### 🔧 Tecnologias Utilizadas

#### Frontend
- **React 19.1** - Framework UI
- **React Router 7** - Roteamento SPA
- **Axios** - Cliente HTTP
- **Vite** - Build tool e dev server
- **CSS** - Estilização

#### Backend
- **Django 5.2** - Framework web
- **Django REST Framework** - API REST
- **PostgreSQL** - Banco de dados
- **Pillow** - Processamento de imagens
- **python-decouple** - Gerenciamento de configurações

#### Captura de Vídeo
- **MediaRecorder API** - Gravação no navegador
- **WebRTC** - Acesso a câmera/tela
- **Buffer Circular** - Armazenamento em memória
- **H.264/WebM** - Codecs de vídeo

#### Infraestrutura
- **CORS Headers** - Comunicação cross-origin
- **Session Authentication** - Autenticação stateful
- **CSRF Protection** - Segurança contra ataques

---

## 📂 Estrutura do Projeto

```
lance-certo/
│
├── backend/                      # Django Backend
│   ├── config/                   # Configurações do projeto
│   │   ├── settings.py          # Configurações principais
│   │   ├── urls.py              # Roteamento principal
│   │   └── wsgi.py              # WSGI config
│   │
│   ├── usuarios/                 # App de usuários
│   │   ├── models.py            # Modelo Usuario (AbstractUser)
│   │   ├── serializers.py       # Serialização de dados
│   │   ├── views.py             # Login, Register, Profile
│   │   └── urls.py              # Rotas de autenticação
│   │
│   ├── momentos/                 # App de momentos
│   │   ├── models.py            # Modelos (Momento, Tag, Like, Comentario)
│   │   ├── serializers.py       # Serialização de momentos
│   │   ├── views.py             # CRUD, Like, Comment, Search
│   │   └── urls.py              # Rotas de momentos
│   │
│   ├── media/                    # Uploads (vídeos, thumbnails)
│   ├── requirements.txt          # Dependências Python
│   └── manage.py                 # CLI Django
│
├── frontend/                     # React Frontend
│   ├── public/                   # Arquivos estáticos
│   │   └── favicon.svg
│   │
│   ├── src/
│   │   ├── components/           # Componentes reutilizáveis
│   │   │   ├── layout/
│   │   │   │   └── Header.jsx   # Header da aplicação
│   │   │   ├── gallery/
│   │   │   │   └── MomentoCard.jsx
│   │   │   ├── profile/
│   │   │   │   └── EditProfileModal.jsx
│   │   │   └── video/
│   │   │       └── VideoSuggestions.jsx
│   │   │
│   │   ├── contexts/             # Context API
│   │   │   └── AuthContext.jsx  # Contexto de autenticação
│   │   │
│   │   ├── pages/                # Páginas
│   │   │   ├── Home.jsx         # Feed de momentos
│   │   │   ├── Capture.jsx      # Captura de vídeo
│   │   │   ├── Profile.jsx      # Perfil do usuário
│   │   │   ├── VideoPlayer.jsx  # Player de vídeo
│   │   │   ├── Login.jsx        # Login
│   │   │   └── Register.jsx     # Registro
│   │   │
│   │   ├── services/             # Serviços
│   │   │   └── api.js           # Cliente API (Axios)
│   │   │
│   │   ├── styles/               # Estilos CSS
│   │   │   ├── global.css
│   │   │   ├── components/
│   │   │   └── pages/
│   │   │
│   │   ├── App.jsx               # Componente raiz
│   │   └── main.jsx              # Entry point
│   │
│   ├── package.json              # Dependências Node
│   └── vite.config.js            # Configuração Vite
│
├── docs/                         # Documentação
│   └── Projeto_Interdisciplinar_II.pdf
│
└── README.md                     # Este arquivo
```

---

## 🚀 Como Executar

### 📋 Pré-requisitos

- Python 3.10+
- Node.js 20+
- PostgreSQL 14+
- Git

### 🔧 Configuração do Backend

1. **Clone o repositório**
```bash
git clone https://github.com/Azeved0k/lance-certo.git
cd lance-certo/backend
```

2. **Crie um ambiente virtual**
```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
# ou
venv\Scripts\activate     # Windows
```

3. **Instale as dependências**
```bash
pip install -r requirements.txt
```

4. **Configure as variáveis de ambiente**

Crie um arquivo `.env` na pasta `backend/` com:

```env
SECRET_KEY=sua-chave-secreta-django
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1

DB_NAME=lance_certo
DB_USER=postgres
DB_PASSWORD=sua-senha
DB_HOST=localhost
DB_PORT=5432

CORS_ALLOWED_ORIGINS=http://localhost:5173
```

5. **Execute as migrações**
```bash
python manage.py migrate
```

6. **Crie um superusuário**
```bash
python manage.py createsuperuser
```

7. **Inicie o servidor**
```bash
python manage.py runserver
```

Backend estará rodando em `http://localhost:8000`

### ⚛️ Configuração do Frontend

1. **Navegue até a pasta frontend**
```bash
cd ../frontend
```

2. **Instale as dependências**
```bash
npm install
```

3. **Inicie o servidor de desenvolvimento**
```bash
npm run dev
```

Frontend estará rodando em `http://localhost:5173`

### 🌐 Acessando a Aplicação

- **Frontend**: http://localhost:5173
- **Backend API**: http://localhost:8000/api
- **Admin Django**: http://localhost:8000/admin

---

## 🎨 Design System

### Paleta de Cores

```css
--primary-color: #3B82F6;      /* Azul principal */
--primary-hover: #2563EB;      /* Azul hover */
--secondary-color: #10B981;    /* Verde sucesso */
--danger-color: #EF4444;       /* Vermelho perigo */
--gray-50 a 900: ...           /* Escala de cinza */
```

### Tipografia

- **Fonte**: System fonts (SF Pro, Segoe UI, Roboto)
- **Tamanhos**: 0.75rem - 2.5rem
- **Pesos**: 400 (regular), 600 (semibold), 700 (bold), 800 (extrabold)

---

## 🧪 Metodologia de Desenvolvimento

### Abordagem Ágil

O projeto segue uma abordagem experimental de pesquisa aplicada:

1. **Desenvolvimento Iterativo** → Protótipos e testes incrementais
2. **Testes de Usabilidade** → Feedback com usuários reais
3. **Análise de Desempenho** → Métricas de latência e estabilidade
4. **Integração com LARCC** → Testes em infraestrutura avançada

### Fases do Projeto

| Fase | Período | Status |
|------|---------|--------|
| Planejamento e Revisão Teórica | Ago-Set/2025 | ✅ Concluído |
| Desenvolvimento do Protótipo | Set-Nov/2025 | ✅ Concluído |
| Testes e Validação | Nov-Dez/2025 | 🚧 Em progresso |

---

## 💡 Funcionalidades Futuras

### Em Desenvolvimento
- 🔄 Edição básica de vídeos (corte, exportação)
- 📊 Dashboard com analytics detalhados
- 🔔 Sistema de notificações em tempo real

### Planejadas
- 🤖 Detecção automática de momentos importantes (IA)
- 🏆 Sistema de conquistas e gamificação
- 🎯 Sistema de campeonatos, reservas e torneios
- 👥 Equipes e organizações
- 💬 Chat em tempo real
- 🌍 Múltiplos idiomas

---

## 📊 Métricas de Desempenho

### Objetivos Técnicos

- ⚡ Latência de captura: < 100ms
- 💾 Tamanho de buffer: 60 segundos (~50-100MB)
- 🎥 Taxa de quadros: 30 FPS mínimo
- 📦 Compressão de vídeo: ~80% de redução
- 🚀 Tempo de upload: < 10s para clipes de 60s

---

## 💰 Orçamento

| Item | Quantidade | Valor (R$) |
|------|------------|------------|
| SSD Sandisk 1TB | 1 | 451,05 |
| Notebook Dell Vostro i5 10ª, 16GB RAM | 1 | 3.762,00 |
| **Total** | | **4.213,05** |

---

## 👥 Equipe

| Nome | Função | Contato |
|------|--------|---------|
| **Enzo Allebrand** | Desenvolvimento e Testes de Desempenho | @Azeved0K |
| **Kauã Patricki** | Desenvolvimento e Testes de Desempenho | @enzzoalle |
| **Leonardo Herkert** | Documentação Técnica | @TooDinho1 |

### Orientação e Apoio
- **SETREM** - Sociedade Educacional Três de Maio

--
### ⚠️ Termos de Uso

- ✅ Uso pessoal e educacional
- ✅ Modificações e melhorias
- ✅ Testes e experimentos
- ❌ Uso comercial sem autorização
- ❌ Captura automatizada em larga escala

---

## 🔗 Links Úteis

- 📘 [Documentação Django](https://docs.djangoproject.com/)
- ⚛️ [Documentação React](https://react.dev/)
- 📊 [Roadmap do Projeto](https://github.com/Azeved0K/lance_certo)

---

## 📞 Contato

- **Instituição**: SETREM - Três de Maio, RS
- **Projeto**: Interdisciplinar de Extensão II
- **Curso**: Engenharia de Computação
- **Ano**: 2025

---

## 🙏 Agradecimentos

Este projeto conta com o apoio de:

- **SETREM** - Pela estrutura e suporte institucional
- **Professores Orientadores** - Pelo conhecimento compartilhado
- **Atletas Testadores** - Pelo feedback valioso

---

<div align="center">

**[⬆ Voltar ao Topo](#-lance-certo--plataforma-inteligente-de-captura-e-compartilhamento-de-momentos-esportivos)**

---

Desenvolvido com ❤️ pelos alunos de Engenharia de Computação da SETREM

📍 Três de Maio, Rio Grande do Sul, Brasil | 🎓 2025

</div>
