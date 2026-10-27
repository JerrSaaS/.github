# INC-UX-001 — Falha de fidelidade visual em fluxo assistido por IA

**Status:** Contido / correção em andamento  
**Data do registro:** 27 de outubro de 2026  
**Área:** Engenharia de Usabilidade / Governança de Ativos Visuais  
**Produto afetado:** JERR SaaS  
**Classificação:** Incidente de fidelidade a requisito e identidade visual

## Resumo executivo

Durante um fluxo de atualização visual assistido por IA, ativos visuais originais previamente aprovados foram substituídos ou representados por composições derivadas que não preservavam fielmente a fonte visual autorizada.

O requisito operacional era simples e determinístico: **o ativo original deveria permanecer como fonte de verdade**, com alterações limitadas a ajustes explicitamente autorizados, como remoção de textos específicos, integração responsiva e otimização técnica.

A divergência foi identificada durante revisão visual do ambiente público e durante a preparação de uma inspeção de Engenharia de Usabilidade.

## Regra esperada

```text
ORIGINAL_ASSET == SOURCE_OF_TRUTH
ALLOW_REPLACEMENT == false
ALLOW_REINTERPRETATION == false
DERIVATIVE_REQUIRES_EXPLICIT_APPROVAL == true
```

## Comportamento observado

O problema teve duas manifestações distintas:

1. **Exposição pública:** uma composição visual simplificada e diferente dos ativos originais aprovados ficou visível no ambiente público.
2. **Recorrência interceptada antes do merge:** uma proposta posterior continha novos derivados visuais que também não eram cópias fiéis dos originais; essa recorrência foi bloqueada antes de promoção.

## Impacto

O incidente gerou:

- inconsistência temporária de identidade visual;
- retrabalho de engenharia;
- revisão adicional de PRs, assets e hashes;
- bloqueio preventivo de promoção;
- risco reputacional e de percepção de maturidade do produto;
- impacto direto na preparação para inspeção de Engenharia de Usabilidade;
- necessidade de reforçar a governança de ativos em fluxos assistidos por IA.

Este registro não atribui intenção econômica ou dolo a qualquer fornecedor. Ele documenta apenas uma **divergência verificável entre requisito explícito e execução**.

## Evidência técnica

Os ativos originais foram preservados e possuem identificação criptográfica.

### Original JERR

```text
SHA-256:
fdfe9d83c65545db6bce9c32ee46bbc0ea3c7953e35869327fb334b77a118148
```

### Original ORCHIMATO

```text
SHA-256:
60432ee86c91f6ea4b9050f87b75b25e58c51e226588fd0695a05ffe930f2918
```

Capturas de tela, histórico de execução, commits, PRs e logs adicionais permanecem preservados em registros internos da JERR.

## Contenção

Após a identificação:

- a promoção da alteração visual foi bloqueada;
- os originais foram redefinidos como fonte de verdade;
- derivados não aprovados foram rejeitados;
- a revisão visual humana passou a ser obrigatória;
- nenhuma nova substituição criativa é permitida sem aprovação explícita.

## Política corretiva

```text
ORIGINAL
→ VERIFY HASH
→ SOURCE OF TRUTH
→ DERIVATIVE ONLY IF AUTHORIZED
→ VISUAL DIFF
→ TEST
→ HUMAN APPROVAL
→ RELEASE
```

Se a origem visual não puder ser determinada:

```text
STOP
```

Nenhum agente deve gerar automaticamente um substituto.

## Critérios de encerramento

O incidente somente pode ser encerrado quando houver:

```text
original visual fidelity: PASS
card dimensions unchanged: PASS
layout consistency: PASS
duplicate content: PASS
responsive validation: PASS
owner visual approval: PASS
```

## Medidas preventivas permanentes

A JERR passa a exigir, para ativos visuais críticos:

- registro do original;
- SHA-256;
- provenance record;
- separação entre original e derivado;
- autorização explícita para derivados;
- visual diff;
- validação responsiva;
- aprovação humana antes de promoção.

## Regra de primeira ordem

Em requisitos determinísticos, uma fonte fornecida e aprovada pelo proprietário prevalece sobre preferência do modelo, interpretação estética, otimização heurística ou velocidade de entrega.

## Objetivo deste registro

Este documento tem finalidade de engenharia, auditoria e melhoria contínua. O objetivo é transformar uma falha observada em um controle verificável e reutilizável para futuros fluxos de IA no ecossistema JERR SaaS.
