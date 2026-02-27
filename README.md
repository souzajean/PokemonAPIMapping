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


### Adicionar o Message Mapping
![Fluxo](imagens/Screenshot_19.png)


### Renomeando o Message Mapping o Mapping
![Fluxo](imagens/Screenshot_20.png)
```
Message Mapping
```


### Adicionando o Mapping
![Fluxo](imagens/Screenshot_21.png)


### Adicionando o Source Mapping
![Fluxo](imagens/Screenshot_22.png)


### Selecionando o Message
![Fluxo](imagens/Screenshot_23.png)
```
<xs:schema attributeFormDefault="unqualified" elementFormDefault="qualified" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="ResultsPokemon">
    <xs:complexType>
      <xs:sequence>
        <xs:element type="xs:string" name="form_name"/>
        <xs:element type="xs:string" name="form_names"/>
        <xs:element type="xs:byte" name="form_order"/>
        <xs:element type="xs:byte" name="id"/>
        <xs:element type="xs:string" name="is_battle_only"/>
        <xs:element type="xs:string" name="is_default"/>
        <xs:element type="xs:string" name="is_mega"/>
        <xs:element type="xs:string" name="name"/>
        <xs:element type="xs:string" name="names"/>
        <xs:element type="xs:byte" name="order"/>
        <xs:element name="pokemon">
          <xs:complexType>
            <xs:sequence>
              <xs:element type="xs:string" name="name"/>
              <xs:element type="xs:string" name="url"/>
            </xs:sequence>
          </xs:complexType>
        </xs:element>
        <xs:element name="sprites">
          <xs:complexType>
            <xs:sequence>
              <xs:element type="xs:string" name="back_default"/>
              <xs:element type="xs:string" name="back_female"/>
              <xs:element type="xs:string" name="back_shiny"/>
              <xs:element type="xs:string" name="back_shiny_female"/>
              <xs:element type="xs:string" name="front_default"/>
              <xs:element type="xs:string" name="front_female"/>
              <xs:element type="xs:string" name="front_shiny"/>
              <xs:element type="xs:string" name="front_shiny_female"/>
              <xs:element name="versions">
                <xs:complexType>
                  <xs:sequence>
                    <xs:element name="generation-ix">
                      <xs:complexType>
                        <xs:sequence>
                          <xs:element name="scarlet-violet">
                            <xs:complexType>
                              <xs:sequence>
                                <xs:element type="xs:string" name="front_default"/>
                                <xs:element type="xs:string" name="front_female"/>
                              </xs:sequence>
                            </xs:complexType>
                          </xs:element>
                        </xs:sequence>
                      </xs:complexType>
                    </xs:element>
                    <xs:element name="generation-viii">
                      <xs:complexType>
                        <xs:sequence>
                          <xs:element name="brilliant-diamond-shining-pearl">
                            <xs:complexType>
                              <xs:sequence>
                                <xs:element type="xs:string" name="front_default"/>
                                <xs:element type="xs:string" name="front_female"/>
                              </xs:sequence>
                            </xs:complexType>
                          </xs:element>
                        </xs:sequence>
                      </xs:complexType>
                    </xs:element>
                  </xs:sequence>
                </xs:complexType>
              </xs:element>
            </xs:sequence>
          </xs:complexType>
        </xs:element>
        <xs:element name="types" maxOccurs="unbounded" minOccurs="0">
          <xs:complexType>
            <xs:sequence>
              <xs:element type="xs:byte" name="slot"/>
              <xs:element name="type">
                <xs:complexType>
                  <xs:sequence>
                    <xs:element type="xs:string" name="name"/>
                    <xs:element type="xs:string" name="url"/>
                  </xs:sequence>
                </xs:complexType>
              </xs:element>
            </xs:sequence>
          </xs:complexType>
        </xs:element>
        <xs:element name="version_group">
          <xs:complexType>
            <xs:sequence>
              <xs:element type="xs:string" name="name"/>
              <xs:element type="xs:string" name="url"/>
            </xs:sequence>
          </xs:complexType>
        </xs:element>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
</xs:schema>
```


### Selecionando o PokemonAPI.xsd
![Fluxo](imagens/Screenshot_24.png)
```
PokemonAPI.xsd
```
📦 [Download do PokemonAPI.xsd – Integração com API Pokémon](https://github.com/souzajean/PokemonAPIMapping/blob/main/ArquivosXSD/PokemonAPI.xsd)


### Adicionando o Mapping
![Fluxo](imagens/Screenshot_25.png)

### Selecionando o PokemonAPI.xsd
![Fluxo](imagens/Screenshot_26.png)


### Selecionando o PokemonAPI_Results.xsd
![Fluxo](imagens/Screenshot_27.png)
```
PokemonAPI_Results.xsd
```
📦 [Download do PokemonAPI_Results.xsd – Integração com API Pokémon](https://github.com/souzajean/PokemonAPIMapping/blob/main/ArquivosXSD/PokemonAPI_Results.xsd)


### Marcando o indices para mapear todos de uma vez
![Fluxo](imagens/Screenshot_28.png)


### Verificar se mapeou corretamente todos os campos
![Fluxo](imagens/Screenshot_29.png)



### Adicionando o Router
![Fluxo](imagens/Screenshot_30.png)


### Adicionar o End Message
![Fluxo](imagens/Screenshot_31.png)


### Renomeando Router
![Fluxo](imagens/Screenshot_32.png)
```
RouterPokemon
```


### Configurando o Content Modifier
![Fluxo](imagens/Screenshot_33.png)
```
Content Modifier - SetContentType
Message Header - create - Content-Type - application/xml
```


### Adicionar o Content Modifier
![Fluxo](imagens/Screenshot_34.png)


### Renomeando Content Modifier
![Fluxo](imagens/Screenshot_35.png)
```
SetContentType
```

### Configurando o Content Modifier
![Fluxo](imagens/Screenshot_36.png)
```
Type: Constant
Message Header - create - Content-Type - application/xml
```


### Roteando o caminho
![Fluxo](imagens/Screenshot_37.png)
```
Router
```

### Adicionando o Content Modifier
![Fluxo](imagens/Screenshot_38.png)
```
Router
```
### Renomeando o Content Modifier
![Fluxo](imagens/Screenshot_38.png)
```
setBody
```

### Adicionando a mensagem no corpo, caso a rota não seja selecionado corretamente
![Fluxo](imagens/Screenshot_40.png)
```
Type: Constant
Body: Escolheu o Pokemon errado
```

### Renomendo a rota para Default
![Fluxo](imagens/Screenshot_41.png)
```
Route Default
```

### Renomendo a rota para Default
![Fluxo](imagens/Screenshot_42.png)


### Configuração no Postman
Adicionar a URL do Endpoint
![Fluxo](imagens/Screenshot_43.png)


## 📦 Exemplo prático – iFlow para baixar

📦 [Download do iFlow – Integração com API Pokémon](https://github.com/souzajean/PokemonAPI/raw/main/Package/Integracao_com_API_Pokemon.zip)

> O arquivo pode ser importado diretamente no SAP Integration Suite (CPI).

