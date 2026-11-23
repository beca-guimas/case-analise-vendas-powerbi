# Relatório Comercial: Vendas, Faturamento e Margem (Power BI & Sheets)

Projeto de análise de dados desenvolvido com Google Sheets e Power BI para avaliar vendas e faturamento de uma empresa de bicicletas com atuação internacional (2013 a 2016).
A partir da demanda da área comercial, fiz toda a limpeza e validação de quatro planilhas brutas e criei um dashboard com duas visões: uma para o time de vendas acompanhar clientes, países e setores no dia a dia, e outra para a diretoria avaliar resultados mensais, anuais e definir estratégias.

*Ferramentas utilizadas:* Power BI | Power Query (M) | DAX | Google Sheets 

---

## Visão Geral do Relatório:

### Página 1 — Executivo (Mensal)

> Visão geral para acompanhamento da diretoria: receita total, lucro, margem, evolução mês a mês e comparação entre anos e segmentos.

<img width="1600" height="829" alt="WhatsApp Image 2026-11-06 at 21 37 18" src="https://github.com/user-attachments/assets/782fec46-54b5-4a46-8f30-4e5681d867ce" />


### Página 2 — Operacional (Time de Vendas)
> Detalhamento por país e produto, impacto dos descontos na margem e filtros para consulta diária da equipe comercial.

<img width="1600" height="833" alt="WhatsApp Image 2026-11-06 at 21 36 56" src="https://github.com/user-attachments/assets/8d014f4a-d905-46a4-8959-ff65a51a39d9" />

---

## 1. Limpeza e Validação dos Dados

O projeto partiu de quatro planilhas separadas (`Sales` e `Manufacturing`, dos períodos `2013-14` e `2015-16`), chegando a **1.358 registros** válidos depois da limpeza:

* **Ajuste de colunas:** Separação da coluna que trazia país e produto juntos (`"País,Produto"`) em 2013-14 e preenchimento da coluna `Units Sold` na base de manufatura a partir da base de vendas.
* **Limpeza de texto e duplicatas:** Exclusão de uma coluna vazia (`Product_Name`), remoção de 15 linhas duplicadas, limpeza de espaços em branco sobrando em 13 registros e correção de 90 erros de digitação (*Governmemt*, *Smal Business*, *Enter&rise*, *FrancE*, etc.).
* **Conferência antes de juntar as bases:** Como as tabelas de vendas e manufatura não tinham uma coluna de ID em comum, conferi o alinhamento linha por linha antes de cruzar os dados (0 divergências), batendo a conta `Sales - COGS = Profit` e comparando `Segment`, `Country` e `Product`.

---

## 2. Modelagem no Power Query e DAX

<img width="1600" height="857" alt="WhatsApp Image 2026-11-06 at 21 37 38" src="https://github.com/user-attachments/assets/6e9bc52c-f0db-425f-a798-f75df383a0e2" />


* **Junção das bases:** Empilhamento dos períodos 2013-14 e 2015-16, criação de índice para cruzar `Sales` com `Manufacturing` sem erro e reconstrução das datas usando `#date([Year], [Month Number], 1)`.
* **Modelo:** Tabela única `Vendas` (1.358 linhas × 16 colunas), deixando as consultas intermediárias desabilitadas para não pesar o arquivo.
* **Medidas DAX:**
  * `Receita = SUM(Vendas[Sales])` → **230,85 mi**
  * `Lucro = SUM(Vendas[Profit])` → **33,33 mi**
  * `Margem % = DIVIDE([Lucro], [Receita])` → **14,44%**

---

## 3. O que os dados Mostraram?

* **Queda forte de lucro em 2016 (Segmento Government):** Em 2015, órgãos públicos geraram 52,5 mi em receita (~94% do total) e 11,4 mi de lucro (margem de 22%). Em 2016, esse segmento sumiu da base, derrubando o lucro total de 12,0 mi para 4,5 mi. *O que fazer:* Verificar se houve falha na extração dos dados de 2016; se a queda for real, focar esforços comerciais para recuperar essa carteira.
* **Desconto alto derruba a margem:** A margem cai conforme o desconto aumenta — vai de **21,9%** (sem desconto) para **9,2%** (desconto alto). *O que fazer:* Criar regras de limite ou aprovação antes de conceder descontos altos.
* **Segmentos no vermelho vs. oportunidade:** `Enterprise` dá prejuízo (**-3,0%** de margem) e precisa ter contratos renegociados. Já `Channel Partners` tem a maior margem (**73%**), mas representa só 1,5% da receita, mostrando espaço para crescer nesse canal.
* **Sazonalidade:** As vendas sempre sobem em **outubro e dezembro**, indicando a necessidade de preparar estoque e negociações antes do fim do ano e criar promoções nos meses mais fracos do começo do ano.

---

## Arquivos do Repositório: 

* [`case_analise_vendas.pbix`](case_analise_vendas.pbix) — Arquivo completo do Power BI
* `dados/brutos/` — Planilhas originais (`Sales` e `Manufacturing` 2013-14 e 2015-16)
* `dados/tratados/` — Planilha tratada e consolidada
* `docs/` — Relatório técnico detalhado do projeto (PDF)



Autor: Beca Guimas :) 
