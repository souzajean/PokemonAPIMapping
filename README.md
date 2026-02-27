# PokemonAPI
SAP BTP CPI - PokemonAPI Mapping

![Capa](imagens/capa-linkedin.png)

📌 Descrição do iFlow – Integração com API Pokémon

Este iFlow tem como objetivo consumir dados da API pública do Pokémon, transformar e validar as informações retornadas, direcionando o processamento conforme o Pokémon selecionado.

🔄 Fluxo de Processamento

Consumo da API Pokémon
O iFlow realiza uma chamada HTTP à API pública do Pokémon para obter os dados do Pokémon com base no ID informado.

Conversão de Formato (JSON → XML)
A resposta da API, originalmente em formato JSON, é convertida para XML, permitindo melhor manipulação dos dados dentro do SAP CPI.

Mapeamento dos dados do Pokémon
Após a conversão, o iFlow extrai informações relevantes (como ID ou nome do Pokémon) e as armazena em propriedades da mensagem para uso posterior no fluxo.

Roteamento por Condição (Router)
O iFlow avalia se o Pokémon retornado corresponde ao Pokémon previamente definido como Pokémon escolhido:

✅ Se for o Pokémon selecionado: o fluxo segue pelo caminho principal de sucesso.

❌ Caso contrário: o processamento é direcionado para o fluxo padrão (default).

Tratamento conforme o Resultado
Cada rota pode executar ações específicas, como retorno da mensagem, log, transformação adicional ou tratamento alternativo.

🎯 Objetivo do iFlow

Garantir que apenas o Pokémon previamente definido seja processado pelo fluxo principal, permitindo validação, controle e direcionamento lógico das mensagens recebidas da API.


📊 Exemplo Prático do Fluxo

### Criando nosso Iflow
![Fluxo](imagens/Screenshot_1.png)
```
PokemonAPI
```

### Adicionando o Artefato do Integration Flow
![Fluxo](imagens/Screenshot_2.png)


### Adicionando o nome do Integration Flow
![Fluxo](imagens/Screenshot_3.png)
```
Integracao_com_API_Pokemon
```

### Editando nosso Iflow
![Fluxo](imagens/Screenshot_4.png)


### Adicionar o HTTPS para o Sender para o Start
![Fluxo](imagens/Screenshot_5.png)


### Adicionando o Endereço para o HTTPS
![Fluxo](imagens/Screenshot_6.png)
```
Address = /Pokemon
```


### Adicionando o Content Modifier
![Fluxo](imagens/Screenshot_7.png)


### Renomeando o Content Modifier
![Fluxo](imagens/Screenshot_8.png)
```
set_Id_Pokemon
```


### Adicionando no Exchange Property
![Fluxo](imagens/Screenshot_9.png)
```
Exchange Property - create - _Id - Constant - 6
```


### Adicionando o External Call
![Fluxo](imagens/Screenshot_10.png)


### Adicionando o Request Replay
![Fluxo](imagens/Screenshot_11.png)


### Renomeando o Request Replay
![Fluxo](imagens/Screenshot_12.png)
```
PokeAPI
```


### Renomeando o Receiver
![Fluxo](imagens/Screenshot_13.png)
```
APIPokemon
```


### Adicionando o HTTP
![Fluxo](imagens/Screenshot_14.png)


### Configurando o HTTP
![Fluxo](imagens/Screenshot_15.png)
```
https://pokeapi.co/api/v2/pokemon-form/${property._Id}
```


### Transformar e Converter JSON to XML
![Fluxo](imagens/Screenshot_16.png)


### Renomear Converter JSON to XML
![Fluxo](imagens/Screenshot_17.png)
```
JSON to XML
```


### Configurar o Converter JSON to XML
![Fluxo](imagens/Screenshot_18.png)
```
Use Namespace Mapping: Desmarcar
Add XML Root Element: Marcar
Name: ResultsPokemon
```


### Adicionar o Content Modifier
![Fluxo](imagens/Screenshot_19.png)


### Renomeando Content Modifier
![Fluxo](imagens/Screenshot_20.png)
```
getNamePokemon
```


### Configurando o Content Modifier
![Fluxo](imagens/Screenshot_21.png)
```
Exchange Property - Create - _namepokemon - XPath - //ResultsPokemon - java.lang.String
```


### Adicionando o Router
![Fluxo](imagens/Screenshot_22.png)


### Renomeando o Router
![Fluxo](imagens/Screenshot_23.png)
```
Router
```


### Renomeando a conexão do Router
![Fluxo](imagens/Screenshot_24.png)
```
RoutePokemon
```


### Adicionando o End Message
![Fluxo](imagens/Screenshot_25.png)


### Conectando o Router com End
![Fluxo](imagens/Screenshot_26.png)
```
Router
```


### Renomeando a conexão do Router
![Fluxo](imagens/Screenshot_27.png)
```
Router Default
```


### Marcando com Default
![Fluxo](imagens/Screenshot_28.png)


### Adicionar o Content Modifier
![Fluxo](imagens/Screenshot_29.png)


### Renomeando Content Modifier
![Fluxo](imagens/Screenshot_30.png)
```
SetContentType
```


### Configurando o Content Modifier
![Fluxo](imagens/Screenshot_31.png)
```
Message Header - create - Content-Type - application/xml
```


### Adicionar o Content Modifier
![Fluxo](imagens/Screenshot_32.png)


### Renomeando Content Modifier
![Fluxo](imagens/Screenshot_33.png)
```
setBody
```

### Configurando o Content Modifier
![Fluxo](imagens/Screenshot_34.png)
```
Type: Constant
Body: Escolheu o Pokemon errado
```


### Save e Deploy
![Fluxo](imagens/Screenshot_35.png)

### Configuração no Postman
Adicionar a URL do Endpoint
![Fluxo](imagens/Screenshot_36.png)


## 📦 Exemplo prático – iFlow para baixar

📦 [Download do iFlow – Integração com API Pokémon](https://github.com/souzajean/PokemonAPI/raw/main/Package/Integracao_com_API_Pokemon.zip)

> O arquivo pode ser importado diretamente no SAP Integration Suite (CPI).

