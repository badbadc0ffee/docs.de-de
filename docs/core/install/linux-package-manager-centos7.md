---
title: Installieren von .NET Core auf CentOS 7 mit einem Paket-Manager (.NET Core)
description: Verwenden Sie einen Paket-Manager, um das .NET Core SDK und die -Runtime auf CentOS 7 zu installieren.
author: thraka
ms.author: adegeo
ms.date: 12/04/2019
ms.openlocfilehash: 66e78aadf933d3e10b99e3d2c7258733e96164f6
ms.sourcegitcommit: cdf5084648bf5e77970cbfeaa23f1cab3e6e234e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/01/2020
ms.locfileid: "76920858"
---
# <a name="centos-7-package-manager---install-net-core"></a>CentOS 7-Paket-Manager: Installieren von .NET Core

[!INCLUDE [package-manager-switcher](./includes/package-manager-switcher.md)]

In diesem Artikel wird beschrieben, wie Sie mit einem Paket-Manager .NET Core auf CentOS 7 installieren. Wenn Sie die Runtime installieren, wird die Installation der [ASP.NET Core-Runtime](#install-the-aspnet-core-runtime) empfohlen, da diese sowohl .NET Core- als auch ASP.NET Core-Runtimes umfasst.

## <a name="register-microsoft-key-and-feed"></a>Registrieren von Microsoft-Schlüsseln und -Feeds

Vor der Installation von .NET müssen Sie folgende Schritte ausführen:

- Registrieren Sie den Microsoft-Schlüssel.
- Registrieren Sie das Produktrepository.
- Installieren Sie erforderliche Abhängigkeiten.

Dies muss nur einmal pro Computer ausgeführt werden.

Öffnen Sie ein Terminal, und führen Sie den folgenden Befehl aus.

```bash
sudo rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm
```

## <a name="install-the-net-core-sdk"></a>Installieren des .NET Core SDK

Aktualisieren Sie die zur Installation verfügbaren Produkte, und installieren Sie dann das .NET Core SDK. Führen Sie in Ihrem Terminal den folgenden Befehl aus.

```bash
sudo yum install dotnet-sdk-3.1
```

## <a name="install-the-aspnet-core-runtime"></a>Installieren der ASP.NET Core-Runtime

Aktualisieren Sie die zur Installation verfügbaren Produkte, und installieren Sie dann die ASP.NET-Runtime. Führen Sie in Ihrem Terminal den folgenden Befehl aus.

```bash
sudo yum install aspnetcore-runtime-3.1
```

## <a name="install-the-net-core-runtime"></a>Installieren der .NET Core-Runtime

Aktualisieren Sie die zur Installation verfügbaren Produkte, und installieren Sie dann die .NET Core-Runtime. Führen Sie in Ihrem Terminal den folgenden Befehl aus.

```bash
sudo yum install dotnet-runtime-3.1
```

## <a name="how-to-install-other-versions"></a>Installieren anderer Versionen

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]

## <a name="troubleshoot-the-package-manager"></a>Problembehandlung des Paket-Managers

Dieser Abschnitt enthält Informationen zu häufigen Fehlern, die bei der Verwendung des Paket-Managers zur Installation von .NET Core auftreten können.

### <a name="failed-to-fetch"></a>Fehler beim Abrufen

[!INCLUDE [package-manager-failed-to-fetch-rpm](includes/package-manager-failed-to-fetch-rpm.md)]
