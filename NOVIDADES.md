# Novidades do port

O Otavix Launcher mostra este arquivo na página "Novidades" do jogo. Cada atualização tem um título
"## <data> · <versão>" e o texto em português (### pt) e inglês (### en). As mais novas ficam em cima.

## 06/11/2026 · 0.1.1
### pt
- **Motor próprio**: o gerador não baixa nem compila mais o PS2Recomp. Agora baixa o motor do port pronto (conferido pelo SHA-256) e compila só o código do jogo: mais rápido (de 5 a 30 minutos, conforme o PC), usa menos memória e não precisa de Git.
- Quem já tinha o port gerado: a próxima geração apaga a pasta `ps2recomp\` antiga e refaz da etapa 3 sozinha.
- O gerador ganhou a etapa do VU1 (agora são 7 etapas, como nos outros ports); sem uma receita deste jogo, o VU1 roda no interpretador do motor.
### en
- **Own engine**: the generator no longer downloads or builds PS2Recomp. It now downloads the prebuilt port engine (checked by SHA-256) and builds only the game code: faster (5 to 30 minutes, depending on the PC), less memory, and no Git needed.
- If you had already generated the port: the next generation deletes the old `ps2recomp\` folder and redoes it from step 3 on its own.
- The generator gained the VU1 step (7 steps now, like the other ports); without a recipe for this game, the VU1 runs on the engine's interpreter.

## 26/10/2026 · 0.1.0
### pt
- **Primeira versão de testes.** O gerador recompila o jogo a partir da sua ISO (versão europeia).
- O jogo inicia e passa pela configuração do sistema, mas ainda não mostra imagem. **Ainda não dá para jogar.**
### en
- **First test version.** The generator rebuilds the game from your ISO (European release).
- The game boots and gets through the system setup, but shows no picture yet. **Not playable yet.**
