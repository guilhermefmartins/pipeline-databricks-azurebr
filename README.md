## ⚙️ Orquestração de Pipelines com Databricks e Azure Data Factory (Imóveis - Azure Data Lake)
Objetivo
Automatizar a execução de notebooks no Azure Databricks utilizando o Azure Data Factory, com foco em pipelines de dados de imóveis organizados nas camadas bronze e silver de um Data Lake na Azure, usando o formato de armazenamento Delta para garantir performance, escalabilidade e versionamento.

# 📌 Sumário
- [Contexto](#contexto)
- [Pipeline de Dados](#pipeline-de-dados)
- [Ferramentas Utilizadas](#ferramentas-utilizadas)
- [Orquestração](#orquestração)
- [Como Reproduzir](#como-reproduzir)
- [Resultados e Conclusões](#resultados-e-conclusões)

Contexto
O projeto teve como foco principal a construção de um pipeline de dados moderno e automatizado, com leitura, transformação e persistência em Delta Lake, utilizando ferramentas de ponta do ecossistema Azure. Os dados simulam o mercado imobiliário e passam por diferentes camadas de tratamento com persistência eficiente.

# 🏗 Pipeline de Dados 
Camadas estruturadas no Data Lake:

Bronze: Ingestão bruta dos dados originais.

Silver: Dados tratados, limpos e prontos para análise e consumo por dashboards ou modelos de machine learning.

Transformações aplicadas:

Leitura de arquivos originais em JSON

Padronização de nomes e tipos de colunas

Escrita dos dados tratados no formato Delta, garantindo versionamento, transações ACID e performance superior para leitura e atualização

# 🛠 Ferramentas Utilizadas
Azure Databricks: Ambiente baseado em Apache Spark com notebooks em PySpark e Scala, usado para ingestão, tratamento e gravação dos dados.

Delta Lake: Formato de armazenamento transacional utilizado para garantir consistência e eficiência nas camadas do Data Lake.

Azure Data Factory (ADF): Interface visual de orquestração para pipelines, controle de execução e integração com serviços da Azure.

Azure Data Lake Storage Gen2: Armazenamento escalável e seguro para os dados, com suporte a hierarquia de diretórios e permissões.

# 🔄 Orquestração
A orquestração foi feita com o Azure Data Factory, utilizando pipelines visuais com agendamentos e monitoramento. As execuções foram programadas com triggers baseadas em horário e configuradas para rodar notebooks específicos no Databricks. ADF gerenciou dependências, falhas e logs, garantindo rastreabilidade e controle no processo.

# 💻 Como Reproduzir
Provisionar os serviços:

Azure Databricks

Azure Data Factory

Azure Data Lake Storage Gen2
<br/>
# Montar o Data Lake no Databricks:
```
val configs = Map(
  "fs.azure.account.auth.type" -> "OAuth",
  "fs.azure.account.oauth.provider.type" -> "org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider",
  "fs.azure.account.oauth2.client.id" -> "<application-id>",
  "fs.azure.account.oauth2.client.secret" -> dbutils.secrets.get(scope="<scope-name>",key="<service-credential-key-name>"),
  "fs.azure.account.oauth2.client.endpoint" -> "https://login.microsoftonline.com/<directory-id>/oauth2/token")
// Optionally, you can add <directory-name> to the source URI of your mount point.
dbutils.fs.mount(
  source = "abfss://<container-name>@<storage-account-name>.dfs.core.windows.net/",
  mountPoint = "/mnt/<mount-name>",
  extraConfigs = configs)
```
<br/>
# 📈 Resultados e Conclusões
 <br/>
- ✅ Os dados foram processados com sucesso em um fluxo robusto e automatizado<br/>
- ✅ O uso do formato Delta permitiu maior controle, performance e confiabilidade nas camadas bronze e silver<br/>
- ✅ O Azure Data Factory ofereceu uma interface visual amigável para orquestração, facilitando o agendamento e rastreamento das execuções<br/>
- ✅ O projeto demonstrou a integração eficaz entre Databricks e os serviços do Azure, com organização modular e escalável<br/>
 <br/>

# 🔍 Este projeto comprova minha capacidade de desenvolver pipelines completos e escaláveis em nuvem, combinando engenharia de dados moderna, automação e boas práticas de orquestração com ferramentas do ecossistema Azure.
