---
title: ICorDebugAppDomain3 Interface
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain3
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain3
helpviewer_keywords:
- ICorDebugAppDomain3 interface [.NET Framework debugging]
ms.assetid: 875ef5be-c1e7-4d95-97e9-d3a667aeaba0
topic_type:
- apiref
ms.openlocfilehash: 1aaccb37ec61ed1ba6a7e6e1f508704973117cca
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2020
ms.locfileid: "76784880"
---
# <a name="icordebugappdomain3-interface"></a>ICorDebugAppDomain3 Interface
Stellt Methoden zum Abrufen von Informationen über die verwalteten Darstellungen von Windows-Runtime Typen bereit, die derzeit in einer Anwendungsdomäne geladen sind. Diese Schnittstelle ist eine Erweiterung der ICorDebugAppDomain-Schnittstelle und der ICorDebugAppDomain2-Schnittstelle.  
  
## <a name="methods"></a>Methoden  
  
|-Methode|Beschreibung|  
|------------|-----------------|  
|[ICorDebugAppDomain3::GetCachedWinRTTypes](icordebugappdomain3-getcachedwinrttypes-method.md)|Ruft einen Enumerator für alle zwischengespeicherten Windows-Runtime Typen ab.|  
|[ICorDebugAppDomain3::GetCachedWinRTTypesForIIDs](icordebugappdomain3-getcachedwinrttypesforiids-method.md)|Ruft einen Enumerator für zwischengespeicherte Windows-Runtime Typen in einer Anwendungsdomäne auf der Grundlage ihrer Schnittstellen Bezeichner ab.|  
  
## <a name="remarks"></a>Hinweise  
 Diese Schnittstelle soll von einem Debugger in Verbindung mit einem Funktions Auswertungs Aufruf`M:System.Runtime.InteropServices.Marshal.GetInspectableIIDs(System.Object)`verwendet werden. Wenn die-Methode die von einem Windows-Runtime Server-Objekt unterstützten Schnittstellen Bezeichner abruft, verwendet der Debugger möglicherweise die in dieser Schnittstelle definierten Methoden, um Sie verwalteten Typen zuzuordnen, die diesen Schnittstellen entsprechen.  
  
 Um eine Instanz dieser Schnittstelle abzurufen, führen Sie `QueryInterface` für eine Instanz der ICorDebugAppDomain-oder ICorDebugAppDomain2-Schnittstelle aus.  
  
> [!NOTE]
> Diese Schnittstelle kann weder computerübergreifend noch prozessübergreifend remote aufgerufen werden.  
  
## <a name="requirements"></a>-Anforderungen  
 **Plattformen:** Windows-Runtime  
  
 **Header:** CorDebug.idl, CorDebug.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework Versionen:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch

- [Debuggen von Schnittstellen](debugging-interfaces.md)
