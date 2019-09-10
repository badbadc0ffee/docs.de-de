---
title: Einführung in Docker
description: Dieser Artikel bietet eine Einführung und einen Überblick über Docker im Rahmen einer.NET Core-Anwendung.
ms.date: 03/20/2019
ms.custom: mvc, seodec18
ms.openlocfilehash: 5da71215e3b539f10993677d23d89e2b8a49cb39
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/07/2019
ms.locfileid: "70799356"
---
# <a name="introduction-to-net-and-docker"></a><span data-ttu-id="69da8-103">Einführung zu .NET und Docker</span><span class="sxs-lookup"><span data-stu-id="69da8-103">Introduction to .NET and Docker</span></span>

<span data-ttu-id="69da8-104">.NET Core kann problemlos in einem Docker-Container ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="69da8-104">.NET Core can easily run in a Docker container.</span></span> <span data-ttu-id="69da8-105">Container bieten eine schlanke Möglichkeit, Ihre Anwendung vom Rest des Hostsystems zu isolieren, indem sie nur den Kernel gemeinsam nutzen und Ressourcen verwenden, die Ihrer Anwendung zur Verfügung gestellt werden.</span><span class="sxs-lookup"><span data-stu-id="69da8-105">Containers provide a lightweight way to isolate your application from the rest of the host system, sharing just the kernel, and using resources given to your application.</span></span> <span data-ttu-id="69da8-106">Wenn Sie mit Docker nicht vertraut sind, wird dringend empfohlen, die [Übersichtsdokumentation](https://docs.docker.com/engine/docker-overview/) von Docker zu lesen.</span><span class="sxs-lookup"><span data-stu-id="69da8-106">If you're unfamiliar with Docker, it's highly recommended that you read through Docker's [overview documentation](https://docs.docker.com/engine/docker-overview/).</span></span>

<span data-ttu-id="69da8-107">Weitere Informationen dazu, wie Sie Docker installieren, finden Sie auf der Downloadseite für [Docker Desktop: Community Edition](https://www.docker.com/products/docker-desktop).</span><span class="sxs-lookup"><span data-stu-id="69da8-107">For more information about how to install Docker, see the download page for [Docker Desktop: Community Edition](https://www.docker.com/products/docker-desktop).</span></span>

## <a name="docker-basics"></a><span data-ttu-id="69da8-108">Docker-Grundlagen</span><span class="sxs-lookup"><span data-stu-id="69da8-108">Docker basics</span></span>

<span data-ttu-id="69da8-109">Es gibt einige Konzepte, die Sie kennen sollten.</span><span class="sxs-lookup"><span data-stu-id="69da8-109">There are a few concepts you should be familiar with.</span></span> <span data-ttu-id="69da8-110">Der Docker-Client verfügt über ein Befehlszeilen-Schnittstellenprogramm, mit dem Sie Images und Container verwalten können.</span><span class="sxs-lookup"><span data-stu-id="69da8-110">The Docker client has a command line interface program you use to manage images and containers.</span></span> <span data-ttu-id="69da8-111">Wie bereits erwähnt, sollten Sie sich die Zeit nehmen, die [Übersichtsdokumentation](https://docs.docker.com/engine/docker-overview/) zu Docker zu lesen.</span><span class="sxs-lookup"><span data-stu-id="69da8-111">As previously stated, you should take the time to read through the [Docker overview](https://docs.docker.com/engine/docker-overview/) documentation.</span></span> 

### <a name="images"></a><span data-ttu-id="69da8-112">Bilder</span><span class="sxs-lookup"><span data-stu-id="69da8-112">Images</span></span>

<span data-ttu-id="69da8-113">Ein Image ist eine geordnete Auflistung von Dateisystemänderungen, die die Grundlage für einen Container bilden.</span><span class="sxs-lookup"><span data-stu-id="69da8-113">An image is an ordered collection of filesystem changes that form the basis of a container.</span></span> <span data-ttu-id="69da8-114">Das Image weist keinen Zustand auf und ist schreibgeschützt.</span><span class="sxs-lookup"><span data-stu-id="69da8-114">The image doesn't have a state and is read-only.</span></span> <span data-ttu-id="69da8-115">Meistens basiert ein Image auf einem anderen Image, allerdings mit einer gewissen Anpassung.</span><span class="sxs-lookup"><span data-stu-id="69da8-115">Much the time an image is based on another image, but with some customization.</span></span> <span data-ttu-id="69da8-116">Wenn Sie beispielsweise ein neues Image für Ihre Anwendung erstellen, würden Sie als Grundlage ein vorhandenes Image verwenden, das bereits die .NET Core Runtime enthält.</span><span class="sxs-lookup"><span data-stu-id="69da8-116">For example, when you create an new image for your application, you would base it on an existing image that already contains the .NET Core runtime.</span></span>

<span data-ttu-id="69da8-117">Da Container aus Images erstellt werden, weisen Images eine Reihe von Ausführungsparametern auf (z.B. eine startende ausführbare Datei), die beim Start des Containers ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="69da8-117">Because containers are created from images, images have a set of run parameters (such as a starting executable) that run when the container starts.</span></span>

### <a name="containers"></a><span data-ttu-id="69da8-118">Container</span><span class="sxs-lookup"><span data-stu-id="69da8-118">Containers</span></span>

<span data-ttu-id="69da8-119">Ein Container ist eine ausgeführte Instanz eines Images.</span><span class="sxs-lookup"><span data-stu-id="69da8-119">A container is a runnable instance of an image.</span></span> <span data-ttu-id="69da8-120">Wenn Sie Ihr Image erstellen, stellen Sie Ihre Anwendung und Abhängigkeiten bereit.</span><span class="sxs-lookup"><span data-stu-id="69da8-120">As you build your image, you deploy your application and dependencies.</span></span> <span data-ttu-id="69da8-121">Anschließend können mehrere Container instanziiert werden, die jeweils voneinander isoliert sind.</span><span class="sxs-lookup"><span data-stu-id="69da8-121">Then, multiple containers can be instantiated, each isolated from one another.</span></span> <span data-ttu-id="69da8-122">Jede Containerinstanz verfügt über ein eigenes Dateisystem, eigenen Speicher und eine eigene Netzwerkschnittstelle.</span><span class="sxs-lookup"><span data-stu-id="69da8-122">Each container instance has its own filesystem, memory, and network interface.</span></span>

### <a name="registries"></a><span data-ttu-id="69da8-123">Registrierungen</span><span class="sxs-lookup"><span data-stu-id="69da8-123">Registries</span></span>

<span data-ttu-id="69da8-124">Containerregistrierungen sind eine Sammlung von Imagerepositorys.</span><span class="sxs-lookup"><span data-stu-id="69da8-124">Container registries are a collection of image repositories.</span></span> <span data-ttu-id="69da8-125">Sie können Ihre Images auf einem Registrierungsimage basieren.</span><span class="sxs-lookup"><span data-stu-id="69da8-125">You can base your images on a registry image.</span></span> <span data-ttu-id="69da8-126">Sie können Container direkt aus einem Image in einer Registrierung erstellen.</span><span class="sxs-lookup"><span data-stu-id="69da8-126">You can create containers directly from an image in a registry.</span></span> <span data-ttu-id="69da8-127">Die [Beziehung zwischen Docker-Containern, -Images und -Registrys](../../architecture/microservices/container-docker-introduction/docker-containers-images-registries.md) ist ein wichtiges Konzept beim [Entwurf und Aufbau von Containeranwendungen oder Microservices](../../architecture/microservices/architect-microservice-container-applications/index.md).</span><span class="sxs-lookup"><span data-stu-id="69da8-127">The [relationship between Docker containers, images, and registries](../../architecture/microservices/container-docker-introduction/docker-containers-images-registries.md) is an important concept when [architecting and building containerized applications or microservices](../../architecture/microservices/architect-microservice-container-applications/index.md).</span></span> <span data-ttu-id="69da8-128">Durch diese Vorgehensweise wird die Zeit zwischen Entwicklung und Bereitstellung deutlich verkürzt.</span><span class="sxs-lookup"><span data-stu-id="69da8-128">This approach greatly shortens the time between development and deployment.</span></span>

<span data-ttu-id="69da8-129">Docker verfügt über eine öffentliche Registrierung, die auf dem [Docker-Hub](https://hub.docker.com/) gehostet wird, die Sie verwenden können.</span><span class="sxs-lookup"><span data-stu-id="69da8-129">Docker has a public registry hosted at the [Docker Hub](https://hub.docker.com/) that you can use.</span></span> <span data-ttu-id="69da8-130">Images, die sich auf [.NET Core beziehen](https://hub.docker.com/_/microsoft-dotnet-core/), werden auf dem Docker-Hub aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="69da8-130">[.NET Core related images](https://hub.docker.com/_/microsoft-dotnet-core/) are listed at the Docker Hub.</span></span> 

<span data-ttu-id="69da8-131">Die Microsoft Container Registry (MCR) ist die offizielle Quelle für von Microsoft bereitgestellte Containerimages.</span><span class="sxs-lookup"><span data-stu-id="69da8-131">The Microsoft Container Registry (MCR) is the official source of Microsoft-provided container images.</span></span> <span data-ttu-id="69da8-132">MCR basiert auf Azure CDN, um global replizierte Images bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="69da8-132">The MCR is built on Azure CDN to provide globally-replicated images.</span></span> <span data-ttu-id="69da8-133">MCR verfügt jedoch nicht über eine öffentlich zugängliche Website, und der primäre Weg, um mehr über von Microsoft bereitgestellte Containerimages zu erfahren, führt über die [Microsoft Docker-Hubseiten](https://hub.docker.com/_/microsoft-dotnet-core/).</span><span class="sxs-lookup"><span data-stu-id="69da8-133">However, the MCR does not have a public-facing website and the primary way to learn about Microsoft-provided container images is through the [Microsoft Docker Hub pages](https://hub.docker.com/_/microsoft-dotnet-core/).</span></span>

### <a name="dockerfile"></a><span data-ttu-id="69da8-134">Docker-Datei</span><span class="sxs-lookup"><span data-stu-id="69da8-134">Dockerfile</span></span>

<span data-ttu-id="69da8-135">Eine **Dockerfile-Datei** ist eine Datei, die einen Satz von Anweisungen definiert, mit dem ein Image erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="69da8-135">A **Dockerfile** is a file that defines a set of instructions that creates an image.</span></span> <span data-ttu-id="69da8-136">Jede Anweisung in der **Dockerfile-Datei** erstellt eine Ebene im Image.</span><span class="sxs-lookup"><span data-stu-id="69da8-136">Each instruction in the **Dockerfile** creates a layer in the image.</span></span> <span data-ttu-id="69da8-137">Wenn Sie das Image neu erstellen, werden in den meisten Fällen nur die Ebenen neu erstellt, die sich geändert haben.</span><span class="sxs-lookup"><span data-stu-id="69da8-137">For the most part, when you rebuild the image only the layers that have changed are rebuilt.</span></span> <span data-ttu-id="69da8-138">Die **Dockerfile-Datei** kann an andere Benutzer verteilt werden und ermöglicht es ihnen, ein neues Image auf die gleiche Weise zu erstellen, wie Sie es erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="69da8-138">The **Dockerfile** can be distributed to others and allows them to recreate to create a new image in the same manner you created it.</span></span> <span data-ttu-id="69da8-139">Dies ermöglicht es Ihnen zwar, die *Anweisungen* zur Erstellung des Images zu verteilen, aber die Hauptmethode zur Verteilung Ihres Images ist die Veröffentlichung in einer Registrierung.</span><span class="sxs-lookup"><span data-stu-id="69da8-139">While this allows you to distribute the *instructions* on how to create the image, the main way to distribute your image is to publish it to a registry.</span></span>

## <a name="net-core-images"></a><span data-ttu-id="69da8-140">.NET Core-Images</span><span class="sxs-lookup"><span data-stu-id="69da8-140">.NET Core images</span></span>

<span data-ttu-id="69da8-141">Offizielle.NET Core Docker-Images werden in Microsoft Container Registry (MCR) veröffentlicht und sind im [Microsoft.NET Core Docker-Hub-Repository](https://hub.docker.com/_/microsoft-dotnet-core/) verfügbar.</span><span class="sxs-lookup"><span data-stu-id="69da8-141">Official .NET Core Docker images are published to the Microsoft Container Registry (MCR) and are discoverable at the [Microsoft .NET Core Docker Hub repository](https://hub.docker.com/_/microsoft-dotnet-core/).</span></span> <span data-ttu-id="69da8-142">Jedes Repository enthält Images für verschiedene Kombinationen von .NET (SDK oder Runtime) und dem Betriebssystem, die Sie verwenden können.</span><span class="sxs-lookup"><span data-stu-id="69da8-142">Each repository contains images for different combinations of the .NET (SDK or Runtime) and OS that you can use.</span></span> 

<span data-ttu-id="69da8-143">Microsoft stellt Images bereit, die auf bestimmte Szenarien zugeschnitten sind.</span><span class="sxs-lookup"><span data-stu-id="69da8-143">Microsoft provides images that are tailored for specific scenarios.</span></span> <span data-ttu-id="69da8-144">So stellt beispielsweise das [ASP.NET Core-Repository](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) Images bereit, die für die Ausführung von ASP.NET Core-Apps in der Produktion erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="69da8-144">For example, the [ASP.NET Core repository](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) provides images that are built for running ASP.NET Core apps in production.</span></span>

## <a name="azure-services"></a><span data-ttu-id="69da8-145">Azure-Dienste</span><span class="sxs-lookup"><span data-stu-id="69da8-145">Azure services</span></span>

<span data-ttu-id="69da8-146">Verschiedene Azure-Dienste unterstützen Container.</span><span class="sxs-lookup"><span data-stu-id="69da8-146">Various Azure services support containers.</span></span> <span data-ttu-id="69da8-147">Sie erstellen ein Docker-Image für Ihre Anwendung und stellen es für einen der folgenden Dienste bereit:</span><span class="sxs-lookup"><span data-stu-id="69da8-147">You create a Docker image for your application and deploy it to one of the following services:</span></span>

* <span data-ttu-id="69da8-148">[Azure Kubernetes Service (AKS)](https://azure.microsoft.com/services/kubernetes-service/)</span><span class="sxs-lookup"><span data-stu-id="69da8-148">[Azure Kubernetes Service (AKS)](https://azure.microsoft.com/services/kubernetes-service/)</span></span>\
<span data-ttu-id="69da8-149">Skalieren und orchestrieren Sie Linux-Container mit Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="69da8-149">Scale and orchestrate Linux containers using Kubernetes.</span></span>

* <span data-ttu-id="69da8-150">[Azure App Service](https://azure.microsoft.com/services/app-service/containers/)</span><span class="sxs-lookup"><span data-stu-id="69da8-150">[Azure App Service](https://azure.microsoft.com/services/app-service/containers/)</span></span>\
<span data-ttu-id="69da8-151">Stellen Sie Web-Apps und APIs mithilfe von Linux-Containern in einer PaaS-Umgebung bereit.</span><span class="sxs-lookup"><span data-stu-id="69da8-151">Deploy web apps or APIs using Linux containers in a PaaS environment.</span></span>

* <span data-ttu-id="69da8-152">[Azure Container Instances](https://azure.microsoft.com/services/container-instances/)</span><span class="sxs-lookup"><span data-stu-id="69da8-152">[Azure Container Instances](https://azure.microsoft.com/services/container-instances/)</span></span>\
<span data-ttu-id="69da8-153">Hosten Sie Ihren Container in der Cloud ohne übergeordnete Verwaltungsdienste.</span><span class="sxs-lookup"><span data-stu-id="69da8-153">Host your container in the cloud without any higher-level management services.</span></span>

* <span data-ttu-id="69da8-154">[Azure Batch](https://azure.microsoft.com/services/batch/)</span><span class="sxs-lookup"><span data-stu-id="69da8-154">[Azure Batch](https://azure.microsoft.com/services/batch/)</span></span>\
<span data-ttu-id="69da8-155">Führen Sie sich wiederholende Computeaufträge mit Containern aus.</span><span class="sxs-lookup"><span data-stu-id="69da8-155">Run repetitive compute jobs using containers.</span></span>

* <span data-ttu-id="69da8-156">[Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/)</span><span class="sxs-lookup"><span data-stu-id="69da8-156">[Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/)</span></span>\
<span data-ttu-id="69da8-157">Optimieren, verschieben und modernisieren Sie .NET-Anwendungen in Microservices mithilfe von Windows Server-Containern.</span><span class="sxs-lookup"><span data-stu-id="69da8-157">Lift, shift, and modernize .NET applications to microservices using Windows Server containers</span></span>

* <span data-ttu-id="69da8-158">[Azure Container Registry](https://azure.microsoft.com/services/container-registry/)</span><span class="sxs-lookup"><span data-stu-id="69da8-158">[Azure Container Registry](https://azure.microsoft.com/services/container-registry/)</span></span>\
<span data-ttu-id="69da8-159">Speichern und verwalten Sie Containerimages für alle Typen von Azure-Bereitstellungen.</span><span class="sxs-lookup"><span data-stu-id="69da8-159">Store and manage container images across all types of Azure deployments.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69da8-160">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="69da8-160">Next steps</span></span>

* [<span data-ttu-id="69da8-161">Bereitstellen einer .NET Core-Anwendung im Container</span><span class="sxs-lookup"><span data-stu-id="69da8-161">Learn how to containerize a .NET Core application.</span></span>](build-docker-netcore-container.md)
* [<span data-ttu-id="69da8-162">Bereitstellen einer ASP.NET Core-Anwendung im Container.</span><span class="sxs-lookup"><span data-stu-id="69da8-162">Learn how to containerize an ASP.NET Core application.</span></span>](/aspnet/core/host-and-deploy/docker/building-net-docker-images)
* [<span data-ttu-id="69da8-163">Tutorial zu ASP.NET Core-Microservices</span><span class="sxs-lookup"><span data-stu-id="69da8-163">Try the Learn ASP.NET Core Microservice tutorial.</span></span>](https://dotnet.microsoft.com/learn/web/aspnet-microservice-tutorial/intro)
* [<span data-ttu-id="69da8-164">Informationen zu Containertools in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="69da8-164">Learn about Container Tools in Visual Studio</span></span>](/visualstudio/containers/overview)