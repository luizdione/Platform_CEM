# Instalar o CEM na sua máquina

O CEM (Claude Environment Manager) faz **backup, restauração, organização e migração** do seu ambiente do
Claude Code. A entrega é um **instalador do Windows**: você baixa um arquivo, dá dois cliques e usa. Não
precisa de Node.js, não precisa compilar nada e não precisa de internet durante a instalação.

> Licença: **PolyForm Strict 1.0.0** — você pode baixar e usar o CEM para fins **não comerciais** (pessoais,
> acadêmicos, institucionais). **Não** é permitido redistribuir cópias, modificar ou usar comercialmente. Texto
> completo em `LICENSE`; programa protegido pela Lei 9.609/98. O instalador mostra a licença e pede o seu
> aceite antes de instalar.

## Pré-requisitos

| O quê | Para quê |
|---|---|
| Windows 10 ou 11, 64 bits | o aplicativo é compilado para essa plataforma |
| Cerca de 400 MB livres em disco | o aplicativo instalado |
| **Nada além disso** | sem Node.js, sem pnpm, sem compilar, sem internet na instalação |

Não precisa de permissão de administrador: a instalação é **da sua conta de usuário**, não da máquina toda.

O CEM não exige que o Claude Code esteja instalado para abrir; ele só lê os arquivos dele se existirem.

## Passo a passo

1. Na aba **Releases** de <https://github.com/luizdione/Platform_CEM>, baixe:
   - `install_CEM-<versão>.exe` — o instalador;
   - `install_CEM-<versão>.exe.sha256` — a soma de verificação (opcional, mas vale conferir).
2. **Confira o arquivo** antes de executar. No PowerShell, na pasta onde baixou:

   ```powershell
   Get-FileHash .\install_CEM-<versão>.exe -Algorithm SHA256
   ```

   O resultado tem de ser igual ao conteúdo do arquivo `.sha256`. Se for diferente, **não execute**: baixe de novo.
3. Dê dois cliques no `install_CEM-<versão>.exe`.
4. **O Windows vai avisar que o editor é desconhecido** — veja a seção seguinte. Isso é esperado.
5. O instalador abre e:
   1. mostra a licença e pede o aceite — você precisa aceitar para continuar;
   2. propõe uma pasta de instalação, que você pode trocar;
   3. instala o aplicativo, cria o atalho **Claude Environment Manager** na Área de Trabalho e no menu Iniciar,
      e associa os arquivos `.cem` ao CEM (dois cliques num backup abrem o programa).
6. Abra pelo atalho. Na primeira abertura o CEM varre o seu ambiente **somente leitura** e mostra o Painel.

### O aviso do Windows (SmartScreen)

O instalador **não tem assinatura digital de código**, porque o certificado é pago e o CEM é distribuído por
um autor individual. Então o Windows mostra *"O Windows protegeu o seu PC"* / *"Editor: desconhecido"*. Para
seguir: **Mais informações → Executar assim mesmo**.

Esse aviso diz que o Windows não conhece o editor — não que o arquivo esteja alterado. Quem garante que o
arquivo é o que o autor publicou é a **soma SHA-256** do passo 2. Confira-a e você tem, quanto à integridade
do arquivo, a mesma garantia que uma assinatura daria. O antivírus pode reclamar pelo mesmo motivo; se
bloquear, libere o arquivo depois de conferir a soma.

## O que o instalador grava (e nada mais)

| Onde | O quê |
|---|---|
| A pasta de instalação que você escolheu | o aplicativo |
| `Área de Trabalho\Claude Environment Manager.lnk` e o menu Iniciar | os atalhos |
| Registro do usuário (`HKCU`) | a entrada de "Aplicativos instalados", para desinstalar, e a associação do `.cem` |
| Pasta de dados do aplicativo, na sua conta | as suas preferências (tema, padrões de backup, privacidade) |

Não mexe no `PATH`, não escreve em `HKEY_LOCAL_MACHINE` e não instala serviço nem tarefa agendada.

## Desinstalar

**Configurações do Windows → Aplicativos → Aplicativos instalados → Claude Environment Manager →
Desinstalar.** Os seus arquivos `.cem` e as suas preferências **não** são apagados: ficam fora da pasta de
instalação, para você poder reinstalar ou atualizar sem perder nada. Para apagar também as preferências,
remova a pasta de dados do aplicativo depois de desinstalar.

## Atualizar

Baixe o `install_CEM-<versão nova>.exe` na aba **Releases**, confira a soma e execute. Ele atualiza a
instalação existente, mantendo as suas preferências e os seus backups.

## A linha de comando `cem` (opcional)

Além do aplicativo, o CEM tem uma linha de comando, entregue à parte porque ela **precisa do Node.js**. Na
aba Releases, baixe `cem-cli-<versão>.tgz` e instale:

```powershell
npm install -g .\cem-cli-<versão>.tgz
```

Isso precisa de **Node.js 20 ou mais novo** (<https://nodejs.org>). Depois:

```powershell
cem --help
cem scan
cem doctor
cem backup
cem verify meu-backup.cem
```

Comandos disponíveis: `scan`, `doctor`, `fix`, `backup`, `export`, `restore`, `import`, `verify`, `profiles`,
`tokens`, `usage`, `mcp`, `managers`, `history` e `sync`. A mesma licença vale para a CLI, e o texto dela vai
dentro do pacote.

## Usar

- **Aplicativo**: Painel, Scanner, Diagnóstico, Inventário do servidor, Análise e uso de tokens,
  MCP / Skills / Agentes / Markdown, Perfis, Backup, Restauração, Histórico e Sincronização. Preferências em
  *Settings*.
- **Backup**: seção **Backup** → escolha a pasta de destino → (opcional) marque a criptografia AES-256-GCM e
  defina uma senha → **Criar backup**. O app mostra o caminho, o tamanho e o número de arquivos do `.cem`.
  **Sem a senha, um `.cem` criptografado não tem recuperação** — guarde-a.
- **Restaurar**: seção **Restore** → escolha o `.cem` → revise o que será escrito → restaure. Dá para
  restaurar só parte, por tipo de artefato ou arquivo por arquivo.
- O CEM começa só **olhando** o seu ambiente, somente leitura. Nada é apagado automaticamente, e cada correção
  proposta em "Resolver problemas" é aceita ou ignorada por você, com backup automático antes.

## Outros sistemas (macOS e Linux)

A entrega pronta é só para Windows. A linha de comando acima funciona em macOS e Linux com Node.js ≥ 20
(`npm install -g ./cem-cli-<versão>.tgz`). Para o aplicativo de desktop nesses sistemas, fale com o autor.

## Problemas comuns

- **"O Windows protegeu o seu PC" / "Editor: desconhecido"**: esperado, veja a seção do SmartScreen acima —
  confira a soma SHA-256 e use **Mais informações → Executar assim mesmo**.
- **A soma SHA-256 não bate**: não execute o arquivo. O download provavelmente veio incompleto; baixe de novo.
- **O antivírus apagou o instalador**: confira a soma do arquivo baixado e libere-o na quarentena do
  antivírus, ou adicione uma exceção para a pasta de download.
- **"Este aplicativo não pode ser executado no seu PC"**: o instalador é 64 bits; confira em
  *Configurações → Sistema → Sobre* se o seu Windows é de 64 bits.
- **O atalho não apareceu**: procure "Claude Environment Manager" no menu Iniciar. Para fixar na barra de
  tarefas, clique com o botão direito na entrada do menu Iniciar → *Fixar na barra de tarefas*: instalador
  nenhum consegue fazer isso sozinho no Windows 10/11.
- **`cem` não é reconhecido depois do `npm install -g`**: abra um console novo, para ele reler o `PATH`.
- **Algo parou no meio da instalação**: rode o instalador de novo; é seguro repetir.
