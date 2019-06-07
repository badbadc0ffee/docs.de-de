---
title: Automatisiertes Machine Learning mit ML.NET
description: Übersicht über die automatische Modellauswahl und das Training
author: natke
ms.date: 05/01/2019
ms.topic: overview
ms.custom: mvc
ms.author: nakersha
ms.openlocfilehash: e6654718f174c9d8b628b05d85d74952c222eb66
ms.sourcegitcommit: 4c10802ad003374641a2c2373b8a92e3c88babc8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/08/2019
ms.locfileid: "65452731"
---
# <a name="automated-machine-learning-with-mlnet"></a><span data-ttu-id="a2591-103">Automatisiertes Machine Learning mit ML.NET</span><span class="sxs-lookup"><span data-stu-id="a2591-103">Automated machine learning with ML.NET</span></span>

<span data-ttu-id="a2591-104">Automatisiertes Machine Learning ist eine Funktion von ML.NET, die eine automatische Modellauswahl und das Training durchführt.</span><span class="sxs-lookup"><span data-stu-id="a2591-104">Automated machine learning is a feature of ML.NET that performs automatic model selection and training.</span></span> <span data-ttu-id="a2591-105">Sie geben den Machine Learning-Task an, stellen das Dataset bereit, und automatisierte ML wählt das Modell mit den besten Metriken aus.</span><span class="sxs-lookup"><span data-stu-id="a2591-105">You specify the machine learning task and supply a dataset, and automated ML chooses the model with the best metrics.</span></span> <span data-ttu-id="a2591-106">Ausgabe:</span><span class="sxs-lookup"><span data-stu-id="a2591-106">It outputs:</span></span>
- <span data-ttu-id="a2591-107">eine Modelldatei, die in die Vorhersageanwendung geladen werden kann</span><span class="sxs-lookup"><span data-stu-id="a2591-107">a model file that can be loaded into your prediction application</span></span>
- <span data-ttu-id="a2591-108">Anwendungscode, um Vorhersagen zu treffen</span><span class="sxs-lookup"><span data-stu-id="a2591-108">application code to make predictions</span></span>
- <span data-ttu-id="a2591-109">den Quellcode für die Funktionsauswahl und das Modelltraining (um das Modell zu verstehen)</span><span class="sxs-lookup"><span data-stu-id="a2591-109">the source code used for feature selection and model training (to understand the model)</span></span>

> [!NOTE]
> <span data-ttu-id="a2591-110">Dieses Feature befindet sich derzeit in der Vorschauphase, und das Material kann jederzeit geändert werden.</span><span class="sxs-lookup"><span data-stu-id="a2591-110">This feature is currently in Preview, and material may be subject to change.</span></span> 

<span data-ttu-id="a2591-111">Das automatisierte ML ist derzeit auf Machine Learning-[Tasks](resources/tasks.md) für binäre Klassifikation, Multiklassenklassifizierung und Regression beschränkt.</span><span class="sxs-lookup"><span data-stu-id="a2591-111">Automated ML is currently limited to the machine learning [tasks](resources/tasks.md) of binary classification, multiclass classification, and regression.</span></span> <span data-ttu-id="a2591-112">Andere Machine Learning-Tasks werden in zukünftigen Versionen unterstützt.</span><span class="sxs-lookup"><span data-stu-id="a2591-112">The other machine learning tasks will be supported in future releases.</span></span>

<span data-ttu-id="a2591-113">Es gibt drei Möglichkeiten, automatisiertes ML zu verwenden:</span><span class="sxs-lookup"><span data-stu-id="a2591-113">There are three ways to use automated ML:</span></span>
1. <span data-ttu-id="a2591-114">Über die Befehlszeile mit der [ML.NET CLI](automate-training-with-cli.md)</span><span class="sxs-lookup"><span data-stu-id="a2591-114">On the command line, with the [ML.NET CLI](automate-training-with-cli.md)</span></span>
1. <span data-ttu-id="a2591-115">Über eine Anwendung mit der [automatisierten ML-API](how-to-guides/how-to-use-the-automl-api.md)</span><span class="sxs-lookup"><span data-stu-id="a2591-115">Via an application, with the [automated ML API](how-to-guides/how-to-use-the-automl-api.md)</span></span>
1. <span data-ttu-id="a2591-116">Über eine grafische Benutzeroberfläche mit dem ML.NET Modell-Generator</span><span class="sxs-lookup"><span data-stu-id="a2591-116">With a graphical user interface, with the the ML.NET Model Builder</span></span>