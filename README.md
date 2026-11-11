<h1 align="center">10.000 Bullets — port nativo para PC</h1>

<p align="center"><i>10.000 Bullets (PS2, PAL): port nativo para PC por recompilação estática (PS2Recomp). Gera a partir da sua ISO. Em desenvolvimento.</i></p>

<p align="center">
  <a href="https://github.com/otavix010/10000-bullets-pc/commits/main"><img alt="Última atualização" src="https://img.shields.io/github/last-commit/otavix010/10000-bullets-pc?label=%C3%BAltima%20atualiza%C3%A7%C3%A3o"></a>
  <a href="https://github.com/otavix010/otavix-launcher/releases/latest"><img alt="Baixar o Otavix Launcher" src="https://img.shields.io/badge/Otavix%20Launcher-baixar-b00020"></a>
  <img alt="Windows 10/11" src="https://img.shields.io/badge/Windows-10%2F11-0078d4">
  <img alt="Linux: não suportado no momento" src="https://img.shields.io/badge/Linux-n%C3%A3o%20suportado-lightgrey">
</p>

<p align="center">
  <a href="#o-que-é">O que é</a> ·
  <a href="#estado-atual-em-desenvolvimento">Estado atual: em desenvolvimento</a> ·
  <a href="#plataformas">Plataformas</a> ·
  <a href="#requisitos">Requisitos</a> ·
  <a href="#desempenho-medido">Desempenho</a> ·
  <a href="#como-gerar">Como gerar</a> ·
  <a href="#perguntas-frequentes">Perguntas frequentes</a> ·
  <a href="#como-funciona">Como funciona</a> ·
  <a href="#licença-e-créditos">Licença e créditos</a> ·
  <a href="#english-summary">English</a>
</p>

> **Projeto de fãs, sem fins lucrativos.** *10.000 Bullets* (*Tsukiyo ni Saraba*) é da Blue Moon Studio e da Taito; este projeto não tem relação com a Blue Moon Studio nem a Taito/Square Enix. Este repositório **não contém o jogo**: você precisa da **sua própria cópia** do DVD (a versão europeia, **SLES-53481**).

> [!IMPORTANT]
> **Para jogar, baixe o [Otavix Launcher](https://github.com/otavix010/otavix-launcher/releases/latest).** Ele baixa este port, pede a sua ISO, gera o jogo no seu PC e o mantém atualizado. Para relatar um problema ou pedir algo, use **"Reportar problema"** na página do jogo no launcher: o relatório já vai com o log e as configurações, e é por ele que as correções saem mais rápido.
>
> **To play, download the [Otavix Launcher](https://github.com/otavix010/otavix-launcher/releases/latest).** It downloads this port, asks for your ISO, makes the game on your PC and keeps it updated. To report a problem or ask for something, use **"Report a problem"** on the game's page in the launcher: the report carries the log and the settings, and that is how fixes come out fastest.

[English summary below](#english-summary)

## O que é

Um port **nativo** do *10.000 Bullets* (PlayStation 2, 2005) para Windows. Não é um emulador: o código do jogo é **traduzido para C++ e compilado** para x86-64 (recompilação estática), com o motor PS2 próprio do projeto (Otavix).

Como o código do jogo não pode ser distribuído, **o seu PC gera e compila a parte do jogo a partir da sua ISO**. Um comando só faz tudo.

## Estado atual: em desenvolvimento

Começando: inicia e passa pela configuração do sistema, mas ainda não mostra imagem: para durante a inicialização do motor do jogo. Por enquanto, só para testes.

## Plataformas

| | **Windows** | **Linux / SteamOS** |
|---|---|---|
| Situação | **em desenvolvimento** (este port) | **não suportado no momento** |
| Como jogar | pelo launcher, ou `gerar.cmd` e `jogar.cmd` | só o port de *God of War: Ascension* tem versão Linux (beta) por enquanto |

## Requisitos

- **Windows 10/11 64 bits**, com o **Visual Studio 2022 Build Tools** (C++ e CMake; o comando está em [Como gerar](#como-gerar)). O launcher confere isso para você.
- A **sua ISO** do *10.000 Bullets*, na versão europeia (PAL) (**SLES-53481**). O gerador confere o executável e, se não bater, diz se é outra edição (outra região ou versão) ou o mesmo disco com o executável modificado.
- **Memória:** o gerador usa uns 3 GB de RAM por compilação em paralelo e escolhe o paralelismo pela memória livre; com pouca RAM funciona, só demora mais.
- **Disco:** alguns GB livres para os arquivos do disco, o código traduzido e a compilação (um jogo desta família usa uns 5 GB; o seu pode variar com o tamanho do disco).
- **AVX2 não é obrigatório**: o gerador detecta a CPU e usa as bibliotecas AVX2 ou SSE4.

## Desempenho medido

FPS de jogo, no motor publicado, sem a resolução interna (1x). **Só colocamos o que foi medido**; as demais máquinas ainda não foram testadas com este jogo.

| Máquina | CPU | GPU | FPS |
|---|---|---|---|
| **PC 1** | Ryzen 7 9800X3D | RTX 5080 | ainda não medido |
| **PC 2** | Core i5-11400F | RX 9060 XT | não medido |
| **Notebook** | Core i5-10300H (4/8) | GTX 1650 | não medido |
| **Portátil** | Legion Go S (Linux) | Radeon 780M | não suportado |

## Problemas conhecidos

- No motor publicado, o jogo pode **ficar sem imagem ou cair logo no início**. Está em correção; ainda não foi confirmado no motor novo.
- Esta é a **versão europeia (PAL)** apenas (SLES-53481); outras regiões e versões são recusadas pelo gerador, com o motivo.

## Como gerar

### Pelo Otavix Launcher

O [Otavix Launcher](https://github.com/otavix010/otavix-launcher/releases/latest) lista este port como **em desenvolvimento**: ele baixa o port, pede a ISO, gera o jogo e abre.

### À mão

**1. O que você precisa ter:** a sua cópia do *10.000 Bullets* **europeu** (SLES-53481, "10.000 Bullets (Europe) (En,Fr,De,Es,It)") como imagem **.iso** do DVD. O gerador confere o executável do jogo pelo hash: outras versões não servem, porque o mapa de funções é o da europeia.

**2. Instale as ferramentas (uma vez só)**, num terminal:
```
winget install Microsoft.VisualStudio.2022.BuildTools --override "--quiet --wait --add Microsoft.VisualStudio.Workload.VCTools --add Microsoft.VisualStudio.Component.VC.CMake.Project --includeRecommended"
```
O resto o gerador baixa sozinho: o motor do port (pacote pronto, conferido pelo SHA-256) e o FFmpeg (LGPL). Não precisa de Python nem de Git.

**3. Baixe este repositório** (botão *Code > Download ZIP*, ou `git clone`) e extraia numa pasta **sem espaços no caminho**, por exemplo `C:\10000-bullets-pc`. Deixe uns 5 GB livres nesse disco (os arquivos do disco, o código traduzido e a compilação).

**4. Clique duas vezes em `gerar.cmd`** e escolha a ISO. Ele:
- confere a ISO e extrai os arquivos do disco para `trabalho\disc`;
- baixa o motor do port (pacote pronto, conferido pelo SHA-256);
- traduz o código do jogo para C++ (só no seu PC);
- compila o código do jogo (de 5 a 30 minutos, conforme o PC; precisa de 16 GB de RAM ou mais).

**5. Jogue com `jogar.cmd`.** O jogo lê os arquivos de `trabalho\disc` e a ISO no lugar onde ela estava na geração (se mudar a ISO de lugar, rode `gerar.cmd -RefazerDe 2`).

Depois de atualizar o port, `gerar.cmd -RefazerDe 3` baixa o motor novo, retraduz e recompila sem extrair o disco de novo.

## Perguntas frequentes

**Este repositório tem o jogo?** Não. Você precisa da sua própria cópia do DVD; o gerador monta o port no seu PC a partir da sua ISO.

**Roda no Linux ou no SteamOS?** Ainda não: só o port de *God of War: Ascension* tem versão Linux (beta). Este roda no Windows.

**O gerador disse "executável modificado" ou "edição diferente". E agora?** "Edição diferente" é outra região ou versão do disco; "executável modificado" é o mesmo disco com um executável alterado (patch, tradução, hack ou outra tiragem). Use uma cópia original sem modificações (SLES-53481).

**Saiu uma atualização do port. O que faço?** Atualize pelo launcher e gere de novo (`gerar.cmd -RefazerDe 3` à mão): ele baixa o motor novo, retraduz e recompila sem extrair o disco de novo.

**Onde relato um problema?** No launcher, em **"Reportar problema"** na página do jogo.

## Como funciona

- **O motor** (tradutor MIPS R5900 → C++ e runtime: GS, VU1, DMA, IOP, áudio SPU2, cartão de memória) é próprio do projeto e vem pronto (bibliotecas compiladas); o seu PC só traduz e compila o código do jogo.
- **O mapa de funções** (`jogo\ghidra_funcoes.csv`) veio de uma análise com o [Ghidra](https://ghidra-sre.org/) e a extensão ghidra-emotionengine-reloaded: são só endereços e nomes, nada do código do jogo. `jogo\entradas_extra.txt` lista funções chamadas só por ponteiro e alvos de tabelas de salto que a análise não marcou, e `jogo\stubs_extra.txt` as funções trocadas por respostas fixas (por exemplo, vídeos pulados por enquanto).

## Licença e créditos

- **O nosso código** (`gerar.ps1`, `gerar.cmd`, `ferramentas\`): [MIT](LICENSE).
- **O motor do port** (pacote `otx-motor-ps2`, baixado pronto pelo gerador) não é coberto pela licença MIT; os avisos de terceiros dele (raylib e glfw: zlib; FFmpeg: LGPL, DLLs à parte) estão no `TERCEIROS.txt` do pacote.
- *10.000 Bullets* (*Tsukiyo ni Saraba*) é da Blue Moon Studio e da Taito. Este é um projeto de fãs, sem fins lucrativos, sem relação com a Blue Moon Studio nem a Taito/Square Enix nem endossado por elas.

## English summary

A **native PC port** of *10.000 Bullets* (PlayStation 2, 2005) made by **static recompilation** with the project's own PS2 engine. **Work in progress.**

**Platforms:** Windows 10/11 only for now (Linux is not supported yet; only the *God of War: Ascension* port has a Linux beta). Performance is listed only where we measured it (see the table above); machines not listed are not measured yet. **Easiest: the [Otavix Launcher](https://github.com/otavix010/otavix-launcher/releases/latest).**

**Bring your own game**: no game code or data here, only the function map (addresses) and translation settings. You need the **European** release (SLES-53481, Redump "10.000 Bullets (Europe) (En,Fr,De,Es,It)") as an **.iso**. Install Visual Studio 2022 Build Tools with C++ and CMake (commands above), download this repository to a path without spaces, double-click **`gerar.cmd`** (it checks your ISO, extracts the disc files, downloads the prebuilt engine package (no Git needed), translates the game code on your PC and builds it, in 5 to 30 minutes), then play with **`jogar.cmd`**.

License: our scripts are MIT; the engine package is not covered by it, and its third-party notices are in its `TERCEIROS.txt`. *10,000 Bullets* (*Tsukiyo ni Saraba*) belongs to Blue Moon Studio and Taito; this is a non-commercial fan project, not affiliated with or endorsed by Blue Moon Studio or Taito/Square Enix.
