# analise-transporte-rj

**Movimento de passageiros no município do Rio de Janeiro, 1995–2025**

![Python 3.12](https://img.shields.io/badge/Python-3.12-blue) ![Código MIT](https://img.shields.io/badge/código-MIT-green)

**Autores** · Giovanna Sigette Lobo e Theo Cubas Reis  
**Orientador** · Alexandre Neves Louzada  
**Filiação** · Centro Universitário La Salle do Rio de Janeiro (UniLaSalle-RJ) · Sistemas de Informação · 6º período · 2026.2  
**Disciplina** · Linguagem de Programação (Análise e Visualização de Dados com Python)

## Resumo executivo

Como mudou o peso dos ônibus no movimento de passageiros do Rio de Janeiro e quais modais recuperaram o volume registrado em 2019? O estudo usa a Tabela 440 do Data.Rio para acompanhar seis séries anuais entre 1995 e 2025. A planilha original foi tratada em Python, mantendo a unidade de milhares de passageiros e as lacunas documentadas para o bonde de Santa Teresa. A comparação combina volumes absolutos, participações em anos com cobertura completa e índices relativos a 2019. Os ônibus mantiveram o maior movimento ao longo da série, mas sua participação caiu de 84,7% em 1995 para 68,1% em 2025. No mesmo intervalo, o metrô passou de 6,0% para 18,9%. Em 2020, todos os modais registraram queda frente ao ano anterior. Em 2025, apenas o bonde e o transporte aeroviário superaram seus volumes de 2019. Os resultados mostram como o crescimento relativo de um modal pode coexistir com um volume ainda inferior ao de anos anteriores. A agregação anual permite descrever essas diferenças, mas impede identificar trajetos individuais ou atribuir as mudanças a uma causa específica.

**Palavras-chave** · Mobilidade urbana, transporte de passageiros, Rio de Janeiro, séries temporais, dados abertos.

## Perguntas e resultados

1. Como evoluiu o volume de passageiros em cada modal?
2. Como mudou a participação dos modais entre 1995 e 2025?
3. Quais modais superaram em 2025 o volume de 2019, após a queda de 2020?

As duas primeiras colunas numéricas representam a parcela do movimento total dos seis modais no ano. As duas últimas medem a variação percentual do volume de cada modal frente a 2019.

| Modal | 1995 (%) | 2025 (%) | 2020 vs. 2019 (%) | 2025 vs. 2019 (%) |
|---|---|---|---|---|
| Ônibus | 84,7 | 68,1 | -45,1 | -33,3 |
| Metrô | 6,0 | 18,9 | -52,9 | -25,8 |
| Trem | 7,0 | 9,1 | -40,2 | -45,3 |
| Bonde | 0,0 | 0,1 | -66,7 | 72,8 |
| Hidroviário | 1,8 | 1,4 | -58,4 | -34,3 |
| Aeroviário | 0,5 | 2,5 | -57,0 | 7,7 |

## Fonte e acesso

A [Tabela 440 do Data.Rio](https://www.data.rio/documents/5d5849bf28bf4f689214f890e3f4ac04/about) reúne dados de operadores e órgãos de transporte. O arquivo bruto está em [data/raw/440.xls](data/raw/440.xls). A aba analisada é `T 440`. Cada linha corresponde a um ano do município do Rio de Janeiro. Vans e kombis estão fora da cobertura. Consulte as unidades, as lacunas e os créditos no [dicionário de dados](data/data_dictionary.md).

[Artigo acadêmico em HTML](https://sasktakeda.github.io/analise-transporte-rj/) · [Notebook de análise](notebooks/analise_exploratoria.ipynb) · [Base tratada em CSV.GZ](data/processed/movimento_passageiros_rio.csv.gz)

## Estrutura do repositório

```text
analise-transporte-rj/
├── README.md
├── LICENSE
├── requirements.txt
├── .gitignore
├── data/
│   ├── raw/440.xls
│   ├── processed/movimento_passageiros_rio.csv.gz
│   └── data_dictionary.md
├── notebooks/analise_exploratoria.ipynb
├── src/
│   ├── __init__.py
│   ├── etl.py
│   └── figuras.py
└── docs/
    ├── index.html
    └── assets/
        ├── series.png
        └── retomada.png
```

## Reprodução

Extraia o ZIP e abra o terminal na pasta que contém este README. Para obter uma cópia a partir do repositório publicado, copie a URL HTTPS no botão **Code** do GitHub e use `git clone URL_COPIADA` seguido de `cd analise-transporte-rj`.

Com Python 3.12, crie o ambiente com `python -m venv .venv`. Ative com `source .venv/bin/activate` em Linux/macOS ou `.\.venv\Scripts\Activate.ps1` em PowerShell. Execute na raiz:

```bash
python -m pip install -r requirements.txt
python -m src.etl
python -m src.figuras
python -m http.server 8000 --directory docs
```

Abra http://localhost:8000 para ler o artigo. O primeiro módulo lê o XLS e grava 31 linhas em CSV comprimido com cabeçalho UTF-8. O segundo refaz as duas figuras. A tabela do artigo corresponde à edição 1995–2025. Para abrir o notebook localmente no mesmo ambiente, instale a interface com `python -m pip install jupyterlab==4.4.10` e execute `python -m jupyterlab notebooks/analise_exploratoria.ipynb`. Execute as células em ordem a partir da raiz ou da pasta `notebooks`.

## Publicação no GitHub Pages

Envie o conteúdo da pasta do projeto para a raiz de um repositório público chamado `analise-transporte-rj`. Em **Settings → Pages → Build and deployment**, selecione **Deploy from a branch**, branch **main**, pasta **/docs** e salve. O endereço público aparecerá nessa mesma tela após a publicação. O artigo identifica o repositório a partir do endereço padrão do GitHub Pages.

## Reutilização e limites

O [código usa a licença MIT](LICENSE). Para o texto e as figuras de autoria da dupla, aplica-se [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/), com atribuição aos autores e à fonte. Para os dados originais e seus valores derivados, consulte as condições do provedor. A planilha anexada não informa uma licença específica. Os totais medem movimento de passageiros e podem contar a mesma pessoa em diferentes viagens ou modais.
