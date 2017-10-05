---
title: Guida alla creazione di un servizio dati per il Marketplace | Documentazione Microsoft
description: Istruzioni dettagliate su come creare, certificare e distribuire un servizio dati per l'acquisto in Azure Marketplace.
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
ms.openlocfilehash: a853b4dbd1952ba4ea8ee68ea3ca98f588bb71a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="mapping-an-existing-web-service-to-odata-through-csdl"></a><span data-ttu-id="62203-103">Mapping di un servizio Web esistente in OData tramite CSDL</span><span class="sxs-lookup"><span data-stu-id="62203-103">Mapping an existing web service to OData through CSDL</span></span>
> [!IMPORTANT]
> <span data-ttu-id="62203-104">**In questo momento non stiamo più caricando nuovi editori di servizi dati. I nuovi servizi dati non saranno approvati per l'elencazione.**</span><span class="sxs-lookup"><span data-stu-id="62203-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="62203-105">Se si dispone di un'applicazione aziendale SaaS che si vuole pubblicare in AppSource, è possibile trovare altre informazioni [qui](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="62203-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="62203-106">Se si dispone di un'applicazione IaaS o di un servizio per gli sviluppatori che si vuole pubblicare in Azure Marketplace, è possibile trovare altre informazioni [qui](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="62203-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="62203-107">In questo articolo viene fornita una panoramica sull'utilizzo di un CSDL per eseguire il mapping di un servizio esistente in uno compatibile con OData.</span><span class="sxs-lookup"><span data-stu-id="62203-107">This article gives an overview on how to use a CSDL to map an existing service to an OData compatible service.</span></span> <span data-ttu-id="62203-108">Viene spiegato come creare il documento di mapping (CSDL) che trasforma la richiesta di input dal client tramite una chiamata del servizio e restituisce l'output (dati) al client tramite un feed compatibile con OData.</span><span class="sxs-lookup"><span data-stu-id="62203-108">It explains how to create the mapping document (CSDL) that transforms the input request from the client via a service call and the output (data) back to the client via an OData compatible feed.</span></span> <span data-ttu-id="62203-109">Microsoft Azure Marketplace espone i servizi agli utenti finali mediante il protocollo OData.</span><span class="sxs-lookup"><span data-stu-id="62203-109">Microsoft’s Azure Marketplace exposes services to the end-users by using the OData protocol.</span></span> <span data-ttu-id="62203-110">I servizi dei provider di contenuti (proprietari di dati) vengono esposti in varie forme, ad esempio REST, SOAP e così via.</span><span class="sxs-lookup"><span data-stu-id="62203-110">Services that are exposed by content providers (Data Owners) are exposed in a variety of forms, such as REST, SOAP, etc.</span></span>

## <a name="what-is-a-csdl-and-its-structure"></a><span data-ttu-id="62203-111">Che cos'è un CSDL e la relativa struttura?</span><span class="sxs-lookup"><span data-stu-id="62203-111">What is a CSDL and its structure?</span></span>
<span data-ttu-id="62203-112">Un CSDL (Conceptual Schema Definition Language) è una specifica che definisce la modalità di descrizione del servizio Web o del servizio di database nel linguaggio XML comune in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="62203-112">A CSDL (Conceptual Schema Definition Language) is a specification defining how to describe web service or database service in common XML verbiage to the Azure Marketplace.</span></span>

<span data-ttu-id="62203-113">Panoramica semplice del **flusso della richiesta:**</span><span class="sxs-lookup"><span data-stu-id="62203-113">Simple overview of the **request flow:**</span></span>

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

<span data-ttu-id="62203-114">Il **flusso di dati** è nella direzione opposta:</span><span class="sxs-lookup"><span data-stu-id="62203-114">The **data flow** is in the opposite direction:</span></span>

  `Client <- Azure Marketplace <- Content Provider’s WebService`

<span data-ttu-id="62203-115">**figura 1** illustra come un client ottiene i dati da un provider di contenuti (il servizio dell'utente) navigando attraverso Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="62203-115">**Figure 1** diagrams how a client would obtain data from a content provider (your service) by going through the Azure Marketplace.</span></span>  <span data-ttu-id="62203-116">Il CSDL viene utilizzato dal componente di mapping o trasformazione per gestire la richiesta e trasmettere i dati tra servizi del provider di contenuti e il client che ha effettuato la richiesta.</span><span class="sxs-lookup"><span data-stu-id="62203-116">The CSDL is used by the Mapping/Transformation component to handle the request and data pass between the content provider’s service(s) and the requesting client.</span></span>

<span data-ttu-id="62203-117">*Figura 1: flusso dettagliato dal client che effettua la richiesta al provider di contenuti tramite Azure Marketplace*</span><span class="sxs-lookup"><span data-stu-id="62203-117">*Figure 1: Detailed flow from requesting client to content provider via Azure Marketplace*</span></span>

  ![disegno](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

<span data-ttu-id="62203-119">Per informazioni generali su Atom, Atom Pub e il protocollo OData su cui vengono sviluppate le estensioni di Azure Marketplace, consultare: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span><span class="sxs-lookup"><span data-stu-id="62203-119">For background on Atom, Atom Pub, and the OData protocol upon which the Azure Marketplace extensions build, please review: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span></span>

<span data-ttu-id="62203-120">Estratto dal collegamento precedente: *"Lo scopo del protocollo Open Data (d'ora in avanti indicato come OData) è fornire un protocollo basato su REST per operazioni di creazione, lettura, aggiornamento ed eliminazione (CRUD, Create, Read, Update, Delete) su risorse esposte come servizi dati. Un "servizio dati" è un endpoint in cui i dati sono esposti da una o più "raccolte", ciascuna con zero o più "voci", costituite da coppie nome-valore tipizzate. OData è pubblicato da Microsoft secondo gli standard OASIS (Organization for the Advancement of Structured Information Standards, Organizzazione per la promozione delle norme sulle informazioni strutturate) affinché chiunque possa creare server, client o strumenti senza restrizioni o il pagamento di diritti".*</span><span class="sxs-lookup"><span data-stu-id="62203-120">Excerpt from above link: *“The purpose of the Open Data protocol (hereafter referred to as OData) is to provide a REST-based protocol for CRUD-style operations (Create, Read, Update and Delete) against resources exposed as data services. A “data service” is an endpoint where there is data exposed from one or more “collections” each with zero or more “entries”, which consist of typed named-value pairs. OData is published by Microsoft under OASIS (Organization for the Advancement of Structured Information Standards) Standards so that anyone that wants to can build servers, clients or tools without royalties or restrictions.”*</span></span>

### <a name="three-critical-pieces-that-have-to-be-defined-by-the-csdl-are"></a><span data-ttu-id="62203-121">Tre componenti critici che devono essere definiti in CSDL sono:</span><span class="sxs-lookup"><span data-stu-id="62203-121">Three Critical Pieces that have to be defined by the CSDL are:</span></span>
* <span data-ttu-id="62203-122">L'**endpoint** del provider di servizi, l'indirizzo Web (URI) del servizio</span><span class="sxs-lookup"><span data-stu-id="62203-122">The **endpoint** of the Service Provider The Web Address (URI) of the Service</span></span>
* <span data-ttu-id="62203-123">I **parametri dei dati** trasmessi come input per il provider di servizi, le definizioni dei parametri inviati al servizio del provider di contenuti fino al tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="62203-123">The **data parameters** being passed as input to the Service Provider The definitions of the parameters being sent to the Content Provider’s service down to the data type.</span></span>
* <span data-ttu-id="62203-124">Lo **schema** dei dati restituiti al servizio che esegue la richiesta, lo schema dei dati inviati dal servizio del provider di contenuti, compresi i tipi di contenitore, raccolte/tabelle, variabili/colonne e dati.</span><span class="sxs-lookup"><span data-stu-id="62203-124">**Schema** of the data being returned to the Requesting Service The schema of the data being delivered by the Content Provider’s service, including Container, collections/tables, variables/columns, and data types.</span></span>

<span data-ttu-id="62203-125">Nel diagramma seguente viene illustrata una panoramica del flusso dal quale il client immette l'istruzione di OData (chiamata al servizio Web del provider di contenuti) per ottenere risultati o dati.</span><span class="sxs-lookup"><span data-stu-id="62203-125">The following diagram shows an overview of the flow from where the client enters the OData statement (call to the content provider’s web service) to getting the results/data back.</span></span>

  ![disegno](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a><span data-ttu-id="62203-127">Passaggi:</span><span class="sxs-lookup"><span data-stu-id="62203-127">Steps:</span></span>
1. <span data-ttu-id="62203-128">Il client invia la richiesta tramite chiamata del servizio con parametri di input definiti in XML in Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="62203-128">Client sends request via Service call complete with Input Parameters defined in XML to the Azure Marketplace</span></span>
2. <span data-ttu-id="62203-129">CSDL viene utilizzato per convalidare la chiamata del servizio.</span><span class="sxs-lookup"><span data-stu-id="62203-129">CSDL is used to validate the Service call.</span></span>
   * <span data-ttu-id="62203-130">La chiamata del servizio formattata viene quindi inviata al servizio del provider di contenuti da Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="62203-130">The Formatted Service Call is then sent to the Content Providers Service by the Azure Marketplace</span></span>
3. <span data-ttu-id="62203-131">Viene avviato WebService, che esegue le azioni del verbo HTTP, ad esempio GET, i dati vengono restituiti ad Azure Marketplace in cui i dati richiesti (se presenti) vengono esposti in formato XML al client tramite il mapping definito nel CSDL.</span><span class="sxs-lookup"><span data-stu-id="62203-131">The Webservice executes and preforms the action of the Http Verb (i.e. GET) The data is returned to Azure Marketplace where the requested data (if any) is exposes in XML Format to the Client using the Mapping defined in the CSDL.</span></span>
4. <span data-ttu-id="62203-132">Al client vengono inviati i dati (se presenti) in formato JSON o XML</span><span class="sxs-lookup"><span data-stu-id="62203-132">The Client is sent the data (if any) in XML or JSON format</span></span>

## <a name="definitions"></a><span data-ttu-id="62203-133">Definizioni</span><span class="sxs-lookup"><span data-stu-id="62203-133">Definitions</span></span>
### <a name="odata-atom-pub"></a><span data-ttu-id="62203-134">OData ATOM Pub</span><span class="sxs-lookup"><span data-stu-id="62203-134">OData ATOM pub</span></span>
<span data-ttu-id="62203-135">Un'estensione di ATOM Pub in cui ciascuna voce rappresenta una riga di un risultato.</span><span class="sxs-lookup"><span data-stu-id="62203-135">An extension to the ATOM pub where each entry represents one row of a result set.</span></span> <span data-ttu-id="62203-136">La parte del contenuto della voce è stata migliorata per contenere i valori della riga, come coppie chiave-valore.</span><span class="sxs-lookup"><span data-stu-id="62203-136">The content part of the entry is enhanced to contain the values of the row – as key value pairs.</span></span> <span data-ttu-id="62203-137">Sono disponibili ulteriori informazioni all'indirizzo: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span><span class="sxs-lookup"><span data-stu-id="62203-137">More information is found here: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span></span>

### <a name="csdl---conceptual-schema-definition-language"></a><span data-ttu-id="62203-138">CSDL - Conceptual Schema Definition Language</span><span class="sxs-lookup"><span data-stu-id="62203-138">CSDL - Conceptual Schema Definition Language</span></span>
<span data-ttu-id="62203-139">Consente di definire le funzioni (SPROC) e le entità che vengono esposte tramite un database.</span><span class="sxs-lookup"><span data-stu-id="62203-139">Allows defining functions (SPROCs) and entities that are exposed through a database.</span></span> <span data-ttu-id="62203-140">Sono disponibili ulteriori informazioni all'indirizzo: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span><span class="sxs-lookup"><span data-stu-id="62203-140">More information found here: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span></span>  

> [!TIP]
> <span data-ttu-id="62203-141">Se l'articolo non viene visualizzato, fare clic sull'elenco a discesa **Altre versioni** e selezionare una versione.</span><span class="sxs-lookup"><span data-stu-id="62203-141">Click the **other versions** dropdown and select a version if you don’t see the article.</span></span>
> 
> 

### <a name="edm---entry-data-model"></a><span data-ttu-id="62203-142">EDM - Entry Data Model, Modello di dati di movimento</span><span class="sxs-lookup"><span data-stu-id="62203-142">EDM - Entry Data Model</span></span>
* <span data-ttu-id="62203-143">Panoramica: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]</span><span class="sxs-lookup"><span data-stu-id="62203-143">Overview: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]</span></span>

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* <span data-ttu-id="62203-144">Anteprima: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]</span><span class="sxs-lookup"><span data-stu-id="62203-144">Preview: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]</span></span>

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* <span data-ttu-id="62203-145">Tipi di dati: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]</span><span class="sxs-lookup"><span data-stu-id="62203-145">Data types: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]</span></span>

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

<span data-ttu-id="62203-146">Di seguito viene illustrato il flusso di dettagli da sinistra a destra da cui il client immette l'istruzione di OData (chiamata al servizio Web del provider di contenuti) per ottenere risultati o dati:</span><span class="sxs-lookup"><span data-stu-id="62203-146">The following shows the detailed Left to Right flow from where the client enters the OData statement (call to the content provider’s web service) to getting the results/data back:</span></span>

  ![disegno](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a><span data-ttu-id="62203-148">Nozioni di base su CSDL</span><span class="sxs-lookup"><span data-stu-id="62203-148">CSDL Basics</span></span>
<span data-ttu-id="62203-149">Un CSDL (Conceptual Schema Definition Language) è una specifica che definisce la modalità di descrizione del servizio Web o del servizio di database nel linguaggio XML comune in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="62203-149">A CSDL (Conceptual Schema Definition Language) is a specification defining how to describe web service or database service in common XML verbiage to the Azure Marketplace.</span></span> <span data-ttu-id="62203-150">CSDL descrive i componenti cruciali che **consentono la trasmissione dei dati dall'origine dati ad Azure Marketplace.**</span><span class="sxs-lookup"><span data-stu-id="62203-150">CSDL describes the critical pieces that **makes the passing of data from the Data Source to the Azure Marketplace possible.**</span></span> <span data-ttu-id="62203-151">I componenti principali sono descritti di seguito:</span><span class="sxs-lookup"><span data-stu-id="62203-151">The main pieces are described here:</span></span>

* <span data-ttu-id="62203-152">Informazioni sull'interfaccia che descrivono tutte le funzioni disponibili pubblicamente (nodo FunctionImport)</span><span class="sxs-lookup"><span data-stu-id="62203-152">Interface information describing all publicly available functions (FunctionImport Node)</span></span>
* <span data-ttu-id="62203-153">Informazioni sul tipo di dati per tutte le richieste di messaggi (input) e risposte ai messaggi (output) (nodi EntityContainer/EntitySet/EntityType)</span><span class="sxs-lookup"><span data-stu-id="62203-153">Data type information for all message requests(input) and message responses(outputs) (EntityContainer/EntitySet/EntityType Nodes)</span></span>
* <span data-ttu-id="62203-154">Informazioni sull'associazione circa il protocollo di trasporto utilizzato (nodo Header)</span><span class="sxs-lookup"><span data-stu-id="62203-154">Binding information about the transport protocol to be used (Header Node)</span></span>
* <span data-ttu-id="62203-155">Informazioni sull'indirizzo per l'individuazione del servizio specificato (attributo BaseURI)</span><span class="sxs-lookup"><span data-stu-id="62203-155">Address information for locating the specified service (BaseURI attribute)</span></span>

<span data-ttu-id="62203-156">In breve, il CSDL rappresenta un contratto indipendente dalla piattaforma e dal linguaggio tra chi richiede il servizio e il provider del servizio stesso.</span><span class="sxs-lookup"><span data-stu-id="62203-156">In a nutshell, the CSDL represents a platform- and language-independent contract between the service requestor and the service provider.</span></span> <span data-ttu-id="62203-157">Il CSDL consente al client di individuare un servizio Web o del database e richiamare una qualsiasi delle relative funzioni disponibili pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="62203-157">Using the CSDL, a client can locate a web service/database service and invoke any of its publicly available functions.</span></span>

### <a name="relating-a-csdl-to-a-database-or-a-collection"></a><span data-ttu-id="62203-158">Correlazione di un CSDL a un database o a una raccolta</span><span class="sxs-lookup"><span data-stu-id="62203-158">Relating a CSDL to a Database or a Collection</span></span>
<span data-ttu-id="62203-159">**La specifica CSDL**</span><span class="sxs-lookup"><span data-stu-id="62203-159">**The CSDL Specification**</span></span>

<span data-ttu-id="62203-160">CSDL è la grammatica XML che descrive un servizio Web.</span><span class="sxs-lookup"><span data-stu-id="62203-160">CSDL is XML grammar for describing a web service.</span></span> <span data-ttu-id="62203-161">La specifica stessa è suddivisa in 4 elementi principali: EntitySet, FunctionImport, NameSpace ed EntityType.</span><span class="sxs-lookup"><span data-stu-id="62203-161">The specification itself is divided into 4 major elements:  EntitySet, FunctionImport; NameSpace, and EntityType.</span></span>

<span data-ttu-id="62203-162">Rendere questa astrazione più comprensibile consente di correlare un CSDL a una tabella.</span><span class="sxs-lookup"><span data-stu-id="62203-162">To make this abstraction easier to understand lets relate a CSDL to a table.</span></span>

<span data-ttu-id="62203-163">Tenere presente:</span><span class="sxs-lookup"><span data-stu-id="62203-163">Remember;</span></span>

  <span data-ttu-id="62203-164">CSDL rappresenta un contratto indipendente dalla piattaforma e dal linguaggio tra **chi richiede il servizio** e il **provider del servizio stesso**.</span><span class="sxs-lookup"><span data-stu-id="62203-164">CSDL represents a platform- and language-independent contract between the **service requestor** and the **service provider**.</span></span> <span data-ttu-id="62203-165">Il CSDL consente al **client** di individuare un **servizio Web o del database** e richiamare una qualsiasi delle relative **funzioni** disponibili pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="62203-165">Using CSDL, a **client** can locate a **web service/database service** and invoke any of its publicly available **functions.**</span></span>

<span data-ttu-id="62203-166">Per un servizio dati, le quattro parti di un CSDL possono essere considerate in termini di un database, una tabella, una colonna e una Stored Procedure.</span><span class="sxs-lookup"><span data-stu-id="62203-166">For a Data Service the four parts of a CSDL can be thought of in terms of a Database, Table, Column, and Store Procedure.</span></span>

<span data-ttu-id="62203-167">Con riferimento a quanto segue per un servizio dati:</span><span class="sxs-lookup"><span data-stu-id="62203-167">Relating these as follows for a Data Service:</span></span>

* <span data-ttu-id="62203-168">EntityContainer  ~=  database</span><span class="sxs-lookup"><span data-stu-id="62203-168">EntityContainer  ~=  Database</span></span>
* <span data-ttu-id="62203-169">EntitySet  ~=  tabella</span><span class="sxs-lookup"><span data-stu-id="62203-169">EntitySet  ~=  Table</span></span>
* <span data-ttu-id="62203-170">EntityType  ~= colonne</span><span class="sxs-lookup"><span data-stu-id="62203-170">EntityType  ~= Columns</span></span>
* <span data-ttu-id="62203-171">FunctionImport  ~=  Stored Procedure</span><span class="sxs-lookup"><span data-stu-id="62203-171">FunctionImport  ~=  Stored Procedure</span></span>

<span data-ttu-id="62203-172">**Verbi HTTP consentiti**</span><span class="sxs-lookup"><span data-stu-id="62203-172">**HTTP Verbs allowed**</span></span>

* <span data-ttu-id="62203-173">GET: restituisce valori dal database (restituisce una raccolta)</span><span class="sxs-lookup"><span data-stu-id="62203-173">GET – returns values from the db (returns a Collection)</span></span>
* <span data-ttu-id="62203-174">POST: consente di passare dati verso e restituire facoltativamente valori dal database (creare una nuova voce nella raccolta, restituire ID/URI)</span><span class="sxs-lookup"><span data-stu-id="62203-174">POST – used to pass data to and optional return values from the db (Create a new entry in the collection, return id/URI)</span></span>
* <span data-ttu-id="62203-175">DELETE: elimina dati dal database (elimina una raccolta)</span><span class="sxs-lookup"><span data-stu-id="62203-175">DELETE – Deletes data from the DB (Deletes a collection)</span></span>
* <span data-ttu-id="62203-176">PUT: consente di aggiornare i dati in un database (sostituire una raccolta o crearne una)</span><span class="sxs-lookup"><span data-stu-id="62203-176">PUT – Update data into a DB (replace a collection or create one)</span></span>

## <a name="metadatamapping-document"></a><span data-ttu-id="62203-177">Documento metadati/mapping</span><span class="sxs-lookup"><span data-stu-id="62203-177">Metadata/Mapping Document</span></span>
<span data-ttu-id="62203-178">Il documento metadati/mapping viene utilizzato per il mapping dei servizi Web esistenti del provider di contenuti, affinché vengano esposti come servizio Web OData dal sistema di Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="62203-178">The metadata/mapping document is used to map a content provider’s existing web services so that it can be exposed as an OData web service by the Azure Marketplace system.</span></span> <span data-ttu-id="62203-179">Tale documento si basa su CSDL e implementa alcune estensioni in quest'ultimo per soddisfare le esigenze dei servizi Web basati su REST esposti tramite Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="62203-179">It is based on CSDL and implements a few extensions to CSDL to accommodate the needs of REST based web services exposed through Azure Marketplace.</span></span> <span data-ttu-id="62203-180">Le estensioni sono disponibili nello spazio dei nomi [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) .</span><span class="sxs-lookup"><span data-stu-id="62203-180">The extensions are found in the [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) namespace.</span></span>

<span data-ttu-id="62203-181">A seguire, un esempio di CSDL: (copiare e incollare il CSDL di esempio seguente in un editor XML e modificarlo affinché corrisponda al proprio servizio.</span><span class="sxs-lookup"><span data-stu-id="62203-181">An example of the CSDL follows:  (Copy and paste the below example CSDL into an XML editor and change to match your Service.</span></span>  <span data-ttu-id="62203-182">Quindi incollare il contenuto nel mapping CSDL, nella scheda DataService, durante la creazione del servizio nel [portale di pubblicazione di Azure Marketplace](https://publish.windowsazure.com)).</span><span class="sxs-lookup"><span data-stu-id="62203-182">Then paste into CSDL Mapping under DataService tab when creating your service in the  [Azure Marketplace Publishing Portal](https://publish.windowsazure.com)).</span></span>

<span data-ttu-id="62203-183">**Condizioni:** correlazione tra i termini di CSDL e i termini dell'interfaccia utente del [portale di pubblicazione](https://publish.windowsazure.com) .</span><span class="sxs-lookup"><span data-stu-id="62203-183">**Terms:** Relating the CSDL terms to the [Publishing Portal](https://publish.windowsazure.com) UI (PPUI) terms.</span></span>

* <span data-ttu-id="62203-184">Il "titolo" dell'offerta nell'interfaccia utente del portale di pubblicazione è correlato a MyWebOffer.</span><span class="sxs-lookup"><span data-stu-id="62203-184">Offer “Title” in the PPUI relates to MyWebOffer</span></span>
* <span data-ttu-id="62203-185">Il valore MyCompany nell'interfaccia utente del portale di pubblicazione è correlato al **Nome visualizzato dell'editore** nell'interfaccia utente del [Centro sviluppatori Microsoft](http://dev.windows.com/registration?accountprogram=azure)</span><span class="sxs-lookup"><span data-stu-id="62203-185">MyCompany in the PPUI relates to **Publisher Display Name** in the [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) UI</span></span>
* <span data-ttu-id="62203-186">L'API è correlata a un servizio Web o un servizio dati, ovvero un piano nell'interfaccia utente del portale di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="62203-186">Your API relates to a Web or Data Service (a Plan in the PPUI)</span></span>

<span data-ttu-id="62203-187">**Gerarchia:** una società (provider di contenuti) è titolare delle offerte con piani, ossia servizi, che si allineano a un'API.</span><span class="sxs-lookup"><span data-stu-id="62203-187">**Hierarchy:** A Company (Content Provider) owns Offer(s) which have Plan(s), namely service(s), which line up with an API.</span></span>

### <a name="webservice-csdl-example"></a><span data-ttu-id="62203-188">Esempio di CSDL di WebService</span><span class="sxs-lookup"><span data-stu-id="62203-188">WebService CSDL Example</span></span>
<span data-ttu-id="62203-189">Si connette a un servizio che espone un endpoint dell'applicazione Web (ad esempio un'applicazione C#)</span><span class="sxs-lookup"><span data-stu-id="62203-189">Connects to a service that is exposing an web application endpoint (like a C# application)</span></span>

        <?xml version="1.0" encoding="utf-8"?>
        <!-- The namespace attribute below is used by our system to generate C#. You can change “MyCompany.MyOffer” to something that makes sense for you, but change “MyOffer” consistently throughout the document. -->
        <Schema Namespace="MyCompany.MyWebOffer" Alias="MyOffer" xmlns="http://schemas.microsoft.com/ado/2009/08/edm" xmlns:d="http://schemas.microsoft.com/dallas/2010/04" >
        <!-- EntityContainer groups all the web service calls together into a single offering. Every web service call has a FunctionImport definition. -->
          <EntityContainer Name="MyOffer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
        @Name is used as reference by FunctionImport @EntitySet. And is used in the customer facing UI as name of the Service.
        @EntityType is used to point at the type definition near the bottom of this file. -->
            <EntitySet Name="MyEntities" EntityType="MyOffer.MyEntityType" />
        <!-- Add a FunctionImport for every service method. Multiple FunctionImports can share a single return type (EntityType). -->
        <!-- ReturnType is either Raw() for a stream or Collection() for an Atom feed. Ex. of Raw: ReturnType=”Raw(text/plain)” -->
        <!—EntitySet is the entityset defined above, and is needed if ReturnType is not Raw -->
        <!-- BaseURI attribute defines the service call, replace & with the encode value (&amp;).
        In the input name value pairs {param} represents passed in value.
        Or the value can be hard coded as with AccountKey. -->
        <!-- AllowedHttpMethods optional (default = “GET”), allows the CSDL to specifically specify the verb of the service, “Get”, “Post”, “Put”, or “Delete”. -->
        <!-- EncodeParameterValues, True encodes the parameter values, false does not. -->
        <!-- BaseURI is translated into an URITemplate which defines how the web service call is exposed to marketplace customers.
        Ex. https://api.datamarket.azure.com/mycompany/MyOfferPlan?name={name}
        BaseURI is XML encoded, the {...} point to the parameters defined below.
        Marketplace will read the parameters from this URITemplate and fill the values into the corresponding parameters of the BaseUri or RequestBody (below) during calls to your service.  
        It is okay for @d:BaseUri to include information only for Marketplace consumption, it will not be exposed to end users. i.e. the hardcoded AccountKey in the above BaseURI does not show up in the client facing URITemplate. -->
            <FunctionImport Name="MyWebServiceMethod"
                            EntitySet="MyEntities"
                            ReturnType="Collection(MyOffer.MyEntityType)"
        d:AllowedHttpMethods="GET"
        d:EncodeParameterValues="true"
        d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <!-- Definition of the RequestBody is only required for HTTP POST requests and is optional for HTTP GET requests. -->
        <d:RequestBody d:httpMethod="POST">
                <!-- Use {} for placeholders to insert parameters. -->
                <!-- This example uses SOAP formatting, but any POST body can be used. -->
            <!-- This example shows how to pass userid and password via the header -->
                <![CDATA[<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:MyOffer="http://services.organization.net/MyServicePath">
                  <soapenv:Header/>
                  <soapenv:Body>
                    <MyOffer:ws_MyWebServiceMethod>
                      <myWebServiceMethodRequest>
                        <!--This information is not exposed to end users. -->
                        <UserId>userid</UserId>
                        <Password>password</Password>
                        <!-- {name} is replaced with the value read from @d:UriTemplate above -->
                        <Name>{name}</Name>
                        <!-- Parameters can be used more than once and are not limited to appearing as the value of an element -->
                        <CustomField Name="{name}" />
                        <MyField>Static content</MyField>
                      </myWebServiceMethodRequest>
                    </MyOffer:ws_MyWebServiceMethod>
                  </soapenv:Body>
                </soapenv:Envelope>      
              ]]>
        </d:RequestBody>
        <!-- Title, Rights and Description are optional and used to specify values to insert into the ATOM feed returned to the end user.  You can specify the element to contain a fixed message by providing a value for the element (this is the default value).  @d:Map is an XPath expression that points into the response returned by your service and is optional.  -->
        <d:Title d:Map="/MyResponse/Title">Default title.</d:Title>
        <d:Rights>© My copyright. This is a fixed response. It is okay to also add a d:Map attribute to override this text.</d:Rights>
        <d:Description d:Map="/MyResponse/Description"></d:Description>
        <d:Namespaces>
        <d:Namespace d:Prefix="p"  d:Uri="http://schemas.organization.net/2010/04/myNamespace" />
        <d:Namespace d:Prefix="p2" d:Uri="http://schemas.organization.net/2010/04/MyNamespace2" />
        </d:Namespaces>
        <!-- Parameters of the web service call:
        @Name should match exactly (case sensitive) the {…} placeholders in the @d:BaseUri, @d:UriTemplate, and d:RequestBody, i.e. “name” parameter in above BaseURI.
        @Mode is always "In", compatibility with CSDL
        @Type is the EDM.SimpleType of the parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx
        @d:Nullable indicates whether the parameter is required.
        @d:Regex - optional, attribute to describe the string, limiting unwanted input at the entry of the system
        @d:Description - optional, is used by Service Explorer as help information
        @d:SampleValues - optional, is used by Service Explorer as help information. Multiple Sample values are separated by '|', e.g. "804735132|234534224|23409823234"
        @d:Enum - optional for string type. Contains an enumeration of possible values separated by a '|', e.g. d:enum="english|metric|raw". Will be converted in a dropdown list in the Service Explorer.
        -->
        <Parameter name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="A name that cannot contain any spaces or non-alpha non-English characters"
        d:Enum="George|John|Thomas|James"
        d:SampleValues="George"/>
        <Parameter Name=" AccountKey" Mode="In" Type="String" d:Nullable="false" />

        <!-- d:ErrorHandling is an optional element. Use it define standardized errors by evaluating the service response. -->
        <d:ErrorHandling>
        <!-- Any number of d:Condition elements are allowed, they are evaluated in the order listed.
        @d:Match is an Xpath query on the service response, it should return true or false where true indicates an error.
        @d:httpStatusCode is the error code to return if an response matches the error.
        @d:errorMessage is the user friendly message to return when an error occurs.
        -->
        <d:Condition d:Match="/Result/ErrorMessage[text()='Invalid token']" d:HttpStatusCode="403" d:ErrorMessage="User cannot connect to the service." />
        </d:ErrorHandling>
           </FunctionImport>

            <!-- The EntityContainer defines the output data schema -->
        </EntityContainer>
        <!-- The EntityType @d:Map defines the repeating node (an XPath query) in the response (output data schema). -->
        <!-- If these nodes are outside a namespace, add the prefix in the xpath. -->
        <!--
        @Name - define your user readable name, will become an XML element in the ATOM feed, so comply with the XML element naming restrictions (no spaces or other illegal characters).
        @Type is the EDM.SimpleType of the parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx.
        @d:Map uses an Xpath query to point at the location to extract the content from your services response.
        The "." is relative to the repeating node in the EntityType @d:Map Xpath expression.
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
> <span data-ttu-id="62203-190">Altri esempi di CSDL di servizi Web sono disponibili nell'articolo relativo agli [esempi di mapping di un servizio Web esistente in OData tramite CSDL](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span><span class="sxs-lookup"><span data-stu-id="62203-190">View more CSDL Web Service examples in the article [Examples of mapping an existing web service to OData through CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span></span>
> 
> 

### <a name="dataservice-csdl-example"></a><span data-ttu-id="62203-191">Esempio di CSDL di DataService</span><span class="sxs-lookup"><span data-stu-id="62203-191">DataService CSDL Example</span></span>
<span data-ttu-id="62203-192">Si connette a un servizio che espone una vista o tabella di database come un endpoint. L'esempio seguente illustra due API per CSDL API basato su database (possibilità di utilizzare viste anziché tabelle).</span><span class="sxs-lookup"><span data-stu-id="62203-192">Connects to a service that is exposing a database table or view as an endpoint Below example shows two APIs for Data base based API CSDL (can use views rather than tables).</span></span>

        <?xml version="1.0"?>
        <!-- The namespace attribute below is used by our system to generate C#. You can change “MyCompany.MyOffer” to something that makes sense for you, but change “MyOffer” consistently throughout the document. -->
        <Schema Namespace="MyCompany.MyDataOffer" Alias="MyOffer" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ado/2009/08/edm">
        <!-- EntityContainer groups all the data service calls together into a single offering. Every web service call has a FunctionImport definition. -->
        <EntityContainer Name="MyOfferContainer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
            Think of the EntitySet as a Service
        @Name is used in the customer facing UI as name of the Service.
        @EntityType is used to point at the type definition (returned set of table columns). -->
        <EntitySet Name="CompanyInfoEntitySet" EntityType="MyOffer.CompanyInfo" />
        <EntitySet Name="ProductInfoEntitySet" EntityType="MyOffer.ProductInfo" />
        </EntityContainer>
        <!-- EntityType defines result (output); the table (or view) and columns to be returned by the data service.)
            Map is the schema.tabel or schema.view
            dals.TableName is the table Name
            Name is the name identifier for the EntityType and the Name of the service exposed to the client via the UI.
            dals:IsExposed determines if the table schema is exposed (generally true).
            dals:IsView (optional) true if this is based on a view rather than a table
            dals:TableSchema is the schema name of the table/view
        -->
        <EntityType
        Map="[dbo].[CompanyInfo]"
        dals:TableName="CompanyInfo"
        Name="CompanyInfo"
        dals:IsExposed="true"
        dals:IsView="false"
        dals:TableSchema="dbo"
        xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <!-- Property defines the column properties and the output of the service.
            dals:ColumnName is the name of the column in the table /view.
            Type is the emd.SimpleType
            Nullable determines if NULL is a valid output value
            dals.CharMaxLenght is the maximum length of the output value
            Name is the name of the Property and is exposed to the client facing UI
            dals:IsReturned is the Boolean that determines if the Service exposes this value to the client.
            IsQueryable is the Boolean that determines if the column can be used in a database query
            (For data Services: To improve Performance make sure that columns marked ISQueryable=”true” are in an index.)
            dals:OrdinalPosition is the numerical position x in the table or the View, where x is from 1 to the number of columns in the table.
            dals:DatabaseDataType is the data type of the column in the database, i.e. SQL data type dals:IsPrimaryKey indicates if the column is the Primary key in the table/view.  (The columns marked ISPrimaryKey are used in the Order by clause when returning data.)
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

## <a name="see-also"></a><span data-ttu-id="62203-193">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="62203-193">See Also</span></span>
* <span data-ttu-id="62203-194">Per ricevere formazione e informazioni sui nodi specifici e i relativi parametri, leggere l'articolo relativo ai [nodi di mapping di OData del servizio dati](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) per definizioni, spiegazioni, esempi e casi di utilizzo contestuali.</span><span class="sxs-lookup"><span data-stu-id="62203-194">If you are interested in learning and understanding the specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="62203-195">Per esaminare gli esempi, leggere l'articolo relativo agli [esempi di mapping di OData del servizio dati](marketplace-publishing-data-service-creation-odata-mapping-examples.md) per consultare il codice di esempio e comprendere il contesto e la sintassi del codice.</span><span class="sxs-lookup"><span data-stu-id="62203-195">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) to see sample code and understand code syntax and context.</span></span>
* <span data-ttu-id="62203-196">Per ripristinare il percorso prescritto per la pubblicazione di un servizio dati in Azure Marketplace, leggere questo articolo [Guida alla pubblicazione del servizio dati](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="62203-196">To return to the prescribed path for publishing a Data Service to the Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

