# Otimizador ATS (ATS Resume Matcher)

Aplicação web desenvolvida para alinhar o currículo do candidato aos requisitos de uma vaga específica, aumentando suas chances de aprovação em processos seletivos que utilizam sistemas de triagem automática (ATS).

🔗 **Aplicação publicada:** [https://pixel-perfect-replay-52315.lovable.app/](https://pixel-perfect-replay-52315.lovable.app/)

---

## 🎯 Qual problema a aplicação resolve?

Muitos candidatos qualificados são descartados logo na triagem inicial porque seus currículos não contêm as palavras-chave exatas exigidas pela vaga ou possuem elementos visuais (colunas, gráficos, tabelas) que dificultam a leitura pelos softwares de recrutamento (ATS — *Applicant Tracking Systems*). 

O **Otimizador ATS** resolve esse problema automatizando a análise de aderência entre o currículo atual e a descrição da vaga, gerando uma versão reestruturada, limpa e com foco em impacto mensurável, pronta para download em PDF.

---

## ⚙️ Como a análise funciona

O fluxo da aplicação transforma os dados brutos enviados pelo usuário em um documento otimizado em quatro etapas:

1. **Entrada e Extração de Dados:** O usuário faz o upload do currículo original (`.pdf` ou `.docx`) e cola o texto completo da vaga desejada. A aplicação extrai o texto do arquivo diretamente no navegador.
2. **Mapeamento de Requisitos e Lacunas:** O motor de análise identifica as *hard skills*, ferramentas, metodologias e palavras-chave críticas presentes na descrição da vaga e cruza com o histórico do candidato.
3. **Reescrita Orientada a Impacto:** Os tópicos de experiência são reformulados incorporando as palavras-chave relevantes de forma natural (sem *keyword stuffing*) e aplicando a fórmula: `[Verbo de ação forte] + [Contexto/Tecnologia] + [Resultado mensurável]`.
4. **Comparação e Exportação ATS-Friendly:** O sistema exibe a taxa de compatibilidade (antes vs. depois) e apresenta o currículo original lado a lado com a versão otimizada — estruturada em cabeçalhos padronizados e livre de ruídos gráficos — permitindo edição rápida e download direto em PDF.

---

## 🧠 Evolução do Mega Prompt

Para construir a aplicação no Lovable, o prompt passou por uma refinação importante entre a concepção inicial e a versão final utilizada na geração:

### O que mudou do prompt inicial para o final?
- **Idioma e Localização:** O prompt inicial estava misturado entre inglês e português; na versão final, toda a especificação foi traduzida e padronizada para o português, garantindo que textos de interface, placeholders e regras de saída fossem gerados nativamente no idioma do usuário.
- **Regras de Negócio mais Rígidas (Anti-Keyword Stuffing):** Na versão final, foi adicionada uma restrição explícita proibindo a repetição forçada de palavras-chave (*keyword stuffing*) e exigindo que os verbos de ação fossem conjugados no passado, acompanhados de exemplos concretos de reescrita.
- **Usabilidade do Fluxo Secundário:** O botão de retorno ("Otimizar Outra Vaga") foi refinado para limpar apenas a descrição da vaga, mantendo o currículo carregado caso o usuário queira testar várias oportunidades em sequência.
- **Detalhamento Visual e Técnico:** Foram especificadas classes exatas do Tailwind CSS, restrições de elementos gráficos que quebram leitores de RH (como barras de progresso de habilidades) e requisitos de legibilidade OCR para a exportação em PDF.

```markdown
Primeira versão do mega prompt
# ATS Resume Matcher & Optimizer

## 1. Project Overview
A web application that takes an existing candidate resume (PDF/DOCX) and a job description text, analyzes keyword gaps and formatting issues, and generates an optimized, ATS-friendly resume displayed in a side-by-side comparison view with instant clean PDF download.

## 2. User Flow & Screens
### Screen 1: Input & Configuration
- Header: Minimalist logo, title ("ATS Resume Matcher"), and a short subtitle explaining the value in one sentence.
- Left Column / Dropzone: Drag-and-drop file upload supporting .pdf and .docx. Shows file name, size, and a remove/replace button once uploaded.
- Right Column / Job Description Input: Large textarea with placeholder: "Paste the complete job description here (responsibilities, requirements, tech stack)...". Character/word counter.
- Action Button: "Analisar e Otimizar Currículo" (disabled until both inputs are provided).

### Processing State (Loading State)
- Skeleton loader or subtle progress indicator showing active steps:
  1. Lendo currículo original...
  2. Extraindo requisitos e palavras-chave da vaga...
  3. Reescrevendo tópicos com verbos de ação e métricas...
  4. Formatando versão ATS limpa...

### Screen 2: Side-by-Side Comparison & Export
- Top Bar: Quick match score (% de aderência antes vs. depois). Main Action Button: "Baixar Currículo em PDF". Secondary Action: "Voltar e testar outra vaga".
- Left Panel (Original Resume): Read-only visual representation of the original text/structure.
- Right Panel (ATS-Friendly Version): Clean, high-legibility document layout. Highlights added keywords and improved bullet points with subtle badges or tooltips explaining the rationale. Option to edit inline.

## 3. ATS Optimization Engine (Logic & Transformation Rules)
1. Keyword Integration: Naturally weave in mandatory hard skills and technical tools found in the job description that are relevant to the candidate's background.
2. Action-Oriented Bullet Points: Use the formula: [Verbo de ação forte] + [Tarefa/Contexto] + [Resultado mensurável ou impacto].
3. Clean ATS Structure: Standardized headings (Dados de Contato, Resumo Profissional, Habilidades Técnicas, Experiência Profissional, Formação Acadêmica, Certificações). No multi-column layouts, graphics, icons, or complex tables.

## 4. Design System (Minimalist Light Mode)
- Style: Clean, Swiss-inspired typography, spacious layout, high contrast, distraction-free.
- Color Palette: Background #FFFFFF / #F8FAFC, Borders #E2E8F0, Text #0F172A / #64748B, Accent #000000 / #0F172A, Highlight #10B981.
- Typography: Sans-serif (Inter or Geist).
- Components: Shadcn/UI.

## 5. Technical Requirements & PDF Export
- Support client-side text extraction from uploaded PDF/DOCX.
- PDF generation with standard margins (1 inch / 2.5 cm), ATS-safe font, and direct download trigger.
```
```markdown
# Otimizador de Currículo ATS (ATS Resume Matcher)

## 1. Visão Geral do Projeto
Uma aplicação web moderna que recebe o currículo atual do candidato (upload em PDF ou DOCX) e o texto descritivo de uma vaga de emprego. A aplicação analisa lacunas de palavras-chave, requisitos técnicos e problemas de formatação, gerando uma versão otimizada e 100% amigável para sistemas ATS (Applicant Tracking Systems). O resultado é apresentado em uma visualização comparativa lado a lado (original vs. otimizado), com download imediato do novo currículo em formato PDF limpo e padronizado.

## 2. Fluxo do Usuário e Telas
### Tela 1: Entrada de Dados (Upload e Vaga)
- Cabeçalho: Logotipo discreto, título da aplicação ("Otimizador ATS") e subtítulo claro explicando o propósito da ferramenta.
- Área de Entrada Dividida em Duas Colunas:
  - Coluna da Esquerda (Currículo Base): Área de arrastar e soltar (drag-and-drop) para upload de arquivos .pdf e .docx. Feedback visual de arquivo carregado com nome do arquivo, tamanho e botão para remover ou substituir.
  - Coluna da Direita (Descrição da Vaga): Campo de texto multilinha (Textarea) amplo e com rolagem suave. Placeholder: "Cole aqui o texto completo da descrição da vaga (responsabilidades, requisitos obrigatórios, diferenciais e tecnologias)...". Contador de caracteres/palavras em tempo real.
- Ação Principal: Botão destacado: "Analisar e Otimizar Currículo" (desabilitado enquanto o arquivo ou o texto da vaga não forem preenchidos).

### Estado de Processamento (Carregamento / Loading)
- Indicador de progresso elegante e minimalista com mensagens sequenciais de feedback:
  1. Extraindo conteúdo do currículo original...
  2. Mapeando requisitos e palavras-chave da vaga...
  3. Reescrevendo tópicos de experiência com foco em impacto e métricas...
  4. Formatando estrutura compatível com leitores ATS...

### Tela 2: Comparação Lado a Lado e Exportação
- Barra Superior de Ações:
  - Indicador de compatibilidade (% de aderência à vaga estimada antes vs. depois).
  - Botão Principal de Exportação: "Baixar Currículo em PDF" (com ícone de download).
  - Botão Secundário: "Otimizar Outra Vaga" (retorna à Tela 1 limpando a vaga mas mantendo o currículo se o usuário desejar).
- Painel da Esquerda (Currículo Original): Exibição em modo somente leitura do conteúdo original para referência rápida do usuário.
- Painel da Direita (Versão Otimizada ATS): Layout limpo, organizado e com alta legibilidade. Destaque sutil (badges ou marcações em verde suave) nas palavras-chave incorporadas e nas frases aprimoradas. Possibilidade de edição rápida caso o usuário queira ajustar algum detalhe antes de exportar.

## 3. Regras de Negócio e Otimização ATS
1. Incorporação Natural de Palavras-Chave: Identificar termos técnicos essenciais, metodologias, ferramentas e certificações citadas na descrição da vaga. Integrar esses termos de maneira contextualizada e honesta nas seções de Habilidades e Experiência do candidato, evitando o "keyword stuffing" (repetição forçada de palavras).
2. Fórmula de Conquistas Orientadas a Ação: Reescrever as atribuições de trabalho usando a estrutura: [Verbo de Ação Forte no Passado] + [Contexto/Tecnologia utilizada] + [Impacto ou Métrica Mensurável].
3. Estrutura Padrão ATS (Sem Ruído Gráfico): Cabeçalhos de seção padronizados (Dados Pessoais / Contato, Resumo Profissional, Habilidades Técnicas, Experiência Profissional, Formação Acadêmica, Cursos e Certificações). Proibição estrita de tabelas complexas, gráficos de nível de conhecimento, caixas de texto flutuantes ou ícones decorativos.

## 4. Design System & Interface (Modo Claro Minimalista)
- Estilo: Estética minimalista, profissional e funcional (inspiração: Notion / Linear Light).
- Paleta de Cores (Tailwind CSS): Fundo #FFFFFF e bg-slate-50, bordas border-slate-200, tipografia text-slate-900 e text-slate-500, botão primário bg-black / bg-slate-900, destaques emerald-600 com fundo emerald-50.
- Tipografia: Fonte sem serifa moderna (Inter ou Geist).
- Componentes: Shadcn/UI (Button, Card, Textarea, Badge, Progress, Tooltip, Dialog).

## 5. Requisitos Técnicos e Exportação do PDF
- Manipulação de Arquivos: Leitura e extração do texto dos arquivos PDF e DOCX enviados no navegador.
- Geração de PDF: Download direto de um arquivo formatado para impressão/A4 com margens padrão (1 polegada / 2,5 cm) e tipografia legível por OCR.
```
Iterações e Ajustes Pós-Geração
Não foram solicitados ajustes adicionais após a primeira geração por dois motivos principais:

Aderência na primeira entrega: Como o mega prompt foi estruturado de forma detalhada e modular antes da execução, a primeira versão gerada já atendeu fielmente ao fluxo, ao design minimalista e às funcionalidades esperadas.

Gestão de recursos (créditos): Devido ao limite de créditos disponíveis na plataforma, optou-se por concentrar os esforços na engenharia prévia do prompt para obter um resultado sólido logo na primeira geração, evitando rodadas extras de refatoração.

Tecnologias Utilizadas
React + TypeScript + Vite

Tailwind CSS & Shadcn/UI (Interface e componentes visuais)

Lovable (Geração e hospedagem da aplicação)
