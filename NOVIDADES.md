# Novidades do port

O Otavix Launcher mostra este arquivo na página "Novidades" do jogo. Cada atualização tem um título
"## <data> · <versão>" e o texto em português (### pt), inglês (### en) e espanhol (### es). As mais novas ficam em cima.

## 23/11/2026 · 0.1.4
### pt
- **Pasta do port copiada ou movida depois de gerar**: a compilação parava no CMake ("CMakeCache.txt directory ... is different"). Agora o gerador apaga a compilação antiga e compila de novo na pasta nova.
### en
- **Port folder copied or moved after generating**: the build stopped in CMake ("CMakeCache.txt directory ... is different"). The generator now deletes the old build and builds again in the new folder.
### es
- **Carpeta del port copiada o movida después de generar**: la compilación se detenía en CMake ("CMakeCache.txt directory ... is different"). Ahora el generador borra la compilación anterior y compila de nuevo en la carpeta nueva.

## 22/11/2026 · 0.1.3
### pt
- **ISO montada no Windows**: escolhida pela letra do drive (por exemplo, F:\), o gerador agora mostra o caminho do arquivo .iso para escolher no lugar dela.
- **DVD no leitor**: o gerador agora explica que é preciso criar antes a ISO do DVD e escolher esse arquivo.
- **Pasta com a ISO dentro**: com uma só .iso na pasta, o gerador usa essa; com várias, lista os nomes para escolher a certa.
### en
- **ISO mounted in Windows**: when picked by its drive letter (for example, F:\), the generator now shows the path of the .iso file to pick instead.
- **DVD in the drive**: the generator now explains that you first need to make an ISO of the DVD and pick that file.
- **Folder with the ISO inside**: with a single .iso in the folder, the generator uses it; with several, it lists their names so you can pick the right one.
### es
- **ISO montada en Windows**: elegida por la letra de la unidad (por ejemplo, F:\), el generador ahora muestra la ruta del archivo .iso para elegirlo en su lugar.
- **DVD en la unidad**: el generador ahora explica que primero hay que crear la ISO del DVD y elegir ese archivo.
- **Carpeta con la ISO dentro**: con una sola .iso en la carpeta, el generador la usa; con varias, muestra sus nombres para elegir la correcta.

## 06/11/2026 · 0.1.2
### pt
- **Mais fps pelo launcher**: aberto pelo launcher, o jogo deixava de usar a thread própria de desenho e esperava a placa de vídeo a cada quadro. Isso derrubava o fps, principalmente em placas de entrada (RTX 5060, por exemplo). Corrigido.
- Reduções e ampliações de imagem que o jogo faz nos efeitos agora seguem o PS2 ponto a ponto.
- Motor 0.1.2: na próxima geração o gerador refaz da etapa 3 sozinho (o disco extraído continua valendo).
### en
- **More fps from the launcher**: when opened from the launcher, the game stopped using its own drawing thread and waited for the graphics card every frame. That lowered the fps, mostly on entry-level cards (an RTX 5060, for example). Fixed.
- Picture reductions and enlargements the game does in its effects now match the PS2 pixel for pixel.
- Engine 0.1.2: on the next generation the generator redoes it from step 3 on its own (the extracted disc is kept).
### es
- **Más fps desde el launcher**: abierto desde el launcher, el juego dejaba de usar su propio hilo de dibujo y esperaba a la tarjeta gráfica en cada fotograma. Eso bajaba los fps, sobre todo en tarjetas de entrada (una RTX 5060, por ejemplo). Corregido.
- Las reducciones y ampliaciones de imagen que el juego hace en sus efectos ahora siguen a la PS2 píxel a píxel.
- Motor 0.1.2: en la próxima generación el generador rehace desde la etapa 3 solo (el disco extraído se mantiene).


## 06/11/2026 · 0.1.1
### pt
- **Motor próprio**: o gerador não baixa nem compila mais o PS2Recomp. Agora baixa o motor do port pronto (conferido pelo SHA-256) e compila só o código do jogo: mais rápido (de 5 a 30 minutos, conforme o PC), usa menos memória e não precisa de Git.
- **Sem Python**: as ferramentas do gerador agora vêm dentro do motor (um executável só). Basta instalar o Visual Studio Build Tools; Python e Git não são mais necessários.
- Quem já tinha o port gerado: a próxima geração apaga a pasta `ps2recomp\` antiga e refaz da etapa 3 sozinha.
- O gerador ganhou a etapa do VU1 (agora são 7 etapas, como nos outros ports); sem uma receita deste jogo, o VU1 roda no interpretador do motor.
### en
- **Own engine**: the generator no longer downloads or builds PS2Recomp. It now downloads the prebuilt port engine (checked by SHA-256) and builds only the game code: faster (5 to 30 minutes, depending on the PC), less memory, and no Git needed.
- **No Python**: the generator tools now ship inside the engine (a single executable). Only Visual Studio Build Tools is needed; Python and Git are no longer required.
- If you had already generated the port: the next generation deletes the old `ps2recomp\` folder and redoes it from step 3 on its own.
- The generator gained the VU1 step (7 steps now, like the other ports); without a recipe for this game, the VU1 runs on the engine's interpreter.

## 26/10/2026 · 0.1.0
### pt
- **Primeira versão de testes.** O gerador recompila o jogo a partir da sua ISO (versão europeia).
- O jogo inicia e passa pela configuração do sistema, mas ainda não mostra imagem. **Ainda não dá para jogar.**
### en
- **First test version.** The generator rebuilds the game from your ISO (European release).
- The game boots and gets through the system setup, but shows no picture yet. **Not playable yet.**
