# Azure Cognitive Search: Utilizando AI Search para Indexação e Consulta de Dados

## Meu Primeiro Contato com Azure Cognitive Search

Quando comecei a explorar o Azure Cognitive Search (também conhecido como AI Search), fiquei impressionado com como essa ferramenta pode transformar a maneira como trabalhamos com dados. Vou compartilhar minha jornada de aprendizado para ajudar outros iniciantes.

## O Que é Azure Cognitive Search?

Azure Cognitive Search é um serviço de busca em nuvem que permite:

- Criar índices de pesquisa ricos
- Adicionar habilidades de IA para extrair insights
- Fornecer experiências de busca poderosas em aplicativos

## Configurando Meu Primeiro Serviço

1. Acessei o [portal.azure.com](https://portal.azure.com)
2. Criei um novo recurso "Azure Cognitive Search"
3. Escolhi um nome, região e tipo de preço (comecei com o gratuito para testes)

## Criando Meu Primeiro Índice

```csharp
// Exemplo de definição de índice em C#
var definition = new Index
{
    Name = "meu-primeiro-indice",
    Fields = FieldBuilder.BuildForType<Produto>(),
    Suggesters = new List<Suggester>
    {
        new Suggester("sg", "nome", "descricao")
    }
};

await searchService.Indexes.CreateAsync(definition);
```

## Indexando Dados Básicos

Usei um conjunto de dados simples em JSON:

```json
[
    {
        "id": "1",
        "nome": "Camiseta Azure",
        "descricao": "Camiseta oficial do Microsoft Azure",
        "preco": 59.99,
        "estoque": 100
    },
    {
        "id": "2",
        "nome": "Caneca DevOps",
        "descricao": "Caneca para desenvolvedores DevOps",
        "preco": 39.90,
        "estoque": 50
    }
]
```

## Realizando Minha Primeira Consulta

```csharp
var parameters = new SearchParameters
{
    Select = new[] { "nome", "preco" },
    Filter = "preco lt 50",
    OrderBy = new[] { "preco desc" }
};

var results = await searchClient.Documents.SearchAsync<Produto>("caneca", parameters);
```

## Lições Aprendidas

1. **Definição de Campos**: É crucial definir corretamente os campos (texto, número, etc.) para uma boa experiência de busca.

2. **Habilidades de IA**: Adicionei habilidades como reconhecimento de entidades para enriquecer meus dados.

3. **Testes Iterativos**: Fiz muitos testes ajustando os parâmetros para melhorar os resultados.

## Próximos Passos na Minha Jornada

- Explorar indexadores automáticos para fontes como Azure SQL e Blob Storage
- Testar o enriquecimento com IA para documentos complexos
- Implementar autocomplete e sugestões em uma aplicação real

## Conclusão

Azure Cognitive Search mostrou-se uma ferramenta poderosa mesmo para iniciantes como eu. Com um pouco de prática, consegui criar um sistema de busca funcional em poucas horas, mas a ferrameta tem muitas outras funções a explorar.

[Documentação Oficial](https://docs.microsoft.com/azure/search/)
