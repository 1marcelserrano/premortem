# premortem

**Imagine que já falhou. Descubra por quê — antes de gastar dinheiro, tempo ou reputação.**

Uma skill do Claude que roda um *premortem* sobre qualquer decisão de alto custo de erro. Assume que o plano já morreu num futuro próximo e trabalha de trás pra frente pra achar todo motivo que o matou. Um arquivo markdown. Sem servidor, sem dependência, sem estado externo.

[Instalar](#instalar) · [Como funciona](#como-funciona) · [Quando usar](#quando-usar) · [Exemplo](#exemplo) · [FAQ](#faq) · [Página](https://mscreative.systems/arsenal/premortem)

---

Um postmortem investiga por que algo morreu depois que morreu. O premortem faz o oposto: você imagina que já falhou e descobre por quê antes de começar.

O método é do psicólogo **Gary Klein**, publicado na *Harvard Business Review* (2007). **Daniel Kahneman** — Nobel, autor de *Rápido e Devagar* — chamou de sua técnica de decisão mais valiosa. A base cognitiva é mais antiga: Mitchell, Russo e Pennington mostraram em 1989 que imaginar um evento futuro como já ocorrido aumenta em ~30% a capacidade de apontar suas causas. Google, Goldman Sachs e Procter & Gamble usam antes de decisões grandes.

Feito pra quem decide sob alto custo de erro — fundador, criador, estrategista — e precisa ouvir o que não quer ouvir enquanto ainda dá pra mudar de rumo.

## Veja como fica

![Exemplo de premortem com três ameaças reais, um elefante, a premissa oculta e um alerta com data](docs/exemplo-premortem.png)

O exemplo usa dados inventados: o mesmo workshop de R$ 1.500 descrito abaixo. A skill separa as ameaças reais (Tigres) do que só assusta, nomeia o Elefante e fecha com a premissa oculta e um alerta datado.

## O problema

Pergunte a um modelo de IA "esse plano é bom?" e ele vai atrás de razões pra confirmar. Pergunte "o que pode dar errado?" e ele responde cauteloso, genérico, hedge. Os dois caminhos protegem o plano em vez de testá-lo.

O custo aparece depois. A premissa que ninguém checou vira o motivo da falha — e você só descobre quando o dinheiro, o tempo e a reputação que estavam em jogo já foram gastos.

A virada: o premortem troca o tempo verbal. Você não pergunta "o que pode dar errado". Você afirma "isso deu errado" e pede a história. O cérebro entra em modo narrativo e gera motivos específicos, ancorados no plano real — não conselho genérico que serve pra qualquer coisa. Pesquisadores de Wharton e Cornell batizaram isso de **hindsight prospectivo**.

## Como funciona

```mermaid
flowchart LR
    A[Contexto mínimo<br>o quê · pra quem · sucesso<br>horizonte · confiança] --> B[Enquadramento<br>'isso já falhou']
    B --> C[Premortem bruto<br>aritmética + motivos]
    C --> D[Triagem<br>Tigre / Papel / Elefante]
    D --> E[Aprofundamento<br>1 agente por Tigre<br>+ red-team da premissa]
    E --> F[Síntese<br>matriz P×I · base rate<br>plano revisado · tripwires]
```

A skill bate uma barra mínima de contexto, monta o enquadramento explícito "isso já falhou", roda a aritmética do plano (break-evens, metas que se contradizem) e gera todo motivo genuíno de falha. Depois tria cada motivo, vai fundo em cada ameaça real em paralelo, ataca a premissa central com um red-team, e fecha numa síntese com matriz Probabilidade × Impacto, base rate da classe de referência, plano revisado e tripwires datados. Entrega um relatório HTML + a transcrição completa.

| Sem premortem | Com premortem |
|---------------|---------------|
| "Esse plano é bom?" → o modelo acha razões pra dizer sim. Otimismo cordial. | "Isso já falhou, explique como" → o modelo para de justificar e passa a explicar o desmoronamento. |

A triagem separa o que merece energia do que só assusta:

- **Tigre** — ameaça real, com evidência. Ignorar seria negligência. Ganha urgência: Bloqueia-Lançamento, Fast-Follow ou Monitorar.
- **Tigre de Papel** — assusta no papel, mas é improvável ou gerenciável. Registra e segue.
- **Elefante** — o que todo mundo sabe e ninguém fala. Costuma ser gente, política ou ego — e é a causa real de falha com mais frequência do que parece.

## Quando usar

**Use quando:**
- Um produto, feature ou lançamento prestes a sair com dinheiro ou reputação em jogo
- Uma mudança de pricing ou de modelo de negócio
- Uma contratação prestes a acontecer
- Um pivô de estratégia ou posicionamento
- Qualquer compromisso onde errar custa caro e a decisão ainda pode mudar de rumo

**Não use quando:**
- A ideia ainda é vaga, sem plano concreto → planeje primeiro, depois rode o premortem
- A pergunta tem uma resposta certa → só responda
- É feedback de rascunho → isso é edição, não premortem
- A decisão já foi tomada e é irreversível → o premortem só serve enquanto dá pra mudar de rumo

## Exemplo

Brief: *"premortem disso: vou lançar um workshop ao vivo de R$1.500 sobre usar Claude pra times de marketing. 50 vagas. Alvo: gestores de marketing em empresas de 10-50 pessoas."*

O premortem bruto achou 6 motivos de falha. A triagem isolou três Tigres e um Elefante: a aprovação de orçamento que trava a compra, o comprador real que é o solo e não o gestor, a prep de 5 semanas vendida como 2, e a audiência que o criador *quer* ter em vez da que tem.

Síntese: a falha mais provável é o descasamento de audiência. A premissa oculta, do red-team: "gestor de empresa de 10-50" não se identifica assim nem frequenta os mesmos lugares. Base rate de audiência fria: 1-3%. Plano revisado, menor experimento primeiro: rode um piloto de R$197 pra 20 pessoas antes de travar o preço público de R$1.500. Tripwire: se em 7 dias menos de 10 inscritos forem gestores de time, o alvo está errado — pivota.

Passo a passo completo do método em [`skills/premortem/SKILL.md`](./skills/premortem/SKILL.md) e no [método canônico](./skills/premortem/references/metodo-canonico.md).

## Instalar

Uma skill é um conjunto de instruções que ensina o Claude a fazer uma tarefa do jeito certo. Você instala uma vez e depois chama pelo nome. Leva alguns minutos, sem terminal.

**O que você precisa ter:** uma conta no Claude e, nas configurações dele, a opção de executar código e criar arquivos ligada (em inglês, "Code execution and file creation"). O Claude pede isso para aceitar skills enviadas. Se o seu Claude é da empresa, o administrador pode precisar liberar o envio de skills.

**Antes de rodar:** para ancorar os cenários na sua realidade, a skill procura rapidamente arquivos de contexto na pasta onde o Claude está aberto (como o `CLAUDE.md` e pastas de memória) e nos arquivos que você citar. Se a pasta tem material que você não quer que ela leia, abra o Claude em outra pasta. Ela também chama ajudantes em paralelo (subagentes) e grava um relatório em HTML.

1. [Baixe o arquivo premortem.skill](https://github.com/1marcelserrano/premortem/releases/latest/download/premortem.skill).
2. Abra o Claude e entre em Customize, o menu das suas skills.
3. Clique em + Add e escolha enviar uma skill (Upload a skill). Selecione o arquivo baixado. Se o Claude recusar, troque o final do nome de `.skill` para `.zip` e envie de novo.
4. Confira se a chave ao lado de premortem está ligada.
5. Abra uma conversa nova e escreva: "roda um premortem disso".

**O que foi testado:** o envio de um arquivo `.skill` por esse caminho foi feito pelo autor com outras skills dele (Fila de Prioridades e Prompt Chain). O Claude aceitou direto, sem renomear, e a skill já entrou ativada. O premortem.skill 1.0.0 tinha o mesmo defeito medido (descrição com 1400 caracteres), e foi corrigido junto. O envio da versão 1.0.1 ainda não foi conferido. Também falta alguém que não seja o autor seguir só este passo a passo, e ver onde o relatório em HTML aparece para quem usa o Claude no site.

Se o Claude recusar o arquivo com a mensagem de que o campo description deve ter no máximo 1024 caracteres, você baixou a versão 1.0.0. Baixe a 1.0.1 ou mais nova na [página de releases](https://github.com/1marcelserrano/premortem/releases/latest).

<details>
<summary>Para quem já usa o terminal</summary>

```bash
git clone https://github.com/1marcelserrano/premortem.git
cp -r premortem/skills/premortem ~/.claude/skills/
```

Pela CLI de skills: `npx skills add 1marcelserrano/premortem`. Para conferir, abra uma sessão nova e rode `/skills`. A skill premortem deve aparecer.

</details>

## FAQ

**Precisa de API key, conta paga ou servidor?** Não. É um arquivo markdown que o Claude carrega. Roda onde o Claude roda.

**Funciona sem sub-agentes?** Sim. Se o ambiente não tem sub-agentes, a skill roda cada aprofundamento inline, como passos analíticos independentes. O resultado é o mesmo; só a orquestração muda.

**Em que idioma ela trabalha?** Português. O corpo da skill e o relatório saem em pt-BR.

**Ela inventa números pra te assustar?** Não. Toda razão de falha precisa de evidência. Razão sem evidência desce pra Tigre de Papel — é o que separa ameaça real de ansiedade.

**É a mesma coisa que pedir "seja crítico"?** Não. Pedir crítica dispara hedge educado. O enquadramento "isso já morreu, explique como" é o mecanismo — é ele que destrava a identificação honesta de falha.

## Comunidade gratuita

Esta skill é um presente. Se você quer construir skills como a Premortem e conversar com quem está fazendo o mesmo, entre na comunidade gratuita:

**[Entrar na comunidade no Skool](https://www.skool.com/marcel-1662/about)**


---

Uma skill do **[MSCREATIVE.SYSTEMS™](https://fronteirista.substack.com)**. Método: Gary Klein, *Performing a Project Pre-Mortem*, HBR (2007); hindsight prospectivo: Mitchell, Russo & Pennington (1989). Licença MIT — use, modifique, redistribua. Mantenha os créditos.
