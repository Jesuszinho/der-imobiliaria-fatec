# DER Imobiliária — FATEC

Diagrama Entidade-Relacionamento (DER) desenvolvido como atividade prática da disciplina de Banco de Dados na FATEC.

## Estrutura do Repositório

```
der-imobiliaria-fatec/
│
├── README.md
├── docs/
│   ├── DER_Imobiliaria.pdf       # Levantamento de entidades e atributos
│   └── explicacao.md             # Explicação detalhada do modelo
│
├── diagram/
│   ├── imobiliaria.drawio.xml    # Arquivo editável (draw.io)
│   ├── imobiliaria.drawio.html   # Versão HTML interativa
│   └── imobiliaria.png           # Imagem exportada do diagrama
│
└── embed/
    └── embed.txt                 # Código de incorporação do diagrama
```

## Sobre o Projeto

Este repositório contém o DER de um sistema de imobiliária, modelando as principais entidades envolvidas no processo de compra, venda e locação de imóveis.

O diagrama foi construído seguindo o padrão fornecido pela professora:

- **Retângulos** — representam as entidades
- **Losangos** — representam os relacionamentos entre entidades
- **Elipses** — representam os atributos; as elipses correspondentes a chaves primárias (PK) são destacadas na cor vermelha

## Resumo do Modelo

| Item | Quantidade |
|------|-----------|
| Entidades | 8 |
| Atributos totais | 55 |
| Relacionamentos | 9 |

### Entidades

| Entidade | Atributos |
|----------|-----------|
| CLIENTE | 7 |
| VISITA | 4 |
| CORRETOR | 7 |
| CONTRATO | 6 |
| PAGAMENTO | 5 |
| IMOVEL | 14 |
| MANUTENCAO | 6 |
| PROPRIETARIO | 6 |

## Relacionamentos (Cardinalidades)

| Relacionamento | Cardinalidade |
|----------------|--------------|
| CLIENTE realiza VISITA | 1:N |
| VISITA ocorre com CORRETOR | N:1 |
| CLIENTE celebra CONTRATO | 1:N |
| CORRETOR intermedia CONTRATO | 1:N |
| CONTRATO gera PAGAMENTO | 1:N |
| CONTRATO vincula-se a IMOVEL | N:1 |
| IMOVEL possui MANUTENCAO | 1:N |
| IMOVEL pertence a PROPRIETARIO | N:1 |
| IMOBILIARIA gerencia IMOVEL | 1:N |

## Ferramenta Utilizada

Diagrama criado com [draw.io](https://app.diagrams.net/). Para editar, abra o arquivo `diagram/imobiliaria.drawio.xml` diretamente no draw.io.

---

Atividade desenvolvida para a disciplina de Banco de Dados — FATEC.
