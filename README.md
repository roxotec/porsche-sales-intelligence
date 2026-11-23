# Porsche Sales Intelligence

Dashboard executiva e interativa para explorar uma base de vendas de veículos Porsche. O projeto foi desenvolvido em **HTML, CSS e JavaScript puro**, em um único arquivo, sem bibliotecas externas e sem backend.

> **Status de publicação:** o projeto está preparado para GitHub Pages por GitHub Actions. O endereço público previsto é [https://roxotec.github.io/porsche-sales-intelligence/](https://roxotec.github.io/porsche-sales-intelligence/). Ele só estará disponível depois que o repositório for criado na conta GitHub e o primeiro deploy terminar com sucesso.

## Repositório

- URL prevista: https://github.com/roxotec/porsche-sales-intelligence
- Nome: `porsche-sales-intelligence`
- Visibilidade pretendida: público
- Arquivo principal: [`index.html`](index.html)

## Perguntas de negócio

As perguntas foram escolhidas para transformar a tela em uma ferramenta de decisão comercial, e não apenas em uma coleção de gráficos:

1. **Quais modelos geram mais receita?** Um ranking de faturamento por modelo ajuda a identificar os produtos que mais contribuem para a receita e comparar o mix comercial.
2. **Como a receita evolui ao longo do tempo?** Uma série mensal ajuda a observar tendências e meses de maior faturamento. Ela usa somente registros com data válida.
3. **Como os clientes pagam?** A distribuição dos métodos de pagamento por quantidade de vendas mostra os meios mais utilizados e a composição do volume.

### Indicadores complementares

- Receita total;
- quantidade de vendas registradas;
- ticket médio;
- percentual e quantidade de entregas concluídas;
- ranking de estados por receita;
- qualidade das datas (válidas versus inválidas).

## Filtros disponíveis

- Modelo Porsche;
- estado;
- ano da venda (derivado da data de venda sanitizada);
- método de pagamento.

Os filtros atualizam os indicadores, gráficos e tabelas em conjunto. O botão **Limpar filtros** restaura a visão completa.

## Prompt utilizado

O prompt de trabalho consolidado que orientou a versão final foi:

> Crie uma dashboard de vendas em HTML, em arquivo único, usando a planilha fornecida como fonte. A dashboard deve responder a três perguntas de negócio: (1) quais modelos geram mais receita, com ranking de faturamento; (2) como a receita evolui mensalmente, com uma série temporal; e (3) quais métodos de pagamento são mais utilizados, com distribuição por quantidade de vendas. Inclua indicadores de receita total, quantidade de vendas, ticket médio e entregas concluídas. Disponibilize filtros interativos por modelo, estado, ano da venda e método de pagamento, que atualizem todos os componentes. Use uma identidade visual executiva inspirada na Porsche, com fundo escuro, vermelho de destaque, tipografia sem serifa, boa hierarquia visual e layout responsivo. Utilize os campos sanitizados da planilha. Não descarte registros com data inválida dos indicadores financeiros; exclua-os apenas da série temporal e apresente a qualidade da data de forma explícita. Remova nomes de clientes e vendedores e quaisquer identificadores pessoais da versão pública. Não dependa de bibliotecas ou serviços externos.

### O que evoluiu até a versão final

- **Da solicitação ampla para perguntas explícitas:** a primeira orientação pedia uma dashboard que respondesse perguntas de negócio. Foram definidas três perguntas concretas e um gráfico adequado para cada uma.
- **Filtros mais úteis:** o filtro geográfico foi definido por estado, além de modelo, ano da venda e método de pagamento.
- **Regra de qualidade de dados:** datas inválidas continuam compondo os KPIs financeiros e de volume, mas não entram na série mensal. A dashboard mostra a proporção de datas válidas e inválidas.
- **Privacidade para publicação:** a versão de portfólio removeu nomes de clientes e vendedores, assim como campos não necessários à visualização.
- **Entrega web:** o HTML foi transformado em `index.html` e foi adicionado um workflow para publicar automaticamente no GitHub Pages a cada atualização da branch `main`.

## Tratamento da base antes de enviar à IA

A planilha fornecida já continha colunas originais e versões sanitizadas. A dashboard utiliza as colunas sanitizadas da aba `Sanitized`:

| Campo | Tratamento utilizado |
|---|---|
| Data da venda | Padronização para `AAAA-MM-DD`; datas impossíveis ou não interpretáveis recebem `INVALID`. |
| Modelo Porsche | Uso do campo padronizado `PorscheModelSanitized`. |
| Ano do modelo | Uso do campo numérico sanitizado `ModelYearSanitized`. |
| Preço | Conversão de formatos textuais de moeda para valor numérico em USD. |
| Quilometragem | Conversão de textos com unidades e separadores para valor numérico. |
| Método de pagamento | Padronização de categorias, por exemplo, `Credit Card` e `Wire Transfer`. |
| Estado | Padronização para siglas de estado. |
| Status de entrega | Padronização de categorias, por exemplo, `Delivered` e `In Transit`. |

### Privacidade e escopo dos dados publicados

- A base de origem contém **100 registros**.
- Na coluna de data sanitizada, **76 registros têm data válida e 24 estão marcados como `INVALID`**.
- Nomes de clientes e vendedores foram excluídos do JSON embutido no HTML.
- A versão pública não contém a planilha Excel original.
- O HTML incorpora somente os campos necessários à análise: data sanitizada, modelo, ano do modelo, receita, quilometragem, método de pagamento, estado e status de entrega.

A receita e o ticket médio são apresentados em **USD**, conforme a unidade monetária da base. A série temporal considera somente as datas válidas; os indicadores de receita e quantidade consideram todos os registros que atendem aos filtros.

## Tecnologia e modo de construção

- HTML5, CSS3 e JavaScript puro;
- gráficos desenhados com Canvas;
- processamento local no navegador;
- arquivo único de dashboard (`index.html`), sem dependências externas.

**Fluxo utilizado:** ChatGPT em conversa normal, com geração e revisão do código. Não foi utilizado Canvas e não foi configurado um agente com skills. O workflow do GitHub Actions é usado somente para publicação contínua no GitHub Pages.

## Estrutura do projeto

```text
porsche-sales-intelligence/
├── .github/
│   └── workflows/
│       └── pages.yml
├── images/
│   └── README.md
├── .nojekyll
├── index.html
└── README.md
```

A pasta `images/` contém instruções para adicionar capturas reais após a validação no GitHub Pages. Não há screenshots artificiais incluídas como evidência.

## Como executar localmente

1. Baixe ou clone o repositório.
2. Abra `index.html` em um navegador moderno.
3. Escolha os filtros para atualizar os indicadores e gráficos.

Não é necessário instalar Python, Node.js ou bibliotecas JavaScript.

## Publicação no GitHub Pages

O arquivo [`.github/workflows/pages.yml`](.github/workflows/pages.yml) publica o conteúdo da branch `main` automaticamente.

Depois de criar o repositório:

1. Acesse **Settings → Pages**.
2. Em **Build and deployment**, selecione **GitHub Actions** como fonte, se ainda não estiver selecionado.
3. Faça o primeiro push para `main` e aguarde o workflow `Deploy dashboard to GitHub Pages` concluir.
4. Confirme que o endereço `https://roxotec.github.io/porsche-sales-intelligence/` abre a dashboard.

## Evidências

Após o deploy, salvar em `images/` uma captura da visão geral e outra com `Modelo = 911 Turbo S` e `Método de pagamento = Wire Transfer`. A pasta inclui instruções; ainda não há capturas porque o repositório precisa ser conectado à conta GitHub e publicado. A ausência de capturas não deve ser interpretada como evidência de deploy concluído.

---

Projeto demonstrativo de análise de dados e storytelling com dados. A marca Porsche é citada apenas como referência visual e temática do conjunto de dados utilizado.
