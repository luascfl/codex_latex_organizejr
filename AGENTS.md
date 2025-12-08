# Repository Guidelines

Use estas notas para manter os artefatos LaTeX da Organize Jr. consistentes e compiláveis em XeLaTeX.

## Project Structure & Module Organization
- `template_organizejr.tex`: modelo XeLaTeX/abnTeX2 com timbrado, margens ABNT e macros de metadados.
- `prompt_mestre_organizejr-latex.txt`: prompt mestre; siga sempre que criar ou ajustar templates.
- `template_organizejr.pdf`: referência visual do layout atual.
- `logo_organizejr.png` e `fonts/`: logotipo e famílias Open Sans, League Spartan e Lexend Deca (usadas via `fontspec`).
- `abntex2-alf-local.bst`: estilo autor-data local; deve ficar ao lado do `.tex`.
- Artefatos `template_organizejr.*`/`test_organizejr.*`: saídas de compilação; não versionar novas.

## Build, Test, and Development Commands
- `latexmk -xelatex template_organizejr.tex`: compila com XeLaTeX e BibTeX usando as fontes locais.
- `latexmk -c template_organizejr.tex`: limpa auxiliares (mantém o PDF).
- Pipeline manual (alternativa): `xelatex template_organizejr.tex && bibtex template_organizejr && xelatex template_organizejr.tex && xelatex template_organizejr.tex`.

## Coding Style & Naming Conventions
- Compile sempre com XeLaTeX; mantenha `fontspec` apontando para `fonts/`.
- Margens ABNT (3 cm sup/esq, 2 cm dir/inf), espaçamento 1,5, recuo 1,25 cm; citações longas em 10 pt com recuo 4 cm.
- Tipografia oficial: títulos/cabeçalhos em League Spartan, corpo em Open Sans, apoio/TOC em Lexend Deca; cores primária `#681582`, apoio `#62F3BC`, texto `#1A1A1A`.
- Use `\autorcite{}` conforme o modelo; não altere a macro nem o `.bst`.
- Inclua `filecontents*` mínimos para `.toc`/`.bib` em novos templates para compilar na primeira passada.

## Testing Guidelines
- Toda alteração em `.tex` deve gerar PDF limpo (sem warnings de fonte ou referência) com `latexmk -xelatex`.
- Compare o PDF gerado com `template_organizejr.pdf` ao ajustar timbrado, margens ou tipografia.
- Se incluir bibliografia, mantenha `abntex2-alf-local` e garanta `.bib` autossuficiente.

## Commit & Pull Request Guidelines
- Mensagens curtas em imperativo (ex.: “Ajusta cabeçalho timbrado”, “Corrige recuo de citação”); agrupe mudanças relacionadas.
- No PR, descreva impacto visual e liste arquivos tocados; anexe o PDF gerado quando alterar layout.
- Não versione tokens ou PDFs temporários; mantenha `fonts/` e `.bst` intactos.

## Agent-Specific Instructions
- Leia `prompt_mestre_organizejr-latex.txt` antes de gerar documentos; siga regras de capa, folha de rosto, sumário, numeração e timbrado em todas as páginas.
- Não substitua ABNT/`abntex2` por outras classes nem remova macros de timbrado, cabeçalho/rodapé ou quebras automáticas de página.
- Se precisar de dados padrão, use UNEB / Organize Jr., Salvador, 2025 e mantenha o timbrado em todas as páginas.
