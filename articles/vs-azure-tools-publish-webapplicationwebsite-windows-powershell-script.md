---
title: Publish-WebApplicationWebSite (script di Windows PowerShell) | Documentazione Microsoft
description: Informazioni su come pubblicare un progetto Web in un sito Web di Azure. Se non sono presenti, lo script crea le risorse necessarie nella sottoscrizione di Azure.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 07d21b7ce6cd8aee1cff704d316e7a2ca8c00437
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a><span data-ttu-id="a1aac-104">Publish-WebApplicationWebSite (script di Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="a1aac-104">Publish-WebApplicationWebSite (Windows PowerShell script)</span></span>
## <a name="syntax"></a><span data-ttu-id="a1aac-105">Sintassi</span><span class="sxs-lookup"><span data-stu-id="a1aac-105">Syntax</span></span>
<span data-ttu-id="a1aac-106">Pubblica un progetto Web in un sito Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="a1aac-106">Publishes a web project to an Azure website.</span></span> <span data-ttu-id="a1aac-107">Se non sono presenti, lo script crea le risorse necessarie nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a1aac-107">The script creates the required resources in your Azure subscription if they don't exist.</span></span>

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a><span data-ttu-id="a1aac-108">Configurazione</span><span class="sxs-lookup"><span data-stu-id="a1aac-108">Configuration</span></span>
<span data-ttu-id="a1aac-109">Percorso del file di configurazione JSON che descrive i dettagli della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a1aac-109">The path to the JSON configuration file that describes the details of the deployment.</span></span>

| <span data-ttu-id="a1aac-110">Parametro</span><span class="sxs-lookup"><span data-stu-id="a1aac-110">Parameter</span></span> | <span data-ttu-id="a1aac-111">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="a1aac-111">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="a1aac-112">Alias</span><span class="sxs-lookup"><span data-stu-id="a1aac-112">Aliases</span></span> |<span data-ttu-id="a1aac-113">nessuno</span><span class="sxs-lookup"><span data-stu-id="a1aac-113">none</span></span> |
| <span data-ttu-id="a1aac-114">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="a1aac-114">Required?</span></span> |<span data-ttu-id="a1aac-115">true</span><span class="sxs-lookup"><span data-stu-id="a1aac-115">true</span></span> |
| <span data-ttu-id="a1aac-116">Posizione</span><span class="sxs-lookup"><span data-stu-id="a1aac-116">Position</span></span> |<span data-ttu-id="a1aac-117">denominata</span><span class="sxs-lookup"><span data-stu-id="a1aac-117">named</span></span> |
| <span data-ttu-id="a1aac-118">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="a1aac-118">Default value</span></span> |<span data-ttu-id="a1aac-119">nessuno</span><span class="sxs-lookup"><span data-stu-id="a1aac-119">none</span></span> |
| <span data-ttu-id="a1aac-120">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="a1aac-120">Accept pipeline input?</span></span> |<span data-ttu-id="a1aac-121">false</span><span class="sxs-lookup"><span data-stu-id="a1aac-121">false</span></span> |
| <span data-ttu-id="a1aac-122">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="a1aac-122">Accept wildcard characters?</span></span> |<span data-ttu-id="a1aac-123">false</span><span class="sxs-lookup"><span data-stu-id="a1aac-123">false</span></span> |

## <a name="subscriptionname"></a><span data-ttu-id="a1aac-124">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="a1aac-124">SubscriptionName</span></span>
<span data-ttu-id="a1aac-125">Nome della sottoscrizione di Azure in cui si vuole creare il sito Web.</span><span class="sxs-lookup"><span data-stu-id="a1aac-125">The name of the Azure subscription that you want to create the website in.</span></span>

| <span data-ttu-id="a1aac-126">Parametro</span><span class="sxs-lookup"><span data-stu-id="a1aac-126">Parameter</span></span> | <span data-ttu-id="a1aac-127">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="a1aac-127">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="a1aac-128">Alias</span><span class="sxs-lookup"><span data-stu-id="a1aac-128">Aliases</span></span> |<span data-ttu-id="a1aac-129">nessuno</span><span class="sxs-lookup"><span data-stu-id="a1aac-129">none</span></span> |
| <span data-ttu-id="a1aac-130">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="a1aac-130">Required?</span></span> |<span data-ttu-id="a1aac-131">false</span><span class="sxs-lookup"><span data-stu-id="a1aac-131">false</span></span> |
| <span data-ttu-id="a1aac-132">Posizione</span><span class="sxs-lookup"><span data-stu-id="a1aac-132">Position</span></span> |<span data-ttu-id="a1aac-133">denominata</span><span class="sxs-lookup"><span data-stu-id="a1aac-133">named</span></span> |
| <span data-ttu-id="a1aac-134">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="a1aac-134">Default value</span></span> |<span data-ttu-id="a1aac-135">nessuno</span><span class="sxs-lookup"><span data-stu-id="a1aac-135">none</span></span> |
| <span data-ttu-id="a1aac-136">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="a1aac-136">Accept pipeline input?</span></span> |<span data-ttu-id="a1aac-137">false</span><span class="sxs-lookup"><span data-stu-id="a1aac-137">false</span></span> |
| <span data-ttu-id="a1aac-138">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="a1aac-138">Accept wildcard characters?</span></span> |<span data-ttu-id="a1aac-139">false</span><span class="sxs-lookup"><span data-stu-id="a1aac-139">false</span></span> |

## <a name="webdeploypackage"></a><span data-ttu-id="a1aac-140">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="a1aac-140">WebDeployPackage</span></span>
<span data-ttu-id="a1aac-141">Percorso al pacchetto di distribuzione Web da pubblicare nel sito Web.</span><span class="sxs-lookup"><span data-stu-id="a1aac-141">The path to the web deployment package to publish to the website.</span></span> <span data-ttu-id="a1aac-142">È possibile creare questo pacchetto usando la pubblicazione Web guidata di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a1aac-142">You can create this package by using the Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="a1aac-143">Per ulteriori informazioni, vedere [Introduzione a Servizi cloud di Azure e ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span><span class="sxs-lookup"><span data-stu-id="a1aac-143">For more information, see [Get started with Azure Cloud Services and ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span></span>

| <span data-ttu-id="a1aac-144">Parametro</span><span class="sxs-lookup"><span data-stu-id="a1aac-144">Parameter</span></span> | <span data-ttu-id="a1aac-145">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="a1aac-145">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="a1aac-146">Alias</span><span class="sxs-lookup"><span data-stu-id="a1aac-146">Aliases</span></span> |<span data-ttu-id="a1aac-147">nessuno</span><span class="sxs-lookup"><span data-stu-id="a1aac-147">none</span></span> |
| <span data-ttu-id="a1aac-148">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="a1aac-148">Required?</span></span> |<span data-ttu-id="a1aac-149">false</span><span class="sxs-lookup"><span data-stu-id="a1aac-149">false</span></span> |
| <span data-ttu-id="a1aac-150">Posizione</span><span class="sxs-lookup"><span data-stu-id="a1aac-150">Position</span></span> |<span data-ttu-id="a1aac-151">denominata</span><span class="sxs-lookup"><span data-stu-id="a1aac-151">named</span></span> |
| <span data-ttu-id="a1aac-152">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="a1aac-152">Default value</span></span> |<span data-ttu-id="a1aac-153">nessuno</span><span class="sxs-lookup"><span data-stu-id="a1aac-153">none</span></span> |
| <span data-ttu-id="a1aac-154">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="a1aac-154">Accept pipeline input?</span></span> |<span data-ttu-id="a1aac-155">false</span><span class="sxs-lookup"><span data-stu-id="a1aac-155">false</span></span> |
| <span data-ttu-id="a1aac-156">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="a1aac-156">Accept wildcard characters?</span></span> |<span data-ttu-id="a1aac-157">false</span><span class="sxs-lookup"><span data-stu-id="a1aac-157">false</span></span> |

## <a name="databaseserverpassword"></a><span data-ttu-id="a1aac-158">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="a1aac-158">DatabaseServerPassword</span></span>
<span data-ttu-id="a1aac-159">Nome utente e password per il database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="a1aac-159">The username and password for the SQL database in Azure.</span></span>

| <span data-ttu-id="a1aac-160">Parametro</span><span class="sxs-lookup"><span data-stu-id="a1aac-160">Parameter</span></span> | <span data-ttu-id="a1aac-161">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="a1aac-161">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="a1aac-162">Alias</span><span class="sxs-lookup"><span data-stu-id="a1aac-162">Aliases</span></span> |<span data-ttu-id="a1aac-163">nessuno</span><span class="sxs-lookup"><span data-stu-id="a1aac-163">none</span></span> |
| <span data-ttu-id="a1aac-164">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="a1aac-164">Required?</span></span> |<span data-ttu-id="a1aac-165">false</span><span class="sxs-lookup"><span data-stu-id="a1aac-165">false</span></span> |
| <span data-ttu-id="a1aac-166">Posizione</span><span class="sxs-lookup"><span data-stu-id="a1aac-166">Position</span></span> |<span data-ttu-id="a1aac-167">denominata</span><span class="sxs-lookup"><span data-stu-id="a1aac-167">named</span></span> |
| <span data-ttu-id="a1aac-168">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="a1aac-168">Default value</span></span> |<span data-ttu-id="a1aac-169">nessuno</span><span class="sxs-lookup"><span data-stu-id="a1aac-169">none</span></span> |
| <span data-ttu-id="a1aac-170">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="a1aac-170">Accept pipeline input?</span></span> |<span data-ttu-id="a1aac-171">false</span><span class="sxs-lookup"><span data-stu-id="a1aac-171">false</span></span> |
| <span data-ttu-id="a1aac-172">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="a1aac-172">Accept wildcard characters?</span></span> |<span data-ttu-id="a1aac-173">false</span><span class="sxs-lookup"><span data-stu-id="a1aac-173">false</span></span> |

## <a name="sendhostmessagestooutput"></a><span data-ttu-id="a1aac-174">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="a1aac-174">SendHostMessagesToOutput</span></span>
<span data-ttu-id="a1aac-175">Se impostato su true, stampa i messaggi dallo script al flusso di output.</span><span class="sxs-lookup"><span data-stu-id="a1aac-175">If true, print messages from the script to the output stream.</span></span>

| <span data-ttu-id="a1aac-176">Parametro</span><span class="sxs-lookup"><span data-stu-id="a1aac-176">Parameter</span></span> | <span data-ttu-id="a1aac-177">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="a1aac-177">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="a1aac-178">Alias</span><span class="sxs-lookup"><span data-stu-id="a1aac-178">Aliases</span></span> |<span data-ttu-id="a1aac-179">nessuno</span><span class="sxs-lookup"><span data-stu-id="a1aac-179">none</span></span> |
| <span data-ttu-id="a1aac-180">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="a1aac-180">Required?</span></span> |<span data-ttu-id="a1aac-181">false</span><span class="sxs-lookup"><span data-stu-id="a1aac-181">false</span></span> |
| <span data-ttu-id="a1aac-182">Posizione</span><span class="sxs-lookup"><span data-stu-id="a1aac-182">Position</span></span> |<span data-ttu-id="a1aac-183">denominata</span><span class="sxs-lookup"><span data-stu-id="a1aac-183">named</span></span> |
| <span data-ttu-id="a1aac-184">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="a1aac-184">Default value</span></span> |<span data-ttu-id="a1aac-185">false</span><span class="sxs-lookup"><span data-stu-id="a1aac-185">false</span></span> |
| <span data-ttu-id="a1aac-186">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="a1aac-186">Accept pipeline input?</span></span> |<span data-ttu-id="a1aac-187">false</span><span class="sxs-lookup"><span data-stu-id="a1aac-187">false</span></span> |
| <span data-ttu-id="a1aac-188">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="a1aac-188">Accept wildcard characters?</span></span> |<span data-ttu-id="a1aac-189">false</span><span class="sxs-lookup"><span data-stu-id="a1aac-189">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="a1aac-190">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="a1aac-190">Remarks</span></span>
<span data-ttu-id="a1aac-191">Per una spiegazione completa sull'uso dello script per creare ambienti di sviluppo e test, vedere [Uso degli script di Windows PowerShell per la pubblicazione in ambienti di sviluppo e test](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="a1aac-191">For a complete explanation of how to use the script to create Dev and Test environments, see [Using Windows PowerShell Scripts to Publish to Dev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="a1aac-192">Il file di configurazione JSON specifica i dettagli degli elementi da distribuire.</span><span class="sxs-lookup"><span data-stu-id="a1aac-192">The JSON configuration file specifies the details of what is to be deployed.</span></span> <span data-ttu-id="a1aac-193">Include le informazioni specificate al momento della creazione del progetto, ad esempio il nome e il nome utente per il sito Web.</span><span class="sxs-lookup"><span data-stu-id="a1aac-193">It includes the information that you specified when you created the project, such as the name and username for the website.</span></span> <span data-ttu-id="a1aac-194">Se esiste, include anche il database di cui eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="a1aac-194">It also includes the database to provision, if any.</span></span> <span data-ttu-id="a1aac-195">Il codice seguente mostra un esempio di file di configurazione JSON:</span><span class="sxs-lookup"><span data-stu-id="a1aac-195">The following code shows an example JSON configuration file:</span></span>

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

<span data-ttu-id="a1aac-196">È possibile modificare il file di configurazione JSON per cambiare gli elementi da distribuire.</span><span class="sxs-lookup"><span data-stu-id="a1aac-196">You can edit the JSON configuration file to change what is deployed.</span></span> <span data-ttu-id="a1aac-197">La sezione webSite è obbligatoria, ma la sezione del database è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="a1aac-197">A webSite section is required, but the database section is optional.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1aac-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a1aac-198">Next steps</span></span>
<span data-ttu-id="a1aac-199">Per ulteriori informazioni, vedere [Publish-WebApplicationVM (script di Windows PowerShell)](vs-azure-tools-publish-webapplicationvm.md)</span><span class="sxs-lookup"><span data-stu-id="a1aac-199">For more information, see [Publish-WebApplicationVM (Windows PowerShell script)](vs-azure-tools-publish-webapplicationvm.md)</span></span>

