# Changelog

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
