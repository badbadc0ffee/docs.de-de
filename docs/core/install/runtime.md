---
title: Installieren von .NET Core-Runtime unter Windows, Linux und macOS (.NET Core)
description: Erfahren Sie. wie Sie .NET Core unter Windows, Linux und macOS installieren. Entdecken Sie die erforderlichen Abhängigkeiten, die für die Ausführung von .NET Core-Apps benötigt werden.
author: thraka
ms.author: adegeo
ms.date: 12/04/2019
ms.custom: updateeachrelease
zone_pivot_groups: operating-systems-set-one
ms.openlocfilehash: d36909e06bd9a3de0940c4c1b2b9eacbf9cafe7f
ms.sourcegitcommit: 9a97c76e141333394676bc5d264c6624b6f45bcf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2020
ms.locfileid: "75740596"
---
# <a name="install-the-net-core-runtime"></a>Installieren der .NET Core-Runtime

In diesem Artikel erfahren Sie, wie Sie die .NET Core-Runtime herunterladen und installieren. Die .NET Core-Runtime wird zur Ausführung der mit .NET Core erstellten Apps verwendet.

::: zone pivot="os-windows"

## <a name="install-with-an-installer"></a>Installieren mit einem Installer

Windows verfügt über eigenständige Installer, die zur Installation der .NET Core-Runtime 3.1 verwendet werden können:

- [x64-CPUs (64 Bit)](https://dotnet.microsoft.com/download/dotnet-core/3.1)
- [x86-CPUs (32 Bit)](https://dotnet.microsoft.com/download/dotnet-core/3.1)

::: zone-end

::: zone pivot="os-macos"

## <a name="install-with-an-installer"></a>Installieren mit einem Installer

macOS verfügt über eigenständige Installer, die zur Installation der .NET Core-Runtime 3.1 verwendet werden können:

- [x64-CPUs (64 Bit)](https://dotnet.microsoft.com/download/dotnet-core/3.1)

::: zone-end

::: zone pivot="os-linux"

## <a name="install-with-a-package-manager"></a>Installieren mit dem Paket-Manager

Sie können die .NET Core-Runtime mit vielen der allgemeinen Linux-Paket-Manager installieren. Weitere Informationen finden Sie unter [Linux-Paket-Manager: Installieren von .NET Core](linux-package-managers.md).

Die Installation mit einem Paket-Manager wird nur in der x64-Architektur unterstützt. Wenn Sie die .NET Core-Runtime mit einer anderen Architektur installieren (z. B. mit ARM), befolgen Sie die Anweisungen im Abschnitt [Herunterladen und manuelles Installieren](#download-and-manually-install). Weitere Informationen zu den unterstützten Architekturen finden Sie unter [.NET Core-Abhängigkeiten und -Anforderungen](dependencies.md).

## <a name="download-and-manually-install"></a>Herunterladen und manuelles Installieren

[Laden Sie zunächst ein .NET Core-Binärrelease herunter](#all-net-core-downloads), um die Runtime zu extrahieren und die .NET Core-CLI-Befehle im Terminal bereitzustellen. Öffnen Sie dann ein Terminal, und führen Sie die folgenden Befehle aus.

```bash
mkdir -p $HOME/dotnet && tar zxf aspnetcore-runtime-3.1.0-linux-x64.tar.gz -C $HOME/dotnet
export DOTNET_ROOT=$HOME/dotnet
export PATH=$PATH:$HOME/dotnet
```

> [!TIP]
> Mit den oben aufgeführten `export`-Befehlen werden nur die .NET Core-CLI-Befehle für die Terminalsitzung bereitgestellt, in der sie ausgeführt wurden.
>
> Sie können Ihr Shell-Profil bearbeiten, um diese Befehle dauerhaft hinzuzufügen. Für Linux sind verschiedene Shells verfügbar, die jeweils über ein anderes Profil verfügen. Zum Beispiel:
>
> - **Bash-Shell**: *~/.bash_profile*, *~/.bashrc*
> - **Korn-Shell**: *~/.kshrc* oder *.profile*
> - **Z-Shell**: *~/.kshrc* oder *.profile*
> 
> Bearbeiten Sie die geeignete Quelldatei für die Shell, und fügen Sie `:$HOME/dotnet` am Ende der vorhandenen `PATH`-Anweisung hinzu. Wenn keine `PATH`-Anweisung enthalten ist, fügen Sie eine neue Zeile mit `export PATH=$PATH:$HOME/dotnet` hinzu.
>
> Fügen Sie außerdem `export DOTNET_ROOT=$HOME/dotnet` am Ende der Datei hinzu.

::: zone-end

::: zone pivot="os-windows"

## <a name="install-with-powershell-automation"></a>Installieren mit PowerShell-Automatisierung

Die [dotnet-Installationsskripts](../tools/dotnet-install-script.md) werden für die Automatisierung und Installationen der Runtime von nicht-Administratoren verwendet. Sie können das Skript über die Seite [dotnet-install-Skriptverweis](../tools/dotnet-install-script.md) herunterladen.

Das Skript installiert standardmäßig die neueste [Langzeitunterstützungsversion](https://dotnet.microsoft.com/platform/support/policy/dotnet-core), nämlich .NET Core 3.1. Sie können eine bestimmte Version durch Angeben der `Channel`-Option auswählen. Schließen Sie die `Runtime`-Option mit ein, um eine Runtime zu installieren. Andernfalls installiert das Skript das [SDK](sdk.md) nicht.

```powershell
dotnet-install.ps1 -Channel 3.1 -Runtime aspnetcore
```

> [!NOTE]
> Durch den obigen Befehl wird die ASP.NET Core-Runtime für maximale Kompatibilität installiert. Die ASP.NET Core-Runtime enthält auch die .NET Core-Standardruntime.

::: zone-end

::: zone pivot="os-linux,os-macos"

## <a name="install-with-bash-automation"></a>Installieren mit der Bash-Automatisierung

Die [dotnet-Installationsskripts](../tools/dotnet-install-script.md) werden für die Automatisierung und Installationen der Runtime von nicht-Administratoren verwendet. Sie können das Skript über die Seite [dotnet-install-Skriptverweis](../tools/dotnet-install-script.md) herunterladen.

Das Skript installiert standardmäßig die neueste [Langzeitunterstützungsversion](https://dotnet.microsoft.com/platform/support/policy/dotnet-core), nämlich .NET Core 3.1. Sie können eine bestimmte Version durch Angeben der `current`-Option auswählen. Schließen Sie die `runtime`-Option mit ein, um eine Runtime zu installieren. Andernfalls installiert das Skript das [SDK](sdk.md) nicht.

```bash
./dotnet-install.sh --channel 3.1 --runtime aspnetcore
```

> [!NOTE]
> Durch den obigen Befehl wird die ASP.NET Core-Runtime für maximale Kompatibilität installiert. Die ASP.NET Core-Runtime enthält auch die .NET Core-Standardruntime.

::: zone-end

## <a name="all-net-core-downloads"></a>Alle .NET Core-Downloads

Sie können .NET Core direkt mit einem der folgenden Links herunterladen und installieren:

- [Downloads von .NET Core 3.1](https://dotnet.microsoft.com/download/dotnet-core/3.1)
- [Downloads von .NET Core 3.0](https://dotnet.microsoft.com/download/dotnet-core/3.0)
- [Downloads von .NET Core 2.2](https://dotnet.microsoft.com/download/dotnet-core/2.2)
- [Downloads von .NET Core 2.1](https://dotnet.microsoft.com/download/dotnet-core/2.1)

## <a name="docker"></a>Docker

Container bieten eine einfache Möglichkeit, Ihre Anwendung vom Rest des Hostsystems zu isolieren. Container auf demselben Computer teilen nur den Kernel und verwenden die Ihrer Anwendung zur Verfügung gestellten Ressourcen.

.NET Core kann in einem Docker-Container ausgeführt werden. Offizielle.NET Core Docker-Images werden in Microsoft Container Registry (MCR) veröffentlicht und sind im [Microsoft.NET Core Docker-Hub-Repository](https://hub.docker.com/_/microsoft-dotnet-core/) verfügbar. Jedes Repository enthält Images für verschiedene Kombinationen von .NET (SDK oder Runtime) und dem Betriebssystem, die Sie verwenden können.

Microsoft stellt Images bereit, die auf bestimmte Szenarien zugeschnitten sind. So stellt beispielsweise das [ASP.NET Core-Repository](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) Images bereit, die für die Ausführung von ASP.NET Core-Apps in der Produktion erstellt wurden.

Weitere Informationen zur Verwendung von .NET Core in einem Docker-Container finden Sie unter [Einführung in .NET und Docker](../docker/introduction.md) und [Beispiele](https://github.com/dotnet/dotnet-docker/blob/master/samples/README.md).

## <a name="next-steps"></a>Nächste Schritte

- [Überprüfen, ob .NET Core bereits installiert ist](how-to-detect-installed-versions.md)
