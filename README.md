# Tealium Solution Design - TudoAzul

## Introdução plataforma Tealium
A Tealium desempenha o papel de um Data Hub, possibilitando a coleta, centralização e padronização dos dados.

Para que a plataforma execute sua função, é necessário mapear e enviar os dados desejados para a mesma.
Neta documentação será descrito quais informações devem ser capturadas e qual momento enviar para a ferramenta.

## Implantação Código Base
A seguir encontram-se os códigos base utilizados pela plataforma Tealium iQ. 
Os mesmos devem ser implementados no código fonte da página, um no topo da tag ```<head>``` e outro logo na abertura
da tag ```<body>```. 
No caso do snippet destinado ao ```<body>```, se possível o objeto Javascript (que será descrito a seguir) deve ser definido e preenchido antes da chamada do código.

##### `<head>`
  ```javascript
  <script src="//tags.tiqcdn.com/utag/azul/tudoazul/prod/utag.sync.js"></script>
  ```
##### `<body>`
```javascript
<script type="text/javascript">
    (function(a,b,c,d){
    a='//tags.tiqcdn.com/utag/azul/tudoazul/prod/utag.js';
    b=document;c='script';d=b.createElement(c);d.src=a;d.type='text/java'+c;d.async=true;
    a=b.getElementsByTagName(c)[0];a.parentNode.insertBefore(d,a);
    })();
</script>
```
Caso não seja possível definir e preencher o objeto Javascript antes do código destinado ao elemento `<body>` (ex: preenchimento
do objeto ocorre no DOM ready) ou o site utilize tecnologia AJAX (ou similar), a função a seguir deve ser chamada quando as informações
desejadas na página estiverem disponíveis.
Veja abaixo:
  ```javascript
  <script type="text/javascript"> 
    utag.view(utag_data); 
  </script> 
  ```
  > ATENÇÃO: A chamada desta função NÃO é obrigatória. 
Deve-se utiliza-la apenas nos casos citados acima

Para um **rastreamento de evento**, é necessário utilizar o seguinte comando:
```javascript
  <script type="text/javascript"> 
    utag.link({"someKey1":"someValue1","someKey2":"someValue2"})
  </script> 
```
> Observação: No exemplo acima, os valores "someKey" e "someValue" serão substituídos pelas variáveis da camada de dados 
e suas respectivas informações definidas a seguir neste documento.

## Camada de dados
#### Implantação objeto JavaScript
Para coletar informações do visitante que navega no site TudoAzul, um dos passos é o preenchimento dinâmico da Camada de Dados (Data Layer), que irá possibilitar a captura de informações via tag manager (Tealium).

A Camada de Dados (Data Layer) é composta pelo objeto Javascript (descrito a seguir) e por triggers personalizadas. A mesma foi desenhada e estruturada baseando-se nas informações que são relevantes para compor os relatórios de Web Analytics desejados.

A seguir está a descrição de cada um dos atributos do objeto e quando devem ser instanciados e preenchidos nas páginas. 

#### Estrutura do objeto JavaScript
O objeto Javascript ,citado anteriormente, recebe o nome **utag_data** e sua estrutura pode ser encontrada aqui. 
Além disso, o objeto segue o modelo de um JSON Flatten Object e são aceitos **apenas valores do tipo String**. A estrutura proposta deve ser rigorosamente seguida e o preenchimento de diferentes atributos que estão diretamente ligados, deve ser realizado de forma coerente, em relação as posições que serão adicionadas nos Arrays. Veja abaixo:
> Quando o tipo do atributo for "Array de String", na verdade o valor esperado é uma String separada por virgulas, onde cada elemento representa uma posição. Exemplo: "VCP_SDU, SDU_VCP"

#### Variáveis da camada de dados
| Variável                  | Descrição                                                       | Exemplo                                                | Tipo   |
|---------------------------|-----------------------------------------------------------------|--------------------------------------------------------|--------|
| customer_childrenQuantity | Quantidade de filhos de um usuário                              | "2", "1", "0"                                          | String |
| customer_companyName      | Nome da empresa informada pelo usuário                          | "Azul Viagens", "Bradesco", ...                        | String |
| customer_companyRole      | Cargo informado pelo usuário                                    | "Analista", "Diretor", ...                             | String |
| customer_cpf              | Cpf do visitante                                                | "22233366638"                                          | String |
| customer_dateBirth        | Data de nascimento do usuário                                   | "01-05-1998", "12-08-1992"                             | String |
| customer_freq_tripYear    | Quantidade de viagens a lazer por ano, selecionado pelo usuário | "0", "1", "2", ...                                     | String |
| customer_gender           | Gênero do usuário                                               | "m", "f"                                               | String |
| customer_language         | Idioma escolhido do usuáio                                      | "pt", "en", ...                                        | String |
| customer_marital status   | Estado civil do usuário                                         | "Solteiro(a)", "Casado(a)", ...                        | String |
| customer_phone            | Telefone do usuário                                             | 11941434675                                            | String |
| customer_prefCinema       | Preferências escolhidas em: Cinema                              | "Ação", "Aventura-Romance", ...                        | String |
| customer_prefDestination  | Aeroporto de destino preferenial escolhido pelo usuário         | "VCP", "SDU", ...                                      | String |
| customer_prefGastronomy   | Preferências escolhidas em: Gastronomia                         | "Restaurantes-Vinhos", "Outros", ...                   | String |
| customer_prefInternet     | Preferências escolhidas em: Atividades culturais                | "Museu", "Artes_plásticas", ...                        | String |
| customer_prefMusic        | Preferências escolhidas em: Música                              | "Rock", "MPB-Jazz-Sertanejo-Clássica", ...             | String |
| customer_prefNightLife    | Preferências escolhidas em: Vida noturna                        | "Bares-Shows", "Restaurantes", ...                     | String |
| customer_prefOrigin       | Aeroporto de origem preferencial escolhido pelo usuário         | "VCP", "SDU", ...                                      | String |
| customer_prefPets         | Preferências escolhidas em: Animais de estimação                | "Cães-Gatos", "Peixes", ...                            | String |
| customer_prefReading      | Preferências escolhidas em: Leitura                             | "Quadrinhos", "Jornais-Revistas", ...                  | String |
| customer_prefSport        | Preferências escolhidas em: Esporte                             | "Academia_ao_ar_livre-Boxe", "Golfe", ...              | String |
| customer_prefTheater      | Preferências escolhidas em: Teatro                              | "Comédia", "Drama-Suspense", ...                       | String |
| event_name                | Nome do evento                                                  | "salvou-alteracoes"                                    | String |
| pageName                  | Nome da página                                                  | "homepage", "comprar passagens"                        | String |
| section                   | Sessão do site que o visitante está acessando                   | "institucional", fluxo de compra"                      | String |
| siteLanguage              | Linguagem do site                                               | "pt", "en"                                             | String |
| user_email                | E-mail cadastrado no programa TudoAzul                          | "fernanda.gomes@gmail.com", "carlos.silva@htomail.com" | String |
| user_name                 | Nome do usuário                                                 | "Fernanda", "Carlos"                                   | String |
| user_pointsBalance        | Saldo de pontos do programa TudoAzul                            | "600000", "77383"                                      | String |
| user_tudoAzulNumber       | Número tudoAzul do usuário                                      | "46201893124", "7990056511"                            | String |
| user_userClassification   | Classificação no programa TudoAzul                              | "TudoAzul", "Safira"...                                | String |
| visitorLoginStatus        | Status do visitante do site                                     | "true","false"                                         | String |

#### Grupos de preenchimento
Nesta parte, será descrito os grupos para as variáveis acima, com suas respectivas condições de preenchimento
##### Grupo 1
_Condição para preenchimento:_ Todas as páginas

| Variável           	|
|--------------------	|
| pageName           	|
| section            	|
| siteLanguage       	|
| visitorLoginStatus 	|

##### Grupo 2
_Condição para preenchimento:_ Quando o usuário realizar o login com sucesso. Caso o usuário ainda não possuir tais informações, não disparar a varíavel

| Variável                  	|
|---------------------------	|
| customer_childrenQuantity 	|
| customer_cpf              	|
| customer_dateBirth        	|
| customer_gender           	|
| customer_language         	|
| customer_marital status   	|
| user_email                	|
| user_name                 	|
| user_pointsBalance        	|
| user_tudoAzulNumber       	|
| user_userClassification   	|

##### Grupo 3
_Condição para preenchimento:_ "Após o usuário alterar suas informações e salva-las com sucesso. OBS: Deve ocorrer uma chamada do tipo "Rastreamento de eventos/ações" quando o usuário salvar suas informações"

| Variável                  	|
|---------------------------	|
| customer_childrenQuantity 	|
| customer_companyName      	|
| customer_companyRole      	|
| customer_dateBirth        	|
| customer_freq_tripYear    	|
| customer_gender           	|
| customer_language         	|
| customer_marital status   	|
| customer_phone            	|
| customer_prefDestination  	|
| customer_prefOrigin       	|
| event_name                  | 
> O valor do event_name deverá ser "salvou-alteracoes"

##### Grupo 4
_Condição para preenchimento:_ "Quando o usuário alterar sua senha com sucesso.
OBS: Deve ocorrer uma chamada do tipo "Rastreamento de eventos/ações".

| Variável            |
|---------------------|
| event_name          |
| user_email          |
| user_tudoAzulNumber |
| customer_cpf        |
> O valor do event_name deverá ser "alterou-senha"
