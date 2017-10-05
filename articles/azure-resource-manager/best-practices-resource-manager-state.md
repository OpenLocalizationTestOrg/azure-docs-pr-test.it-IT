---
title: Passare valori complessi tra modelli di Azure | Documentazione Microsoft
description: Mostra gli approcci consigliati per usare oggetti complessi per condividere i dati sullo stato con modelli di Azure Resource Manager e modelli collegati.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fd2f5e2d-d56d-4e01-a57d-34f3eaead4a9
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: tomfitz
ms.openlocfilehash: 23cc4321159a87b61c177b11381646af8bd9eb35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="share-state-to-and-from-azure-resource-manager-templates"></a><span data-ttu-id="25b1c-103">Condividere lo stato tra modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="25b1c-103">Share state to and from Azure Resource Manager templates</span></span>
<span data-ttu-id="25b1c-104">Questo argomento illustra le procedure consigliate per la gestione e la condivisione dello stato all'interno dei modelli.</span><span class="sxs-lookup"><span data-stu-id="25b1c-104">This topic shows best practices for managing and sharing state within templates.</span></span> <span data-ttu-id="25b1c-105">I parametri e le variabili illustrati in questo argomento sono esempi del tipo di oggetti che è possibile definire per organizzare facilmente i requisiti di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="25b1c-105">The parameters and variables shown in this topic are examples of the type of objects you can define to conveniently organize your deployment requirements.</span></span> <span data-ttu-id="25b1c-106">Da questi esempi, è possibile implementare gli oggetti con valori di proprietà utili per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="25b1c-106">From these examples, you can implement your own objects with property values that make sense for your environment.</span></span>

<span data-ttu-id="25b1c-107">Questo argomento fa parte di un white paper di dimensioni maggiori.</span><span class="sxs-lookup"><span data-stu-id="25b1c-107">This topic is part of a larger whitepaper.</span></span> <span data-ttu-id="25b1c-108">Per leggere il documento completo, scaricare [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf) (Considerazioni e procedure consigliate sui modelli di Resource Manager a livello internazionale).</span><span class="sxs-lookup"><span data-stu-id="25b1c-108">To read the full paper, download [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span></span>

## <a name="provide-standard-configuration-settings"></a><span data-ttu-id="25b1c-109">Uso di impostazioni di configurazione standard</span><span class="sxs-lookup"><span data-stu-id="25b1c-109">Provide standard configuration settings</span></span>
<span data-ttu-id="25b1c-110">Anziché offrire un modello che fornisce la massima flessibilità e innumerevoli varianti, un modello comune fornisce una selezione di configurazioni note.</span><span class="sxs-lookup"><span data-stu-id="25b1c-110">Rather than offer a template that provides total flexibility and countless variations, a common pattern is to provide a selection of known configurations.</span></span> <span data-ttu-id="25b1c-111">In effetti, gli utenti possono selezionare taglie standard, come sandbox, small, medium e large.</span><span class="sxs-lookup"><span data-stu-id="25b1c-111">In effect, users can select standard t-shirt sizes such as sandbox, small, medium, and large.</span></span> <span data-ttu-id="25b1c-112">Altri esempi di taglie sono le offerte di prodotti, come Community Edition o Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="25b1c-112">Other examples of t-shirt sizes are product offerings, such as community edition or enterprise edition.</span></span> <span data-ttu-id="25b1c-113">In altri casi, potrebbero essere configurazioni specifiche per i carichi di lavoro di una determinata tecnologia, ad esempio map reduce o no sql.</span><span class="sxs-lookup"><span data-stu-id="25b1c-113">In other cases, it may be workload-specific configurations of a technology – such as map reduce or no sql.</span></span>

<span data-ttu-id="25b1c-114">Con gli oggetti complessi, è possibile creare variabili che contengono insiemi di dati, talvolta note come "contenitori di proprietà" e utilizzare tali dati per guidare la dichiarazione delle risorse nel modello.</span><span class="sxs-lookup"><span data-stu-id="25b1c-114">With complex objects, you can create variables that contain collections of data, sometimes known as "property bags" and use that data to drive the resource declaration in your template.</span></span> <span data-ttu-id="25b1c-115">Questo approccio fornisce configurazioni note ed efficienti di dimensioni variabili, preconfigurate per i clienti.</span><span class="sxs-lookup"><span data-stu-id="25b1c-115">This approach provides good, known configurations of varying sizes that are preconfigured for customers.</span></span> <span data-ttu-id="25b1c-116">Senza configurazioni note, gli utenti del modello devono determinare autonomamente la dimensione del cluster, includere i limiti di risorse della piattaforma ed effettuare calcoli matematici per identificare il partizionamento risultante degli account di archiviazione e altre risorse (a causa della dimensione del cluster e dei limiti di risorse).</span><span class="sxs-lookup"><span data-stu-id="25b1c-116">Without known configurations, users of the template must determine cluster sizing on their own, factor in platform resource constraints, and do math to identify the resulting partitioning of storage accounts and other resources (due to cluster size and resource constraints).</span></span> <span data-ttu-id="25b1c-117">Oltre a migliorare l'esperienza del cliente, un numero limitato di configurazioni note è più facile da supportare e consente di offrire un livello superiore di densità.</span><span class="sxs-lookup"><span data-stu-id="25b1c-117">In addition to making a better experience for the customer, a few known configurations are easier to support and can help you deliver a higher level of density.</span></span>

<span data-ttu-id="25b1c-118">Il seguente esempio mostra come definire variabili contenenti oggetti complessi per rappresentare raccolte di dati.</span><span class="sxs-lookup"><span data-stu-id="25b1c-118">The following example shows how to define variables that contain complex objects for representing collections of data.</span></span> <span data-ttu-id="25b1c-119">Le raccolte definiscono i valori usati per le dimensioni della macchina virtuale, le impostazioni di rete, le impostazioni del sistema operativo e le impostazioni di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="25b1c-119">The collections define values that are used for virtual machine size, network settings, operating system settings and availability settings.</span></span>

    "variables": {
      "tshirtSize": "[variables(concat('tshirtSize', parameters('tshirtSize')))]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      },
      "tshirtSizeMedium": {
        "vmSize": "Standard_A3",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-8disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1],
          "jumpbox": 0
        }
      },
      "tshirtSizeLarge": {
        "vmSize": "Standard_A4",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-16disk-resources.json')]",
        "vmCount": 3,
        "slaveCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1,1],
          "jumpbox": 0
        }
      },
      "osSettings": {
        "scripts": [
          "[concat(variables('templateBaseUrl'), 'install_postgresql.sh')]",
          "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/shared_scripts/ubuntu/vm-disk-utils-0.1.sh"
        ],
        "imageReference": {
          "publisher": "Canonical",
          "offer": "UbuntuServer",
          "sku": "14.04.2-LTS",
          "version": "latest"
        }
      },
      "networkSettings": {
        "vnetName": "[parameters('virtualNetworkName')]",
        "addressPrefix": "10.0.0.0/16",
        "subnets": {
          "dmz": {
            "name": "dmz",
            "prefix": "10.0.0.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          },
          "data": {
            "name": "data",
            "prefix": "10.0.1.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          }
        }
      },
      "availabilitySetSettings": {
        "name": "pgsqlAvailabilitySet",
        "fdCount": 3,
        "udCount": 5
      }
    }

<span data-ttu-id="25b1c-120">Si noti che la variabile **tshirtSize** concatena la taglia delle t-shirt fornita tramite un parametro (**Small**, **Medium**, **Large**) al testo **tshirtSize**.</span><span class="sxs-lookup"><span data-stu-id="25b1c-120">Notice that the **tshirtSize** variable concatenates the t-shirt size you provided through a parameter (**Small**, **Medium**, **Large**) to the text **tshirtSize**.</span></span> <span data-ttu-id="25b1c-121">Questa variabile viene usata per recuperare la variabile oggetto complesso associata per questa taglia.</span><span class="sxs-lookup"><span data-stu-id="25b1c-121">You use this variable to retrieve the associated complex object variable for that t-shirt size.</span></span>

<span data-ttu-id="25b1c-122">È possibile fare riferimento a queste variabili in un secondo momento nel modello.</span><span class="sxs-lookup"><span data-stu-id="25b1c-122">You can then reference these variables later in the template.</span></span> <span data-ttu-id="25b1c-123">La possibilità di fare riferimento a variabili denominate e alle relative proprietà semplifica la sintassi del modello e semplifica la comprensione del contesto.</span><span class="sxs-lookup"><span data-stu-id="25b1c-123">The ability to reference named-variables and their properties simplifies the template syntax, and makes it easy to understand context.</span></span> <span data-ttu-id="25b1c-124">L'esempio seguente definisce una risorsa da distribuire usando gli oggetti indicati sopra per impostare i valori.</span><span class="sxs-lookup"><span data-stu-id="25b1c-124">The following example defines a resource to deploy by using the objects shown previously to set values.</span></span> <span data-ttu-id="25b1c-125">Ad esempio, le dimensioni della VM vengono impostate recuperando il valore di `variables('tshirtSize').vmSize`, mentre il valore delle dimensioni del disco viene recuperato da `variables('tshirtSize').diskSize`.</span><span class="sxs-lookup"><span data-stu-id="25b1c-125">For example, the VM size is set by retrieving the value for `variables('tshirtSize').vmSize` while the value for the disk size is retrieved from `variables('tshirtSize').diskSize`.</span></span> <span data-ttu-id="25b1c-126">Inoltre, l'URI di un modello collegato viene impostato con il valore di `variables('tshirtSize').vmTemplate`.</span><span class="sxs-lookup"><span data-stu-id="25b1c-126">In addition, the URI for a linked template is set with the value for `variables('tshirtSize').vmTemplate`.</span></span>

    "name": "master-node",
    "type": "Microsoft.Resources/deployments",
    "apiVersion": "2015-01-01",
    "dependsOn": [
        "[concat('Microsoft.Resources/deployments/', 'shared')]"
    ],
    "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[variables('tshirtSize').vmTemplate]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "value": "[parameters('adminPassword')]"
          },
          "replicatorPassword": {
            "value": "[parameters('replicatorPassword')]"
          },
          "osSettings": {
            "value": "[variables('osSettings')]"
          },
          "subnet": {
            "value": "[variables('networkSettings').subnets.data]"
          },
          "commonSettings": {
            "value": {
              "region": "[parameters('region')]",
              "adminUsername": "[parameters('adminUsername')]",
              "namespace": "ms"
            }
          },
          "storageSettings": {
            "value":"[variables('tshirtSize').storage]"
          },
          "machineSettings": {
            "value": {
              "vmSize": "[variables('tshirtSize').vmSize]",
              "diskSize": "[variables('tshirtSize').diskSize]",
              "vmCount": 1,
              "availabilitySet": "[variables('availabilitySetSettings').name]"
            }
          },
          "masterIpAddress": {
            "value": "0"
          },
          "dbType": {
            "value": "MASTER"
          }
        }
      }
    }

## <a name="pass-state-to-a-template"></a><span data-ttu-id="25b1c-127">Passaggio dello stato a un modello</span><span class="sxs-lookup"><span data-stu-id="25b1c-127">Pass state to a template</span></span>
<span data-ttu-id="25b1c-128">È possibile condividere lo stato in un modello tramite parametri forniti direttamente durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="25b1c-128">You share state into a template through parameters that you provide directly during deployment.</span></span>

<span data-ttu-id="25b1c-129">La tabella seguente elenca i parametri di uso comune nei modelli.</span><span class="sxs-lookup"><span data-stu-id="25b1c-129">The following table lists commonly used parameters in templates.</span></span>

| <span data-ttu-id="25b1c-130">Nome</span><span class="sxs-lookup"><span data-stu-id="25b1c-130">Name</span></span> | <span data-ttu-id="25b1c-131">Valore</span><span class="sxs-lookup"><span data-stu-id="25b1c-131">Value</span></span> | <span data-ttu-id="25b1c-132">Descrizione</span><span class="sxs-lookup"><span data-stu-id="25b1c-132">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="25b1c-133">location</span><span class="sxs-lookup"><span data-stu-id="25b1c-133">location</span></span> |<span data-ttu-id="25b1c-134">Stringa da un elenco vincolato di aree di Azure</span><span class="sxs-lookup"><span data-stu-id="25b1c-134">String from a constrained list of Azure regions</span></span> |<span data-ttu-id="25b1c-135">Posizione in cui sono distribuite le risorse.</span><span class="sxs-lookup"><span data-stu-id="25b1c-135">The location where the resources are deployed.</span></span> |
| <span data-ttu-id="25b1c-136">storageAccountNamePrefix</span><span class="sxs-lookup"><span data-stu-id="25b1c-136">storageAccountNamePrefix</span></span> |<span data-ttu-id="25b1c-137">String</span><span class="sxs-lookup"><span data-stu-id="25b1c-137">String</span></span> |<span data-ttu-id="25b1c-138">Nome DNS univoco dell'account di archiviazione in cui vengono inseriti i dischi della VM</span><span class="sxs-lookup"><span data-stu-id="25b1c-138">Unique DNS name for the Storage Account where the VM's disks are placed</span></span> |
| <span data-ttu-id="25b1c-139">domainName</span><span class="sxs-lookup"><span data-stu-id="25b1c-139">domainName</span></span> |<span data-ttu-id="25b1c-140">String</span><span class="sxs-lookup"><span data-stu-id="25b1c-140">String</span></span> |<span data-ttu-id="25b1c-141">Nome di dominio della VM Jumpbox accessibile pubblicamente nel formato: **{domainName}.{location}.cloudapp.com**, ad esempio: **mydomainname.westus.cloudapp.azure.com**</span><span class="sxs-lookup"><span data-stu-id="25b1c-141">Domain name of the publicly accessible jumpbox VM in the format: **{domainName}.{location}.cloudapp.com** For example: **mydomainname.westus.cloudapp.azure.com**</span></span> |
| <span data-ttu-id="25b1c-142">adminUsername</span><span class="sxs-lookup"><span data-stu-id="25b1c-142">adminUsername</span></span> |<span data-ttu-id="25b1c-143">Stringa</span><span class="sxs-lookup"><span data-stu-id="25b1c-143">String</span></span> |<span data-ttu-id="25b1c-144">Nome utente per le VM</span><span class="sxs-lookup"><span data-stu-id="25b1c-144">Username for the VMs</span></span> |
| <span data-ttu-id="25b1c-145">adminPassword</span><span class="sxs-lookup"><span data-stu-id="25b1c-145">adminPassword</span></span> |<span data-ttu-id="25b1c-146">Stringa</span><span class="sxs-lookup"><span data-stu-id="25b1c-146">String</span></span> |<span data-ttu-id="25b1c-147">Password delle VM</span><span class="sxs-lookup"><span data-stu-id="25b1c-147">Password for the VMs</span></span> |
| <span data-ttu-id="25b1c-148">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="25b1c-148">tshirtSize</span></span> |<span data-ttu-id="25b1c-149">Stringa da un elenco vincolato di taglie offerte</span><span class="sxs-lookup"><span data-stu-id="25b1c-149">String from a constrained list of offered t-shirt sizes</span></span> |<span data-ttu-id="25b1c-150">Dimensioni dell'unità di scala denominata di cui effettuare il provisioning.</span><span class="sxs-lookup"><span data-stu-id="25b1c-150">The named scale unit size to provision.</span></span> <span data-ttu-id="25b1c-151">Ad esempio, "Small", "Medium", "Large"</span><span class="sxs-lookup"><span data-stu-id="25b1c-151">For example, "Small", "Medium", "Large"</span></span> |
| <span data-ttu-id="25b1c-152">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="25b1c-152">virtualNetworkName</span></span> |<span data-ttu-id="25b1c-153">Stringa</span><span class="sxs-lookup"><span data-stu-id="25b1c-153">String</span></span> |<span data-ttu-id="25b1c-154">Nome della rete virtuale che l'utente vuole usare.</span><span class="sxs-lookup"><span data-stu-id="25b1c-154">Name of the virtual network that the consumer wants to use.</span></span> |
| <span data-ttu-id="25b1c-155">enableJumpbox</span><span class="sxs-lookup"><span data-stu-id="25b1c-155">enableJumpbox</span></span> |<span data-ttu-id="25b1c-156">Stringa da un elenco vincolato (abilitato/disabilitato)</span><span class="sxs-lookup"><span data-stu-id="25b1c-156">String from a constrained list (enabled/disabled)</span></span> |<span data-ttu-id="25b1c-157">Parametro che indica se abilitare Jumpbox per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="25b1c-157">Parameter that identifies whether to enable a jumpbox for the environment.</span></span> <span data-ttu-id="25b1c-158">Valori: "enabled", "disabled"</span><span class="sxs-lookup"><span data-stu-id="25b1c-158">Values: "enabled", "disabled"</span></span> |

<span data-ttu-id="25b1c-159">Il parametro **tshirtSize** usato nella sezione precedente viene definito come:</span><span class="sxs-lookup"><span data-stu-id="25b1c-159">The **tshirtSize** parameter used in the previous section is defined as:</span></span>

    "parameters": {
      "tshirtSize": {
        "type": "string",
        "defaultValue": "Small",
        "allowedValues": [
          "Small",
          "Medium",
          "Large"
        ],
        "metadata": {
          "Description": "T-shirt size of the MongoDB deployment"
        }
      }
    }


## <a name="pass-state-to-linked-templates"></a><span data-ttu-id="25b1c-160">Passaggio dello stato ai modelli collegati</span><span class="sxs-lookup"><span data-stu-id="25b1c-160">Pass state to linked templates</span></span>
<span data-ttu-id="25b1c-161">Quando ci si connette a modelli collegati, si usa spesso una combinazione di variabili statiche e generate.</span><span class="sxs-lookup"><span data-stu-id="25b1c-161">When connecting to linked templates, you often use a mix of static and generated variables.</span></span>

### <a name="static-variables"></a><span data-ttu-id="25b1c-162">Variabili statiche</span><span class="sxs-lookup"><span data-stu-id="25b1c-162">Static variables</span></span>
<span data-ttu-id="25b1c-163">Le variabili statiche vengono usate spesso per fornire i valori di base, ad esempio URL, usati in un modello.</span><span class="sxs-lookup"><span data-stu-id="25b1c-163">Static variables are often used to provide base values, such as URLs, that are used throughout a template.</span></span>

<span data-ttu-id="25b1c-164">Nell'estratto di modello seguente, `templateBaseUrl` specifica il percorso radice del modello in GitHub.</span><span class="sxs-lookup"><span data-stu-id="25b1c-164">In the following template excerpt, `templateBaseUrl` specifies the root location for the template in GitHub.</span></span> <span data-ttu-id="25b1c-165">La riga successiva compila una nuova variabile `sharedTemplateUrl` che concatena l'URL di base con il nome noto del modello di risorse condiviso.</span><span class="sxs-lookup"><span data-stu-id="25b1c-165">The next line builds a new variable `sharedTemplateUrl` that concatenates the base URL with the known name of the shared resources template.</span></span> <span data-ttu-id="25b1c-166">Sotto questa riga, una variabile oggetto complesso viene usata per archiviare una taglia, dove l'URL di base viene concatenato al percorso del modello di configurazione noto e archiviato nella proprietà `vmTemplate`.</span><span class="sxs-lookup"><span data-stu-id="25b1c-166">Below that line, a complex object variable is used to store a t-shirt size, where the base URL is concatenated to the known configuration template location and stored in the `vmTemplate` property.</span></span>

<span data-ttu-id="25b1c-167">Il vantaggio di questo approccio è di poter modificare la variabile statica solo in un'unica posizione, che la passa in tutti i modelli collegati se il percorso del modello cambia.</span><span class="sxs-lookup"><span data-stu-id="25b1c-167">The benefit of this approach is that if the template location changes, you only need to change the static variable in one place, which passes it throughout the linked templates.</span></span>

    "variables": {
      "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
      "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "slaveCount": 1,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      }
    }

### <a name="generated-variables"></a><span data-ttu-id="25b1c-168">Variabili generate</span><span class="sxs-lookup"><span data-stu-id="25b1c-168">Generated variables</span></span>
<span data-ttu-id="25b1c-169">Oltre alle variabili statiche, numerose variabili vengono generate dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="25b1c-169">In addition to static variables, several variables are generated dynamically.</span></span> <span data-ttu-id="25b1c-170">Questa sezione identifica alcuni dei tipi comuni di variabili generate.</span><span class="sxs-lookup"><span data-stu-id="25b1c-170">This section identifies some of the common types of generated variables.</span></span>

#### <a name="tshirtsize"></a><span data-ttu-id="25b1c-171">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="25b1c-171">tshirtSize</span></span>
<span data-ttu-id="25b1c-172">A questo punto si ha familiarità con la variabile generata dagli esempi precedenti.</span><span class="sxs-lookup"><span data-stu-id="25b1c-172">You are familiar with this generated variable from the examples above.</span></span>

#### <a name="networksettings"></a><span data-ttu-id="25b1c-173">networkSettings</span><span class="sxs-lookup"><span data-stu-id="25b1c-173">networkSettings</span></span>
<span data-ttu-id="25b1c-174">In una capacità, funzionalità o modello di soluzione con ambito end-to-end, i modelli collegati di solito creano risorse esistenti in una rete.</span><span class="sxs-lookup"><span data-stu-id="25b1c-174">In a capacity, capability, or end-to-end scoped solution template, the linked templates typically create resources that exist on a network.</span></span> <span data-ttu-id="25b1c-175">Un approccio semplice consiste nell'usare un oggetto complesso per archiviare le impostazioni di rete e passarle ai modelli collegati.</span><span class="sxs-lookup"><span data-stu-id="25b1c-175">One straightforward approach is to use a complex object to store network settings and pass them to linked templates.</span></span>

<span data-ttu-id="25b1c-176">Di seguito è riportato un esempio di impostazioni di rete di comunicazione.</span><span class="sxs-lookup"><span data-stu-id="25b1c-176">An example of communicating network settings can be seen below.</span></span>

    "networkSettings": {
      "vnetName": "[parameters('virtualNetworkName')]",
      "addressPrefix": "10.0.0.0/16",
      "subnets": {
        "dmz": {
          "name": "dmz",
          "prefix": "10.0.0.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        },
        "data": {
          "name": "data",
          "prefix": "10.0.1.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        }
      }
    }

#### <a name="availabilitysettings"></a><span data-ttu-id="25b1c-177">availabilitySettings</span><span class="sxs-lookup"><span data-stu-id="25b1c-177">availabilitySettings</span></span>
<span data-ttu-id="25b1c-178">Le risorse create nei modelli collegati vengono spesso inserite in un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="25b1c-178">Resources created in linked templates are often placed in an availability set.</span></span> <span data-ttu-id="25b1c-179">Nell'esempio seguente, vengono specificati il nome del set di disponibilità e anche il conteggio di domini di errore e di domini di aggiornamento da usare.</span><span class="sxs-lookup"><span data-stu-id="25b1c-179">In the following example, the availability set name is specified and also the fault domain and update domain count to use.</span></span>

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

<span data-ttu-id="25b1c-180">Se sono necessari più set di disponibilità (ad esempio, uno per i nodi master e un altro per i nodi dati), è possibile usare un nome come prefisso, specificare più set di disponibilità o seguire il modello mostrato prima per creare una variabile per una taglia specifica.</span><span class="sxs-lookup"><span data-stu-id="25b1c-180">If you need multiple availability sets (for example, one for master nodes and another for data nodes), you can use a name as a prefix, specify multiple availability sets, or follow the model shown earlier for creating a variable for a specific t-shirt size.</span></span>

#### <a name="storagesettings"></a><span data-ttu-id="25b1c-181">storageSettings</span><span class="sxs-lookup"><span data-stu-id="25b1c-181">storageSettings</span></span>
<span data-ttu-id="25b1c-182">I dettagli di archiviazione spesso vengono condivisi con i modelli collegati.</span><span class="sxs-lookup"><span data-stu-id="25b1c-182">Storage details are often shared with linked templates.</span></span> <span data-ttu-id="25b1c-183">Nell'esempio seguente, un oggetto *storageSettings* fornisce i dettagli sull'account di archiviazione e sui nomi dei contenitori.</span><span class="sxs-lookup"><span data-stu-id="25b1c-183">In the example below, a *storageSettings* object provides details about the storage account and container names.</span></span>

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a><span data-ttu-id="25b1c-184">osSettings</span><span class="sxs-lookup"><span data-stu-id="25b1c-184">osSettings</span></span>
<span data-ttu-id="25b1c-185">Con i modelli collegati, potrebbe essere necessario passare le impostazioni del sistema operativo a vari tipi di nodi tra tipi di configurazione noti diversi.</span><span class="sxs-lookup"><span data-stu-id="25b1c-185">With linked templates, you may need to pass operating system settings to various nodes types across different known configuration types.</span></span> <span data-ttu-id="25b1c-186">Un oggetto complesso consente di archiviare e condividere facilmente le informazioni sul sistema operativo e di supportare più scelte del sistema operativo per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="25b1c-186">A complex object is an easy way to store and share operating system information and also makes it easier to support multiple operating system choices for deployment.</span></span>

<span data-ttu-id="25b1c-187">Il seguente esempio mostra un oggetto per *osSettings*:</span><span class="sxs-lookup"><span data-stu-id="25b1c-187">The following example shows an object for *osSettings*:</span></span>

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a><span data-ttu-id="25b1c-188">machineSettings</span><span class="sxs-lookup"><span data-stu-id="25b1c-188">machineSettings</span></span>
<span data-ttu-id="25b1c-189">Una variabile generata, *machineSettings* è un oggetto complesso contenente una combinazione di variabili principali per la creazione di una nuova VM:</span><span class="sxs-lookup"><span data-stu-id="25b1c-189">A generated variable, *machineSettings* is a complex object containing a mix of core variables for creating a VM.</span></span> <span data-ttu-id="25b1c-190">nome utente e password dell'amministratore, un prefisso per i nomi delle VM e un riferimento a un'immagine del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="25b1c-190">The variables include administrator user name and password, a prefix for the VM names, and an operating system image reference.</span></span>

    "machineSettings": {
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "machineNamePrefix": "mongodb-",
        "osImageReference": {
            "publisher": "[variables('osFamilySpec').imagePublisher]",
            "offer": "[variables('osFamilySpec').imageOffer]",
            "sku": "[variables('osFamilySpec').imageSKU]",
            "version": "latest"
        }
    },

<span data-ttu-id="25b1c-191">Si noti che *osImageReference* recupera i valori della variabile *osSettings* definita nel modello principale.</span><span class="sxs-lookup"><span data-stu-id="25b1c-191">Note that *osImageReference* retrieves the values from the *osSettings* variable defined in the main template.</span></span> <span data-ttu-id="25b1c-192">Ciò significa che è possibile modificare facilmente il sistema operativo per una VM, interamente o in base alla preferenza di un utente del modello.</span><span class="sxs-lookup"><span data-stu-id="25b1c-192">That means you can easily change the operating system for a VM—entirely or based on the preference of a template consumer.</span></span>

#### <a name="vmscripts"></a><span data-ttu-id="25b1c-193">vmScripts</span><span class="sxs-lookup"><span data-stu-id="25b1c-193">vmScripts</span></span>
<span data-ttu-id="25b1c-194">L'oggetto *vmScripts* contiene i dettagli sugli script per il download e l'esecuzione in un'istanza di una VM, inclusi i riferimenti esterni e interni.</span><span class="sxs-lookup"><span data-stu-id="25b1c-194">The *vmScripts* object contains details about the scripts to download and execute on a VM instance, including outside and inside references.</span></span> <span data-ttu-id="25b1c-195">I riferimenti esterni includono l'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="25b1c-195">Outside references include the infrastructure.</span></span>
<span data-ttu-id="25b1c-196">I riferimenti interni includono il software installato e la configurazione.</span><span class="sxs-lookup"><span data-stu-id="25b1c-196">Inside references include the installed software installed and configuration.</span></span>

<span data-ttu-id="25b1c-197">La proprietà *scriptsToDownload* viene usata per elencare gli script per il download nella VM.</span><span class="sxs-lookup"><span data-stu-id="25b1c-197">You use the *scriptsToDownload* property to list the scripts to download to the VM.</span></span> <span data-ttu-id="25b1c-198">Questo oggetto contiene anche i riferimenti agli argomenti della riga di comando per diversi tipi di azioni.</span><span class="sxs-lookup"><span data-stu-id="25b1c-198">This object also contains references to command-line arguments for different types of actions.</span></span> <span data-ttu-id="25b1c-199">Queste azioni includono l'esecuzione dell'installazione predefinita per ogni nodo, un'installazione eseguita dopo che tutti i nodi sono stati distribuiti ed eventuali altri script specifici di un determinato modello.</span><span class="sxs-lookup"><span data-stu-id="25b1c-199">These actions include executing the default installation for each individual node, an installation that runs after all nodes are deployed, and any additional scripts that may be specific to a given template.</span></span>

<span data-ttu-id="25b1c-200">Questo esempio deriva da un modello usato per distribuire MongoDB, che richiede un arbitro per offrire elevati livelli di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="25b1c-200">This example is from a template used to deploy MongoDB, which requires an arbiter to deliver high availability.</span></span> <span data-ttu-id="25b1c-201">*arbiterNodeInstallCommand* è stato aggiunto a *vmScripts* per installare l'arbitro.</span><span class="sxs-lookup"><span data-stu-id="25b1c-201">The *arbiterNodeInstallCommand* has been added to *vmScripts* to install the arbiter.</span></span>

<span data-ttu-id="25b1c-202">Nella sezione delle variabili è possibile trovare le variabili che definiscono il testo specifico per eseguire lo script con i valori appropriati.</span><span class="sxs-lookup"><span data-stu-id="25b1c-202">The variables section is where you find the variables that define the specific text to execute the script with the proper values.</span></span>

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a><span data-ttu-id="25b1c-203">Restituzione dello stato da un modello</span><span class="sxs-lookup"><span data-stu-id="25b1c-203">Return state from a template</span></span>
<span data-ttu-id="25b1c-204">Non è solo possibile passare i dati a un modello, ma anche condividerli di nuovo con il modello chiamante.</span><span class="sxs-lookup"><span data-stu-id="25b1c-204">Not only can you pass data into a template, you can also share data back to the calling template.</span></span> <span data-ttu-id="25b1c-205">Nella sezione **outputs** di un modello collegato, è possibile specificare le coppie chiave/valore che possono essere utilizzate dal modello di origine.</span><span class="sxs-lookup"><span data-stu-id="25b1c-205">In the **outputs** section of a linked template, you can provide key/value pairs that can be consumed by the source template.</span></span>

<span data-ttu-id="25b1c-206">Il seguente esempio mostra come passare l'indirizzo IP privato generato in un modello collegato.</span><span class="sxs-lookup"><span data-stu-id="25b1c-206">The following example shows how to pass the private IP address generated in a linked template.</span></span>

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

<span data-ttu-id="25b1c-207">All'interno del modello principale, è possibile usare tali dati con la sintassi seguente:</span><span class="sxs-lookup"><span data-stu-id="25b1c-207">Within the main template, you can use that data with the following syntax:</span></span>

    "[reference('master-node').outputs.masterip.value]"

<span data-ttu-id="25b1c-208">È possibile usare l'espressione seguente nella sezione outputs o nella sezione resources del modello principale.</span><span class="sxs-lookup"><span data-stu-id="25b1c-208">You can use this expression in either the outputs section or the resources section of the main template.</span></span> <span data-ttu-id="25b1c-209">Non è possibile usare l'espressione nella sezione delle variabili in quanto si basa sullo stato di runtime.</span><span class="sxs-lookup"><span data-stu-id="25b1c-209">You cannot use the expression in the variables section because it relies on the runtime state.</span></span> <span data-ttu-id="25b1c-210">Per restituire il valore dal modello principale, usare:</span><span class="sxs-lookup"><span data-stu-id="25b1c-210">To return this value from the main template, use:</span></span>

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

<span data-ttu-id="25b1c-211">Per un esempio di uso della sezione outputs di un modello collegato per la restituzione dei dischi dati per una macchina virtuale, vedere [Creazione di più dischi dati per una macchina virtuale](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="25b1c-211">For an example of using the outputs section of a linked template to return data disks for a virtual machine, see [Creating multiple data disks for a Virtual Machine](resource-group-create-multiple.md).</span></span>

## <a name="define-authentication-settings-for-virtual-machine"></a><span data-ttu-id="25b1c-212">Definizione delle impostazioni di autenticazione per la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="25b1c-212">Define authentication settings for virtual machine</span></span>
<span data-ttu-id="25b1c-213">È possibile usare il modello descritto in precedenza per le impostazioni di configurazione per specificare le impostazioni di autenticazione per una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="25b1c-213">You can use the same pattern shown previously for configuration settings to specify the authentication settings for a virtual machine.</span></span> <span data-ttu-id="25b1c-214">Creare un parametro per passare il tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="25b1c-214">You create a parameter for passing in the type of authentication.</span></span>

    "parameters": {
      "authenticationType": {
        "allowedValues": [
          "password",
          "sshPublicKey"
        ],
        "defaultValue": "password",
        "metadata": {
          "description": "Authentication type"
        },
        "type": "string"
      }
    }

<span data-ttu-id="25b1c-215">Aggiungere le variabili per i diversi tipi di autenticazione e una variabile per archiviare il tipo usato per la distribuzione in base al valore del parametro.</span><span class="sxs-lookup"><span data-stu-id="25b1c-215">You add variables for the different authentication types, and a variable to store which type is used for this deployment based on the value of the parameter.</span></span>

    "variables": {
      "osProfile": "[variables(concat('osProfile', parameters('authenticationType')))]",
      "osProfilepassword": {
        "adminPassword": "[parameters('adminPassword')]",
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]"
      },
      "osProfilesshPublicKey": {
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]",
        "linuxConfiguration": {
          "disablePasswordAuthentication": "true",
          "ssh": {
            "publicKeys": [
              {
                "keyData": "[parameters('sshPublicKey')]",
                "path": "/home/notused/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
    }

<span data-ttu-id="25b1c-216">Quando si definisce la macchina virtuale, si imposta **osProfile** sulla variabile creata.</span><span class="sxs-lookup"><span data-stu-id="25b1c-216">When defining the virtual machine, you set the **osProfile** to the variable you created.</span></span>

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a><span data-ttu-id="25b1c-217">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25b1c-217">Next steps</span></span>
* <span data-ttu-id="25b1c-218">Per informazioni sulle sezioni del modello, vedere [Creazione di modelli di Gestione risorse di Azure](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="25b1c-218">To learn about the sections of the template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="25b1c-219">Per tutte le funzioni disponibili in un modello, vedere [Funzioni del modello di Gestione risorse di Azure](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="25b1c-219">To see the functions that are available within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md)</span></span>
