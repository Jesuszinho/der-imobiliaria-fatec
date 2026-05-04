# Explicação do DER — Sistema Imobiliário

Este documento descreve as decisões de modelagem do Diagrama Entidade-Relacionamento (DER) do sistema de imobiliária, detalhando cada entidade, seus atributos e os relacionamentos entre elas.

---

## Entidades e Atributos

### 1. CLIENTE
Representa a pessoa física interessada em alugar ou comprar um imóvel.

| Atributo | Descrição |
|----------|-----------|
| `id_cliente` | Identificador único do cliente (PK) |
| `nome_completo` | Nome completo do cliente |
| `cpf` | CPF do cliente (UK) |
| `data_nascimento` | Data de nascimento |
| `telefone` | Contato telefônico |
| `email` | Endereço de e-mail |
| `tipo_cliente` | Indica se é comprador, locatário ou ambos |

---

### 2. VISITA
Registra as visitas realizadas por clientes a imóveis, com intermediação de um corretor.

| Atributo | Descrição |
|----------|-----------|
| `id_visita` | Identificador único da visita (PK) |
| `data_visita` | Data em que a visita foi realizada |
| `horario` | Horário agendado |
| `observacoes` | Anotações relevantes sobre a visita |

---

### 3. CORRETOR
Profissional responsável por intermediar negociações e acompanhar visitas.

| Atributo | Descrição |
|----------|-----------|
| `id_corretor` | Identificador único do corretor (PK) |
| `nome_completo` | Nome completo |
| `numero_creci` | Registro profissional no CRECI (UK) |
| `data_admissao` | Data de entrada na imobiliária |
| `telefone` | Contato telefônico (UK) |
| `email` | Endereço de e-mail |
| `salario` | Salário base do corretor |

---

### 4. CONTRATO
Documento formal que formaliza a relação entre cliente, corretor e imóvel (venda ou locação).

| Atributo | Descrição |
|----------|-----------|
| `id_contrato` | Identificador único do contrato (PK) |
| `tipo_contrato` | Venda ou locação |
| `data_inicio` | Data de início da vigência |
| `data_fim` | Data de encerramento |
| `valor_total` | Valor total acordado |
| `status` | Situação atual (ativo, encerrado, cancelado) |

---

### 5. PAGAMENTO
Registra cada pagamento vinculado a um contrato.

| Atributo | Descrição |
|----------|-----------|
| `id_pagamento` | Identificador único do pagamento (PK) |
| `data_pagamento` | Data em que o pagamento foi efetuado |
| `valor_pago` | Valor da parcela paga |
| `forma_pagamento` | PIX, boleto, transferência, etc. |
| `status_pagamento` | Pago, pendente ou atrasado |

---

### 6. IMÓVEL
Unidade imobiliária cadastrada no sistema, podendo ser ofertada para venda ou locação.

| Atributo | Descrição |
|----------|-----------|
| `id_imovel` | Identificador único do imóvel (PK) |
| `tipo_imovel` | Casa, apartamento, sala comercial, etc. |
| `endereco` | Logradouro completo |
| `cidade` | Cidade do imóvel |
| `estado` | Estado (UF) |
| `cep` | CEP |
| `area_total_m2` | Área total em metros quadrados |
| `area_construida_m2` | Área construída em metros quadrados |
| `quantidade_quartos` | Número de quartos |
| `quantidade_banheiros` | Número de banheiros |
| `vagas_garagem` | Quantidade de vagas de garagem |
| `valor_venda` | Valor para venda |
| `valor_locacao` | Valor mensal de locação |
| `status` | Disponível, vendido ou alugado |

---

### 7. MANUTENÇÃO
Registra serviços de manutenção realizados em um imóvel.

| Atributo | Descrição |
|----------|-----------|
| `id_manutencao` | Identificador único (PK) |
| `descricao` | Descrição do serviço executado |
| `data_inicio` | Início da manutenção |
| `data_fim` | Conclusão da manutenção |
| `custo` | Custo total do serviço |
| `status` | Em andamento, concluída ou cancelada |

---

### 8. PROPRIETÁRIO
Pessoa física ou jurídica que detém a posse do imóvel e o disponibiliza à imobiliária.

| Atributo | Descrição |
|----------|-----------|
| `id_proprietario` | Identificador único (PK) |
| `nome_completo` | Nome completo ou razão social |
| `cpf_cnpj` | CPF (pessoa física) ou CNPJ (pessoa jurídica) (UK) |
| `telefone` | Contato telefônico |
| `email` | Endereço de e-mail |
| `endereco` | Endereço do proprietário |

---

## Relacionamentos e Cardinalidades

### CLIENTE — realiza — VISITA `(1:N)`
Um cliente pode agendar e realizar várias visitas a diferentes imóveis. Cada visita pertence a um único cliente.

### VISITA — ocorre com — CORRETOR `(N:1)`
Várias visitas podem ser conduzidas pelo mesmo corretor. Cada visita é acompanhada por um único corretor.

### CLIENTE — celebra — CONTRATO `(1:N)`
Um cliente pode firmar mais de um contrato ao longo do tempo (ex: alugar um imóvel e depois comprar outro). Cada contrato está vinculado a um único cliente.

### CORRETOR — intermedia — CONTRATO `(1:N)`
Um corretor pode intermediar vários contratos. Cada contrato é fechado com a participação de um único corretor.

### CONTRATO — gera — PAGAMENTO `(1:N)`
Um contrato pode gerar múltiplos pagamentos (parcelas mensais de aluguel, por exemplo). Cada pagamento está associado a um único contrato.

### CONTRATO — vincula-se — IMÓVEL `(N:1)`
Vários contratos podem envolver o mesmo imóvel ao longo do tempo (ex: contratos de aluguel consecutivos). Cada contrato, porém, refere-se a um único imóvel em determinado período.

### IMÓVEL — possui — MANUTENÇÃO `(1:N)`
Um imóvel pode passar por diversas manutenções ao longo do tempo. Cada manutenção está vinculada a um único imóvel.

### IMÓVEL — pertence a — PROPRIETÁRIO `(N:1)`
Vários imóveis podem pertencer ao mesmo proprietário. Cada imóvel tem um único proprietário registrado.

### IMOBILIÁRIA — gerencia — IMÓVEL `(1:N)`
A imobiliária administra o portfólio de imóveis cadastrados. Um imóvel é gerenciado por uma única imobiliária.

---

## Observações de Modelagem

- O atributo `tipo_cliente` na entidade CLIENTE foi incluído para diferenciar perfis de interesse (comprador, locatário ou ambos), facilitando filtros e relatórios.
- A entidade PROPRIETÁRIO usa `cpf_cnpj` como atributo único para contemplar tanto pessoas físicas quanto jurídicas sem necessidade de entidades separadas.
- O atributo `status` presente em IMÓVEL, CONTRATO, PAGAMENTO e MANUTENÇÃO padroniza o controle de ciclo de vida em todas as entidades operacionais.
- A separação entre `area_total_m2` e `area_construida_m2` no IMÓVEL permite maior precisão na descrição de terrenos e imóveis com área externa.
