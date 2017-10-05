---
title: Publish-WebApplicationVM | Documentazione Microsoft
description: Informazioni su come distribuire un'applicazione Web in una macchina virtuale. Se non sono presenti, lo script crea le risorse necessarie nella sottoscrizione di Azure.
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
ms.openlocfilehash: 2738fc1dff50a177a227ae2c7719bd9a192d82ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a><span data-ttu-id="6b567-104">Publish-WebApplicationVM (Windows PowerShell script)</span><span class="sxs-lookup"><span data-stu-id="6b567-104">Publish-WebApplicationVM (Windows PowerShell script)</span></span>
<span data-ttu-id="6b567-105">Consente di distribuire un'applicazione Web in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b567-105">Deploys a web application to a virtual machine.</span></span> <span data-ttu-id="6b567-106">Se non sono presenti, lo script crea le risorse necessarie nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6b567-106">The script creates the required resources in your Azure subscription if they don't exist.</span></span>

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

### <a name="configuration"></a><span data-ttu-id="6b567-107">Configurazione</span><span class="sxs-lookup"><span data-stu-id="6b567-107">Configuration</span></span>
<span data-ttu-id="6b567-108">Percorso del file di configurazione JSON che descrive i dettagli della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="6b567-108">The path to the JSON configuration file that describes the details of the deployment.</span></span>

| <span data-ttu-id="6b567-109">Alias</span><span class="sxs-lookup"><span data-stu-id="6b567-109">Aliases</span></span> | <span data-ttu-id="6b567-110">nessuno</span><span class="sxs-lookup"><span data-stu-id="6b567-110">none</span></span> |
| --- | --- |
| <span data-ttu-id="6b567-111">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="6b567-111">Required?</span></span> |<span data-ttu-id="6b567-112">true</span><span class="sxs-lookup"><span data-stu-id="6b567-112">true</span></span> |
| <span data-ttu-id="6b567-113">Posizione</span><span class="sxs-lookup"><span data-stu-id="6b567-113">Position</span></span> |<span data-ttu-id="6b567-114">denominata</span><span class="sxs-lookup"><span data-stu-id="6b567-114">named</span></span> |
| <span data-ttu-id="6b567-115">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="6b567-115">Default value</span></span> |<span data-ttu-id="6b567-116">nessuno</span><span class="sxs-lookup"><span data-stu-id="6b567-116">none</span></span> |
| <span data-ttu-id="6b567-117">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="6b567-117">Accept pipeline input?</span></span> |<span data-ttu-id="6b567-118">false</span><span class="sxs-lookup"><span data-stu-id="6b567-118">false</span></span> |
| <span data-ttu-id="6b567-119">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="6b567-119">Accept wildcard characters?</span></span> |<span data-ttu-id="6b567-120">false</span><span class="sxs-lookup"><span data-stu-id="6b567-120">false</span></span> |

### <a name="subscriptionname"></a><span data-ttu-id="6b567-121">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="6b567-121">SubscriptionName</span></span>
<span data-ttu-id="6b567-122">Nome della sottoscrizione di Azure in cui creare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b567-122">The name of the Azure subscription in which you want to create the virtual machine.</span></span>

| <span data-ttu-id="6b567-123">Alias</span><span class="sxs-lookup"><span data-stu-id="6b567-123">Aliases</span></span> | <span data-ttu-id="6b567-124">nessuno</span><span class="sxs-lookup"><span data-stu-id="6b567-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="6b567-125">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="6b567-125">Required?</span></span> |<span data-ttu-id="6b567-126">false</span><span class="sxs-lookup"><span data-stu-id="6b567-126">false</span></span> |
| <span data-ttu-id="6b567-127">Posizione</span><span class="sxs-lookup"><span data-stu-id="6b567-127">Position</span></span> |<span data-ttu-id="6b567-128">denominata</span><span class="sxs-lookup"><span data-stu-id="6b567-128">named</span></span> |
| <span data-ttu-id="6b567-129">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="6b567-129">Default value</span></span> |<span data-ttu-id="6b567-130">Usa la prima sottoscrizione nel file di sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="6b567-130">Uses the first subscription in the subscription file</span></span> |
| <span data-ttu-id="6b567-131">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="6b567-131">Accept pipeline input?</span></span> |<span data-ttu-id="6b567-132">false</span><span class="sxs-lookup"><span data-stu-id="6b567-132">false</span></span> |
| <span data-ttu-id="6b567-133">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="6b567-133">Accept wildcard characters?</span></span> |<span data-ttu-id="6b567-134">false</span><span class="sxs-lookup"><span data-stu-id="6b567-134">false</span></span> |

### <a name="webdeploypackage"></a><span data-ttu-id="6b567-135">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="6b567-135">WebDeployPackage</span></span>
<span data-ttu-id="6b567-136">Percorso al pacchetto di distribuzione Web da pubblicare nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b567-136">The path to the web deployment package to publish to the virtual machine.</span></span> <span data-ttu-id="6b567-137">È possibile creare questo pacchetto usando la pubblicazione Web guidata di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6b567-137">You can create this package by using the Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="6b567-138">Vedere [Procedura: Creare un pacchetto di distribuzione Web in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b567-138">See [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span>

| <span data-ttu-id="6b567-139">Alias</span><span class="sxs-lookup"><span data-stu-id="6b567-139">Aliases</span></span> | <span data-ttu-id="6b567-140">nessuno</span><span class="sxs-lookup"><span data-stu-id="6b567-140">none</span></span> |
| --- | --- |
| <span data-ttu-id="6b567-141">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="6b567-141">Required?</span></span> |<span data-ttu-id="6b567-142">false</span><span class="sxs-lookup"><span data-stu-id="6b567-142">false</span></span> |
| <span data-ttu-id="6b567-143">Posizione</span><span class="sxs-lookup"><span data-stu-id="6b567-143">Position</span></span> |<span data-ttu-id="6b567-144">denominata</span><span class="sxs-lookup"><span data-stu-id="6b567-144">named</span></span> |
| <span data-ttu-id="6b567-145">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="6b567-145">Default value</span></span> |<span data-ttu-id="6b567-146">nessuno</span><span class="sxs-lookup"><span data-stu-id="6b567-146">none</span></span> |
| <span data-ttu-id="6b567-147">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="6b567-147">Accept pipeline input?</span></span> |<span data-ttu-id="6b567-148">false</span><span class="sxs-lookup"><span data-stu-id="6b567-148">false</span></span> |
| <span data-ttu-id="6b567-149">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="6b567-149">Accept wildcard characters?</span></span> |<span data-ttu-id="6b567-150">false</span><span class="sxs-lookup"><span data-stu-id="6b567-150">false</span></span> |

### <a name="allowuntrusted"></a><span data-ttu-id="6b567-151">AllowUntrusted</span><span class="sxs-lookup"><span data-stu-id="6b567-151">AllowUntrusted</span></span>
<span data-ttu-id="6b567-152">Se true, consente l'utilizzo di certificati che non sono firmati da un'autorità radice attendibile.</span><span class="sxs-lookup"><span data-stu-id="6b567-152">If true, allow the use of certificates that aren't signed by a trusted root authority.</span></span>

| <span data-ttu-id="6b567-153">Alias</span><span class="sxs-lookup"><span data-stu-id="6b567-153">Aliases</span></span> | <span data-ttu-id="6b567-154">nessuno</span><span class="sxs-lookup"><span data-stu-id="6b567-154">none</span></span> |
| --- | --- |
| <span data-ttu-id="6b567-155">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="6b567-155">Required?</span></span> |<span data-ttu-id="6b567-156">false</span><span class="sxs-lookup"><span data-stu-id="6b567-156">false</span></span> |
| <span data-ttu-id="6b567-157">Posizione</span><span class="sxs-lookup"><span data-stu-id="6b567-157">Position</span></span> |<span data-ttu-id="6b567-158">denominata</span><span class="sxs-lookup"><span data-stu-id="6b567-158">named</span></span> |
| <span data-ttu-id="6b567-159">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="6b567-159">Default value</span></span> |<span data-ttu-id="6b567-160">false</span><span class="sxs-lookup"><span data-stu-id="6b567-160">false</span></span> |
| <span data-ttu-id="6b567-161">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="6b567-161">Accept pipeline input?</span></span> |<span data-ttu-id="6b567-162">false</span><span class="sxs-lookup"><span data-stu-id="6b567-162">false</span></span> |
| <span data-ttu-id="6b567-163">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="6b567-163">Accept wildcard characters?</span></span> |<span data-ttu-id="6b567-164">false</span><span class="sxs-lookup"><span data-stu-id="6b567-164">false</span></span> |

### <a name="vmpassword"></a><span data-ttu-id="6b567-165">VMPassword</span><span class="sxs-lookup"><span data-stu-id="6b567-165">VMPassword</span></span>
<span data-ttu-id="6b567-166">Le credenziali per l'account della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b567-166">The credentials for the virtual machine account.</span></span> <span data-ttu-id="6b567-167">Esempio: - VMPassword @{nome = "admin"; Password = "password"}</span><span class="sxs-lookup"><span data-stu-id="6b567-167">Example: -VMPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="6b567-168">Alias</span><span class="sxs-lookup"><span data-stu-id="6b567-168">Aliases</span></span> | <span data-ttu-id="6b567-169">nessuno</span><span class="sxs-lookup"><span data-stu-id="6b567-169">none</span></span> |
| --- | --- |
| <span data-ttu-id="6b567-170">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="6b567-170">Required?</span></span> |<span data-ttu-id="6b567-171">false</span><span class="sxs-lookup"><span data-stu-id="6b567-171">false</span></span> |
| <span data-ttu-id="6b567-172">Posizione</span><span class="sxs-lookup"><span data-stu-id="6b567-172">Position</span></span> |<span data-ttu-id="6b567-173">denominata</span><span class="sxs-lookup"><span data-stu-id="6b567-173">named</span></span> |
| <span data-ttu-id="6b567-174">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="6b567-174">Default value</span></span> |<span data-ttu-id="6b567-175">nessuno</span><span class="sxs-lookup"><span data-stu-id="6b567-175">none</span></span> |
| <span data-ttu-id="6b567-176">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="6b567-176">Accept pipeline input?</span></span> |<span data-ttu-id="6b567-177">false</span><span class="sxs-lookup"><span data-stu-id="6b567-177">false</span></span> |
| <span data-ttu-id="6b567-178">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="6b567-178">Accept wildcard characters?</span></span> |<span data-ttu-id="6b567-179">false</span><span class="sxs-lookup"><span data-stu-id="6b567-179">false</span></span> |

### <a name="databaseserverpassword"></a><span data-ttu-id="6b567-180">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="6b567-180">DatabaseServerPassword</span></span>
<span data-ttu-id="6b567-181">Le credenziali del database SQL in Azure.</span><span class="sxs-lookup"><span data-stu-id="6b567-181">The credentials for the SQL database in Azure.</span></span> <span data-ttu-id="6b567-182">Esempio: - DatabaseServerPassword @{nome = "admin"; Password = "password"}</span><span class="sxs-lookup"><span data-stu-id="6b567-182">Example: -DatabaseServerPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="6b567-183">Alias</span><span class="sxs-lookup"><span data-stu-id="6b567-183">Aliases</span></span> | <span data-ttu-id="6b567-184">nessuno</span><span class="sxs-lookup"><span data-stu-id="6b567-184">none</span></span> |
| --- | --- |
| <span data-ttu-id="6b567-185">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="6b567-185">Required?</span></span> |<span data-ttu-id="6b567-186">false</span><span class="sxs-lookup"><span data-stu-id="6b567-186">false</span></span> |
| <span data-ttu-id="6b567-187">Posizione</span><span class="sxs-lookup"><span data-stu-id="6b567-187">Position</span></span> |<span data-ttu-id="6b567-188">denominata</span><span class="sxs-lookup"><span data-stu-id="6b567-188">named</span></span> |
| <span data-ttu-id="6b567-189">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="6b567-189">Default value</span></span> |<span data-ttu-id="6b567-190">nessuno</span><span class="sxs-lookup"><span data-stu-id="6b567-190">none</span></span> |
| <span data-ttu-id="6b567-191">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="6b567-191">Accept pipeline input?</span></span> |<span data-ttu-id="6b567-192">false</span><span class="sxs-lookup"><span data-stu-id="6b567-192">false</span></span> |
| <span data-ttu-id="6b567-193">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="6b567-193">Accept wildcard characters?</span></span> |<span data-ttu-id="6b567-194">false</span><span class="sxs-lookup"><span data-stu-id="6b567-194">false</span></span> |

### <a name="sendhostmessagestooutput"></a><span data-ttu-id="6b567-195">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="6b567-195">SendHostMessagesToOutput</span></span>
<span data-ttu-id="6b567-196">Se impostato su true, stampa i messaggi dallo script al flusso di output.</span><span class="sxs-lookup"><span data-stu-id="6b567-196">If true, print messages from the script to the output stream.</span></span>

| <span data-ttu-id="6b567-197">Alias</span><span class="sxs-lookup"><span data-stu-id="6b567-197">Aliases</span></span> | <span data-ttu-id="6b567-198">nessuno</span><span class="sxs-lookup"><span data-stu-id="6b567-198">none</span></span> |
| --- | --- |
| <span data-ttu-id="6b567-199">Obbligatorio?</span><span class="sxs-lookup"><span data-stu-id="6b567-199">Required?</span></span> |<span data-ttu-id="6b567-200">false</span><span class="sxs-lookup"><span data-stu-id="6b567-200">false</span></span> |
| <span data-ttu-id="6b567-201">Posizione</span><span class="sxs-lookup"><span data-stu-id="6b567-201">Position</span></span> |<span data-ttu-id="6b567-202">denominata</span><span class="sxs-lookup"><span data-stu-id="6b567-202">named</span></span> |
| <span data-ttu-id="6b567-203">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="6b567-203">Default value</span></span> |<span data-ttu-id="6b567-204">false</span><span class="sxs-lookup"><span data-stu-id="6b567-204">false</span></span> |
| <span data-ttu-id="6b567-205">Input pipeline accettato?</span><span class="sxs-lookup"><span data-stu-id="6b567-205">Accept pipeline input?</span></span> |<span data-ttu-id="6b567-206">false</span><span class="sxs-lookup"><span data-stu-id="6b567-206">false</span></span> |
| <span data-ttu-id="6b567-207">Caratteri jolly accettati?</span><span class="sxs-lookup"><span data-stu-id="6b567-207">Accept wildcard characters?</span></span> |<span data-ttu-id="6b567-208">false</span><span class="sxs-lookup"><span data-stu-id="6b567-208">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="6b567-209">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="6b567-209">Remarks</span></span>
<span data-ttu-id="6b567-210">Per una spiegazione completa sull'uso dello script per creare ambienti di sviluppo e test, vedere [Uso degli script di Windows PowerShell per la pubblicazione in ambienti di sviluppo e test](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="6b567-210">For a complete explanation of how to use the script to create Dev and Test environments, see [Using Windows PowerShell Scripts to Publish to Dev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="6b567-211">Il file di configurazione JSON specifica i dettagli degli elementi da distribuire.</span><span class="sxs-lookup"><span data-stu-id="6b567-211">The JSON configuration file specifies the details of what is to be deployed.</span></span> <span data-ttu-id="6b567-212">Include le informazioni specificate al momento della creazione del progetto, ad esempio il nome, il set di affinità, l’immagine VHD e la dimensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b567-212">It includes the information that you specified when you created the project, such as the name, affinity group, VHD image, and size of the virtual machine.</span></span> <span data-ttu-id="6b567-213">Inoltre include gli endpoint nella macchina virtuale, i database per eseguire il provisioning, se presente, e i parametri di distribuzione Web.</span><span class="sxs-lookup"><span data-stu-id="6b567-213">It also includes the endpoints on the virtual machine, the databases to provision, if any, and web deployment parameters.</span></span> <span data-ttu-id="6b567-214">Il codice seguente mostra un esempio di file di configurazione JSON:</span><span class="sxs-lookup"><span data-stu-id="6b567-214">The following code shows an example JSON configuration file:</span></span>

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

<span data-ttu-id="6b567-215">È possibile modificare il file di configurazione JSON per cambiare gli elementi del provisioning.</span><span class="sxs-lookup"><span data-stu-id="6b567-215">You can edit the JSON configuration file to change what is provisioned.</span></span> <span data-ttu-id="6b567-216">Una macchina virtuale e un servizio cloud sono necessari, ma la sezione del database è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="6b567-216">A virtual machine and a cloud service are required, but the database section is optional.</span></span>

