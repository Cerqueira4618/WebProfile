<script setup>
import { ref, computed, onMounted, nextTick } from 'vue';

// 1. DICIONÁRIO DE TRADUÇÕES (PT / EN)
const translations = {
    pt: {
        nav_about: "Sobre Mim",
        nav_skills: "Competências",
        nav_projects: "Projetos",
        nav_contact: "Contacto",
        
        hero_badge: "Universidade do Minho • LEI",
        hero_title_1: "Olá, eu sou o",
        hero_subtitle: "Estudante do 2.º Ano (2.º Semestre) de Licenciatura em Engenharia Informática. Apaixonado por desenvolvimento de software, algoritmos e construção de soluções digitais eficientes.",
        hero_cta_primary: "Ver Projetos",
        hero_cta_secondary: "Entrar em Contacto",
        
        about_title: "Sobre Mim",
        about_p1: "Atualmente estou a frequentar a **Licenciatura em Engenharia Informática (LEI)** na **Universidade do Minho**, em Braga. A frequentar o segundo semestre do segundo ano, tenho focado a minha aprendizagem nas bases teóricas e práticas da computação.",
        about_p2: "O meu percurso académico tem-me permitido dominar paradigmas que vão da programação imperativa e funcional até à programação orientada a objetos, bem como o desenho de algoritmos eficientes, arquiteturas de computadores, bases de dados relacionais e sistemas operativos de baixo nível.",
        stat_year: "Ano de LEI",
        stat_languages: "Linguagens/Tech",
        stat_projects: "Projetos Práticos",
        
        timeline_title: "Percurso Académico",
        timeline_y2_title: "2.º Ano - Consolidação e Sistemas",
        timeline_y2_desc: "Foco em Programação Orientada a Objetos (Java), Sistemas Operativos (C / Chamadas ao Sistema Linux), Bases de Dados (Modelação Relacional e SQL) e Laboratórios de Informática III (processamento massivo de dados em C).",
        timeline_y1_title: "1.º Ano - Os Fundamentos",
        timeline_y1_desc: "Introdução à programação com Programação Funcional (Haskell) e Programação Imperativa (C). Desenvolvimento de projetos práticos em Laboratórios de Informática I (Haskell) e II (C) e conceitos fundamentais de Álgebra e Análise Matemática.",
        
        skills_title: "Competências",
        skills_cat_languages: "Linguagens de Programação",
        skills_cat_tools: "Tecnologias & Ferramentas",
        
        projects_title: "Projetos",
        filter_all: "Todos",
        filter_academic: "Académicos (UMinho)",
        filter_personal: "Pessoais",
        
        contact_title: "Contacto",
        contact_subtitle: "Vamos trabalhar juntos?",
        contact_p: "Estou sempre aberto a novos desafios, projetos de código aberto ou simplesmente para conversar sobre tecnologia e Engenharia Informática na UMinho. Podes contactar-me através de qualquer uma das redes ou do meu email!",
        
        footer_rights: "Todos os direitos reservados.",
        footer_tag: "Criado com Vue.js 3, Vite e CSS3."
    },
    en: {
        nav_about: "About Me",
        nav_skills: "Skills",
        nav_projects: "Projects",
        nav_contact: "Contact",
        
        hero_badge: "University of Minho • LEI",
        hero_title_1: "Hi, I am",
        hero_subtitle: "2nd Year (2nd Semester) Software Engineering Student at University of Minho. Passionate about software development, algorithms, and building efficient digital solutions.",
        hero_cta_primary: "View Projects",
        hero_cta_secondary: "Get in Touch",
        
        about_title: "About Me",
        about_p1: "I am currently pursuing a **Bachelor's Degree in Software Engineering (LEI)** at the **University of Minho**, in Braga. Now in my second year, second semester, I've been focusing my learning on both theoretical and practical foundations of computer science.",
        about_p2: "My academic path has allowed me to master paradigms ranging from functional and imperative programming to object-oriented programming, as well as efficient algorithm design, computer architectures, relational databases, and low-level operating systems.",
        stat_year: "Year of LEI",
        stat_languages: "Languages/Tech",
        stat_projects: "Practical Projects",
        
        timeline_title: "Academic Path",
        timeline_y2_title: "2nd Year - Consolidation & Systems",
        timeline_y2_desc: "Focused on Object-Oriented Programming (Java), Operating Systems (C / Linux System Calls), Databases (Relational Modeling and SQL), and Software Laboratories III (large-scale data processing in C).",
        timeline_y1_title: "1st Year - The Foundations",
        timeline_y1_desc: "Introduction to programming with Functional Programming (Haskell) and Imperative Programming (C). Practical project development in Software Laboratories I (Haskell) and II (C), alongside foundational concepts in Algebra and Calculus.",
        
        skills_title: "Skills",
        skills_cat_languages: "Programming Languages",
        skills_cat_tools: "Technologies & Tools",
        
        projects_title: "Projects",
        filter_all: "All",
        filter_academic: "Academic (UMinho)",
        filter_personal: "Personal",
        
        contact_title: "Contact",
        contact_subtitle: "Let's work together?",
        contact_p: "I am always open to new challenges, open-source projects, or simply to talk about technology and Software Engineering at UMinho. Reach out to me via any social media or my email!",
        
        footer_rights: "All rights reserved.",
        footer_tag: "Created with Vue.js 3, Vite and CSS3."
    }
};

// 2. BANCO DE DADOS DE PROJETOS
const projectsData = [
    {
        id: "bugsbyte-2026",
        category: "personal",
        title: {
            pt: "BUGSBYTE-2026 • Monitor de Arbitragem",
            en: "BUGSBYTE-2026 • Arbitrage Monitor"
        },
        desc: {
            pt: "Sistema de simulação e monitorização de arbitragem de criptomoedas em tempo real. Backend robusto em Python (FastAPI, WebSockets, SQLite/PostgreSQL) e Frontend interativo em Vue 3 (TypeScript, Vite) para visualização instantânea de spreads de mercado.",
            en: "Real-time cryptocurrency arbitrage monitoring and simulation system. Features a robust Python backend (FastAPI, WebSockets, SQLite/PostgreSQL) and an interactive Vue 3 frontend (TypeScript, Vite) for instantaneous market spread visualization."
        },
        tags: ["Python", "FastAPI", "WebSockets", "Vue.js 3", "Vite", "TypeScript"],
        github: "https://github.com/Cerqueira4618/BUGSBYTE-2026",
        demo: ""
    },
    {
        id: "li3-airport-manager",
        category: "uminho",
        title: {
            pt: "LI3 • Airport Manager",
            en: "LI3 • Airport Manager"
        },
        desc: {
            pt: "Motor de processamento, filtragem e interrogação de dados de tráfego aéreo de larga escala em memória. Desenvolvido inteiramente em C modular com otimizações extremas recorrendo a Árvores AVL, Tabelas Hash e análise minuciosa com Valgrind.",
            en: "Large-scale in-memory airport log processing and database query engine. Developed entirely in modular C with advanced structures like AVL trees and Hash tables, optimized for memory footprint and performance via Valgrind."
        },
        tags: ["C", "AVL Trees", "Hash Maps", "Valgrind", "2.º Ano"],
        github: "https://github.com/Cerqueira4618/LI3-AIRPORT-MANAGER",
        demo: ""
    },
    {
        id: "li1-tower-defense",
        category: "uminho",
        title: {
            pt: "LI1 • Tower Defense 2D",
            en: "LI1 • 2D Tower Defense"
        },
        desc: {
            pt: "Jogo de estratégia em 2D interativo com mapas procedimentais e inimigos com inteligência artificial básica. Implementado em Haskell sobre o paradigma funcional puro, utilizando a biblioteca gráfica Gloss para renderização em tempo real.",
            en: "Interactive 2D strategy game featuring procedural maps and basic AI enemies. Implemented in Haskell adhering to pure functional programming concepts, utilizing the Gloss graphical library for real-time rendering."
        },
        tags: ["Haskell", "Gloss", "Functional", "Game Dev", "1.º Ano"],
        github: "https://github.com/Cerqueira4618/LI1---2D-Tower-Defense-Game",
        demo: ""
    },
    {
        id: "li2-board-game",
        category: "uminho",
        title: {
            pt: "LI2 • Jogo de Tabuleiro CGI",
            en: "LI2 • CGI Grid Strategy Game"
        },
        desc: {
            pt: "Jogo de tabuleiro estratégico baseado em grelha a correr no terminal Linux, estendido com suporte para interface web dinâmica baseada em CGI (Common Gateway Interface), gerando layouts interativos com HTML/CSS a partir de C.",
            en: "Strategic grid-based board game running natively in the Linux terminal, extended with support for a dynamic web interface using CGI (Common Gateway Interface) to render interactive HTML/CSS layouts straight from C."
        },
        tags: ["C", "CGI", "Web Interface", "Algorithms", "1.º Ano"],
        github: "https://github.com/Cerqueira4618/LI2",
        demo: ""
    }
];

// 3. COMPETÊNCIAS ESTÁTICAS
const languagesList = [
    { name: "C", level: { pt: "Avançado", en: "Advanced" }, percent: 90 },
    { name: "Java", level: { pt: "Iniciante", en: "Beginner" }, percent: 45 },
    { name: "Haskell", level: { pt: "Intermédio-Baixo", en: "Intermediate-Low" }, percent: 55 },
    { name: "SQL", level: { pt: "Intermédio", en: "Intermediate" }, percent: 70 },
    { name: "Vue.js 3", level: { pt: "Intermédio", en: "Intermediate" }, percent: 75 }
];

const toolsList = [
    { name: "Git & GitHub", level: { pt: "Avançado", en: "Advanced" }, percent: 85 },
    { name: "Ambiente Linux & Terminal Bash", level: { pt: "Avançado", en: "Advanced" }, percent: 85 },
    { name: "Algoritmos & Estruturas de Dados", level: { pt: "Intermédio-Alto", en: "Intermediate-High" }, percent: 80 },
    { name: "Modelação de Bases de Dados (SQL)", level: { pt: "Intermédio-Alto", en: "Intermediate-High" }, percent: 80 },
    { name: "Depuração de Código (Valgrind, GDB)", level: { pt: "Intermédio", en: "Intermediate" }, percent: 75 }
];

// Estados Reativos
const currentLanguage = ref(localStorage.getItem("language") || "pt");
const currentTheme = ref("dark");
const activeFilter = ref("all");
const mobileMenuOpen = ref(false);
const emailCopied = ref(false);
const skillsVisible = ref(false); // Animação reativa das barras no scroll

// Função de Tradução Reativa
const t = (key) => {
    const dictionary = translations[currentLanguage.value];
    if (!dictionary || !dictionary[key]) return key;
    
    let text = dictionary[key];
    if (text.includes("**")) {
        return text.replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>');
    }
    return text;
};

// Filtro Computado de Projetos
const filteredProjects = computed(() => {
    if (activeFilter.value === "all") {
        return projectsData;
    }
    return projectsData.filter(proj => proj.category === activeFilter.value);
});

// Alternar Idioma
const toggleLanguage = () => {
    const nextLang = currentLanguage.value === "pt" ? "en" : "pt";
    currentLanguage.value = nextLang;
    document.documentElement.lang = nextLang;
    localStorage.setItem("language", nextLang);
};

// Alternar Tema (Luz / Escuro)
const toggleTheme = () => {
    const nextTheme = currentTheme.value === "dark" ? "light" : "dark";
    currentTheme.value = nextTheme;
    localStorage.setItem("color-scheme", nextTheme);
    
    // Sincronizar tags do browser
    const metaTag = document.querySelector('meta[name="color-scheme"]');
    if (metaTag) {
        metaTag.content = nextTheme === "dark" ? "dark" : "light";
    }
    
    // Sincronizar classes globais
    if (nextTheme === "dark") {
        document.documentElement.classList.remove("light");
        document.documentElement.classList.add("dark");
        document.body.classList.remove("light");
        document.body.classList.add("dark");
    } else {
        document.documentElement.classList.remove("dark");
        document.documentElement.classList.add("light");
        document.body.classList.remove("dark");
        document.body.classList.add("light");
    }
};

// Controlo do Menu Mobile Hamburguer
const toggleMobileMenu = () => {
    mobileMenuOpen.value = !mobileMenuOpen.value;
};

const closeMobileMenu = () => {
    mobileMenuOpen.value = false;
};

// Filtro de Categorias de Projetos
const setFilter = (filter) => {
    activeFilter.value = filter;
};

// Cópia Fácil de Email
const copyEmail = async () => {
    const email = "cerqueira.lei.uminho@example.com";
    try {
        await navigator.clipboard.writeText(email);
        emailCopied.value = true;
        
        setTimeout(() => {
            emailCopied.value = false;
        }, 2000);
    } catch (err) {
        console.error("Falha ao copiar email: ", err);
    }
};

// Ouvinte de alterações do SO para o tema
window.matchMedia("(prefers-color-scheme: dark)").addEventListener("change", (e) => {
    if (!localStorage.getItem("color-scheme")) {
        currentTheme.value = e.matches ? "dark" : "light";
        toggleTheme();
    }
});

// Configuração de IntersectionObserver no Mounted (Animação de Scroll)
onMounted(() => {
    // Garantir que as classes no HTML batem com o estado reativo inicial
    document.documentElement.classList.remove("light", "dark");
    document.body.classList.remove("light", "dark");
    document.documentElement.classList.add("dark");
    document.body.classList.add("dark");

    // Tradução inicial
    document.documentElement.lang = currentLanguage.value;

    // Scroll Reveal Observer
    const revealElements = document.querySelectorAll(".scroll-reveal");
    const revealObserver = new IntersectionObserver((entries, observer) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.classList.add("visible");
                
                // Ativar animação das barras de skills
                if (entry.target.id === "skills") {
                    skillsVisible.value = true;
                }
                
                observer.unobserve(entry.target);
            }
        });
    }, {
        threshold: 0.15,
        rootMargin: "0px 0px -50px 0px"
    });

    revealElements.forEach(element => {
        revealObserver.observe(element);
    });
});

// --- LÓGICA DO MINI-TERMINAL INTERATIVO ---
const terminalOpen = ref(false);
const terminalInput = ref("");
const terminalHistory = ref([
    { text: "Bem-vindo ao UMinho LEI OS v2.0 (Terminal Interativo)!", type: "info" },
    { text: "Digita 'help' para veres uma lista dos comandos disponíveis.", type: "info" },
    { text: "", type: "break" }
]);

const terminalBody = ref(null);
const terminalInputRef = ref(null);

const scrollToBottom = () => {
    nextTick(() => {
        if (terminalBody.value) {
            terminalBody.value.scrollTop = terminalBody.value.scrollHeight;
        }
    });
};

const focusTerminalInput = () => {
    nextTick(() => {
        if (terminalInputRef.value) {
            terminalInputRef.value.focus();
        }
    });
};

const toggleTerminal = () => {
    terminalOpen.value = !terminalOpen.value;
    if (terminalOpen.value) {
        focusTerminalInput();
        scrollToBottom();
    }
};

const executeCommand = (cmdText) => {
    const rawCmd = cmdText.trim();
    if (!rawCmd) return;
    
    // Adiciona o comando ao histórico
    terminalHistory.value.push({ text: `guest@cerqueira.dev:~$ ${rawCmd}`, type: "command" });
    
    const args = rawCmd.split(/\s+/);
    const cmd = args[0].toLowerCase();
    
    switch (cmd) {
        case "clear":
            terminalHistory.value = [];
            break;
            
        case "help":
            terminalHistory.value.push({ text: "Comandos disponíveis:", type: "header" });
            terminalHistory.value.push({ text: "  about     - Uma breve apresentação sobre o meu percurso.", type: "text" });
            terminalHistory.value.push({ text: "  projects  - Lista detalhada dos meus projetos reais.", type: "text" });
            terminalHistory.value.push({ text: "  skills    - Apresenta as minhas competências com barras de nível.", type: "text" });
            terminalHistory.value.push({ text: "  neofetch  - Estatísticas do sistema em estilo retro ASCII.", type: "text" });
            terminalHistory.value.push({ text: "  contact   - Mostra as minhas ligações e e-mail oficiais.", type: "text" });
            terminalHistory.value.push({ text: "  clear     - Limpa o ecrã do terminal.", type: "text" });
            terminalHistory.value.push({ text: "  sudo      - Comando administrativo super-secreto.", type: "text" });
            break;
            
        case "about":
            terminalHistory.value.push({ text: "Sobre João Cerqueira:", type: "header" });
            terminalHistory.value.push({ text: "Estudante do 2.º Ano (2.º Semestre) de Engenharia Informática na Universidade do Minho.", type: "text" });
            terminalHistory.value.push({ text: "Focado em desenvolvimento de software eficiente, algoritmos e programação de baixo nível (SO/C).", type: "text" });
            break;
            
        case "projects":
            terminalHistory.value.push({ text: "Os meus projetos principais:", type: "header" });
            projectsData.forEach(p => {
                const titleStr = currentLanguage.value === 'pt' ? p.title.pt : p.title.en;
                terminalHistory.value.push({ text: `* ${titleStr} (${p.tags.slice(0, 3).join(', ')})`, type: "project-title" });
                terminalHistory.value.push({ text: `  -> Repo: ${p.github}`, type: "link" });
            });
            break;
            
        case "skills":
            terminalHistory.value.push({ text: "Competências e Proficiência:", type: "header" });
            languagesList.forEach(lang => {
                const barSize = Math.round(lang.percent / 10);
                const bar = "[" + "=".repeat(barSize) + " ".repeat(10 - barSize) + "]";
                terminalHistory.value.push({ text: `  ${lang.name.padEnd(12)} ${bar} ${lang.percent}%`, type: "skill" });
            });
            break;
            
        case "neofetch":
            terminalHistory.value.push({ text: "      .---.       guest@cerqueira.dev", type: "ascii" });
            terminalHistory.value.push({ text: "     /     \\      -------------------", type: "ascii" });
            terminalHistory.value.push({ text: "     \\_.._./      OS: UMinho LEI OS v2.0", type: "ascii" });
            terminalHistory.value.push({ text: "     `----'       Host: cerqueira-dev-box", type: "ascii" });
            terminalHistory.value.push({ text: "    /      \\      Kernel: Vue 3 / Vite 5", type: "ascii" });
            terminalHistory.value.push({ text: "   |  (o)(o) |     Uptime: 2 Anos (2º Ano 2º Semestre)", type: "ascii" });
            terminalHistory.value.push({ text: "   |    __   |     Shell: Bash (Custom Terminal)", type: "ascii" });
            terminalHistory.value.push({ text: "    \\  '--' /      IDE: Neovim / VS Code", type: "ascii" });
            terminalHistory.value.push({ text: "     `-----'       CPU: C & Haskell Compiler Engine", type: "ascii" });
            break;
            
        case "contact":
            terminalHistory.value.push({ text: "Informações de Contacto:", type: "header" });
            terminalHistory.value.push({ text: "  Email:  cerqueira.lei.uminho@example.com", type: "text" });
            terminalHistory.value.push({ text: "  GitHub: https://github.com/Cerqueira4618", type: "text" });
            break;
            
        case "sudo":
            if (args[1]) {
                terminalHistory.value.push({ text: `guest is not in the sudoers file. This incident will be reported.`, type: "error" });
            } else {
                terminalHistory.value.push({ text: "Uso: sudo [comando]", type: "error" });
            }
            break;
            
        default:
            terminalHistory.value.push({ text: `Comando não reconhecido: '${cmd}'. Digita 'help' para veres os comandos válidos.`, type: "error" });
    }
    
    // Reseta o input do terminal
    terminalInput.value = "";
    
    // Auto-scroll
    scrollToBottom();
};
</script>

<template>
    <!-- Grelha de Fundo Tecnológica (Grid Effect) -->
    <div class="tech-grid" aria-hidden="true"></div>
    <div class="glow-orb glow-1" aria-hidden="true"></div>
    <div class="glow-orb glow-2" aria-hidden="true"></div>

    <!-- Cabeçalho (Header) -->
    <header class="main-header glass">
        <div class="header-container">
            <a href="#" class="logo" id="logo-link">
                <span class="logo-accent">&lt;</span>cerqueira<span class="logo-accent">.dev /&gt;</span>
            </a>
            
            <nav class="nav-menu" :class="{ open: mobileMenuOpen }" id="navigation-menu">
                <a href="#about" class="nav-link" @click="closeMobileMenu">{{ t('nav_about') }}</a>
                <a href="#skills" class="nav-link" @click="closeMobileMenu">{{ t('nav_skills') }}</a>
                <a href="#projects" class="nav-link" @click="closeMobileMenu">{{ t('nav_projects') }}</a>
                <a href="#contact" class="nav-link" @click="closeMobileMenu">{{ t('nav_contact') }}</a>
            </nav>

            <div class="header-actions">
                <!-- Seletor de Idioma -->
                <button id="lang-toggle-btn" class="action-btn lang-btn" @click="toggleLanguage" :aria-label="currentLanguage === 'pt' ? 'Mudar para Inglês' : 'Switch to Portuguese'" :title="currentLanguage === 'pt' ? 'Mudar para Inglês' : 'Switch to Portuguese'">
                    <i class="fa-solid fa-globe"></i>
                    <span>{{ currentLanguage === 'pt' ? 'EN' : 'PT' }}</span>
                </button>

                
                <!-- Menu Mobile Hamburguer -->
                <button id="mobile-menu-btn" class="mobile-menu-toggle" :class="{ active: mobileMenuOpen }" @click="toggleMobileMenu" aria-label="Abrir menu" :aria-expanded="mobileMenuOpen">
                    <span class="bar"></span>
                    <span class="bar"></span>
                    <span class="bar"></span>
                </button>
            </div>
        </div>
    </header>

    <main class="content-wrapper">
        <!-- Hero Section -->
        <section id="hero" class="hero-section">
            <div class="hero-content">
                <div class="badge-container animate-fade-in">
                    <span class="status-badge">
                        <span class="pulse-dot"></span> {{ t('hero_badge') }}
                    </span>
                </div>
                <h1 class="hero-title animate-title">
                    <span>{{ t('hero_title_1') }} </span>
                    <span class="text-gradient">Cerqueira</span>
                </h1>
                <p class="hero-subtitle animate-fade-in">
                    {{ t('hero_subtitle') }}
                </p>
                
                <div class="hero-ctas animate-fade-in">
                    <a href="#projects" class="btn btn-primary" id="hero-btn-projects">
                        <span>{{ t('hero_cta_primary') }}</span>
                        <i class="fa-solid fa-arrow-right"></i>
                    </a>
                    <a href="#contact" class="btn btn-secondary" id="hero-btn-contact">
                        {{ t('hero_cta_secondary') }}
                    </a>
                </div>

                <div class="hero-socials animate-fade-in">
                    <a href="https://github.com/Cerqueira4618" target="_blank" rel="noopener noreferrer" aria-label="GitHub Profile" title="GitHub">
                        <i class="fa-brands fa-github"></i>
                    </a>
                    <a href="https://linkedin.com" target="_blank" rel="noopener noreferrer" aria-label="LinkedIn Profile" title="LinkedIn">
                        <i class="fa-brands fa-linkedin"></i>
                    </a>
                    <a href="mailto:cerqueira.lei.uminho@example.com" aria-label="Enviar Email" title="Email">
                        <i class="fa-solid fa-envelope"></i>
                    </a>
                </div>
            </div>
            
            <div class="hero-graphic animate-fade-in">
                <div class="code-window glass">
                    <div class="window-header">
                        <span class="dot red"></span>
                        <span class="dot yellow"></span>
                        <span class="dot green"></span>
                        <span class="window-title">student.hs</span>
                    </div>
                    <div class="window-body">
                        <pre><code><span class="keyword">module</span> <span class="type">Student</span> <span class="keyword">where</span>

<span class="keyword">data</span> <span class="type">Developer</span> = <span class="type">Developer</span> 
  { name     :: <span class="type">String</span>
  , course   :: <span class="type">String</span>
  , semester :: <span class="type">String</span>
  , skills   :: [<span class="type">String</span>]
  }

<span class="function">me</span> :: <span class="type">Developer</span>
<span class="function">me</span> = <span class="type">Developer</span>
  { name     = <span class="string">"Cerqueira"</span>
  , course   = <span class="string">"LEI @ UMinho"</span>
  , semester = <span class="string">"2º Ano - 2º Semestre"</span>
  , skills   = [<span class="string">"C"</span>, <span class="string">"Haskell"</span>, <span class="string">"Java"</span>, <span class="string">"SQL"</span>]
  }</code></pre>
                    </div>
                </div>
            </div>
        </section>

        <!-- Sobre Mim Section -->
        <section id="about" class="about-section scroll-reveal">
            <div class="section-header">
                <h2 class="section-title">{{ t('about_title') }}</h2>
                <div class="accent-line"></div>
            </div>
            
            <div class="about-grid">
                <div class="about-text glass">
                    <p v-html="t('about_p1')"></p>
                    <p v-html="t('about_p2')"></p>
                    <div class="stats-grid">
                        <div class="stat-card">
                            <span class="stat-num">2º</span>
                            <span class="stat-label">{{ t('stat_year') }}</span>
                        </div>
                        <div class="stat-card">
                            <span class="stat-num">5+</span>
                            <span class="stat-label">{{ t('stat_languages') }}</span>
                        </div>
                        <div class="stat-card">
                            <span class="stat-num">4</span>
                            <span class="stat-label">{{ t('stat_projects') }}</span>
                        </div>
                    </div>
                </div>
                
                <div class="about-timeline glass">
                    <h3 class="timeline-title">{{ t('timeline_title') }}</h3>
                    
                    <div class="timeline">
                        <!-- 2º Ano -->
                        <div class="timeline-item">
                            <div class="timeline-dot"></div>
                            <div class="timeline-content">
                                <span class="timeline-date">2025 - Presente</span>
                                <h4 class="timeline-heading">{{ t('timeline_y2_title') }}</h4>
                                <p>{{ t('timeline_y2_desc') }}</p>
                            </div>
                        </div>
                        
                        <!-- 1º Ano -->
                        <div class="timeline-item">
                            <div class="timeline-dot"></div>
                            <div class="timeline-content">
                                <span class="timeline-date">2024 - 2025</span>
                                <h4 class="timeline-heading">{{ t('timeline_y1_title') }}</h4>
                                <p>{{ t('timeline_y1_desc') }}</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Competências (Skills) Section -->
        <section id="skills" class="skills-section scroll-reveal">
            <div class="section-header">
                <h2 class="section-title">{{ t('skills_title') }}</h2>
                <div class="accent-line"></div>
            </div>
            
            <div class="skills-grid">
                <!-- Categoria 1: Linguagens -->
                <div class="skills-category glass">
                    <div class="category-header">
                        <i class="fa-solid fa-code"></i>
                        <h3>{{ t('skills_cat_languages') }}</h3>
                    </div>
                    <div class="skills-list">
                        <div class="skill-item" v-for="skill in languagesList" :key="skill.name">
                            <div class="skill-info">
                                <span>{{ skill.name }}</span>
                                <span class="skill-level">{{ currentLanguage === 'pt' ? skill.level.pt : skill.level.en }}</span>
                            </div>
                            <div class="skill-bar-wrapper">
                                <div class="skill-bar" :style="{ width: (skillsVisible ? skill.percent : 0) + '%' }"></div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Categoria 2: Ferramentas e Metodologias -->
                <div class="skills-category glass">
                    <div class="category-header">
                        <i class="fa-solid fa-screwdriver-wrench"></i>
                        <h3>{{ t('skills_cat_tools') }}</h3>
                    </div>
                    <div class="skills-list">
                        <div class="skill-item" v-for="skill in toolsList" :key="skill.name">
                            <div class="skill-info">
                                <span>{{ skill.name }}</span>
                                <span class="skill-level">{{ currentLanguage === 'pt' ? skill.level.pt : skill.level.en }}</span>
                            </div>
                            <div class="skill-bar-wrapper">
                                <div class="skill-bar" :style="{ width: (skillsVisible ? skill.percent : 0) + '%' }"></div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Projetos Section -->
        <section id="projects" class="projects-section scroll-reveal">
            <div class="section-header">
                <h2 class="section-title">{{ t('projects_title') }}</h2>
                <div class="accent-line"></div>
            </div>
            
            <!-- Barra de Filtros -->
            <div class="projects-filter-bar">
                <button class="filter-btn" :class="{ active: activeFilter === 'all' }" @click="setFilter('all')">
                    {{ t('filter_all') }}
                </button>
                <button class="filter-btn" :class="{ active: activeFilter === 'uminho' }" @click="setFilter('uminho')">
                    {{ t('filter_academic') }}
                </button>
                <button class="filter-btn" :class="{ active: activeFilter === 'personal' }" @click="setFilter('personal')">
                    {{ t('filter_personal') }}
                </button>
            </div>
            
            <!-- Grelha de Projetos reativa do Vue -->
            <div class="projects-grid" id="projects-container">
                <div class="project-card glass scroll-reveal visible" v-for="project in filteredProjects" :key="project.id" :data-category="project.category">
                    <div class="project-card-header">
                        <span class="project-category-tag">
                            {{ project.category === 'uminho' ? 'UMinho' : (currentLanguage === 'pt' ? 'Pessoal' : 'Personal') }}
                        </span>
                        <div class="project-links">
                            <a v-if="project.github" :href="project.github" target="_blank" rel="noopener noreferrer" aria-label="GitHub Repository" title="Repositório GitHub">
                                <i class="fa-brands fa-github"></i>
                            </a>
                            <a v-if="project.demo" :href="project.demo" target="_blank" rel="noopener noreferrer" aria-label="Live Demo" title="Ver Aplicação">
                                <i class="fa-solid fa-arrow-up-right-from-square"></i>
                            </a>
                        </div>
                    </div>
                    <div class="project-card-body">
                        <h3 class="project-card-title">{{ currentLanguage === 'pt' ? project.title.pt : project.title.en }}</h3>
                        <p class="project-card-desc">{{ currentLanguage === 'pt' ? project.desc.pt : project.desc.en }}</p>
                        <div class="project-tags">
                            <span class="project-tag" v-for="tag in project.tags" :key="tag">{{ tag }}</span>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Contacto Section -->
        <section id="contact" class="contact-section scroll-reveal">
            <div class="section-header">
                <h2 class="section-title">{{ t('contact_title') }}</h2>
                <div class="accent-line"></div>
            </div>
            
            <div class="contact-card glass">
                <div class="contact-icon-container">
                    <i class="fa-solid fa-paper-plane text-gradient-icon"></i>
                </div>
                <h3>{{ t('contact_subtitle') }}</h3>
                <p v-html="t('contact_p')"></p>
                
                <div class="contact-details">
                    <div class="contact-item">
                        <i class="fa-solid fa-envelope"></i>
                        <span id="email-address">cerqueira.lei.uminho@example.com</span>
                        <button id="copy-email-btn" class="copy-btn" @click="copyEmail" :class="{ success: emailCopied }" aria-label="Copiar email" title="Copiar email">
                            <i class="fa-regular fa-copy icon-copy" v-if="!emailCopied"></i>
                            <i class="fa-solid fa-check icon-check" v-else></i>
                        </button>
                    </div>
                </div>
                
                <div class="contact-social-grid">
                    <a href="https://github.com/Cerqueira4618" target="_blank" rel="noopener noreferrer" class="social-card glass">
                        <i class="fa-brands fa-github"></i>
                        <span>GitHub</span>
                    </a>
                    <a href="https://linkedin.com" target="_blank" rel="noopener noreferrer" class="social-card glass">
                        <i class="fa-brands fa-linkedin"></i>
                        <span>LinkedIn</span>
                    </a>
                </div>
            </div>
        </section>
    </main>

    <!-- Rodapé (Footer) -->
    <footer class="main-footer">
        <div class="footer-content">
            <p>&copy; 2026 Cerqueira. <span>{{ t('footer_rights') }}</span></p>
            <p class="footer-subtext">{{ t('footer_tag') }}</p>
        </div>
    </footer>

    <!-- Botão Flutuante do Terminal -->
    <button class="terminal-toggle-btn glass" @click="toggleTerminal" aria-label="Abrir Terminal" title="Abrir Terminal Interativo">
        <i class="fa-solid fa-terminal" v-if="!terminalOpen"></i>
        <i class="fa-solid fa-xmark" v-else></i>
    </button>

    <!-- Janela do Terminal -->
    <div class="terminal-window glass" :class="{ open: terminalOpen }" @click="focusTerminalInput">
        <div class="terminal-header">
            <div class="window-controls">
                <span class="dot red" @click.stop="toggleTerminal"></span>
                <span class="dot yellow"></span>
                <span class="dot green"></span>
            </div>
            <span class="terminal-title">guest@cerqueira.dev:~</span>
        </div>
        <div class="terminal-body" ref="terminalBody">
            <div v-for="(line, idx) in terminalHistory" :key="idx" :class="['terminal-line', line.type]">
                <span v-if="line.type === 'ascii'" class="ascii-art">{{ line.text }}</span>
                <span v-else-if="line.type === 'error'" class="text-error"><i class="fa-solid fa-triangle-exclamation"></i> {{ line.text }}</span>
                <span v-else-if="line.type === 'header'" class="text-gradient font-bold">{{ line.text }}</span>
                <span v-else v-html="line.text"></span>
            </div>
        </div>
        <div class="terminal-input-wrapper">
            <span class="terminal-prompt">guest@cerqueira.dev:~$</span>
            <input 
                ref="terminalInputRef" 
                v-model="terminalInput" 
                type="text" 
                class="terminal-input" 
                @keydown.enter="executeCommand(terminalInput)" 
                placeholder="Digita 'help'..."
                autocomplete="off"
                autocorrect="off"
                autocapitalize="off"
                spellcheck="false"
            />
        </div>
    </div>
</template>

<style>
/* Ocular flashes de compilação do Vue em ambientes sem pré-renderização */
[v-cloak] {
    display: none !important;
}
</style>
