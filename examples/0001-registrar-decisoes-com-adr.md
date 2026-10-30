# ADR 0001 — Registrar decisões de arquitetura com ADRs

> Exemplo fictício · Empresa Exemplo S.A.

| Campo | Valor |
|---|---|
| **Status** | Aceito |
| **Data** | 2026-01-15 |
| **Decisores** | Arquitetura corporativa, CTO |
| **Camada TOGAF** | Governança |

## 1. Contexto

As decisões de arquitetura ficavam espalhadas em atas, e-mails e apresentações. Em uma auditoria interna, 7 de 10 decisões amostradas não tinham justificativa recuperável, e duas discussões sobre o mesmo tema foram reabertas no mesmo trimestre.

## 2. Direcionadores

- Rastreabilidade das decisões para auditoria e novos integrantes
- Reduzir retrabalho em discussões recorrentes
- Dar previsibilidade ao ARB

## 3. Opções consideradas

| Opção | Prós | Contras |
|---|---|---|
| A — ADRs em Markdown versionados no Git | Simples, revisável por PR, histórico completo | Exige disciplina de escrita |
| B — Ferramenta de EA (repositório de decisões) | Integra com portfólio | Licença; curva de aprendizado; menos adesão dos times |
| C — Manter atas | Nenhum esforço novo | Não resolve o problema |

## 4. Decisão

Adotar **ADRs em Markdown** (opção A), um por arquivo, revisados via *pull request*, usando o [modelo padrão](../templates/adr-template.md).

## 5. Consequências

**Positivas** — histórico auditável; revisão assíncrona; onboarding mais rápido.
**Negativas** — esforço inicial de escrita. Mitigação: modelo curto e apoio do arquiteto de domínio.

## 7. Governança

- **Revisar em:** 6 meses
- **Indicador:** 100% das decisões do ARB com ADR associado
