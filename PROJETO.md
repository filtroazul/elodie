# um passeio sanrio 🎀 — joguinho de aniversário

**FONTE DE VERDADE deste projeto. LER PRIMEIRO antes de mexer em qualquer coisa.**

## o que é

joguinho-presente de aniversário pra ela, tema sanrio. ela controla a **elodie** —
pinsher com capuz da kuromi (pixel art, gola de bobo da corte com pompons rosa,
caudinha de diabinho) — que anda num grid (labirinto fofo pastel) desviando de
obstáculos e nuvenzinhas bravas ☁️💢. no caminho encontra **9 amiguinhos sanrio** —
cada um abre um modal com um textinho. no fim do labirinto tem o **bolo**: festa
com confete + mensagem final.

- roda direto no navegador: abrir `index.html` (arquivo único, sem build)
- funciona no **pc (setas/wasd)** e no **celular (swipe + d-pad na tela)**
- iphone-friendly (safe-area, touch-action none)

## estado atual (11/07/2026)

✅ MOTOR PRONTO E TESTADO com 9 amiguinhos (partida completa validada, 98 passos)
✅ elodie no jogo: `img/dog.png` (rembg do `Downloads/Elodie.png`, fundo removido, aparada)
✅ os 9 amiguinhos em `img/1.png` … `img/9.png` (nomes no `CONFIG`):
   1 eliza (hello kitty) · 2 dylan (dear daniel) · 3 kaia (badtz-maru) ·
   4 richard (chococat) · 5 kael (ratinha) · 6 gi (my melody) ·
   7 kat saboy (ovelhinha piano, rembg do Downloads/6.5.png, entrou depois entre gi e tim —
   os antigos 7/8 viraram 8/9) · 8 tim (pochacco) · 9 lottie (keroppi)
✅ TEXTOS de eliza, kaia, richard, kael, tim e lottie já no `CONFIG` (cartinhas
   dos amigos do RPG pra Soraia/Soso; texto do kael usa fonte itálica unicode, manter)
✅ MÚSICA plugada: `musica.mp3` na raiz toca em loop no toque do "começar"
   (gesto do usuário → autoplay liberado em iphone/android/pc; retenta no
   próximo toque se o navegador barrar; silêncio sem erro se o arquivo faltar)
✅ amiguinho 6 (gi) = CARTINHA EM IMAGEM (`img/msg6.jpg`, copiada de
   Downloads/mensagem_elo_aniversario_.jpg): modal mostra miniatura → toque abre
   LIGHTBOX com zoom (arrastar, pinça, rolinho, toque duplo; ✕ ou Esc fecha).
   no CONFIG usa `imagem:` em vez de `texto:` — qualquer amiguinho pode ser assim.
✅ textos longos: área do modal rola (max-height 42dvh, alinhado à esquerda)

✅ texto da kat saboy (7) no `CONFIG` ("futura titia")
✅ texto do dylan (2) no `CONFIG` — TODOS os 9 textos prontos!
✅ musica.mp3 na raiz, testada tocando
✅ repositório git → https://github.com/filtroazul/elodie (push a cada mudança;
   sugerido github pages pra ela jogar pelo link)
✅ controles celular: swipe + setinhas com andar contínuo ao segurar;
   instrução da tela inicial adapta pc/celular

🔴 FALTA:
1. **mensagemFinal** (ainda placeholder)
2. **grid de caminhada da elodie** → Iagho gera no gpt a partir do Elodie.png e me manda;
   eu processo (rembg/fatiar/normalizar) e salvo como `img/dog-grid.png`.
   **formato que o motor espera**: 4 quadros lado a lado numa única linha (grade 4×1),
   células do MESMO tamanho, personagem de perfil andando PARA A DIREITA (o motor
   espelha pra esquerda), fundo transparente. quadro 1 = pose parada.
   se vier em outro layout, ajustar `GRID_FRAMES` e/ou fatiar. o motor detecta o
   arquivo sozinho e troca a imagem estática pela animação (1 quadro por passo,
   volta pra pose parada após 380ms sem andar).
5. `img/bolo.png` (opcional, tem 🎂 de fallback)

## como funciona por dentro

- `MAPA`: array de strings 9 colunas × 65 linhas. `#` obstáculo, `.` chão,
  `1`-`9` amiguinhos (portões que bloqueiam o caminho — garantem a ordem),
  `B` bolo, `S` início. **se editar o mapa, manter um caminho possível!**
- amiguinho encontrado fica translúcido com 💗 e vira passagem
- nuvens (`NUVENS_INIT`, 9): patrulham fileiras abertas, quicam nas paredes;
  se esbarram na jogadora, dão um empurrãozinho e voltam
- bolo antes dos 9: modal "calma, calma!" avisando quantos faltam
- HUD: contador 💜 X/9 com coraçõezinhos que acendem
- imagens: `onload` marca `tem-img`/`tem-grid` (fallback automático:
  grid > dog.png > svg placeholder; amiguinho png > bolinha numerada)
- teste automatizado: existe um driver BFS (scratchpad da sessão) que joga a
  partida inteira via `agent-browser eval` — refazer se mexer no mapa

## prompt sugerido pro gpt (grid de caminhada)

> usando exatamente esta personagem (pixel art), crie um sprite sheet de
> animação de caminhada: 4 quadros lado a lado numa única linha (grade 4×1),
> todas as células do mesmo tamanho, a personagem de corpo inteiro vista de
> perfil andando para a direita, mesmo estilo e proporções em todos os quadros,
> quadro 1 parada, quadros 2–4 ciclo de passos, fundo branco liso, sem sombra

## decisões tomadas

- personagens numerados 1–8 (Iagho nomeia depois no CONFIG)
- plataforma: pc + celular
- final: festa com bolo + mensagem
- estilo: pastel lilás/rosa, vibe kuromi (deco 🌸🎀⭐🍓💜🌷 nos arbustos)
- elodie = pixel art (image-rendering: pixelated no sprite-grid)
