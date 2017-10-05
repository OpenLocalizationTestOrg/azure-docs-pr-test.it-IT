---
title: Guida alla creazione di un servizio dati per il Marketplace | Documentazione Microsoft
description: Istruzioni dettagliate su come creare, certificare e distribuire un servizio dati per l'acquisto in Azure Marketplace.
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
ms.openlocfilehash: 2ab624941fc385f14b62bb5d743927f157955845
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="examples-of-mapping-an-existing-web-service-to-odata-through-csdls"></a><span data-ttu-id="c01e2-103">Esempi di mapping di un servizio Web esistente in OData tramite CSDL</span><span class="sxs-lookup"><span data-stu-id="c01e2-103">Examples of mapping an existing web service to OData through CSDLs</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c01e2-104">**In questo momento non stiamo più caricando nuovi editori di servizi dati. I nuovi servizi dati non saranno approvati per l'elencazione.**</span><span class="sxs-lookup"><span data-stu-id="c01e2-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="c01e2-105">Se si dispone di un'applicazione aziendale SaaS che si vuole pubblicare in AppSource, è possibile trovare altre informazioni [qui](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="c01e2-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="c01e2-106">Se si dispone di un'applicazione IaaS o di un servizio per gli sviluppatori che si vuole pubblicare in Azure Marketplace, è possibile trovare altre informazioni [qui](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="c01e2-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

## <a name="example-functionimport-for-raw-data-returned-using-post"></a><span data-ttu-id="c01e2-107">Esempio: FunctionImport per i dati "Raw" restituiti utilizzando "POST"</span><span class="sxs-lookup"><span data-stu-id="c01e2-107">Example: FunctionImport for "Raw" data returned using "POST"</span></span>
<span data-ttu-id="c01e2-108">Utilizzare dati Raw POST per creare un nuovo subordinato e restituire il relativo URL definito dal server (percorso) o per aggiornare una parte del subordinato nell’URL definito dal server.</span><span class="sxs-lookup"><span data-stu-id="c01e2-108">Use POST Raw data to create a new subordinate and return its server defined URL(location) or to update part of the subordinate at the server defined URL.</span></span>  <span data-ttu-id="c01e2-109">Dove il subordinato è una struttura, ad esempio</span><span class="sxs-lookup"><span data-stu-id="c01e2-109">Where the subordinate is a stream, i.e.</span></span> <span data-ttu-id="c01e2-110">non strutturata, come</span><span class="sxs-lookup"><span data-stu-id="c01e2-110">unstructured, ex.</span></span> <span data-ttu-id="c01e2-111">un file di testo.</span><span class="sxs-lookup"><span data-stu-id="c01e2-111">a text file.</span></span>  <span data-ttu-id="c01e2-112">Prestare attenzione che POST non è idempotente senza un percorso.</span><span class="sxs-lookup"><span data-stu-id="c01e2-112">Beware POST in not idempotent without a location.</span></span>

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

## <a name="example-functionimport-using-delete"></a><span data-ttu-id="c01e2-113">Esempio: FunctionImport utilizzando "DELETE"</span><span class="sxs-lookup"><span data-stu-id="c01e2-113">Example: FunctionImport using "DELETE"</span></span>
<span data-ttu-id="c01e2-114">Utilizzare DELETE per rimuovere un URI specificato.</span><span class="sxs-lookup"><span data-stu-id="c01e2-114">Use DELETE to remove a specified URI.</span></span>

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

## <a name="example-functionimport-using-post"></a><span data-ttu-id="c01e2-115">Esempio: FunctionImport utilizzando "POST"</span><span class="sxs-lookup"><span data-stu-id="c01e2-115">Example: FunctionImport using "POST"</span></span>
<span data-ttu-id="c01e2-116">Utilizzare dati Raw POST per creare un nuovo subordinato e restituire il relativo URL definito dal server (percorso) o per aggiornare una parte del subordinato nell’URL definito dal server.</span><span class="sxs-lookup"><span data-stu-id="c01e2-116">Use POST Raw data to create a new subordinate and return its server defined URL(location) or to update part of the subordinate at the server defined URL.</span></span>  <span data-ttu-id="c01e2-117">In cui la subordinata è una struttura.</span><span class="sxs-lookup"><span data-stu-id="c01e2-117">Where the subordinate is a structure.</span></span> <span data-ttu-id="c01e2-118">Prestare attenzione che POST non è idempotente senza un percorso.</span><span class="sxs-lookup"><span data-stu-id="c01e2-118">Beware POST is not idempotent without a location.</span></span>

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

## <a name="example-functionimport-using-put"></a><span data-ttu-id="c01e2-119">Esempio: FunctionImport mediante "PUT"</span><span class="sxs-lookup"><span data-stu-id="c01e2-119">Example: FunctionImport using "PUT"</span></span>
<span data-ttu-id="c01e2-120">Utilizzare PUT per creare un nuovo subordinato o per aggiornare l'intero subordinato in un URL definito dal server.</span><span class="sxs-lookup"><span data-stu-id="c01e2-120">Use PUT to create a new subordinate or to update the entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="c01e2-121">Dove il subordinato è una struttura, PUT è idempotente, quindi più occorrenze comportano lo stesso stato, ovvero</span><span class="sxs-lookup"><span data-stu-id="c01e2-121">Where the subordinate is a structure, PUT is idempotent so multiple occurrences will result in the same state, i.e</span></span> <span data-ttu-id="c01e2-122">x=5.</span><span class="sxs-lookup"><span data-stu-id="c01e2-122">x=5.</span></span>  <span data-ttu-id="c01e2-123">PUT deve essere utilizzato con il contenuto completo della risorsa specificata.</span><span class="sxs-lookup"><span data-stu-id="c01e2-123">Put should be used with the full content of the specified resource.</span></span>

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


## <a name="example-functionimport-for-raw-data-returned-using-put"></a><span data-ttu-id="c01e2-124">Esempio: FunctionImport per i dati "Raw" restituiti utilizzando "PUT"</span><span class="sxs-lookup"><span data-stu-id="c01e2-124">Example: FunctionImport for "Raw" data returned using "PUT"</span></span>
<span data-ttu-id="c01e2-125">Utilizzare dati Raw PUT per creare un nuovo subordinato o per aggiornare l'intero subordinato in un URL definito dal server.</span><span class="sxs-lookup"><span data-stu-id="c01e2-125">Use PUT Raw data to create a new subordinate or to update the entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="c01e2-126">Dove il subordinato è una struttura, ad esempio</span><span class="sxs-lookup"><span data-stu-id="c01e2-126">Where the subordinate is a stream, i.e.</span></span> <span data-ttu-id="c01e2-127">non strutturata, come</span><span class="sxs-lookup"><span data-stu-id="c01e2-127">unstructured, ex.</span></span> <span data-ttu-id="c01e2-128">un file di testo.</span><span class="sxs-lookup"><span data-stu-id="c01e2-128">a text file.</span></span>  <span data-ttu-id="c01e2-129">PUT è idempotente, quindi più occorrenze comportano lo stesso stato, ovvero</span><span class="sxs-lookup"><span data-stu-id="c01e2-129">PUT is idempotent so multiple occurrences will result in the same state, i.e</span></span> <span data-ttu-id="c01e2-130">x=5.</span><span class="sxs-lookup"><span data-stu-id="c01e2-130">x=5.</span></span>  <span data-ttu-id="c01e2-131">PUT deve essere utilizzato con il contenuto completo della risorsa specificata.</span><span class="sxs-lookup"><span data-stu-id="c01e2-131">Put should be used with the full content of the specified resource.</span></span>

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


## <a name="example-functionimport-for-raw-data-returned-using-get"></a><span data-ttu-id="c01e2-132">Esempio: FunctionImport per i dati "Raw" restituiti utilizzando "GET"</span><span class="sxs-lookup"><span data-stu-id="c01e2-132">Example: FunctionImport for "Raw" data returned using "GET"</span></span>
<span data-ttu-id="c01e2-133">Utilizzare dati Raw GET per restituire un subordinato non strutturato, ad esempio testo.</span><span class="sxs-lookup"><span data-stu-id="c01e2-133">Use GET Raw data to return a subordinate that is unstructured, i.e. text.</span></span>

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

## <a name="example-functionimport-for-paging-through-returned-data"></a><span data-ttu-id="c01e2-134">Esempio: FunctionImport per "Paging" tramite dati restituiti</span><span class="sxs-lookup"><span data-stu-id="c01e2-134">Example: FunctionImport for "Paging" through returned data</span></span>
<span data-ttu-id="c01e2-135">Utilizzare il paging RESTful implementato tramite i dati con GET.</span><span class="sxs-lookup"><span data-stu-id="c01e2-135">Use implement RESTful paging through your data with GET.</span></span>  <span data-ttu-id="c01e2-136">Il paging predefinito è impostato su 100 righe per ogni pagina di dati.</span><span class="sxs-lookup"><span data-stu-id="c01e2-136">Default paging is set to 100 row per page of data.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="c01e2-137">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c01e2-137">See Also</span></span>
* <span data-ttu-id="c01e2-138">Per apprendere il processo di mapping generale e lo scopo di OData , leggere questo articolo [Mapping di OData del servizio dati](marketplace-publishing-data-service-creation-odata-mapping.md) per esaminare le definizioni, le strutture e le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="c01e2-138">If you are interested in understanding the overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) to review definitions, structures, and instructions.</span></span>
* <span data-ttu-id="c01e2-139">Per ricevere formazione e informazioni sui nodi specifici e i relativi parametri, leggere questo articolo [Nodi di mapping di OData del servizio dati](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) per le definizioni e le spiegazioni e per esempi e casi di utilizzo contestuali.</span><span class="sxs-lookup"><span data-stu-id="c01e2-139">If you are interested in learning and understanding the specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="c01e2-140">Per ripristinare il percorso prescritto per la pubblicazione di un servizio dati in Azure Marketplace, leggere l'articolo di [guida alla pubblicazione del servizio dati](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="c01e2-140">To return to the prescribed path for publishing a Data Service to the Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

