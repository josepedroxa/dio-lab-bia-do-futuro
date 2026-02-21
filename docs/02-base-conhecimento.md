# Base de Conhecimento

## Dados Utilizados

Descreva se usou os arquivos da pasta `data`, por exemplo:

| Arquivo | Formato | Agente Robert IA Finance  |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | Contextualizar interações anteriores , dar continuidade ao atendimento de forma mais eficiente .|
| `perfil_investidor.json` | JSON | Personalizar as explicações sobre as duvidas e necessidades de aprendizado do cliente  |
| `produtos_financeiros.json` | JSON | Conhecer os produtos disponiveis para que ele possam ser explicado aos cliente . |
| `transacoes.csv` | CSV | Analisar padrão de gastos do cliente , e usar essas informações de forma didática |



---

## Adaptações nos Dados

> Você modificou ou expandiu os dados mockados? Descreva aqui.
> o Fundo imobiliario FII substituiu o fundo multi mercado, foram adicionados , as metas orçamentarias para PJ, e PF, tendo em vista o controle orçamentario par ambos , Assim poderei validar as resposta do Robert de forma mais clara , e assertiva 

[Sua descrição aqui]

---

## Estratégia de Integração

### Como os dados são carregados?
>
>import json
import  pandas as pd
perfil = json.load (open('./data/perfil_investidor.jason'))
transacoes = pd.read_csv('./data/transacoes.csv')
historico = pd.read_csv('./data/historico_atendimento')
produtos = json.load(open('./data/produtos_financeiros.json'))

[ex: Os JSON/CSV são carregados no início da sessão e incluídos no contexto do prompt]

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

[Sua descrição aqui]
Existe dua possibilidades, os  dados podem ser inseridos  via prompt , ou carregar via codigo.
---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.
>
> Para simplificar podemos incluir informações dos prompt

```
texto 
Meta do PJ
Perfil Do PJ:
{
  "nome": "João Silva ",
  "idade": 32,
  "profissao": "Analista de Sistemas",
  "renda_mensal": 5000.00,
  "perfil_investidor": "moderado",
  "objetivo_principal": "Construir reserva de emergência",
  "patrimonio_total": 15000.00,
  "reserva_emergencia_atual": 10000.00,
  "aceita_risco": false,
  "metas": [
    {
      "meta": "Completar reserva de emergência",
      "valor_necessario": 15000.00,
      "prazo": "2026-06"
    },
    {
      "meta": "Entrada do apartamento",
      "valor_necessario": 50000.00,
      "prazo": "2027-12"
    }
  ]
}












 Meta do PF 
Perfil Do PF :

{
  "nome": "João Silva",
  "idade": 32,
  "profissao": "Analista de Sistemas",
  "renda_mensal": 5000.00,
  "perfil_investidor": "moderado",
  "objetivo_principal": "Construir reserva de emergência",
  "patrimonio_total": 15000.00,
  "reserva_emergencia_atual": 10000.00,
  "aceita_risco": false,
  "metas": [
    {
      "meta": "Completar reserva de emergência",
      "valor_necessario": 15000.00,
      "prazo": "2026-06"
    },
    {
      "meta": "Entrada do apartamento",
      "valor_necessario": 50000.00,
      "prazo": "2027-12"
    }
  ]
}

Transações do cliente;

data	descricao	categoria	valor	tipo
2025-10-01	Salário	receita	5000.00	entrada
2025-10-02	Aluguel	moradia	1200.00	saida
2025-10-03	Supermercado	alimentacao	450.00	saida
2025-10-05	Netflix	lazer	55.90	saida
2025-10-07	Farmácia	saude	89.00	saida
2025-10-10	Restaurante	alimentacao	120.00	saida
2025-10-12	Uber	transporte	45.00	saida
2025-10-15	Conta de Luz	moradia	180.00	saida
2025-10-20	Academia	saude	99.00	saida
2025-10-25	Combustível	transporte	250.00	saida
2025-10-25	Meta	Orçamento	550.00	saida
2025-10-25	Limite da Meta	Orçamento	550.00	saida


Produtos disponiveis para ensino  :


[
  {
    "nome": "Tesouro Selic",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "100% da Selic",
    "aporte_minimo": 30.00,
    "indicado_para": "Reserva de emergência e iniciantes"
  },
  {
    "nome": "CDB Liquidez Diária",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "102% do CDI",
    "aporte_minimo": 100.00,
    "indicado_para": "Quem busca segurança com rendimento diário"
  },
  {
    "nome": "LCI/LCA",
    "categoria": "renda_fixa",
    "risco": "baixo",
    "rentabilidade": "95% do CDI",
    "aporte_minimo": 1000.00,
    "indicado_para": "Quem pode esperar 90 dias (isento de IR)"
  },
  {
    "nome": "Fundo Imboliario (FII)",
    "categoria": "fundo",
    "risco": "medio",
    "rentabilidade": "6% + 12%",
    "aporte_minimo": 100.00,
    "indicado_para": "Perfil moderado que busca diversificação"
  },
  {
    "nome": "Fundo de Ações",
    "categoria": "fundo",
    "risco": "alto",
    "rentabilidade": "Variável",
    "aporte_minimo": 100.00,
    "indicado_para": "Perfil arrojado com foco no longo prazo"


    {
    "nome": "Meta Orçamentaria  (PF)",
    "categoria": "fundo",
    "risco": "medio",
    "rentabilidade": "12% + 14%",
    "aporte_minimo": 450.00,
    "indicado_para": "Perfil moderado, e diversificado "
  },


    {
    "nome": "Meta Orçamentaria  (PJ)",
    "categoria": "fundo",
    "risco": "alto",
    "rentabilidade": "75% + 95%",
    "aporte_minimo": 1000000.00,
    "indicado_para": "Perfil  Alto Risco,  buscar investimentos em consultoria  "
  },
  
  }
]

```


```
Dados do Cliente:
- Nome: João Silva
- Perfil: Moderado
- Saldo disponível: R$ 5.000

Últimas transações:
- 01/11: Supermercado - R$ 450
- 03/11: Streaming - R$ 55
...
```
