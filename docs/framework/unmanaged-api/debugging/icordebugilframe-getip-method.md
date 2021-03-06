---
title: ICorDebugILFrame::GetIP-Methode
ms.date: 03/30/2017
api_name:
- ICorDebugILFrame.GetIP
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugILFrame::GetIP
helpviewer_keywords:
- GetIP method, ICorDebugILFrame interface [.NET Framework debugging]
- ICorDebugILFrame::GetIP method [.NET Framework debugging]
ms.assetid: 18217ba1-1776-4297-a3b9-f77e64b0fead
topic_type:
- apiref
ms.openlocfilehash: 7e1605eede55360e72d65da6744bc1dcce4f107f
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2019
ms.locfileid: "73130989"
---
# <a name="icordebugilframegetip-method"></a>ICorDebugILFrame::GetIP-Methode
Ruft den Wert des Anweisungs Zeigers und einen bitweisen Kombinationswert ab, der beschreibt, wie der Wert des Anweisungs Zeigers abgerufen wurde.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT GetIP (  
    [out] ULONG32               *pnOffset,   
    [out] CorDebugMappingResult *pMappingResult  
);  
```  
  
## <a name="parameters"></a>Parameter  
 `pnOffset`  
 vorgenommen Der Wert des Anweisungs Zeigers.  
  
 `pMappingResult`  
 vorgenommen Ein Zeiger auf eine bitweise Kombination der cordbugmappingresult-Enumerationswerte, die beschreiben, wie der Wert des Anweisungs Zeigers abgerufen wurde.  
  
## <a name="remarks"></a>Hinweise  
 Der Wert des Anweisungs Zeigers ist der Offset des Stapel Rahmens im MSIL-Code (Microsoft Intermediate Language) der Funktion. Wenn der Stapel Rahmen aktiv ist, ist diese Adresse die nächste Anweisung, die ausgeführt werden soll. Wenn der Stapel Rahmen nicht aktiv ist, handelt es sich bei dieser Adresse um die nächste Anweisung, die ausgeführt werden soll, wenn der Stapel Rahmen erneut aktiviert wird.  
  
 Handelt es sich bei diesem Frame um einen JIT-kompilierten Frame (Just-in-Time), wird der Wert des Anweisungs Zeigers durch die Zuordnung rückwärts aus dem eigentlichen systemeigenen Anweisungs Zeiger bestimmt, sodass der Wert nur ungefähre Werte aufweisen kann.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorDebug.idl, CorDebug.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
