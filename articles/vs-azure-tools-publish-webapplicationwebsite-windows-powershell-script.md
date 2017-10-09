---
title: aaaPublish-WebApplicationWebSite (script di Windows PowerShell) | Documenti Microsoft
description: Informazioni su come toopublish web progetto tooan sito Web di Azure. In caso contrario, questo script crea le risorse necessarie hello nella sottoscrizione di Azure.
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
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a><span data-ttu-id="4c775-104">Publish-WebApplicationWebSite (script di Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="4c775-104">Publish-WebApplicationWebSite (Windows PowerShell script)</span></span>
## <a name="syntax"></a><span data-ttu-id="4c775-105">Sintassi</span><span class="sxs-lookup"><span data-stu-id="4c775-105">Syntax</span></span>
<span data-ttu-id="4c775-106">Pubblica un tooan progetto web sito Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="4c775-106">Publishes a web project tooan Azure website.</span></span> <span data-ttu-id="4c775-107">script di Hello crea risorse hello necessarie nella sottoscrizione di Azure, se non sono presenti.</span><span class="sxs-lookup"><span data-stu-id="4c775-107">hello script creates hello required resources in your Azure subscription if they don't exist.</span></span>

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a><span data-ttu-id="4c775-108">Configurazione</span><span class="sxs-lookup"><span data-stu-id="4c775-108">Configuration</span></span>
<span data-ttu-id="4c775-109">Hello percorso toohello file di configurazione JSON che descrive i dettagli di hello della distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="4c775-109">hello path toohello JSON configuration file that describes hello details of hello deployment.</span></span>

| <span data-ttu-id="4c775-110">.</span><span class="sxs-lookup"><span data-stu-id="4c775-110">Parameter</span></span> | <span data-ttu-id="4c775-111">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="4c775-111">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="4c775-112">Alias</span><span class="sxs-lookup"><span data-stu-id="4c775-112">Aliases</span></span> |<span data-ttu-id="4c775-113">nessuno</span><span class="sxs-lookup"><span data-stu-id="4c775-113">none</span></span> |
| <span data-ttu-id="4c775-114">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="4c775-114">Required?</span></span> |<span data-ttu-id="4c775-115">true</span><span class="sxs-lookup"><span data-stu-id="4c775-115">true</span></span> |
| <span data-ttu-id="4c775-116">Posizione</span><span class="sxs-lookup"><span data-stu-id="4c775-116">Position</span></span> |<span data-ttu-id="4c775-117">denominata</span><span class="sxs-lookup"><span data-stu-id="4c775-117">named</span></span> |
| <span data-ttu-id="4c775-118">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="4c775-118">Default value</span></span> |<span data-ttu-id="4c775-119">nessuno</span><span class="sxs-lookup"><span data-stu-id="4c775-119">none</span></span> |
| <span data-ttu-id="4c775-120">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="4c775-120">Accept pipeline input?</span></span> |<span data-ttu-id="4c775-121">false</span><span class="sxs-lookup"><span data-stu-id="4c775-121">false</span></span> |
| <span data-ttu-id="4c775-122">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="4c775-122">Accept wildcard characters?</span></span> |<span data-ttu-id="4c775-123">false</span><span class="sxs-lookup"><span data-stu-id="4c775-123">false</span></span> |

## <a name="subscriptionname"></a><span data-ttu-id="4c775-124">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="4c775-124">SubscriptionName</span></span>
<span data-ttu-id="4c775-125">nome Hello della sottoscrizione di Azure da sito Web di hello toocreate in hello.</span><span class="sxs-lookup"><span data-stu-id="4c775-125">hello name of hello Azure subscription that you want toocreate hello website in.</span></span>

| <span data-ttu-id="4c775-126">.</span><span class="sxs-lookup"><span data-stu-id="4c775-126">Parameter</span></span> | <span data-ttu-id="4c775-127">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="4c775-127">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="4c775-128">Alias</span><span class="sxs-lookup"><span data-stu-id="4c775-128">Aliases</span></span> |<span data-ttu-id="4c775-129">nessuno</span><span class="sxs-lookup"><span data-stu-id="4c775-129">none</span></span> |
| <span data-ttu-id="4c775-130">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="4c775-130">Required?</span></span> |<span data-ttu-id="4c775-131">false</span><span class="sxs-lookup"><span data-stu-id="4c775-131">false</span></span> |
| <span data-ttu-id="4c775-132">Posizione</span><span class="sxs-lookup"><span data-stu-id="4c775-132">Position</span></span> |<span data-ttu-id="4c775-133">denominata</span><span class="sxs-lookup"><span data-stu-id="4c775-133">named</span></span> |
| <span data-ttu-id="4c775-134">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="4c775-134">Default value</span></span> |<span data-ttu-id="4c775-135">nessuno</span><span class="sxs-lookup"><span data-stu-id="4c775-135">none</span></span> |
| <span data-ttu-id="4c775-136">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="4c775-136">Accept pipeline input?</span></span> |<span data-ttu-id="4c775-137">false</span><span class="sxs-lookup"><span data-stu-id="4c775-137">false</span></span> |
| <span data-ttu-id="4c775-138">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="4c775-138">Accept wildcard characters?</span></span> |<span data-ttu-id="4c775-139">false</span><span class="sxs-lookup"><span data-stu-id="4c775-139">false</span></span> |

## <a name="webdeploypackage"></a><span data-ttu-id="4c775-140">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="4c775-140">WebDeployPackage</span></span>
<span data-ttu-id="4c775-141">Hello percorso toohello web pacchetto toopublish toohello sito Web di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4c775-141">hello path toohello web deployment package toopublish toohello website.</span></span> <span data-ttu-id="4c775-142">È possibile creare il pacchetto utilizzando la procedura guidata pubblica Web hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4c775-142">You can create this package by using hello Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="4c775-143">Per ulteriori informazioni, vedere [Introduzione a Servizi cloud di Azure e ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span><span class="sxs-lookup"><span data-stu-id="4c775-143">For more information, see [Get started with Azure Cloud Services and ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span></span>

| <span data-ttu-id="4c775-144">Parametro</span><span class="sxs-lookup"><span data-stu-id="4c775-144">Parameter</span></span> | <span data-ttu-id="4c775-145">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="4c775-145">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="4c775-146">Alias</span><span class="sxs-lookup"><span data-stu-id="4c775-146">Aliases</span></span> |<span data-ttu-id="4c775-147">nessuno</span><span class="sxs-lookup"><span data-stu-id="4c775-147">none</span></span> |
| <span data-ttu-id="4c775-148">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="4c775-148">Required?</span></span> |<span data-ttu-id="4c775-149">false</span><span class="sxs-lookup"><span data-stu-id="4c775-149">false</span></span> |
| <span data-ttu-id="4c775-150">Posizione</span><span class="sxs-lookup"><span data-stu-id="4c775-150">Position</span></span> |<span data-ttu-id="4c775-151">denominata</span><span class="sxs-lookup"><span data-stu-id="4c775-151">named</span></span> |
| <span data-ttu-id="4c775-152">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="4c775-152">Default value</span></span> |<span data-ttu-id="4c775-153">nessuno</span><span class="sxs-lookup"><span data-stu-id="4c775-153">none</span></span> |
| <span data-ttu-id="4c775-154">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="4c775-154">Accept pipeline input?</span></span> |<span data-ttu-id="4c775-155">false</span><span class="sxs-lookup"><span data-stu-id="4c775-155">false</span></span> |
| <span data-ttu-id="4c775-156">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="4c775-156">Accept wildcard characters?</span></span> |<span data-ttu-id="4c775-157">false</span><span class="sxs-lookup"><span data-stu-id="4c775-157">false</span></span> |

## <a name="databaseserverpassword"></a><span data-ttu-id="4c775-158">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="4c775-158">DatabaseServerPassword</span></span>
<span data-ttu-id="4c775-159">Hello username e password per il database SQL di hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="4c775-159">hello username and password for hello SQL database in Azure.</span></span>

| <span data-ttu-id="4c775-160">.</span><span class="sxs-lookup"><span data-stu-id="4c775-160">Parameter</span></span> | <span data-ttu-id="4c775-161">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="4c775-161">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="4c775-162">Alias</span><span class="sxs-lookup"><span data-stu-id="4c775-162">Aliases</span></span> |<span data-ttu-id="4c775-163">nessuno</span><span class="sxs-lookup"><span data-stu-id="4c775-163">none</span></span> |
| <span data-ttu-id="4c775-164">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="4c775-164">Required?</span></span> |<span data-ttu-id="4c775-165">false</span><span class="sxs-lookup"><span data-stu-id="4c775-165">false</span></span> |
| <span data-ttu-id="4c775-166">Posizione</span><span class="sxs-lookup"><span data-stu-id="4c775-166">Position</span></span> |<span data-ttu-id="4c775-167">denominata</span><span class="sxs-lookup"><span data-stu-id="4c775-167">named</span></span> |
| <span data-ttu-id="4c775-168">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="4c775-168">Default value</span></span> |<span data-ttu-id="4c775-169">nessuno</span><span class="sxs-lookup"><span data-stu-id="4c775-169">none</span></span> |
| <span data-ttu-id="4c775-170">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="4c775-170">Accept pipeline input?</span></span> |<span data-ttu-id="4c775-171">false</span><span class="sxs-lookup"><span data-stu-id="4c775-171">false</span></span> |
| <span data-ttu-id="4c775-172">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="4c775-172">Accept wildcard characters?</span></span> |<span data-ttu-id="4c775-173">false</span><span class="sxs-lookup"><span data-stu-id="4c775-173">false</span></span> |

## <a name="sendhostmessagestooutput"></a><span data-ttu-id="4c775-174">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="4c775-174">SendHostMessagesToOutput</span></span>
<span data-ttu-id="4c775-175">Se true, i messaggi di stampanti da hello script toohello flusso di output.</span><span class="sxs-lookup"><span data-stu-id="4c775-175">If true, print messages from hello script toohello output stream.</span></span>

| <span data-ttu-id="4c775-176">.</span><span class="sxs-lookup"><span data-stu-id="4c775-176">Parameter</span></span> | <span data-ttu-id="4c775-177">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="4c775-177">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="4c775-178">Alias</span><span class="sxs-lookup"><span data-stu-id="4c775-178">Aliases</span></span> |<span data-ttu-id="4c775-179">nessuno</span><span class="sxs-lookup"><span data-stu-id="4c775-179">none</span></span> |
| <span data-ttu-id="4c775-180">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="4c775-180">Required?</span></span> |<span data-ttu-id="4c775-181">false</span><span class="sxs-lookup"><span data-stu-id="4c775-181">false</span></span> |
| <span data-ttu-id="4c775-182">Posizione</span><span class="sxs-lookup"><span data-stu-id="4c775-182">Position</span></span> |<span data-ttu-id="4c775-183">denominata</span><span class="sxs-lookup"><span data-stu-id="4c775-183">named</span></span> |
| <span data-ttu-id="4c775-184">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="4c775-184">Default value</span></span> |<span data-ttu-id="4c775-185">false</span><span class="sxs-lookup"><span data-stu-id="4c775-185">false</span></span> |
| <span data-ttu-id="4c775-186">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="4c775-186">Accept pipeline input?</span></span> |<span data-ttu-id="4c775-187">false</span><span class="sxs-lookup"><span data-stu-id="4c775-187">false</span></span> |
| <span data-ttu-id="4c775-188">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="4c775-188">Accept wildcard characters?</span></span> |<span data-ttu-id="4c775-189">false</span><span class="sxs-lookup"><span data-stu-id="4c775-189">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="4c775-190">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="4c775-190">Remarks</span></span>
<span data-ttu-id="4c775-191">Per una spiegazione completa di toouse hello script toocreate Dev e ambienti di Test, vedere [tooDev tooPublish tramite script di Windows PowerShell e gli ambienti di Test](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="4c775-191">For a complete explanation of how toouse hello script toocreate Dev and Test environments, see [Using Windows PowerShell Scripts tooPublish tooDev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="4c775-192">file di configurazione JSON Hello specifica dettagli hello novità toobe distribuito.</span><span class="sxs-lookup"><span data-stu-id="4c775-192">hello JSON configuration file specifies hello details of what is toobe deployed.</span></span> <span data-ttu-id="4c775-193">Sono incluse informazioni hello specificato al momento della creazione progetto di hello, ad esempio nome hello e il nome utente per il sito Web di hello.</span><span class="sxs-lookup"><span data-stu-id="4c775-193">It includes hello information that you specified when you created hello project, such as hello name and username for hello website.</span></span> <span data-ttu-id="4c775-194">Include inoltre tooprovision database hello, se presente.</span><span class="sxs-lookup"><span data-stu-id="4c775-194">It also includes hello database tooprovision, if any.</span></span> <span data-ttu-id="4c775-195">Hello di codice seguente viene illustrato un file di configurazione JSON di esempio:</span><span class="sxs-lookup"><span data-stu-id="4c775-195">hello following code shows an example JSON configuration file:</span></span>

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

<span data-ttu-id="4c775-196">È possibile modificare i file hello JSON configurazione toochange con gli elementi da distribuire.</span><span class="sxs-lookup"><span data-stu-id="4c775-196">You can edit hello JSON configuration file toochange what is deployed.</span></span> <span data-ttu-id="4c775-197">Una sezione del sito Web è necessaria, ma hello database sezione è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="4c775-197">A webSite section is required, but hello database section is optional.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c775-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4c775-198">Next steps</span></span>
<span data-ttu-id="4c775-199">Per ulteriori informazioni, vedere [Publish-WebApplicationVM (script di Windows PowerShell)](vs-azure-tools-publish-webapplicationvm.md)</span><span class="sxs-lookup"><span data-stu-id="4c775-199">For more information, see [Publish-WebApplicationVM (Windows PowerShell script)](vs-azure-tools-publish-webapplicationvm.md)</span></span>

