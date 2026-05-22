# 💻 Portefólio Profissional & Académico (LEI UMinho)

Bem-vindo ao repositório do meu portefólio pessoal! Este é um espaço digital interativo concebido para apresentar o meu percurso académico na **Licenciatura em Engenharia Informática (LEI)** na **Universidade do Minho** (UMinho), bem como os meus projetos práticos de programação, competências e ferramentas.

O projeto foi construído de raiz sob uma arquitetura modular de alta fidelidade recorrendo a **Vite** + **Vue.js 3 (Single-File Components)** e estilizado com **CSS3 puro** (usando design tokens modernos em cores OKLCH e técnicas de Glassmorphism).

---

## 🌟 Destaques do Web Profile

* 📱 **Design Premium Matte Carbon**: Visual minimalista escuro e sofisticado com brilhos Modena Yellow e Rosso Corsa, totalmente responsivo para qualquer tamanho de ecrã.
* 🌎 **Sistema Multilingue Nativo (PT / EN)**: Dicionário de traduções reativo integrado no componente principal Vue 3 para comutação de idioma instantânea.
* 📦 **Integração Real de Projetos**: Galeria de projetos sincronizada com repositórios reais e competências de baixo nível e alto nível.
* ⚡ **Performance Elevada**: Carregamento ultra-rápido de recursos compilados estaticamente e prontos para publicação de alto desempenho.

---

## 💻 Mini-Terminal Linux Interativo ("Easter Egg" CLI)

O maior atrativo interativo do portefólio é o **Mini-Terminal de Linha de Comandos** flutuante no canto inferior direito. Ele simula uma consola bash Linux real e dispõe de autofocus inteligente, scroll automático e adaptação para ecrã inteiro em dispositivos móveis.

### Comandos Disponíveis na Consola:
| Comando | Descrição do Output |
| :--- | :--- |
| `help` | Imprime a lista tabular de todos os comandos disponíveis no terminal. |
| `about` | Apresenta a minha biografia profissional e percurso em LEI. |
| `projects` | Lista os meus 4 projetos em desenvolvimento com links de repositório clicáveis. |
| `skills` | Imprime barras de progresso retro-ASCII para expressar a minha proficiência de linguagens. |
| `neofetch` | Gera o Tux em arte ASCII e as estatísticas do meu sistema virtual (`OS: UMinho LEI OS`, `CPU: C & Haskell Compiler Engine`, `Host: cerqueira-dev-box`). |
| `contact` | Exibe as minhas informações rápidas de contacto (email oficial e GitHub). |
| `clear` | Limpa o histórico de comandos e outputs da janela. |
| `sudo [comando]` | Easter Egg clássico das consolas Unix. |

---

## 🛠️ Tecnologias Utilizadas

* **Framework Core**: [Vue.js 3](https://vuejs.org/) (SFC, Composition API, Refs, Computeds)
* **Build Tool & Bundler**: [Vite](https://vitejs.dev/) (para bundling otimizado e HMR instantâneo)
* **Estilização**: CSS3 Puro (Layers CSS `@layer`, variáveis de cor dinâmicas `light-dark()`, Glassmorphic backdrop filters e variáveis OKLCH)
* **Tipografia**: Space Grotesk (Display Mono) & Outfit (Body)
* **Ícones**: [Font Awesome 6](https://fontawesome.com/)

---

## 📁 Estrutura de Pastas Principal

```bash
├── dist/                  # Bundle de produção minificado estático (gerado pelo Vite)
├── node_modules/          # Dependências locais do npm
├── src/
│   ├── main.js            # Ponto de entrada do script Vue 3
│   ├── App.vue            # Componente Single-File (Lógica, HTML e traduções do site)
│   └── style.css          # Folha de estilos CSS global, variáveis e estilo do terminal
├── index.html             # Estrutura base HTML5 com tags SEO
├── package.json           # Declaração de scripts e dependências do projeto
├── vite.config.js         # Configurações do compilador Vite
└── .gitignore             # Definição de exclusões de pastas para commits seguros
```

---

## 🚀 Como Testar e Correr Localmente

Garante que tens o [Node.js](https://nodejs.org/) instalado no teu sistema. Siga os passos abaixo na pasta do projeto:

### 1. Instalar as dependências
```bash
npm install
```

### 2. Iniciar o servidor de desenvolvimento
Executa o servidor local na porta padrão do projeto (`http://localhost:3000`):
```bash
npm run dev
```

### 3. Gerar o Build de Produção
Para compilar e comprimir o portefólio para alojamento:
```bash
npm run build
```

### 4. Testar a Pré-Visualização do Build
Para simular a performance do site final de produção no teu computador local:
```bash
npm run preview
```


