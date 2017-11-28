---
title: origini dei dati in Azure Data Catalog aaaSupported | Documenti Microsoft
description: In questo articolo vengono elencate le specifiche di origini dati hello attualmente supportato.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: jstevens
editor: 
tags: 
ms.assetid: fd4345ca-2ed8-4c5e-9c4b-f954be2fc9f9
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 4bfcabf31bf9fd781c939a5026abc42a5407df32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="supported-data-sources-in-azure-data-catalog"></a><span data-ttu-id="1a76a-103">Origini dati supportate in Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="1a76a-103">Supported data sources in Azure Data Catalog</span></span>

<span data-ttu-id="1a76a-104">È possibile pubblicare metadati tramite un'API pubblica o un clic-strumento di registrazione una volta, o immettendo manualmente le informazioni direttamente toohello Azure Data Catalog portale web.</span><span class="sxs-lookup"><span data-stu-id="1a76a-104">You can publish metadata by using a public API or a click-once registration tool, or by manually entering information directly toohello Azure Data Catalog web portal.</span></span> <span data-ttu-id="1a76a-105">Hello nella tabella seguente sono riepilogate tutte le origini dati che sono attualmente supportate dal catalogo hello e hello funzionalità di pubblicazione per ogni.</span><span class="sxs-lookup"><span data-stu-id="1a76a-105">hello following table summarizes all data sources that are supported by hello catalog today, and hello publishing capabilities for each.</span></span> <span data-ttu-id="1a76a-106">È inoltre elencati hello strumenti dati esterni che ogni origine dati può essere avviato dalla nostra esperienza del portale "open-in".</span><span class="sxs-lookup"><span data-stu-id="1a76a-106">Also listed are hello external data tools that each data source can launch from our portal "open-in" experience.</span></span> <span data-ttu-id="1a76a-107">Hello seconda tabella contiene una specifica più tecnica di ogni proprietà di connessione dell'origine dati.</span><span class="sxs-lookup"><span data-stu-id="1a76a-107">hello second table contains a more technical specification of each data-source connection property.</span></span>


## <a name="list-of-supported-data-sources"></a><span data-ttu-id="1a76a-108">Elenco di origini dati supportate</span><span class="sxs-lookup"><span data-stu-id="1a76a-108">List of supported data sources</span></span>

<table>
    <tr>
       <td><span data-ttu-id="1a76a-109"><b>Oggetto origine dati</b></span><span class="sxs-lookup"><span data-stu-id="1a76a-109"><b>Data source object</b></span></span></td>
       <td><span data-ttu-id="1a76a-110"><b>API</b></span><span class="sxs-lookup"><span data-stu-id="1a76a-110"><b>API</b></span></span></td>
       <td><span data-ttu-id="1a76a-111"><b>Immissione manuale</b></span><span class="sxs-lookup"><span data-stu-id="1a76a-111"><b>Manual entry</b></span></span></td>
       <td><span data-ttu-id="1a76a-112"><b>Strumento di registrazione</b></span><span class="sxs-lookup"><span data-stu-id="1a76a-112"><b>Registration tool</b></span></span></td>
       <td><span data-ttu-id="1a76a-113"><b>Strumenti di apertura</b></span><span class="sxs-lookup"><span data-stu-id="1a76a-113"><b>Open-in tools</b></span></span></td>
       <td><span data-ttu-id="1a76a-114"><b>Note</b></span><span class="sxs-lookup"><span data-stu-id="1a76a-114"><b>Notes</b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-115">Directory di Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1a76a-115">Azure Data Lake Store directory</span></span></td>
      <td><span data-ttu-id="1a76a-116">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-116">✓</span></span></td>
      <td><span data-ttu-id="1a76a-117">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-117">✓</span></span></td>
      <td><span data-ttu-id="1a76a-118">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-118">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-119">File di Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1a76a-119">Azure Data Lake Store file</span></span></td>
      <td><span data-ttu-id="1a76a-120">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-120">✓</span></span></td>
      <td><span data-ttu-id="1a76a-121">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-121">✓</span></span></td>
      <td><span data-ttu-id="1a76a-122">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-122">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-123">Archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="1a76a-123">Azure Blob storage</span></span></td>
      <td><span data-ttu-id="1a76a-124">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-124">✓</span></span></td>
      <td><span data-ttu-id="1a76a-125">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-125">✓</span></span></td>
      <td><span data-ttu-id="1a76a-126">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-126">✓</span></span></td>
      <td><span data-ttu-id="1a76a-127"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-127"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-128">Directory di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1a76a-128">Azure Storage directory</span></span></td>
      <td><span data-ttu-id="1a76a-129">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-129">✓</span></span></td>
      <td><span data-ttu-id="1a76a-130">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-130">✓</span></span></td>
      <td><span data-ttu-id="1a76a-131">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-131">✓</span></span></td>
      <td><span data-ttu-id="1a76a-132"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-132"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-133">Tabella di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1a76a-133">Azure Storage table</span></span></td>
      <td><span data-ttu-id="1a76a-134">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-134">✓</span></span></td>
      <td><span data-ttu-id="1a76a-135">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-135">✓</span></span></td>
      <td><span data-ttu-id="1a76a-136">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-136">✓</span></span></td>
      <td>
        <font size="2"></font>
      </td>
      <td>
        <font size="2"></font>
      </td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-137">Directory HDFS</span><span class="sxs-lookup"><span data-stu-id="1a76a-137">HDFS directory</span></span></td>
      <td><span data-ttu-id="1a76a-138">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-138">✓</span></span></td>
      <td><span data-ttu-id="1a76a-139">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-139">✓</span></span></td>
      <td><span data-ttu-id="1a76a-140">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-140">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-141">File HDFS</span><span class="sxs-lookup"><span data-stu-id="1a76a-141">HDFS file</span></span></td>
      <td><span data-ttu-id="1a76a-142">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-142">✓</span></span></td>
      <td><span data-ttu-id="1a76a-143">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-143">✓</span></span></td>
      <td><span data-ttu-id="1a76a-144">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-144">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-145">Tabella Hive</span><span class="sxs-lookup"><span data-stu-id="1a76a-145">Hive table</span></span></td>
      <td><span data-ttu-id="1a76a-146">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-146">✓</span></span></td>
      <td><span data-ttu-id="1a76a-147">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-147">✓</span></span></td>
      <td><span data-ttu-id="1a76a-148">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-148">✓</span></span></td>
      <td><span data-ttu-id="1a76a-149"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-149"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-150">Vista di Hive</span><span class="sxs-lookup"><span data-stu-id="1a76a-150">Hive view</span></span></td>
      <td><span data-ttu-id="1a76a-151">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-151">✓</span></span></td>
      <td><span data-ttu-id="1a76a-152">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-152">✓</span></span></td>
      <td><span data-ttu-id="1a76a-153">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-153">✓</span></span></td>
      <td><span data-ttu-id="1a76a-154"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-154"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-155">Tabella MySQL</span><span class="sxs-lookup"><span data-stu-id="1a76a-155">MySQL table</span></span></td>
      <td><span data-ttu-id="1a76a-156">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-156">✓</span></span></td>
      <td><span data-ttu-id="1a76a-157">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-157">✓</span></span></td>
      <td><span data-ttu-id="1a76a-158">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-158">✓</span></span></td>
      <td><span data-ttu-id="1a76a-159"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-159"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-160">Vista MySQL</span><span class="sxs-lookup"><span data-stu-id="1a76a-160">MySQL view</span></span></td>
      <td><span data-ttu-id="1a76a-161">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-161">✓</span></span></td>
      <td><span data-ttu-id="1a76a-162">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-162">✓</span></span></td>
      <td><span data-ttu-id="1a76a-163">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-163">✓</span></span></td>
      <td><span data-ttu-id="1a76a-164"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-164"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-165">Tabella di Database Oracle</span><span class="sxs-lookup"><span data-stu-id="1a76a-165">Oracle Database table</span></span></td>
      <td><span data-ttu-id="1a76a-166">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-166">✓</span></span></td>
      <td><span data-ttu-id="1a76a-167">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-167">✓</span></span></td>
      <td><span data-ttu-id="1a76a-168">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-168">✓</span></span></td>
      <td><span data-ttu-id="1a76a-169"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-169"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-170">Vista di Database Oracle</span><span class="sxs-lookup"><span data-stu-id="1a76a-170">Oracle Database view</span></span></td>
      <td><span data-ttu-id="1a76a-171">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-171">✓</span></span></td>
      <td><span data-ttu-id="1a76a-172">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-172">✓</span></span></td>
      <td><span data-ttu-id="1a76a-173">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-173">✓</span></span></td>
      <td><span data-ttu-id="1a76a-174"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-174"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-175">Altro (asset generico)</span><span class="sxs-lookup"><span data-stu-id="1a76a-175">Other (generic asset)</span></span></td>
      <td><span data-ttu-id="1a76a-176">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-176">✓</span></span></td>
      <td><span data-ttu-id="1a76a-177">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-177">✓</span></span></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-178">Tabella di Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1a76a-178">Azure SQL Data Warehouse table</span></span></td>
      <td><span data-ttu-id="1a76a-179">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-179">✓</span></span></td>
      <td><span data-ttu-id="1a76a-180">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-180">✓</span></span></td>
      <td><span data-ttu-id="1a76a-181">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-181">✓</span></span></td>
      <td><span data-ttu-id="1a76a-182"><font size=2>Excel, PowerBI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-182"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-183">Vista di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1a76a-183">SQL Data Warehouse view</span></span></td>
      <td><span data-ttu-id="1a76a-184">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-184">✓</span></span></td>
      <td><span data-ttu-id="1a76a-185">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-185">✓</span></span></td>
      <td><span data-ttu-id="1a76a-186">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-186">✓</span></span></td>
      <td><span data-ttu-id="1a76a-187"><font size=2>Excel, PowerBI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-187"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-188">Dimensione di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="1a76a-188">SQL Server Analysis Services dimension</span></span></td>
      <td><span data-ttu-id="1a76a-189">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-189">✓</span></span></td>
      <td><span data-ttu-id="1a76a-190">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-190">✓</span></span></td>
      <td><span data-ttu-id="1a76a-191">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-191">✓</span></span></td>
      <td><span data-ttu-id="1a76a-192"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-192"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-193">KPI di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="1a76a-193">SQL Server Analysis Services KPI</span></span></td>
      <td><span data-ttu-id="1a76a-194">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-194">✓</span></span></td>
      <td><span data-ttu-id="1a76a-195">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-195">✓</span></span></td>
      <td><span data-ttu-id="1a76a-196">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-196">✓</span></span></td>
      <td><span data-ttu-id="1a76a-197"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-197"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-198">Misura di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="1a76a-198">SQL Server Analysis Services measure</span></span></td>
      <td><span data-ttu-id="1a76a-199">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-199">✓</span></span></td>
      <td><span data-ttu-id="1a76a-200">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-200">✓</span></span></td>
      <td><span data-ttu-id="1a76a-201">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-201">✓</span></span></td>
      <td><span data-ttu-id="1a76a-202"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-202"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-203">Tabella di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="1a76a-203">SQL Server Analysis Services table</span></span></td>
      <td><span data-ttu-id="1a76a-204">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-204">✓</span></span></td>
      <td><span data-ttu-id="1a76a-205">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-205">✓</span></span></td>
      <td><span data-ttu-id="1a76a-206">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-206">✓</span></span></td>
      <td><span data-ttu-id="1a76a-207"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-207"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-208">Report di SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="1a76a-208">SQL Server Reporting Services report</span></span></td>
      <td><span data-ttu-id="1a76a-209">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-209">✓</span></span></td>
      <td><span data-ttu-id="1a76a-210">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-210">✓</span></span></td>
      <td><span data-ttu-id="1a76a-211">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-211">✓</span></span></td>
      <td><span data-ttu-id="1a76a-212"><font size=2>Browser</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-212"><font size=2>Browser</font></span></span></td>
      <td><span data-ttu-id="1a76a-213"><font size=2>Solo server in modalità nativa. Modalità SharePoint non supportata.</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-213"><font size=2>Native mode servers only. SharePoint mode is not supported.</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-214">Tabella di SQL Server</span><span class="sxs-lookup"><span data-stu-id="1a76a-214">SQL Server table</span></span></td>
      <td><span data-ttu-id="1a76a-215">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-215">✓</span></span></td>
      <td><span data-ttu-id="1a76a-216">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-216">✓</span></span></td>
      <td><span data-ttu-id="1a76a-217">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-217">✓</span></span></td>
      <td><span data-ttu-id="1a76a-218"><font size=2>Excel, PowerBI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-218"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-219">Visualizzazione SQL Server</span><span class="sxs-lookup"><span data-stu-id="1a76a-219">SQL Server view</span></span></td>
      <td><span data-ttu-id="1a76a-220">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-220">✓</span></span></td>
      <td><span data-ttu-id="1a76a-221">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-221">✓</span></span></td>
      <td><span data-ttu-id="1a76a-222">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-222">✓</span></span></td>
      <td><span data-ttu-id="1a76a-223"><font size=2>Excel, PowerBI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-223"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-224">Tabella Teradata</span><span class="sxs-lookup"><span data-stu-id="1a76a-224">Teradata table</span></span></td>
      <td><span data-ttu-id="1a76a-225">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-225">✓</span></span></td>
      <td><span data-ttu-id="1a76a-226">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-226">✓</span></span></td>
      <td><span data-ttu-id="1a76a-227">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-227">✓</span></span></td>
      <td><span data-ttu-id="1a76a-228"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-228"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-229">Visualizzazione Teradata</span><span class="sxs-lookup"><span data-stu-id="1a76a-229">Teradata view</span></span></td>
      <td><span data-ttu-id="1a76a-230">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-230">✓</span></span></td>
      <td><span data-ttu-id="1a76a-231">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-231">✓</span></span></td>
      <td><span data-ttu-id="1a76a-232">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-232">✓</span></span></td>
      <td><span data-ttu-id="1a76a-233"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-233"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-234">Vista di SAP HANA</span><span class="sxs-lookup"><span data-stu-id="1a76a-234">SAP HANA view</span></span></td>
      <td><span data-ttu-id="1a76a-235">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-235">✓</span></span></td>
      <td><span data-ttu-id="1a76a-236">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-236">✓</span></span></td>
      <td><span data-ttu-id="1a76a-237">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-237">✓</span></span></td>
      <td><span data-ttu-id="1a76a-238"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-238"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-239">Tabella di DB2</span><span class="sxs-lookup"><span data-stu-id="1a76a-239">DB2 table</span></span></td>
      <td><span data-ttu-id="1a76a-240">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-240">✓</span></span></td>
      <td><span data-ttu-id="1a76a-241">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-241">✓</span></span></td>
      <td><span data-ttu-id="1a76a-242">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-242">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-243">Vista di DB2</span><span class="sxs-lookup"><span data-stu-id="1a76a-243">DB2 view</span></span></td>
      <td><span data-ttu-id="1a76a-244">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-244">✓</span></span></td>
      <td><span data-ttu-id="1a76a-245">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-245">✓</span></span></td>
      <td><span data-ttu-id="1a76a-246">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-246">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-247">File del file system</span><span class="sxs-lookup"><span data-stu-id="1a76a-247">File system file</span></span></td>
      <td><span data-ttu-id="1a76a-248">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-248">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-249">Directory FTP</span><span class="sxs-lookup"><span data-stu-id="1a76a-249">FTP directory</span></span></td>
      <td><span data-ttu-id="1a76a-250">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-250">✓</span></span></td>
      <td><span data-ttu-id="1a76a-251">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-251">✓</span></span></td>
      <td><span data-ttu-id="1a76a-252">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-252">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-253">File FTP</span><span class="sxs-lookup"><span data-stu-id="1a76a-253">FTP file</span></span></td>
      <td><span data-ttu-id="1a76a-254">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-254">✓</span></span></td>
      <td><span data-ttu-id="1a76a-255">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-255">✓</span></span></td>
      <td><span data-ttu-id="1a76a-256">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-256">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-257">Report HTTP</span><span class="sxs-lookup"><span data-stu-id="1a76a-257">HTTP report</span></span></td>
      <td><span data-ttu-id="1a76a-258">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-258">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-259">Endpoint HTTP</span><span class="sxs-lookup"><span data-stu-id="1a76a-259">HTTP endpoint</span></span></td>
      <td><span data-ttu-id="1a76a-260">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-260">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-261">File HTTP</span><span class="sxs-lookup"><span data-stu-id="1a76a-261">HTTP file</span></span></td>
      <td><span data-ttu-id="1a76a-262">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-262">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-263">Set di entità OData</span><span class="sxs-lookup"><span data-stu-id="1a76a-263">OData entity set</span></span></td>
      <td><span data-ttu-id="1a76a-264">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-264">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-265">Funzione OData</span><span class="sxs-lookup"><span data-stu-id="1a76a-265">OData function</span></span></td>
      <td><span data-ttu-id="1a76a-266">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-266">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-267">Tabella di PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1a76a-267">PostgreSQL table</span></span></td>
      <td><span data-ttu-id="1a76a-268">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-268">✓</span></span></td>
      <td><span data-ttu-id="1a76a-269">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-269">✓</span></span></td>
      <td><span data-ttu-id="1a76a-270">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-270">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-271">Vista di PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1a76a-271">PostgreSQL view</span></span></td>
      <td><span data-ttu-id="1a76a-272">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-272">✓</span></span></td>
      <td><span data-ttu-id="1a76a-273">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-273">✓</span></span></td>
      <td><span data-ttu-id="1a76a-274">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-274">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-275">Vista di SAP HANA</span><span class="sxs-lookup"><span data-stu-id="1a76a-275">SAP HANA view</span></span></td>
      <td><span data-ttu-id="1a76a-276">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-276">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td> <span data-ttu-id="1a76a-277">Oggetto Salesforce</span><span class="sxs-lookup"><span data-stu-id="1a76a-277">Salesforce object</span></span></td>
      <td><span data-ttu-id="1a76a-278">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-278">✓</span></span></td>
      <td><span data-ttu-id="1a76a-279">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-279">✓</span></span></td>
      <td><span data-ttu-id="1a76a-280">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-280">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-281">Elenco SharePoint</span><span class="sxs-lookup"><span data-stu-id="1a76a-281">SharePoint list</span></span> </td>
      <td><span data-ttu-id="1a76a-282">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-282">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-283">Raccolta di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1a76a-283">Azure Cosmos DB collection</span></span></td>
      <td><span data-ttu-id="1a76a-284">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-284">✓</span></span></td>
      <td><span data-ttu-id="1a76a-285">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-285">✓</span></span></td>
      <td><span data-ttu-id="1a76a-286">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-286">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-287">Tabella ODBC generica</span><span class="sxs-lookup"><span data-stu-id="1a76a-287">Generic ODBC table</span></span></td>
      <td><span data-ttu-id="1a76a-288">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-288">✓</span></span></td>
      <td><span data-ttu-id="1a76a-289">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-289">✓</span></span></td>
      <td><span data-ttu-id="1a76a-290">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-290">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-291">Visualizzazione ODBC generica</span><span class="sxs-lookup"><span data-stu-id="1a76a-291">Generic ODBC view</span></span></td>
      <td><span data-ttu-id="1a76a-292">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-292">✓</span></span></td>
      <td><span data-ttu-id="1a76a-293">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-293">✓</span></span></td>
      <td><span data-ttu-id="1a76a-294">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-294">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-295">Tabella Cassandra</span><span class="sxs-lookup"><span data-stu-id="1a76a-295">Cassandra table</span></span></td>
      <td><span data-ttu-id="1a76a-296">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-296">✓</span></span></td>
      <td><span data-ttu-id="1a76a-297">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-297">✓</span></span></td>
      <td><span data-ttu-id="1a76a-298">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-298">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="1a76a-299"><font size=2>Pubblicare come asset ODBC generico</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-299"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-300">Vista Cassandra</span><span class="sxs-lookup"><span data-stu-id="1a76a-300">Cassandra view</span></span></td>
      <td><span data-ttu-id="1a76a-301">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-301">✓</span></span></td>
      <td><span data-ttu-id="1a76a-302">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-302">✓</span></span></td>
      <td><span data-ttu-id="1a76a-303">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-303">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="1a76a-304"><font size=2>Pubblicare come asset ODBC generico</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-304"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-305">Tabella Sybase</span><span class="sxs-lookup"><span data-stu-id="1a76a-305">Sybase table</span></span></td>
      <td><span data-ttu-id="1a76a-306">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-306">✓</span></span></td>
      <td><span data-ttu-id="1a76a-307">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-307">✓</span></span></td>
      <td><span data-ttu-id="1a76a-308">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-308">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-309">Vista Sybase</span><span class="sxs-lookup"><span data-stu-id="1a76a-309">Sybase view</span></span></td>
      <td><span data-ttu-id="1a76a-310">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-310">✓</span></span></td>
      <td><span data-ttu-id="1a76a-311">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-311">✓</span></span></td>
      <td><span data-ttu-id="1a76a-312">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-312">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-313">Tabella MongoDB</span><span class="sxs-lookup"><span data-stu-id="1a76a-313">MongoDB table</span></span></td>
      <td><span data-ttu-id="1a76a-314">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-314">✓</span></span></td>
      <td><span data-ttu-id="1a76a-315">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-315">✓</span></span></td>
      <td><span data-ttu-id="1a76a-316">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-316">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="1a76a-317"><font size=2>Pubblicare come asset ODBC generico</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-317"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-318">Vista MongoDB</span><span class="sxs-lookup"><span data-stu-id="1a76a-318">MongoDB view</span></span></td>
      <td><span data-ttu-id="1a76a-319">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-319">✓</span></span></td>
      <td><span data-ttu-id="1a76a-320">✓ </span><span class="sxs-lookup"><span data-stu-id="1a76a-320">✓</span></span></td>
      <td><span data-ttu-id="1a76a-321">✓</span><span class="sxs-lookup"><span data-stu-id="1a76a-321">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="1a76a-322"><font size=2>Pubblicare come asset ODBC generico</font></span><span class="sxs-lookup"><span data-stu-id="1a76a-322"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
</table>

<span data-ttu-id="1a76a-323">Se è necessario il supporto per le origini aggiuntive, inviare un toohello richiesta funzionalità [forum di Azure Data Catalog](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="1a76a-323">If you need support for additional sources, submit a feature request toohello [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span></span>


## <a name="data-source-reference-specification"></a><span data-ttu-id="1a76a-324">Specifica di riferimento per l'origine dati</span><span class="sxs-lookup"><span data-stu-id="1a76a-324">Data-source reference specification</span></span>
> [!NOTE]
> <span data-ttu-id="1a76a-325">Hello **struttura DSL** colonna hello nella tabella seguente sono elencati solo hello proprietà "address" contenitore delle proprietà di connessione utilizzate da Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="1a76a-325">hello **DSL structure** column in hello following table lists only hello connection properties for "address" property bag that are used by Azure Data Catalog.</span></span> <span data-ttu-id="1a76a-326">Vale a dire, elenco di proprietà "address" può contenere altre proprietà di connessione dell'origine dati hello Azure Data Catalog persiste, ma non utilizza.</span><span class="sxs-lookup"><span data-stu-id="1a76a-326">That is, "address" property bag can contain other connection properties of hello data source which Azure Data Catalog persists, but does not use.</span></span>

<table>
    <tr>
       <td><span data-ttu-id="1a76a-327"><b>Tipo di origine</b></span><span class="sxs-lookup"><span data-stu-id="1a76a-327"><b>Source type</b></span></span></td>
       <td><span data-ttu-id="1a76a-328"><b>Tipo di asset</b></span><span class="sxs-lookup"><span data-stu-id="1a76a-328"><b>Asset type</b></span></span></td>
       <td><span data-ttu-id="1a76a-329"><b>Tipi di oggetti</b></span><span class="sxs-lookup"><span data-stu-id="1a76a-329"><b>Object types</b></span></span></td>
       <td><span data-ttu-id="1a76a-330"><b>Struttura DSL<b></span><span class="sxs-lookup"><span data-stu-id="1a76a-330"><b>DSL structure<b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-331">Archivio Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="1a76a-331">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="1a76a-332">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-332">Container</span></span></td>
      <td><span data-ttu-id="1a76a-333">Data Lake</span><span class="sxs-lookup"><span data-stu-id="1a76a-333">Data Lake</span></span></td>
      <td><span data-ttu-id="1a76a-334">
        <font size=2> Protocollo: webhdfs</span><span class="sxs-lookup"><span data-stu-id="1a76a-334">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="1a76a-335">Autenticazione: {basic, oauth}</span><span class="sxs-lookup"><span data-stu-id="1a76a-335">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="1a76a-336">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-336">Address:</span></span> <br><span data-ttu-id="1a76a-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-338">Archivio Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="1a76a-338">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="1a76a-339">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-339">Table</span></span></td>
      <td><span data-ttu-id="1a76a-340">Directory, file</span><span class="sxs-lookup"><span data-stu-id="1a76a-340">Directory, file</span></span></td>
      <td><span data-ttu-id="1a76a-341">
        <font size=2> Protocollo: webhdfs</span><span class="sxs-lookup"><span data-stu-id="1a76a-341">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="1a76a-342">Autenticazione: {basic, oauth}</span><span class="sxs-lookup"><span data-stu-id="1a76a-342">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="1a76a-343">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-343">Address:</span></span> <br><span data-ttu-id="1a76a-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-345">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1a76a-345">Azure Storage</span></span></td>
      <td><span data-ttu-id="1a76a-346">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-346">Container</span></span></td>
      <td><span data-ttu-id="1a76a-347">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-347">Container</span></span></td>
      <td><span data-ttu-id="1a76a-348">
        <font size=2> Protocollo: azure-blobs</span><span class="sxs-lookup"><span data-stu-id="1a76a-348">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="1a76a-349">Autenticazione: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="1a76a-349">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="1a76a-350">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-350">Address:</span></span> <br><span data-ttu-id="1a76a-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; dominio</span><span class="sxs-lookup"><span data-stu-id="1a76a-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="1a76a-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span><span class="sxs-lookup"><span data-stu-id="1a76a-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="1a76a-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; contenitore </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-354">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1a76a-354">Azure Storage</span></span></td>
      <td><span data-ttu-id="1a76a-355">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-355">Table</span></span></td>
      <td><span data-ttu-id="1a76a-356">BLOB, directory</span><span class="sxs-lookup"><span data-stu-id="1a76a-356">Blob, directory</span></span></td>
      <td><span data-ttu-id="1a76a-357">
        <font size=2> Protocollo: azure-blobs</span><span class="sxs-lookup"><span data-stu-id="1a76a-357">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="1a76a-358">Autenticazione: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="1a76a-358">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="1a76a-359">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-359">Address:</span></span> <br><span data-ttu-id="1a76a-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; dominio</span><span class="sxs-lookup"><span data-stu-id="1a76a-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="1a76a-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span><span class="sxs-lookup"><span data-stu-id="1a76a-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="1a76a-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container</span></span> <br><span data-ttu-id="1a76a-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; nome </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-364">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1a76a-364">Azure Storage</span></span></td>
      <td><span data-ttu-id="1a76a-365">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-365">Container</span></span></td>
      <td><span data-ttu-id="1a76a-366">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-366">Container</span></span></td>
      <td><span data-ttu-id="1a76a-367">
        <font size=2> Protocollo: azure-tables</span><span class="sxs-lookup"><span data-stu-id="1a76a-367">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="1a76a-368">Autenticazione: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="1a76a-368">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="1a76a-369">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-369">Address:</span></span> <br><span data-ttu-id="1a76a-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; dominio</span><span class="sxs-lookup"><span data-stu-id="1a76a-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="1a76a-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-372">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1a76a-372">Azure Storage</span></span></td>
      <td><span data-ttu-id="1a76a-373">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-373">Table</span></span></td>
      <td><span data-ttu-id="1a76a-374">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-374">Table</span></span></td>
      <td><span data-ttu-id="1a76a-375">
        <font size=2> Protocollo: azure-tables</span><span class="sxs-lookup"><span data-stu-id="1a76a-375">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="1a76a-376">Autenticazione: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="1a76a-376">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="1a76a-377">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-377">Address:</span></span> <br><span data-ttu-id="1a76a-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; dominio</span><span class="sxs-lookup"><span data-stu-id="1a76a-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="1a76a-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span><span class="sxs-lookup"><span data-stu-id="1a76a-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="1a76a-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; nome </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-381">Cosmos</span><span class="sxs-lookup"><span data-stu-id="1a76a-381">Cosmos</span></span></td>
      <td><span data-ttu-id="1a76a-382">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-382">Container</span></span></td>
      <td><span data-ttu-id="1a76a-383">Cluster virtuale</span><span class="sxs-lookup"><span data-stu-id="1a76a-383">Virtual cluster</span></span></td>
      <td><span data-ttu-id="1a76a-384">
        <font size=2> Protocollo: cosmos</span><span class="sxs-lookup"><span data-stu-id="1a76a-384">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="1a76a-385">Autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-385">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="1a76a-386">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-386">Address:</span></span> <br><span data-ttu-id="1a76a-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-388">Cosmos</span><span class="sxs-lookup"><span data-stu-id="1a76a-388">Cosmos</span></span></td>
      <td><span data-ttu-id="1a76a-389">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-389">Table</span></span></td>
      <td><span data-ttu-id="1a76a-390">Flusso, set di flussi, vista</span><span class="sxs-lookup"><span data-stu-id="1a76a-390">Stream, stream set, view</span></span></td>
      <td><span data-ttu-id="1a76a-391">
        <font size=2> Protocollo: cosmos</span><span class="sxs-lookup"><span data-stu-id="1a76a-391">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="1a76a-392">Autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-392">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="1a76a-393">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-393">Address:</span></span> <br><span data-ttu-id="1a76a-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-395">Datazen</span><span class="sxs-lookup"><span data-stu-id="1a76a-395">Datazen</span></span></td>
      <td><span data-ttu-id="1a76a-396">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-396">Container</span></span></td>
      <td><span data-ttu-id="1a76a-397">Sito</span><span class="sxs-lookup"><span data-stu-id="1a76a-397">Site</span></span></td>
      <td><span data-ttu-id="1a76a-398">
        <font size=2> Protocollo: http</span><span class="sxs-lookup"><span data-stu-id="1a76a-398">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="1a76a-399">Autenticazione: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="1a76a-399">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="1a76a-400">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-400">Address:</span></span> <br><span data-ttu-id="1a76a-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-402">Datazen</span><span class="sxs-lookup"><span data-stu-id="1a76a-402">Datazen</span></span></td>
      <td><span data-ttu-id="1a76a-403">Report</span><span class="sxs-lookup"><span data-stu-id="1a76a-403">Report</span></span></td>
      <td><span data-ttu-id="1a76a-404">Report, dashboard</span><span class="sxs-lookup"><span data-stu-id="1a76a-404">Report, dashboard</span></span></td>
      <td><span data-ttu-id="1a76a-405">
        <font size=2> Protocollo: http</span><span class="sxs-lookup"><span data-stu-id="1a76a-405">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="1a76a-406">Autenticazione: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="1a76a-406">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="1a76a-407">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-407">Address:</span></span> <br><span data-ttu-id="1a76a-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-409">DB2</span><span class="sxs-lookup"><span data-stu-id="1a76a-409">DB2</span></span></td>
      <td><span data-ttu-id="1a76a-410">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-410">Container</span></span></td>
      <td><span data-ttu-id="1a76a-411">Database</span><span class="sxs-lookup"><span data-stu-id="1a76a-411">Database</span></span></td>
      <td><span data-ttu-id="1a76a-412">
        <font size=2> Protocollo: db2</span><span class="sxs-lookup"><span data-stu-id="1a76a-412">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="1a76a-413">Autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-413">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="1a76a-414">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-414">Address:</span></span> <br><span data-ttu-id="1a76a-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-417">DB2</span><span class="sxs-lookup"><span data-stu-id="1a76a-417">DB2</span></span></td>
      <td><span data-ttu-id="1a76a-418">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-418">Table</span></span></td>
      <td><span data-ttu-id="1a76a-419">Tabella, vista</span><span class="sxs-lookup"><span data-stu-id="1a76a-419">Table, view</span></span></td>
      <td><span data-ttu-id="1a76a-420">
        <font size=2> Protocollo: db2</span><span class="sxs-lookup"><span data-stu-id="1a76a-420">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="1a76a-421">Autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-421">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="1a76a-422">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-422">Address:</span></span> <br><span data-ttu-id="1a76a-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto</span><span class="sxs-lookup"><span data-stu-id="1a76a-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="1a76a-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-427">File system</span><span class="sxs-lookup"><span data-stu-id="1a76a-427">File system</span></span></td>
      <td><span data-ttu-id="1a76a-428">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-428">Table</span></span></td>
      <td><span data-ttu-id="1a76a-429">File</span><span class="sxs-lookup"><span data-stu-id="1a76a-429">File</span></span></td>
      <td><span data-ttu-id="1a76a-430">
        <font size=2> Protocollo: file</span><span class="sxs-lookup"><span data-stu-id="1a76a-430">
        <font size=2> Protocol: file</span></span> <br><span data-ttu-id="1a76a-431">Autenticazione: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-431">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="1a76a-432">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-432">Address:</span></span> <br><span data-ttu-id="1a76a-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; percorso </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-434">FTP</span><span class="sxs-lookup"><span data-stu-id="1a76a-434">FTP</span></span></td>
      <td><span data-ttu-id="1a76a-435">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-435">Table</span></span></td>
      <td><span data-ttu-id="1a76a-436">Directory, file</span><span class="sxs-lookup"><span data-stu-id="1a76a-436">Directory, file</span></span></td>
      <td><span data-ttu-id="1a76a-437">
        <font size=2> Protocollo: ftp</span><span class="sxs-lookup"><span data-stu-id="1a76a-437">
        <font size=2> Protocol: ftp</span></span> <br><span data-ttu-id="1a76a-438">Autenticazione: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-438">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="1a76a-439">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-439">Address:</span></span> <br><span data-ttu-id="1a76a-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-441">Hadoop Distributed File System</span><span class="sxs-lookup"><span data-stu-id="1a76a-441">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="1a76a-442">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-442">Container</span></span></td>
      <td><span data-ttu-id="1a76a-443">HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a76a-443">Cluster</span></span></td>
      <td><span data-ttu-id="1a76a-444">
        <font size=2> Protocollo: webhdfs</span><span class="sxs-lookup"><span data-stu-id="1a76a-444">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="1a76a-445">Autenticazione: {basic, oauth}</span><span class="sxs-lookup"><span data-stu-id="1a76a-445">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="1a76a-446">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-446">Address:</span></span> <br><span data-ttu-id="1a76a-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-448">Hadoop Distributed File System</span><span class="sxs-lookup"><span data-stu-id="1a76a-448">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="1a76a-449">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-449">Table</span></span></td>
      <td><span data-ttu-id="1a76a-450">Directory, file</span><span class="sxs-lookup"><span data-stu-id="1a76a-450">Directory, file</span></span></td>
      <td><span data-ttu-id="1a76a-451">
        <font size=2> Protocollo: webhdfs</span><span class="sxs-lookup"><span data-stu-id="1a76a-451">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="1a76a-452">Autenticazione: {basic, oauth}</span><span class="sxs-lookup"><span data-stu-id="1a76a-452">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="1a76a-453">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-453">Address:</span></span> <br><span data-ttu-id="1a76a-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-455">Hive</span><span class="sxs-lookup"><span data-stu-id="1a76a-455">Hive</span></span></td>
      <td><span data-ttu-id="1a76a-456">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-456">Container</span></span></td>
      <td><span data-ttu-id="1a76a-457">Database</span><span class="sxs-lookup"><span data-stu-id="1a76a-457">Database</span></span></td>
      <td><span data-ttu-id="1a76a-458">
        <font size=2> Protocollo: hive</span><span class="sxs-lookup"><span data-stu-id="1a76a-458">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="1a76a-459">Autenticazione: {HDInsight, basic, username, none}</span><span class="sxs-lookup"><span data-stu-id="1a76a-459">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="1a76a-460">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-460">Address:</span></span> <br><span data-ttu-id="1a76a-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-463">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="1a76a-463">connectionProperties:</span></span> <br><span data-ttu-id="1a76a-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-465">Hive</span><span class="sxs-lookup"><span data-stu-id="1a76a-465">Hive</span></span></td>
      <td><span data-ttu-id="1a76a-466">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-466">Table</span></span></td>
      <td><span data-ttu-id="1a76a-467">Tabella, vista</span><span class="sxs-lookup"><span data-stu-id="1a76a-467">Table, view</span></span></td>
      <td><span data-ttu-id="1a76a-468">
        <font size=2> Protocollo: hive</span><span class="sxs-lookup"><span data-stu-id="1a76a-468">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="1a76a-469">Autenticazione: {HDInsight, basic, username, none}</span><span class="sxs-lookup"><span data-stu-id="1a76a-469">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="1a76a-470">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-470">Address:</span></span> <br><span data-ttu-id="1a76a-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto</span><span class="sxs-lookup"><span data-stu-id="1a76a-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="1a76a-474">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="1a76a-474">connectionProperties:</span></span> <br><span data-ttu-id="1a76a-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-476">http</span><span class="sxs-lookup"><span data-stu-id="1a76a-476">HTTP</span></span></td>
      <td><span data-ttu-id="1a76a-477">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-477">Container</span></span></td>
      <td><span data-ttu-id="1a76a-478">Sito</span><span class="sxs-lookup"><span data-stu-id="1a76a-478">Site</span></span></td>
      <td><span data-ttu-id="1a76a-479">
        <font size=2> Protocollo: http</span><span class="sxs-lookup"><span data-stu-id="1a76a-479">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="1a76a-480">Autenticazione: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="1a76a-480">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="1a76a-481">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-481">Address:</span></span> <br><span data-ttu-id="1a76a-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-483">http</span><span class="sxs-lookup"><span data-stu-id="1a76a-483">HTTP</span></span></td>
      <td><span data-ttu-id="1a76a-484">Report</span><span class="sxs-lookup"><span data-stu-id="1a76a-484">Report</span></span></td>
      <td><span data-ttu-id="1a76a-485">Report, dashboard</span><span class="sxs-lookup"><span data-stu-id="1a76a-485">Report, dashboard</span></span></td>
      <td><span data-ttu-id="1a76a-486">
        <font size=2> Protocollo: http</span><span class="sxs-lookup"><span data-stu-id="1a76a-486">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="1a76a-487">Autenticazione: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="1a76a-487">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="1a76a-488">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-488">Address:</span></span> <br><span data-ttu-id="1a76a-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-490">http</span><span class="sxs-lookup"><span data-stu-id="1a76a-490">HTTP</span></span></td>
      <td><span data-ttu-id="1a76a-491">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-491">Table</span></span></td>
      <td><span data-ttu-id="1a76a-492">Endpoint, file</span><span class="sxs-lookup"><span data-stu-id="1a76a-492">Endpoint, file</span></span></td>
      <td><span data-ttu-id="1a76a-493">
        <font size=2> Protocollo: http</span><span class="sxs-lookup"><span data-stu-id="1a76a-493">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="1a76a-494">Autenticazione: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="1a76a-494">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="1a76a-495">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-495">Address:</span></span> <br><span data-ttu-id="1a76a-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-497">MySQL</span><span class="sxs-lookup"><span data-stu-id="1a76a-497">MySQL</span></span></td>
      <td><span data-ttu-id="1a76a-498">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-498">Container</span></span></td>
      <td><span data-ttu-id="1a76a-499">Database</span><span class="sxs-lookup"><span data-stu-id="1a76a-499">Database</span></span></td>
      <td><span data-ttu-id="1a76a-500">
        <font size=2> Protocollo: mysql</span><span class="sxs-lookup"><span data-stu-id="1a76a-500">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="1a76a-501">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-501">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="1a76a-502">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-502">Address:</span></span> <br><span data-ttu-id="1a76a-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-505">MySQL</span><span class="sxs-lookup"><span data-stu-id="1a76a-505">MySQL</span></span></td>
      <td><span data-ttu-id="1a76a-506">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-506">Table</span></span></td>
      <td><span data-ttu-id="1a76a-507">Tabella, vista</span><span class="sxs-lookup"><span data-stu-id="1a76a-507">Table, view</span></span></td>
      <td><span data-ttu-id="1a76a-508">
        <font size=2> Protocollo: mysql</span><span class="sxs-lookup"><span data-stu-id="1a76a-508">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="1a76a-509">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-509">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="1a76a-510">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-510">Address:</span></span> <br><span data-ttu-id="1a76a-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-514">OData</span><span class="sxs-lookup"><span data-stu-id="1a76a-514">OData</span></span></td>
      <td><span data-ttu-id="1a76a-515">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-515">Container</span></span></td>
      <td><span data-ttu-id="1a76a-516">Contenitore di entità</span><span class="sxs-lookup"><span data-stu-id="1a76a-516">Entity container</span></span></td>
      <td><span data-ttu-id="1a76a-517">
        <font size=2> Protocollo: odata</span><span class="sxs-lookup"><span data-stu-id="1a76a-517">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="1a76a-518">Autenticazione: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-518">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="1a76a-519">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-519">Address:</span></span> <br><span data-ttu-id="1a76a-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-521">OData</span><span class="sxs-lookup"><span data-stu-id="1a76a-521">OData</span></span></td>
      <td><span data-ttu-id="1a76a-522">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-522">Table</span></span></td>
      <td><span data-ttu-id="1a76a-523">Set di entità, funzione</span><span class="sxs-lookup"><span data-stu-id="1a76a-523">Entity set, function</span></span></td>
      <td><span data-ttu-id="1a76a-524">
        <font size=2> Protocollo: odata</span><span class="sxs-lookup"><span data-stu-id="1a76a-524">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="1a76a-525">Autenticazione: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-525">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="1a76a-526">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-526">Address:</span></span> <br><span data-ttu-id="1a76a-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="1a76a-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="1a76a-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; risorsa </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-529">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="1a76a-529">Oracle Database</span></span></td>
      <td><span data-ttu-id="1a76a-530">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-530">Container</span></span></td>
      <td><span data-ttu-id="1a76a-531">Database</span><span class="sxs-lookup"><span data-stu-id="1a76a-531">Database</span></span></td>
      <td><span data-ttu-id="1a76a-532">
        <font size=2> Protocollo: oracle</span><span class="sxs-lookup"><span data-stu-id="1a76a-532">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="1a76a-533">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-533">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="1a76a-534">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-534">Address:</span></span> <br><span data-ttu-id="1a76a-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-537">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="1a76a-537">Oracle Database</span></span></td>
      <td><span data-ttu-id="1a76a-538">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-538">Table</span></span></td>
      <td><span data-ttu-id="1a76a-539">Tabella, vista</span><span class="sxs-lookup"><span data-stu-id="1a76a-539">Table, view</span></span></td>
      <td><span data-ttu-id="1a76a-540">
        <font size=2> Protocollo: oracle</span><span class="sxs-lookup"><span data-stu-id="1a76a-540">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="1a76a-541">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-541">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="1a76a-542">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-542">Address:</span></span> <br><span data-ttu-id="1a76a-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="1a76a-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="1a76a-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-547">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1a76a-547">PostgreSQL</span></span></td>
      <td><span data-ttu-id="1a76a-548">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-548">Container</span></span></td>
      <td><span data-ttu-id="1a76a-549">Database</span><span class="sxs-lookup"><span data-stu-id="1a76a-549">Database</span></span></td>
      <td><span data-ttu-id="1a76a-550">
        <font size=2> Protocollo: postgresql</span><span class="sxs-lookup"><span data-stu-id="1a76a-550">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="1a76a-551">Autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-551">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="1a76a-552">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-552">Address:</span></span> <br><span data-ttu-id="1a76a-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-555">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="1a76a-555">PostgreSQL</span></span></td>
      <td><span data-ttu-id="1a76a-556">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-556">Table</span></span></td>
      <td><span data-ttu-id="1a76a-557">Tabella, vista</span><span class="sxs-lookup"><span data-stu-id="1a76a-557">Table, view</span></span></td>
      <td><span data-ttu-id="1a76a-558">
        <font size=2> Protocollo: postgresql</span><span class="sxs-lookup"><span data-stu-id="1a76a-558">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="1a76a-559">Autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-559">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="1a76a-560">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-560">Address:</span></span> <br><span data-ttu-id="1a76a-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="1a76a-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="1a76a-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-565">Power BI</span><span class="sxs-lookup"><span data-stu-id="1a76a-565">Power BI</span></span></td>
      <td><span data-ttu-id="1a76a-566">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-566">Container</span></span></td>
      <td><span data-ttu-id="1a76a-567">Sito</span><span class="sxs-lookup"><span data-stu-id="1a76a-567">Site</span></span></td>
      <td><span data-ttu-id="1a76a-568">
        <font size=2> Protocollo: http</span><span class="sxs-lookup"><span data-stu-id="1a76a-568">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="1a76a-569">Autenticazione: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="1a76a-569">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="1a76a-570">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-570">Address:</span></span> <br><span data-ttu-id="1a76a-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-572">Power BI</span><span class="sxs-lookup"><span data-stu-id="1a76a-572">Power BI</span></span></td>
      <td><span data-ttu-id="1a76a-573">Report</span><span class="sxs-lookup"><span data-stu-id="1a76a-573">Report</span></span></td>
      <td><span data-ttu-id="1a76a-574">Report, dashboard</span><span class="sxs-lookup"><span data-stu-id="1a76a-574">Report, dashboard</span></span></td>
      <td><span data-ttu-id="1a76a-575">
        <font size=2> Protocollo: http</span><span class="sxs-lookup"><span data-stu-id="1a76a-575">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="1a76a-576">Autenticazione: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="1a76a-576">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="1a76a-577">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-577">Address:</span></span> <br><span data-ttu-id="1a76a-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-579">Power Query</span><span class="sxs-lookup"><span data-stu-id="1a76a-579">Power Query</span></span></td>
      <td><span data-ttu-id="1a76a-580">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-580">Table</span></span></td>
      <td><span data-ttu-id="1a76a-581">Mashup di dati</span><span class="sxs-lookup"><span data-stu-id="1a76a-581">Data mashup</span></span></td>
      <td><span data-ttu-id="1a76a-582">
        <font size=2> Protocollo: power-query</span><span class="sxs-lookup"><span data-stu-id="1a76a-582">
        <font size=2> Protocol: power-query</span></span> <br><span data-ttu-id="1a76a-583">Autenticazione: {oauth}</span><span class="sxs-lookup"><span data-stu-id="1a76a-583">Authentication: {oauth}</span></span> <br><span data-ttu-id="1a76a-584">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-584">Address:</span></span> <br><span data-ttu-id="1a76a-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-586">Salesforce</span><span class="sxs-lookup"><span data-stu-id="1a76a-586">Salesforce</span></span></td>
      <td><span data-ttu-id="1a76a-587">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-587">Table</span></span></td>
      <td><span data-ttu-id="1a76a-588">Oggetto</span><span class="sxs-lookup"><span data-stu-id="1a76a-588">Object</span></span></td>
      <td><span data-ttu-id="1a76a-589">
        <font size=2> Protocollo: salesforce-com</span><span class="sxs-lookup"><span data-stu-id="1a76a-589">
        <font size=2> Protocol: salesforce-com</span></span> <br><span data-ttu-id="1a76a-590">Autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-590">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="1a76a-591">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-591">Address:</span></span> <br><span data-ttu-id="1a76a-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span><span class="sxs-lookup"><span data-stu-id="1a76a-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span></span> <br><span data-ttu-id="1a76a-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; classe</span><span class="sxs-lookup"><span data-stu-id="1a76a-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span></span> <br><span data-ttu-id="1a76a-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-595">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="1a76a-595">SAP HANA</span></span></td>
      <td><span data-ttu-id="1a76a-596">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-596">Container</span></span></td>
      <td><span data-ttu-id="1a76a-597">Server</span><span class="sxs-lookup"><span data-stu-id="1a76a-597">Server</span></span></td>
      <td><span data-ttu-id="1a76a-598">
        <font size=2> Protocollo: sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="1a76a-598">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="1a76a-599">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-599">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="1a76a-600">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-600">Address:</span></span> <br><span data-ttu-id="1a76a-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-602">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="1a76a-602">SAP HANA</span></span></td>
      <td><span data-ttu-id="1a76a-603">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-603">Table</span></span></td>
      <td><span data-ttu-id="1a76a-604">Visualizza</span><span class="sxs-lookup"><span data-stu-id="1a76a-604">View</span></span></td>
      <td><span data-ttu-id="1a76a-605">
        <font size=2> Protocollo: sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="1a76a-605">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="1a76a-606">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-606">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="1a76a-607">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-607">Address:</span></span> <br><span data-ttu-id="1a76a-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="1a76a-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="1a76a-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-611">SharePoint</span><span class="sxs-lookup"><span data-stu-id="1a76a-611">SharePoint</span></span></td>
      <td><span data-ttu-id="1a76a-612">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-612">Table</span></span></td>
      <td><span data-ttu-id="1a76a-613">Elenco</span><span class="sxs-lookup"><span data-stu-id="1a76a-613">List</span></span></td>
      <td><span data-ttu-id="1a76a-614">
        <font size=2> Protocollo: sharepoint-list</span><span class="sxs-lookup"><span data-stu-id="1a76a-614">
        <font size=2> Protocol: sharepoint-list</span></span> <br><span data-ttu-id="1a76a-615">Autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-615">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="1a76a-616">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-616">Address:</span></span> <br><span data-ttu-id="1a76a-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-618">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1a76a-618">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="1a76a-619">Comando</span><span class="sxs-lookup"><span data-stu-id="1a76a-619">Command</span></span></td>
      <td><span data-ttu-id="1a76a-620">Stored procedure</span><span class="sxs-lookup"><span data-stu-id="1a76a-620">Stored procedure</span></span></td>
      <td><span data-ttu-id="1a76a-621">
        <font size=2> Protocollo: tds</span><span class="sxs-lookup"><span data-stu-id="1a76a-621">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="1a76a-622">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-622">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="1a76a-623">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-623">Address:</span></span> <br><span data-ttu-id="1a76a-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="1a76a-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="1a76a-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-628">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1a76a-628">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="1a76a-629">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="1a76a-629">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="1a76a-630">Funzione con valori di tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-630">Table-valued function</span></span></td>
      <td><span data-ttu-id="1a76a-631">
        <font size=2> Protocollo: tds</span><span class="sxs-lookup"><span data-stu-id="1a76a-631">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="1a76a-632">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-632">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="1a76a-633">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-633">Address:</span></span> <br><span data-ttu-id="1a76a-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="1a76a-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="1a76a-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-638">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1a76a-638">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="1a76a-639">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-639">Container</span></span></td>
      <td><span data-ttu-id="1a76a-640">Database</span><span class="sxs-lookup"><span data-stu-id="1a76a-640">Database</span></span></td>
      <td><span data-ttu-id="1a76a-641">
        <font size=2> Protocollo: tds</span><span class="sxs-lookup"><span data-stu-id="1a76a-641">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="1a76a-642">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-642">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="1a76a-643">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-643">Address:</span></span> <br><span data-ttu-id="1a76a-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-646">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1a76a-646">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="1a76a-647">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-647">Table</span></span></td>
      <td><span data-ttu-id="1a76a-648">Tabella, vista</span><span class="sxs-lookup"><span data-stu-id="1a76a-648">Table, view</span></span></td>
      <td><span data-ttu-id="1a76a-649">
        <font size=2> Protocollo: tds</span><span class="sxs-lookup"><span data-stu-id="1a76a-649">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="1a76a-650">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-650">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="1a76a-651">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-651">Address:</span></span> <br><span data-ttu-id="1a76a-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="1a76a-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="1a76a-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-656">SQL Server</span><span class="sxs-lookup"><span data-stu-id="1a76a-656">SQL Server</span></span></td>
      <td><span data-ttu-id="1a76a-657">Comando</span><span class="sxs-lookup"><span data-stu-id="1a76a-657">Command</span></span></td>
      <td><span data-ttu-id="1a76a-658">Stored procedure</span><span class="sxs-lookup"><span data-stu-id="1a76a-658">Stored procedure</span></span></td>
      <td><span data-ttu-id="1a76a-659">
        <font size=2> Protocollo: tds</span><span class="sxs-lookup"><span data-stu-id="1a76a-659">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="1a76a-660">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-660">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="1a76a-661">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-661">Address:</span></span> <br><span data-ttu-id="1a76a-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="1a76a-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="1a76a-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-666">SQL Server</span><span class="sxs-lookup"><span data-stu-id="1a76a-666">SQL Server</span></span></td>
      <td><span data-ttu-id="1a76a-667">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="1a76a-667">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="1a76a-668">Funzione con valori di tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-668">Table-valued function</span></span></td>
      <td><span data-ttu-id="1a76a-669">
        <font size=2> Protocollo: tds</span><span class="sxs-lookup"><span data-stu-id="1a76a-669">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="1a76a-670">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-670">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="1a76a-671">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-671">Address:</span></span> <br><span data-ttu-id="1a76a-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="1a76a-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="1a76a-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-676">SQL Server</span><span class="sxs-lookup"><span data-stu-id="1a76a-676">SQL Server</span></span></td>
      <td><span data-ttu-id="1a76a-677">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-677">Container</span></span></td>
      <td><span data-ttu-id="1a76a-678">Database</span><span class="sxs-lookup"><span data-stu-id="1a76a-678">Database</span></span></td>
      <td><span data-ttu-id="1a76a-679">
        <font size=2> Protocollo: tds</span><span class="sxs-lookup"><span data-stu-id="1a76a-679">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="1a76a-680">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-680">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="1a76a-681">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-681">Address:</span></span> <br><span data-ttu-id="1a76a-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-684">SQL Server</span><span class="sxs-lookup"><span data-stu-id="1a76a-684">SQL Server</span></span></td>
      <td><span data-ttu-id="1a76a-685">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-685">Table</span></span></td>
      <td><span data-ttu-id="1a76a-686">Tabella, vista</span><span class="sxs-lookup"><span data-stu-id="1a76a-686">Table, view</span></span></td>
      <td><span data-ttu-id="1a76a-687">
        <font size=2> Protocollo: tds</span><span class="sxs-lookup"><span data-stu-id="1a76a-687">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="1a76a-688">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-688">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="1a76a-689">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-689">Address:</span></span> <br><span data-ttu-id="1a76a-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="1a76a-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="1a76a-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-694">Modelli multidimensionali di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="1a76a-694">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="1a76a-695">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-695">Container</span></span></td>
      <td><span data-ttu-id="1a76a-696">Modello</span><span class="sxs-lookup"><span data-stu-id="1a76a-696">Model</span></span></td>
      <td><span data-ttu-id="1a76a-697">
        <font size=2> Protocollo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="1a76a-697">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="1a76a-698">Autenticazione: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="1a76a-698">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="1a76a-699">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-699">Address:</span></span> <br><span data-ttu-id="1a76a-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modello </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-703">Modelli multidimensionali di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="1a76a-703">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="1a76a-704">KPI</span><span class="sxs-lookup"><span data-stu-id="1a76a-704">KPI</span></span></td>
      <td><span data-ttu-id="1a76a-705">KPI</span><span class="sxs-lookup"><span data-stu-id="1a76a-705">KPI</span></span></td>
      <td><span data-ttu-id="1a76a-706">
        <font size=2> Protocollo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="1a76a-706">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="1a76a-707">Autenticazione: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="1a76a-707">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="1a76a-708">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-708">Address:</span></span> <br><span data-ttu-id="1a76a-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modello</span><span class="sxs-lookup"><span data-stu-id="1a76a-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="1a76a-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto</span><span class="sxs-lookup"><span data-stu-id="1a76a-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="1a76a-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-714">Modelli multidimensionali di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="1a76a-714">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="1a76a-715">Measure</span><span class="sxs-lookup"><span data-stu-id="1a76a-715">Measure</span></span></td>
      <td><span data-ttu-id="1a76a-716">Measure</span><span class="sxs-lookup"><span data-stu-id="1a76a-716">Measure</span></span></td>
      <td><span data-ttu-id="1a76a-717">
        <font size=2> Protocollo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="1a76a-717">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="1a76a-718">Autenticazione: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="1a76a-718">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="1a76a-719">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-719">Address:</span></span> <br><span data-ttu-id="1a76a-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modello</span><span class="sxs-lookup"><span data-stu-id="1a76a-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="1a76a-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto</span><span class="sxs-lookup"><span data-stu-id="1a76a-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="1a76a-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-725">Modelli multidimensionali di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="1a76a-725">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="1a76a-726">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-726">Table</span></span></td>
      <td><span data-ttu-id="1a76a-727">Dimensione</span><span class="sxs-lookup"><span data-stu-id="1a76a-727">Dimension</span></span></td>
      <td><span data-ttu-id="1a76a-728">
        <font size=2> Protocollo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="1a76a-728">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="1a76a-729">Autenticazione: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="1a76a-729">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="1a76a-730">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-730">Address:</span></span> <br><span data-ttu-id="1a76a-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modello</span><span class="sxs-lookup"><span data-stu-id="1a76a-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="1a76a-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto</span><span class="sxs-lookup"><span data-stu-id="1a76a-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="1a76a-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-736">Tabulare di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="1a76a-736">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="1a76a-737">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-737">Container</span></span></td>
      <td><span data-ttu-id="1a76a-738">Modello</span><span class="sxs-lookup"><span data-stu-id="1a76a-738">Model</span></span></td>
      <td><span data-ttu-id="1a76a-739">
        <font size=2> Protocollo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="1a76a-739">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="1a76a-740">Autenticazione: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="1a76a-740">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="1a76a-741">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-741">Address:</span></span> <br><span data-ttu-id="1a76a-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modello </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-745">Tabulare di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="1a76a-745">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="1a76a-746">KPI</span><span class="sxs-lookup"><span data-stu-id="1a76a-746">KPI</span></span></td>
      <td><span data-ttu-id="1a76a-747">KPI</span><span class="sxs-lookup"><span data-stu-id="1a76a-747">KPI</span></span></td>
      <td><span data-ttu-id="1a76a-748">
        <font size=2> Protocollo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="1a76a-748">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="1a76a-749">Autenticazione: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="1a76a-749">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="1a76a-750">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-750">Address:</span></span> <br><span data-ttu-id="1a76a-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modello</span><span class="sxs-lookup"><span data-stu-id="1a76a-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="1a76a-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto</span><span class="sxs-lookup"><span data-stu-id="1a76a-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="1a76a-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-756">Tabulare di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="1a76a-756">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="1a76a-757">Measure</span><span class="sxs-lookup"><span data-stu-id="1a76a-757">Measure</span></span></td>
      <td><span data-ttu-id="1a76a-758">Measure</span><span class="sxs-lookup"><span data-stu-id="1a76a-758">Measure</span></span></td>
      <td><span data-ttu-id="1a76a-759">
        <font size=2> Protocollo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="1a76a-759">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="1a76a-760">Autenticazione: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="1a76a-760">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="1a76a-761">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-761">Address:</span></span> <br><span data-ttu-id="1a76a-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modello</span><span class="sxs-lookup"><span data-stu-id="1a76a-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="1a76a-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto</span><span class="sxs-lookup"><span data-stu-id="1a76a-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="1a76a-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-767">Tabulare di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="1a76a-767">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="1a76a-768">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-768">Table</span></span></td>
      <td><span data-ttu-id="1a76a-769">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-769">Table</span></span></td>
      <td><span data-ttu-id="1a76a-770">
        <font size=2> Protocollo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="1a76a-770">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="1a76a-771">Autenticazione: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="1a76a-771">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="1a76a-772">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-772">Address:</span></span> <br><span data-ttu-id="1a76a-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modello</span><span class="sxs-lookup"><span data-stu-id="1a76a-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="1a76a-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto</span><span class="sxs-lookup"><span data-stu-id="1a76a-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="1a76a-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-778">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="1a76a-778">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="1a76a-779">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-779">Container</span></span></td>
      <td><span data-ttu-id="1a76a-780">Server</span><span class="sxs-lookup"><span data-stu-id="1a76a-780">Server</span></span></td>
      <td><span data-ttu-id="1a76a-781">
        <font size=2> Protocollo: reporting-services</span><span class="sxs-lookup"><span data-stu-id="1a76a-781">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="1a76a-782">Autenticazione: {windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-782">Authentication: {windows}</span></span> <br><span data-ttu-id="1a76a-783">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-783">Address:</span></span> <br><span data-ttu-id="1a76a-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; versione: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-786">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="1a76a-786">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="1a76a-787">Report</span><span class="sxs-lookup"><span data-stu-id="1a76a-787">Report</span></span></td>
      <td><span data-ttu-id="1a76a-788">Report</span><span class="sxs-lookup"><span data-stu-id="1a76a-788">Report</span></span></td>
      <td><span data-ttu-id="1a76a-789">
        <font size=2> Protocollo: reporting-services</span><span class="sxs-lookup"><span data-stu-id="1a76a-789">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="1a76a-790">Autenticazione: {windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-790">Authentication: {windows}</span></span> <br><span data-ttu-id="1a76a-791">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-791">Address:</span></span> <br><span data-ttu-id="1a76a-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; percorso</span><span class="sxs-lookup"><span data-stu-id="1a76a-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span></span> <br><span data-ttu-id="1a76a-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; versione: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-795">Teradata</span><span class="sxs-lookup"><span data-stu-id="1a76a-795">Teradata</span></span></td>
      <td><span data-ttu-id="1a76a-796">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-796">Container</span></span></td>
      <td><span data-ttu-id="1a76a-797">Database</span><span class="sxs-lookup"><span data-stu-id="1a76a-797">Database</span></span></td>
      <td><span data-ttu-id="1a76a-798">
        <font size=2> Protocollo: teradata</span><span class="sxs-lookup"><span data-stu-id="1a76a-798">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="1a76a-799">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-799">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="1a76a-800">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-800">Address:</span></span> <br><span data-ttu-id="1a76a-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-803">Teradata</span><span class="sxs-lookup"><span data-stu-id="1a76a-803">Teradata</span></span></td>
      <td><span data-ttu-id="1a76a-804">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-804">Table</span></span></td>
      <td><span data-ttu-id="1a76a-805">Tabella, vista</span><span class="sxs-lookup"><span data-stu-id="1a76a-805">Table, view</span></span></td>
      <td><span data-ttu-id="1a76a-806">
        <font size=2> Protocollo: teradata</span><span class="sxs-lookup"><span data-stu-id="1a76a-806">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="1a76a-807">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-807">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="1a76a-808">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-808">Address:</span></span> <br><span data-ttu-id="1a76a-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-812">Master Data Services di SQL Server</span><span class="sxs-lookup"><span data-stu-id="1a76a-812">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="1a76a-813">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-813">Container</span></span></td>
      <td><span data-ttu-id="1a76a-814">Modello</span><span class="sxs-lookup"><span data-stu-id="1a76a-814">Model</span></span></td>
      <td><span data-ttu-id="1a76a-815">
        <font size="2"> Protocollo: mssql mds</span><span class="sxs-lookup"><span data-stu-id="1a76a-815">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="1a76a-816">Autenticazione: {windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-816">Authentication: {windows}</span></span> <br><span data-ttu-id="1a76a-817">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-817">Address:</span></span> <br><span data-ttu-id="1a76a-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="1a76a-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="1a76a-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modello</span><span class="sxs-lookup"><span data-stu-id="1a76a-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="1a76a-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; versione </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-821">Master Data Services di SQL Server</span><span class="sxs-lookup"><span data-stu-id="1a76a-821">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="1a76a-822">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-822">Table</span></span></td>
      <td><span data-ttu-id="1a76a-823">Entità</span><span class="sxs-lookup"><span data-stu-id="1a76a-823">Entity</span></span></td>
      <td><span data-ttu-id="1a76a-824">
        <font size="2"> Protocollo: mssql mds</span><span class="sxs-lookup"><span data-stu-id="1a76a-824">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="1a76a-825">Autenticazione: {windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-825">Authentication: {windows}</span></span> <br><span data-ttu-id="1a76a-826">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-826">Address:</span></span> <br><span data-ttu-id="1a76a-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="1a76a-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="1a76a-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modello</span><span class="sxs-lookup"><span data-stu-id="1a76a-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="1a76a-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; versione</span><span class="sxs-lookup"><span data-stu-id="1a76a-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span></span> <br><span data-ttu-id="1a76a-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entità </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-831">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1a76a-831">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="1a76a-832">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-832">Container</span></span></td>
      <td><span data-ttu-id="1a76a-833">Database</span><span class="sxs-lookup"><span data-stu-id="1a76a-833">Database</span></span></td>
      <td><span data-ttu-id="1a76a-834">
        <font size=2> Protocollo: document-db</span><span class="sxs-lookup"><span data-stu-id="1a76a-834">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="1a76a-835">Autenticazione: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="1a76a-835">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="1a76a-836">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-836">Address:</span></span> <br><span data-ttu-id="1a76a-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="1a76a-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="1a76a-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-839">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1a76a-839">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="1a76a-840">Raccolta</span><span class="sxs-lookup"><span data-stu-id="1a76a-840">Collection</span></span></td>
      <td><span data-ttu-id="1a76a-841">Raccolta</span><span class="sxs-lookup"><span data-stu-id="1a76a-841">Collection</span></span></td>
      <td><span data-ttu-id="1a76a-842">
        <font size=2> Protocollo: document-db</span><span class="sxs-lookup"><span data-stu-id="1a76a-842">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="1a76a-843">Autenticazione: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="1a76a-843">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="1a76a-844">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-844">Address:</span></span> <br><span data-ttu-id="1a76a-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="1a76a-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="1a76a-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; raccolta </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; collection </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-848">ODBC generico</span><span class="sxs-lookup"><span data-stu-id="1a76a-848">Generic ODBC</span></span></td>
      <td><span data-ttu-id="1a76a-849">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-849">Container</span></span></td>
      <td><span data-ttu-id="1a76a-850">Database</span><span class="sxs-lookup"><span data-stu-id="1a76a-850">Database</span></span></td>
      <td><span data-ttu-id="1a76a-851">
        <font size=2> Protocollo: odbc</span><span class="sxs-lookup"><span data-stu-id="1a76a-851">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="1a76a-852">Autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-852">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="1a76a-853">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-853">Address:</span></span> <br><span data-ttu-id="1a76a-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; opzioni</span><span class="sxs-lookup"><span data-stu-id="1a76a-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="1a76a-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-856">ODBC generico</span><span class="sxs-lookup"><span data-stu-id="1a76a-856">Generic ODBC</span></span></td>
      <td><span data-ttu-id="1a76a-857">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-857">Table</span></span></td>
      <td><span data-ttu-id="1a76a-858">Tabella, vista</span><span class="sxs-lookup"><span data-stu-id="1a76a-858">Table, View</span></span></td>
      <td><span data-ttu-id="1a76a-859">
        <font size=2> Protocollo: odbc</span><span class="sxs-lookup"><span data-stu-id="1a76a-859">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="1a76a-860">Autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-860">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="1a76a-861">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-861">Address:</span></span> <br><span data-ttu-id="1a76a-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; opzioni</span><span class="sxs-lookup"><span data-stu-id="1a76a-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="1a76a-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto</span><span class="sxs-lookup"><span data-stu-id="1a76a-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="1a76a-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-866">Sybase</span><span class="sxs-lookup"><span data-stu-id="1a76a-866">Sybase</span></span></td>
      <td><span data-ttu-id="1a76a-867">Contenitore</span><span class="sxs-lookup"><span data-stu-id="1a76a-867">Container</span></span></td>
      <td><span data-ttu-id="1a76a-868">Database</span><span class="sxs-lookup"><span data-stu-id="1a76a-868">Database</span></span></td>
      <td><span data-ttu-id="1a76a-869">
        <font size=2>protocollo: sybase</span><span class="sxs-lookup"><span data-stu-id="1a76a-869">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="1a76a-870">autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-870">authentication: {basic, windows}</span></span> <br><span data-ttu-id="1a76a-871">indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-871">address:</span></span> <br><span data-ttu-id="1a76a-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-874">Sybase</span><span class="sxs-lookup"><span data-stu-id="1a76a-874">Sybase</span></span></td>
      <td><span data-ttu-id="1a76a-875">Tabella</span><span class="sxs-lookup"><span data-stu-id="1a76a-875">Table</span></span></td>
      <td><span data-ttu-id="1a76a-876">Tabella, vista</span><span class="sxs-lookup"><span data-stu-id="1a76a-876">Table, View</span></span></td>
      <td><span data-ttu-id="1a76a-877">
        <font size=2>protocollo: sybase</span><span class="sxs-lookup"><span data-stu-id="1a76a-877">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="1a76a-878">autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="1a76a-878">authentication: {basic, windows}</span></span> <br><span data-ttu-id="1a76a-879">indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-879">address:</span></span> <br><span data-ttu-id="1a76a-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="1a76a-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="1a76a-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="1a76a-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="1a76a-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="1a76a-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="1a76a-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="1a76a-884">Altro (nessuno di hello precedente)</span><span class="sxs-lookup"><span data-stu-id="1a76a-884">Other (none of hello above)</span></span></td>
      <td>\*</td>
      <td>\*</td>
      <td><span data-ttu-id="1a76a-885">
        <font size=2> Protocollo: generic-asset</span><span class="sxs-lookup"><span data-stu-id="1a76a-885">
        <font size=2> Protocol: generic-asset</span></span> <br><span data-ttu-id="1a76a-886">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="1a76a-886">Address:</span></span> <br><span data-ttu-id="1a76a-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span><span class="sxs-lookup"><span data-stu-id="1a76a-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span></span></td>
    </tr>
</table>
