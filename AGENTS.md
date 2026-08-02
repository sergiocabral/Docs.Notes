# Instruções para agentes de inteligência artificial

## Objetivo

Este é um modelo de coleções de notas em AsciiDoc com três usos:

- componente importável por outro site Antora;
- site Antora executável localmente;
- geração de HTML, PDF e EPUB para arquivamento.

Uma coleção de notas não precisa formar um livro nem possuir uma leitura linear. Priorize conteúdo, caminhos previsíveis e pouca infraestrutura. Leia `README.adoc` antes de agir e preserve alterações preexistentes do usuário.

## Fontes de verdade

- `modules/`: conteúdo reconhecido pelo Antora.
- `modules/ROOT/pages/index.adoc`: apresentação geral do repositório.
- `modules/ROOT/assets/`: recursos e capas compartilhados.
- `modules/<módulo>/pages/index.adoc`: apresentação da coleção.
- `modules/<módulo>/nav.adoc`: navegação Antora da coleção.
- `antora.yml`: componente, página inicial e módulos de navegação.
- `antora-playbook.yml`: execução local do site.
- `asciidoctor/publication.yml`: autor, títulos, slugs, idiomas e coleções exportadas.
- `asciidoctor/contents/<módulo>.adoc`: ordem do HTML, PDF e EPUB de cada coleção.
- `asciidoctor/support/`: infraestrutura compartilhada dos formatos consolidados.

Não coloque identidade editorial no `Rakefile`, em `package.json` ou em `asciidoctor/support`.

## Criar outro repositório de notas

Ao substituir o conteúdo deste modelo:

1. Atualize `README.adoc` e `modules/ROOT/pages/index.adoc`.
2. Substitua os módulos `my-notes` e `other-notes` pelas coleções reais.
3. Atualize `antora.yml`, `antora-playbook.yml` e `asciidoctor/publication.yml`.
4. Crie um `asciidoctor/contents/<módulo>.adoc` para cada coleção exportada.
5. Substitua as capas somente quando os arquivos consolidados precisarem de outra identidade visual.
6. Remova todas as referências, títulos e slugs do exemplo.
7. Execute Antora e Asciidoctor antes de considerar o trabalho concluído.

O diretório em `modules/`, a chave em `publication.yml`, o arquivo em `asciidoctor/contents/` e a entrada em `antora.yml` devem usar o mesmo nome de módulo. O campo `lang`, como `pt-BR`, seleciona o perfil de idioma e é independente desse nome.

Edite arquivos de infraestrutura somente quando a solicitação tratar da forma de executar ou publicar o projeto.

## Conteúdo e navegação

Antes de criar ou atualizar conteúdo preparado para busca ou conversa com
inteligência artificial, leia integralmente
[AGENTS-RAG.md](AGENTS-RAG.md). Esse arquivo define a pasta `rag/`, os corpora,
as coordenadas de origem, o chunking, os resumos e a geração determinística
compartilhada com as demais famílias `Docs.*`.

Use slugs ASCII minúsculos. Quando houver uma ordem editorial útil, prefixe nomes com números e deixe intervalos para inserções.

O primeiro item de cada `nav.adoc` deve ligar diretamente ao `index.adoc` do módulo. Organize as demais páginas abaixo dele. Não liste centenas de registros na navegação lateral quando índices intermediários forem mais legíveis.

Sempre atualize `nav.adoc` e `asciidoctor/contents/<módulo>.adoc` ao adicionar, remover, renomear ou reordenar páginas.

## Recursos e capas

Use `modules/ROOT/assets/images/` para recursos compartilhados e `modules/<módulo>/assets/images/` para imagens exclusivas de uma coleção. Valide as referências no Antora e nos formatos gerados pelo Rake.

Preserve a função destes arquivos:

- `cover-complete.png`: capa pronta do PDF e do EPUB;
- `cover-background.png`: página de título do PDF;
- `cover-banner.png`: apresentação inicial do HTML.

## Infraestrutura

- Preserve `:doctype: book`; é o tipo técnico dos arquivos consolidados.
- Mantenha `asciidoctor/support` reutilizável entre repositórios.
- Mantenha `package.json` genérico; versões editoriais são tags Git.
- Não versione `build/` nem `node_modules/`.
- Atualize lockfiles somente junto com mudanças de dependências.
- Não acrescente bibliotecas, serviços, temas ou automações sem necessidade explícita.
- Não crie commits, tags, releases ou pushes sem autorização explícita.

## Validação

Execute:

```shell
npm exec -- antora antora-playbook.yml
bundle exec rake
```

Confirme:

- ausência de referências, inclusões ou imagens quebradas;
- HTML, PDF e EPUB para todas as coleções;
- ordem definida em `asciidoctor/contents/<módulo>.adoc`;
- rótulos no idioma selecionado;
- somente mudanças intencionais no `git status`.

## Releases

O workflow `.github/workflows/release.yml` responde a tags anotadas `vX.Y.Z` e publica os formatos gerados. Não crie ou envie tags sem autorização. Depois de publicada, não mova, apague ou reutilize uma tag.
