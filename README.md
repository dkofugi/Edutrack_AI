# EduTrack AI — Gestão Acadêmica Inteligente (Versão Web / PC Desktop & Mobile)

Aplicativo completo de gestão acadêmica projetado para **telas de computadores/notebooks (Web / PC)** com layout widescreen, barra lateral fixa de navegação (Sidebar), visualizações em grid multi-colunas e modais centralizados, mantendo compatibilidade responsiva para dispositivos móveis.

Desenvolvido com HTML5, CSS3 moderno e Vanilla JavaScript modular, seguindo os princípios de **Spec-Driven Development** e preparado para integração com backend em Python (FastAPI) e PostgreSQL.

---

## 🖥️ Destaques da Versão Web / Desktop
- **Sidebar de Navegação Fixa**: Menu lateral completo à esquerda com logo, links de páginas, perfil do aluno e atalhos rápidos (`+ Nova Disciplina`, `+ Nova Tarefa`).
- **Dashboard Widescreen**: Layout em 2 colunas com 4 métricas ampliadas, gráfico de carga horária interativo em SVG (barras/donut) e lista de progresso.
- **Grid de Disciplinas**: Exibição em cards multi-colunas (2 a 3 matérias por linha).
- **Detalhes em 2 Colunas**: Informações da disciplina ao lado da lista e filtros de tarefas.
- **Modais Centralizados**: Formulários de criação/edição centralizados para uso com mouse e teclado.

---

## 🚀 Como Executar o Projeto

A aplicação integra o frontend Web/Desktop com uma API backend de autenticação segura na porta **8000**:

### Opção 1: Usando Python (Servidor Integrado Completo)
No terminal da pasta do projeto, execute:
```bash
py server.py
```
Em seguida, abra no seu navegador:
👉 **[http://localhost:8000](http://localhost:8000)**

### Opção 2: Usando npm
Se você tiver o Node.js/npm instalado:
```bash
npm start
```

### 🧪 Executando os Testes Automatizados
Para rodar a suíte de testes de autenticação e endpoints HTTP:
```bash
# Via npm
npm test

# Ou diretamente via Python
py -m unittest discover -s tests -p "test_*.py" -v
```

### 🗄️ Configuração do Banco de Dados (PostgreSQL)
A camada de autenticação utiliza PostgreSQL por padrão quando a variável `DATABASE_URL` (ou variáveis `PG*`) estiver configurada:
```bash
# Exemplo via string de conexão
$env:DATABASE_URL="postgresql://usuario:senha@localhost:5432/edutrack"
py server.py
```
> **Nota:** Caso o PostgreSQL não esteja ativo localmente durante testes offline, o sistema possui fallback transparente para SQLite local mantendo o mesmo esquema e hash bcrypt, garantindo que o desenvolvimento e os testes nunca quebrem.

---

## 📱 Telas Implementadas e Fluxos de Navegação

1. **Login**:
   - Campos: E-mail acadêmico e senha.
   - Acesso direto ao Dashboard, links para Cadastro e Recuperação de Senha.
   - Usuário de teste pré-preenchido: `aluno@edutrack.ai` / `123456`.

2. **Cadastro**:
   - Campos: Nome, E-mail, Senha e Confirmação de Senha.
   - Botão de voltar consistente ao Login e link para login direto.

3. **Recuperar Senha**:
   - Campo de e-mail com fluxo de envio simulado e mensagem de confirmação.
   - Botão de retorno ao Login.

4. **Dashboard**:
   - Boas-vindas com nome do estudante.
   - Métricas em cards: Total de Disciplinas, Tarefas Pendentes e Tarefas Concluídas.
   - **Gráfico de Carga Horária/Tempo**: visualização interativa em SVG com alternância entre formato **Barras** e **Pizza (Donut)**.
   - Lista de disciplinas com barras visuais de **% de progresso** e contagem de tarefas.
   - Clique em qualquer disciplina navega diretamente para sua tela de detalhes.

5. **Disciplinas**:
   - Listagem completa com cards estilizados na paleta verde suave.
   - Informações exibidas: nome, professor, carga horária, datas de início/fim e ementa.
   - Botão **"+ Nova Disciplina"**: modal completo para cadastro e edição.
   - Botões de **Editar** e **Excluir** (com confirmação e remoção em cascata).

6. **Detalhe da Disciplina**:
   - Cabeçalho com métricas da matéria e barra de progresso consolidada.
   - Filtros por status de tarefas: **Todas**, **Pendentes**, **Em Andamento** e **Concluídas**.
   - Botão **"+ Nova Tarefa"** pré-vinculada à disciplina.
   - Checkbox para alternar status da tarefa imediatamente (Pendente ↔ Concluída).
   - Botão consistente de **Voltar**.

7. **Tarefas**:
   - Visão geral de todas as tarefas de todas as matérias.
   - Modal de criação/edição com campos: disciplina, título, descrição, data prevista e status (`Pendente`, `Em Andamento`, `Concluída`).

---

## 🎨 Identidade Visual e Recursos de UI

- **Paleta Verde Claro / Menta / Sálvia**: Projetada com foco em tranquilidade, organização e concentração (`#10b981`, `#059669`, `#ecfdf5`, etc.).
- **Suporte a Tema Claro e Escuro**:
  - Botão de alternância no cabeçalho (ícones de Sol e Lua).
  - Persistência da preferência em `localStorage`.
  - Detecção automática do `prefers-color-scheme` do sistema operacional.
- **Armazenamento Reativo (`localStorage`)**:
  - Todas as criações, edições e exclusões persistem e atualizam métricas e gráficos em tempo real.
  - Função de logout e controle de sessão mockada.

---

## 📐 Especificação Técnica de Backend (OpenSpec)

O contrato de dados e arquitetura futura do backend foi documentado em:
📄 [`spec/backend_spec.md`](./spec/backend_spec.md)

- **PostgreSQL**: Entidades em `snake_case` (`users`, `subjects`, `academic_tasks`).
- **Python / FastAPI**: Endpoints RESTful previstos para autenticação JWT e operações CRUD.
