---
title: <startup>-Element
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/startup
- http://schemas.microsoft.com/.NetConfiguration/v2.0#startup
helpviewer_keywords:
- container tags, <startup> element
- <startup> element
- startup element
ms.assetid: 536acfd8-f827-452f-838a-e14fa3b87621
ms.openlocfilehash: 634d9c5248c33619abec50d441d95c111febdcbf
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2019
ms.locfileid: "71699415"
---
# <a name="startup-element"></a>\<startup >-Element

Gibt Common Language Runtime Startinformationen an.

[ **\<configuration>** ](../configuration-element.md)  
&nbsp;&nbsp; **\<startup>**  

## <a name="syntax"></a>Syntax

```xml
<startup useLegacyV2RuntimeActivationPolicy="true|false" > 
</startup>
```

## <a name="attributes-and-elements"></a>Attribute und Elemente

 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.

### <a name="attributes"></a>Attribute

|Attribut|Beschreibung|
|---------------|-----------------|
|`useLegacyV2RuntimeActivationPolicy`|Optionales Attribut.<br /><br /> Gibt an, ob die Richtlinie für die .NET Framework 2,0-Lauf Zeit Aktivierung aktiviert oder die .NET Framework 4-Aktivierungs Richtlinie verwendet werden soll.|

## <a name="uselegacyv2runtimeactivationpolicy-attribute"></a>useLegacyV2RuntimeActivationPolicy-Attribut

|Wert|Beschreibung|
|-----------|-----------------|
|`true`|Aktivieren Sie die Richtlinie für die .NET Framework 2,0-Lauf Zeit Aktivierung für die ausgewählte Laufzeit, die Legacy-Lauf Zeit Aktivierungs Techniken (z. b. die [CorBindToRuntimeEx-Funktion](../../../unmanaged-api/hosting/corbindtoruntimeex-function.md)) an die von der Konfigurationsdatei gewählte Laufzeit bindet, anstatt Sie bei der CLR zu untersuchen. Version 2,0. Wenn also CLR-Version 4 oder höher aus der Konfigurationsdatei ausgewählt wird, werden Assemblys im gemischten Modus, die mit früheren Versionen der .NET Framework erstellt wurden, mit der ausgewählten CLR-Version geladen. Durch Festlegen dieses Werts wird verhindert, dass CLR-Version 1,1 oder CLR-Version 2,0 in denselben Prozess geladen wird, wodurch die Prozess interne parallele Funktion deaktiviert wird.|
|`false`|Verwenden Sie die Standard Aktivierungs Richtlinie für die .NET Framework 4 und höher, damit ältere Lauf Zeit Aktivierungs Techniken die CLR-Version 1,1 oder 2,0 in den Prozess laden können. Durch Festlegen dieses Werts wird verhindert, dass Assemblys im gemischten Modus in die .NET Framework 4 oder höher geladen werden, es sei denn, Sie wurden mit dem .NET Framework 4 oder höher erstellt Dies ist der Standardwert.|

### <a name="child-elements"></a>Untergeordnete Elemente

|Element|Beschreibung|
|-------------|-----------------|
|[\<requiredRuntime>](requiredruntime-element.md)|Gibt an, dass die Anwendung nur Version 1.0 der Common Language Runtime unterstützt. Anwendungen, die mit der Runtime-Version 1,1 oder höher erstellt wurden, sollten das **\<supportedruntime->-** Element verwenden.|
|[\<supportedRuntime>](supportedruntime-element.md)|Gibt an, welche Versionen der Common Language Runtime von der Anwendung unterstützt werden.|

### <a name="parent-elements"></a>Übergeordnete Elemente

|Element|Beschreibung|
|-------------|-----------------|
|`configuration`|Das Stammelement in jeder von den Common Language Runtime- und .NET Framework-Anwendungen verwendeten Konfigurationsdatei.|

## <a name="remarks"></a>Hinweise

 Das **\<supportedruntime->** Element sollte von allen Anwendungen verwendet werden, die mit Version 1,1 oder höher der Laufzeit erstellt wurden. Anwendungen, die zur Unterstützung von nur Version 1,0 der Laufzeit erstellt wurden, müssen das **\<requirements druntime >-** Element verwenden.

 Der Startcode für eine in Microsoft Internet Explorer gehostete Anwendung ignoriert das **\<startup >-** Element und seine untergeordneten Elemente.

## <a name="the-uselegacyv2runtimeactivationpolicy-attribute"></a>Das useLegacyV2RuntimeActivationPolicy-Attribut

 Dieses Attribut ist nützlich, wenn Ihre Anwendung ältere Aktivierungs Pfade verwendet, wie z. b. die [CorBindToRuntimeEx-Funktion](../../../unmanaged-api/hosting/corbindtoruntimeex-function.md), und Sie möchten, dass diese Pfade Version 4 der CLR anstelle einer früheren Version aktivieren, oder wenn Ihre Anwendung mit .NET erstellt wurde. Framework 4, aber eine Abhängigkeit von einer Assembly im gemischten Modus, die mit einer früheren Version des .NET Framework erstellt wurde. Legen Sie in diesen Szenarien das-Attribut auf `true` fest.

> [!NOTE]
> Wenn das-Attribut auf `true` festgelegt wird, wird verhindert, dass CLR-Version 1,1 oder CLR-Version 2,0 in denselben Prozess geladen wird, wodurch die Prozess interne parallele Funktion deaktiviert wird (siehe parallele [Ausführung für COM-Interop](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/8t8td04t(v=vs.100))).

## <a name="example"></a>Beispiel

 Im folgenden Beispiel wird gezeigt, wie die Laufzeitversion in einer Konfigurationsdatei angegeben wird.

```xml
<!-- When used with version 1.0 of the .NET Framework runtime -->
<configuration>
   <startup>
      <requiredRuntime version="v1.0.3705" safemode="true"/>
   </startup>
</configuration>
<!-- When used with version 1.1 (or later) of the runtime -->
<configuration>
   <startup>
      <supportedRuntime version="v1.1.4322"/>
      <supportedRuntime version="v1.0.3705"/>
   </startup>
</configuration>
```

## <a name="see-also"></a>Siehe auch

- [Startup Settings Schema (Schema für Starteinstellungen)](index.md)
- [Konfigurationsdateischema](../index.md)
- [Vorgehensweise: Konfigurieren einer App zur Unterstützung von .NET Framework 4 oder höher](../../../migration-guide/how-to-configure-an-app-to-support-net-framework-4-or-4-5.md)
- [Parallele Ausführung für COM-Interop](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/8t8td04t(v=vs.100))
- [Prozessinterne parallele Ausführung](../../../deployment/in-process-side-by-side-execution.md)
