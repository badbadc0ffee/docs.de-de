---
title: <generatePublisherEvidence>-Element
ms.date: 03/30/2017
helpviewer_keywords:
- generatePublisherEvidence element
- <generatePublisherEvidence> element
ms.assetid: 7d208f50-e8d5-4a42-bc1a-1cf3590706a8
ms.openlocfilehash: b04ef53d6e9c3d954b0925ea8634b3d220b36af7
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2019
ms.locfileid: "73116576"
---
# <a name="generatepublisherevidence-element"></a>\<generatePublisherEvidence > Element
Gibt an, ob die Laufzeit <xref:System.Security.Policy.Publisher> Beweise für Code Zugriffssicherheit (CAS) erstellt.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp; &nbsp;[ **\<runtime >** ](runtime-element.md) \
&nbsp;&nbsp;&nbsp;&nbsp; **\<generatePublisherEvidence >**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<generatePublisherEvidence    
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### <a name="attributes"></a>Attribute  
  
|Attribut|Beschreibung|  
|---------------|-----------------|  
|`enabled`|Erforderliches Attribut.<br /><br /> Gibt an, ob die Laufzeit <xref:System.Security.Policy.Publisher> Beweis erstellt.|  
  
## <a name="enabled-attribute"></a>Enabled-Attribut  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|`false`|Erstellt keine <xref:System.Security.Policy.Publisher> Beweise.|  
|`true`|Erstellt <xref:System.Security.Policy.Publisher> Beweise. Dies ist die Standardeinstellung.|  
  
### <a name="child-elements"></a>Untergeordnete Elemente  
 Keine  
  
### <a name="parent-elements"></a>Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|-----------------|  
|`configuration`|Das Stammelement in jeder von den Common Language Runtime- und .NET Framework-Anwendungen verwendeten Konfigurationsdatei.|  
|`runtime`|Enthält Informationen über Laufzeitinitialisierungsoptionen.|  
  
## <a name="remarks"></a>Hinweise  
  
> [!NOTE]
> In der .NET Framework 4 und höher hat dieses Element keine Auswirkung auf die assemblyladezeiten. Weitere Informationen finden Sie im Abschnitt "Vereinfachung der Sicherheitsrichtlinie" unter " [Sicherheitsänderungen](../../../security/security-changes.md)".  
  
 Der Common Language Runtime (CLR) versucht, die Authenticode-Signatur zur Ladezeit zu überprüfen, um <xref:System.Security.Policy.Publisher> Beweise für die Assembly zu erstellen. Die meisten Anwendungen benötigen jedoch standardmäßig keine <xref:System.Security.Policy.Publisher> Beweise. Die Standard-CAS-Richtlinie beruht nicht auf der <xref:System.Security.Policy.PublisherMembershipCondition>. Vermeiden Sie unnötige Startkosten im Zusammenhang mit der Überprüfung der Herausgeber Signatur, es sei denn, Ihre Anwendung wird auf einem Computer mit einer benutzerdefinierten CAS-Richtlinie ausgeführt oder beabsichtigt, Anforderungen für <xref:System.Security.Permissions.PublisherIdentityPermission> in einer teilweise vertrauenswürdigen Umgebung zu erfüllen. (Ansprüche für Identitäts Berechtigungen sind immer erfolgreich in einer vollständig vertrauenswürdigen Umgebung.)  
  
> [!NOTE]
> Wir empfehlen, dass Dienste das `<generatePublisherEvidence>`-Element verwenden, um die Startleistung zu verbessern.  Mithilfe dieses Elements können auch Verzögerungen vermieden werden, die einen Timeout und den Abbruch des Dienst Starts verursachen können.  
  
## <a name="configuration-file"></a>Konfigurationsdatei  
 Dieses Element kann nur in der Anwendungs Konfigurationsdatei verwendet werden.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird gezeigt, wie das `<generatePublisherEvidence>`-Element verwendet wird, um die Prüfung der CAS-Herausgeber Richtlinie für eine Anwendung zu deaktivieren  
  
```xml  
<configuration>  
    <runtime>  
        <generatePublisherEvidence enabled="false"/>  
    </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>Siehe auch

- [Schema für Laufzeiteinstellungen](index.md)
- [Konfigurationsdateischema](../index.md)
