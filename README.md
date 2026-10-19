# 🛍️ Gerenciador de Vendas — Loja de Roupas

Sistema em Python, que roda no terminal, para **gerar, ler e gerenciar registros de vendas** de uma loja de roupas armazenados em arquivos CSV.

> 🎓 Projeto desenvolvido como **trabalho final da disciplina de Programação de Computadores I** do curso de Ciência da Computação da **Universidade Federal Fluminense (UFF)**.

---

## 📋 Sobre o projeto

O trabalho foi dividido em **três etapas**. Cada uma usa o resultado da anterior:

```
ETAPA 1                 ETAPA 2                     ETAPA 3
Gera o CSV     ──▶      Lê o CSV e cria     ──▶     Menu para adicionar,
com vendas              objetos de venda            buscar, remover e
aleatórias              (classe item)               salvar vendas
```

Conceitos de programação trabalhados:

- Manipulação de arquivos (leitura e escrita de CSV)
- Programação orientada a objetos (classe com getters e setters)
- Geração de dados aleatórios
- Tratamento de exceções (`try`/`except`)
- Modularização (importação entre arquivos)
- Medição de desempenho com `time`

---

## 🗂️ Estrutura

```
├── ETAPA1.py   # Gerador de vendas aleatórias
├── ETAPA2.py   # Leitura do CSV e classe item
├── ETAPA3.py   # Menu interativo de gerenciamento
└── teste.csv   # Exemplo de arquivo gerado (15 vendas)
```

### Formato do CSV

| id venda | data       | categoria   | preço unitário | quantidade | valor total | id vendedor |
|----------|------------|-------------|----------------|------------|-------------|-------------|
| 01       | 2025-07-07 | Short Jeans | R$96.08        | 4          | R$384.32    | 0002        |

---

## ⚙️ As etapas

### Etapa 1: Geração de dados (`ETAPA1.py`)

Cria um arquivo CSV com quantas vendas fictícias o usuário quiser.

- Pergunta o **nome do arquivo** e o **número de linhas** (vendas).
- Para cada venda, sorteia:
  - uma **categoria** entre 9 produtos (camiseta básica, camisa social, regata, casaco de moletom, bermuda de moletom, calça jeans, casaco de couro, short jeans e bermuda de elastano);
  - um **preço unitário** dentro da faixa realista daquela categoria (ex.: regata de R$ 19,90 a R$ 49,90, casaco de couro de R$ 219,90 a R$ 349,90);
  - uma **quantidade** de 1 a 5 unidades;
  - um **vendedor** entre três IDs (`0001`, `0002`, `0003`).
- Calcula o **valor total** (preço × quantidade).
- Gera o **ID da venda** sequencial, completado com zeros à esquerda conforme o tamanho do arquivo (ex.: `0001` em um arquivo com 1000 vendas).
- Gera as **datas** a partir do dia atual, avançando 7 horas a cada venda. Assim, as vendas ficam distribuídas ao longo de vários dias.
- No final, mostra **quanto tempo** levou para gerar o arquivo. Isso permite comparar o desempenho com arquivos de tamanhos diferentes.

### Etapa 2: Leitura e modelagem (`ETAPA2.py`)

Transforma cada linha do CSV em um objeto Python.

- Define a classe **`item`**, que representa uma venda, com os atributos `id`, `data`, `categoria`, `preco`, `quantidade`, `vtotal` e `vendedor`, além de **getters e setters** para cada um.
- Na criação do objeto, converte preço e valor total para `float` e quantidade para `int`. Se algum valor for inválido, usa `0` em vez de quebrar o programa.
- A função **`acesso(arquivo)`**:
  - lê o arquivo e ignora o cabeçalho;
  - pula linhas vazias ou com número de colunas diferente de 7;
  - remove o prefixo `R$` e troca vírgula por ponto nos valores;
  - devolve uma **lista de objetos `item`**, ou `None` se o arquivo não existir ou não puder ser lido.
- Executado sozinho, o arquivo mostra os dados do segundo item da lista, como teste de que a leitura funcionou.

### Etapa 3: Gerenciamento interativo (`ETAPA3.py`)

Usa a Etapa 2 para carregar o CSV e oferece um **menu** de operações:

| Opção | Ação | O que faz |
|:-----:|------|-----------|
| 1 | **Adicionar venda** | Escolhe categoria, quantidade, preço e vendedor. O ID é gerado automaticamente (o último ID + 1, com os mesmos zeros à esquerda), a data é a de hoje e o valor total é calculado. |
| 2 | **Buscar por linha** | Mostra todos os dados da venda na posição escolhida. |
| 3 | **Remover venda** | Procura a venda pelo ID e pede confirmação (`s/n`) antes de remover. |
| 4 | **Salvar alterações** | Grava a lista atualizada de volta no mesmo arquivo CSV. |
| 5 | **Sair** | Encerra o programa. |

As alterações ficam só na memória até o usuário escolher **Salvar**. Entradas inválidas, como letras no lugar de números ou opções fora da lista, são tratadas com mensagens de erro e não fecham o programa.

---

## 🚀 Como executar

Requisito: **Python 3** (só bibliotecas padrão, nada para instalar).

```bash
git clone https://github.com/Gbravo22/gerenciador-de-vendas-python.git
cd gerenciador-de-vendas-python
```

**1. Gere um arquivo de vendas:**

```bash
python ETAPA1.py
```
```
Qual o nome do arquivo que você deseja criar?
vendas.csv
Qual o número total de linhas que você deseja ter no seu arquivo?
1000
O tempo que levou para gerar o arquivo vendas.csv, foi de 0.0074 segundos
```

**2. (Opcional) Teste a leitura:**

```bash
python ETAPA2.py
```

**3. Gerencie as vendas pelo menu:**

```bash
python ETAPA3.py
```
```
Nome do arquivo CSV para carregar: vendas.csv

===== MENU =====
1. Adicionar venda
2. Buscar por linha
3. Remover venda
4. Salvar alterações
5. Sair
Escolha:
```

> 💡 Para testar sem gerar nada, use o arquivo `teste.csv` que já vem no repositório.

---

## 👤 Autor

**Gabriel Francisco Bravo**, estudante de Ciência da Computação na UFF
[github.com/Gbravo22](https://github.com/Gbravo22)
