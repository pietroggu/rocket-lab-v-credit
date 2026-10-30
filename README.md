V-Credit | Transformação Digital no Atendimento e Governança de Dados

Repositório oficial da solução desenvolvida para o case da V-Credit (Visagio | Rocket Lab 2026). Este projeto aborda a reestruturação da operação de atendimento e da infraestrutura analítica, unindo engenharia de dados robusta (Arquitetura Medalhão no Databricks) e inteligência de negócio orientada a evidências.

🏗️ Arquitetura do Projeto (Arquitetura Medalhão)

O pipeline foi estruturado de forma modular e idempotente no Databricks, garantindo rastreabilidade, qualidade de dados e reprodutibilidade:

00_Config: Centralização de variáveis globais e caminhos da Landing Zone.

01_Setup: Inicialização do catálogo v_credit, schemas (bronze, silver, gold) e validação de dependências.

02_Bronze_Layer: Ingestão bruta dos arquivos operacionais da V-Credit (com suporte a codificação windows-1252 para bases legadas) e injeção de metadados de auditoria.

03_Silver_Layer: Limpeza, normalização textual, tratamento de horários, cálculo de durações e aplicação de regras de validação (com auditoria de qualidade gravada em dq_log). Inclui a detecção da anomalia estrutural de autosserviço.

04_Gold_Layer: Modelagem dimensional (Star Schema), consolidação de custos e pesquisas de satisfação no grão transacional, e geração do agregado executivo mensal.

05_Export_Gold_To_CSV: Rotina de exportação das tabelas da camada Gold para formato CSV, viabilizando a construção do painel analítico.

## Dashboard Power BI

O dashboard apresenta indicadores dos chamados da V-Credit entre janeiro de 2025 e julho de 2026, organizados em quatro páginas:

- **Visão executiva:** panorama dos principais indicadores;
- **Resolução:** análise dos resultados por canal e motivo;
- **Custos, eficiência e satisfação:** acompanhamento dos custos e dos indicadores operacionais e de satisfação;
- **Perfis:** recortes agregados de clientes e atendentes por região, faixa etária e nível de atendimento.

### Estrutura e execução

O arquivo `V_Credit.pbix`, na raiz do repositório, contém o relatório do Power BI. A pasta `dados_bi/` reúne os CSVs usados como fontes do modelo: `agg_visao_executiva_mensal.csv`, `dim_atendentes.csv`, `dim_canais.csv`, `dim_clientes.csv`, `dim_data.csv`, `dim_motivos.csv` e `fato_chamados.csv`.

Para visualizar o dashboard, mantenha o PBIX e a pasta `dados_bi/` na estrutura do projeto, abra `V_Credit.pbix` no Power BI Desktop e, se solicitado, confirme ou ajuste a localização das fontes CSV para os arquivos correspondentes dentro de `dados_bi/`. Em seguida, navegue pelas quatro páginas do relatório.

Os chamados são contados por `id_chamado`. As taxas de resolução consideram chamados com status informado; o CSAT considera respostas válidas com nota 4 ou 5; e os tempos médios usam intervalos válidos. As comparações entre perfis são descritivas e não demonstram causalidade.

Link de Apresentação

🔗 Apresentação Executiva (Slides): [https://docs.google.com/presentation/d/1iI-lNpGAfoaOATxug7eFuo3vARMqj9G97A_Gx19cfPc/edit?slide=id.h21613369c00ac88e_7_0#slide=id.h21613369c00ac88e_7_0)](https://docs.google.com/presentation/d/1iI-lNpGAfoaOATxug7eFuo3vARMqj9G97A_Gx19cfPc/edit?usp=sharing)

🚀 Como Executar o Pipeline

O pipeline está totalmente orquestrado e parametrizado para execução idempotente. O arquivo de configuração do job encontra-se na raiz do repositório:

job_execução.yaml

Para reexecutar manualmente, siga a ordem sequencial dos notebooks de 00_Config até 04_Gold_Layer.

