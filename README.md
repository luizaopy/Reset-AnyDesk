# Reset AnyDesk

Use o comando correspondente ao seu sistema operacional. Não é necessário baixar ou clonar este repositório.

> [!IMPORTANT]
> O AnyDesk precisa estar instalado. Execute somente em um computador que você administra e faça backup das configurações importantes.

## Windows — PowerShell

Abra o **PowerShell**, copie o comando completo abaixo, cole e pressione **Enter**. Quando o Windows solicitar, aceite a execução como administrador.

```powershell
$arquivo = Join-Path $env:TEMP "Anydesk-Reset.cmd"; Invoke-WebRequest -UseBasicParsing -Uri "https://raw.githubusercontent.com/luizaopy/Reset-AnyDesk/main/Anydesk-Reset.cmd" -OutFile $arquivo; Start-Process -FilePath $arquivo -Verb RunAs -Wait
```

## Linux — Terminal

Abra o **Terminal**, copie o comando completo abaixo, cole e pressione **Enter**. Digite sua senha quando solicitado.

```bash
arquivo="$(mktemp)" && curl -fsSL "https://raw.githubusercontent.com/luizaopy/Reset-AnyDesk/main/anydesk_licenca.sh" -o "$arquivo" && sudo env HOME="$HOME" bash "$arquivo"; rm -f "$arquivo"
```

## macOS — Terminal

Abra o **Terminal**, copie o comando completo abaixo, cole e pressione **Enter**. Digite sua senha se o macOS solicitar.

```bash
arquivo="$(mktemp)" && curl -fsSL "https://raw.githubusercontent.com/luizaopy/Reset-AnyDesk/main/reset_licenca_macos.sh" -o "$arquivo" && bash "$arquivo"; rm -f "$arquivo"
```
