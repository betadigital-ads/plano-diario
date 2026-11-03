# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Projeto

"Home de Rotina Diária" do Cedrick: uma página estática, **um único ficheiro** [index.html](index.html) com `<style>` interno. Não há build, dependências, testes nem linter. Para ver alterações, abrir o ficheiro no browser (a única dependência externa são as Google Fonts: Gloock, Fraunces, Inter). Conteúdo e comentários estão em português (pt-PT); manter assim.

## Regras do projeto (do brief original)

- Apenas HTML + CSS puros. **Sem JavaScript e sem frameworks.** Toda a interatividade tem de ser feita em CSS.
- Estética minimalista premium: espaçamento amplo, linhas finas, sombras suaves, animações leves de hover.
- Tudo deve continuar fácil de editar à mão: manter os comentários de secção e as variáveis CSS.
- O brief original pedia paleta branco/cinza/dourado, mas a página implementada usa uma **paleta verde** (`#051F20 → #DAF1DE`, referência em `palete_planner.jpg`). `design.jpg`, `H1.png` e `H2.png` são referências visuais. Seguir a paleta verde atual, não o dourado do brief.

## Arquitetura de [index.html](index.html)

- **CSS (linhas ~12-420), dividido em blocos numerados** (`1. VARIÁVEIS`, … `13. POP-UP`, `14. ANIMAÇÕES`). Cores, fontes, raio e espaçamentos vivem em `:root`; nunca fixar cores nas regras.
- **Modo claro/escuro sem JS:** um `<input type="checkbox" id="tema">` no topo do `.container` + `html:has(#tema:checked)` que redefine as variáveis `:root`. O `<label for="tema">` no header é o interruptor. Qualquer cor nova tem de existir nos dois temas, via variável.
- **Pop-ups dos módulos com `:target`:** cada `<li>` de módulo liga a `#mod-c1…c5` (Claude) ou `#mod-t1…t5` (Tráfego); os `.modal` correspondentes estão no fim do `<main>` e abrem/fecham via `:target`. Fechar volta a `#cursos`. Ao adicionar um módulo, criar o `<li>` **e** o `.modal` com o `id` correspondente.
- **Barras de progresso:** `.bar > span` usa a custom property inline `--value` (ex.: `style="--value:30%"`). Atualizar o `<strong>` de percentagem e o `aria-valuenow` em conjunto. Existem barras na secção "Cursos em andamento" e na "Progresso dos Cursos" — manter os valores consistentes.
- **Animações de scroll** usam `animation-timeline: view()` dentro de `@supports`, com fallback estático; `prefers-reduced-motion` desliga tudo.
- **Secções do `<main>`, por ordem:** Prioridade Máxima, Metas do Dia (checkboxes estilizados com `.check`/`.box`), Cursos em andamento, Progresso dos Cursos, Mini Dashboard, Rotina Manhã/Noite, Hábitos essenciais, Motivação diária (frase e autor trocados manualmente no comentário indicado), Vitórias do Dia, e o footer.
- Breakpoints responsivos: `900px` e `680px`.

## Git

Repositório privado: https://github.com/betadigital-ads/planner (branch `main`, tag `v0.1.0` = backup da versão inicial).

- Fazer commit de **cada alteração** com mensagem clara, e `git push` regularmente. O objetivo é poder reverter se algo correr mal.
- Criar uma tag anotada (`vX.Y.Z`) em marcos importantes.
- A identidade git está definida apenas localmente neste repo (Cedrick / cebeta44@gmail.com).
- O `gh` não está no PATH do PowerShell; usar `& "C:\Program Files\GitHub CLI\gh.exe"`.
