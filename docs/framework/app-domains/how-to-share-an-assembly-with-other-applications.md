---
title: 'Vorgehensweise: Verwenden einer Assembly mit anderen Anwendungen'
ms.date: 08/19/2019
ms.assetid: c30e972b-1693-4e05-b115-c31831fdf9f2
ms.openlocfilehash: b1ef195458dd2de95eeb5e25089339e55d9e3fbb
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972882"
---
# <a name="how-to-share-an-assembly-with-other-applications"></a><span data-ttu-id="90575-102">Vorgehensweise: Verwenden einer Assembly mit anderen Anwendungen</span><span class="sxs-lookup"><span data-stu-id="90575-102">How to: Share an assembly with other applications</span></span>
<span data-ttu-id="90575-103">Assemblys können sowohl privat als auch freigegeben sein: Standardmäßig bestehen die meisten einfachen Programme aus einer privaten Assembly, da sie nicht für den Gebrauch durch andere Anwendungen vorgesehen sind.</span><span class="sxs-lookup"><span data-stu-id="90575-103">Assemblies can be private or shared: by default, most simple programs consist of a private assembly because they are not intended to be used by other applications.</span></span>  

<span data-ttu-id="90575-104">Wenn Sie eine Assembly mit anderen Anwendungen verwenden möchten, muss diese in den [globalen Assemblycache](gac.md) eingefügt werden.</span><span class="sxs-lookup"><span data-stu-id="90575-104">In order to share an assembly with other applications, it must be placed in the [global assembly cache (GAC)](gac.md).</span></span>  
  
<span data-ttu-id="90575-105">So nutzen Sie eine Assembly mit anderen Anwendungen:</span><span class="sxs-lookup"><span data-stu-id="90575-105">To share an assembly:</span></span>
  
1. <span data-ttu-id="90575-106">Erstellen Ihrer Assembly.</span><span class="sxs-lookup"><span data-stu-id="90575-106">Create your assembly.</span></span> <span data-ttu-id="90575-107">Weitere Informationen finden Sie unter [Erstellen von Assemblys](../../standard/assembly/create.md).</span><span class="sxs-lookup"><span data-stu-id="90575-107">For more information, see [Create assemblies](../../standard/assembly/create.md).</span></span>  
  
2. <span data-ttu-id="90575-108">Weisen Sie Ihrer Assembly einen starken Namen zu.</span><span class="sxs-lookup"><span data-stu-id="90575-108">Assign a strong name to your assembly.</span></span> <span data-ttu-id="90575-109">Weitere Informationen finden Sie unter [Vorgehensweise: Signieren einer Assembly mit einem starken Namen](../../standard/assembly/sign-strong-name.md).</span><span class="sxs-lookup"><span data-stu-id="90575-109">For more information, see [How to: Sign an assembly with a strong name](../../standard/assembly/sign-strong-name.md).</span></span>  
  
3. <span data-ttu-id="90575-110">Weisen Sie Ihrer Assembly Versionsinformationen zu.</span><span class="sxs-lookup"><span data-stu-id="90575-110">Assign version information to your assembly.</span></span> <span data-ttu-id="90575-111">Weitere Informationen dazu finden Sie unter [Versionsverwaltung für Assemblys](../../standard/assembly/versioning.md).</span><span class="sxs-lookup"><span data-stu-id="90575-111">For more information, see [Assembly versioning](../../standard/assembly/versioning.md).</span></span>  
  
4. <span data-ttu-id="90575-112">Fügen Sie Ihre Assembly in den globalen Assemblycache ein.</span><span class="sxs-lookup"><span data-stu-id="90575-112">Add your assembly to the global assembly cache.</span></span> <span data-ttu-id="90575-113">Weitere Informationen finden Sie unter [Vorgehensweise: Installieren einer Assembly im globalen Assemblycache](install-assembly-into-gac.md).</span><span class="sxs-lookup"><span data-stu-id="90575-113">For more information, see [How to: Install an assembly into the global assembly cache](install-assembly-into-gac.md).</span></span>  
  
5. <span data-ttu-id="90575-114">Greifen Sie über andere Anwendungen auf die Typen in der Assembly zu.</span><span class="sxs-lookup"><span data-stu-id="90575-114">Access the types contained in the assembly from other applications.</span></span> <span data-ttu-id="90575-115">Weitere Informationen finden Sie unter [Vorgehensweise: Verweisen auf eine Assembly mit starkem Namen](../../standard/assembly/reference-strong-named.md).</span><span class="sxs-lookup"><span data-stu-id="90575-115">For more information, see [How to: Reference a strong-named assembly](../../standard/assembly/reference-strong-named.md).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="90575-116">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="90575-116">See also</span></span>

- [<span data-ttu-id="90575-117">C#-Programmierhandbuch</span><span class="sxs-lookup"><span data-stu-id="90575-117">C# programming guide</span></span>](../../../api/index.md)
- [<span data-ttu-id="90575-118">Programmierkonzepte (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="90575-118">Programming concepts (Visual Basic)</span></span>](../../../api/index.md)
- [<span data-ttu-id="90575-119">Programmieren mit Assemblys</span><span class="sxs-lookup"><span data-stu-id="90575-119">Program with assemblies</span></span>](../../standard/assembly/program.md)