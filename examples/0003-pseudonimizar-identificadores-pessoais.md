# ADR 0003 — Pseudonimizar CPF/CNPJ nas integrações

> Exemplo fictício · Empresa Exemplo S.A.

| Campo | Valor |
|---|---|
| **Status** | Aceito |
| **Data** | 2026-03-10 |
| **Decisores** | Arquitetura corporativa, DPO, Segurança, Dados |
| **Camada TOGAF** | Dados |

## 1. Contexto

O CPF é usado como chave de integração entre CRM, ERP, ITSM e o data lake, e aparece em logs, filas e cargas analíticas. Isso amplia a superfície de exposição de dados pessoais e contraria os princípios de minimização e segurança da LGPD.

## 2. Direcionadores

- Conformidade com a LGPD (minimização, segurança)
- Manter a capacidade de cruzar dados entre sistemas
- Não depender de reescrever o sistema de registro

## 3. Opções consideradas

| Opção | Prós | Contras |
|---|---|---|
| A — Hash SHA-256 do CPF | Simples | Reversível por força bruta (espaço de ~10⁹ valores) |
| B — HMAC-SHA256 com chave no cofre, por contexto | Irreversível sem a chave; determinístico; separa domínios | Exige gestão e rotação de chave |
| C — Tokenização com cofre de tokens | Reversível de forma controlada | Mais um serviço crítico; custo |

## 4. Decisão

Adotar a **opção B**. O CPF/CNPJ em claro fica apenas no sistema de registro; as demais plataformas recebem um pseudônimo HMAC por contexto, em formato UUID quando usado como External ID.

Implementação de referência: [lgpd-pseudonymization-reference](https://github.com/ncontatori/lgpd-pseudonymization-reference).

## 5. Consequências

**Positivas** — menos dado pessoal trafegando; joins preservados; logs sem CPF.
**Negativas** — dado pseudonimizado continua sendo dado pessoal; rotação de chave exige recarga. Mitigação: versionar a chave junto do pseudônimo.

## 7. Governança

- **Indicador:** nº de integrações que ainda trafegam CPF em claro (meta: zero)
- **Revisar em:** 12 meses ou em caso de incidente
