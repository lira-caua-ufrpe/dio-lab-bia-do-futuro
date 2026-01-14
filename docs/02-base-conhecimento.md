# Base de Conhecimento

## Dados Utilizados

Descreva se usou os arquivos da pasta `data`, por exemplo:

| Arquivo                   | Formato | Utilização no Agente                                                                          |
| ------------------------- | ------- | --------------------------------------------------------------------------------------------- |
| `dataset_operacional.csv` | CSV     | Fonte principal de dados para análises exploratórias, segmentações e geração de insights      |
| `dicionario_dados.json`   | JSON    | Definir o significado semântico de cada coluna do dataset, evitando interpretações incorretas |
| `metricas_analise.json`   | JSON    | Orientar quais métricas e KPIs o agente pode calcular e sugerir                               |
| `regras_analista.json`    | JSON    | Definir limites de atuação do agente e prevenir alucinações                                   |
> [!TIP]
> **Quer um dataset mais robusto?** Você pode utilizar datasets públicos do [Hugging Face](https://huggingface.co/datasets) relacionados a finanças, desde que sejam adequados ao contexto do desafio.

---

## Adaptações nos Dados

> Você modificou ou expandiu os dados mockados? Descreva aqui.

Os dados mockados foram expandidos e enriquecidos em relação ao template original, passando de um cenário simples para um dataset operacional mais próximo de dados reais de negócio.

As principais adaptações incluem:

- Inclusão de múltiplas dimensões (categoria, produto, canal, região, tipo de cliente e status)

- Adição de métricas quantitativas como valor e quantidade

- Estruturação de um dicionário de dados para padronizar o significado das colunas

- Definição explícita de métricas e KPIs permitidos para análise

- Criação de regras de governança para limitar a atuação do agente

Essas adaptações permitem análises mais ricas e realistas, mantendo o escopo adequado ao desafio.

---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.

Os arquivos CSV e JSON localizados na pasta data são carregados no início da sessão do agente e incluídos como parte do contexto base utilizado na construção do prompt.

Os dados estruturados servem como a única fonte de verdade para as análises realizadas pelo agente.

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

- As regras definidas em `regras_analista.json` são incluídas no system prompt, delimitando o comportamento e as restrições do agente.

- O dicionário de dados `dicionario_dados.json` é utilizado para interpretação semântica das colunas durante as análises.

- As métricas disponíveis `metricas_analise.json` orientam quais análises podem ser sugeridas ou executadas.

- O dataset `dataset_operacional.csv` é consultado dinamicamente para geração de insights, resumos e explicações analíticas.

- O agente não cria dados ou métricas fora do que está definido nesses arquivos.

---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

```
Dataset Operacional:
- Total de registros: 10
- Categorias presentes: vendas, operacional
- Canais: ecommerce, loja_fisica, interno
- Regiões: sudeste, nordeste, sul

Métricas disponíveis:
- Receita total
- Ticket médio
- Volume por canal
- Receita por região
- Tendência temporal

Regras do Analista:
- Analisar apenas dados fornecidos
- Explicar o raciocínio utilizado
- Não criar valores ou categorias inexistentes

Solicitação do Usuário:
"Quais insights podem ser extraídos sobre vendas por canal e região?"
```
