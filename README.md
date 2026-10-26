# 10.000 Bullets — port nativo para PC

> **Projeto de fãs, sem fins lucrativos.** *10.000 Bullets* (*Tsukiyo ni Saraba*) é da Blue Moon Studio e da Taito; este projeto não tem relação com a Blue Moon Studio nem a Taito/Square Enix. Este repositório **não contém o jogo**: você precisa da **sua própria cópia** do DVD (a versão europeia, **SLES-53481**).

[English summary below](#english-summary)

## O que é

Um port **nativo** do *10.000 Bullets* (PlayStation 2, 2005) para Windows. Não é um emulador: o código do jogo é **traduzido para C++ e compilado** para x86-64 (recompilação estática), em cima do [PS2Recomp](https://github.com/ran-j/PS2Recomp).

Como o código do jogo não pode ser distribuído, **o seu PC gera e compila a parte do jogo a partir da sua ISO**. Um comando só faz tudo.

## Estado atual: em desenvolvimento

Começando: inicia e passa pela configuração do sistema, mas ainda não mostra imagem: para durante a inicialização do motor do jogo. Por enquanto, só para testes.

## Como gerar

### Pelo Otavix Launcher

O [Otavix Launcher](https://github.com/otavix010/otavix-launcher/releases/latest) lista este port como **em desenvolvimento**: ele baixa o port, pede a ISO, gera o jogo e abre.

### À mão

**1. O que você precisa ter:** a sua cópia do *10.000 Bullets* **europeu** (SLES-53481, "10.000 Bullets (Europe) (En,Fr,De,Es,It)") como imagem **.iso** do DVD. O gerador confere o executável do jogo pelo hash: outras versões não servem, porque o mapa de funções é o da europeia.

**2. Instale as ferramentas (uma vez só)**, num terminal:
```
winget install Python.Python.3.12
winget install Microsoft.VisualStudio.2022.BuildTools --override "--quiet --wait --add Microsoft.VisualStudio.Workload.VCTools --add Microsoft.VisualStudio.Component.VC.CMake.Project --includeRecommended"
```
O resto o gerador baixa sozinho: o PS2Recomp (na versão fixada), as bibliotecas dele e, se o PC não tiver Git, o Git portátil (MinGit).

**3. Baixe este repositório** (botão *Code > Download ZIP*, ou `git clone`) e extraia numa pasta **sem espaços no caminho**, por exemplo `C:\10000-bullets-pc`. Deixe uns 15 GB livres nesse disco (o código traduzido e a compilação ocupam bastante).

**4. Clique duas vezes em `gerar.cmd`** e escolha a ISO. Ele:
- confere a ISO e extrai os arquivos do disco para `trabalho\disc`;
- baixa o PS2Recomp, aplica as nossas correções (`patches\`) e compila o tradutor;
- traduz o código do jogo para C++ (só no seu PC);
- compila o jogo (de 20 minutos a 1 hora, conforme o PC; precisa de 16 GB de RAM ou mais).

**5. Jogue com `jogar.cmd`.** O jogo lê os arquivos de `trabalho\disc` e a ISO no lugar onde ela estava na geração (se mudar a ISO de lugar, rode `gerar.cmd -RefazerDe 2`).

Depois de atualizar o port, `gerar.cmd -RefazerDe 3` aplica as correções novas, retraduz e recompila sem extrair o disco de novo.

## Como funciona

- **PS2Recomp** traduz o executável do PS2 (MIPS R5900, o "Emotion Engine") para C++ e compila com o runtime dele (GS por software, VU1, DMA, IOP, áudio, cartão de memória).
- **O mapa de funções** (`jogo\ghidra_funcoes.csv`) veio de uma análise com o [Ghidra](https://ghidra-sre.org/) e a extensão [ghidra-emotionengine-reloaded](https://github.com/chaoticgd/ghidra-emotionengine-reloaded): são só endereços e nomes, nada do código do jogo. `jogo\entradas_extra.txt` lista funções chamadas só por ponteiro e alvos de tabelas de salto que a análise não marcou, e `jogo\stubs_extra.txt` as funções trocadas por respostas fixas (por exemplo, vídeos pulados por enquanto).
- **As nossas correções no PS2Recomp** (GPLv3 como ele):
  - no tradutor (`patches\recomp_otavix.patch`): os desvios BLTZ/BGEZ/BLEZ/BGTZ testam o registrador inteiro de 64 bits, como no EE (antes, a subtração de `double` por software e o `pow` davam lixo);
  - no runtime (`patches\runtime_otavix.patch`): interrupções que respeitam o `di`/`ei` do EE, pilha do `SetupThread` no topo da RAM, pilha do executável de 256 MB (o código traduzido tem funções com quadros de mais de 1 MB), pacotes internos numa área do kernel em vez do heap do jogo, callback do `sceCdCallback`, comandos SIF do EE entregues aos módulos que rodam no IOP emulado, leitura de setores direto da ISO, transferência de som EE→IOP, `sceCdReadDvdDualInfo`, cache de textura invalidado nos uploads, VU1 mais rápido e ferramentas de diagnóstico;
  - na montagem (`ferramentas\monta_config.py`): as funções de `double` da libm (`pow`, `sin`, `sqrt`…) rodam o código do próprio jogo em vez dos substitutos de `float` do runtime.

## Licença e créditos

- **O nosso código** (`gerar.ps1`, `gerar.cmd`, `ferramentas\`): [MIT](LICENSE).
- **PS2Recomp** (baixado pelo gerador) e **as nossas correções nele** (`patches\`): [GPLv3](https://github.com/ran-j/PS2Recomp/blob/main/LICENSE), de ran-j e colaboradores. O executável gerado no seu PC também é GPLv3.
- *10.000 Bullets* (*Tsukiyo ni Saraba*) é da Blue Moon Studio e da Taito. Este é um projeto de fãs, sem fins lucrativos, sem relação com a Blue Moon Studio nem a Taito/Square Enix nem endossado por elas.

## English summary

A **native PC port** of *10.000 Bullets* (PlayStation 2, 2005) made by **static recompilation** with [PS2Recomp](https://github.com/ran-j/PS2Recomp). **Work in progress.**

**Bring your own game**: no game code or data here, only the function map (addresses) and translation settings. You need the **European** release (SLES-53481, Redump "10.000 Bullets (Europe) (En,Fr,De,Es,It)") as an **.iso**. Install Python 3.11+ and Visual Studio 2022 Build Tools with C++ and CMake (commands above), download this repository to a path without spaces, double-click **`gerar.cmd`** (it checks your ISO, extracts the disc files, fetches the pinned PS2Recomp, applies our runtime patches, translates the game code on your PC and builds it), then play with **`jogar.cmd`**.

License: our scripts are MIT; PS2Recomp and our patches to it are GPLv3. *10,000 Bullets* (*Tsukiyo ni Saraba*) belongs to Blue Moon Studio and Taito; this is a non-commercial fan project, not affiliated with or endorsed by Blue Moon Studio or Taito/Square Enix.
