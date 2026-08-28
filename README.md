# Redefinição do ID e das configurações locais do AnyDesk

Este repositório contém scripts experimentais para Windows, Linux e macOS que interrompem o AnyDesk, alteram arquivos locais de configuração e iniciam o aplicativo novamente.

> [!IMPORTANT]
> Os scripts não instalam nem ativam uma licença do AnyDesk e não garantem a remoção de limitações aplicadas pelo serviço. Use-os somente em computadores que você administra, por sua conta e risco. Para uso frequente ou profissional, adquira uma licença oficial.

## O que foi implementado

| Sistema | Script | Comportamento atual |
| --- | --- | --- |
| Windows | `Anydesk-Reset.cmd` | Exige administrador, para o serviço e o processo, preserva `user.conf` e miniaturas, remove arquivos de configuração, reinicia o serviço para gerar um novo `system.conf` e restaura os dados preservados. |
| Linux | `anydesk_licenca.sh` | Exige `root`, para serviço e processos, salva `user.conf` e miniaturas, limpa a configuração em `$HOME/.anydesk`, espera um ID em `/etc/anydesk/system.conf` e restaura os dados salvos. |
| macOS | `reset_licenca_macos.sh` | Para o aplicativo, preserva `user.conf`, remove miniaturas, abre o AnyDesk, aguarda até 30 segundos por um ID em `system.conf` e restaura a configuração preservada. |

Em linhas gerais, o fluxo é:

1. Encerrar o serviço e os processos do AnyDesk.
2. Fazer uma cópia temporária de parte da configuração do usuário.
3. Remover configurações selecionadas.
4. Iniciar o AnyDesk e aguardar a recriação dos arquivos locais.
5. Restaurar os dados preservados e iniciar o aplicativo novamente.

## Requisitos

- AnyDesk já instalado.
- [Git](https://git-scm.com/downloads) para clonar o repositório.
- Permissão de administrador no Windows ou acesso a `sudo` no Linux/macOS.
- Acesso à internet para baixar o repositório GitHub [`luizaopy/Reset-AnyDesk`](https://github.com/luizaopy/Reset-AnyDesk).

## Instalação pela conta GitHub

Clone o repositório da conta `luizaopy`:

```bash
git clone https://github.com/luizaopy/Reset-AnyDesk.git
cd Reset-AnyDesk
```

Para atualizar uma cópia já instalada:

```bash
git pull origin main
```

## Execução no Windows

### Método automático pelo PowerShell

Abra o PowerShell, cole o comando abaixo e pressione **Enter**:

```powershell
$arquivo = Join-Path $env:TEMP "Anydesk-Reset.cmd"; Invoke-WebRequest -Uri "https://raw.githubusercontent.com/luizaopy/Reset-AnyDesk/main/Anydesk-Reset.cmd" -OutFile $arquivo; Start-Process -FilePath $arquivo -Verb RunAs -Wait
```

O script será baixado para a pasta temporária do Windows. Aceite a solicitação do Controle de Conta de Usuário para executá-lo como administrador.

> [!NOTE]
> O download funcionará depois que o repositório público `luizaopy/Reset-AnyDesk` e o arquivo `Anydesk-Reset.cmd` forem publicados na branch `main`.

### Método pelo repositório clonado

Abra o **PowerShell como administrador**, entre na pasta clonada e execute:

```powershell
.\Anydesk-Reset.cmd
```

Alternativamente, clique com o botão direito em `Anydesk-Reset.cmd` e escolha **Executar como administrador**.

## Execução no Linux

Depois de clonar o repositório:

```bash
chmod +x anydesk_licenca.sh
sudo ./anydesk_licenca.sh
```

> [!WARNING]
> No estado atual, o script usa `$HOME`. Ao executá-lo com `sudo`, esse caminho pode apontar para `/root` em vez da pasta do usuário que utiliza o AnyDesk. Confira o script e faça backup das configurações antes de executar.

## Execução no macOS

Depois de clonar o repositório:

```bash
chmod +x reset_licenca_macos.sh
./reset_licenca_macos.sh
```

O macOS poderá solicitar a senha de administrador ao tentar controlar o serviço.

## Limitações conhecidas

- O script do Windows aguarda indefinidamente a criação de `system.conf` com `ad.anynet.id=` caso o AnyDesk não consiga gerar esse arquivo.
- O script do Linux também não possui tempo limite nessa espera e pode usar o diretório pessoal de `root` quando executado com `sudo`.
- O script do macOS possui tempo limite, mas o identificador do serviço (`com.anydesk.anydesk`) pode variar conforme a versão/forma de instalação.
- Caminhos e nomes de serviço podem mudar entre versões do AnyDesk.
- Faça backup antes de executar. Configurações locais não contempladas pelo backup do script podem ser perdidas.

## Autoria

Projeto mantido por [@luizaopy](https://github.com/luizaopy).
