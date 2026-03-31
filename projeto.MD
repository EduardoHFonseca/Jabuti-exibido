# Jabuti Exibido

## Definição do Projeto
O objetivo do projeto **Jabuti Exibido** é monitorar projetos de lei em sites governamentais através de um Web Crawler. O sistema extrairá informações, armazenará em um RAG (Retrieval-Augmented Generation) e utilizará um LLM para identificar "Jabutis" — trechos de texto inseridos em projetos de lei que não possuem relação direta com o objetivo primário da norma. Além disso, o LLM analisará o conteúdo sob outros prismas, como aumento de gastos públicos ou supressão de direitos individuais. Os resultados processados serão enviados para uma aplicação Mobile para consulta pública.

## Funcionalidades Principais
- **Web Crawler:** Varredura periódica de sites do Governo em busca de novos PLs.
- **RAG System:** Armazenamento e recuperação eficiente do conteúdo das leis usando busca semântica.
- **LLM Processing:** 
  - Identificação de "Jabutis".
  - Análise de impacto (custos, direitos, etc.).
- **Integração Mobile:** Disponibilização dos dados analisados e notificações push sobre novos projetos polêmicos.

## Arquitetura e Stack Técnica (MVP)
| Componente | Tecnologia Recomendada |
| :--- | :--- |
| **Backend + API** | Python (FastAPI) no Railway.app |
| **Banco de Dados** | Supabase (PostgreSQL + pgvector para RAG) |
| **Autenticação** | Supabase Auth |
| **LLM (IA)** | Groq (Llama 3.1 70B / Mixtral 8x22B) |
| **Crawler** | GitHub Actions + Playwright (Python) |
| **App Mobile** | Flutter |
| **Notificações** | Firebase Cloud Messaging (FCM) |
| **Monitoramento** | Sentry + Logtail |
| **Domínio/SSL** | Cloudflare |

## Detalhamento de Telas (Protótipo)

### Perfil: Operador / Administrador
1. **Dashboard:** Status dos Crawlers, volume de PLs e fila de análise crítica (IA).
2. **Fontes (Alvos):** Gestão de URLs (Câmara, Senado, etc.).
3. **Configuração de IA:** Gestão dos critérios de análise (ex: "Aumenta despesa?").
4. **Editor de Jabutis:** Visualização do texto original com destaques da IA para revisão manual antes da publicação.

### Perfil: Parlamentar (Com Voto)
1. **Login:** Acesso restrito com preview de notificações (3 linhas de PLs Novos/Alterados).
2. **Dashboard Parlamentar:** Lista "Em Pauta" com indicadores visual de Novo/Alterado e barra de busca.
3. **Detalhes do PL:**
    - Ficha técnica: Nro, Nome, Autor, Regime de Urgência, Texto Original (Sim/Não).
    - Orientações: Partido, Bancada (definidas pelo líder) e "Sentimento da Casa" (Gradiente de cor).
4. **Votação Interativa:** Botões Aprovo/Abstenho/Reprovo que reagem visualmente e atualizam a orientação do partido (se for líder).
5. **Ações:** Links para "Ver Detalhes" (Análise IA) e "Ver Resumo".

### Perfil: Público Geral (Pendente Detalhamento)
- Foco em alertas, linguagem simples e impacto social.

## Backlog
### Pesquisa e Planejamento
- [x] Definir stack tecnológica inicial.
- [ ] Listar URLs dos sites da Câmara, Senado e Diário Oficial.
- [ ] Mapear estrutura de dados (Schema) para os Projetos de Lei.

### Desenvolvimento do Backend/Crawler
- [ ] Criar estrutura base do Backend (FastAPI + Supabase SDK).
- [ ] Implementar Crawler inicial para uma fonte (ex: Câmara dos Deputados).
- [ ] Configurar tabela de vetores no Supabase (pgvector).
- [ ] Criar e testar Prompts para detecção de "Jabutis" no Groq.
- [ ] Implementar pipeline de processamento: Crawler -> RAG -> LLM -> DB.

### Entrega e Mobile
- [x] Criar protótipo de UI (Simulado em HTML/Tailwind interativo).
- [ ] Implementar perfil de Parlamentar (Sigla Partido, Flag Líder de Bancada).
- [ ] Lógica de Orientação: Voto do Líder define orientação para o partido.
- [ ] Integrar App com a API do Backend.
- [ ] Configurar GitHub Actions para execução diária do Crawler.
- [ ] Implementar sistema de alertas via FCM.
