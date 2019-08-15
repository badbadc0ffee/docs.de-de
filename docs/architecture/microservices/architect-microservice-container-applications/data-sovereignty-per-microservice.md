---
title: Datensouveränität pro Microservice
description: Datensouveränität pro Microservice gehört zu den Eckpfeilern von Microservices. Jeder Microservice muss der alleinige Besitzer seiner Datenbank sein – sie darf nicht freigegeben werden. Alle Instanzen eines Microservices verbinden sich mit der gleichen hochverfügbaren Datenbank.
ms.date: 09/20/2018
ms.openlocfilehash: ccb12451cd7cd44938e09d171eb29e614786f469
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/30/2019
ms.locfileid: "68673177"
---
# <a name="data-sovereignty-per-microservice"></a><span data-ttu-id="716c9-105">Datensouveränität pro Microservice</span><span class="sxs-lookup"><span data-stu-id="716c9-105">Data sovereignty per microservice</span></span>

<span data-ttu-id="716c9-106">Eine wichtige Regel für die Microservicesarchitektur ist, dass jeder Microservice seine eigenen Domänendaten und Domänenlogik besitzen muss.</span><span class="sxs-lookup"><span data-stu-id="716c9-106">An important rule for microservices architecture is that each microservice must own its domain data and logic.</span></span> <span data-ttu-id="716c9-107">Ebenso wie eine vollständige Anwendung, die eigene Logik und Daten besitzt, muss jeder Microservice eigene Logik und Daten in einem autonomen Lebenszyklus mit unabhängigen Bereitstellungen pro Microservice besitzen.</span><span class="sxs-lookup"><span data-stu-id="716c9-107">Just as a full application owns its logic and data, so must each microservice own its logic and data under an autonomous lifecycle, with independent deployment per microservice.</span></span>

<span data-ttu-id="716c9-108">Dies bedeutet, dass das konzeptionelle Modell der Domäne sich bei Subsystemen bzw. Microservices unterscheidet.</span><span class="sxs-lookup"><span data-stu-id="716c9-108">This means that the conceptual model of the domain will differ between subsystems or microservices.</span></span> <span data-ttu-id="716c9-109">Betrachten Sie z.B. Unternehmensanwendungen, bei denen CRM-Anwendungen (Customer Relationship Management), transaktionsgesteuerte Einkaufssubsysteme und Kundendienstsubsystemen eindeutige Kundenentitätsattribute und Daten in Anspruch nehmen und andere Kontextgrenzen (BC) nutzen.</span><span class="sxs-lookup"><span data-stu-id="716c9-109">Consider enterprise applications, where customer relationship management (CRM) applications, transactional purchase subsystems, and customer support subsystems each call on unique customer entity attributes and data, and where each employs a different Bounded Context (BC).</span></span>

<span data-ttu-id="716c9-110">Dieses Prinzip ist ähnlich bei [domänengesteuertem Design (DDD)](https://en.wikipedia.org/wiki/Domain-driven_design), wobei jeder [begrenzte Kontext](https://martinfowler.com/bliki/BoundedContext.html) oder jedes autonome Subsystem oder Dienst sein Domänenmodell (Daten plus Logik und Verhalten) besitzen muss.</span><span class="sxs-lookup"><span data-stu-id="716c9-110">This principle is similar in [Domain-driven design (DDD)](https://en.wikipedia.org/wiki/Domain-driven_design), where each [Bounded Context](https://martinfowler.com/bliki/BoundedContext.html) or autonomous subsystem or service must own its domain model (data plus logic and behavior).</span></span> <span data-ttu-id="716c9-111">Jeder begrenzte Kontext von DDD entspricht einem Microservice für Unternehmen (mindestens ein Dienst).</span><span class="sxs-lookup"><span data-stu-id="716c9-111">Each DDD Bounded Context correlates to one business microservice (one or several services).</span></span> <span data-ttu-id="716c9-112">Die begrenzten Kontextmuster werden im nächsten Abschnitt ausführlich erläutert.</span><span class="sxs-lookup"><span data-stu-id="716c9-112">This point about the Bounded Context pattern is expanded in the next section.</span></span>

<span data-ttu-id="716c9-113">Andererseits verfügt der herkömmliche (monolithische Daten-)Ansatz, der in vielen Anwendungen verwendet wird, über eine einzelne zentrale Datenbank oder nur wenige Datenbanken.</span><span class="sxs-lookup"><span data-stu-id="716c9-113">On the other hand, the traditional (monolithic data) approach used in many applications is to have a single centralized database or just a few databases.</span></span> <span data-ttu-id="716c9-114">Dabei handelt es sich häufig um eine normalisierte SQL-Datenbank, die für die gesamte Anwendung und alle ihre interne Subsysteme verwendet wird (s. Abbildung 4-7).</span><span class="sxs-lookup"><span data-stu-id="716c9-114">This is often a normalized SQL database that's used for the whole application and all its internal subsystems, as shown in Figure 4-7.</span></span>

![Der traditionelle Ansatz sieht vor, dass eine einzige Datenbank für alle Dienste gemeinsam genutzt wird, typischerweise in einer mehrstufigen Architektur.](./media/image7.png)

<span data-ttu-id="716c9-117">**Abbildung 4-7**.</span><span class="sxs-lookup"><span data-stu-id="716c9-117">**Figure 4-7**.</span></span> <span data-ttu-id="716c9-118">Vergleich der Datensouveränität: monolithische Datenbank im Vergleich zu Microservices</span><span class="sxs-lookup"><span data-stu-id="716c9-118">Data sovereignty comparison: monolithic database versus microservices</span></span>

<span data-ttu-id="716c9-119">Dieser zentralisierte Datenbankansatz sieht anfänglich einfacher aus und scheint die Wiederverwendung von Entitäten in verschiedenen Subsystemen zu ermöglichen, um Konsistenz zu gewährleisten.</span><span class="sxs-lookup"><span data-stu-id="716c9-119">The centralized database approach initially looks simpler and seems to enable reuse of entities in different subsystems to make everything consistent.</span></span> <span data-ttu-id="716c9-120">Doch in Wirklichkeit haben Sie es mit riesigen Tabellen zu tun, die Anforderungen vieler verschiedener Subsysteme erfüllen und Attribute und Spalten enthalten, die in den meisten Fällen nicht nötig sind.</span><span class="sxs-lookup"><span data-stu-id="716c9-120">But the reality is you end up with huge tables that serve many different subsystems, and that include attributes and columns that aren't needed in most cases.</span></span> <span data-ttu-id="716c9-121">Das ist wie der Versuch, dieselbe Karte für eine kurze Wanderung, einen Tagesausflug mit dem Auto und das Erlernen von Topografie zu nutzen.</span><span class="sxs-lookup"><span data-stu-id="716c9-121">It's like trying to use the same physical map for hiking a short trail, taking a day-long car trip, and learning geography.</span></span>

<span data-ttu-id="716c9-122">Eine monolithische Anwendung, typischerweise mit einer relationalen Datenbank, hat die folgenden wichtigen Vorteile: [ACID-Transaktionen](https://en.wikipedia.org/wiki/ACID) und SQL, die für alle Tabellen und Daten Ihrer Anwendung funktionieren.</span><span class="sxs-lookup"><span data-stu-id="716c9-122">A monolithic application with typically a single relational database has two important benefits: [ACID transactions](https://en.wikipedia.org/wiki/ACID) and the SQL language, both working across all the tables and data related to your application.</span></span> <span data-ttu-id="716c9-123">Dieser Ansatz bietet eine Möglichkeit zum einfachen Schreiben einer Abfrage, die Daten aus mehreren Tabellen kombiniert.</span><span class="sxs-lookup"><span data-stu-id="716c9-123">This approach provides a way to easily write a query that combines data from multiple tables.</span></span>

<span data-ttu-id="716c9-124">Der Datenzugriff wird jedoch beim Wechsel zu einer Microservicesarchitektur wesentlich komplexer.</span><span class="sxs-lookup"><span data-stu-id="716c9-124">However, data access becomes much more complex when you move to a microservices architecture.</span></span> <span data-ttu-id="716c9-125">Aber selbst wenn ACID-Transaktionen innerhalb eines Microservices oder eines begrenzten Kontexts verwendet werden können oder sollen, sind die Daten im Besitz jedes Microservices für diesen Microservice privat und es kann nur über seine Microservice-API auf sie zugegriffen werden.</span><span class="sxs-lookup"><span data-stu-id="716c9-125">But even when ACID transactions can or should be used within a microservice or Bounded Context, the data owned by each microservice is private to that microservice and can only be accessed via its microservice API.</span></span> <span data-ttu-id="716c9-126">Kapseln von Daten stellt sicher, dass die Microservices locker gekoppelt sind und sich unabhängig voneinander weiterentwickeln können.</span><span class="sxs-lookup"><span data-stu-id="716c9-126">Encapsulating the data ensures that the microservices are loosely coupled and can evolve independently of one another.</span></span> <span data-ttu-id="716c9-127">Wenn mehrere Dienste auf die gleichen Daten zugreifen, benötigen Schemaupdates koordinierte Updates für alle Dienste.</span><span class="sxs-lookup"><span data-stu-id="716c9-127">If multiple services were accessing the same data, schema updates would require coordinated updates to all the services.</span></span> <span data-ttu-id="716c9-128">Dadurch würde die Autonomie des Lebenszyklus der Microservices unterbrochen.</span><span class="sxs-lookup"><span data-stu-id="716c9-128">This would break the microservice lifecycle autonomy.</span></span> <span data-ttu-id="716c9-129">Allerdings bedeuten verteilte Datenstrukturen, dass Sie keine einzelne ACID-Transaktion über Microservices vornehmen können.</span><span class="sxs-lookup"><span data-stu-id="716c9-129">But distributed data structures mean that you can't make a single ACID transaction across microservices.</span></span> <span data-ttu-id="716c9-130">Dies bedeutet wiederum, dass Sie die letztliche Konsistenz verwenden müssen, wenn ein Geschäftsprozess mehrere Microservices umfasst.</span><span class="sxs-lookup"><span data-stu-id="716c9-130">This in turn means you must use eventual consistency when a business process spans multiple microservices.</span></span> <span data-ttu-id="716c9-131">Dies ist viel schwieriger zu implementieren als einfache SQL-Joins, da Sie weder Integritätseinschränkungen erstellen noch verteilte Transaktionen zwischen verschiedenen Datenbanken verwenden können, wie später erläutert wird.</span><span class="sxs-lookup"><span data-stu-id="716c9-131">This is much harder to implement than simple SQL joins, because you can't create integrity constraints or use distributed transactions between separate databases, as we'll explain later on.</span></span> <span data-ttu-id="716c9-132">Ebenso sind viele andere Funktionen der relationalen Datenbank nicht für mehrere Microservices verfügbar.</span><span class="sxs-lookup"><span data-stu-id="716c9-132">Similarly, many other relational database features aren't available across multiple microservices.</span></span>

<span data-ttu-id="716c9-133">Darüber hinaus verwenden verschiedene Microservices häufig unterschiedliche *Arten* von Datenbanken.</span><span class="sxs-lookup"><span data-stu-id="716c9-133">Going even further, different microservices often use different *kinds* of databases.</span></span> <span data-ttu-id="716c9-134">Moderne Anwendungen speichern und verarbeiten verschiedene Typen von Daten. Eine relationale Datenbank ist nicht immer die beste Wahl.</span><span class="sxs-lookup"><span data-stu-id="716c9-134">Modern applications store and process diverse kinds of data, and a relational database isn't always the best choice.</span></span> <span data-ttu-id="716c9-135">In einigen Anwendungsfällen verfügt eine NoSQL-Datenbank wie Azure CosmosDB oder MongoDB über ein praktischeres Datenmodell und bietet eine bessere Leistung und Skalierbarkeit als eine SQL-Datenbank wie SQL Server oder die Azure SQL-Datenbank.</span><span class="sxs-lookup"><span data-stu-id="716c9-135">For some use cases, a NoSQL database such as Azure CosmosDB or MongoDB might have a more convenient data model and offer better performance and scalability than a SQL database like SQL Server or Azure SQL Database.</span></span> <span data-ttu-id="716c9-136">In anderen Fällen ist eine relationale Datenbank immer noch die beste Herangehensweise.</span><span class="sxs-lookup"><span data-stu-id="716c9-136">In other cases, a relational database is still the best approach.</span></span> <span data-ttu-id="716c9-137">Aus diesem Grund verwenden auf Microservices basierende Anwendungen häufig eine Mischung aus SQL- und NoSQL-Datenbanken, was in einigen Fällen auch [Polyglot-Persistence](https://martinfowler.com/bliki/PolyglotPersistence.html)-Ansatz genannt wird.</span><span class="sxs-lookup"><span data-stu-id="716c9-137">Therefore, microservices-based applications often use a mixture of SQL and NoSQL databases, which is sometimes called the [polyglot persistence](https://martinfowler.com/bliki/PolyglotPersistence.html) approach.</span></span>

<span data-ttu-id="716c9-138">Eine partitionierte, polyglotte, persistente Architektur für die Datenspeicherung weist viele Vorteile auf.</span><span class="sxs-lookup"><span data-stu-id="716c9-138">A partitioned, polyglot-persistent architecture for data storage has many benefits.</span></span> <span data-ttu-id="716c9-139">Dazu gehören lose miteinander verknüpfte Dienste und eine bessere Leistung, Skalierbarkeit, Kosten und Verwaltbarkeit.</span><span class="sxs-lookup"><span data-stu-id="716c9-139">These include loosely coupled services and better performance, scalability, costs, and manageability.</span></span> <span data-ttu-id="716c9-140">Allerdings kann dies einige Herausforderungen für die verteilte Datenverwaltung hervorrufen, wie weiter unten in diesem Kapitel unter [Identifizieren von Domänenmodellgrenzen](identify-microservice-domain-model-boundaries.md) erläutert wird.</span><span class="sxs-lookup"><span data-stu-id="716c9-140">However, it can introduce some distributed data management challenges, as explained in "[Identifying domain-model boundaries](identify-microservice-domain-model-boundaries.md)" later in this chapter.</span></span>

## <a name="the-relationship-between-microservices-and-the-bounded-context-pattern"></a><span data-ttu-id="716c9-141">Die Beziehung zwischen Microservices und dem BC-Muster</span><span class="sxs-lookup"><span data-stu-id="716c9-141">The relationship between microservices and the Bounded Context pattern</span></span>

<span data-ttu-id="716c9-142">Das Konzept der Microservice leitet sich vom [BC-Muster (Begrenzter Kontext)](https://martinfowler.com/bliki/BoundedContext.html) in [domänengesteuertem Design (DDD)](https://en.wikipedia.org/wiki/Domain-driven_design) ab.</span><span class="sxs-lookup"><span data-stu-id="716c9-142">The concept of microservice derives from the [Bounded Context (BC) pattern](https://martinfowler.com/bliki/BoundedContext.html) in [domain-driven design (DDD)](https://en.wikipedia.org/wiki/Domain-driven_design).</span></span> <span data-ttu-id="716c9-143">DDD arbeitet mit großen Modellen, unterteilt diese in mehrere BCs und definiert explizite Umrisslinien.</span><span class="sxs-lookup"><span data-stu-id="716c9-143">DDD deals with large models by dividing them into multiple BCs and being explicit about their boundaries.</span></span> <span data-ttu-id="716c9-144">Jeder BC benötigt sein eigenes Modell und seine eigene Datenbank. Ebenso besitzt jeder Microservice seine verwandten Daten.</span><span class="sxs-lookup"><span data-stu-id="716c9-144">Each BC must have its own model and database; likewise, each microservice owns its related data.</span></span> <span data-ttu-id="716c9-145">Darüber hinaus verfügt jede BC in der Regel über eine eigene [ubiquitäre Sprache](https://martinfowler.com/bliki/UbiquitousLanguage.html) zur vereinfachten Kommunikation zwischen Softwareentwickler und Domänenexperten.</span><span class="sxs-lookup"><span data-stu-id="716c9-145">In addition, each BC usually has its own [ubiquitous language](https://martinfowler.com/bliki/UbiquitousLanguage.html) to help communication between software developers and domain experts.</span></span>

<span data-ttu-id="716c9-146">Diese Benennungen (v.a. Domänenentitäten) in der ubiquitären Sprache können unterschiedliche Namen in unterschiedlichen begrenzten Kontexten haben, selbst wenn die verschiedenen Domänenentitäten über die gleiche Identität verfügen (d.h. die eindeutige ID, die zum Lesen der Entität aus dem Speicher verwendet wird).</span><span class="sxs-lookup"><span data-stu-id="716c9-146">Those terms (mainly domain entities) in the ubiquitous language can have different names in different Bounded Contexts, even when different domain entities share the same identity (that is, the unique ID that's used to read the entity from storage).</span></span> <span data-ttu-id="716c9-147">In einem begrenzten Kontext in einem Benutzerprofil verfügt die Entität „User domain“ beispielsweise über die gleiche Identität wie die Entität „Buyer domain“ im begrenzten Bestellkontext.</span><span class="sxs-lookup"><span data-stu-id="716c9-147">For instance, in a user-profile Bounded Context, the User domain entity might share identity with the Buyer domain entity in the ordering Bounded Context.</span></span>

<span data-ttu-id="716c9-148">Ein Microservice ist daher wie ein begrenzter Kontext. Aber er gibt auch an, dass es sich um einen verteilten Dienst handelt.</span><span class="sxs-lookup"><span data-stu-id="716c9-148">A microservice is therefore like a Bounded Context, but it also specifies that it's a distributed service.</span></span> <span data-ttu-id="716c9-149">Er wird als separater Prozess für jeden begrenzten Kontext erstellt, und muss die oben erwähnten verteilten Protokolle wie HTTP/HTTPS, WebSockets oder [AMQP](https://en.wikipedia.org/wiki/Advanced_Message_Queuing_Protocol) verwenden.</span><span class="sxs-lookup"><span data-stu-id="716c9-149">It's built as a separate process for each Bounded Context, and it must use the distributed protocols noted earlier, like HTTP/HTTPS, WebSockets, or [AMQP](https://en.wikipedia.org/wiki/Advanced_Message_Queuing_Protocol).</span></span> <span data-ttu-id="716c9-150">Das begrenzte Kontextmuster gibt allerdings nicht an, ob der begrenzte Kontext ein verteilter Dienst oder einfach eine logische Begrenzung (z.B. ein generisches Subsystem) in einer monolithisch bereitgestellten Anwendung ist.</span><span class="sxs-lookup"><span data-stu-id="716c9-150">The Bounded Context pattern, however, doesn't specify whether the Bounded Context is a distributed service or if it's simply a logical boundary (such as a generic subsystem) within a monolithic-deployment application.</span></span>

<span data-ttu-id="716c9-151">Es ist wichtig hervorzuheben, dass die Definition eines Dienst für jeden begrenzten Kontext ein guter Ausgangspunkt ist.</span><span class="sxs-lookup"><span data-stu-id="716c9-151">It's important to highlight that defining a service for each Bounded Context is a good place to start.</span></span> <span data-ttu-id="716c9-152">Sie müssen Ihren Entwurf allerdings nicht darauf beschränken.</span><span class="sxs-lookup"><span data-stu-id="716c9-152">But you don't have to constrain your design to it.</span></span> <span data-ttu-id="716c9-153">In einigen Fällen müssen Sie einen begrenzten Kontext oder einen Microservice für ein Unternehmen entwerfen, die aus mehreren physischen Diensten bestehen.</span><span class="sxs-lookup"><span data-stu-id="716c9-153">Sometimes you must design a Bounded Context or business microservice composed of several physical services.</span></span> <span data-ttu-id="716c9-154">Aber letztendlich sind beide Muster – begrenzter Kontext und Microservice – eng miteinander verknüpft.</span><span class="sxs-lookup"><span data-stu-id="716c9-154">But ultimately, both patterns -Bounded Context and microservice- are closely related.</span></span>

<span data-ttu-id="716c9-155">DDD profitiert von Microservices durch echte Grenzen in Form von verteilten Microservices.</span><span class="sxs-lookup"><span data-stu-id="716c9-155">DDD benefits from microservices by getting real boundaries in the form of distributed microservices.</span></span> <span data-ttu-id="716c9-156">Aber Sie brauchen auch Ideen in einem begrenzten Kontext, wie die, das Modell nicht zwischen Microservices freizugeben.</span><span class="sxs-lookup"><span data-stu-id="716c9-156">But ideas like not sharing the model between microservices are what you also want in a Bounded Context.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="716c9-157">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="716c9-157">Additional resources</span></span>

- <span data-ttu-id="716c9-158">**Chris Richardson. Pattern: Database per service (Muster: Datenbank pro Dienst)**  </span><span class="sxs-lookup"><span data-stu-id="716c9-158">**Chris Richardson. Pattern: Database per service** </span></span>\
  <https://microservices.io/patterns/data/database-per-service.html>

- <span data-ttu-id="716c9-159">**Martin Fowler. BoundedContext** </span><span class="sxs-lookup"><span data-stu-id="716c9-159">**Martin Fowler. BoundedContext** </span></span>\
  <https://martinfowler.com/bliki/BoundedContext.html>

- <span data-ttu-id="716c9-160">**Martin Fowler. PolyglotPersistence** </span><span class="sxs-lookup"><span data-stu-id="716c9-160">**Martin Fowler. PolyglotPersistence** </span></span>\
  <https://martinfowler.com/bliki/PolyglotPersistence.html>

- <span data-ttu-id="716c9-161">**Alberto Brandolini. Strategic Domain Driven Design with Context Mapping (Strategisches domänengesteuertes Design mithilfe der Kontextzuordnung)**  </span><span class="sxs-lookup"><span data-stu-id="716c9-161">**Alberto Brandolini. Strategic Domain Driven Design with Context Mapping** </span></span>\
  <https://www.infoq.com/articles/ddd-contextmapping>

>[!div class="step-by-step"]
><span data-ttu-id="716c9-162">[Zurück](microservices-architecture.md)
>[Weiter](logical-versus-physical-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="716c9-162">[Previous](microservices-architecture.md)
[Next](logical-versus-physical-architecture.md)</span></span>