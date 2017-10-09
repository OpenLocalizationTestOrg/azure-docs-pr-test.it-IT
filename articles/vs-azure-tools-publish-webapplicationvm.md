---
title: aaaPublish-WebApplicationVM | Documenti Microsoft
description: Informazioni su come toodeploy una macchina virtuale del tooa applicazioni web. In caso contrario, questo script crea le risorse necessarie hello nella sottoscrizione di Azure.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: e4b52b620bebf44b87ddfc3b19c155bb65111814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a><span data-ttu-id="67f44-104">Publish-WebApplicationVM (Windows PowerShell script)</span><span class="sxs-lookup"><span data-stu-id="67f44-104">Publish-WebApplicationVM (Windows PowerShell script)</span></span>
<span data-ttu-id="67f44-105">Consente di distribuire una macchina virtuale del tooa applicazioni web.</span><span class="sxs-lookup"><span data-stu-id="67f44-105">Deploys a web application tooa virtual machine.</span></span> <span data-ttu-id="67f44-106">script di Hello crea risorse hello necessarie nella sottoscrizione di Azure, se non sono presenti.</span><span class="sxs-lookup"><span data-stu-id="67f44-106">hello script creates hello required resources in your Azure subscription if they don't exist.</span></span>

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a><span data-ttu-id="67f44-107">Configurazione</span><span class="sxs-lookup"><span data-stu-id="67f44-107">Configuration</span></span>
<span data-ttu-id="67f44-108">Hello percorso toohello file di configurazione JSON che descrive i dettagli di hello della distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="67f44-108">hello path toohello JSON configuration file that describes hello details of hello deployment.</span></span>

| <span data-ttu-id="67f44-109">Alias</span><span class="sxs-lookup"><span data-stu-id="67f44-109">Aliases</span></span> | <span data-ttu-id="67f44-110">nessuno</span><span class="sxs-lookup"><span data-stu-id="67f44-110">none</span></span> |
| --- | --- |
| <span data-ttu-id="67f44-111">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="67f44-111">Required?</span></span> |<span data-ttu-id="67f44-112">true</span><span class="sxs-lookup"><span data-stu-id="67f44-112">true</span></span> |
| <span data-ttu-id="67f44-113">Posizione</span><span class="sxs-lookup"><span data-stu-id="67f44-113">Position</span></span> |<span data-ttu-id="67f44-114">denominata</span><span class="sxs-lookup"><span data-stu-id="67f44-114">named</span></span> |
| <span data-ttu-id="67f44-115">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="67f44-115">Default value</span></span> |<span data-ttu-id="67f44-116">nessuno</span><span class="sxs-lookup"><span data-stu-id="67f44-116">none</span></span> |
| <span data-ttu-id="67f44-117">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="67f44-117">Accept pipeline input?</span></span> |<span data-ttu-id="67f44-118">false</span><span class="sxs-lookup"><span data-stu-id="67f44-118">false</span></span> |
| <span data-ttu-id="67f44-119">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="67f44-119">Accept wildcard characters?</span></span> |<span data-ttu-id="67f44-120">false</span><span class="sxs-lookup"><span data-stu-id="67f44-120">false</span></span> |

### <a name="subscriptionname"></a><span data-ttu-id="67f44-121">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="67f44-121">SubscriptionName</span></span>
<span data-ttu-id="67f44-122">nome Hello di hello sottoscrizione di Azure in cui si desidera macchina virtuale di toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="67f44-122">hello name of hello Azure subscription in which you want toocreate hello virtual machine.</span></span>

| <span data-ttu-id="67f44-123">Alias</span><span class="sxs-lookup"><span data-stu-id="67f44-123">Aliases</span></span> | <span data-ttu-id="67f44-124">nessuno</span><span class="sxs-lookup"><span data-stu-id="67f44-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="67f44-125">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="67f44-125">Required?</span></span> |<span data-ttu-id="67f44-126">false</span><span class="sxs-lookup"><span data-stu-id="67f44-126">false</span></span> |
| <span data-ttu-id="67f44-127">Posizione</span><span class="sxs-lookup"><span data-stu-id="67f44-127">Position</span></span> |<span data-ttu-id="67f44-128">denominata</span><span class="sxs-lookup"><span data-stu-id="67f44-128">named</span></span> |
| <span data-ttu-id="67f44-129">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="67f44-129">Default value</span></span> |<span data-ttu-id="67f44-130">Usa prima sottoscrizione hello nel file di sottoscrizione hello</span><span class="sxs-lookup"><span data-stu-id="67f44-130">Uses hello first subscription in hello subscription file</span></span> |
| <span data-ttu-id="67f44-131">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="67f44-131">Accept pipeline input?</span></span> |<span data-ttu-id="67f44-132">false</span><span class="sxs-lookup"><span data-stu-id="67f44-132">false</span></span> |
| <span data-ttu-id="67f44-133">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="67f44-133">Accept wildcard characters?</span></span> |<span data-ttu-id="67f44-134">false</span><span class="sxs-lookup"><span data-stu-id="67f44-134">false</span></span> |

### <a name="webdeploypackage"></a><span data-ttu-id="67f44-135">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="67f44-135">WebDeployPackage</span></span>
<span data-ttu-id="67f44-136">Hello percorso toohello web distribuzione pacchetto toopublish toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="67f44-136">hello path toohello web deployment package toopublish toohello virtual machine.</span></span> <span data-ttu-id="67f44-137">È possibile creare il pacchetto utilizzando la procedura guidata pubblica Web hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="67f44-137">You can create this package by using hello Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="67f44-138">Vedere [Procedura: Creare un pacchetto di distribuzione Web in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="67f44-138">See [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span>

| <span data-ttu-id="67f44-139">Alias</span><span class="sxs-lookup"><span data-stu-id="67f44-139">Aliases</span></span> | <span data-ttu-id="67f44-140">nessuno</span><span class="sxs-lookup"><span data-stu-id="67f44-140">none</span></span> |
| --- | --- |
| <span data-ttu-id="67f44-141">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="67f44-141">Required?</span></span> |<span data-ttu-id="67f44-142">false</span><span class="sxs-lookup"><span data-stu-id="67f44-142">false</span></span> |
| <span data-ttu-id="67f44-143">Posizione</span><span class="sxs-lookup"><span data-stu-id="67f44-143">Position</span></span> |<span data-ttu-id="67f44-144">denominata</span><span class="sxs-lookup"><span data-stu-id="67f44-144">named</span></span> |
| <span data-ttu-id="67f44-145">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="67f44-145">Default value</span></span> |<span data-ttu-id="67f44-146">nessuno</span><span class="sxs-lookup"><span data-stu-id="67f44-146">none</span></span> |
| <span data-ttu-id="67f44-147">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="67f44-147">Accept pipeline input?</span></span> |<span data-ttu-id="67f44-148">false</span><span class="sxs-lookup"><span data-stu-id="67f44-148">false</span></span> |
| <span data-ttu-id="67f44-149">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="67f44-149">Accept wildcard characters?</span></span> |<span data-ttu-id="67f44-150">false</span><span class="sxs-lookup"><span data-stu-id="67f44-150">false</span></span> |

### <a name="allowuntrusted"></a><span data-ttu-id="67f44-151">AllowUntrusted</span><span class="sxs-lookup"><span data-stu-id="67f44-151">AllowUntrusted</span></span>
<span data-ttu-id="67f44-152">Se true, consente l'uso di hello di certificati che non sono firmati da un'autorità radice attendibile.</span><span class="sxs-lookup"><span data-stu-id="67f44-152">If true, allow hello use of certificates that aren't signed by a trusted root authority.</span></span>

| <span data-ttu-id="67f44-153">Alias</span><span class="sxs-lookup"><span data-stu-id="67f44-153">Aliases</span></span> | <span data-ttu-id="67f44-154">nessuno</span><span class="sxs-lookup"><span data-stu-id="67f44-154">none</span></span> |
| --- | --- |
| <span data-ttu-id="67f44-155">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="67f44-155">Required?</span></span> |<span data-ttu-id="67f44-156">false</span><span class="sxs-lookup"><span data-stu-id="67f44-156">false</span></span> |
| <span data-ttu-id="67f44-157">Posizione</span><span class="sxs-lookup"><span data-stu-id="67f44-157">Position</span></span> |<span data-ttu-id="67f44-158">denominata</span><span class="sxs-lookup"><span data-stu-id="67f44-158">named</span></span> |
| <span data-ttu-id="67f44-159">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="67f44-159">Default value</span></span> |<span data-ttu-id="67f44-160">false</span><span class="sxs-lookup"><span data-stu-id="67f44-160">false</span></span> |
| <span data-ttu-id="67f44-161">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="67f44-161">Accept pipeline input?</span></span> |<span data-ttu-id="67f44-162">false</span><span class="sxs-lookup"><span data-stu-id="67f44-162">false</span></span> |
| <span data-ttu-id="67f44-163">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="67f44-163">Accept wildcard characters?</span></span> |<span data-ttu-id="67f44-164">false</span><span class="sxs-lookup"><span data-stu-id="67f44-164">false</span></span> |

### <a name="vmpassword"></a><span data-ttu-id="67f44-165">VMPassword</span><span class="sxs-lookup"><span data-stu-id="67f44-165">VMPassword</span></span>
<span data-ttu-id="67f44-166">credenziali di Hello per l'account della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="67f44-166">hello credentials for hello virtual machine account.</span></span> <span data-ttu-id="67f44-167">Esempio: - VMPassword @{nome = "admin"; Password = "password"}</span><span class="sxs-lookup"><span data-stu-id="67f44-167">Example: -VMPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="67f44-168">Alias</span><span class="sxs-lookup"><span data-stu-id="67f44-168">Aliases</span></span> | <span data-ttu-id="67f44-169">nessuno</span><span class="sxs-lookup"><span data-stu-id="67f44-169">none</span></span> |
| --- | --- |
| <span data-ttu-id="67f44-170">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="67f44-170">Required?</span></span> |<span data-ttu-id="67f44-171">false</span><span class="sxs-lookup"><span data-stu-id="67f44-171">false</span></span> |
| <span data-ttu-id="67f44-172">Posizione</span><span class="sxs-lookup"><span data-stu-id="67f44-172">Position</span></span> |<span data-ttu-id="67f44-173">denominata</span><span class="sxs-lookup"><span data-stu-id="67f44-173">named</span></span> |
| <span data-ttu-id="67f44-174">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="67f44-174">Default value</span></span> |<span data-ttu-id="67f44-175">nessuno</span><span class="sxs-lookup"><span data-stu-id="67f44-175">none</span></span> |
| <span data-ttu-id="67f44-176">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="67f44-176">Accept pipeline input?</span></span> |<span data-ttu-id="67f44-177">false</span><span class="sxs-lookup"><span data-stu-id="67f44-177">false</span></span> |
| <span data-ttu-id="67f44-178">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="67f44-178">Accept wildcard characters?</span></span> |<span data-ttu-id="67f44-179">false</span><span class="sxs-lookup"><span data-stu-id="67f44-179">false</span></span> |

### <a name="databaseserverpassword"></a><span data-ttu-id="67f44-180">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="67f44-180">DatabaseServerPassword</span></span>
<span data-ttu-id="67f44-181">credenziali Hello per il database SQL di hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="67f44-181">hello credentials for hello SQL database in Azure.</span></span> <span data-ttu-id="67f44-182">Esempio: - DatabaseServerPassword @{nome = "admin"; Password = "password"}</span><span class="sxs-lookup"><span data-stu-id="67f44-182">Example: -DatabaseServerPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="67f44-183">Alias</span><span class="sxs-lookup"><span data-stu-id="67f44-183">Aliases</span></span> | <span data-ttu-id="67f44-184">nessuno</span><span class="sxs-lookup"><span data-stu-id="67f44-184">none</span></span> |
| --- | --- |
| <span data-ttu-id="67f44-185">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="67f44-185">Required?</span></span> |<span data-ttu-id="67f44-186">false</span><span class="sxs-lookup"><span data-stu-id="67f44-186">false</span></span> |
| <span data-ttu-id="67f44-187">Posizione</span><span class="sxs-lookup"><span data-stu-id="67f44-187">Position</span></span> |<span data-ttu-id="67f44-188">denominata</span><span class="sxs-lookup"><span data-stu-id="67f44-188">named</span></span> |
| <span data-ttu-id="67f44-189">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="67f44-189">Default value</span></span> |<span data-ttu-id="67f44-190">nessuno</span><span class="sxs-lookup"><span data-stu-id="67f44-190">none</span></span> |
| <span data-ttu-id="67f44-191">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="67f44-191">Accept pipeline input?</span></span> |<span data-ttu-id="67f44-192">false</span><span class="sxs-lookup"><span data-stu-id="67f44-192">false</span></span> |
| <span data-ttu-id="67f44-193">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="67f44-193">Accept wildcard characters?</span></span> |<span data-ttu-id="67f44-194">false</span><span class="sxs-lookup"><span data-stu-id="67f44-194">false</span></span> |

### <a name="sendhostmessagestooutput"></a><span data-ttu-id="67f44-195">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="67f44-195">SendHostMessagesToOutput</span></span>
<span data-ttu-id="67f44-196">Se true, i messaggi di stampanti da hello script toohello flusso di output.</span><span class="sxs-lookup"><span data-stu-id="67f44-196">If true, print messages from hello script toohello output stream.</span></span>

| <span data-ttu-id="67f44-197">Alias</span><span class="sxs-lookup"><span data-stu-id="67f44-197">Aliases</span></span> | <span data-ttu-id="67f44-198">nessuno</span><span class="sxs-lookup"><span data-stu-id="67f44-198">none</span></span> |
| --- | --- |
| <span data-ttu-id="67f44-199">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="67f44-199">Required?</span></span> |<span data-ttu-id="67f44-200">false</span><span class="sxs-lookup"><span data-stu-id="67f44-200">false</span></span> |
| <span data-ttu-id="67f44-201">Posizione</span><span class="sxs-lookup"><span data-stu-id="67f44-201">Position</span></span> |<span data-ttu-id="67f44-202">denominata</span><span class="sxs-lookup"><span data-stu-id="67f44-202">named</span></span> |
| <span data-ttu-id="67f44-203">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="67f44-203">Default value</span></span> |<span data-ttu-id="67f44-204">false</span><span class="sxs-lookup"><span data-stu-id="67f44-204">false</span></span> |
| <span data-ttu-id="67f44-205">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="67f44-205">Accept pipeline input?</span></span> |<span data-ttu-id="67f44-206">false</span><span class="sxs-lookup"><span data-stu-id="67f44-206">false</span></span> |
| <span data-ttu-id="67f44-207">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="67f44-207">Accept wildcard characters?</span></span> |<span data-ttu-id="67f44-208">false</span><span class="sxs-lookup"><span data-stu-id="67f44-208">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="67f44-209">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="67f44-209">Remarks</span></span>
<span data-ttu-id="67f44-210">Per una spiegazione completa di toouse hello script toocreate Dev e ambienti di Test, vedere [tooDev tooPublish tramite script di Windows PowerShell e gli ambienti di Test](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="67f44-210">For a complete explanation of how toouse hello script toocreate Dev and Test environments, see [Using Windows PowerShell Scripts tooPublish tooDev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="67f44-211">file di configurazione JSON Hello specifica dettagli hello novità toobe distribuito.</span><span class="sxs-lookup"><span data-stu-id="67f44-211">hello JSON configuration file specifies hello details of what is toobe deployed.</span></span> <span data-ttu-id="67f44-212">Sono incluse informazioni hello specificato al momento della creazione progetto di hello, ad esempio nome hello, gruppo di affinità, immagine VHD e dimensioni di macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="67f44-212">It includes hello information that you specified when you created hello project, such as hello name, affinity group, VHD image, and size of hello virtual machine.</span></span> <span data-ttu-id="67f44-213">Inoltre include endpoint hello nella macchina virtuale hello hello tooprovision di database, se presente e i parametri di distribuzione web.</span><span class="sxs-lookup"><span data-stu-id="67f44-213">It also includes hello endpoints on hello virtual machine, hello databases tooprovision, if any, and web deployment parameters.</span></span> <span data-ttu-id="67f44-214">Hello di codice seguente viene illustrato un file di configurazione JSON di esempio:</span><span class="sxs-lookup"><span data-stu-id="67f44-214">hello following code shows an example JSON configuration file:</span></span>

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="67f44-215">È possibile modificare hello JSON configurazione file toochange ciò che viene eseguito il provisioning.</span><span class="sxs-lookup"><span data-stu-id="67f44-215">You can edit hello JSON configuration file toochange what is provisioned.</span></span> <span data-ttu-id="67f44-216">Una macchina virtuale e un servizio cloud sono necessarie, ma hello database sezione è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="67f44-216">A virtual machine and a cloud service are required, but hello database section is optional.</span></span>

