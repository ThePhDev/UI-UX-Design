# Changelog

## v1.5.0 — 2026-09-25
- **Prompt kit reescrito** (`prompt-kit.md`): as telas geradas agora parecem um print final de Figma/Dribbble, e toda foto vira um bloco em branco com legenda do que vai ali (o gerador não inventa mais o lugar). Paleta e tipografia próprias, fugindo do padrão de IA (dafont e fundições criativas primeiro), faixas de cor por seção com a transição descrita, ilustração vetorial com luz e profundidade mais objetos em 3D. Notas para geradores mais criativos (Midjourney v7, Ideogram 3, Recraft v3).
- **Prompt pack é obrigatório e bloqueante**: pesquisar o negócio, mandar os prompts e esperar a resposta antes de qualquer código, mesmo quando o cliente já tem fotos.
- **Conteúdo, espaço e fluxo de seções** (SKILL.md): todo fato do negócio tem lugar, mas a superfície é mínima e o resto fica atrás de interação (hotspots, cards que expandem, acordeões, sheets animados); 160–240px entre seções; cor de fundo que transiciona entre as seções no scroll.
- **Padrão de ilustração e SVG**: camadas, uma direção de luz, gradientes, sombra suave, profundidade, alguns elementos em 3D (three.js ou CSS 3D) e loop contínuo tipo GIF em toda ilustração, pausado fora da tela e parado com reduced motion.
- Gauntlet: portões 4 e 5 passam a cobrar essas regras.

## v1.4.1 — 2026-09-25
- `motion-craft.md` §4: efeitos assinatura para páginas Experiência/Persuadir: dither, renderização ASCII, malha 3D que dobra (three.js TSL + GSAP, verso com UV invertido), distorção por cursor e transições de página com View Transitions API. Com orçamento de 60fps no celular e fallback estático.

## v1.4.0 — 2026-09-25
- `motion-craft.md`: repertório de motion de nível Dribbble (uma forma só com morph, molas, bordas líquidas, manipulação direta, trocas com blur, ritmo, regras de engenharia seek-safe) + brief melhorado para reels de UI com HyperFrames.
- `scripts/motion/springs.js`: molas de forma fechada (duration/bounce), `retarget`, `liquidEdges`, `rubberBand`, `dragThenRelease`, `swap`, `beat`, `LiveSpring`. Testado numericamente e num demo real (`demo.html`).

## v1.3.0 — 2026-09-25
- **Gerador de prompts** (`prompt-kit.md`): em projetos sem referência, a skill entrega primeiro um conceito em 5 linhas e os prompts para gerar as telas de desktop, mobile e app no estilo minimalista criativo feito por humanos. O usuário gera as imagens e a skill clona (Path A), ou manda construir direto.
- **DNA de estilo** tirado de 7 referências estudadas (Wandor, Mugic, ShipSphere, FNJ, Finley, Odella, Oriel), salvas em `references/creative-minimal/` para servir de referência de estilo nos geradores de imagem.

## v1.2.0 — 2026-09-25
- **Júri Awwwards (portão 8):** 5 jurados independentes, com Design 40 % / Usabilidade 30 % / Criatividade 20 % / Conteúdo 10 % e o voto mais distante da média descartado em cada critério. Passa com ≥ 8,0 (nível SOTD) e nenhum critério abaixo de 7.
- **`vitals.py`:** LCP, CLS, TBT, tempo de carga e peso, no desktop e num celular com a CPU e a rede limitadas. Entrou no portão 7.
- **Técnicas do Impeccable:** 4 modos por tela, piso de artesanato (Verificar / Recusar, superfícies do navegador tematizadas), `impeccable detect` no portão 5 e nota de Nielsen ≥ 32/40 no portão 7.
- A inspeção agora é feita em lote (um render para todos os checks do portão).

## v1.1.0 — 2026-09-25
- A tasteskill original (`design-taste-frontend`) foi recuperada dos registros e incorporada como `taste-reference.md`: Design Read, 3 dials (8/10/4), diretriz cinematográfica (GSAP, cursor SVG animado, todo SVG animado), design systems oficiais, protocolo de redesign, AI tells e proibição do travessão.
- O gauntlet ganhou o método do Gauntlet Loop: contrato de aceite, construtor e crítico separados, A/B cego, registro de problemas com severidade e regras de parada PASS / UNVERIFIED / NEEDS WORK.
- Nova rota para redesign de sites que já existem.

## v1.0.0 — 2026-09-25
Primeira versão estável ("safe").
- Uma única skill para qualquer interface, com dois caminhos: com referência (clone pixel a pixel) e sem referência (direção visual).
- Gauntlet de 7 portões com restart e críticos independentes.
- Regras de tipografia (dafont primeiro, licença, cobertura de glifos) e de mobile com o mesmo cuidado do PC.
- Motion no padrão Emil Kowalski e catálogo React Bits (217 componentes).
- Scripts: `palette.py`, `shoot.py` (prints estáveis + auditoria), `diff.py` (mapa de calor, exclusões), `publish.py` (Cloudflare).
