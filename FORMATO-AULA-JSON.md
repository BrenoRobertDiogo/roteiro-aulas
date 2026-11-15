# Formato JSON das aulas (app Roteiro das Aulas)

Quando o professor pedir a aula **para o app**, entregue **somente um bloco de código JSON** neste formato. Ele copia, abre o app no celular, toca em **Importar aula** e cola. A aula fica salva no aparelho.

Este formato vale para a entrega ao app e tem prioridade sobre a seção "Como entregar o plano" do contexto, que descreve mensagens de WhatsApp. Todo o resto do contexto continua valendo: vida primeiro e texto depois, perguntas de posição ou de exemplo, pouco conteúdo e muita conversa, só quadro, revista e Bíblia. O professor dispensou "se apertar" e "reserva".

## Modelo

```json
{
  "app": "roteiro-aulas",
  "v": 1,
  "aulas": [
    {
      "chave": "romanos-03-2026-11-15",
      "title": "Todos pecaram",
      "subtitle": "Romanos 3:9-26",
      "date": "2026-11-15",
      "book": "Romanos",
      "sections": [
        {
          "label": "Abertura",
          "title": "Uma nota que ninguém alcança",
          "start": 0,
          "end": 10,
          "blocks": [
            {
              "type": "say",
              "text": "Imagine uma prova em que a nota de corte é 100. Ninguém da sala tira 100."
            },
            {
              "type": "ask",
              "text": "Quem concorda que existe uma nota de corte que a gente não alcança sozinho? Me dá um exemplo do dia a dia."
            },
            {
              "type": "board",
              "text": "NOTA DE CORTE: 100\n(escrever o que a turma disser)"
            }
          ]
        },
        {
          "label": "1",
          "title": "Todos ficam aquém",
          "start": 10,
          "end": 30,
          "blocks": [
            {
              "type": "ask",
              "text": "Quem acha que as pessoas boas não precisam de ajuda de Deus? Por quê?"
            },
            {
              "type": "read",
              "ref": "Rm 3:23"
            },
            {
              "type": "steps",
              "items": [
                {
                  "t": "O texto não deixa ninguém de fora",
                  "s": "Compare com o quadro. Veja também Rm 6:23."
                }
              ]
            },
            {
              "type": "manga",
              "text": "Ideia extra, um item por linha"
            },
            {
              "type": "avoid",
              "text": "Cuidado a tomar, um item por linha"
            }
          ]
        },
        {
          "label": "Fechar",
          "title": "Silêncio e oração",
          "start": 30,
          "end": 40,
          "blocks": [
            {
              "type": "board",
              "text": "RESUMO DA AULA"
            },
            {
              "type": "steps",
              "items": [
                {
                  "t": "Um minuto de silêncio",
                  "s": "Pergunta para levar para a semana"
                },
                {
                  "t": "Oração",
                  "s": ""
                }
              ]
            }
          ]
        }
      ],
      "verses": [
        {
          "ref": "Rm 3:23",
          "text": "Porque todos pecaram e destituídos estão da glória de Deus;",
          "must": true
        },
        {
          "ref": "Rm 6:23",
          "text": "",
          "must": false
        }
      ]
    }
  ]
}
```

## Regras

1. Tipos de bloco aceitos: ask, board, say, read, steps, manga, avoid, note. Outros tipos são ignorados.
2. label é o nome curto da aba (até 12 caracteres): Abertura, 1, 2, Fechar. start e end são minutos desde o início da aula.
3. ask: pergunta de posição ("quem concorda?") ou de exemplo ("me dá uma situação em que..."). Nunca peça para achar a resposta no texto.
4. board: texto puro do que escrever no quadro, em blocos simples (colunas, linha do tempo). Use \n para quebrar linha.
5. read: só a referência do versículo curto para ler em voz alta. O texto vem de verses.
6. steps: o que dizer depois que a turma reagir. t é o ponto, s é o detalhe. Cada ponto deve se apoiar na Bíblia, citando o versículo.
7. Referências como "Rm 3:23" ou "Romanos 3:23-24" viram toque na tela. Escreva sempre com o livro.
8. verses: um item para cada versículo citado. Use somente o texto real da Bíblia usada pela turma. Se não tiver certeza do texto, deixe "text": "" (o app mostra "abra na sua Bíblia"). Nunca invente texto bíblico. must: true marca os indispensáveis (ficam em vermelho).
9. chave: identificador fixo da aula. Importar de novo com a mesma chave pergunta se quer substituir a aula.
10. date no formato AAAA-MM-DD. Não use "se apertar" nem "reserva": o professor dispensa essas partes.

## Campos

| Nível | Campo | Obrigatório | Observação |
|---|---|---|---|
| aula | `title` | sim | Título da aula |
| aula | `sections` | sim | Lista de telas, na ordem em que a aula acontece |
| aula | `subtitle`, `date`, `book`, `chave` | não | `book` permite referências sem livro (ex.: `3:23`) |
| aula | `verses` | não, mas recomendado | Versículos citados, com texto |
| tela | `label` | sim | Nome curto da aba |
| tela | `title`, `start`, `end` | não | `start` e `end` ligam a tela ao relógio da aula |
| tela | `blocks` | sim | Lista de blocos |
| bloco | `type` | sim | `ask`, `board`, `say`, `read`, `steps`, `manga`, `avoid`, `note` |
| bloco | `text` | conforme o tipo | Texto do bloco. Em `manga` e `avoid`, um item por linha |
| bloco `read` | `ref` | sim | Referência do versículo |
| bloco `steps` | `items` | sim | Lista de `{ "t": "ponto", "s": "detalhe" }` |

## Cuidados

- Responda só com o JSON, sem texto antes ou depois, para o professor copiar de uma vez.
- Todo versículo citado em `read` ou dentro dos textos precisa ter um item em `verses`. Sem texto confirmado, deixe `"text": ""`.
- Ao revisar uma aula já importada, mantenha a mesma `chave`: o app oferece substituir.
