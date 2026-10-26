---
name: revisao-adversarial
description: Revisão independente de uma entrega antes de declará-la concluída. Use sempre que o usuário pedir para revisar, validar, auditar ou "checar se está pronto", e também antes de dizer "pronto", "concluído" ou "feito" em tarefas de código, documentos ou configuração que tenham requisitos verificáveis. Um revisor que não viu o processo confere cada requisito do pedido original, escreve testes que tentam quebrar a solução, procura efeitos colaterais e devolve um veredito com evidência. Acione também quando a entrega parecer boa mas o usuário pedir uma segunda opinião.
compatibility: Requer acesso a leitura do projeto e capacidade de executar testes. Não requer dependências externas.
---

# Revisão adversarial

Esta skill separa quem entrega de quem verifica. Quem fez a tarefa tende a avaliar o próprio trabalho com boa vontade. O revisor, ao contrário, recebe só o pedido original e o resultado, e tem uma tarefa: encontrar motivos para a entrega não estar pronta.

## Entradas

Antes de começar, reúna três coisas:

1. **Pedido original**: o texto exato que o usuário pediu, sem resumo. Se o pedido veio em vários turnos, junte todos.
2. **Entrega**: os arquivos alterados e, se houver, o diff ou a lista de mudanças.
3. **Evidência de execução**: o que foi rodado e com qual resultado, se existir. Use isso como pista, não como prova.

Se o pedido original não estiver disponível, pare e diga isso. Sem ele, a revisão não tem referência.

## Passos

### 1. Quebrar o pedido em requisitos

Liste cada requisito verificável do pedido original, numerado. Um requisito é algo que pode ser confirmado ou negado: "a função aceita vazio", "o arquivo se chama X", "o endpoint retorna 404 para id inexistente". Frases vagas como "deixar melhor" não são requisitos; anote-as como ambíguas.

Não corrija o pedido nem infira o que o usuário "provavelmente" quis. Se algo não estiver claro, registre a ambiguidade no relatório.

### 2. Conferir cada requisito contra a entrega

Para cada requisito, procure evidência no código ou no documento. Classifique em:

- **atendido**: a evidência está no resultado, e você apontou onde.
- **não atendido**: a evidência mostra o contrário ou a ausência.
- **não verificável**: depende de algo que você não consegue checar aqui (um serviço externo, um ambiente).

Não marque "atendido" com base no que a entrega diz sobre si mesma. Leia o código.

### 3. Escrever testes que tentem quebrar

Para cada requisito atendido, pergunte: que entrada faria isto falhar? Escreva o teste. Procure, nesta ordem:

- entradas vazias, nulas, zero, negativas e muito grandes
- valores na fronteira (o primeiro e o último elemento, o limite exato)
- caminhos de erro: o que acontece quando a dependência falha
- concorrência e repetição, quando aplicável
- o mesmo caso rodado duas vezes

Rode os testes. Um teste que falha é evidência forte. Um teste que passa vale pouco por si só, e não deve ser apresentado como prova de que está tudo certo.

Não altere a entrega para fazer um teste passar. Se precisar de uma mudança para testar, faça isso num arquivo temporário e apague depois.

### 4. Procurar efeitos colaterais

Compare o estado antes e depois. Aponte o que mudou além do pedido: arquivos alterados que não deveriam, dependências adicionadas, configurações tocadas, comentários removidos, segredos expostos. Um efeito colateral não é automaticamente um erro, mas precisa ser declarado.

### 5. Emitir o veredito

Dê um dos três vereditos:

- **Aprovado**: todos os requisitos atendidos, nenhum teste falhou, nenhum efeito colateral indevido.
- **Reprovado**: ao menos um requisito não atendido ou um teste falhou. Liste cada falha com o teste que a provou.
- **Aprovado com ressalvas**: requisitos atendidos, mas com ambiguidades, itens não verificáveis ou efeitos colaterais a confirmar.

Cada falha deve trazer evidência concreta: o arquivo e a linha, o teste e a saída. "Parece ter um problema" não serve.

## Formato do relatório

Use esta estrutura, nesta ordem:

```
## Veredito: [Aprovado | Reprovado | Aprovado com ressalvas]

## Requisitos
1. [atendido | não atendido | não verificável | ambíguo] — descrição — evidência
2. ...

## Falhas
- Arquivo:linha — o que está errado — teste que prova (entrada e saída observada)

## Efeitos colaterais
- o que mudou além do pedido

## Não verificado
- o que não foi possível checar e por quê
```

Omita uma seção vazia, exceto "Veredito" e "Requisitos", que sempre aparecem.

## Princípios

- **Evidência antes de opinião.** Cada afirmação aponta para um arquivo, uma linha ou uma saída.
- **Não corrija durante a revisão.** O papel é revisar. Se houver correção a fazer, sugira; quem decide é quem entregou ou o usuário.
- **Ser justo também.** Se a entrega atende ao pedido, diga isso com a mesma clareza com que apontaria um erro. Um revisor que sempre reprova não ajuda.
- **Declarar o que não foi feito.** Um relatório que diz o que não conseguiu verificar é mais útil do que um que parece completo.

## Quando não usar

- Perguntas simples que não têm entrega a conferir.
- Tarefas sem requisitos verificáveis, como escolher um nome ou um tom de texto. Para essas, uma revisão de clareza basta.
