# Jabuti Exibido

## Definição do Projeto
O projeto **Jabuti Exibido** monitora projetos de lei em sites governamentais através de um Web Crawler. O sistema extrai informações, armazena em um RAG (Retrieval-Augmented Generation) e utiliza um LLM para identificar "Jabutis" — trechos inseridos em PLs sem relação com o objetivo primário da norma. O sistema fornece análises técnicas sobre riscos fiscais, jurídicos e ambientais para auxiliar parlamentares e o público.

## Funcionalidades Principais
- **Web Crawler:** Varredura periódica de sites (Câmara, Senado, DOU).
- **RAG System (Detector de Reencarnação):** Busca semântica e comparação de embeddings a nível de artigo para detectar reintrodução de textos rejeitados ou já votados.
- **Snapshotting & Versionamento:** Captura e armazenamento de todas as versões de um PL (Original, Substitutivos, Emendas) para detectar fatiamento legislativo e mudanças súbitas de texto.
- **Memória do Parlamentar:** Cruzamento automático do texto atual com o histórico de votos do usuário, sinalizando alinhamento ou contradição com posições passadas.
- **LLM Processing:** 
  - Identificação de "Jabutis" (contrabando legislativo).
  - **9 Quesitos de Análise IA:** Criação de Impostos, Aumento do Estado, Censura & Regulação, Cartel & Monopólio, Benefício Social, Impacto Ambiental, Confusão Jurídica, Fragmentação Normativa e Cria discricionariedade.
  - **Customização por Partido:** Filtros ideológicos e técnicos específicos por agremiação (ex: NOVO, PT, PL).
  - **Comparação Histórica (Deep Diff):** Detecção de fatiamento através da comparação entre versões do mesmo projeto.
- **Integração Mobile:** Interface de alta legibilidade para consulta de pauta e alertas em tempo real.

## Arquitetura e Stack Técnica
| Componente | Tecnologia |
| :--- | :--- |
| **Backend + API** | Python (FastAPI) |
| **Banco de Dados** | Supabase (PostgreSQL + pgvector) |
| **LLM (IA)** | Groq / OpenAI (GPT-4o) |
| **Crawler** | Playwright (Python) |
| **Hospedagem** | GitHub (Hospedagem de Protótipo: here.now) |

## Detalhamento de Telas (Status Atual)

### 1. Perfil Parlamentar / Consumidor
- **Login:** Splash screen com logo e preview de notificações (PLs Novos/Alterados).
- **Projetos em Pauta:** Lista simplificada com títulos curtos e status.
- **Ficha Técnica (Capa):** 
    - Identificação: Nro, Autor, Estado, Regime de Urgência.
    - **Alerta de DNA Legislativo:** Badge de alerta rápido na capa caso haja reencarnação de texto detectada.
    - Orientações: Partido, Bancada e sua inclinação pessoal.
    - **Percepção da Casa/Partido:** Slider gradiente (Verde/Amarelo/Vermelho) dinâmico por perfil.
    - **Notas do Gabinete:** Espaço para comentários internos.
- **Análise IA (Riscos & Alertas):** Lista de 9 quesitos com níveis de risco (Alto, Moderado, Baixo) e Impacto Ambiental.
    - **Alerta de Reencarnação:** Indicador visual específico. 
        - Botão Vermelho com contador (ex: [2]) se houver fatiamento detectado.
        - Botão Verde com [0] se o texto for inédito/limpo.
- **Parecer Técnico (Análise Detalhada):** Estrutura modular (O que é, Jabuti Detectado, Impacto Técnico, Recomendação, Confronto RAG).
    - **Card de Reencarnação (Sub-tela):** Mesma diagramação de riscos altos/moderados, detalhando o histórico do DNA do texto:
        - *Exemplo 1:* "Capítulo IV, art.18 foi tentado no PL 2345/2017 votado em Out.21 (rejeitado) e na PEC 23/2019 votada em Abril 22 (vetada)".
        - *Exemplo 2:* "Seção II, art.5º (Regulação de IA) identificado como cópia integral do Substitutivo do PL 456/2021, retirado de pauta por falta de quórum em Dez.23".

### 2. Perfil Operador / Gestor
- **Gestão de Fontes:** Grid de URLs com controle de periodicidade e horário de busca.
- **Captura Manual:** Interface para forçar a busca de um projeto específico.
- **Console de Operações:** Log em tempo real das atividades do crawler e da IA.
- **Editor de Jabutis:** Interface de validação humana (Split View) com navegador de quesitos e ajuste de pareceres antes da publicação.

## Status do Desenvolvimento
- [x] **Protótipo Interativo:** Finalizado e publicado (Desktop & Mobile).
- [x] **Definição de Fluxos:** Parlamentar e Operador mapeados.
- [x] **Integração GitHub:** Repositório inicializado e sincronizado.
- [ ] **Próxima Etapa:** Modelagem do Schema de Banco de Dados no Supabase.

- [ ] **Chat Contextual:** Interface de diálogo para perguntas e respostas sobre o projeto.
- [ ] **Filtros por Tema (IA):** Subitens na tela de riscos para perguntas rápidas sugeridas.

## Backlog Pendente
- [ ] **Mapeamento de APIs:** Listar URLs da API da Câmara e Senado, focando em "Inteiro Teor" e histórico de votações.
- [ ] **Schema do Banco (Supabase):** Modelagem de tabelas para `proposicao_versoes` e `vetores_legislativos`.
- [ ] **PoC do Crawler (Playwright):** Script para captura de PDFs e textos de múltiplas versões de um projeto.
- [ ] **Configuração pgvector:** Implementar a lógica de busca por "Reencarnação" de artigos.
- [ ] **Backend Base (FastAPI):** Estrutura inicial para servir dados e integrar com LLM.
- [ ] **Sugestões Rápidas de IA:** Organizar como subitens na tela de riscos e alertas.

## Backlog de UI & UX (Melhorias Sugeridas)
- [ ] **Badge de Consistência Política:** Sinalização visual na Capa baseada no histórico de votos (Memória do Parlamentar).
- [ ] **Tela de Comparação de Versões (Deep Diff):** Interface para visualizar fatiamento legislativo (Original vs Substitutivo).
- [ ] **Tela de Memória do Parlamentar:** Detalhamento dos votos históricos cruzados com o PL atual.
- [ ] **Interatividade nos 9 Quesitos:** Permitir expansão de justificativas para todos os níveis de risco (Alto, Médio, Baixo).
- [ ] **Editor de Jabutis (Split View):** Interface lado-a-lado para validação humana no perfil Operador.
- [ ] **Navegação Inferior (Bottom Nav):** Menu de acesso rápido (Pauta, Busca, Alertas) para perfil Parlamentar.
- [ ] **Polimento Visual:** Implementação de Glassmorphism, sombras suaves e micro-interações de processamento de IA.
- [ ] **Onboarding & Router de Personas:** Tela de entrada para segmentação (Cidadão, Imprensa, Gabinete, Parlamentar).
- [ ] **Landing Page de Planos:** Interface de checkout para planos Simbólico (Cidadão) e Premium (Imprensa).
- [ ] **Histórico de Consultas IA:** Registro persistente das conversas no Chat Contextual, organizado por projeto e parlamentar.
- [ ] **Favoritos na Análise:** Funcionalidade na tela de Análise para favoritar artigos específicos ou respostas da IA (itens para "bater o pé").
- [ ] **Indicador de Favoritos na Capa:** Sinalização visual na Ficha Técnica (Capa) informando que existem itens marcados como importantes naquele projeto.
- [ ] **Dashboard de Dúvidas Recentes (Operador):** Painel anonimizado de "Trending Topics" para identificar trechos ambíguos nos projetos baseados nas perguntas frequentes dos parlamentares.

## Regras de Negócio e Gestão de Licenças (Backlog)
- [ ] **Gestão de Licenças de Gabinete:**
    *   Definição de limites de licenças por parlamentar (ex: base + assessores).
    *   Fluxo de pagamento e faturamento (Mensalidade/Anuidade).
    *   Regras de Bloqueio Automático por inadimplência.
    *   Liberação manual de usuários em contingência.
    *   Sincronização de status "Ativo/Inativo" entre Gestão de Parlamentares e acesso ao App.
- [ ] **Segurança e Autenticação Crítica:**
    *   **Confirmação de Identidade:** Parlamentares e Assessores ficam com status "Pendente de Autenticação" até validação manual ou por documento/e-mail institucional para evitar personificação e influência indevida em votações.
    *   **Reset de Senha Seguro:** Definição de fluxos rigorosos de recuperação de conta para perfis de Gabinete, visando mitigar riscos de engenharia social.

## Regras de Negócio e Fluxos Específicos

### Métricas de Engajamento Partidário
- [ ] **Estratégia de Monetização e Acesso:**
    - **Cidadão (Freemium):** App em lojas (Play/Apple) com acesso a resumos IA; Chat IA ilimitado via taxa simbólica.
    - **Imprensa (Premium):** Assinatura para acesso a dados agregados, alertas de DNA repetido e tendências de bancada.
- [ ] **Definir lógica de cálculo:**
    - **Orientação Definida:** % de projetos em que a liderança registrou orientação oficial vs. total de projetos analisados.
    - **Engajamento de Escolha:** Média percentual de "Inclinação Pessoal" preenchida pelos deputados do partido.
- [ ] **Taxonomia da Dúvida (IA):**
    - Implementar classificador de intenção para categorizar consultas em: *Clareza de Redação, Impacto Prático, Risco/Conformidade e Posicionamento*.
    - **Log de Dúvidas:** Persistir cada consulta vinculada ao parlamentar e projeto para análise de tendências e predição de comportamento.
    - **Alerta de Ambiguidade:** Disparar alerta visual na tela do parlamentar caso o volume de dúvidas de "Redação" ou "Risco" ultrapasse um limiar crítico (indicando texto obscuro ou perigoso).

### Orientação de Bancada e Liderança
1. **Definição de Líder:** No Painel de Controle, um parlamentar pode ser designado como "Líder do Partido".
2. **Fluxo de Orientação:**
   - Quando um novo projeto é capturado e analisado, a **Orientação do Partido** nasce automaticamente como **Neutra**.
   - O Líder do Partido possui o poder de definir a orientação oficial.
   - Assim que o Líder registra sua escolha (Sim/Não/Abster) na tela de Ficha Técnica, essa decisão é propagada como a "Orientação do Partido" para todos os outros parlamentares da mesma agremiação.
   - O sistema envia uma notificação de atualização assim que o Líder define o posicionamento.

## Conclusões Técnicas de Pré-Projeto
1. **Infraestrutura:** O sistema requer execução 24/7 para crawlers agendados e processamento assíncrono de RAG.
2. **Escalabilidade:** O uso de embeddings por artigo (chunking granular) é essencial para detectar fatiamento e reencarnação de textos em diferentes projetos.
3. **Persistência Offline (PWA):** O front-end deve suportar cache local (Local Storage) para permitir consulta de pautas e análises em ambientes sem conexão.
4. **Segurança de Dados:** Armazenamento do histórico de votos do parlamentar para cruzamento de dados e alertas personalizados de consistência política.
