

## Cognitive Search com AI Search

Neste laboratório, aprendemos a configurar todas as etapas necessárias para o deploy de uma solução de indexação e mineração de dados baseada em documentos, utilizando o serviço Azure AI Search.

Relatarei uma visão global da criação dos elementos que possibilitam a indexação e mineração, dando um resumo ao final dos dados de interesse extraídos e minhas considerações.

### Recursos necessários para utilização do AI Search

O AI Search service é um recurso que depende de uma estrutura de infraestrutura básica para operar. São os recursos:

- *Serviço AI Search*
- *Group Resources (Grupo de Recursos)*
- *Azure IA Services (Recurso)*
  - *Storage Account com 2 containers criados antecipadamente e um criado pelo próprio serviço posteriormente:*
    - Um do tipo Blob para os documentos que virarão o dataset; 	
    - Um para a base de conhecimento (dataset); 	
    - Um para os skills criados ao definir as opções do serviço.

### Criação do AI Search

Cheguei ao Azure AI Search a partir do link [https://portal.azure.com/#home](https://portal.azure.com/#home) e lá efetuei uma busca pela opção AI Search. Uma vez localizada, criei um novo serviço ***AI Search*** seguindo os passos guiados pelo vídeo da aula. Nomeei esse serviço de AIS-service.

### Criação do Resource Group

Utilizando a opção ***Resource Group > Create***, criei o grupo de recursos (Resource Group) que conterá o resource do Azure AI Services com o nome de AIS-res-group.

### Criação do Azure AI Services (resource)

Voltei para a tela inicial (home) e utilizando as opções ***Create Resource***, escolhi a opção ***AI + Machine Learning*** do menu lateral esquerdo. Assim, mais opções apareceram no centro da tela, nelas escolhi a opção ***Create*** do ***Azure AI services***. Preenchi conforme orientado no vídeo, nomeando o recurso como ***AIS-res***. Finalizei o processo e voltei à tela principal do portal.

### Criação do Storage Account

Uma vez na tela principal, escolhi a opção ***Storage Accounts*** e mais uma vez segui os passos ensinados no vídeo para completar essa etapa. Aqui deve-se ter muita atenção para os detalhes, como a habilitação do acesso anônimo nas configurações do storage, na criação do tipo de container como Blob e no seu acesso como anônimo. O storage eu nomeei como ***aisstorage*** e o container blob como ***aisreviews***.

Após a conclusão, utilizei a opção ***Upload*** do container ***aisreviews*** para subir os arquivos docx para processamento e geração do dataset. Uma vez terminado o upload, prossegui para as demais configurações no ***AI Search***. 

### Importando dados e configurando o AI Search

Acessei o serviço ***AIS-service*** e nele cliquei na opção ***Import Data***, definindo o tipo ***Azure Blob Storage*** conforme o nosso storage account ***aisstorage*** e o container de dados ***aisreviews***.

A seguir, configurei a opção ***Add Cognitive Skills*** informando o nosso Azure AI Resource ***AIS-res***. Aqui descobri algo interessante: o resource deve estar na mesma região (*region*) do AI Search, caso contrário, ele não aparecerá na lista de resources disponíveis para uso. Acredito que os demais também seguem esse princípio, como meu tempo está muito corrido deixarei para testar os outros recursos depois.

Continuei as configurações e, seguindo as orientações, preenchi a etapa ***Add Enrichments***. Nessa etapa, criamos o segundo container para a base de conhecimento, nomeei esse novo container como ***aisknowledgment-store*** e selecionando-o na conclusão de sua criação.

E lá fui eu para a última etapa de configurações: ***Customize target index***, segui as orientações e ao término encerrei o processo clicando em ***Submit***.

### Search Explorer

Com todo ambiente criado, chegou a hora de testar os recursos do ***IA Search***. Para isso, utilizei queries básicas para gerar alguns dados bem interessantes. Procurei, mas não encontrei uma documentação que me desse mais recursos de seleção para incrementar as queries, mas fiz algo bem básico mesmo apenas para conhecer o poder do serviço. Acredito que uma vez feito o deploy e criado um endpoint, consiga extrair muita informação dele.

## Análise dos documentos de opiniões (reviews)

Nessas queries básicas, peguei alguns dados apenas para ter um resumo dos resultados retornados em json. Achei o retorno dos dados bem rápido e com muita informação pertinente. Além disso, tem a facilidade de analisar vários modelos ao mesmo tempo como palavras-chave, sentimentos e etc.

| Quantidade de Arquivos Analisados | Quantidade de Reviews |
|-----------------------------------|-----------------------|
| 9                                 | 9                     |

| Localidade   | Sentimentos                    | Qtde de Reviews |
|--------------|--------------------------------|-----------------|
| Chicago      | positivo: 2 - negativo: 1      | 3               |
| Seattle      | positivo: 3 - misto: 1         | 4               |
| Los Angeles  | positivo: 2                    | 2               |

### Considerações finais

Estou bem animado com os serviços de IA do Azure, creio que para as grandes empresas já podem contar com esses recursos para melhorar vários processos internos, conhecer mais sobre a visão que seus clientes têm de seus produtos e serviços e por aí vai, as possibilidades são muitas!

Como desenvolvedor, a conta free cai como uma luva, lembrando sempre de criar os serviços, testar e deletar tudo! Sempre!