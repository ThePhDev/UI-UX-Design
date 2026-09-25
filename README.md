<div align="center">

# 🎨 PH_Design_Skill

**O padrão de design do PH para o Claude Code.**
Qualquer interface, com ou sem referência: medida pixel a pixel, pensada para celular desde o início, com animação caprichada e revisada por um gauntlet de 7 portões antes de chegar em você com link de preview.

`v1.0.0` · Claude Code skill · Python + Playwright

</div>

---

## ✨ O que ela faz

A skill é carregada sozinha em **qualquer tarefa com interface**: sites, landing pages, portfólios, web apps, telas de app, PWAs, dashboards, apps de estudo, componentes soltos e até "deixa esse botão mais bonito". Ela entra antes da primeira linha de código.

| | Com imagem de referência | Sem referência |
|---|---|---|
| **Começo** | Lê a imagem como uma especificação: cores em hex, grid, espaçamentos, tipografia, raios, sombras | Define a direção: público, clima, paleta, fontes e uma ideia assinatura |
| **Construção** | Copia na largura exata da referência | Desktop e mobile desenhados juntos |
| **Prova** | Comparação pixel a pixel até **≥ 97 %** de igualdade | Crítico confere se o resultado segue a direção |
| **Depois** | Mobile → Motion → Textos → Gauntlet → Link de preview | Mobile → Motion → Textos → Gauntlet → Link de preview |

## 🧭 Como funciona

```
imagem? ──sim──► spec.md ─► clone estático ─► loop de medição (print → diff → corrige a pior região) ─┐
   │                                                                                                  │
   └──não──► direction.md ─► desktop + mobile juntos ─────────────────────────────────────────────────┤
                                                                                                      ▼
                         mobile caprichado ─► motion (padrão Emil) ─► textos (humanizer) ─► GAUNTLET ─► link + prints
                                                                                               ▲   │
                                                                                               └───┘ falhou? corrige e recomeça do portão 1
```

### 🔤 Tipografia
- Identifica a fonte real (WhatTheFont, Matcherator) e procura **primeiro no [dafont](https://www.dafont.com/pt/)**, conferindo a licença. Depois vai para a fundição, o Fontshare ou o Font Squirrel. **Google Fonts só como reserva.**
- Com referência, testa 2 ou 3 fontes candidatas e fica com a que tiver a menor diferença pixel a pixel.
- Confere se a fonte tem acentos e símbolos (Ω, Δ, Σ). Usa uma família por papel e hospeda os arquivos no projeto.

### 📱 Mobile com o mesmo cuidado do PC
- O celular é planejado **antes** do código, mesmo quando a referência só mostra o desktop.
- Prints em 5 tamanhos (1440, 1280, 768, 390 e 360) com auditoria automática: rolagem lateral, texto abaixo de 12px, alvos de toque pequenos, imagens sem `alt` e erros de console.
- Apps ganham cara de nativo: áreas seguras, `100dvh`, sem flash ao tocar, inputs que não dão zoom.

### 🎬 Motion no padrão Emil Kowalski
| Superfície | Orçamento de movimento |
|---|---|
| Hero, seções, primeira carga | **Expressivo**: coreografia, scroll, WebGL, cursor |
| Botões, menus, abas, formulários | **Rápido e sutil**: 150–250 ms, interrompível |
| Ações repetidas ou de teclado | Nenhum ou instantâneo |

- Consulta primeiro o **catálogo React Bits** com 217 componentes animados ([`react-bits-catalog.md`](react-bits-catalog.md)). Também adapta para sites sem React.
- Anima só transform, opacity e filter. Respeita `prefers-reduced-motion` e termina com `review-animations`.

### 🥊 Gauntlet de 7 portões ([`gauntlet.md`](gauntlet.md))
| # | Portão | Passa quando |
|---|---|---|
| 1 | Fidelidade | diff ≥ 97 %, deslocamento vertical ≤ 8px, nenhuma célula > 10 % |
| 2 | Detalhes pixel a pixel | crítico compara zooms 2x: peso da fonte, raios, bordas, sombras, ícones |
| 3 | Responsivo | `shoot.py` em 5 tamanhos sem nenhum problema |
| 4 | Motion | `review-animations` aprova, dentro do orçamento, sem layout shift |
| 5 | Design humano | nenhum sinal de template de IA |
| 6 | Texto humano | passou pelo humanizer, sem frases prontas |
| 7 | Qualidade | contraste AA, foco visível, semântica, teclado, sem rolagem lateral |

Um round só vale se **todos** passarem juntos. Os portões 2, 5 e 7 são julgados por agentes críticos independentes. O limite é de 8 rounds.

### 🔗 Entrega
Build → túnel do Cloudflare → você recebe o **link público** e os prints de desktop e mobile, e também o % de igualdade quando tem referência.

## 🛠️ Ferramentas

| Script | O que faz |
|---|---|
| `scripts/palette.py` | Tamanho, cores dominantes em hex, cor exata de um ponto, zoom de regiões e extração de logos e fotos |
| `scripts/shoot.py` | Prints estáveis (espera as animações e o GSAP terminarem) em qualquer tamanho, mais a auditoria de responsividade |
| `scripts/diff.py` | Porcentagem de igualdade, deslocamento de altura, piores regiões, mapa de calor e comparação lado a lado |
| `scripts/publish.py` | Publica uma pasta ou porta num link `trycloudflare.com` e confere se o link responde |

```bash
python scripts/palette.py ref.png --at 120,40 --crop 0,0,600,300 zoom.png
python scripts/shoot.py http://localhost:5173 qa --viewports 1920x1080,mobile --no-scroll
python scripts/diff.py ref.png qa/1920x1080.png qa/round1 --exclude 900,100,1400,600
python scripts/publish.py dist        # publica
python scripts/publish.py stop        # derruba os túneis
```

## 📦 Instalação

```bash
git clone https://github.com/ThePhDev/PH_Design_Skill ~/.claude/skills/ph-design-skill
pip install playwright numpy pillow && python -m playwright install chromium
# cloudflared no PATH (ou em ~/bin) para o link de preview
```

**Skills que ela usa como apoio:**
```bash
npx skills add emilkowalski/skills -s emil-design-eng animate animation-vocabulary apple-design find-animation-opportunities improve-animations mobile-native pick-ui-library prototype review-animations -g -a claude-code -y
npx skills add pbakaus/impeccable -g -a claude-code -y
npx skills add https://github.com/anthropics/skills --skill frontend-design -g -a claude-code -y
```
Também usa `humanizer` para os textos e, opcionalmente, `web-design-guidelines` no portão 7.

## 🗂️ Estrutura
```
ph-design-skill/
├── SKILL.md               # a skill (o que o Claude lê)
├── gauntlet.md            # os 7 portões
├── react-bits-catalog.md  # 217 componentes animados, por categoria
├── scripts/               # palette · shoot · diff · publish
├── CHANGELOG.md
└── README.md
```

## 🛟 Versões e backup
Cada versão estável ganha uma **tag** e uma **release** com o `.zip` da skill. Para voltar a uma versão segura:
```bash
cd ~/.claude/skills/ph-design-skill
git fetch --tags && git checkout v1.0.0     # só para olhar
git reset --hard v1.0.0                     # para voltar de vez
```

## 🙏 Créditos
- [Emil Kowalski / skills](https://github.com/emilkowalski/skills): a filosofia de motion e de polimento
- [React Bits](https://github.com/DavidHDev/react-bits): o catálogo de componentes animados
- [Impeccable](https://github.com/pbakaus/impeccable) e o [frontend-design](https://github.com/anthropics/skills) da Anthropic: direção estética
