---
title: Origini dati supportate in Azure Analysis Services | Microsoft Docs
description: Descrive le origini dati supportate per i modelli di dati di Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 6ec63319-ff9b-4b01-a1cd-274481dc8995
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 8bd6c3b5a923ce2f3cd0f60af82e59c5cc27cbb4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="data-sources-supported-in-azure-analysis-services"></a><span data-ttu-id="1cf6f-103">Origini dati supportate in Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="1cf6f-103">Data sources supported in Azure Analysis Services</span></span>
<span data-ttu-id="1cf6f-104">I server Azure Analysis Services supportano la connessione alle origini dati nel cloud e locali nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="1cf6f-104">Azure Analysis Services servers support connecting to data sources in the cloud and on-premises in your organization.</span></span> <span data-ttu-id="1cf6f-105">Altre origine dati supportate vengono continuamente aggiunte.</span><span class="sxs-lookup"><span data-stu-id="1cf6f-105">Additional supported data sources are being added all the time.</span></span> <span data-ttu-id="1cf6f-106">Ricontrollare spesso.</span><span class="sxs-lookup"><span data-stu-id="1cf6f-106">Check back often.</span></span> 

<span data-ttu-id="1cf6f-107">Sono attualmente supportate le origini dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="1cf6f-107">The following data sources are currently supported:</span></span>

| <span data-ttu-id="1cf6f-108">Cloud</span><span class="sxs-lookup"><span data-stu-id="1cf6f-108">Cloud</span></span>  |
|---|
| <span data-ttu-id="1cf6f-109">Archiviazione BLOB di Azure*</span><span class="sxs-lookup"><span data-stu-id="1cf6f-109">Azure Blob Storage*</span></span>  |
| <span data-ttu-id="1cf6f-110">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="1cf6f-110">Azure SQL Database</span></span>  |
| <span data-ttu-id="1cf6f-111">Azure Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1cf6f-111">Azure Data Warehouse</span></span> |


| <span data-ttu-id="1cf6f-112">Locale</span><span class="sxs-lookup"><span data-stu-id="1cf6f-112">On-premises</span></span>  |   |   |   |
|---|---|---|---|
| <span data-ttu-id="1cf6f-113">Database di Access</span><span class="sxs-lookup"><span data-stu-id="1cf6f-113">Access Database</span></span>  | <span data-ttu-id="1cf6f-114">Cartella*</span><span class="sxs-lookup"><span data-stu-id="1cf6f-114">Folder*</span></span> | <span data-ttu-id="1cf6f-115">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="1cf6f-115">Oracle Database</span></span>  | <span data-ttu-id="1cf6f-116">Database Teradata</span><span class="sxs-lookup"><span data-stu-id="1cf6f-116">Teradata Database</span></span> |
| <span data-ttu-id="1cf6f-117">Active Directory*</span><span class="sxs-lookup"><span data-stu-id="1cf6f-117">Active Directory*</span></span>  | <span data-ttu-id="1cf6f-118">Documento JSON*</span><span class="sxs-lookup"><span data-stu-id="1cf6f-118">JSON document*</span></span>  | <span data-ttu-id="1cf6f-119">Database PostgreSQL*</span><span class="sxs-lookup"><span data-stu-id="1cf6f-119">Postgre SQL Database*</span></span>  |<span data-ttu-id="1cf6f-120">Tabella XML*</span><span class="sxs-lookup"><span data-stu-id="1cf6f-120">XML table*</span></span> |
| <span data-ttu-id="1cf6f-121">Analysis Services</span><span class="sxs-lookup"><span data-stu-id="1cf6f-121">Analysis Services</span></span>  | <span data-ttu-id="1cf6f-122">Righe da file binario*</span><span class="sxs-lookup"><span data-stu-id="1cf6f-122">Lines from binary*</span></span>  | <span data-ttu-id="1cf6f-123">SAP HANA*</span><span class="sxs-lookup"><span data-stu-id="1cf6f-123">SAP HANA*</span></span>  |
| <span data-ttu-id="1cf6f-124">Piattaforma di strumenti analitici</span><span class="sxs-lookup"><span data-stu-id="1cf6f-124">Analytics Platform System</span></span>  | <span data-ttu-id="1cf6f-125">MySQL Database</span><span class="sxs-lookup"><span data-stu-id="1cf6f-125">MySQL Database</span></span>  | <span data-ttu-id="1cf6f-126">SAP Business Warehouse*</span><span class="sxs-lookup"><span data-stu-id="1cf6f-126">SAP Business Warehouse*</span></span>  | |
| <span data-ttu-id="1cf6f-127">Dynamics CRM*</span><span class="sxs-lookup"><span data-stu-id="1cf6f-127">Dynamics CRM*</span></span>  | <span data-ttu-id="1cf6f-128">Feed OData*</span><span class="sxs-lookup"><span data-stu-id="1cf6f-128">OData Feed*</span></span>  | <span data-ttu-id="1cf6f-129">SharePoint*</span><span class="sxs-lookup"><span data-stu-id="1cf6f-129">SharePoint*</span></span>  |
| <span data-ttu-id="1cf6f-130">Cartella di lavoro di Excel</span><span class="sxs-lookup"><span data-stu-id="1cf6f-130">Excel workbook</span></span>  | <span data-ttu-id="1cf6f-131">Query ODBC</span><span class="sxs-lookup"><span data-stu-id="1cf6f-131">ODBC query</span></span>  | <span data-ttu-id="1cf6f-132">Database SQL</span><span class="sxs-lookup"><span data-stu-id="1cf6f-132">SQL Database</span></span>  |
| <span data-ttu-id="1cf6f-133">Exchange*</span><span class="sxs-lookup"><span data-stu-id="1cf6f-133">Exchange*</span></span>  | <span data-ttu-id="1cf6f-134">OLE DB</span><span class="sxs-lookup"><span data-stu-id="1cf6f-134">OLE DB</span></span>  | <span data-ttu-id="1cf6f-135">Database di Sybase</span><span class="sxs-lookup"><span data-stu-id="1cf6f-135">Sybase Database</span></span>  |

<span data-ttu-id="1cf6f-136">\* Solo modelli tabulari 1400.</span><span class="sxs-lookup"><span data-stu-id="1cf6f-136">\* Tabular 1400 models only.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="1cf6f-137">Per connettersi alle origini dati locali, in un computer dell'ambiente deve essere installato un [gateway dati locale](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="1cf6f-137">Connecting to on-premises data sources require an [On-premises data gateway](analysis-services-gateway.md) installed on a computer in your environment.</span></span>

## <a name="data-providers"></a><span data-ttu-id="1cf6f-138">Provider di dati</span><span class="sxs-lookup"><span data-stu-id="1cf6f-138">Data providers</span></span>

<span data-ttu-id="1cf6f-139">Durante la connessione a particolari origini dati, i modelli di dati di Azure Analysis Services possono richiedere provider di dati differenti.</span><span class="sxs-lookup"><span data-stu-id="1cf6f-139">Data models in Azure Analysis Services may require different data providers when connecting to certain data sources.</span></span> <span data-ttu-id="1cf6f-140">In alcuni casi, i modelli tabulari che si connettono alle origini dati usando provider nativi quali SQL Server Native Client (SQLNCLI11) possono restituire un errore.</span><span class="sxs-lookup"><span data-stu-id="1cf6f-140">In some cases, tabular models connecting to data sources using native providers such as SQL Server Native Client (SQLNCLI11) may return an error.</span></span>

<span data-ttu-id="1cf6f-141">Per modelli di dati che si connettono a un'origine dati cloud, ad esempio il database SQL di Azure, se si usano provider nativi diversi da SQLOLEDB, è possibile che venga visualizzato un messaggio di errore simile al seguente: **"Il provider 'SQLNCLI11.1' non è registrato"**.</span><span class="sxs-lookup"><span data-stu-id="1cf6f-141">For data models that connect to a cloud data source such as Azure SQL Database, if you use native providers other than SQLOLEDB, you may see error message: **“The provider 'SQLNCLI11.1' is not registered.”**</span></span> <span data-ttu-id="1cf6f-142">Se invece si dispone di un modello DirectQuery che si connette a origini dati locali, se si usano provider nativi è possibile che venga visualizzato un messaggio di errore simile al seguente: **"Errore durante la creazione del set di righe OLE DB. Sintassi errata vicino a 'LIMIT'"**.</span><span class="sxs-lookup"><span data-stu-id="1cf6f-142">Or, if you have a DirectQuery model connecting to on-premises data sources, if you use native providers you may see error message: **“Error creating OLE DB row set. Incorrect syntax near 'LIMIT'”**.</span></span>

<span data-ttu-id="1cf6f-143">I provider di origine dati seguenti sono supportati per i modelli di dati DirectQuery o in memoria nella connessione a origini dati nel cloud o in locale:</span><span class="sxs-lookup"><span data-stu-id="1cf6f-143">The following datasource providers are supported for in-memory or DirectQuery data models when connecting to data sources in the cloud or on-premises:</span></span>

### <a name="cloud"></a><span data-ttu-id="1cf6f-144">Cloud</span><span class="sxs-lookup"><span data-stu-id="1cf6f-144">Cloud</span></span>
| <span data-ttu-id="1cf6f-145">**Origine dati**</span><span class="sxs-lookup"><span data-stu-id="1cf6f-145">**Datasource**</span></span> | <span data-ttu-id="1cf6f-146">**In-memory**</span><span class="sxs-lookup"><span data-stu-id="1cf6f-146">**In-memory**</span></span> | <span data-ttu-id="1cf6f-147">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="1cf6f-147">**DirectQuery**</span></span> |
|  --- | --- | --- |
| <span data-ttu-id="1cf6f-148">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1cf6f-148">Azure SQL Data Warehouse</span></span> |<span data-ttu-id="1cf6f-149">Provider di dati .NET Framework per SQL Server</span><span class="sxs-lookup"><span data-stu-id="1cf6f-149">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="1cf6f-150">Provider di dati .NET Framework per SQL Server</span><span class="sxs-lookup"><span data-stu-id="1cf6f-150">.NET Framework Data Provider for SQL Server</span></span> |
| <span data-ttu-id="1cf6f-151">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="1cf6f-151">Azure SQL Database</span></span> |<span data-ttu-id="1cf6f-152">Provider di dati .NET Framework per SQL Server</span><span class="sxs-lookup"><span data-stu-id="1cf6f-152">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="1cf6f-153">Provider di dati .NET Framework per SQL Server</span><span class="sxs-lookup"><span data-stu-id="1cf6f-153">.NET Framework Data Provider for SQL Server</span></span> | |

### <a name="on-premises-via-gateway"></a><span data-ttu-id="1cf6f-154">Locale (tramite gateway)</span><span class="sxs-lookup"><span data-stu-id="1cf6f-154">On-premises (via Gateway)</span></span>
|<span data-ttu-id="1cf6f-155">**Origine dati**</span><span class="sxs-lookup"><span data-stu-id="1cf6f-155">**Datasource**</span></span> | <span data-ttu-id="1cf6f-156">**In-memory**</span><span class="sxs-lookup"><span data-stu-id="1cf6f-156">**In-memory**</span></span> | <span data-ttu-id="1cf6f-157">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="1cf6f-157">**DirectQuery**</span></span> |
|  --- | --- | --- |
| <span data-ttu-id="1cf6f-158">SQL Server</span><span class="sxs-lookup"><span data-stu-id="1cf6f-158">SQL Server</span></span> |<span data-ttu-id="1cf6f-159">SQL Server Native Client 11.0</span><span class="sxs-lookup"><span data-stu-id="1cf6f-159">SQL Server Native Client 11.0</span></span> |<span data-ttu-id="1cf6f-160">Provider di dati .NET Framework per SQL Server</span><span class="sxs-lookup"><span data-stu-id="1cf6f-160">.NET Framework Data Provider for SQL Server</span></span> |
| <span data-ttu-id="1cf6f-161">SQL Server</span><span class="sxs-lookup"><span data-stu-id="1cf6f-161">SQL Server</span></span> |<span data-ttu-id="1cf6f-162">Provider Microsoft OLE DB per SQL Server</span><span class="sxs-lookup"><span data-stu-id="1cf6f-162">Microsoft OLE DB Provider for SQL Server</span></span> |<span data-ttu-id="1cf6f-163">Provider di dati .NET Framework per SQL Server</span><span class="sxs-lookup"><span data-stu-id="1cf6f-163">.NET Framework Data Provider for SQL Server</span></span> | |
| <span data-ttu-id="1cf6f-164">SQL Server</span><span class="sxs-lookup"><span data-stu-id="1cf6f-164">SQL Server</span></span> |<span data-ttu-id="1cf6f-165">Provider di dati .NET Framework per SQL Server</span><span class="sxs-lookup"><span data-stu-id="1cf6f-165">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="1cf6f-166">Provider di dati .NET Framework per SQL Server</span><span class="sxs-lookup"><span data-stu-id="1cf6f-166">.NET Framework Data Provider for SQL Server</span></span> | |
| <span data-ttu-id="1cf6f-167">Oracle</span><span class="sxs-lookup"><span data-stu-id="1cf6f-167">Oracle</span></span> |<span data-ttu-id="1cf6f-168">Provider Microsoft OLE DB per Oracle</span><span class="sxs-lookup"><span data-stu-id="1cf6f-168">Microsoft OLE DB Provider for Oracle</span></span> |<span data-ttu-id="1cf6f-169">Provider di dati Oracle per .NET</span><span class="sxs-lookup"><span data-stu-id="1cf6f-169">Oracle Data Provider for .NET</span></span> | |
| <span data-ttu-id="1cf6f-170">Oracle</span><span class="sxs-lookup"><span data-stu-id="1cf6f-170">Oracle</span></span> |<span data-ttu-id="1cf6f-171">Provider di dati Oracle per .NET</span><span class="sxs-lookup"><span data-stu-id="1cf6f-171">Oracle Data Provider for .NET</span></span> |<span data-ttu-id="1cf6f-172">Provider di dati Oracle per .NET</span><span class="sxs-lookup"><span data-stu-id="1cf6f-172">Oracle Data Provider for .NET</span></span> | |
| <span data-ttu-id="1cf6f-173">Teradata</span><span class="sxs-lookup"><span data-stu-id="1cf6f-173">Teradata</span></span> |<span data-ttu-id="1cf6f-174">Provider OLE DB per Teradata</span><span class="sxs-lookup"><span data-stu-id="1cf6f-174">OLE DB Provider for Teradata</span></span> |<span data-ttu-id="1cf6f-175">Provider di dati Teradata per .NET</span><span class="sxs-lookup"><span data-stu-id="1cf6f-175">Teradata Data Provider for .NET</span></span> | |
| <span data-ttu-id="1cf6f-176">Teradata</span><span class="sxs-lookup"><span data-stu-id="1cf6f-176">Teradata</span></span> |<span data-ttu-id="1cf6f-177">Provider di dati Teradata per .NET</span><span class="sxs-lookup"><span data-stu-id="1cf6f-177">Teradata Data Provider for .NET</span></span> |<span data-ttu-id="1cf6f-178">Provider di dati Teradata per .NET</span><span class="sxs-lookup"><span data-stu-id="1cf6f-178">Teradata Data Provider for .NET</span></span> | |
| <span data-ttu-id="1cf6f-179">Piattaforma di strumenti analitici</span><span class="sxs-lookup"><span data-stu-id="1cf6f-179">Analytics Platform System</span></span> |<span data-ttu-id="1cf6f-180">Provider di dati .NET Framework per SQL Server</span><span class="sxs-lookup"><span data-stu-id="1cf6f-180">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="1cf6f-181">Provider di dati .NET Framework per SQL Server</span><span class="sxs-lookup"><span data-stu-id="1cf6f-181">.NET Framework Data Provider for SQL Server</span></span> | |

> [!NOTE]
> <span data-ttu-id="1cf6f-182">Quando si usa il gateway locale, verificare che siano installati provider a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="1cf6f-182">Ensure 64-bit providers are installed when using On-premises gateway.</span></span>
> 
> 

<span data-ttu-id="1cf6f-183">Durante la migrazione di un modello tabulare SQL Server Analysis Services locale in Azure Analysis Services, può essere necessario modificare il provider.</span><span class="sxs-lookup"><span data-stu-id="1cf6f-183">When migrating an on-premises SQL Server Analysis Services tabular model to Azure Analysis Services, it may be necessary to change the provider.</span></span>

<span data-ttu-id="1cf6f-184">**Per specificare un provider dell'origine dati**</span><span class="sxs-lookup"><span data-stu-id="1cf6f-184">**To specify a datasource provider**</span></span>

1. <span data-ttu-id="1cf6f-185">In SSDT > **Esplora modelli tabulari** > **Origini dati** fare clic con il pulsante destro del mouse su una connessione a un'origine dati e scegliere **Modifica origine dati**.</span><span class="sxs-lookup"><span data-stu-id="1cf6f-185">In SSDT > **Tabular Model Explorer** > **Data Sources**, right-click a data source connection, and then click **Edit Data Source**.</span></span>
2. <span data-ttu-id="1cf6f-186">In **Modifica connessione** fare clic su **Avanzate** per aprire la finestra Proprietà avanzate.</span><span class="sxs-lookup"><span data-stu-id="1cf6f-186">In **Edit Connection**, click **Advanced** to open the Advance properties window.</span></span>
3. <span data-ttu-id="1cf6f-187">Selezionare **Impostazione delle proprietà avanzate** > **Provider** e quindi scegliere il provider appropriato.</span><span class="sxs-lookup"><span data-stu-id="1cf6f-187">In **Set Advanced Properties** > **Providers**, then select the appropriate provider.</span></span>

## <a name="impersonation"></a><span data-ttu-id="1cf6f-188">Rappresentazione</span><span class="sxs-lookup"><span data-stu-id="1cf6f-188">Impersonation</span></span>
<span data-ttu-id="1cf6f-189">In alcuni casi può essere necessario specificare un account di rappresentazione differente.</span><span class="sxs-lookup"><span data-stu-id="1cf6f-189">In some cases, it may be necessary to specify a different impersonation account.</span></span> <span data-ttu-id="1cf6f-190">L'account di rappresentazione può essere specificato in SSDT o SSMS.</span><span class="sxs-lookup"><span data-stu-id="1cf6f-190">Impersonation account can be specified in SSDT or SSMS.</span></span>

<span data-ttu-id="1cf6f-191">Per le origini dati locali:</span><span class="sxs-lookup"><span data-stu-id="1cf6f-191">For on-premises data sources:</span></span>

* <span data-ttu-id="1cf6f-192">Se si usa l'autenticazione SQL, la rappresentazione deve essere l'account del servizio.</span><span class="sxs-lookup"><span data-stu-id="1cf6f-192">If using SQL authentication, impersonation should be Service Account.</span></span>
* <span data-ttu-id="1cf6f-193">Se si usa l'autenticazione di Windows, impostare nome utente/password di Windows.</span><span class="sxs-lookup"><span data-stu-id="1cf6f-193">If using Windows authentication, set Windows user/password.</span></span> <span data-ttu-id="1cf6f-194">Per SQL Server, l'autenticazione di Windows con un account di rappresentazione specifico è supportata solo per i modelli di dati In-memory.</span><span class="sxs-lookup"><span data-stu-id="1cf6f-194">For SQL Server, Windows authentication with a specific impersonation account is supported only for in-memory data models.</span></span>

<span data-ttu-id="1cf6f-195">Per le origini dati cloud:</span><span class="sxs-lookup"><span data-stu-id="1cf6f-195">For cloud data sources:</span></span>

* <span data-ttu-id="1cf6f-196">Se si usa l'autenticazione SQL, la rappresentazione deve essere l'account del servizio.</span><span class="sxs-lookup"><span data-stu-id="1cf6f-196">If using SQL authentication, impersonation should be Service Account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1cf6f-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1cf6f-197">Next steps</span></span>
<span data-ttu-id="1cf6f-198">Se si dispone di origini dati locali, verificare di installare il [gateway locale](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="1cf6f-198">If you have on-premises data sources, be sure to install the [On-premises gateway](analysis-services-gateway.md).</span></span>   
<span data-ttu-id="1cf6f-199">Per altre informazioni sulla gestione del server in SSDT o SSMS, vedere [Manage your server](analysis-services-manage.md) (Gestione del server).</span><span class="sxs-lookup"><span data-stu-id="1cf6f-199">To learn more about managing your server in SSDT or SSMS, see [Manage your server](analysis-services-manage.md).</span></span>

