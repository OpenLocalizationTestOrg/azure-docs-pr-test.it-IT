---
title: aaaGuide toocreating un servizio dati per hello Marketplace | Documenti Microsoft
description: Istruzioni dettagliate su come toocreate, certificare e distribuire un servizio dati per acquistano su hello Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 148f8638-ee80-4100-8d63-5afa4167ca1b
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 8917a43959834d15f70866297f98d24bb83e217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="examples-of-mapping-an-existing-web-service-tooodata-through-csdls"></a><span data-ttu-id="34af8-103">Esempi di mapping esistente web servizio tooOData tramite CSDLs</span><span class="sxs-lookup"><span data-stu-id="34af8-103">Examples of mapping an existing web service tooOData through CSDLs</span></span>
> [!IMPORTANT]
> <span data-ttu-id="34af8-104">**In questo momento non stiamo più caricando nuovi editori di servizi dati. I nuovi servizi dati non saranno approvati per l'elencazione.**</span><span class="sxs-lookup"><span data-stu-id="34af8-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="34af8-105">Se si dispone di un'applicazione SaaS di business si desidera toopublish in AppSource è possibile trovare ulteriori informazioni [qui](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="34af8-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="34af8-106">Se si utilizzano applicazioni IaaS sviluppatore del servizio si sarebbe ad esempio toopublish in Azure Marketplace è possibile trovare ulteriori informazioni [qui](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="34af8-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

## <a name="example-functionimport-for-raw-data-returned-using-post"></a><span data-ttu-id="34af8-107">Esempio: FunctionImport per i dati "Raw" restituiti utilizzando "POST"</span><span class="sxs-lookup"><span data-stu-id="34af8-107">Example: FunctionImport for "Raw" data returned using "POST"</span></span>
<span data-ttu-id="34af8-108">Utilizzare toocreate dati non elaborati POST una forma subordinata di nuovo e restituire il relativo server definiti URL(location) o tooupdate parte subordinata server hello hello URL.</span><span class="sxs-lookup"><span data-stu-id="34af8-108">Use POST Raw data toocreate a new subordinate and return its server defined URL(location) or tooupdate part of hello subordinate at hello server defined URL.</span></span>  <span data-ttu-id="34af8-109">In un flusso, vale a dire non strutturato, ad esempio hello subordinati.</span><span class="sxs-lookup"><span data-stu-id="34af8-109">Where hello subordinate is a stream, i.e. unstructured, ex.</span></span> <span data-ttu-id="34af8-110">un file di testo.</span><span class="sxs-lookup"><span data-stu-id="34af8-110">a text file.</span></span>  <span data-ttu-id="34af8-111">Prestare attenzione che POST non è idempotente senza un percorso.</span><span class="sxs-lookup"><span data-stu-id="34af8-111">Beware POST in not idempotent without a location.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="AddUsageEvent" ReturnType="Raw(text/plain)" d:EncodeParameterValues="true" d:AllowedHttpMethods="POST" d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Add usage event (data acquisition)</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-using-delete"></a><span data-ttu-id="34af8-112">Esempio: FunctionImport utilizzando "DELETE"</span><span class="sxs-lookup"><span data-stu-id="34af8-112">Example: FunctionImport using "DELETE"</span></span>
<span data-ttu-id="34af8-113">Utilizzare DELETE tooremove un URI specificato.</span><span class="sxs-lookup"><span data-stu-id="34af8-113">Use DELETE tooremove a specified URI.</span></span>

        <EntitySet Name="DeleteUsageFileEntitySet" EntityType="MyOffer.DeleteUsageFileEntity" />
        <FunctionImport Name="DeleteUsageFile" EntitySet="DeleteUsageFileEntitySet" ReturnType="Collection(MyOffer.DeleteUsageFileEntity)"  d:AllowedHttpMethods="DELETE" d:EncodeParameterValues="true” d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643" >
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Delete usage File</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>
        <EntityType Name="DeleteUsageFileEntity" d:Map="//boolean">
        <Property Name="boolean" Type="String" Nullable="true" d:Map="./boolean" />
        </EntityType>

## <a name="example-functionimport-using-post"></a><span data-ttu-id="34af8-114">Esempio: FunctionImport utilizzando "POST"</span><span class="sxs-lookup"><span data-stu-id="34af8-114">Example: FunctionImport using "POST"</span></span>
<span data-ttu-id="34af8-115">Utilizzare toocreate dati non elaborati POST una forma subordinata di nuovo e restituire il relativo server definiti URL(location) o tooupdate parte subordinata server hello hello URL.</span><span class="sxs-lookup"><span data-stu-id="34af8-115">Use POST Raw data toocreate a new subordinate and return its server defined URL(location) or tooupdate part of hello subordinate at hello server defined URL.</span></span>  <span data-ttu-id="34af8-116">Dove subordinati hello sono una struttura.</span><span class="sxs-lookup"><span data-stu-id="34af8-116">Where hello subordinate is a structure.</span></span> <span data-ttu-id="34af8-117">Prestare attenzione che POST non è idempotente senza un percorso.</span><span class="sxs-lookup"><span data-stu-id="34af8-117">Beware POST is not idempotent without a location.</span></span>

        <EntitySet Name="CreateANewModelEntitySet2" EntityType=" MyOffer.CreateANewModelEntity2" />
        <FunctionImport Name="CreateModel" EntitySet="CreateANewModelEntitySet2" ReturnType="Collection(MyOffer.CreateANewModelEntity2)" d:EncodeParameterValues="true" d:AllowedHttpMethods="POST" d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Create A New Model</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-using-put"></a><span data-ttu-id="34af8-118">Esempio: FunctionImport mediante "PUT"</span><span class="sxs-lookup"><span data-stu-id="34af8-118">Example: FunctionImport using "PUT"</span></span>
<span data-ttu-id="34af8-119">Utilizzare PUT toocreate una forma subordinata di nuovo o forma subordinata intero tooupdate hello in un server definito dall'URL.</span><span class="sxs-lookup"><span data-stu-id="34af8-119">Use PUT toocreate a new subordinate or tooupdate hello entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="34af8-120">Hello subordinate, in cui una struttura, PUT è idempotente in modo più occorrenze comporterà hello stesso stato, ovvero</span><span class="sxs-lookup"><span data-stu-id="34af8-120">Where hello subordinate is a structure, PUT is idempotent so multiple occurrences will result in hello same state, i.e</span></span> <span data-ttu-id="34af8-121">x=5.</span><span class="sxs-lookup"><span data-stu-id="34af8-121">x=5.</span></span>  <span data-ttu-id="34af8-122">PUT deve essere utilizzato con hello completa del contenuto di hello specificato risorse.</span><span class="sxs-lookup"><span data-stu-id="34af8-122">Put should be used with hello full content of hello specified resource.</span></span>

        <EntitySet Name="UpdateAnExistingModelEntitySet" EntityType="MyOffer.UpdateAnExistingModelEntity" />
        <FunctionImport Name="UpdateModel" EntitySet="UpdateAnExistingModelEntitySet" ReturnType="Collection(MyOffer.UpdateAnExistingModelEntity)" d:EncodeParameterValues="true" d:AllowedHttpMethods="PUT" d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Update an Existing Model</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>
        <EntityType Name="UpdateAnExistingModelEntity" d:Map="//string">
        <Property Name="string"     Type="String" Nullable="true" d:Map="./string" />
        </EntityType>


## <a name="example-functionimport-for-raw-data-returned-using-put"></a><span data-ttu-id="34af8-123">Esempio: FunctionImport per i dati "Raw" restituiti utilizzando "PUT"</span><span class="sxs-lookup"><span data-stu-id="34af8-123">Example: FunctionImport for "Raw" data returned using "PUT"</span></span>
<span data-ttu-id="34af8-124">Utilizzare toocreate dati inseriti non elaborato una forma subordinata di nuovo o subordinati di tooupdate hello intera in un URL del server definito.</span><span class="sxs-lookup"><span data-stu-id="34af8-124">Use PUT Raw data toocreate a new subordinate or tooupdate hello entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="34af8-125">In un flusso, vale a dire non strutturato, ad esempio hello subordinati.</span><span class="sxs-lookup"><span data-stu-id="34af8-125">Where hello subordinate is a stream, i.e. unstructured, ex.</span></span> <span data-ttu-id="34af8-126">un file di testo.</span><span class="sxs-lookup"><span data-stu-id="34af8-126">a text file.</span></span>  <span data-ttu-id="34af8-127">PUT è idempotente in modo più occorrenze comporterà hello stesso stato, ovvero</span><span class="sxs-lookup"><span data-stu-id="34af8-127">PUT is idempotent so multiple occurrences will result in hello same state, i.e</span></span> <span data-ttu-id="34af8-128">x=5.</span><span class="sxs-lookup"><span data-stu-id="34af8-128">x=5.</span></span>  <span data-ttu-id="34af8-129">PUT deve essere utilizzato con hello completa del contenuto di hello specificato risorse.</span><span class="sxs-lookup"><span data-stu-id="34af8-129">Put should be used with hello full content of hello specified resource.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="CancelBuild” ReturnType="Raw(text/plain)" d:AllowedHttpMethods="PUT" d:EncodeParameterValues="true" d:BaseUri=” http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Cancel Build</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>


## <a name="example-functionimport-for-raw-data-returned-using-get"></a><span data-ttu-id="34af8-130">Esempio: FunctionImport per i dati "Raw" restituiti utilizzando "GET"</span><span class="sxs-lookup"><span data-stu-id="34af8-130">Example: FunctionImport for "Raw" data returned using "GET"</span></span>
<span data-ttu-id="34af8-131">Utilizzare Raw ottenere dati tooreturn una forma subordinata che non è strutturata, ad esempio testo.</span><span class="sxs-lookup"><span data-stu-id="34af8-131">Use GET Raw data tooreturn a subordinate that is unstructured, i.e. text.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="GetModelUsageFile" ReturnType="Raw(text/plain)" d:EncodeParameterValues="true" d:AllowedHttpMethods="GET" d:BaseUri="https://cmla.cloudapp.net/api2/model/builder/build?buildId={buildId}&amp;apiVersion={apiVersion}">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Download A Models Usage File</d:Description>
        <d:Headers>
        <d:Header d:Name="Accept" d:Value="application/xml,application/xhtml+xml,text/html;" />
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-for-paging-through-returned-data"></a><span data-ttu-id="34af8-132">Esempio: FunctionImport per "Paging" tramite dati restituiti</span><span class="sxs-lookup"><span data-stu-id="34af8-132">Example: FunctionImport for "Paging" through returned data</span></span>
<span data-ttu-id="34af8-133">Utilizzare il paging RESTful implementato tramite i dati con GET.</span><span class="sxs-lookup"><span data-stu-id="34af8-133">Use implement RESTful paging through your data with GET.</span></span>  <span data-ttu-id="34af8-134">Paging predefinito viene impostato too100 riga per ogni pagina di dati.</span><span class="sxs-lookup"><span data-stu-id="34af8-134">Default paging is set too100 row per page of data.</span></span>

        <EntitySet Name=”CropEntitySet" EntityType="MyOffer.CropEntity" />
        <FunctionImport    Name="GetCropReport" EntitySet="CropEntitySet” ReturnType="Collection(MyOffer.CropEntity)" d:EmitSelfLink="false" d:EncodeParameterValues="true" d:Paging="SkipTake" d:MaxPageSize="100" d:BaseUri="http://api.mydata.org/Crop? report={report}&amp;series={series}&amp;start={$skip}&amp;size=100">
        <Parameter Name="report" Type="Int32" Mode="In" Nullable="false" d:SampleValues="4"  d:enum="1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19"  />
        <Parameter Name="series"    Type="String"    Mode="In" Nullable="false" d:SampleValues="FARM" />
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="text/xml;charset=UTF-8" />
        </d:Headers>
        <d:Namespaces>
        <d:Namespace d:Prefix="diffgr" d:Uri="urn:schemas-microsoft-com:xml-diffgram-v1" />
        </d:Namespaces>
        </FunctionImport>

## <a name="see-also"></a><span data-ttu-id="34af8-135">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="34af8-135">See Also</span></span>
* <span data-ttu-id="34af8-136">Se si è interessati alla comprensione hello l'intero processo di mapping di OData e lo scopo, leggere questo articolo [Mapping di dati del servizio OData](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definizioni, strutture e le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="34af8-136">If you are interested in understanding hello overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definitions, structures, and instructions.</span></span>
* <span data-ttu-id="34af8-137">Se è interessati a learning e informazioni sui nodi specifici di hello e i relativi parametri, leggere questo articolo [nodi Mapping di dati del servizio OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) per le definizioni e le spiegazioni, esempi e il contesto casi di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="34af8-137">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="34af8-138">toohello tooreturn previsto percorso per la pubblicazione toohello un servizio dati Azure Marketplace, leggere questo articolo [Guida alla pubblicazione di dati del servizio](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="34af8-138">tooreturn toohello prescribed path for publishing a Data Service toohello Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

