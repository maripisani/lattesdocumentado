# Montador de Anexos do Currículo Lattes

Ferramenta web (100% client-side, sem servidor) para montar automaticamente o PDF de comprovação exigido em processos seletivos acadêmicos (mestrado, doutorado, bolsas, concursos): **Currículo Lattes + certificados comprobatórios**, na ordem exata definida pela planilha de pontuação do processo, com cada anexo numerado.

Nenhum arquivo é enviado a servidores externos — tudo é processado localmente no navegador do usuário, usando [SheetJS](https://sheetjs.com/) (leitura de `.xlsx`) e [pdf-lib](https://pdf-lib.js.org/) (montagem do PDF).

## O problema que resolve

Muitos programas de pós-graduação exigem que o candidato:

1. Preencha uma planilha de pontuação, indicando em uma coluna **ANEXO** o código de cada documento comprobatório (ex.: `2.4-1, 2.4-2`);
2. Anexe, ao final do PDF do Currículo Lattes, cada certificado correspondente, numerado e na mesma sequência do formulário.

Fazer isso manualmente é repetitivo e sujeito a erro de ordem/numeração. Esta ferramenta automatiza o processo.

## Como usar

1. Abra o arquivo `montador-anexos-lattes.html` em qualquer navegador (Chrome, Edge, Firefox).
2. **Passo 1** — envie a planilha de pontuação (`.xlsx`). O app localiza automaticamente a coluna `ANEXO` e extrai todos os códigos exigidos, agrupados por seção do formulário.
3. **Passo 2** — envie o PDF do Currículo Lattes (exportado da Plataforma Lattes).
4. **Passo 3** — anexe um PDF para cada código exigido no checklist. Cada item mostra uma dica do tipo de comprovante aceito, extraída da aba de regras da própria planilha (quando existir).
5. **Passo 4** — clique em "Gerar PDF final". O app monta um único PDF: Currículo Lattes → sumário dos anexos → certificados na ordem do formulário, com o código do anexo carimbado no topo de cada documento.
6. Baixe o PDF final e revise antes de entregar.

## Compatibilidade com outras planilhas

O parser é genérico: procura, em qualquer aba, por uma linha de cabeçalho contendo a célula `ANEXO`, e por uma aba de regras cujo nome contenha "regra", "instru" ou "orienta". Funciona com formulários de pontuação de outros programas de pós-graduação que sigam estrutura semelhante (coluna de descrição da atividade + coluna de anexo com códigos separados por vírgula).

## Estrutura do repositório

```
montador-anexos-lattes.html   # aplicação completa (HTML + CSS + JS em arquivo único)
README.md                     # este arquivo
```

## Tecnologias

- [SheetJS (xlsx)](https://cdnjs.com/libraries/xlsx) — leitura de planilhas Excel no navegador
- [pdf-lib](https://cdnjs.com/libraries/pdf-lib) — leitura, criação e mesclagem de PDFs no navegador

## Limitações conhecidas

- A validação do tipo de certificado é apenas informativa (mostra a regra da planilha como dica) — não há verificação automática de conteúdo do PDF anexado.
- Certificados protegidos por senha não podem ser processados.

## Licença

MIT
