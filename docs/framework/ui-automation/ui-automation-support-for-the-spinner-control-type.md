---
title: Benutzeroberflächenautomatisierungs-Unterstützung für den Drehfeld-Steuerelementtyp
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, Spinner control type
- Spinner control type
- control types, Spinner
ms.assetid: 3a29d185-65d8-42e3-bcc3-7f43e96f40c5
ms.openlocfilehash: 189773525a448befe670e2a62a1ee4134ff71b0f
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76785964"
---
# <a name="ui-automation-support-for-the-spinner-control-type"></a>Benutzeroberflächenautomatisierungs-Unterstützung für den Drehfeld-Steuerelementtyp
> [!NOTE]
> Diese Dokumentation ist für .NET Framework-Entwickler vorgesehen, die die verwalteten [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]-Klassen verwenden möchten, die im <xref:System.Windows.Automation>-Namespace definiert sind. Aktuelle Informationen zur [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]finden Sie auf der Seite zur [Windows-Automatisierungs-API: UI-Automatisierung](/windows/win32/winauto/entry-uiauto-win32).  
  
 Dieses Thema enthält Informationen zur [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] -Unterstützung für den Steuerelementtyp „Spinner“. In [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]umfasst ein Steuerelementtyp eine Reihe von Bedingungen, die ein Steuerelement erfüllen muss, damit die <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty> -Eigenschaft verwendet werden kann. Die Bedingungen schließen bestimmte Richtlinien für [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] -Struktur, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] -Eigenschaftswerte und Steuerelementmuster ein.  
  
 Spinner-Steuerelemente werden dazu verwendet, um aus einem Bereich von Elementen oder Zahlen auszuwählen.  
  
 In den folgenden Abschnitten werden die [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] -Struktur, -Eigenschaften, -Steuerelementmuster und -Ereignisse definiert, die für den Steuerelementtyp „Spinner“ erforderlich sind. Die [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] Anforderungen gelten für alle Spinner-Steuerelemente, ob [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], Win32 oder Windows Forms.  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## <a name="required-ui-automation-tree-structure"></a>Erforderliche Benutzeroberflächenautomatisierungs-Struktur  
 In der folgende Tabelle wird die Steuerelementansicht und Inhaltsansicht der [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] -Struktur dargestellt, die für Spinner-Steuerelemente gelten, wenn sie die „Range Value“-, „Value“- und „Selection“-Steuerelementmuster unterstützen und beschreiben, was in der jeweiligen Ansicht enthalten sein kann. Weitere Informationen zur [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] -Struktur finden Sie unter [UI Automation Tree Overview](ui-automation-tree-overview.md).  
  
 **„Range Value“- oder „Value“-Steuerelementmuster**  
  
|Steuerelementansicht|Inhaltsansicht|  
|------------------|------------------|  
|Spinner<br /><br /> -Edit (0 oder 1)<br />-Schaltfläche (2)|Spinner|  
  
 **Selection-Steuerelementmuster**  
  
|Steuerelementansicht|Inhaltsansicht|  
|------------------|------------------|  
|Spinner<br /><br /> -Edit (0 oder 1)<br />-Schaltfläche (2)<br />-List item (0 oder mehr)|Spinner<br /><br /> -ListItem (0 oder mehr)|  
  
 Um sicherzustellen, dass die beiden Schaltflächen in der Teilstruktur der Steuerelement Ansicht von automatisierten Testtools unterschieden werden können, weisen Sie die `SmallIncrement` oder `SmallDecrement` `AutomationId` entsprechend zu. Bei einigen Implementierungen ist das zugeordnete Edit-Steuerelement möglicherweise ein Peer des Spinner-Steuerelements.  
  
<a name="Required_UI_Automation_Properties"></a>   
## <a name="required-ui-automation-properties"></a>Erforderliche Benutzeroberflächenautomatisierungs-Eigenschaften  
 In der folgenden Tabelle werden die [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] -Eigenschaften aufgelistet, deren Wert oder Definition für Spinner-Steuerelemente besonders relevant ist. Weitere Informationen zu [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] Eigenschaften finden Sie unter [Benutzeroberflächenautomatisierungs-Eigenschaften für Clients](ui-automation-properties-for-clients.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] -Eigenschaft|{2&gt;Wert&lt;2}|Hinweise|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|Siehe Hinweise.|Der Wert dieser Eigenschaft muss für alle Steuerelemente in einer Anwendung eindeutig sein.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Siehe Hinweise.|Das äußere Rechteck, das das gesamte Steuerelement enthält.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|Siehe Hinweise.|Der durch Klicken aktivierbare Punkt des Spinner-Steuerelements übergibt den Fokus an den Bearbeitungsbereich des Steuerelements.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|Siehe Hinweise.|Wenn das Steuerelement den Tastaturfokus erhalten kann, muss es diese Eigenschaft unterstützen.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|Siehe Hinweise.|Das Spinner-Steuerelement ruft seinen Namen in der Regel aus einer statischen Textbezeichnung ab.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|Siehe Hinweise.|Spinner-Steuerelemente verfügen über eine statische Textbezeichnung.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|Spinner|Dieser Wert ist für alle Benutzeroberflächen-Frameworks gleich.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|„Drehfeld“|Lokalisierte Zeichenfolge für den Steuerelementtyp „Spinner“.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|Das Spinner-Steuerelement muss immer ein Inhaltselement sein.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|Das Spinner-Steuerelement muss immer ein Steuerelement sein.|  
  
<a name="Required_UI_Automation_Control_Patterns_and_Properties"></a>   
## <a name="required-ui-automation-control-patterns-and-properties"></a>Erforderliche Benutzeroberflächenautomatisierungs-Steuerelementmuster und -Eigenschaften  
 In der folgenden Tabelle werden die [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] -Steuerelementmuster aufgelistet, die von allen Spinner-Steuerelementen unterstützt werden müssen. Weitere Informationen zu Steuerelementmustern finden Sie unter [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md).  
  
|Steuerelementmuster/Mustereigenschaft|Unterstützung/Wert|Hinweise|  
|---------------------------------------|--------------------|-----------|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider>|Variabel|Spinner-Steuerelemente mit einer zur Auswahl stehenden Liste von Elementen müssen dieses Muster unterstützen.|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.CanSelectMultiple%2A>|Falsch|Spinner-Steuerelemente sind immer Einfachauswahlcontainer.|  
|<xref:System.Windows.Automation.Provider.IRangeValueProvider>|Variabel|Spinner-Steuerelemente, die einen numerischen Bereich umfassen, können dieses Muster unterstützen.|  
|<xref:System.Windows.Automation.Provider.IValueProvider>|Variabel|Spinner-Steuerelemente, die einen einzelnen Satz von Optionen oder Zahlen umfassen, können dieses Muster unterstützen.|  
  
<a name="Required_UI_Automation_Events"></a>   
## <a name="required-ui-automation-events"></a>Erforderliche Benutzeroberflächenautomatisierungs-Ereignisse  
 Die folgende Tabelle enthält die [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] -Ereignisse, die von allen Spinner-Steuerelementen unterstützt werden müssen. Weitere Informationen zu Ereignissen finden Sie unter [UI Automation Events Overview](ui-automation-events-overview.md).  
  
|[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] -Ereignis|-Unterstützung|Hinweise|  
|---------------------------------------------------------------------------------|-------------|-----------|  
|<xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent>|Variabel|Keine|  
|Durch geänderte<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> -Eigenschaft ausgelöstes Ereignis.|Erforderlich|Keine|  
|Durch geänderte<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> -Eigenschaft ausgelöstes Ereignis.|Erforderlich|Keine|  
|Durch geänderte<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> -Eigenschaft ausgelöstes Ereignis.|Erforderlich|Keine|  
|Durch geänderte<xref:System.Windows.Automation.ValuePatternIdentifiers.ValueProperty> -Eigenschaft ausgelöstes Ereignis.|Variabel|Keine|  
|Durch geänderte<xref:System.Windows.Automation.RangeValuePatternIdentifiers.ValueProperty> -Eigenschaft ausgelöstes Ereignis.|Variabel|Keine|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Erforderlich|Keine|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Erforderlich|Keine|  
  
## <a name="see-also"></a>Siehe auch

- <xref:System.Windows.Automation.ControlType.Spinner>
- [Übersicht über Steuerelementtypen für Benutzeroberflächenautomatisierung](ui-automation-control-types-overview.md)
- [Übersicht über die Benutzeroberflächenautomatisierung](ui-automation-overview.md)
