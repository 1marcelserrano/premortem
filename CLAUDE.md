# CLAUDE.md — premortem

## O que é este repo

Uma skill do Claude distribuída como repositório público no GitHub. A única
fonte de verdade do comportamento é `skills/premortem/SKILL.md`. Toda mudança de
comportamento começa por lá.

A skill implementa o premortem de Gary Klein (HBR, 2007) + hindsight prospectivo
(Mitchell, Russo & Pennington, 1989): um protocolo que assume que a decisão já
falhou e trabalha de trás pra frente. O repo é uma vitrine — o README é uma
landing page, não só documentação.

## O que editar

| Arquivo | O que controla |
|---------|----------------|
| `skills/premortem/SKILL.md` | Comportamento da skill — triggers, fluxo, formato de saída. O corpo que o agente carrega. PT-BR, canônico. |
| `skills/premortem/references/metodo-canonico.md` | Profundidade: origem, critérios de triagem, base rates, tripwires, template do relatório HTML. |
| `skills/premortem/evals/evals.json` | Casos de teste de trigger e comportamento. |
| `skills/premortem/README.md` | Resumo por-skill voltado pra humano. |
| `README.md` (raiz) | Porta de entrada do produto. Otimizar pra quem decide sob alto custo de erro. |
| `assets/social-preview.html` | Fonte DS V3.0 do social card do GitHub (1280×640, lima). |
| `page/index.html` | Página-vitrine interativa publicada na Vercel. |

## O que NÃO editar

- Não edite a skill canônica no monorepo privado `mscs-skills` a partir daqui —
  este repo é um espelho publicado. Mudanças de comportamento fluem pelo `skills-sync`.
- Mantenha o frontmatter do SKILL.md (`name`, `description`) intacto — `npx skills`
  e o loader de plugin do Claude fazem parse dele.
- Não fabrique números de eficácia. A prova empírica vem dos papers citados.
- Nunca commite `.env`, tokens ou credenciais.

## Convenções

- Idioma: README/skill em PT-BR; voz Tradutor, frases curtas, voz ativa, zero floreio.
  Sem léxico inflado, sem paralelismo negativo.
- Commits: Conventional Commits. Push só com SHA verificado (local = remote).

## Licença

MIT. Contribuições bem-vindas. Ver CONTRIBUTING.md.
