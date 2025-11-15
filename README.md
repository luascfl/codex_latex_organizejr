# Papel Timbrado OrganizeJr. 2025 – Prompt Guide

Este repositório guarda o PDF de referência, o logotipo e as fontes oficiais usados no papel timbrado da Organize Jr. 2025. A ideia é usar esses insumos para construir prompts consistentes para IAs gerarem **código LaTeX completo** que, por sua vez, produz o PDF do timbrado já com o conteúdo da carta ou documento.

## Arquivos disponíveis

- `Papel Timbrado OrganizeJr. 2025.pdf` – base visual do layout (margens, posicionamento de logotipo e bloco de rodapé).
- `logo_organizejr.png` – logotipo em alta resolução para ser inserido via `\includegraphics`.
- `Lexend_Deca.zip` e `League_Spartan.zip` – famílias tipográficas oficiais (Google Fonts + OFL).
- `.gitignore` – impede versionar tokens locais.
- `create_and_push_repo.sh` – utilitário local para automatizar push (fica fora do versionamento remoto).

## Como estruturar o prompt para IA

1. **Defina o objetivo**: “Gerar um documento LaTeX que compile em PDF replicando o papel timbrado 2025 da Organize Jr. já com o conteúdo abaixo”.
2. **Descreva o layout**:
   - Página A4, margens superiores e inferiores iguais às do PDF (aprox. 2.5 cm).  
   - Logotipo alinhado à esquerda no topo; texto do cabeçalho à direita com fontes em caixa alta.
   - Rodapé com endereço e contatos, em uma faixa inferior com a mesma tipografia do PDF.
3. **Especifique tipografia**:
   - Títulos/elementos institucionais com `League Spartan`.
   - Corpo do texto com `Lexend Deca`.
   - Caso a IA não consiga usar fontes externas, peça fallback para `sans-serif` mas mantenha espaçamento semelhante.
4. **Inclua o conteúdo dinâmico**: corpo do ofício, data, assinatura, anexos etc.
5. **Consistência visual**:
   - Mencione que as cores devem seguir o logotipo (extraia os hex codes a partir de `logo_organizejr.png` se necessário, ex.: `#0B3B60` para o azul predominante).
   - Reforçe o alinhamento central do rodapé (“R. Silveira Martins…”) e mantenha letras maiúsculas.
6. **Macros utilitárias (opcional)**: se precisar de comandos como `\autorcite`, deixe claro que devem ser declarados com o número de argumentos, por exemplo `\newcommand{\autorcite}[1]{(\citeauthoronline{#1}, \citeyear{#1})}`. Isso evita o erro `Illegal parameter number`.

## Template de prompt

```text
Quero que você aja como um especialista em LaTeX focado em identidades visuais.
Gere um arquivo completo que compile com pdfLaTeX e replique o papel timbrado 2025 da Organize Jr.

Requisitos obrigatórios:
- Formato A4 com margens de ~2.5 cm.
- Logotipo `logo_organizejr.png` posicionado no canto superior esquerdo com largura de 4 cm.
- Cabeçalho com a frase “ORGANIZE JR.” usando League Spartan em caixa alta, alinhado à direita do logo.
- Rodapé centralizado com o texto:
  “R. Silveira Martins, 2555 – Departamento de Educação (DEDC I), Cabula, Salvador – BA,
   CEP 41150-000 | @organizejr | presidencia@organizejr.com”
- Corpo do ofício em Lexend Deca 11 pt, espaçamento 1.15.
- Cor principal: azul `#0B3B60`; textos do corpo em preto `#111111`.

Conteúdo que deve aparecer no corpo:
[COLE AQUI O TEXTO DA CARTA/OFÍCIO, DATA, ASSINATURA, CARGO ETC.]

Caso use citação automática, inclua exatamente o comando abaixo (observe o `[1]`):

```
\newcommand{\autorcite}[1]{(\citeauthoronline{#1}, \citeyear{#1})}
```

Entregue apenas o código LaTeX final dentro de ```latex ... ``` incluindo preâmbulo, uso dos pacotes necessários
(`geometry`, `xcolor`, `graphicx`, `fontspec` ou `helvet` caso o LaTeX escolhido suporte XeLaTeX/LuaLaTeX).
```

Adapte os itens em maiúsculo antes de enviar para a IA (por exemplo, substitua `[COLE AQUI...]`).

## Preparando o ambiente local

1. Instale as fontes (Linux exemplo):
   ```bash
   unzip Lexend_Deca.zip -d fonts/Lexend_Deca
   unzip League_Spartan.zip -d fonts/League_Spartan
   mkdir -p ~/.local/share/fonts/OrganizeJr
   cp fonts/Lexend_Deca/static/*.ttf ~/.local/share/fonts/OrganizeJr/
   cp fonts/League_Spartan/static/*.ttf ~/.local/share/fonts/OrganizeJr/
   fc-cache -fv ~/.local/share/fonts/OrganizeJr
   ```
2. Com as fontes instaladas, compile o `.tex` com `xelatex` ou `lualatex` para garantir suporte às famílias.
3. Compare o PDF gerado com `Papel Timbrado OrganizeJr. 2025.pdf` para validar espaçamentos.

## Roteiro rápido para automatizar o push

```bash
export GITHUB_TOKEN="seu_token_pat"
./create_and_push_repo.sh
```

O script força o branch `main`, cria (ou reutiliza) `luascfl/codex_latex_organizejr` e faz o push ignorando tokens. Use somente se estiver confortável com esse fluxo automatizado.

## Ideias futuras

- Adicionar um `.tex` canônico do timbrado pronto para importação em prompts.
- Publicar exemplos de prompts + respostas bem-sucedidas.
- Documentar a paleta oficial (hex + CMYK) e disponibilizar arquivos vetoriais extras (.svg).
