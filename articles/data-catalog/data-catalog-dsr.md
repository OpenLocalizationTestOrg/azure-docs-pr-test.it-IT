---
title: Origini dati supportate in Azure Data Catalog | Microsoft Docs
description: Questo articolo elenca le specifiche delle origini dati attualmente supportate.
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
ms.openlocfilehash: d6867c73bc6ea3c238cceef8a68466d451f3365c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="supported-data-sources-in-azure-data-catalog"></a><span data-ttu-id="b42e7-103">Origini dati supportate in Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="b42e7-103">Supported data sources in Azure Data Catalog</span></span>

<span data-ttu-id="b42e7-104">È possibile pubblicare metadati usando un'API pubblica o uno strumento di registrazione di tipo ClickOnce oppure immettendo manualmente le informazioni direttamente nel portale Web di Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="b42e7-104">You can publish metadata by using a public API or a click-once registration tool, or by manually entering information directly to the Azure Data Catalog web portal.</span></span> <span data-ttu-id="b42e7-105">La tabella seguente fornisce un riepilogo di tutte le origini dati supportate attualmente dal catalogo e delle relative funzionalità di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="b42e7-105">The following table summarizes all data sources that are supported by the catalog today, and the publishing capabilities for each.</span></span> <span data-ttu-id="b42e7-106">Sono anche elencati gli strumenti dati esterni che ogni origine dati può avviare dal portale.</span><span class="sxs-lookup"><span data-stu-id="b42e7-106">Also listed are the external data tools that each data source can launch from our portal "open-in" experience.</span></span> <span data-ttu-id="b42e7-107">La seconda tabella contiene una specifica più tecnica della proprietà di connessione delle singole origini dati.</span><span class="sxs-lookup"><span data-stu-id="b42e7-107">The second table contains a more technical specification of each data-source connection property.</span></span>


## <a name="list-of-supported-data-sources"></a><span data-ttu-id="b42e7-108">Elenco di origini dati supportate</span><span class="sxs-lookup"><span data-stu-id="b42e7-108">List of supported data sources</span></span>

<table>
    <tr>
       <td><span data-ttu-id="b42e7-109"><b>Oggetto origine dati</b></span><span class="sxs-lookup"><span data-stu-id="b42e7-109"><b>Data source object</b></span></span></td>
       <td><span data-ttu-id="b42e7-110"><b>API</b></span><span class="sxs-lookup"><span data-stu-id="b42e7-110"><b>API</b></span></span></td>
       <td><span data-ttu-id="b42e7-111"><b>Immissione manuale</b></span><span class="sxs-lookup"><span data-stu-id="b42e7-111"><b>Manual entry</b></span></span></td>
       <td><span data-ttu-id="b42e7-112"><b>Strumento di registrazione</b></span><span class="sxs-lookup"><span data-stu-id="b42e7-112"><b>Registration tool</b></span></span></td>
       <td><span data-ttu-id="b42e7-113"><b>Strumenti di apertura</b></span><span class="sxs-lookup"><span data-stu-id="b42e7-113"><b>Open-in tools</b></span></span></td>
       <td><span data-ttu-id="b42e7-114"><b>Note</b></span><span class="sxs-lookup"><span data-stu-id="b42e7-114"><b>Notes</b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-115">Directory di Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b42e7-115">Azure Data Lake Store directory</span></span></td>
      <td><span data-ttu-id="b42e7-116">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-116">✓</span></span></td>
      <td><span data-ttu-id="b42e7-117">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-117">✓</span></span></td>
      <td><span data-ttu-id="b42e7-118">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-118">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-119">File di Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b42e7-119">Azure Data Lake Store file</span></span></td>
      <td><span data-ttu-id="b42e7-120">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-120">✓</span></span></td>
      <td><span data-ttu-id="b42e7-121">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-121">✓</span></span></td>
      <td><span data-ttu-id="b42e7-122">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-122">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-123">Archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="b42e7-123">Azure Blob storage</span></span></td>
      <td><span data-ttu-id="b42e7-124">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-124">✓</span></span></td>
      <td><span data-ttu-id="b42e7-125">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-125">✓</span></span></td>
      <td><span data-ttu-id="b42e7-126">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-126">✓</span></span></td>
      <td><span data-ttu-id="b42e7-127"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-127"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-128">Directory di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b42e7-128">Azure Storage directory</span></span></td>
      <td><span data-ttu-id="b42e7-129">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-129">✓</span></span></td>
      <td><span data-ttu-id="b42e7-130">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-130">✓</span></span></td>
      <td><span data-ttu-id="b42e7-131">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-131">✓</span></span></td>
      <td><span data-ttu-id="b42e7-132"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-132"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-133">Tabella di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b42e7-133">Azure Storage table</span></span></td>
      <td><span data-ttu-id="b42e7-134">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-134">✓</span></span></td>
      <td><span data-ttu-id="b42e7-135">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-135">✓</span></span></td>
      <td><span data-ttu-id="b42e7-136">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-136">✓</span></span></td>
      <td>
        <font size="2"></font>
      </td>
      <td>
        <font size="2"></font>
      </td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-137">Directory HDFS</span><span class="sxs-lookup"><span data-stu-id="b42e7-137">HDFS directory</span></span></td>
      <td><span data-ttu-id="b42e7-138">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-138">✓</span></span></td>
      <td><span data-ttu-id="b42e7-139">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-139">✓</span></span></td>
      <td><span data-ttu-id="b42e7-140">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-140">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-141">File HDFS</span><span class="sxs-lookup"><span data-stu-id="b42e7-141">HDFS file</span></span></td>
      <td><span data-ttu-id="b42e7-142">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-142">✓</span></span></td>
      <td><span data-ttu-id="b42e7-143">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-143">✓</span></span></td>
      <td><span data-ttu-id="b42e7-144">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-144">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-145">Tabella Hive</span><span class="sxs-lookup"><span data-stu-id="b42e7-145">Hive table</span></span></td>
      <td><span data-ttu-id="b42e7-146">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-146">✓</span></span></td>
      <td><span data-ttu-id="b42e7-147">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-147">✓</span></span></td>
      <td><span data-ttu-id="b42e7-148">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-148">✓</span></span></td>
      <td><span data-ttu-id="b42e7-149"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-149"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-150">Vista di Hive</span><span class="sxs-lookup"><span data-stu-id="b42e7-150">Hive view</span></span></td>
      <td><span data-ttu-id="b42e7-151">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-151">✓</span></span></td>
      <td><span data-ttu-id="b42e7-152">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-152">✓</span></span></td>
      <td><span data-ttu-id="b42e7-153">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-153">✓</span></span></td>
      <td><span data-ttu-id="b42e7-154"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-154"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-155">Tabella MySQL</span><span class="sxs-lookup"><span data-stu-id="b42e7-155">MySQL table</span></span></td>
      <td><span data-ttu-id="b42e7-156">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-156">✓</span></span></td>
      <td><span data-ttu-id="b42e7-157">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-157">✓</span></span></td>
      <td><span data-ttu-id="b42e7-158">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-158">✓</span></span></td>
      <td><span data-ttu-id="b42e7-159"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-159"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-160">Vista MySQL</span><span class="sxs-lookup"><span data-stu-id="b42e7-160">MySQL view</span></span></td>
      <td><span data-ttu-id="b42e7-161">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-161">✓</span></span></td>
      <td><span data-ttu-id="b42e7-162">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-162">✓</span></span></td>
      <td><span data-ttu-id="b42e7-163">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-163">✓</span></span></td>
      <td><span data-ttu-id="b42e7-164"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-164"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-165">Tabella di Database Oracle</span><span class="sxs-lookup"><span data-stu-id="b42e7-165">Oracle Database table</span></span></td>
      <td><span data-ttu-id="b42e7-166">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-166">✓</span></span></td>
      <td><span data-ttu-id="b42e7-167">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-167">✓</span></span></td>
      <td><span data-ttu-id="b42e7-168">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-168">✓</span></span></td>
      <td><span data-ttu-id="b42e7-169"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-169"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-170">Vista di Database Oracle</span><span class="sxs-lookup"><span data-stu-id="b42e7-170">Oracle Database view</span></span></td>
      <td><span data-ttu-id="b42e7-171">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-171">✓</span></span></td>
      <td><span data-ttu-id="b42e7-172">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-172">✓</span></span></td>
      <td><span data-ttu-id="b42e7-173">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-173">✓</span></span></td>
      <td><span data-ttu-id="b42e7-174"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-174"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-175">Altro (asset generico)</span><span class="sxs-lookup"><span data-stu-id="b42e7-175">Other (generic asset)</span></span></td>
      <td><span data-ttu-id="b42e7-176">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-176">✓</span></span></td>
      <td><span data-ttu-id="b42e7-177">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-177">✓</span></span></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-178">Tabella di Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b42e7-178">Azure SQL Data Warehouse table</span></span></td>
      <td><span data-ttu-id="b42e7-179">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-179">✓</span></span></td>
      <td><span data-ttu-id="b42e7-180">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-180">✓</span></span></td>
      <td><span data-ttu-id="b42e7-181">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-181">✓</span></span></td>
      <td><span data-ttu-id="b42e7-182"><font size=2>Excel, PowerBI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-182"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-183">Vista di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b42e7-183">SQL Data Warehouse view</span></span></td>
      <td><span data-ttu-id="b42e7-184">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-184">✓</span></span></td>
      <td><span data-ttu-id="b42e7-185">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-185">✓</span></span></td>
      <td><span data-ttu-id="b42e7-186">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-186">✓</span></span></td>
      <td><span data-ttu-id="b42e7-187"><font size=2>Excel, PowerBI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-187"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-188">Dimensione di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="b42e7-188">SQL Server Analysis Services dimension</span></span></td>
      <td><span data-ttu-id="b42e7-189">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-189">✓</span></span></td>
      <td><span data-ttu-id="b42e7-190">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-190">✓</span></span></td>
      <td><span data-ttu-id="b42e7-191">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-191">✓</span></span></td>
      <td><span data-ttu-id="b42e7-192"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-192"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-193">KPI di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="b42e7-193">SQL Server Analysis Services KPI</span></span></td>
      <td><span data-ttu-id="b42e7-194">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-194">✓</span></span></td>
      <td><span data-ttu-id="b42e7-195">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-195">✓</span></span></td>
      <td><span data-ttu-id="b42e7-196">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-196">✓</span></span></td>
      <td><span data-ttu-id="b42e7-197"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-197"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-198">Misura di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="b42e7-198">SQL Server Analysis Services measure</span></span></td>
      <td><span data-ttu-id="b42e7-199">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-199">✓</span></span></td>
      <td><span data-ttu-id="b42e7-200">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-200">✓</span></span></td>
      <td><span data-ttu-id="b42e7-201">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-201">✓</span></span></td>
      <td><span data-ttu-id="b42e7-202"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-202"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-203">Tabella di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="b42e7-203">SQL Server Analysis Services table</span></span></td>
      <td><span data-ttu-id="b42e7-204">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-204">✓</span></span></td>
      <td><span data-ttu-id="b42e7-205">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-205">✓</span></span></td>
      <td><span data-ttu-id="b42e7-206">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-206">✓</span></span></td>
      <td><span data-ttu-id="b42e7-207"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-207"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-208">Report di SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="b42e7-208">SQL Server Reporting Services report</span></span></td>
      <td><span data-ttu-id="b42e7-209">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-209">✓</span></span></td>
      <td><span data-ttu-id="b42e7-210">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-210">✓</span></span></td>
      <td><span data-ttu-id="b42e7-211">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-211">✓</span></span></td>
      <td><span data-ttu-id="b42e7-212"><font size=2>Browser</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-212"><font size=2>Browser</font></span></span></td>
      <td><span data-ttu-id="b42e7-213"><font size=2>Solo server in modalità nativa. Modalità SharePoint non supportata.</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-213"><font size=2>Native mode servers only. SharePoint mode is not supported.</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-214">Tabella di SQL Server</span><span class="sxs-lookup"><span data-stu-id="b42e7-214">SQL Server table</span></span></td>
      <td><span data-ttu-id="b42e7-215">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-215">✓</span></span></td>
      <td><span data-ttu-id="b42e7-216">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-216">✓</span></span></td>
      <td><span data-ttu-id="b42e7-217">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-217">✓</span></span></td>
      <td><span data-ttu-id="b42e7-218"><font size=2>Excel, PowerBI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-218"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-219">Visualizzazione SQL Server</span><span class="sxs-lookup"><span data-stu-id="b42e7-219">SQL Server view</span></span></td>
      <td><span data-ttu-id="b42e7-220">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-220">✓</span></span></td>
      <td><span data-ttu-id="b42e7-221">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-221">✓</span></span></td>
      <td><span data-ttu-id="b42e7-222">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-222">✓</span></span></td>
      <td><span data-ttu-id="b42e7-223"><font size=2>Excel, PowerBI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-223"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-224">Tabella Teradata</span><span class="sxs-lookup"><span data-stu-id="b42e7-224">Teradata table</span></span></td>
      <td><span data-ttu-id="b42e7-225">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-225">✓</span></span></td>
      <td><span data-ttu-id="b42e7-226">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-226">✓</span></span></td>
      <td><span data-ttu-id="b42e7-227">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-227">✓</span></span></td>
      <td><span data-ttu-id="b42e7-228"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-228"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-229">Visualizzazione Teradata</span><span class="sxs-lookup"><span data-stu-id="b42e7-229">Teradata view</span></span></td>
      <td><span data-ttu-id="b42e7-230">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-230">✓</span></span></td>
      <td><span data-ttu-id="b42e7-231">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-231">✓</span></span></td>
      <td><span data-ttu-id="b42e7-232">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-232">✓</span></span></td>
      <td><span data-ttu-id="b42e7-233"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-233"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-234">Vista di SAP HANA</span><span class="sxs-lookup"><span data-stu-id="b42e7-234">SAP HANA view</span></span></td>
      <td><span data-ttu-id="b42e7-235">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-235">✓</span></span></td>
      <td><span data-ttu-id="b42e7-236">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-236">✓</span></span></td>
      <td><span data-ttu-id="b42e7-237">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-237">✓</span></span></td>
      <td><span data-ttu-id="b42e7-238"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-238"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-239">Tabella di DB2</span><span class="sxs-lookup"><span data-stu-id="b42e7-239">DB2 table</span></span></td>
      <td><span data-ttu-id="b42e7-240">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-240">✓</span></span></td>
      <td><span data-ttu-id="b42e7-241">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-241">✓</span></span></td>
      <td><span data-ttu-id="b42e7-242">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-242">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-243">Vista di DB2</span><span class="sxs-lookup"><span data-stu-id="b42e7-243">DB2 view</span></span></td>
      <td><span data-ttu-id="b42e7-244">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-244">✓</span></span></td>
      <td><span data-ttu-id="b42e7-245">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-245">✓</span></span></td>
      <td><span data-ttu-id="b42e7-246">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-246">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-247">File del file system</span><span class="sxs-lookup"><span data-stu-id="b42e7-247">File system file</span></span></td>
      <td><span data-ttu-id="b42e7-248">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-248">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-249">Directory FTP</span><span class="sxs-lookup"><span data-stu-id="b42e7-249">FTP directory</span></span></td>
      <td><span data-ttu-id="b42e7-250">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-250">✓</span></span></td>
      <td><span data-ttu-id="b42e7-251">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-251">✓</span></span></td>
      <td><span data-ttu-id="b42e7-252">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-252">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-253">File FTP</span><span class="sxs-lookup"><span data-stu-id="b42e7-253">FTP file</span></span></td>
      <td><span data-ttu-id="b42e7-254">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-254">✓</span></span></td>
      <td><span data-ttu-id="b42e7-255">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-255">✓</span></span></td>
      <td><span data-ttu-id="b42e7-256">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-256">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-257">Report HTTP</span><span class="sxs-lookup"><span data-stu-id="b42e7-257">HTTP report</span></span></td>
      <td><span data-ttu-id="b42e7-258">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-258">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-259">Endpoint HTTP</span><span class="sxs-lookup"><span data-stu-id="b42e7-259">HTTP endpoint</span></span></td>
      <td><span data-ttu-id="b42e7-260">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-260">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-261">File HTTP</span><span class="sxs-lookup"><span data-stu-id="b42e7-261">HTTP file</span></span></td>
      <td><span data-ttu-id="b42e7-262">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-262">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-263">Set di entità OData</span><span class="sxs-lookup"><span data-stu-id="b42e7-263">OData entity set</span></span></td>
      <td><span data-ttu-id="b42e7-264">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-264">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-265">Funzione OData</span><span class="sxs-lookup"><span data-stu-id="b42e7-265">OData function</span></span></td>
      <td><span data-ttu-id="b42e7-266">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-266">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-267">Tabella di PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="b42e7-267">PostgreSQL table</span></span></td>
      <td><span data-ttu-id="b42e7-268">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-268">✓</span></span></td>
      <td><span data-ttu-id="b42e7-269">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-269">✓</span></span></td>
      <td><span data-ttu-id="b42e7-270">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-270">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-271">Vista di PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="b42e7-271">PostgreSQL view</span></span></td>
      <td><span data-ttu-id="b42e7-272">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-272">✓</span></span></td>
      <td><span data-ttu-id="b42e7-273">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-273">✓</span></span></td>
      <td><span data-ttu-id="b42e7-274">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-274">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-275">Vista di SAP HANA</span><span class="sxs-lookup"><span data-stu-id="b42e7-275">SAP HANA view</span></span></td>
      <td><span data-ttu-id="b42e7-276">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-276">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td> <span data-ttu-id="b42e7-277">Oggetto Salesforce</span><span class="sxs-lookup"><span data-stu-id="b42e7-277">Salesforce object</span></span></td>
      <td><span data-ttu-id="b42e7-278">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-278">✓</span></span></td>
      <td><span data-ttu-id="b42e7-279">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-279">✓</span></span></td>
      <td><span data-ttu-id="b42e7-280">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-280">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-281">Elenco SharePoint</span><span class="sxs-lookup"><span data-stu-id="b42e7-281">SharePoint list</span></span> </td>
      <td><span data-ttu-id="b42e7-282">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-282">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-283">Raccolta di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b42e7-283">Azure Cosmos DB collection</span></span></td>
      <td><span data-ttu-id="b42e7-284">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-284">✓</span></span></td>
      <td><span data-ttu-id="b42e7-285">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-285">✓</span></span></td>
      <td><span data-ttu-id="b42e7-286">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-286">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-287">Tabella ODBC generica</span><span class="sxs-lookup"><span data-stu-id="b42e7-287">Generic ODBC table</span></span></td>
      <td><span data-ttu-id="b42e7-288">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-288">✓</span></span></td>
      <td><span data-ttu-id="b42e7-289">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-289">✓</span></span></td>
      <td><span data-ttu-id="b42e7-290">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-290">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-291">Visualizzazione ODBC generica</span><span class="sxs-lookup"><span data-stu-id="b42e7-291">Generic ODBC view</span></span></td>
      <td><span data-ttu-id="b42e7-292">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-292">✓</span></span></td>
      <td><span data-ttu-id="b42e7-293">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-293">✓</span></span></td>
      <td><span data-ttu-id="b42e7-294">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-294">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-295">Tabella Cassandra</span><span class="sxs-lookup"><span data-stu-id="b42e7-295">Cassandra table</span></span></td>
      <td><span data-ttu-id="b42e7-296">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-296">✓</span></span></td>
      <td><span data-ttu-id="b42e7-297">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-297">✓</span></span></td>
      <td><span data-ttu-id="b42e7-298">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-298">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="b42e7-299"><font size=2>Pubblicare come asset ODBC generico</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-299"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-300">Vista Cassandra</span><span class="sxs-lookup"><span data-stu-id="b42e7-300">Cassandra view</span></span></td>
      <td><span data-ttu-id="b42e7-301">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-301">✓</span></span></td>
      <td><span data-ttu-id="b42e7-302">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-302">✓</span></span></td>
      <td><span data-ttu-id="b42e7-303">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-303">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="b42e7-304"><font size=2>Pubblicare come asset ODBC generico</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-304"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-305">Tabella Sybase</span><span class="sxs-lookup"><span data-stu-id="b42e7-305">Sybase table</span></span></td>
      <td><span data-ttu-id="b42e7-306">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-306">✓</span></span></td>
      <td><span data-ttu-id="b42e7-307">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-307">✓</span></span></td>
      <td><span data-ttu-id="b42e7-308">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-308">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-309">Vista Sybase</span><span class="sxs-lookup"><span data-stu-id="b42e7-309">Sybase view</span></span></td>
      <td><span data-ttu-id="b42e7-310">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-310">✓</span></span></td>
      <td><span data-ttu-id="b42e7-311">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-311">✓</span></span></td>
      <td><span data-ttu-id="b42e7-312">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-312">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-313">Tabella MongoDB</span><span class="sxs-lookup"><span data-stu-id="b42e7-313">MongoDB table</span></span></td>
      <td><span data-ttu-id="b42e7-314">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-314">✓</span></span></td>
      <td><span data-ttu-id="b42e7-315">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-315">✓</span></span></td>
      <td><span data-ttu-id="b42e7-316">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-316">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="b42e7-317"><font size=2>Pubblicare come asset ODBC generico</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-317"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-318">Vista MongoDB</span><span class="sxs-lookup"><span data-stu-id="b42e7-318">MongoDB view</span></span></td>
      <td><span data-ttu-id="b42e7-319">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-319">✓</span></span></td>
      <td><span data-ttu-id="b42e7-320">✓ </span><span class="sxs-lookup"><span data-stu-id="b42e7-320">✓</span></span></td>
      <td><span data-ttu-id="b42e7-321">✓</span><span class="sxs-lookup"><span data-stu-id="b42e7-321">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="b42e7-322"><font size=2>Pubblicare come asset ODBC generico</font></span><span class="sxs-lookup"><span data-stu-id="b42e7-322"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
</table>

<span data-ttu-id="b42e7-323">Per il supporto di altre origini, inviare una richiesta di funzionalità al [forum di Azure Data Catalog](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="b42e7-323">If you need support for additional sources, submit a feature request to the [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span></span>


## <a name="data-source-reference-specification"></a><span data-ttu-id="b42e7-324">Specifica di riferimento per l'origine dati</span><span class="sxs-lookup"><span data-stu-id="b42e7-324">Data-source reference specification</span></span>
> [!NOTE]
> <span data-ttu-id="b42e7-325">La colonna **Struttura DSL** nella tabella seguente elenca solo le proprietà di connessione per il contenitore di proprietà "indirizzo" usate da Azure Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="b42e7-325">The **DSL structure** column in the following table lists only the connection properties for "address" property bag that are used by Azure Data Catalog.</span></span> <span data-ttu-id="b42e7-326">Ovvero, l'elenco di proprietà "indirizzo" può contenere altre proprietà di connessione dell'origine dati che Azure Data Catalog mantiene ma non usa.</span><span class="sxs-lookup"><span data-stu-id="b42e7-326">That is, "address" property bag can contain other connection properties of the data source which Azure Data Catalog persists, but does not use.</span></span>

<table>
    <tr>
       <td><span data-ttu-id="b42e7-327"><b>Tipo di origine</b></span><span class="sxs-lookup"><span data-stu-id="b42e7-327"><b>Source type</b></span></span></td>
       <td><span data-ttu-id="b42e7-328"><b>Tipo di asset</b></span><span class="sxs-lookup"><span data-stu-id="b42e7-328"><b>Asset type</b></span></span></td>
       <td><span data-ttu-id="b42e7-329"><b>Tipi di oggetti</b></span><span class="sxs-lookup"><span data-stu-id="b42e7-329"><b>Object types</b></span></span></td>
       <td><span data-ttu-id="b42e7-330"><b>Struttura DSL<b></span><span class="sxs-lookup"><span data-stu-id="b42e7-330"><b>DSL structure<b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-331">Archivio Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="b42e7-331">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="b42e7-332">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-332">Container</span></span></td>
      <td><span data-ttu-id="b42e7-333">Data Lake</span><span class="sxs-lookup"><span data-stu-id="b42e7-333">Data Lake</span></span></td>
      <td><span data-ttu-id="b42e7-334">
        <font size=2> Protocollo: webhdfs</span><span class="sxs-lookup"><span data-stu-id="b42e7-334">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="b42e7-335">Autenticazione: {basic, oauth}</span><span class="sxs-lookup"><span data-stu-id="b42e7-335">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="b42e7-336">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-336">Address:</span></span> <br><span data-ttu-id="b42e7-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-338">Archivio Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="b42e7-338">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="b42e7-339">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-339">Table</span></span></td>
      <td><span data-ttu-id="b42e7-340">Directory, file</span><span class="sxs-lookup"><span data-stu-id="b42e7-340">Directory, file</span></span></td>
      <td><span data-ttu-id="b42e7-341">
        <font size=2> Protocollo: webhdfs</span><span class="sxs-lookup"><span data-stu-id="b42e7-341">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="b42e7-342">Autenticazione: {basic, oauth}</span><span class="sxs-lookup"><span data-stu-id="b42e7-342">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="b42e7-343">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-343">Address:</span></span> <br><span data-ttu-id="b42e7-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-345">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b42e7-345">Azure Storage</span></span></td>
      <td><span data-ttu-id="b42e7-346">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-346">Container</span></span></td>
      <td><span data-ttu-id="b42e7-347">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-347">Container</span></span></td>
      <td><span data-ttu-id="b42e7-348">
        <font size=2> Protocollo: azure-blobs</span><span class="sxs-lookup"><span data-stu-id="b42e7-348">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="b42e7-349">Autenticazione: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="b42e7-349">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="b42e7-350">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-350">Address:</span></span> <br><span data-ttu-id="b42e7-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; dominio</span><span class="sxs-lookup"><span data-stu-id="b42e7-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="b42e7-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span><span class="sxs-lookup"><span data-stu-id="b42e7-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="b42e7-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; contenitore </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-354">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b42e7-354">Azure Storage</span></span></td>
      <td><span data-ttu-id="b42e7-355">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-355">Table</span></span></td>
      <td><span data-ttu-id="b42e7-356">BLOB, directory</span><span class="sxs-lookup"><span data-stu-id="b42e7-356">Blob, directory</span></span></td>
      <td><span data-ttu-id="b42e7-357">
        <font size=2> Protocollo: azure-blobs</span><span class="sxs-lookup"><span data-stu-id="b42e7-357">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="b42e7-358">Autenticazione: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="b42e7-358">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="b42e7-359">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-359">Address:</span></span> <br><span data-ttu-id="b42e7-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; dominio</span><span class="sxs-lookup"><span data-stu-id="b42e7-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="b42e7-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span><span class="sxs-lookup"><span data-stu-id="b42e7-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="b42e7-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container</span></span> <br><span data-ttu-id="b42e7-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; nome </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-364">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b42e7-364">Azure Storage</span></span></td>
      <td><span data-ttu-id="b42e7-365">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-365">Container</span></span></td>
      <td><span data-ttu-id="b42e7-366">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-366">Container</span></span></td>
      <td><span data-ttu-id="b42e7-367">
        <font size=2> Protocollo: azure-tables</span><span class="sxs-lookup"><span data-stu-id="b42e7-367">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="b42e7-368">Autenticazione: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="b42e7-368">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="b42e7-369">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-369">Address:</span></span> <br><span data-ttu-id="b42e7-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; dominio</span><span class="sxs-lookup"><span data-stu-id="b42e7-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="b42e7-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-372">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b42e7-372">Azure Storage</span></span></td>
      <td><span data-ttu-id="b42e7-373">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-373">Table</span></span></td>
      <td><span data-ttu-id="b42e7-374">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-374">Table</span></span></td>
      <td><span data-ttu-id="b42e7-375">
        <font size=2> Protocollo: azure-tables</span><span class="sxs-lookup"><span data-stu-id="b42e7-375">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="b42e7-376">Autenticazione: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="b42e7-376">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="b42e7-377">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-377">Address:</span></span> <br><span data-ttu-id="b42e7-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; dominio</span><span class="sxs-lookup"><span data-stu-id="b42e7-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="b42e7-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span><span class="sxs-lookup"><span data-stu-id="b42e7-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="b42e7-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; nome </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-381">Cosmos</span><span class="sxs-lookup"><span data-stu-id="b42e7-381">Cosmos</span></span></td>
      <td><span data-ttu-id="b42e7-382">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-382">Container</span></span></td>
      <td><span data-ttu-id="b42e7-383">Cluster virtuale</span><span class="sxs-lookup"><span data-stu-id="b42e7-383">Virtual cluster</span></span></td>
      <td><span data-ttu-id="b42e7-384">
        <font size=2> Protocollo: cosmos</span><span class="sxs-lookup"><span data-stu-id="b42e7-384">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="b42e7-385">Autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-385">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="b42e7-386">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-386">Address:</span></span> <br><span data-ttu-id="b42e7-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-388">Cosmos</span><span class="sxs-lookup"><span data-stu-id="b42e7-388">Cosmos</span></span></td>
      <td><span data-ttu-id="b42e7-389">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-389">Table</span></span></td>
      <td><span data-ttu-id="b42e7-390">Flusso, set di flussi, vista</span><span class="sxs-lookup"><span data-stu-id="b42e7-390">Stream, stream set, view</span></span></td>
      <td><span data-ttu-id="b42e7-391">
        <font size=2> Protocollo: cosmos</span><span class="sxs-lookup"><span data-stu-id="b42e7-391">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="b42e7-392">Autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-392">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="b42e7-393">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-393">Address:</span></span> <br><span data-ttu-id="b42e7-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-395">Datazen</span><span class="sxs-lookup"><span data-stu-id="b42e7-395">Datazen</span></span></td>
      <td><span data-ttu-id="b42e7-396">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-396">Container</span></span></td>
      <td><span data-ttu-id="b42e7-397">Sito</span><span class="sxs-lookup"><span data-stu-id="b42e7-397">Site</span></span></td>
      <td><span data-ttu-id="b42e7-398">
        <font size=2> Protocollo: http</span><span class="sxs-lookup"><span data-stu-id="b42e7-398">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="b42e7-399">Autenticazione: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="b42e7-399">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="b42e7-400">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-400">Address:</span></span> <br><span data-ttu-id="b42e7-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-402">Datazen</span><span class="sxs-lookup"><span data-stu-id="b42e7-402">Datazen</span></span></td>
      <td><span data-ttu-id="b42e7-403">Report</span><span class="sxs-lookup"><span data-stu-id="b42e7-403">Report</span></span></td>
      <td><span data-ttu-id="b42e7-404">Report, dashboard</span><span class="sxs-lookup"><span data-stu-id="b42e7-404">Report, dashboard</span></span></td>
      <td><span data-ttu-id="b42e7-405">
        <font size=2> Protocollo: http</span><span class="sxs-lookup"><span data-stu-id="b42e7-405">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="b42e7-406">Autenticazione: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="b42e7-406">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="b42e7-407">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-407">Address:</span></span> <br><span data-ttu-id="b42e7-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-409">DB2</span><span class="sxs-lookup"><span data-stu-id="b42e7-409">DB2</span></span></td>
      <td><span data-ttu-id="b42e7-410">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-410">Container</span></span></td>
      <td><span data-ttu-id="b42e7-411">Database</span><span class="sxs-lookup"><span data-stu-id="b42e7-411">Database</span></span></td>
      <td><span data-ttu-id="b42e7-412">
        <font size=2> Protocollo: db2</span><span class="sxs-lookup"><span data-stu-id="b42e7-412">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="b42e7-413">Autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-413">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="b42e7-414">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-414">Address:</span></span> <br><span data-ttu-id="b42e7-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-417">DB2</span><span class="sxs-lookup"><span data-stu-id="b42e7-417">DB2</span></span></td>
      <td><span data-ttu-id="b42e7-418">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-418">Table</span></span></td>
      <td><span data-ttu-id="b42e7-419">Tabella, vista</span><span class="sxs-lookup"><span data-stu-id="b42e7-419">Table, view</span></span></td>
      <td><span data-ttu-id="b42e7-420">
        <font size=2> Protocollo: db2</span><span class="sxs-lookup"><span data-stu-id="b42e7-420">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="b42e7-421">Autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-421">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="b42e7-422">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-422">Address:</span></span> <br><span data-ttu-id="b42e7-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto</span><span class="sxs-lookup"><span data-stu-id="b42e7-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="b42e7-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-427">File system</span><span class="sxs-lookup"><span data-stu-id="b42e7-427">File system</span></span></td>
      <td><span data-ttu-id="b42e7-428">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-428">Table</span></span></td>
      <td><span data-ttu-id="b42e7-429">File</span><span class="sxs-lookup"><span data-stu-id="b42e7-429">File</span></span></td>
      <td><span data-ttu-id="b42e7-430">
        <font size=2> Protocollo: file</span><span class="sxs-lookup"><span data-stu-id="b42e7-430">
        <font size=2> Protocol: file</span></span> <br><span data-ttu-id="b42e7-431">Autenticazione: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-431">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="b42e7-432">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-432">Address:</span></span> <br><span data-ttu-id="b42e7-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; percorso </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-434">FTP</span><span class="sxs-lookup"><span data-stu-id="b42e7-434">FTP</span></span></td>
      <td><span data-ttu-id="b42e7-435">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-435">Table</span></span></td>
      <td><span data-ttu-id="b42e7-436">Directory, file</span><span class="sxs-lookup"><span data-stu-id="b42e7-436">Directory, file</span></span></td>
      <td><span data-ttu-id="b42e7-437">
        <font size=2> Protocollo: ftp</span><span class="sxs-lookup"><span data-stu-id="b42e7-437">
        <font size=2> Protocol: ftp</span></span> <br><span data-ttu-id="b42e7-438">Autenticazione: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-438">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="b42e7-439">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-439">Address:</span></span> <br><span data-ttu-id="b42e7-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-441">Hadoop Distributed File System</span><span class="sxs-lookup"><span data-stu-id="b42e7-441">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="b42e7-442">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-442">Container</span></span></td>
      <td><span data-ttu-id="b42e7-443">HDInsight</span><span class="sxs-lookup"><span data-stu-id="b42e7-443">Cluster</span></span></td>
      <td><span data-ttu-id="b42e7-444">
        <font size=2> Protocollo: webhdfs</span><span class="sxs-lookup"><span data-stu-id="b42e7-444">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="b42e7-445">Autenticazione: {basic, oauth}</span><span class="sxs-lookup"><span data-stu-id="b42e7-445">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="b42e7-446">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-446">Address:</span></span> <br><span data-ttu-id="b42e7-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-448">Hadoop Distributed File System</span><span class="sxs-lookup"><span data-stu-id="b42e7-448">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="b42e7-449">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-449">Table</span></span></td>
      <td><span data-ttu-id="b42e7-450">Directory, file</span><span class="sxs-lookup"><span data-stu-id="b42e7-450">Directory, file</span></span></td>
      <td><span data-ttu-id="b42e7-451">
        <font size=2> Protocollo: webhdfs</span><span class="sxs-lookup"><span data-stu-id="b42e7-451">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="b42e7-452">Autenticazione: {basic, oauth}</span><span class="sxs-lookup"><span data-stu-id="b42e7-452">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="b42e7-453">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-453">Address:</span></span> <br><span data-ttu-id="b42e7-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-455">Hive</span><span class="sxs-lookup"><span data-stu-id="b42e7-455">Hive</span></span></td>
      <td><span data-ttu-id="b42e7-456">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-456">Container</span></span></td>
      <td><span data-ttu-id="b42e7-457">Database</span><span class="sxs-lookup"><span data-stu-id="b42e7-457">Database</span></span></td>
      <td><span data-ttu-id="b42e7-458">
        <font size=2> Protocollo: hive</span><span class="sxs-lookup"><span data-stu-id="b42e7-458">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="b42e7-459">Autenticazione: {HDInsight, basic, username, none}</span><span class="sxs-lookup"><span data-stu-id="b42e7-459">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="b42e7-460">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-460">Address:</span></span> <br><span data-ttu-id="b42e7-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-463">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="b42e7-463">connectionProperties:</span></span> <br><span data-ttu-id="b42e7-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-465">Hive</span><span class="sxs-lookup"><span data-stu-id="b42e7-465">Hive</span></span></td>
      <td><span data-ttu-id="b42e7-466">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-466">Table</span></span></td>
      <td><span data-ttu-id="b42e7-467">Tabella, vista</span><span class="sxs-lookup"><span data-stu-id="b42e7-467">Table, view</span></span></td>
      <td><span data-ttu-id="b42e7-468">
        <font size=2> Protocollo: hive</span><span class="sxs-lookup"><span data-stu-id="b42e7-468">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="b42e7-469">Autenticazione: {HDInsight, basic, username, none}</span><span class="sxs-lookup"><span data-stu-id="b42e7-469">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="b42e7-470">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-470">Address:</span></span> <br><span data-ttu-id="b42e7-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto</span><span class="sxs-lookup"><span data-stu-id="b42e7-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="b42e7-474">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="b42e7-474">connectionProperties:</span></span> <br><span data-ttu-id="b42e7-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-476">http</span><span class="sxs-lookup"><span data-stu-id="b42e7-476">HTTP</span></span></td>
      <td><span data-ttu-id="b42e7-477">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-477">Container</span></span></td>
      <td><span data-ttu-id="b42e7-478">Sito</span><span class="sxs-lookup"><span data-stu-id="b42e7-478">Site</span></span></td>
      <td><span data-ttu-id="b42e7-479">
        <font size=2> Protocollo: http</span><span class="sxs-lookup"><span data-stu-id="b42e7-479">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="b42e7-480">Autenticazione: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="b42e7-480">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="b42e7-481">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-481">Address:</span></span> <br><span data-ttu-id="b42e7-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-483">http</span><span class="sxs-lookup"><span data-stu-id="b42e7-483">HTTP</span></span></td>
      <td><span data-ttu-id="b42e7-484">Report</span><span class="sxs-lookup"><span data-stu-id="b42e7-484">Report</span></span></td>
      <td><span data-ttu-id="b42e7-485">Report, dashboard</span><span class="sxs-lookup"><span data-stu-id="b42e7-485">Report, dashboard</span></span></td>
      <td><span data-ttu-id="b42e7-486">
        <font size=2> Protocollo: http</span><span class="sxs-lookup"><span data-stu-id="b42e7-486">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="b42e7-487">Autenticazione: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="b42e7-487">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="b42e7-488">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-488">Address:</span></span> <br><span data-ttu-id="b42e7-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-490">http</span><span class="sxs-lookup"><span data-stu-id="b42e7-490">HTTP</span></span></td>
      <td><span data-ttu-id="b42e7-491">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-491">Table</span></span></td>
      <td><span data-ttu-id="b42e7-492">Endpoint, file</span><span class="sxs-lookup"><span data-stu-id="b42e7-492">Endpoint, file</span></span></td>
      <td><span data-ttu-id="b42e7-493">
        <font size=2> Protocollo: http</span><span class="sxs-lookup"><span data-stu-id="b42e7-493">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="b42e7-494">Autenticazione: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="b42e7-494">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="b42e7-495">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-495">Address:</span></span> <br><span data-ttu-id="b42e7-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-497">MySQL</span><span class="sxs-lookup"><span data-stu-id="b42e7-497">MySQL</span></span></td>
      <td><span data-ttu-id="b42e7-498">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-498">Container</span></span></td>
      <td><span data-ttu-id="b42e7-499">Database</span><span class="sxs-lookup"><span data-stu-id="b42e7-499">Database</span></span></td>
      <td><span data-ttu-id="b42e7-500">
        <font size=2> Protocollo: mysql</span><span class="sxs-lookup"><span data-stu-id="b42e7-500">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="b42e7-501">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-501">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="b42e7-502">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-502">Address:</span></span> <br><span data-ttu-id="b42e7-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-505">MySQL</span><span class="sxs-lookup"><span data-stu-id="b42e7-505">MySQL</span></span></td>
      <td><span data-ttu-id="b42e7-506">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-506">Table</span></span></td>
      <td><span data-ttu-id="b42e7-507">Tabella, vista</span><span class="sxs-lookup"><span data-stu-id="b42e7-507">Table, view</span></span></td>
      <td><span data-ttu-id="b42e7-508">
        <font size=2> Protocollo: mysql</span><span class="sxs-lookup"><span data-stu-id="b42e7-508">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="b42e7-509">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-509">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="b42e7-510">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-510">Address:</span></span> <br><span data-ttu-id="b42e7-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-514">OData</span><span class="sxs-lookup"><span data-stu-id="b42e7-514">OData</span></span></td>
      <td><span data-ttu-id="b42e7-515">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-515">Container</span></span></td>
      <td><span data-ttu-id="b42e7-516">Contenitore di entità</span><span class="sxs-lookup"><span data-stu-id="b42e7-516">Entity container</span></span></td>
      <td><span data-ttu-id="b42e7-517">
        <font size=2> Protocollo: odata</span><span class="sxs-lookup"><span data-stu-id="b42e7-517">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="b42e7-518">Autenticazione: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-518">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="b42e7-519">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-519">Address:</span></span> <br><span data-ttu-id="b42e7-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-521">OData</span><span class="sxs-lookup"><span data-stu-id="b42e7-521">OData</span></span></td>
      <td><span data-ttu-id="b42e7-522">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-522">Table</span></span></td>
      <td><span data-ttu-id="b42e7-523">Set di entità, funzione</span><span class="sxs-lookup"><span data-stu-id="b42e7-523">Entity set, function</span></span></td>
      <td><span data-ttu-id="b42e7-524">
        <font size=2> Protocollo: odata</span><span class="sxs-lookup"><span data-stu-id="b42e7-524">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="b42e7-525">Autenticazione: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-525">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="b42e7-526">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-526">Address:</span></span> <br><span data-ttu-id="b42e7-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="b42e7-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="b42e7-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; risorsa </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-529">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="b42e7-529">Oracle Database</span></span></td>
      <td><span data-ttu-id="b42e7-530">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-530">Container</span></span></td>
      <td><span data-ttu-id="b42e7-531">Database</span><span class="sxs-lookup"><span data-stu-id="b42e7-531">Database</span></span></td>
      <td><span data-ttu-id="b42e7-532">
        <font size=2> Protocollo: oracle</span><span class="sxs-lookup"><span data-stu-id="b42e7-532">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="b42e7-533">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-533">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="b42e7-534">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-534">Address:</span></span> <br><span data-ttu-id="b42e7-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-537">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="b42e7-537">Oracle Database</span></span></td>
      <td><span data-ttu-id="b42e7-538">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-538">Table</span></span></td>
      <td><span data-ttu-id="b42e7-539">Tabella, vista</span><span class="sxs-lookup"><span data-stu-id="b42e7-539">Table, view</span></span></td>
      <td><span data-ttu-id="b42e7-540">
        <font size=2> Protocollo: oracle</span><span class="sxs-lookup"><span data-stu-id="b42e7-540">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="b42e7-541">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-541">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="b42e7-542">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-542">Address:</span></span> <br><span data-ttu-id="b42e7-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="b42e7-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="b42e7-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-547">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="b42e7-547">PostgreSQL</span></span></td>
      <td><span data-ttu-id="b42e7-548">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-548">Container</span></span></td>
      <td><span data-ttu-id="b42e7-549">Database</span><span class="sxs-lookup"><span data-stu-id="b42e7-549">Database</span></span></td>
      <td><span data-ttu-id="b42e7-550">
        <font size=2> Protocollo: postgresql</span><span class="sxs-lookup"><span data-stu-id="b42e7-550">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="b42e7-551">Autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-551">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="b42e7-552">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-552">Address:</span></span> <br><span data-ttu-id="b42e7-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-555">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="b42e7-555">PostgreSQL</span></span></td>
      <td><span data-ttu-id="b42e7-556">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-556">Table</span></span></td>
      <td><span data-ttu-id="b42e7-557">Tabella, vista</span><span class="sxs-lookup"><span data-stu-id="b42e7-557">Table, view</span></span></td>
      <td><span data-ttu-id="b42e7-558">
        <font size=2> Protocollo: postgresql</span><span class="sxs-lookup"><span data-stu-id="b42e7-558">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="b42e7-559">Autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-559">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="b42e7-560">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-560">Address:</span></span> <br><span data-ttu-id="b42e7-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="b42e7-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="b42e7-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-565">Power BI</span><span class="sxs-lookup"><span data-stu-id="b42e7-565">Power BI</span></span></td>
      <td><span data-ttu-id="b42e7-566">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-566">Container</span></span></td>
      <td><span data-ttu-id="b42e7-567">Sito</span><span class="sxs-lookup"><span data-stu-id="b42e7-567">Site</span></span></td>
      <td><span data-ttu-id="b42e7-568">
        <font size=2> Protocollo: http</span><span class="sxs-lookup"><span data-stu-id="b42e7-568">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="b42e7-569">Autenticazione: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="b42e7-569">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="b42e7-570">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-570">Address:</span></span> <br><span data-ttu-id="b42e7-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-572">Power BI</span><span class="sxs-lookup"><span data-stu-id="b42e7-572">Power BI</span></span></td>
      <td><span data-ttu-id="b42e7-573">Report</span><span class="sxs-lookup"><span data-stu-id="b42e7-573">Report</span></span></td>
      <td><span data-ttu-id="b42e7-574">Report, dashboard</span><span class="sxs-lookup"><span data-stu-id="b42e7-574">Report, dashboard</span></span></td>
      <td><span data-ttu-id="b42e7-575">
        <font size=2> Protocollo: http</span><span class="sxs-lookup"><span data-stu-id="b42e7-575">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="b42e7-576">Autenticazione: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="b42e7-576">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="b42e7-577">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-577">Address:</span></span> <br><span data-ttu-id="b42e7-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-579">Power Query</span><span class="sxs-lookup"><span data-stu-id="b42e7-579">Power Query</span></span></td>
      <td><span data-ttu-id="b42e7-580">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-580">Table</span></span></td>
      <td><span data-ttu-id="b42e7-581">Mashup di dati</span><span class="sxs-lookup"><span data-stu-id="b42e7-581">Data mashup</span></span></td>
      <td><span data-ttu-id="b42e7-582">
        <font size=2> Protocollo: power-query</span><span class="sxs-lookup"><span data-stu-id="b42e7-582">
        <font size=2> Protocol: power-query</span></span> <br><span data-ttu-id="b42e7-583">Autenticazione: {oauth}</span><span class="sxs-lookup"><span data-stu-id="b42e7-583">Authentication: {oauth}</span></span> <br><span data-ttu-id="b42e7-584">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-584">Address:</span></span> <br><span data-ttu-id="b42e7-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-586">Salesforce</span><span class="sxs-lookup"><span data-stu-id="b42e7-586">Salesforce</span></span></td>
      <td><span data-ttu-id="b42e7-587">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-587">Table</span></span></td>
      <td><span data-ttu-id="b42e7-588">Oggetto</span><span class="sxs-lookup"><span data-stu-id="b42e7-588">Object</span></span></td>
      <td><span data-ttu-id="b42e7-589">
        <font size=2> Protocollo: salesforce-com</span><span class="sxs-lookup"><span data-stu-id="b42e7-589">
        <font size=2> Protocol: salesforce-com</span></span> <br><span data-ttu-id="b42e7-590">Autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-590">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="b42e7-591">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-591">Address:</span></span> <br><span data-ttu-id="b42e7-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span><span class="sxs-lookup"><span data-stu-id="b42e7-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span></span> <br><span data-ttu-id="b42e7-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; classe</span><span class="sxs-lookup"><span data-stu-id="b42e7-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span></span> <br><span data-ttu-id="b42e7-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-595">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="b42e7-595">SAP HANA</span></span></td>
      <td><span data-ttu-id="b42e7-596">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-596">Container</span></span></td>
      <td><span data-ttu-id="b42e7-597">Server</span><span class="sxs-lookup"><span data-stu-id="b42e7-597">Server</span></span></td>
      <td><span data-ttu-id="b42e7-598">
        <font size=2> Protocollo: sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="b42e7-598">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="b42e7-599">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-599">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="b42e7-600">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-600">Address:</span></span> <br><span data-ttu-id="b42e7-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-602">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="b42e7-602">SAP HANA</span></span></td>
      <td><span data-ttu-id="b42e7-603">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-603">Table</span></span></td>
      <td><span data-ttu-id="b42e7-604">Visualizza</span><span class="sxs-lookup"><span data-stu-id="b42e7-604">View</span></span></td>
      <td><span data-ttu-id="b42e7-605">
        <font size=2> Protocollo: sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="b42e7-605">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="b42e7-606">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-606">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="b42e7-607">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-607">Address:</span></span> <br><span data-ttu-id="b42e7-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="b42e7-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="b42e7-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-611">SharePoint</span><span class="sxs-lookup"><span data-stu-id="b42e7-611">SharePoint</span></span></td>
      <td><span data-ttu-id="b42e7-612">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-612">Table</span></span></td>
      <td><span data-ttu-id="b42e7-613">Elenco</span><span class="sxs-lookup"><span data-stu-id="b42e7-613">List</span></span></td>
      <td><span data-ttu-id="b42e7-614">
        <font size=2> Protocollo: sharepoint-list</span><span class="sxs-lookup"><span data-stu-id="b42e7-614">
        <font size=2> Protocol: sharepoint-list</span></span> <br><span data-ttu-id="b42e7-615">Autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-615">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="b42e7-616">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-616">Address:</span></span> <br><span data-ttu-id="b42e7-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-618">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b42e7-618">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="b42e7-619">Comando</span><span class="sxs-lookup"><span data-stu-id="b42e7-619">Command</span></span></td>
      <td><span data-ttu-id="b42e7-620">Stored procedure</span><span class="sxs-lookup"><span data-stu-id="b42e7-620">Stored procedure</span></span></td>
      <td><span data-ttu-id="b42e7-621">
        <font size=2> Protocollo: tds</span><span class="sxs-lookup"><span data-stu-id="b42e7-621">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="b42e7-622">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-622">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="b42e7-623">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-623">Address:</span></span> <br><span data-ttu-id="b42e7-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="b42e7-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="b42e7-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-628">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b42e7-628">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="b42e7-629">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="b42e7-629">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="b42e7-630">Funzione con valori di tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-630">Table-valued function</span></span></td>
      <td><span data-ttu-id="b42e7-631">
        <font size=2> Protocollo: tds</span><span class="sxs-lookup"><span data-stu-id="b42e7-631">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="b42e7-632">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-632">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="b42e7-633">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-633">Address:</span></span> <br><span data-ttu-id="b42e7-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="b42e7-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="b42e7-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-638">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b42e7-638">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="b42e7-639">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-639">Container</span></span></td>
      <td><span data-ttu-id="b42e7-640">Database</span><span class="sxs-lookup"><span data-stu-id="b42e7-640">Database</span></span></td>
      <td><span data-ttu-id="b42e7-641">
        <font size=2> Protocollo: tds</span><span class="sxs-lookup"><span data-stu-id="b42e7-641">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="b42e7-642">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-642">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="b42e7-643">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-643">Address:</span></span> <br><span data-ttu-id="b42e7-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-646">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b42e7-646">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="b42e7-647">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-647">Table</span></span></td>
      <td><span data-ttu-id="b42e7-648">Tabella, vista</span><span class="sxs-lookup"><span data-stu-id="b42e7-648">Table, view</span></span></td>
      <td><span data-ttu-id="b42e7-649">
        <font size=2> Protocollo: tds</span><span class="sxs-lookup"><span data-stu-id="b42e7-649">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="b42e7-650">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-650">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="b42e7-651">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-651">Address:</span></span> <br><span data-ttu-id="b42e7-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="b42e7-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="b42e7-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-656">SQL Server</span><span class="sxs-lookup"><span data-stu-id="b42e7-656">SQL Server</span></span></td>
      <td><span data-ttu-id="b42e7-657">Comando</span><span class="sxs-lookup"><span data-stu-id="b42e7-657">Command</span></span></td>
      <td><span data-ttu-id="b42e7-658">Stored procedure</span><span class="sxs-lookup"><span data-stu-id="b42e7-658">Stored procedure</span></span></td>
      <td><span data-ttu-id="b42e7-659">
        <font size=2> Protocollo: tds</span><span class="sxs-lookup"><span data-stu-id="b42e7-659">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="b42e7-660">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-660">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="b42e7-661">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-661">Address:</span></span> <br><span data-ttu-id="b42e7-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="b42e7-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="b42e7-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-666">SQL Server</span><span class="sxs-lookup"><span data-stu-id="b42e7-666">SQL Server</span></span></td>
      <td><span data-ttu-id="b42e7-667">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="b42e7-667">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="b42e7-668">Funzione con valori di tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-668">Table-valued function</span></span></td>
      <td><span data-ttu-id="b42e7-669">
        <font size=2> Protocollo: tds</span><span class="sxs-lookup"><span data-stu-id="b42e7-669">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="b42e7-670">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-670">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="b42e7-671">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-671">Address:</span></span> <br><span data-ttu-id="b42e7-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="b42e7-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="b42e7-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-676">SQL Server</span><span class="sxs-lookup"><span data-stu-id="b42e7-676">SQL Server</span></span></td>
      <td><span data-ttu-id="b42e7-677">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-677">Container</span></span></td>
      <td><span data-ttu-id="b42e7-678">Database</span><span class="sxs-lookup"><span data-stu-id="b42e7-678">Database</span></span></td>
      <td><span data-ttu-id="b42e7-679">
        <font size=2> Protocollo: tds</span><span class="sxs-lookup"><span data-stu-id="b42e7-679">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="b42e7-680">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-680">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="b42e7-681">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-681">Address:</span></span> <br><span data-ttu-id="b42e7-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-684">SQL Server</span><span class="sxs-lookup"><span data-stu-id="b42e7-684">SQL Server</span></span></td>
      <td><span data-ttu-id="b42e7-685">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-685">Table</span></span></td>
      <td><span data-ttu-id="b42e7-686">Tabella, vista</span><span class="sxs-lookup"><span data-stu-id="b42e7-686">Table, view</span></span></td>
      <td><span data-ttu-id="b42e7-687">
        <font size=2> Protocollo: tds</span><span class="sxs-lookup"><span data-stu-id="b42e7-687">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="b42e7-688">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-688">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="b42e7-689">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-689">Address:</span></span> <br><span data-ttu-id="b42e7-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="b42e7-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="b42e7-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-694">Modelli multidimensionali di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="b42e7-694">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="b42e7-695">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-695">Container</span></span></td>
      <td><span data-ttu-id="b42e7-696">Modello</span><span class="sxs-lookup"><span data-stu-id="b42e7-696">Model</span></span></td>
      <td><span data-ttu-id="b42e7-697">
        <font size=2> Protocollo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="b42e7-697">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="b42e7-698">Autenticazione: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="b42e7-698">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="b42e7-699">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-699">Address:</span></span> <br><span data-ttu-id="b42e7-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modello </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-703">Modelli multidimensionali di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="b42e7-703">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="b42e7-704">KPI</span><span class="sxs-lookup"><span data-stu-id="b42e7-704">KPI</span></span></td>
      <td><span data-ttu-id="b42e7-705">KPI</span><span class="sxs-lookup"><span data-stu-id="b42e7-705">KPI</span></span></td>
      <td><span data-ttu-id="b42e7-706">
        <font size=2> Protocollo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="b42e7-706">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="b42e7-707">Autenticazione: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="b42e7-707">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="b42e7-708">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-708">Address:</span></span> <br><span data-ttu-id="b42e7-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modello</span><span class="sxs-lookup"><span data-stu-id="b42e7-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="b42e7-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto</span><span class="sxs-lookup"><span data-stu-id="b42e7-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="b42e7-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-714">Modelli multidimensionali di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="b42e7-714">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="b42e7-715">Measure</span><span class="sxs-lookup"><span data-stu-id="b42e7-715">Measure</span></span></td>
      <td><span data-ttu-id="b42e7-716">Measure</span><span class="sxs-lookup"><span data-stu-id="b42e7-716">Measure</span></span></td>
      <td><span data-ttu-id="b42e7-717">
        <font size=2> Protocollo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="b42e7-717">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="b42e7-718">Autenticazione: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="b42e7-718">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="b42e7-719">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-719">Address:</span></span> <br><span data-ttu-id="b42e7-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modello</span><span class="sxs-lookup"><span data-stu-id="b42e7-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="b42e7-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto</span><span class="sxs-lookup"><span data-stu-id="b42e7-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="b42e7-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-725">Modelli multidimensionali di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="b42e7-725">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="b42e7-726">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-726">Table</span></span></td>
      <td><span data-ttu-id="b42e7-727">Dimensione</span><span class="sxs-lookup"><span data-stu-id="b42e7-727">Dimension</span></span></td>
      <td><span data-ttu-id="b42e7-728">
        <font size=2> Protocollo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="b42e7-728">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="b42e7-729">Autenticazione: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="b42e7-729">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="b42e7-730">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-730">Address:</span></span> <br><span data-ttu-id="b42e7-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modello</span><span class="sxs-lookup"><span data-stu-id="b42e7-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="b42e7-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto</span><span class="sxs-lookup"><span data-stu-id="b42e7-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="b42e7-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-736">Tabulare di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="b42e7-736">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="b42e7-737">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-737">Container</span></span></td>
      <td><span data-ttu-id="b42e7-738">Modello</span><span class="sxs-lookup"><span data-stu-id="b42e7-738">Model</span></span></td>
      <td><span data-ttu-id="b42e7-739">
        <font size=2> Protocollo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="b42e7-739">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="b42e7-740">Autenticazione: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="b42e7-740">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="b42e7-741">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-741">Address:</span></span> <br><span data-ttu-id="b42e7-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modello </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-745">Tabulare di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="b42e7-745">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="b42e7-746">KPI</span><span class="sxs-lookup"><span data-stu-id="b42e7-746">KPI</span></span></td>
      <td><span data-ttu-id="b42e7-747">KPI</span><span class="sxs-lookup"><span data-stu-id="b42e7-747">KPI</span></span></td>
      <td><span data-ttu-id="b42e7-748">
        <font size=2> Protocollo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="b42e7-748">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="b42e7-749">Autenticazione: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="b42e7-749">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="b42e7-750">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-750">Address:</span></span> <br><span data-ttu-id="b42e7-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modello</span><span class="sxs-lookup"><span data-stu-id="b42e7-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="b42e7-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto</span><span class="sxs-lookup"><span data-stu-id="b42e7-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="b42e7-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-756">Tabulare di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="b42e7-756">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="b42e7-757">Measure</span><span class="sxs-lookup"><span data-stu-id="b42e7-757">Measure</span></span></td>
      <td><span data-ttu-id="b42e7-758">Measure</span><span class="sxs-lookup"><span data-stu-id="b42e7-758">Measure</span></span></td>
      <td><span data-ttu-id="b42e7-759">
        <font size=2> Protocollo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="b42e7-759">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="b42e7-760">Autenticazione: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="b42e7-760">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="b42e7-761">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-761">Address:</span></span> <br><span data-ttu-id="b42e7-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modello</span><span class="sxs-lookup"><span data-stu-id="b42e7-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="b42e7-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto</span><span class="sxs-lookup"><span data-stu-id="b42e7-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="b42e7-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-767">Tabulare di SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="b42e7-767">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="b42e7-768">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-768">Table</span></span></td>
      <td><span data-ttu-id="b42e7-769">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-769">Table</span></span></td>
      <td><span data-ttu-id="b42e7-770">
        <font size=2> Protocollo: analysis-services</span><span class="sxs-lookup"><span data-stu-id="b42e7-770">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="b42e7-771">Autenticazione: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="b42e7-771">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="b42e7-772">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-772">Address:</span></span> <br><span data-ttu-id="b42e7-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modello</span><span class="sxs-lookup"><span data-stu-id="b42e7-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="b42e7-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto</span><span class="sxs-lookup"><span data-stu-id="b42e7-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="b42e7-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-778">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="b42e7-778">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="b42e7-779">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-779">Container</span></span></td>
      <td><span data-ttu-id="b42e7-780">Server</span><span class="sxs-lookup"><span data-stu-id="b42e7-780">Server</span></span></td>
      <td><span data-ttu-id="b42e7-781">
        <font size=2> Protocollo: reporting-services</span><span class="sxs-lookup"><span data-stu-id="b42e7-781">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="b42e7-782">Autenticazione: {windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-782">Authentication: {windows}</span></span> <br><span data-ttu-id="b42e7-783">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-783">Address:</span></span> <br><span data-ttu-id="b42e7-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; versione: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-786">SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="b42e7-786">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="b42e7-787">Report</span><span class="sxs-lookup"><span data-stu-id="b42e7-787">Report</span></span></td>
      <td><span data-ttu-id="b42e7-788">Report</span><span class="sxs-lookup"><span data-stu-id="b42e7-788">Report</span></span></td>
      <td><span data-ttu-id="b42e7-789">
        <font size=2> Protocollo: reporting-services</span><span class="sxs-lookup"><span data-stu-id="b42e7-789">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="b42e7-790">Autenticazione: {windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-790">Authentication: {windows}</span></span> <br><span data-ttu-id="b42e7-791">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-791">Address:</span></span> <br><span data-ttu-id="b42e7-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; percorso</span><span class="sxs-lookup"><span data-stu-id="b42e7-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span></span> <br><span data-ttu-id="b42e7-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; versione: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-795">Teradata</span><span class="sxs-lookup"><span data-stu-id="b42e7-795">Teradata</span></span></td>
      <td><span data-ttu-id="b42e7-796">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-796">Container</span></span></td>
      <td><span data-ttu-id="b42e7-797">Database</span><span class="sxs-lookup"><span data-stu-id="b42e7-797">Database</span></span></td>
      <td><span data-ttu-id="b42e7-798">
        <font size=2> Protocollo: teradata</span><span class="sxs-lookup"><span data-stu-id="b42e7-798">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="b42e7-799">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-799">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="b42e7-800">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-800">Address:</span></span> <br><span data-ttu-id="b42e7-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-803">Teradata</span><span class="sxs-lookup"><span data-stu-id="b42e7-803">Teradata</span></span></td>
      <td><span data-ttu-id="b42e7-804">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-804">Table</span></span></td>
      <td><span data-ttu-id="b42e7-805">Tabella, vista</span><span class="sxs-lookup"><span data-stu-id="b42e7-805">Table, view</span></span></td>
      <td><span data-ttu-id="b42e7-806">
        <font size=2> Protocollo: teradata</span><span class="sxs-lookup"><span data-stu-id="b42e7-806">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="b42e7-807">Autenticazione: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-807">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="b42e7-808">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-808">Address:</span></span> <br><span data-ttu-id="b42e7-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-812">Master Data Services di SQL Server</span><span class="sxs-lookup"><span data-stu-id="b42e7-812">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="b42e7-813">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-813">Container</span></span></td>
      <td><span data-ttu-id="b42e7-814">Modello</span><span class="sxs-lookup"><span data-stu-id="b42e7-814">Model</span></span></td>
      <td><span data-ttu-id="b42e7-815">
        <font size="2"> Protocollo: mssql mds</span><span class="sxs-lookup"><span data-stu-id="b42e7-815">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="b42e7-816">Autenticazione: {windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-816">Authentication: {windows}</span></span> <br><span data-ttu-id="b42e7-817">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-817">Address:</span></span> <br><span data-ttu-id="b42e7-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="b42e7-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="b42e7-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modello</span><span class="sxs-lookup"><span data-stu-id="b42e7-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="b42e7-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; versione </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-821">Master Data Services di SQL Server</span><span class="sxs-lookup"><span data-stu-id="b42e7-821">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="b42e7-822">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-822">Table</span></span></td>
      <td><span data-ttu-id="b42e7-823">Entità</span><span class="sxs-lookup"><span data-stu-id="b42e7-823">Entity</span></span></td>
      <td><span data-ttu-id="b42e7-824">
        <font size="2"> Protocollo: mssql mds</span><span class="sxs-lookup"><span data-stu-id="b42e7-824">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="b42e7-825">Autenticazione: {windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-825">Authentication: {windows}</span></span> <br><span data-ttu-id="b42e7-826">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-826">Address:</span></span> <br><span data-ttu-id="b42e7-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="b42e7-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="b42e7-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; modello</span><span class="sxs-lookup"><span data-stu-id="b42e7-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="b42e7-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; versione</span><span class="sxs-lookup"><span data-stu-id="b42e7-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span></span> <br><span data-ttu-id="b42e7-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entità </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-831">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b42e7-831">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="b42e7-832">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-832">Container</span></span></td>
      <td><span data-ttu-id="b42e7-833">Database</span><span class="sxs-lookup"><span data-stu-id="b42e7-833">Database</span></span></td>
      <td><span data-ttu-id="b42e7-834">
        <font size=2> Protocollo: document-db</span><span class="sxs-lookup"><span data-stu-id="b42e7-834">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="b42e7-835">Autenticazione: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="b42e7-835">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="b42e7-836">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-836">Address:</span></span> <br><span data-ttu-id="b42e7-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="b42e7-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="b42e7-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-839">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b42e7-839">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="b42e7-840">Raccolta</span><span class="sxs-lookup"><span data-stu-id="b42e7-840">Collection</span></span></td>
      <td><span data-ttu-id="b42e7-841">Raccolta</span><span class="sxs-lookup"><span data-stu-id="b42e7-841">Collection</span></span></td>
      <td><span data-ttu-id="b42e7-842">
        <font size=2> Protocollo: document-db</span><span class="sxs-lookup"><span data-stu-id="b42e7-842">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="b42e7-843">Autenticazione: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="b42e7-843">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="b42e7-844">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-844">Address:</span></span> <br><span data-ttu-id="b42e7-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="b42e7-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="b42e7-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; raccolta </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; collection </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-848">ODBC generico</span><span class="sxs-lookup"><span data-stu-id="b42e7-848">Generic ODBC</span></span></td>
      <td><span data-ttu-id="b42e7-849">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-849">Container</span></span></td>
      <td><span data-ttu-id="b42e7-850">Database</span><span class="sxs-lookup"><span data-stu-id="b42e7-850">Database</span></span></td>
      <td><span data-ttu-id="b42e7-851">
        <font size=2> Protocollo: odbc</span><span class="sxs-lookup"><span data-stu-id="b42e7-851">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="b42e7-852">Autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-852">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="b42e7-853">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-853">Address:</span></span> <br><span data-ttu-id="b42e7-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; opzioni</span><span class="sxs-lookup"><span data-stu-id="b42e7-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="b42e7-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-856">ODBC generico</span><span class="sxs-lookup"><span data-stu-id="b42e7-856">Generic ODBC</span></span></td>
      <td><span data-ttu-id="b42e7-857">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-857">Table</span></span></td>
      <td><span data-ttu-id="b42e7-858">Tabella, vista</span><span class="sxs-lookup"><span data-stu-id="b42e7-858">Table, View</span></span></td>
      <td><span data-ttu-id="b42e7-859">
        <font size=2> Protocollo: odbc</span><span class="sxs-lookup"><span data-stu-id="b42e7-859">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="b42e7-860">Autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-860">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="b42e7-861">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-861">Address:</span></span> <br><span data-ttu-id="b42e7-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; opzioni</span><span class="sxs-lookup"><span data-stu-id="b42e7-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="b42e7-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto</span><span class="sxs-lookup"><span data-stu-id="b42e7-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="b42e7-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-866">Sybase</span><span class="sxs-lookup"><span data-stu-id="b42e7-866">Sybase</span></span></td>
      <td><span data-ttu-id="b42e7-867">Contenitore</span><span class="sxs-lookup"><span data-stu-id="b42e7-867">Container</span></span></td>
      <td><span data-ttu-id="b42e7-868">Database</span><span class="sxs-lookup"><span data-stu-id="b42e7-868">Database</span></span></td>
      <td><span data-ttu-id="b42e7-869">
        <font size=2>protocollo: sybase</span><span class="sxs-lookup"><span data-stu-id="b42e7-869">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="b42e7-870">autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-870">authentication: {basic, windows}</span></span> <br><span data-ttu-id="b42e7-871">indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-871">address:</span></span> <br><span data-ttu-id="b42e7-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-874">Sybase</span><span class="sxs-lookup"><span data-stu-id="b42e7-874">Sybase</span></span></td>
      <td><span data-ttu-id="b42e7-875">Tabella</span><span class="sxs-lookup"><span data-stu-id="b42e7-875">Table</span></span></td>
      <td><span data-ttu-id="b42e7-876">Tabella, vista</span><span class="sxs-lookup"><span data-stu-id="b42e7-876">Table, View</span></span></td>
      <td><span data-ttu-id="b42e7-877">
        <font size=2>protocollo: sybase</span><span class="sxs-lookup"><span data-stu-id="b42e7-877">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="b42e7-878">autenticazione: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="b42e7-878">authentication: {basic, windows}</span></span> <br><span data-ttu-id="b42e7-879">indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-879">address:</span></span> <br><span data-ttu-id="b42e7-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="b42e7-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="b42e7-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="b42e7-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="b42e7-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="b42e7-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="b42e7-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; oggetto </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="b42e7-884">Altro (nessuna delle opzioni precedenti)</span><span class="sxs-lookup"><span data-stu-id="b42e7-884">Other (none of the above)</span></span></td>
      <td>\*</td>
      <td>\*</td>
      <td><span data-ttu-id="b42e7-885">
        <font size=2> Protocollo: generic-asset</span><span class="sxs-lookup"><span data-stu-id="b42e7-885">
        <font size=2> Protocol: generic-asset</span></span> <br><span data-ttu-id="b42e7-886">Indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b42e7-886">Address:</span></span> <br><span data-ttu-id="b42e7-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span><span class="sxs-lookup"><span data-stu-id="b42e7-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span></span></td>
    </tr>
</table>
