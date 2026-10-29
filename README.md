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

📊 Links de Apresentação e Painéis

Preencha os links abaixo conforme finalizar os entregáveis visuais.

🔗 Dashboard (Power BI / Visualização): [INSERIR_LINK_DO_DASHBOARD_AQUI]

🔗 Apresentação Executiva (Slides): [INSERIR_LINK_DA_APRESENTACAO_AQUI]

🚀 Como Executar o Pipeline

O pipeline está totalmente orquestrado e parametrizado para execução idempotente. O arquivo de configuração do job encontra-se na raiz do repositório:

job_execução.yaml

Para reexecutar manualmente, siga a ordem sequencial dos notebooks de 00_Config até 04_Gold_Layer.
