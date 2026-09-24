# Locales da rede EXE

Todo texto que o jogador vê sai daqui. Plugin nenhum crava texto no código nem no `config.yml`.

## Onde fica cada chave

A chave `plugins.<namespace>.…` vive em `pt_br.lang/<bundle>/<namespace>.jsonc`, ou em
`pt_br.lang/<bundle>/<namespace>/<assunto>.jsonc` quando o namespace é grande (`core`, `essentials`,
`lobby`). Cada arquivo guarda um namespace só.

- `global/`: o que vale em todos os servidores.
- `p4free/`: o que só existe no P4Free.

Uma chave existe num lugar só, inclusive entre `global/` e `p4free/`. Comentário `//` pode; vírgula
sobrando antes de `}` não.

## Como mudar um texto

Edite o `.jsonc` em `pt_br.lang/` e faça push no `main`. Não há build nem `dist/`: em até 1 minuto a
plataforma baixa as fontes, monta os bundles e avisa os servidores pelo Echo, sem reiniciar nada.
Para ser na hora, `/admin reload --content` em jogo: ele diz se o locale e os menus mudaram. Menus
abertos, hologramas e a espada e o machado do P4Free se redesenham sozinhos; o título de um menu
aberto só muda quando ele é reaberto.

Se um arquivo fugir da regra (namespace trocado, chave repetida, texto com quebra de linha, JSONC
inválido), a plataforma recusa a versão inteira, o jogo continua com a anterior e o motivo aparece no
painel como "Conteúdo recusado: lang".

## Bundles

O servidor recebe o `global` mais a pasta do seu `serverId` (`p4free`); sem pasta própria (`auth`,
`lobby`, `proxy`), recebe só o `global`. Quem monta é o `LocaleBundles`, no core do monorepo.

## Auditoria

`node audit-code-keys.mjs <caminho do monorepo exe>` lista as chaves que o código pede e não
existem aqui, e os namespaces daqui que nenhum código cita (texto de plugin que não existe mais).
