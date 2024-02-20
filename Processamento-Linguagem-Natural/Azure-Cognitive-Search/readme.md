<h3> Explore um índice do Azure AI Search (UI) </h3>

Vamos imaginar que você trabalha para a Fourth Coffee, uma rede nacional de cafés. Você foi solicitado a ajudar a criar uma solução de mineração de conhecimento que facilite a busca de insights sobre as experiências dos clientes. Você decide criar um índice do Azure AI Search usando dados extraídos de avaliações de clientes.

<h4> >Neste laboratório você irá: </h4>

Criar recursos do Azure
Extrair dados de uma fonte de dados
Enriqueça os dados com habilidades de IA
Utilize o indexador do Azure no portal do Azure
Consulte seu índice de pesquisa
Revise os resultados salvos em uma Loja de conhecimento



<h4> Recursos do Azure necessários </h4>

A solução que você criará para o Fourth Coffee requer os seguintes recursos na sua assinatura do Azure:

Um recurso do Azure AI Search , que gerenciará a indexação e a consulta.
Um recurso de serviços de IA do Azure , que fornece serviços de IA para habilidades que sua solução de pesquisa pode usar para enriquecer os dados na fonte de dados com insights gerados por IA.

Nota Os recursos do Azure AI Search e dos serviços Azure AI devem estar no mesmo local!

Uma conta de armazenamento com contêineres de blobs, que armazenará documentos brutos e outras coleções de tabelas, objetos ou arquivos.



<h4> Crie um recurso do Azure AI Search </h4>
Entre no portal do Azure .

Clique no botão + Criar um recurso , pesquise Azure AI Search e crie um recurso Azure AI Search com as seguintes configurações:

Assinatura : sua assinatura do Azure .
Grupo de recursos : Selecione ou crie um grupo de recursos com um nome exclusivo .
Nome do serviço : um nome exclusivo .
Localização : Escolha qualquer região disponível .
Nível de preços : Básico
Selecione Review + create e depois de ver a resposta Validation Success , selecione Create .

Após a conclusão da implantação, selecione Ir para o recurso . Na página de visão geral do Azure AI Search, você pode adicionar índices, importar dados e pesquisar índices criados.

![alt text](image.png)

![alt text](image-1.png)

![alt text](image-2.png)

![alt text](image-3.png)

![alt text](image-4.png)

![alt text](image-5.png)

![alt text](image-6.png)

![alt text](image-7.png)

![alt text](image-8.png)

<h4> Crie um recurso de serviços de IA do Azure</h4>

Você precisará provisionar um recurso de serviços de IA do Azure que esteja no mesmo local que seu recurso do Azure AI Search. Sua solução de pesquisa usará esse recurso para enriquecer os dados no armazenamento de dados com insights gerados por IA.

Retorne à página inicial do portal do Azure. Clique no botão ＋Criar um recurso e pesquise os serviços de IA do Azure . Selecione criar um plano de serviços de IA do Azure . Você será levado a uma página para criar um recurso de serviços de IA do Azure. Configure-o com as seguintes configurações:

Assinatura : sua assinatura do Azure .
Grupo de recursos : O mesmo grupo de recursos que seu recurso do Azure AI Search .
Região : o mesmo local do recurso do Azure AI Search .
Nome : Um nome exclusivo .
Nível de preços : Padrão S0
Ao marcar esta caixa, confirmo que li e compreendi todos os termos abaixo : Selecionado
Selecione Revisar + criar . Depois de ver a resposta Validation Passed , selecione Create .

Aguarde a conclusão da implantação e visualize os detalhes da implantação.

![alt text](image-9.png)

![alt text](image-10.png)

![alt text](image-11.png)

![alt text](image-12.png)

![alt text](image-13.png)

![alt text](image-14.png)

![alt text](image-15.png)

![alt text](image-16.png)


<h4> Crie uma conta de armazenamento </h4>

Retorne à página inicial do portal do Azure e selecione o botão + Criar um recurso .

Procure conta de armazenamento e crie um recurso de conta de armazenamento com as seguintes configurações:
Assinatura : sua assinatura do Azure .
Grupo de recursos : O mesmo grupo de recursos que os recursos do Azure AI Search e dos serviços Azure AI .
Nome da conta de armazenamento : um nome exclusivo .
Localização : Escolha qualquer localização disponível .
Padrão de desempenho
Redundância : armazenamento localmente redundante (LRS)
Clique em Revisar e em Criar . Aguarde a conclusão da implantação e vá para o recurso implantado.

Na conta de Armazenamento do Azure que você criou, no painel de menu esquerdo, selecione Configuração (em Configurações ).
Altere a configuração de Permitir acesso anônimo de Blob para Habilitado e selecione Salvar .

Selecione + Contêiner . Um painel do seu lado direito é aberto.

Insira as seguintes configurações e clique em Criar :
Nome : Coffee-Reviews
Nível de acesso público : Container (acesso de leitura anônimo para containers e blobs)
Avançado : sem alterações .
Em uma nova guia do navegador, baixe as avaliações de café compactadas em https://aka.ms/mslearn-coffee-reviewse extraia os arquivos para a pasta de avaliações .

No portal do Azure, selecione o contêiner de avaliações de café . No contêiner, selecione Carregar .

![alt text](image-17.png)

![alt text](image-18.png)

![alt text](image-19.png)

![alt text](image-20.png)

![alt text](image-21.png)

![alt text](image-22.png)

![alt text](image-23.png)

![alt text](image-24.png)

![alt text](image-25.png)

![alt text](image-26.png)

![alt text](image-27.png)

![alt text](image-28.png)

![alt text](image-29.png)

![alt text](image-31.png)

![alt text](image-30.png)

![alt text](image-32.png)

![alt text](image-33.png)

![alt text](image-34.png)

No painel Carregar blob , selecione Selecionar um arquivo .

Na janela do Explorer, selecione todos os arquivos na pasta de avaliações , selecione Abrir e, em seguida, selecione Carregar .

Depois que o upload for concluído, você poderá fechar o painel Upload blob . Seus documentos estão agora em seu contêiner de armazenamento de avaliações de café .

![alt text](image-35.png)


<h4> Indexar os documentos </h4>

Depois de armazenar os documentos, você poderá usar o Azure AI Search para extrair insights dos documentos. O portal do Azure fornece um assistente de importação de dados . Com este assistente, você pode criar automaticamente um índice e um indexador para fontes de dados suportadas. Você usará o assistente para criar um índice e importar seus documentos de pesquisa do armazenamento para o índice do Azure AI Search.

No portal do Azure, navegue até o recurso Azure AI Search. Na página Visão geral , selecione Importar dados .

Na página Conectar-se aos seus dados , na lista Fonte de Dados , selecione Azure Blob Storage . Preencha os detalhes do armazenamento de dados com os seguintes valores:
Fonte de dados : Armazenamento de Blobs do Azure
Nome da fonte de dados : coffee-customer-data
Dados a extrair : Conteúdo e metadados
Modo de análise : Padrão
Cadeia de conexão : *Selecione Escolha uma conexão existente . Selecione sua conta de armazenamento, selecione o contêiner de avaliações de café e clique em Selecionar .
Autenticação de identidade gerenciada : Nenhuma
Nome do contêiner : esta configuração é preenchida automaticamente depois que você escolhe uma conexão existente .
Pasta Blob : deixe em branco .
Descrição : Avaliações sobre Fourth Coffee Shops.
Selecione Próximo: Adicionar habilidades cognitivas (opcional) .

Na secção Anexar Serviços Cognitivos , selecione o seu recurso de serviços Azure AI.

Na seção Adicionar enriquecimentos :
Altere o nome da qualificação para coffee-skillset .
Marque a caixa de seleção Habilitar OCR e mesclar todo o texto no campo merged_content .
Nota É importante selecionar Habilitar OCR para ver todas as opções de campo enriquecido.

Certifique-se de que o campo Dados de origem esteja configurado como merged_content .
Altere o nível de granularidade de enriquecimento para Páginas (blocos de 5.000 caracteres) .
Não selecione Habilitar enriquecimento incremental
Selecione os seguintes campos enriquecidos:

![alt text](image-36.png)

Em Salvar enriquecimentos em um armazenamento de conhecimento , selecione:
Projeções de imagem
Documentos
Páginas
Frases chave
Entidades
Detalhes da imagem
Referências de imagem

elecione projeções de blob do Azure: Documento . Uma configuração para o nome do contêiner com as exibições preenchidas automaticamente do contêiner de armazenamento de conhecimento . Não altere o nome do contêiner.

Selecione Próximo: Personalizar índice de destino . Altere o nome do índice para coffee-index .

Certifique-se de que a chave esteja configurada como metadata_storage_path . Deixe o nome do sugeridor em branco e o modo de pesquisa preenchido automaticamente.

Revise as configurações padrão dos campos de índice. Selecione filtrável para todos os campos que já estão selecionados por padrão.

Selecione Próximo: Criar um indexador .

Altere o nome do indexador para coffee-indexer .

Deixe a programação definida como Once .

Expanda as opções avançadas . Certifique-se de que a opção Base-64 Encode Keys esteja selecionada, pois as chaves de codificação podem tornar o índice mais eficiente.

Selecione Enviar para criar a fonte de dados, o conjunto de habilidades, o índice e o indexador. O indexador é executado automaticamente e executa o pipeline de indexação, que:
Extrai os campos de metadados do documento e o conteúdo da fonte de dados.
Executa o conjunto de habilidades cognitivas para gerar campos mais enriquecidos.
Mapeia os campos extraídos para o índice.
Volte à página de recursos do Azure AI Search. No painel esquerdo, em Gerenciamento de pesquisa , selecione Indexadores . Selecione o indexador de café recém-criado . Espere um minuto e selecione ↻ Atualize até que o Status indique sucesso.

Selecione o nome do indexador para ver mais detalhes.

![alt text](image-37.png)

![alt text](image-38.png)

![alt text](image-39.png)

![alt text](image-40.png)

![alt text](image-41.png)

![alt text](image-42.png)

![alt text](image-43.png)

![alt text](image-44.png)

![alt text](image-45.png)

![alt text](image-46.png)

![alt text](image-47.png)

![alt text](image-48.png)

![alt text](image-49.png)

![alt text](image-50.png)

![alt text](image-51.png)

![alt text](image-52.png)

![alt text](image-53.png)

![alt text](image-54.png)

![alt text](image-55.png)

![alt text](image-56.png)

![alt text](image-57.png)


<h4> Consultar o índice </h4>

Use o Search Explorer para escrever e testar consultas. O explorador de pesquisa é uma ferramenta incorporada no portal do Azure que oferece uma maneira fácil de validar a qualidade do seu índice de pesquisa. Você pode usar o Search Explorer para escrever consultas e revisar resultados em JSON.

Na página Visão geral do serviço de pesquisa , selecione Explorador de pesquisa na parte superior da tela.

Observe como o índice selecionado é o índice de café que você criou. Abaixo do índice selecionado, altere a visualização para JSON view .

No campo do editor de consultas JSON , copie e cole:

{
    "search": "*",
    "count": true
}


Selecione Pesquisar . A consulta de pesquisa retorna todos os documentos no índice de pesquisa, incluindo uma contagem de todos os documentos no campo @odata.count . O índice de pesquisa deve retornar um documento JSON contendo os resultados da pesquisa.

Agora vamos filtrar por localização. No campo do editor de consultas JSON , copie e cole:

{
 "search": "locations:'Chicago'",
 "count": true
}

Selecione Pesquisar . A consulta pesquisa todos os documentos no índice e filtra revisões com localização em Chicago. Você deveria ver 3no @odata.countcampo.

Agora vamos filtrar por sentimento. No campo do editor de consultas JSON , copie e cole


{
 "search": "sentiment:'negative'",
 "count": true
}

Selecione Pesquisar . A consulta pesquisa todos os documentos no índice e filtra revisões com sentimento negativo. Você deveria ver 1no @odata.countcampo.

Nota Veja como os resultados são classificados por @search.score. Esta é a pontuação atribuída pelo mecanismo de pesquisa para mostrar o quão próximos os resultados correspondem à consulta fornecida.

Um dos problemas que podemos querer resolver é por que pode haver certas avaliações. Vamos dar uma olhada nas frases-chave associadas à avaliação negativa. O que você acha que pode ser a causa da revisão?

![alt text](image-58.png)

![alt text](image-60.png)

![alt text](image-61.png)

![alt text](image-62.png)

![alt text](image-63.png)

![alt text](image-64.png)

![alt text](image-65.png)

![alt text](image-66.png)

![alt text](image-67.png)


<h4> Revise o armazenamento de conhecimento </h4>

Vamos ver o poder do armazenamento de conhecimento em ação. Ao executar o assistente Importar dados , você também criou um armazenamento de conhecimento. Dentro do armazenamento de conhecimento, você encontrará os dados enriquecidos extraídos pelas habilidades de IA que persistem na forma de projeções e tabelas.

No portal do Azure, navegue de volta para a sua conta de armazenamento do Azure.

No painel do menu esquerdo, selecione Containers . Selecione o contêiner de armazenamento de conhecimento .

Selecione qualquer um dos itens e clique no arquivo objectprojection.json .

Selecione Editar para ver o JSON produzido para um dos documentos do seu armazenamento de dados do Azure.

Selecione a localização atual do blob de armazenamento no canto superior esquerdo da tela para retornar à conta de armazenamento Containers .

Em Containers , selecione o contêiner coffee-skillset-image-projection . Selecione qualquer um dos itens.

Selecione qualquer um dos arquivos .jpg . Selecione Editar para ver a imagem armazenada no documento. Observe como todas as imagens dos documentos são armazenadas desta forma.

Selecione a localização atual do blob de armazenamento no canto superior esquerdo da tela para retornar à conta de armazenamento Containers .

Selecione Navegador de armazenamento no painel esquerdo e selecione Tabelas . Há uma tabela para cada entidade no índice. Selecione a tabela coffeeSkillsetKeyPhrases .

Observe as frases-chave que o armazenamento de conhecimento conseguiu capturar do conteúdo das avaliações. Muitos dos campos são chaves, portanto você pode vincular as tabelas como um banco de dados relacional. O último campo mostra as frases-chave que foram extraídas pelo conjunto de habilidades.

![alt text](image-68.png)

![alt text](image-69.png)

![alt text](image-70.png)

![alt text](image-71.png)

![alt text](image-72.png)

![alt text](image-73.png)





https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/11-ai-search.html