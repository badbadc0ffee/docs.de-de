---
title: Cert2spc.exe (Software Publisher Certificate Test-Tool)
ms.date: 03/30/2017
helpviewer_keywords:
- SPC
- Software Publisher Certificate Test tool
- Software Publisher Certificate
- Cert2spc.exe
- certificates, Software Publisher's Certificate
ms.assetid: be434d7d-9c0d-46e7-8392-58a9b542d11d
ms.openlocfilehash: 809b7d0383f172a5fbcb2ac4ac3ffb96ff0b8e20
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2019
ms.locfileid: "73129883"
---
# <a name="cert2spcexe-software-publisher-certificate-test-tool"></a>Cert2spc.exe (Software Publisher Certificate Test-Tool)
Das Software Publisher Certificate Test-Tool erstellt ein SPC (Software Publisher's Certificate, Softwareherausgeberzertifikat) aus einem oder mehreren X.509-Zertifikaten. "Cert2spc.exe" wird ausschließlich zu Textzwecken verwendet. Sie erhalten ein gültiges SPC von einer Zertifizierungsstelle, beispielsweise VeriSign oder Thawte. Weitere Informationen zum Erstellen von X.509-Zertifikaten finden Sie unter [Makecert.exe (Certificate Creation-Tool)](/windows/desktop/SecCrypto/makecert).  
  
 Dieses Tool wird automatisch mit Visual Studio installiert. Verwenden Sie die Developer-Eingabeaufforderung für Visual Studio (oder die Visual Studio-Eingabeaufforderung in Windows 7), um das Tool auszuführen. Weitere Informationen finden Sie unter [Eingabeaufforderungen](developer-command-prompt-for-vs.md).  
  
 Geben Sie an der Eingabeaufforderung Folgendes ein:  
  
## <a name="syntax"></a>Syntax  
  
```console  
cert2spc cert1.cer | crl1.crl [... certN.cer | crlN.crl] outputSPCfile.spc  
```  
  
## <a name="parameters"></a>Parameter  
  
|Argument|BESCHREIBUNG|  
|--------------|-----------------|  
|`certN.cer`|Der Name eines X.509-Zertifikats, das in die SPC-Datei eingebunden werden soll. Sie können mehrere Namen angeben, die durch Leerzeichen voneinander getrennt werden müssen.|  
|`crlN.crl`|Der Name einer Zertifikatssperrliste, die in die SPC-Datei aufgenommen werden soll. Sie können mehrere Namen angeben, die durch Leerzeichen voneinander getrennt werden müssen.|  
|`outputSPCfile.spc`|Der Name des PKCS #7-Objekts, das die X.509-Zertifikate enthält.|  
  
|Option|BESCHREIBUNG|  
|------------|-----------------|  
|**/?**|Zeigt Befehlssyntax und Optionen für das Tool an.|  
  
## <a name="examples"></a>Beispiele  
 Der folgende Befehl erstellt ein SPC aus `myCertificate.cer` und platziert es in `mySPCFile.spc`.  
  
```console
cert2spc myCertificate.cer mySPCFile.spc  
```  
  
 Der folgende Befehl erstellt ein SPC aus `oneCertificate.cer` und `twoCertificate.cer` und platziert es in `mySPCFile.spc`.  
  
```console
cert2spc oneCertificate.cer twoCertificate.cer mySPCFile.spc  
```  
  
## <a name="see-also"></a>Siehe auch

- [Extras](index.md)
- [Makecert.exe (Tool für die Zertifikaterstellung)](/windows/desktop/SecCrypto/makecert)
- [Eingabeaufforderungen](developer-command-prompt-for-vs.md)
