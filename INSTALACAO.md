# Instalar o CEM na sua máquina

O CEM (Claude Environment Manager) faz **backup, restauração, organização e migração** do seu ambiente do
Claude Code. O instalador confere os pré-requisitos, baixa as dependências, compila o aplicativo de desktop e
a linha de comando `cem` e, se você quiser, cria um atalho. Tudo fica dentro da pasta do pacote.

> Licença: **PolyForm Strict 1.0.0** — você pode baixar e usar o CEM para fins **não comerciais** (pessoais,
> acadêmicos, institucionais). **Não** é permitido redistribuir cópias, modificar ou usar comercialmente. Texto
> completo em `LICENSE`; programa protegido pela Lei 9.609/98. O instalador pede o seu aceite antes de instalar.

## Pré-requisitos (já instalados por você)

| O quê | Para quê | Onde |
|---|---|---|
| Windows 10/11 64 bits | o instalador é PowerShell | — |
| **Node.js 20 ou mais novo** (versão LTS) | compilar e rodar o app e a CLI | https://nodejs.org |
| **pnpm 10 ou mais novo** (ou o `corepack`, que já vem com o Node até a versão 24) | instalar as dependências | `npm install -g pnpm` |
| Internet durante a instalação | baixa as dependências e o runtime do Electron (~100 MB) | — |
| Espaço em disco: cerca de 1 GB livre | `node_modules` ocupa ~660 MB depois de instalado | — |

O CEM não precisa que o Claude Code esteja instalado para rodar; só lê os arquivos dele se existirem.

## Passo a passo

1. Baixe o pacote `CEM-<versão>-instalador.zip` (e o `.sha256`, se quiser conferir) na página de *Releases* de
   https://github.com/luizdione/CEM_platform.
2. (Opcional) Confira o arquivo no PowerShell e compare com o conteúdo do `.sha256`:
   `Get-FileHash .\CEM-<versão>-instalador.zip -Algorithm SHA256`
3. Extraia numa **pasta curta**, por exemplo `C:\CEM` (o caminho da pasta precisa ter no máximo 120 caracteres: o
   Windows não executa programas em caminhos de mais de 260 caracteres e a compilação falharia; evite também
   pastas sincronizadas pelo OneDrive). Dentro da pasta extraída haverá `CEM-<versão>\`.
4. Dê dois cliques em **`Instalar-CEM.bat`** (dentro de `CEM-<versão>\`). Abre uma janela de console que:
   1. mostra o resumo da licença e pede o aceite — digite **S** para aceitar;
   2. confere o Node.js (≥ 20) e o pnpm (≥ 10, ou usa o corepack);
   3. instala as dependências (`pnpm install --frozen-lockfile`);
   4. compila os pacotes e a CLI (`pnpm build`) e o app desktop;
   5. confere que a CLI responde com a versão do pacote;
   6. pergunta se você quer o atalho **Claude Environment Manager (CEM)** na Área de Trabalho.
5. Abra o CEM pelo atalho ou, na pasta do pacote:
   `apps\desktop\node_modules\electron\dist\electron.exe apps\desktop`
   Na primeira abertura ele varre o seu ambiente (somente leitura) e mostra o Painel.

Para testar sem perguntas e sem atalho: `Instalar-CEM.bat -AutoTeste`.

## O que o instalador grava (e nada mais)

| Onde | O quê |
|---|---|
| `<pasta do pacote>\node_modules\` e `apps\*\node_modules\` | as dependências (inclui o runtime do Electron) |
| `<pasta do pacote>\apps\desktop\out\` e `...\dist\` | o app e a CLI compilados |
| `Área de Trabalho\Claude Environment Manager (CEM).lnk` | o atalho, só se você aceitar |
| cache do pnpm / corepack | só o cache de downloads do próprio pnpm, se ele for usado via corepack |

Não altera o `PATH`, o registro do Windows nem variáveis de ambiente. Para remover, apague a pasta do pacote e o atalho.

## Usar

- **Aplicativo**: Painel, Scanner, Diagnóstico, Inventário do servidor, Análise e uso de tokens, MCP / Skills /
  Agentes / Markdown, Perfis, Backup, Restauração, Histórico e Sincronização. Preferências em *Settings*.
- **Linha de comando**, na pasta do pacote: `node apps\cli\dist\index.js --help`, por exemplo
  `node apps\cli\dist\index.js scan`, `... doctor`, `... backup`, `... verify <arquivo.cem>`.
- **Backup**: o app mostra o caminho, o tamanho e o número de arquivos do `.cem` criado. Marque a criptografia
  AES-256-GCM e defina uma senha se o ambiente tiver segredos; sem a senha não há como recuperar o arquivo.
- **Atualizar**: baixe o novo `.zip`, extraia numa pasta nova e rode o instalador de novo. Seus `.cem` e as
  preferências ficam fora da pasta do pacote e não são perdidos.

## Outros sistemas

O instalador em `.bat` é só para Windows. Em macOS ou Linux, para uso pessoal sob a mesma licença, dentro da
pasta extraída com Node.js ≥ 20 e pnpm ≥ 10:

```bash
pnpm install --frozen-lockfile
pnpm build
pnpm --filter @cem/desktop build
node apps/cli/dist/index.js --help
```

## Problemas comuns

- **"Node.js não encontrado" / "Node.js ... é antigo"**: instale a versão LTS em https://nodejs.org e abra um
  console novo antes de rodar o instalador de novo.
- **"pnpm não encontrado"**: rode `npm install -g pnpm` num console novo (ou ative o corepack) e tente de novo.
- **"A pasta do pacote tem caminho longo demais"**: extraia numa pasta curta, como `C:\CEM`.
- **"A execução de scripts foi desabilitada"**: o `.bat` já passa `-ExecutionPolicy Bypass`; se rodar o `.ps1` à
  mão, use `powershell -ExecutionPolicy Bypass -File instalador\Instalar-CEM.ps1`.
- **Falha ao baixar o Electron** (rede corporativa, proxy, antivírus): rode o instalador de novo numa rede sem
  bloqueio; ele é seguro de repetir.
- **O Windows SmartScreen ou o antivírus avisa sobre o `.bat`**: o arquivo é texto e pode ser lido antes de
  executar; confira o `.sha256` do `.zip`.
- **Algo parou no meio**: rode `Instalar-CEM.bat` de novo; é seguro repetir.
