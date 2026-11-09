# CEM — Claude Environment Manager (backup, restauração e migração do ambiente do Claude Code)

![Licença](https://img.shields.io/badge/licen%C3%A7a-PolyForm%20Strict%201.0.0-orange)
![Plataforma](https://img.shields.io/badge/plataforma-Windows%2010%2F11-blue)
![Uso](https://img.shields.io/badge/uso-n%C3%A3o%20comercial-lightgrey)

O **CEM** (Claude Environment Manager) é um aplicativo de desktop e uma linha de comando para quem usa o
**Claude Code** e quer **guardar, restaurar, organizar e levar para outro computador** o próprio ambiente:
configurações, skills, agentes, servidores MCP, arquivos `CLAUDE.md`, prompts e templates. Ele localiza tudo
sozinho, mostra o que há de duplicado, quebrado ou pesado e empacota o ambiente num arquivo `.cem` (com
conferência de integridade e criptografia opcional) para reinstalar em poucos cliques. Tudo é **local**: nada
sai da sua máquina.

O CEM **nunca** modifica, intercepta nem faz engenharia reversa do Claude Code ou de qualquer software da
Anthropic: só lê e grava arquivos locais documentados, do próprio usuário, e só altera algo quando você manda
(criar backup, restaurar, aplicar correção).

Este repositório é a **página de distribuição** do CEM: aqui ficam o guia de instalação, a licença e o
instalador (aba **Releases**). O código-fonte não é publicado: o que você baixa é o **aplicativo já
compilado**.

## Para quem é

Quem usa o Claude Code no dia a dia — pesquisadores, desenvolvedores, quem troca de computador ou mantém vários
ambientes — e quer um jeito seguro de fazer backup e migração, sem refazer tudo à mão.

## O que você recebe

- **Painel**: estado do ambiente, contagem de skills, agentes, MCPs e perfis, tamanho em disco e alertas.
- **Scanner e diagnóstico**: descoberta somente-leitura de todos os artefatos; referências órfãs, MCPs quebrados,
  duplicados e arquivos que pesam demais no contexto; "Resolver problemas" propõe uma correção por achado e você
  aceita ou ignora cada uma, com backup automático.
- **Backup e restauração** em `.cem`: manifesto, somas de verificação, restauração seletiva e criptografia
  AES-256-GCM opcional.
- **Uso de tokens**: consumo real por sessão e projeto em 24 h, 3, 7 e 30 dias, lido dos transcritos locais, com
  propostas de melhoria.
- **Inventário do servidor** (somente leitura): CPU, discos, RAM, GPU NVIDIA (inclusive a VRAM que transborda
  para a RAM), conda, WSL, Docker, programas instalados e alertas de gargalo.
- **Perfis**, gerenciadores de MCP, skills, agentes e markdown, histórico e sincronização opcional por git.
- **CLI** `cem`: `scan`, `doctor`, `fix`, `backup`, `restore`, `verify`, `profiles`, `tokens`, `usage`,
  `mcp`, `history`, `sync` e outros.

## Instalação (resumo)

Pré-requisito: **Windows 10/11 64 bits** e cerca de 400 MB livres em disco. Nada mais — sem Node.js, sem
compilar, sem internet durante a instalação, sem permissão de administrador.

1. Na aba **Releases**, baixe `install_CEM-<versão>.exe` e, para conferir, o `.sha256`.
2. Confira a soma: `Get-FileHash .\install_CEM-<versão>.exe -Algorithm SHA256` tem de bater com o `.sha256`.
3. Dê dois cliques no instalador. O Windows avisa que o **editor é desconhecido** (o instalador não é assinado,
   e é por isso que existe a soma de verificação): **Mais informações → Executar assim mesmo**.
4. Leia a licença e aceite; escolha a pasta, se quiser mudar. O instalador cria o atalho **Claude Environment
   Manager** na Área de Trabalho e no menu Iniciar.
5. Abra pelo atalho. Na primeira abertura ele varre o seu ambiente (somente leitura) e mostra o Painel.

Passo a passo completo, o aviso do SmartScreen, o que é gravado onde, como desinstalar e problemas comuns:
[INSTALACAO.md](INSTALACAO.md).

### Linha de comando (opcional)

A CLI vai à parte, porque ela precisa de **Node.js 20 ou mais novo**. Baixe `cem-cli-<versão>.tgz` em
**Releases** e instale com `npm install -g .\cem-cli-<versão>.tgz`; depois, `cem --help`. Funciona também em
macOS e Linux.

## Configurar e usar

- O CEM começa só **olhando** o seu ambiente (somente leitura). Nada é apagado automaticamente.
- Para fazer backup: seção **Backup** → escolha a pasta de destino → (opcional) marque a criptografia e defina
  uma senha → **Criar backup**. Para restaurar: seção **Restore** → escolha o `.cem` → revise → restaure.
  Sem a senha, um `.cem` criptografado não tem recuperação.
- Preferências (tema, padrões de backup, privacidade) ficam em **Settings**.
- Atualizar: baixe o instalador da versão nova em **Releases** e execute. Ele atualiza por cima, mantendo as
  suas preferências e os seus backups.

## Licença

**PolyForm Strict 1.0.0** ([LICENSE](LICENSE)) — licença de **uso**: você pode baixar e usar o CEM
gratuitamente para fins **não comerciais** (pesquisa, ensino, uso pessoal, instituições sem fins lucrativos e
órgãos públicos). **Não é permitido** redistribuir cópias, modificar ou criar obras derivadas, nem usar o CEM em
atividade comercial ou vendê-lo. Para qualquer outro uso, fale com o autor. Programa de computador protegido
pela Lei 9.609/98, de autor único.

Required Notice: Copyright Luiz Dione Barbosa De-Melo (https://github.com/luizdione/Platform_CEM)

Esta licença vale a partir da versão 1.5.0. As versões até a 1.4.0 foram publicadas antes, sob licença MIT, e
continuam sob ela. Os componentes de terceiros embutidos no aplicativo (Electron, React e as demais
dependências) têm as próprias licenças.

## Autor

Luiz Dione Barbosa De-Melo — desenvolvedor e único titular do CEM. Dúvidas, relatos de problema e pedidos de
uso fora da licença: abra uma *issue* neste repositório.
