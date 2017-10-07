---
title: aaaGuide toocreating un servizio dati per hello Marketplace | Documenti Microsoft
description: Istruzioni dettagliate su come toocreate, certificare e distribuire un servizio dati per acquistano su hello Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 3a632825-db5b-49ec-98bd-887138798bc4
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: deb2e52dd03f5beb2ad6a927bd2d03e47d20b691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="mapping-an-existing-web-service-tooodata-through-csdl"></a><span data-ttu-id="4be8d-103">Mapping di un tooOData del servizio web esistente tramite CSDL</span><span class="sxs-lookup"><span data-stu-id="4be8d-103">Mapping an existing web service tooOData through CSDL</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4be8d-104">**In questo momento non stiamo più caricando nuovi editori di servizi dati. I nuovi servizi dati non saranno approvati per l'elencazione.**</span><span class="sxs-lookup"><span data-stu-id="4be8d-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="4be8d-105">Se si dispone di un'applicazione SaaS di business si desidera toopublish in AppSource è possibile trovare ulteriori informazioni [qui](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="4be8d-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="4be8d-106">Se si utilizzano applicazioni IaaS sviluppatore del servizio si sarebbe ad esempio toopublish in Azure Marketplace è possibile trovare ulteriori informazioni [qui](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="4be8d-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="4be8d-107">In questo articolo viene fornita una panoramica su come toouse un toomap CSDL un tooan servizio esistente servizio compatibile OData.</span><span class="sxs-lookup"><span data-stu-id="4be8d-107">This article gives an overview on how toouse a CSDL toomap an existing service tooan OData compatible service.</span></span> <span data-ttu-id="4be8d-108">Viene spiegato come toocreate hello documento di mapping (CSDL) che trasforma una richiesta di input hello del client di hello tramite una chiamata al servizio e hello output client toohello (backup dei dati) tramite un feed di OData compatibile.</span><span class="sxs-lookup"><span data-stu-id="4be8d-108">It explains how toocreate hello mapping document (CSDL) that transforms hello input request from hello client via a service call and hello output (data) back toohello client via an OData compatible feed.</span></span> <span data-ttu-id="4be8d-109">Microsoft Azure Marketplace espone gli utenti finali toohello servizi protocollo OData hello.</span><span class="sxs-lookup"><span data-stu-id="4be8d-109">Microsoft’s Azure Marketplace exposes services toohello end-users by using hello OData protocol.</span></span> <span data-ttu-id="4be8d-110">I servizi dei provider di contenuti (proprietari di dati) vengono esposti in varie forme, ad esempio REST, SOAP e così via.</span><span class="sxs-lookup"><span data-stu-id="4be8d-110">Services that are exposed by content providers (Data Owners) are exposed in a variety of forms, such as REST, SOAP, etc.</span></span>

## <a name="what-is-a-csdl-and-its-structure"></a><span data-ttu-id="4be8d-111">Che cos'è un CSDL e la relativa struttura?</span><span class="sxs-lookup"><span data-stu-id="4be8d-111">What is a CSDL and its structure?</span></span>
<span data-ttu-id="4be8d-112">Un file CSDL (Conceptual Schema Definition Language) è una specifica definizione come servizio web toodescribe o il database del servizio in comune XML lettera toohello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4be8d-112">A CSDL (Conceptual Schema Definition Language) is a specification defining how toodescribe web service or database service in common XML verbiage toohello Azure Marketplace.</span></span>

<span data-ttu-id="4be8d-113">Panoramica semplice di hello **del flusso di richiesta:**</span><span class="sxs-lookup"><span data-stu-id="4be8d-113">Simple overview of hello **request flow:**</span></span>

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

<span data-ttu-id="4be8d-114">Hello **il flusso di dati** in hello opposto direzione:</span><span class="sxs-lookup"><span data-stu-id="4be8d-114">hello **data flow** is in hello opposite direction:</span></span>

  `Client <- Azure Marketplace <- Content Provider’s WebService`

<span data-ttu-id="4be8d-115">**Figura 1** diagrammi come un client potrebbe ottenere i dati da un provider di contenuti (servizio) attraverso hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4be8d-115">**Figure 1** diagrams how a client would obtain data from a content provider (your service) by going through hello Azure Marketplace.</span></span>  <span data-ttu-id="4be8d-116">Hello CSDL viene utilizzato dalla richiesta di hello Mapping o la trasformazione componente toohandle hello e passare dati tra i servizi del provider di hello contenuti e hello richiesta client.</span><span class="sxs-lookup"><span data-stu-id="4be8d-116">hello CSDL is used by hello Mapping/Transformation component toohandle hello request and data pass between hello content provider’s service(s) and hello requesting client.</span></span>

<span data-ttu-id="4be8d-117">*Figura 1: Flusso dettagliato richiedano provider toocontent client tramite Azure Marketplace*</span><span class="sxs-lookup"><span data-stu-id="4be8d-117">*Figure 1: Detailed flow from requesting client toocontent provider via Azure Marketplace*</span></span>

  ![disegno](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

<span data-ttu-id="4be8d-119">Per informazioni generali su protocollo OData hello al quale hello compilazione estensioni di Azure Marketplace, Atom Pub e Atom, vedere: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span><span class="sxs-lookup"><span data-stu-id="4be8d-119">For background on Atom, Atom Pub, and hello OData protocol upon which hello Azure Marketplace extensions build, please review: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span></span>

<span data-ttu-id="4be8d-120">L'estratto di codice di sopra del collegamento: *"hello hello Open Data protocol (OData a cui si fa riferimento successivamente tooas) mira protocollo tooprovide basato su REST per operazioni in stile CRUD (Create, Read, Update e Delete) su risorse esposte come servizi di dati. Un "servizio dati" è un endpoint in cui i dati sono esposti da una o più "raccolte", ciascuna con zero o più "voci", costituite da coppie nome-valore tipizzate. OData viene pubblicato da Microsoft in standard OASIS (Organization for hello Advancement of Structured Information Standards) in modo che qualsiasi utente che desidera toocan creare server, client o gli strumenti di senza restrizioni o royalty."*</span><span class="sxs-lookup"><span data-stu-id="4be8d-120">Excerpt from above link: *“hello purpose of hello Open Data protocol (hereafter referred tooas OData) is tooprovide a REST-based protocol for CRUD-style operations (Create, Read, Update and Delete) against resources exposed as data services. A “data service” is an endpoint where there is data exposed from one or more “collections” each with zero or more “entries”, which consist of typed named-value pairs. OData is published by Microsoft under OASIS (Organization for hello Advancement of Structured Information Standards) Standards so that anyone that wants toocan build servers, clients or tools without royalties or restrictions.”*</span></span>

### <a name="three-critical-pieces-that-have-toobe-defined-by-hello-csdl-are"></a><span data-ttu-id="4be8d-121">Tre importanti che sono definiti da hello CSDL toobe sono:</span><span class="sxs-lookup"><span data-stu-id="4be8d-121">Three Critical Pieces that have toobe defined by hello CSDL are:</span></span>
* <span data-ttu-id="4be8d-122">Hello **endpoint** di Provider di servizi di hello hello Web indirizzo (URI) di hello servizio</span><span class="sxs-lookup"><span data-stu-id="4be8d-122">hello **endpoint** of hello Service Provider hello Web Address (URI) of hello Service</span></span>
* <span data-ttu-id="4be8d-123">Hello **parametri dati** passati come input toohello Provider di servizi le definizioni di hello dei parametri di hello inviati servizio del Provider contenuto toohello toohello tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="4be8d-123">hello **data parameters** being passed as input toohello Service Provider hello definitions of hello parameters being sent toohello Content Provider’s service down toohello data type.</span></span>
* <span data-ttu-id="4be8d-124">**Schema** di dati hello restituiti toohello richiesta servizio hello schema dell'hello dati inviati dal servizio del Provider di hello contenuto, inclusi i tipi di contenitore, raccolte e alle tabelle, variabili o colonne e dati.</span><span class="sxs-lookup"><span data-stu-id="4be8d-124">**Schema** of hello data being returned toohello Requesting Service hello schema of hello data being delivered by hello Content Provider’s service, including Container, collections/tables, variables/columns, and data types.</span></span>

<span data-ttu-id="4be8d-125">Hello seguente diagramma mostra una panoramica del flusso di hello dalla quale client hello immette hello OData istruzione (servizio di chiamata toohello del provider di contenuti web) toogetting hello risultati/backup dei dati.</span><span class="sxs-lookup"><span data-stu-id="4be8d-125">hello following diagram shows an overview of hello flow from where hello client enters hello OData statement (call toohello content provider’s web service) toogetting hello results/data back.</span></span>

  ![disegno](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a><span data-ttu-id="4be8d-127">Passaggi:</span><span class="sxs-lookup"><span data-stu-id="4be8d-127">Steps:</span></span>
1. <span data-ttu-id="4be8d-128">Il client invia richiesta tramite chiamata al servizio con i parametri di Input definiti in XML toohello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="4be8d-128">Client sends request via Service call complete with Input Parameters defined in XML toohello Azure Marketplace</span></span>
2. <span data-ttu-id="4be8d-129">CSDL è usato toovalidate hello chiamata del servizio.</span><span class="sxs-lookup"><span data-stu-id="4be8d-129">CSDL is used toovalidate hello Service call.</span></span>
   * <span data-ttu-id="4be8d-130">Hello formattato nella chiamata di servizio viene poi inviata toohello servizio provider di contenuto tramite hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="4be8d-130">hello Formatted Service Call is then sent toohello Content Providers Service by hello Azure Marketplace</span></span>
3. <span data-ttu-id="4be8d-131">esegue Hello Webservice e vengono eseguite azioni di hello di hello verbo Http (ad esempio, GET) dati hello restituiti tooAzure Marketplace in hello richiesta dei dati (se presente) è espone in formato XML toohello Client utilizzando hello Mapping definito nel file CSDL hello.</span><span class="sxs-lookup"><span data-stu-id="4be8d-131">hello Webservice executes and preforms hello action of hello Http Verb (i.e. GET) hello data is returned tooAzure Marketplace where hello requested data (if any) is exposes in XML Format toohello Client using hello Mapping defined in hello CSDL.</span></span>
4. <span data-ttu-id="4be8d-132">Hello Client verrà inviato dati hello (se presente) in formato XML o JSON</span><span class="sxs-lookup"><span data-stu-id="4be8d-132">hello Client is sent hello data (if any) in XML or JSON format</span></span>

## <a name="definitions"></a><span data-ttu-id="4be8d-133">Definizioni</span><span class="sxs-lookup"><span data-stu-id="4be8d-133">Definitions</span></span>
### <a name="odata-atom-pub"></a><span data-ttu-id="4be8d-134">OData ATOM Pub</span><span class="sxs-lookup"><span data-stu-id="4be8d-134">OData ATOM pub</span></span>
<span data-ttu-id="4be8d-135">Impostare un ATOM pub toohello estensione in cui ogni voce rappresenta una riga di un risultato.</span><span class="sxs-lookup"><span data-stu-id="4be8d-135">An extension toohello ATOM pub where each entry represents one row of a result set.</span></span> <span data-ttu-id="4be8d-136">parte di contenuto Hello della voce hello è toocontain avanzata hello valori di riga hello – come coppie chiave-valore.</span><span class="sxs-lookup"><span data-stu-id="4be8d-136">hello content part of hello entry is enhanced toocontain hello values of hello row – as key value pairs.</span></span> <span data-ttu-id="4be8d-137">Sono disponibili ulteriori informazioni all'indirizzo: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span><span class="sxs-lookup"><span data-stu-id="4be8d-137">More information is found here: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span></span>

### <a name="csdl---conceptual-schema-definition-language"></a><span data-ttu-id="4be8d-138">CSDL - Conceptual Schema Definition Language</span><span class="sxs-lookup"><span data-stu-id="4be8d-138">CSDL - Conceptual Schema Definition Language</span></span>
<span data-ttu-id="4be8d-139">Consente di definire le funzioni (SPROC) e le entità che vengono esposte tramite un database.</span><span class="sxs-lookup"><span data-stu-id="4be8d-139">Allows defining functions (SPROCs) and entities that are exposed through a database.</span></span> <span data-ttu-id="4be8d-140">Sono disponibili ulteriori informazioni all'indirizzo: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span><span class="sxs-lookup"><span data-stu-id="4be8d-140">More information found here: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span></span>  

> [!TIP]
> <span data-ttu-id="4be8d-141">Fare clic su hello **altre versioni** elenco a discesa e selezionare una versione, se non viene visualizzato articolo hello.</span><span class="sxs-lookup"><span data-stu-id="4be8d-141">Click hello **other versions** dropdown and select a version if you don’t see hello article.</span></span>
> 
> 

### <a name="edm---entry-data-model"></a><span data-ttu-id="4be8d-142">EDM - Entry Data Model, Modello di dati di movimento</span><span class="sxs-lookup"><span data-stu-id="4be8d-142">EDM - Entry Data Model</span></span>
* <span data-ttu-id="4be8d-143">Panoramica: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]</span><span class="sxs-lookup"><span data-stu-id="4be8d-143">Overview: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]</span></span>

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* <span data-ttu-id="4be8d-144">Anteprima: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]</span><span class="sxs-lookup"><span data-stu-id="4be8d-144">Preview: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]</span></span>

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* <span data-ttu-id="4be8d-145">Tipi di dati: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]</span><span class="sxs-lookup"><span data-stu-id="4be8d-145">Data types: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]</span></span>

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

<span data-ttu-id="4be8d-146">Hello seguente hello dettagliate tooRight sinistro flusso dal quale client hello immette hello OData istruzione (servizio di chiamata toohello del provider di contenuti web) toogetting hello risultati/backup dei dati:</span><span class="sxs-lookup"><span data-stu-id="4be8d-146">hello following shows hello detailed Left tooRight flow from where hello client enters hello OData statement (call toohello content provider’s web service) toogetting hello results/data back:</span></span>

  ![disegno](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a><span data-ttu-id="4be8d-148">Nozioni di base su CSDL</span><span class="sxs-lookup"><span data-stu-id="4be8d-148">CSDL Basics</span></span>
<span data-ttu-id="4be8d-149">Un file CSDL (Conceptual Schema Definition Language) è una specifica definizione come servizio web toodescribe o il database del servizio in comune XML lettera toohello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4be8d-149">A CSDL (Conceptual Schema Definition Language) is a specification defining how toodescribe web service or database service in common XML verbiage toohello Azure Marketplace.</span></span> <span data-ttu-id="4be8d-150">Descrive CSDL hello critico pezzi che **consente il passaggio di hello dei dati dall'origine dati di hello toohello Azure Marketplace.**</span><span class="sxs-lookup"><span data-stu-id="4be8d-150">CSDL describes hello critical pieces that **makes hello passing of data from hello Data Source toohello Azure Marketplace possible.**</span></span> <span data-ttu-id="4be8d-151">parti principali di Hello sono descritti di seguito:</span><span class="sxs-lookup"><span data-stu-id="4be8d-151">hello main pieces are described here:</span></span>

* <span data-ttu-id="4be8d-152">Informazioni sull'interfaccia che descrivono tutte le funzioni disponibili pubblicamente (nodo FunctionImport)</span><span class="sxs-lookup"><span data-stu-id="4be8d-152">Interface information describing all publicly available functions (FunctionImport Node)</span></span>
* <span data-ttu-id="4be8d-153">Informazioni sul tipo di dati per tutte le richieste di messaggi (input) e risposte ai messaggi (output) (nodi EntityContainer/EntitySet/EntityType)</span><span class="sxs-lookup"><span data-stu-id="4be8d-153">Data type information for all message requests(input) and message responses(outputs) (EntityContainer/EntitySet/EntityType Nodes)</span></span>
* <span data-ttu-id="4be8d-154">Informazioni su toobe protocollo di trasporto hello di associazione utilizzato (nodo intestazione)</span><span class="sxs-lookup"><span data-stu-id="4be8d-154">Binding information about hello transport protocol toobe used (Header Node)</span></span>
* <span data-ttu-id="4be8d-155">Informazioni sull'indirizzo per l'individuazione di hello specificato del servizio (BaseURI attributo)</span><span class="sxs-lookup"><span data-stu-id="4be8d-155">Address information for locating hello specified service (BaseURI attribute)</span></span>

<span data-ttu-id="4be8d-156">In breve, hello CSDL rappresenta un contratto di indipendente dalla piattaforma e linguaggio tra richiedente del servizio hello e provider di servizi di hello.</span><span class="sxs-lookup"><span data-stu-id="4be8d-156">In a nutshell, hello CSDL represents a platform- and language-independent contract between hello service requestor and hello service provider.</span></span> <span data-ttu-id="4be8d-157">Utilizza hello CSDL, un client può individuare un servizio di database o del servizio web e richiamare le relative funzioni disponibili pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="4be8d-157">Using hello CSDL, a client can locate a web service/database service and invoke any of its publicly available functions.</span></span>

### <a name="relating-a-csdl-tooa-database-or-a-collection"></a><span data-ttu-id="4be8d-158">Relativo a un Database di tooa CSDL o una raccolta</span><span class="sxs-lookup"><span data-stu-id="4be8d-158">Relating a CSDL tooa Database or a Collection</span></span>
<span data-ttu-id="4be8d-159">**Hello specifica CSDL**</span><span class="sxs-lookup"><span data-stu-id="4be8d-159">**hello CSDL Specification**</span></span>

<span data-ttu-id="4be8d-160">CSDL è la grammatica XML che descrive un servizio Web.</span><span class="sxs-lookup"><span data-stu-id="4be8d-160">CSDL is XML grammar for describing a web service.</span></span> <span data-ttu-id="4be8d-161">Specifica Hello è diviso 4 elementi principali: EntitySet, FunctionImport; Spazio dei nomi ed EntityType.</span><span class="sxs-lookup"><span data-stu-id="4be8d-161">hello specification itself is divided into 4 major elements:  EntitySet, FunctionImport; NameSpace, and EntityType.</span></span>

<span data-ttu-id="4be8d-162">toomake toounderstand di più facile Questa astrazione consente di collegare una tabella tooa CSDL.</span><span class="sxs-lookup"><span data-stu-id="4be8d-162">toomake this abstraction easier toounderstand lets relate a CSDL tooa table.</span></span>

<span data-ttu-id="4be8d-163">Tenere presente:</span><span class="sxs-lookup"><span data-stu-id="4be8d-163">Remember;</span></span>

  <span data-ttu-id="4be8d-164">CSDL rappresenta un contratto indipendente dalla piattaforma e linguaggio tra hello **richiedente del servizio** hello e **provider di servizi**.</span><span class="sxs-lookup"><span data-stu-id="4be8d-164">CSDL represents a platform- and language-independent contract between hello **service requestor** and hello **service provider**.</span></span> <span data-ttu-id="4be8d-165">Il CSDL consente al **client** di individuare un **servizio Web o del database** e richiamare una qualsiasi delle relative **funzioni** disponibili pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="4be8d-165">Using CSDL, a **client** can locate a **web service/database service** and invoke any of its publicly available **functions.**</span></span>

<span data-ttu-id="4be8d-166">Per hello un servizio dati costituito da quattro parti di un file CSDL può essere considerato in termini di un Database, tabelle, colonne e Stored Procedure.</span><span class="sxs-lookup"><span data-stu-id="4be8d-166">For a Data Service hello four parts of a CSDL can be thought of in terms of a Database, Table, Column, and Store Procedure.</span></span>

<span data-ttu-id="4be8d-167">Con riferimento a quanto segue per un servizio dati:</span><span class="sxs-lookup"><span data-stu-id="4be8d-167">Relating these as follows for a Data Service:</span></span>

* <span data-ttu-id="4be8d-168">EntityContainer  ~=  database</span><span class="sxs-lookup"><span data-stu-id="4be8d-168">EntityContainer  ~=  Database</span></span>
* <span data-ttu-id="4be8d-169">EntitySet  ~=  tabella</span><span class="sxs-lookup"><span data-stu-id="4be8d-169">EntitySet  ~=  Table</span></span>
* <span data-ttu-id="4be8d-170">EntityType  ~= colonne</span><span class="sxs-lookup"><span data-stu-id="4be8d-170">EntityType  ~= Columns</span></span>
* <span data-ttu-id="4be8d-171">FunctionImport  ~=  Stored Procedure</span><span class="sxs-lookup"><span data-stu-id="4be8d-171">FunctionImport  ~=  Stored Procedure</span></span>

<span data-ttu-id="4be8d-172">**Verbi HTTP consentiti**</span><span class="sxs-lookup"><span data-stu-id="4be8d-172">**HTTP Verbs allowed**</span></span>

* <span data-ttu-id="4be8d-173">GET-restituisce i valori da db hello (restituisce una raccolta)</span><span class="sxs-lookup"><span data-stu-id="4be8d-173">GET – returns values from hello db (returns a Collection)</span></span>
* <span data-ttu-id="4be8d-174">POST-utilizzate toopass dati tooand facoltativo i valori restituiti da db hello (creazione di una nuova voce nella raccolta di hello, id o URI restituito)</span><span class="sxs-lookup"><span data-stu-id="4be8d-174">POST – used toopass data tooand optional return values from hello db (Create a new entry in hello collection, return id/URI)</span></span>
* <span data-ttu-id="4be8d-175">ELIMINARE – Elimina i dati hello DB (Elimina una raccolta)</span><span class="sxs-lookup"><span data-stu-id="4be8d-175">DELETE – Deletes data from hello DB (Deletes a collection)</span></span>
* <span data-ttu-id="4be8d-176">PUT: consente di aggiornare i dati in un database (sostituire una raccolta o crearne una)</span><span class="sxs-lookup"><span data-stu-id="4be8d-176">PUT – Update data into a DB (replace a collection or create one)</span></span>

## <a name="metadatamapping-document"></a><span data-ttu-id="4be8d-177">Documento metadati/mapping</span><span class="sxs-lookup"><span data-stu-id="4be8d-177">Metadata/Mapping Document</span></span>
<span data-ttu-id="4be8d-178">documento di metadati e mapping Hello è toomap utilizzato in modo che può essere esposto come un servizio web OData dal sistema di hello Azure Marketplace di servizi web esistenti di un provider di contenuti.</span><span class="sxs-lookup"><span data-stu-id="4be8d-178">hello metadata/mapping document is used toomap a content provider’s existing web services so that it can be exposed as an OData web service by hello Azure Marketplace system.</span></span> <span data-ttu-id="4be8d-179">Si basa su CSDL e implementa alcune estensioni tooCSDL tooaccommodate hello esigenze di REST basato su servizi web esposti tramite Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4be8d-179">It is based on CSDL and implements a few extensions tooCSDL tooaccommodate hello needs of REST based web services exposed through Azure Marketplace.</span></span> <span data-ttu-id="4be8d-180">vengono trovate estensioni di Hello in hello [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="4be8d-180">hello extensions are found in hello [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) namespace.</span></span>

<span data-ttu-id="4be8d-181">Segue un esempio di hello CSDL: (copia e Incolla hello esempio CSDL in un editor XML seguente e modificare toomatch il servizio.</span><span class="sxs-lookup"><span data-stu-id="4be8d-181">An example of hello CSDL follows:  (Copy and paste hello below example CSDL into an XML editor and change toomatch your Service.</span></span>  <span data-ttu-id="4be8d-182">Incollare in CSDL Mapping nella scheda DataService durante la creazione del servizio in hello [portale di pubblicazione di Azure Marketplace](https://publish.windowsazure.com)).</span><span class="sxs-lookup"><span data-stu-id="4be8d-182">Then paste into CSDL Mapping under DataService tab when creating your service in hello  [Azure Marketplace Publishing Portal](https://publish.windowsazure.com)).</span></span>

<span data-ttu-id="4be8d-183">**Condizioni:** hello riguardanti CSDL termini toohello [portale pubblicazione](https://publish.windowsazure.com) termini dell'interfaccia utente (PPUI).</span><span class="sxs-lookup"><span data-stu-id="4be8d-183">**Terms:** Relating hello CSDL terms toohello [Publishing Portal](https://publish.windowsazure.com) UI (PPUI) terms.</span></span>

* <span data-ttu-id="4be8d-184">Offrono "Title" hello PPUI correlato tooMyWebOffer</span><span class="sxs-lookup"><span data-stu-id="4be8d-184">Offer “Title” in hello PPUI relates tooMyWebOffer</span></span>
* <span data-ttu-id="4be8d-185">MyCompany in hello PPUI si riferisce troppo**nome visualizzato editore** in hello [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="4be8d-185">MyCompany in hello PPUI relates too**Publisher Display Name** in hello [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) UI</span></span>
* <span data-ttu-id="4be8d-186">L'API correlata tooa Web o un servizio dati (un piano di hello PPUI)</span><span class="sxs-lookup"><span data-stu-id="4be8d-186">Your API relates tooa Web or Data Service (a Plan in hello PPUI)</span></span>

<span data-ttu-id="4be8d-187">**Gerarchia:** una società (provider di contenuti) è titolare delle offerte con piani, ossia servizi, che si allineano a un'API.</span><span class="sxs-lookup"><span data-stu-id="4be8d-187">**Hierarchy:** A Company (Content Provider) owns Offer(s) which have Plan(s), namely service(s), which line up with an API.</span></span>

### <a name="webservice-csdl-example"></a><span data-ttu-id="4be8d-188">Esempio di CSDL di WebService</span><span class="sxs-lookup"><span data-stu-id="4be8d-188">WebService CSDL Example</span></span>
<span data-ttu-id="4be8d-189">Si connette tooa servizio che espone un endpoint dell'applicazione web (ad esempio, un'applicazione c#)</span><span class="sxs-lookup"><span data-stu-id="4be8d-189">Connects tooa service that is exposing an web application endpoint (like a C# application)</span></span>

        <?xml version="1.0" encoding="utf-8"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyWebOffer" Alias="MyOffer" xmlns="http://schemas.microsoft.com/ado/2009/08/edm" xmlns:d="http://schemas.microsoft.com/dallas/2010/04" >
        <!-- EntityContainer groups all hello web service calls together into a single offering. Every web service call has a FunctionImport definition. -->
          <EntityContainer Name="MyOffer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
        @Name is used as reference by FunctionImport @EntitySet. And is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition near hello bottom of this file. -->
            <EntitySet Name="MyEntities" EntityType="MyOffer.MyEntityType" />
        <!-- Add a FunctionImport for every service method. Multiple FunctionImports can share a single return type (EntityType). -->
        <!-- ReturnType is either Raw() for a stream or Collection() for an Atom feed. Ex. of Raw: ReturnType=”Raw(text/plain)” -->
        <!—EntitySet is hello entityset defined above, and is needed if ReturnType is not Raw -->
        <!-- BaseURI attribute defines hello service call, replace & with hello encode value (&amp;).
        In hello input name value pairs {param} represents passed in value.
        Or hello value can be hard coded as with AccountKey. -->
        <!-- AllowedHttpMethods optional (default = “GET”), allows hello CSDL toospecifically specify hello verb of hello service, “Get”, “Post”, “Put”, or “Delete”. -->
        <!-- EncodeParameterValues, True encodes hello parameter values, false does not. -->
        <!-- BaseURI is translated into an URITemplate which defines how hello web service call is exposed toomarketplace customers.
        Ex. https://api.datamarket.azure.com/mycompany/MyOfferPlan?name={name}
        BaseURI is XML encoded, hello {...} point toohello parameters defined below.
        Marketplace will read hello parameters from this URITemplate and fill hello values into hello corresponding parameters of hello BaseUri or RequestBody (below) during calls tooyour service.  
        It is okay for @d:BaseUri tooinclude information only for Marketplace consumption, it will not be exposed tooend users. i.e. hello hardcoded AccountKey in hello above BaseURI does not show up in hello client facing URITemplate. -->
            <FunctionImport Name="MyWebServiceMethod"
                            EntitySet="MyEntities"
                            ReturnType="Collection(MyOffer.MyEntityType)"
        d:AllowedHttpMethods="GET"
        d:EncodeParameterValues="true"
        d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <!-- Definition of hello RequestBody is only required for HTTP POST requests and is optional for HTTP GET requests. -->
        <d:RequestBody d:httpMethod="POST">
                <!-- Use {} for placeholders tooinsert parameters. -->
                <!-- This example uses SOAP formatting, but any POST body can be used. -->
            <!-- This example shows how toopass userid and password via hello header -->
                <![CDATA[<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:MyOffer="http://services.organization.net/MyServicePath">
                  <soapenv:Header/>
                  <soapenv:Body>
                    <MyOffer:ws_MyWebServiceMethod>
                      <myWebServiceMethodRequest>
                        <!--This information is not exposed tooend users. -->
                        <UserId>userid</UserId>
                        <Password>password</Password>
                        <!-- {name} is replaced with hello value read from @d:UriTemplate above -->
                        <Name>{name}</Name>
                        <!-- Parameters can be used more than once and are not limited tooappearing as hello value of an element -->
                        <CustomField Name="{name}" />
                        <MyField>Static content</MyField>
                      </myWebServiceMethodRequest>
                    </MyOffer:ws_MyWebServiceMethod>
                  </soapenv:Body>
                </soapenv:Envelope>      
              ]]>
        </d:RequestBody>
        <!-- Title, Rights and Description are optional and used toospecify values tooinsert into hello ATOM feed returned toohello end user.  You can specify hello element toocontain a fixed message by providing a value for hello element (this is hello default value).  @d:Map is an XPath expression that points into hello response returned by your service and is optional.  -->
        <d:Title d:Map="/MyResponse/Title">Default title.</d:Title>
        <d:Rights>© My copyright. This is a fixed response. It is okay tooalso add a d:Map attribute toooverride this text.</d:Rights>
        <d:Description d:Map="/MyResponse/Description"></d:Description>
        <d:Namespaces>
        <d:Namespace d:Prefix="p"  d:Uri="http://schemas.organization.net/2010/04/myNamespace" />
        <d:Namespace d:Prefix="p2" d:Uri="http://schemas.organization.net/2010/04/MyNamespace2" />
        </d:Namespaces>
        <!-- Parameters of hello web service call:
        @Name should match exactly (case sensitive) hello {…} placeholders in hello @d:BaseUri, @d:UriTemplate, and d:RequestBody, i.e. “name” parameter in above BaseURI.
        @Mode is always "In", compatibility with CSDL
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx
        @d:Nullable indicates whether hello parameter is required.
        @d:Regex - optional, attribute toodescribe hello string, limiting unwanted input at hello entry of hello system
        @d:Description - optional, is used by Service Explorer as help information
        @d:SampleValues - optional, is used by Service Explorer as help information. Multiple Sample values are separated by '|', e.g. "804735132|234534224|23409823234"
        @d:Enum - optional for string type. Contains an enumeration of possible values separated by a '|', e.g. d:enum="english|metric|raw". Will be converted in a dropdown list in hello Service Explorer.
        -->
        <Parameter name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="A name that cannot contain any spaces or non-alpha non-English characters"
        d:Enum="George|John|Thomas|James"
        d:SampleValues="George"/>
        <Parameter Name=" AccountKey" Mode="In" Type="String" d:Nullable="false" />

        <!-- d:ErrorHandling is an optional element. Use it define standardized errors by evaluating hello service response. -->
        <d:ErrorHandling>
        <!-- Any number of d:Condition elements are allowed, they are evaluated in hello order listed.
        @d:Match is an Xpath query on hello service response, it should return true or false where true indicates an error.
        @d:httpStatusCode is hello error code tooreturn if an response matches hello error.
        @d:errorMessage is hello user friendly message tooreturn when an error occurs.
        -->
        <d:Condition d:Match="/Result/ErrorMessage[text()='Invalid token']" d:HttpStatusCode="403" d:ErrorMessage="User cannot connect toohello service." />
        </d:ErrorHandling>
           </FunctionImport>

            <!-- hello EntityContainer defines hello output data schema -->
        </EntityContainer>
        <!-- hello EntityType @d:Map defines hello repeating node (an XPath query) in hello response (output data schema). -->
        <!-- If these nodes are outside a namespace, add hello prefix in hello xpath. -->
        <!--
        @Name - define your user readable name, will become an XML element in hello ATOM feed, so comply with hello XML element naming restrictions (no spaces or other illegal characters).
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx.
        @d:Map uses an Xpath query toopoint at hello location tooextract hello content from your services response.
        hello "." is relative toohello repeating node in hello EntityType @d:Map Xpath expression.
        -->
            <EntityType Name="MyEntityType" d:Map="/MyResponse/MyEntities">
        <Property Name="ID"    d:IsPrimaryKey="True" Type="Int32"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="Amount"    Type="Double"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="City"    Type="String"    Nullable="false" d:Map="./City"/>
        <Property Name="State"    Type="String"    Nullable="false" d:Map="./State"/>
        <Property Name="Zip"    Type="Int32"    Nullable="false" d:Map="./Zip"/>
        <Property Name="Updated"    Type="DateTime"    Nullable="false" d:Map="./Updated"/>
        <Property Name="AdditionalInfo" Type="String" Nullable="true"
        d:Map="./Info/More[1]"/>
            </EntityType>
        </Schema>

> [!TIP]
> <span data-ttu-id="4be8d-190">Visualizzare ulteriori esempi di servizio Web di CSDL nell'articolo hello [esempi di mapping esistente web servizio tooOData tramite CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span><span class="sxs-lookup"><span data-stu-id="4be8d-190">View more CSDL Web Service examples in hello article [Examples of mapping an existing web service tooOData through CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span></span>
> 
> 

### <a name="dataservice-csdl-example"></a><span data-ttu-id="4be8d-191">Esempio di CSDL di DataService</span><span class="sxs-lookup"><span data-stu-id="4be8d-191">DataService CSDL Example</span></span>
<span data-ttu-id="4be8d-192">Stabilisce la connessione del servizio tooa che viene esposto da una vista o tabella di database come un endpoint di esempio seguente vengono illustrati due API per i dati di base basato su API CSDL (possibile utilizzare viste anziché tabelle).</span><span class="sxs-lookup"><span data-stu-id="4be8d-192">Connects tooa service that is exposing a database table or view as an endpoint Below example shows two APIs for Data base based API CSDL (can use views rather than tables).</span></span>

        <?xml version="1.0"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyDataOffer" Alias="MyOffer" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ado/2009/08/edm">
        <!-- EntityContainer groups all hello data service calls together into a single offering. Every web service call has a FunctionImport definition. -->
        <EntityContainer Name="MyOfferContainer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
            Think of hello EntitySet as a Service
        @Name is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition (returned set of table columns). -->
        <EntitySet Name="CompanyInfoEntitySet" EntityType="MyOffer.CompanyInfo" />
        <EntitySet Name="ProductInfoEntitySet" EntityType="MyOffer.ProductInfo" />
        </EntityContainer>
        <!-- EntityType defines result (output); hello table (or view) and columns toobe returned by hello data service.)
            Map is hello schema.tabel or schema.view
            dals.TableName is hello table Name
            Name is hello name identifier for hello EntityType and hello Name of hello service exposed toohello client via hello UI.
            dals:IsExposed determines if hello table schema is exposed (generally true).
            dals:IsView (optional) true if this is based on a view rather than a table
            dals:TableSchema is hello schema name of hello table/view
        -->
        <EntityType
        Map="[dbo].[CompanyInfo]"
        dals:TableName="CompanyInfo"
        Name="CompanyInfo"
        dals:IsExposed="true"
        dals:IsView="false"
        dals:TableSchema="dbo"
        xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <!-- Property defines hello column properties and hello output of hello service.
            dals:ColumnName is hello name of hello column in hello table /view.
            Type is hello emd.SimpleType
            Nullable determines if NULL is a valid output value
            dals.CharMaxLenght is hello maximum length of hello output value
            Name is hello name of hello Property and is exposed toohello client facing UI
            dals:IsReturned is hello Boolean that determines if hello Service exposes this value toohello client.
            IsQueryable is hello Boolean that determines if hello column can be used in a database query
            (For data Services: tooimprove Performance make sure that columns marked ISQueryable=”true” are in an index.)
            dals:OrdinalPosition is hello numerical position x in hello table or hello View, where x is from 1 toohello number of columns in hello table.
            dals:DatabaseDataType is hello data type of hello column in hello database, i.e. SQL data type dals:IsPrimaryKey indicates if hello column is hello Primary key in hello table/view.  (hello columns marked ISPrimaryKey are used in hello Order by clause when returning data.)
        -->
        <Property dals:ColumnName="data" Type="String" Nullable="true" dals:CharMaxLength="-1" Name="data" dals:IsReturned="true" dals:IsQueryable="false" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="ticker" Type="String" Nullable="true" dals:CharMaxLength="10" Name="ticker" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        <EntityType Map="[dbo].[ProductInfo]" dals:TableName="ProductInfo" Name="ProductInfo" dals:IsExposed="true" dals:IsView="false" dals:TableSchema="dbo" xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <Property dals:ColumnName="companyid" Type="Int32" Nullable="true" Name="companyid" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="product" Type="String" Nullable="true" dals:CharMaxLength="50" Name="product" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        </Schema>

## <a name="see-also"></a><span data-ttu-id="4be8d-193">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="4be8d-193">See Also</span></span>
* <span data-ttu-id="4be8d-194">Se è interessati a learning e informazioni sui nodi specifici di hello e i relativi parametri, leggere questo articolo [nodi Mapping di dati del servizio OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) per le definizioni e le spiegazioni, esempi e il contesto casi di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="4be8d-194">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="4be8d-195">Se si è interessati a esaminare alcuni esempi, leggere questo articolo [esempi di Mapping di dati del servizio OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee codice di esempio e comprendere la sintassi di codice e il contesto.</span><span class="sxs-lookup"><span data-stu-id="4be8d-195">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee sample code and understand code syntax and context.</span></span>
* <span data-ttu-id="4be8d-196">toohello tooreturn previsto percorso per la pubblicazione toohello un servizio dati Azure Marketplace, leggere questo articolo [Guida alla pubblicazione di dati del servizio](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="4be8d-196">tooreturn toohello prescribed path for publishing a Data Service toohello Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

