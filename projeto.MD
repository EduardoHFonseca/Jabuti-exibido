# Jabuti Exibido

## Definição do Projeto
O projeto **Jabuti Exibido** monitora projetos de lei em sites governamentais através de um Web Crawler. O sistema extrai informações, armazena em um RAG (Retrieval-Augmented Generation) e utiliza um LLM para identificar "Jabutis" — trechos inseridos em PLs sem relação com o objetivo primário da norma. O sistema fornece análises técnicas sobre riscos fiscais, jurídicos e ambientais para auxiliar parlamentares e o público.

## Funcionalidades Principais
- **Web Crawler:** Varredura periódica de sites (Câmara, Senado, DOU).
- **RAG System:** Busca semântica baseada na Constituição Federal, leis vigentes e histórico de projetos rejeitados.
- **LLM Processing:** 
  - Identificação de "Jabutis" (contrabando legislativo).
  - **9 Quesitos de Análise IA:** Criação de Impostos, Aumento do Estado, Censura & Regulação, Cartel & Monopólio, Benefício Social, Impacto Ambiental, Confusão Jurídica, Fragmentação Normativa e Avança competências.
  - **Customização por Partido:** Filtros ideológicos e técnicos específicos por agremiação (ex: NOVO, PT, PL).
  - **Comparação Histórica:** Detecção de reintrodução de textos (fatiamento legislativo).
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
    - Orientações: Partido, Bancada e sua inclinação pessoal.
    - **Percepção da Casa/Partido:** Slider gradiente (Verde/Amarelo/Vermelho) dinâmico por perfil.
    - **Notas do Gabinete:** Espaço para comentários internos.
- **Análise IA (Riscos & Alertas):** Lista de 9 quesitos com níveis de risco (Alto, Moderado, Baixo) e Impacto Ambiental (Positivo, Neutro, Negativo).
- **Parecer Técnico (Análise Detalhada):** Estrutura modular (O que é, Jabuti Detectado, Impacto Técnico, Recomendação, Confronto RAG).

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

## Backlog Pendente
- [ ] Listar URLs exatas da API da Câmara e Senado.
- [ ] Implementar Backend base em FastAPI.
- [ ] Desenvolver PoC do Crawler com Playwright.
- [ ] Configurar busca vetorial (RAG) para histórico legislativo.
