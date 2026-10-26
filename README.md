# revisao-adversarial

Uma skill para Claude que separa quem entrega de quem verifica. Antes de dizer "pronto", um revisor que não viu o processo recebe só o pedido original e o resultado, confere cada requisito, escreve testes que tentam quebrar a solução, procura efeitos colaterais e devolve um veredito com evidência: **Aprovado**, **Reprovado** ou **Aprovado com ressalvas**.

## Instalar

**Claude Code (plugin marketplace)**

```
/plugin marketplace add voidsilva/revisao-adversarial
/plugin install revisao-adversarial@voidsilva-skills
```

**Qualquer agente compatível (skills CLI)**

```
npx skills add voidsilva/revisao-adversarial
```

**Manual**: copie a pasta `skills/revisao-adversarial` para `~/.claude/skills/` (ou `.claude/skills/` no seu projeto). No claude.ai, compacte a pasta em .zip e envie em Configurações > Capacidades > Skills.

## Quando ela entra em ação

- Quando você pede para revisar, validar, auditar ou "checar se está pronto".
- Antes de o Claude declarar "pronto", "concluído" ou "feito" em código, documentos ou configuração com requisitos verificáveis.
- Quando a entrega parece boa e você quer uma segunda opinião.

## Formato do relatório

```
## Veredito: [Aprovado | Reprovado | Aprovado com ressalvas]
## Requisitos
## Falhas
## Efeitos colaterais
## Não verificado
```

---

## English

**revisao-adversarial** (adversarial review) is a Claude skill, written in Brazilian Portuguese, that has an independent reviewer check a deliverable before it is called done. The reviewer sees only the original request and the result, maps every verifiable requirement, writes tests that try to break the solution, looks for side effects, and returns a verdict backed by evidence (file and line, test input and output).

Install with `/plugin marketplace add voidsilva/revisao-adversarial` then `/plugin install revisao-adversarial@voidsilva-skills`, or `npx skills add voidsilva/revisao-adversarial`.

## Licença

MIT
