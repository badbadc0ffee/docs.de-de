---
title: ICorDebugHeapValue2::CreateHandle-Methode
ms.date: 03/30/2017
api_name:
- ICorDebugHeapValue2.CreateHandle
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugHeapValue2::CreateHandle
helpviewer_keywords:
- CreateHandle method [.NET Framework debugging]
- ICorDebugHeapValue2::CreateHandle method [.NET Framework debugging]
ms.assetid: fbc418e8-fa22-420d-84ec-e0e1800db041
topic_type:
- apiref
ms.openlocfilehash: b9eab1274f2d0ad562c0dec6adeddb85c6cfc458
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2019
ms.locfileid: "73138390"
---
# <a name="icordebugheapvalue2createhandle-method"></a>ICorDebugHeapValue2::CreateHandle-Methode
Erstellt ein Handle des angegebenen Typs für den Heap Wert, der durch dieses ICorDebugHeapValue2-Objekt dargestellt wird.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT CreateHandle (  
    [in] CorDebugHandleType      type,   
    [out] ICorDebugHandleValue   **ppHandle  
);  
```  
  
## <a name="parameters"></a>Parameter  
 `type`  
 in Ein Wert der CorDebugHandleType-Enumeration, der den Typ des zu erstellenden Handles angibt.  
  
 `ppHandle`  
 vorgenommen Ein Zeiger auf die Adresse eines ICorDebugHandleValue-Objekts, das das neue Handle für diesen Heapwert darstellt.  
  
## <a name="remarks"></a>Hinweise  
 Das Handle wird in der Anwendungsdomäne erstellt, die dem Heap Wert zugeordnet ist, und wird ungültig, wenn die Anwendungsdomäne entladen wird.  
  
 Mehrere Aufrufe dieser Funktion für denselben Heap Wert werden mehrere Handles erstellen. Da Handles die Leistung des Garbage Collector beeinflussen, sollte sich der Debugger auf eine relativ kleine Anzahl von Handles (etwa 256) beschränken, die gleichzeitig aktiv sind.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorDebug.idl, CorDebug.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
