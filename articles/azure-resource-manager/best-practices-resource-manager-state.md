---
title: aaaPass valori complessi tra modelli di Azure | Documenti Microsoft
description: Mostra consigliabile approcci per l'utilizzo di dati relativi allo stato tooshare oggetti complessi con i modelli di gestione risorse di Azure e collegato.
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
ms.openlocfilehash: 72df1dee351446cea6ce15269e6db288b1f1db79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="share-state-tooand-from-azure-resource-manager-templates"></a><span data-ttu-id="a3dbe-103">Condivisione dello stato tooand dai modelli di gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="a3dbe-103">Share state tooand from Azure Resource Manager templates</span></span>
<span data-ttu-id="a3dbe-104">Questo argomento illustra le procedure consigliate per la gestione e la condivisione dello stato all'interno dei modelli.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-104">This topic shows best practices for managing and sharing state within templates.</span></span> <span data-ttu-id="a3dbe-105">Hello parametri e variabili illustrate in questo argomento sono riportati alcuni esempi di tipo hello degli oggetti è possibile definire tooconveniently organizzare i requisiti di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-105">hello parameters and variables shown in this topic are examples of hello type of objects you can define tooconveniently organize your deployment requirements.</span></span> <span data-ttu-id="a3dbe-106">Da questi esempi, è possibile implementare gli oggetti con valori di proprietà utili per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-106">From these examples, you can implement your own objects with property values that make sense for your environment.</span></span>

<span data-ttu-id="a3dbe-107">Questo argomento fa parte di un white paper di dimensioni maggiori.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-107">This topic is part of a larger whitepaper.</span></span> <span data-ttu-id="a3dbe-108">scaricare hello tooread completo carta, [World classe Resource Manager modelli considerazioni e procedure consigliate di rivelati](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span><span class="sxs-lookup"><span data-stu-id="a3dbe-108">tooread hello full paper, download [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span></span>

## <a name="provide-standard-configuration-settings"></a><span data-ttu-id="a3dbe-109">Uso di impostazioni di configurazione standard</span><span class="sxs-lookup"><span data-stu-id="a3dbe-109">Provide standard configuration settings</span></span>
<span data-ttu-id="a3dbe-110">Piuttosto che offrono un modello che fornisce la massima flessibilità e le variazioni innumerevoli, un modello comune è tooprovide una selezione di una configurazione conosciuta.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-110">Rather than offer a template that provides total flexibility and countless variations, a common pattern is tooprovide a selection of known configurations.</span></span> <span data-ttu-id="a3dbe-111">In effetti, gli utenti possono selezionare taglie standard, come sandbox, small, medium e large.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-111">In effect, users can select standard t-shirt sizes such as sandbox, small, medium, and large.</span></span> <span data-ttu-id="a3dbe-112">Altri esempi di taglie sono le offerte di prodotti, come Community Edition o Enterprise Edition.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-112">Other examples of t-shirt sizes are product offerings, such as community edition or enterprise edition.</span></span> <span data-ttu-id="a3dbe-113">In altri casi, potrebbero essere configurazioni specifiche per i carichi di lavoro di una determinata tecnologia, ad esempio map reduce o no sql.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-113">In other cases, it may be workload-specific configurations of a technology – such as map reduce or no sql.</span></span>

<span data-ttu-id="a3dbe-114">Con gli oggetti complessi, è possibile creare le variabili che contengono raccolte di dati, talvolta noti anche come "elenchi di proprietà" e utilizzare tale dichiarazione della risorsa di hello toodrive dati nel modello.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-114">With complex objects, you can create variables that contain collections of data, sometimes known as "property bags" and use that data toodrive hello resource declaration in your template.</span></span> <span data-ttu-id="a3dbe-115">Questo approccio fornisce configurazioni note ed efficienti di dimensioni variabili, preconfigurate per i clienti.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-115">This approach provides good, known configurations of varying sizes that are preconfigured for customers.</span></span> <span data-ttu-id="a3dbe-116">Senza configurazioni note, gli utenti del modello di hello devono determinare dimensioni cluster autonomamente, fattore nei vincoli di risorse di piattaforma ed eseguire matematiche tooidentify hello risultante partizionamento dell'account di archiviazione e altre risorse (a causa delle dimensioni toocluster e limitazioni delle risorse).</span><span class="sxs-lookup"><span data-stu-id="a3dbe-116">Without known configurations, users of hello template must determine cluster sizing on their own, factor in platform resource constraints, and do math tooidentify hello resulting partitioning of storage accounts and other resources (due toocluster size and resource constraints).</span></span> <span data-ttu-id="a3dbe-117">Inoltre toomaking una migliore esperienza per cliente hello, alcune configurazioni note sono toosupport più semplice e consentono di offrire un livello di densità.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-117">In addition toomaking a better experience for hello customer, a few known configurations are easier toosupport and can help you deliver a higher level of density.</span></span>

<span data-ttu-id="a3dbe-118">Hello seguente esempio viene illustrato come le variabili di toodefine che contengono oggetti complessi per la rappresentazione di raccolte di dati.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-118">hello following example shows how toodefine variables that contain complex objects for representing collections of data.</span></span> <span data-ttu-id="a3dbe-119">le raccolte di Hello definiscono i valori utilizzati per la dimensione della macchina virtuale, le impostazioni di rete, impostazioni del sistema operativo e disponibilità.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-119">hello collections define values that are used for virtual machine size, network settings, operating system settings and availability settings.</span></span>

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

<span data-ttu-id="a3dbe-120">Si noti che hello **tshirtSize** variabile concatena magliette hello fornite tramite un parametro (**Small**, **Media**, **grande**) toohello testo **tshirtSize**.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-120">Notice that hello **tshirtSize** variable concatenates hello t-shirt size you provided through a parameter (**Small**, **Medium**, **Large**) toohello text **tshirtSize**.</span></span> <span data-ttu-id="a3dbe-121">Utilizzare questa variabile di oggetto complesso associato hello tooretrieve variabile per tale magliette.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-121">You use this variable tooretrieve hello associated complex object variable for that t-shirt size.</span></span>

<span data-ttu-id="a3dbe-122">È quindi possibile fare riferimento a queste variabili in un secondo momento nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-122">You can then reference these variables later in hello template.</span></span> <span data-ttu-id="a3dbe-123">Hello possibilità tooreference denominato le variabili e le relative proprietà semplifica la sintassi dei modelli di hello e rende facile toounderstand contesto.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-123">hello ability tooreference named-variables and their properties simplifies hello template syntax, and makes it easy toounderstand context.</span></span> <span data-ttu-id="a3dbe-124">Hello di esempio seguente definisce una risorsa toodeploy utilizzando oggetti hello illustrati in precedenza tooset valori.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-124">hello following example defines a resource toodeploy by using hello objects shown previously tooset values.</span></span> <span data-ttu-id="a3dbe-125">Ad esempio, hello dimensioni della macchina virtuale è impostato per il recupero del valore di hello per `variables('tshirtSize').vmSize` mentre il valore di hello per dimensioni del disco hello vengano recuperata dal `variables('tshirtSize').diskSize`.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-125">For example, hello VM size is set by retrieving hello value for `variables('tshirtSize').vmSize` while hello value for hello disk size is retrieved from `variables('tshirtSize').diskSize`.</span></span> <span data-ttu-id="a3dbe-126">Inoltre, hello URI per un modello collegato viene impostato con il valore di hello per `variables('tshirtSize').vmTemplate`.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-126">In addition, hello URI for a linked template is set with hello value for `variables('tshirtSize').vmTemplate`.</span></span>

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

## <a name="pass-state-tooa-template"></a><span data-ttu-id="a3dbe-127">Passaggio di stato tooa modello</span><span class="sxs-lookup"><span data-stu-id="a3dbe-127">Pass state tooa template</span></span>
<span data-ttu-id="a3dbe-128">È possibile condividere lo stato in un modello tramite parametri forniti direttamente durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-128">You share state into a template through parameters that you provide directly during deployment.</span></span>

<span data-ttu-id="a3dbe-129">Hello seguenti tabella elenchi comunemente utilizzati parametri nei modelli.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-129">hello following table lists commonly used parameters in templates.</span></span>

| <span data-ttu-id="a3dbe-130">Nome</span><span class="sxs-lookup"><span data-stu-id="a3dbe-130">Name</span></span> | <span data-ttu-id="a3dbe-131">Valore</span><span class="sxs-lookup"><span data-stu-id="a3dbe-131">Value</span></span> | <span data-ttu-id="a3dbe-132">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a3dbe-132">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a3dbe-133">location</span><span class="sxs-lookup"><span data-stu-id="a3dbe-133">location</span></span> |<span data-ttu-id="a3dbe-134">Stringa da un elenco vincolato di aree di Azure</span><span class="sxs-lookup"><span data-stu-id="a3dbe-134">String from a constrained list of Azure regions</span></span> |<span data-ttu-id="a3dbe-135">percorso di Hello in cui vengono distribuite le risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-135">hello location where hello resources are deployed.</span></span> |
| <span data-ttu-id="a3dbe-136">storageAccountNamePrefix</span><span class="sxs-lookup"><span data-stu-id="a3dbe-136">storageAccountNamePrefix</span></span> |<span data-ttu-id="a3dbe-137">String</span><span class="sxs-lookup"><span data-stu-id="a3dbe-137">String</span></span> |<span data-ttu-id="a3dbe-138">Nome DNS univoco per l'Account di archiviazione in cui vengono collocati i dischi della macchina virtuale di hello hello</span><span class="sxs-lookup"><span data-stu-id="a3dbe-138">Unique DNS name for hello Storage Account where hello VM's disks are placed</span></span> |
| <span data-ttu-id="a3dbe-139">domainName</span><span class="sxs-lookup"><span data-stu-id="a3dbe-139">domainName</span></span> |<span data-ttu-id="a3dbe-140">String</span><span class="sxs-lookup"><span data-stu-id="a3dbe-140">String</span></span> |<span data-ttu-id="a3dbe-141">Nome di dominio di hello accessibile pubblicamente jumpbox macchina virtuale in formato hello: **{domainName}. { percorso}.cloudapp.com** ad esempio: **mydomainname.westus.cloudapp.azure.com**</span><span class="sxs-lookup"><span data-stu-id="a3dbe-141">Domain name of hello publicly accessible jumpbox VM in hello format: **{domainName}.{location}.cloudapp.com** For example: **mydomainname.westus.cloudapp.azure.com**</span></span> |
| <span data-ttu-id="a3dbe-142">adminUsername</span><span class="sxs-lookup"><span data-stu-id="a3dbe-142">adminUsername</span></span> |<span data-ttu-id="a3dbe-143">String</span><span class="sxs-lookup"><span data-stu-id="a3dbe-143">String</span></span> |<span data-ttu-id="a3dbe-144">Nome utente per hello macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="a3dbe-144">Username for hello VMs</span></span> |
| <span data-ttu-id="a3dbe-145">adminPassword</span><span class="sxs-lookup"><span data-stu-id="a3dbe-145">adminPassword</span></span> |<span data-ttu-id="a3dbe-146">String</span><span class="sxs-lookup"><span data-stu-id="a3dbe-146">String</span></span> |<span data-ttu-id="a3dbe-147">Password per hello macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="a3dbe-147">Password for hello VMs</span></span> |
| <span data-ttu-id="a3dbe-148">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="a3dbe-148">tshirtSize</span></span> |<span data-ttu-id="a3dbe-149">Stringa da un elenco vincolato di taglie offerte</span><span class="sxs-lookup"><span data-stu-id="a3dbe-149">String from a constrained list of offered t-shirt sizes</span></span> |<span data-ttu-id="a3dbe-150">Hello denominato tooprovision dimensioni unità di scala.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-150">hello named scale unit size tooprovision.</span></span> <span data-ttu-id="a3dbe-151">Ad esempio, "Small", "Medium", "Large"</span><span class="sxs-lookup"><span data-stu-id="a3dbe-151">For example, "Small", "Medium", "Large"</span></span> |
| <span data-ttu-id="a3dbe-152">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="a3dbe-152">virtualNetworkName</span></span> |<span data-ttu-id="a3dbe-153">String</span><span class="sxs-lookup"><span data-stu-id="a3dbe-153">String</span></span> |<span data-ttu-id="a3dbe-154">Nome di rete virtuale hello hello consumer desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-154">Name of hello virtual network that hello consumer wants toouse.</span></span> |
| <span data-ttu-id="a3dbe-155">enableJumpbox</span><span class="sxs-lookup"><span data-stu-id="a3dbe-155">enableJumpbox</span></span> |<span data-ttu-id="a3dbe-156">Stringa da un elenco vincolato (abilitato/disabilitato)</span><span class="sxs-lookup"><span data-stu-id="a3dbe-156">String from a constrained list (enabled/disabled)</span></span> |<span data-ttu-id="a3dbe-157">Parametro che identifica se tooenable un jumpbox per ambiente hello.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-157">Parameter that identifies whether tooenable a jumpbox for hello environment.</span></span> <span data-ttu-id="a3dbe-158">Valori: "enabled", "disabled"</span><span class="sxs-lookup"><span data-stu-id="a3dbe-158">Values: "enabled", "disabled"</span></span> |

<span data-ttu-id="a3dbe-159">Hello **tshirtSize** parametro usato nella sezione precedente hello è definito come:</span><span class="sxs-lookup"><span data-stu-id="a3dbe-159">hello **tshirtSize** parameter used in hello previous section is defined as:</span></span>

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
          "Description": "T-shirt size of hello MongoDB deployment"
        }
      }
    }


## <a name="pass-state-toolinked-templates"></a><span data-ttu-id="a3dbe-160">Passare modelli toolinked stato</span><span class="sxs-lookup"><span data-stu-id="a3dbe-160">Pass state toolinked templates</span></span>
<span data-ttu-id="a3dbe-161">Quando ci si connette toolinked modelli, spesso utilizzare una combinazione di statico e generato le variabili.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-161">When connecting toolinked templates, you often use a mix of static and generated variables.</span></span>

### <a name="static-variables"></a><span data-ttu-id="a3dbe-162">Variabili statiche</span><span class="sxs-lookup"><span data-stu-id="a3dbe-162">Static variables</span></span>
<span data-ttu-id="a3dbe-163">Variabili statiche sono spesso valori di base tooprovide utilizzato, ad esempio, gli URL vengono utilizzati in un modello.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-163">Static variables are often used tooprovide base values, such as URLs, that are used throughout a template.</span></span>

<span data-ttu-id="a3dbe-164">Nel seguente estratto di codice modello hello `templateBaseUrl` specifica il percorso radice hello per modello hello in GitHub.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-164">In hello following template excerpt, `templateBaseUrl` specifies hello root location for hello template in GitHub.</span></span> <span data-ttu-id="a3dbe-165">riga successiva Hello compila una nuova variabile `sharedTemplateUrl` che concatena hello l'URL di base con nome noto di hello del modello di risorse condivise hello.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-165">hello next line builds a new variable `sharedTemplateUrl` that concatenates hello base URL with hello known name of hello shared resources template.</span></span> <span data-ttu-id="a3dbe-166">Sotto tale riga, una variabile oggetto complesso è toostore usato un magliette, dove l'URL di base hello è concatenato toohello noto percorso del modello di configurazione e archiviati in hello `vmTemplate` proprietà.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-166">Below that line, a complex object variable is used toostore a t-shirt size, where hello base URL is concatenated toohello known configuration template location and stored in hello `vmTemplate` property.</span></span>

<span data-ttu-id="a3dbe-167">Il vantaggio di Hello di questo approccio è che se il percorso di modello hello viene modificato, è necessario solo toochange variabile statica di hello in un'unica posizione, che viene passata in tutti i modelli di hello collegato.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-167">hello benefit of this approach is that if hello template location changes, you only need toochange hello static variable in one place, which passes it throughout hello linked templates.</span></span>

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

### <a name="generated-variables"></a><span data-ttu-id="a3dbe-168">Variabili generate</span><span class="sxs-lookup"><span data-stu-id="a3dbe-168">Generated variables</span></span>
<span data-ttu-id="a3dbe-169">Nelle variabili toostatic aggiunta, vengono generate in modo dinamico diverse variabili.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-169">In addition toostatic variables, several variables are generated dynamically.</span></span> <span data-ttu-id="a3dbe-170">In questa sezione vengono illustrati alcuni dei tipi di variabili generate comuni hello.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-170">This section identifies some of hello common types of generated variables.</span></span>

#### <a name="tshirtsize"></a><span data-ttu-id="a3dbe-171">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="a3dbe-171">tshirtSize</span></span>
<span data-ttu-id="a3dbe-172">Si ha familiarità con questa variabile generata dagli esempi hello precedenti.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-172">You are familiar with this generated variable from hello examples above.</span></span>

#### <a name="networksettings"></a><span data-ttu-id="a3dbe-173">networkSettings</span><span class="sxs-lookup"><span data-stu-id="a3dbe-173">networkSettings</span></span>
<span data-ttu-id="a3dbe-174">In un hello capacità, funzionalità o il modello di soluzione con ambito end-to-end, modelli collegati in genere creano risorse esistenti in una rete.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-174">In a capacity, capability, or end-to-end scoped solution template, hello linked templates typically create resources that exist on a network.</span></span> <span data-ttu-id="a3dbe-175">Un approccio semplice è toouse le impostazioni di rete toostore un oggetto complesso e passarli toolinked modelli.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-175">One straightforward approach is toouse a complex object toostore network settings and pass them toolinked templates.</span></span>

<span data-ttu-id="a3dbe-176">Di seguito è riportato un esempio di impostazioni di rete di comunicazione.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-176">An example of communicating network settings can be seen below.</span></span>

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

#### <a name="availabilitysettings"></a><span data-ttu-id="a3dbe-177">availabilitySettings</span><span class="sxs-lookup"><span data-stu-id="a3dbe-177">availabilitySettings</span></span>
<span data-ttu-id="a3dbe-178">Le risorse create nei modelli collegati vengono spesso inserite in un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-178">Resources created in linked templates are often placed in an availability set.</span></span> <span data-ttu-id="a3dbe-179">Nel seguente esempio di hello, hello Nome set di disponibilità specificato e hello anche dominio di errore e aggiorna toouse conteggio di dominio.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-179">In hello following example, hello availability set name is specified and also hello fault domain and update domain count toouse.</span></span>

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

<span data-ttu-id="a3dbe-180">Se è necessario più set di disponibilità (ad esempio, uno per i nodi principali) e un altro per i nodi di dati, è possibile utilizzare un nome come prefisso, specificare più set di disponibilità o di seguire il modello di hello illustrato in precedenza per la creazione di una variabile per una specifica magliette.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-180">If you need multiple availability sets (for example, one for master nodes and another for data nodes), you can use a name as a prefix, specify multiple availability sets, or follow hello model shown earlier for creating a variable for a specific t-shirt size.</span></span>

#### <a name="storagesettings"></a><span data-ttu-id="a3dbe-181">storageSettings</span><span class="sxs-lookup"><span data-stu-id="a3dbe-181">storageSettings</span></span>
<span data-ttu-id="a3dbe-182">I dettagli di archiviazione spesso vengono condivisi con i modelli collegati.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-182">Storage details are often shared with linked templates.</span></span> <span data-ttu-id="a3dbe-183">Nell'esempio hello riportato di seguito, un *storageSettings* oggetto fornisce informazioni dettagliate su hello i nomi degli account e il contenitore di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-183">In hello example below, a *storageSettings* object provides details about hello storage account and container names.</span></span>

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a><span data-ttu-id="a3dbe-184">osSettings</span><span class="sxs-lookup"><span data-stu-id="a3dbe-184">osSettings</span></span>
<span data-ttu-id="a3dbe-185">Con i modelli collegati, potrebbe essere tipi di nodi toovarious le impostazioni del sistema operativo toopass tra tipi diversi di configurazione.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-185">With linked templates, you may need toopass operating system settings toovarious nodes types across different known configuration types.</span></span> <span data-ttu-id="a3dbe-186">Un oggetto complesso è un modo semplice toostore e condivisione di informazioni sul sistema operativo e lo rende anche più facile toosupport più sistemi operativi disponibili per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-186">A complex object is an easy way toostore and share operating system information and also makes it easier toosupport multiple operating system choices for deployment.</span></span>

<span data-ttu-id="a3dbe-187">Hello esempio seguente viene illustrato un oggetto per *osSettings*:</span><span class="sxs-lookup"><span data-stu-id="a3dbe-187">hello following example shows an object for *osSettings*:</span></span>

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a><span data-ttu-id="a3dbe-188">machineSettings</span><span class="sxs-lookup"><span data-stu-id="a3dbe-188">machineSettings</span></span>
<span data-ttu-id="a3dbe-189">Una variabile generata, *machineSettings* è un oggetto complesso contenente una combinazione di variabili principali per la creazione di una nuova VM:</span><span class="sxs-lookup"><span data-stu-id="a3dbe-189">A generated variable, *machineSettings* is a complex object containing a mix of core variables for creating a VM.</span></span> <span data-ttu-id="a3dbe-190">variabili di Hello includono nome utente dell'amministratore e la password, un prefisso per i nomi di macchina virtuale hello e riferimento a un'immagine del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-190">hello variables include administrator user name and password, a prefix for hello VM names, and an operating system image reference.</span></span>

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

<span data-ttu-id="a3dbe-191">Si noti che *osImageReference* recupera hello valori hello *osSettings* variabile definita nel modello principale hello.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-191">Note that *osImageReference* retrieves hello values from hello *osSettings* variable defined in hello main template.</span></span> <span data-ttu-id="a3dbe-192">Pertanto, è possibile modificare facilmente hello del sistema operativo per una macchina virtuale, interamente o in base alle preferenze hello di un consumer di modello.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-192">That means you can easily change hello operating system for a VM—entirely or based on hello preference of a template consumer.</span></span>

#### <a name="vmscripts"></a><span data-ttu-id="a3dbe-193">vmScripts</span><span class="sxs-lookup"><span data-stu-id="a3dbe-193">vmScripts</span></span>
<span data-ttu-id="a3dbe-194">Hello *vmScripts* oggetto contiene i dettagli sul toodownload script hello ed eseguire in un'istanza di macchina virtuale, inclusi i riferimenti esterni e interni.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-194">hello *vmScripts* object contains details about hello scripts toodownload and execute on a VM instance, including outside and inside references.</span></span> <span data-ttu-id="a3dbe-195">All'esterno di riferimenti includono infrastruttura hello.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-195">Outside references include hello infrastructure.</span></span>
<span data-ttu-id="a3dbe-196">I riferimenti interni includono configurazione e hello installato software installato.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-196">Inside references include hello installed software installed and configuration.</span></span>

<span data-ttu-id="a3dbe-197">Utilizzare hello *scriptsToDownload* hello toolist proprietà script toodownload toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-197">You use hello *scriptsToDownload* property toolist hello scripts toodownload toohello VM.</span></span> <span data-ttu-id="a3dbe-198">Inoltre, l'oggetto contiene argomenti della riga di toocommand riferimenti per i diversi tipi di azioni.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-198">This object also contains references toocommand-line arguments for different types of actions.</span></span> <span data-ttu-id="a3dbe-199">Tali azioni includono l'esecuzione di installazione predefinita di hello per ogni singolo nodo, un'installazione che viene eseguito dopo che tutti i nodi vengono distribuiti e script aggiuntivi che possono essere specifico tooa modello specificato.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-199">These actions include executing hello default installation for each individual node, an installation that runs after all nodes are deployed, and any additional scripts that may be specific tooa given template.</span></span>

<span data-ttu-id="a3dbe-200">Questo esempio è tratto toodeploy un modello utilizzato MongoDB, che richiede un'analisi toodeliver la disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-200">This example is from a template used toodeploy MongoDB, which requires an arbiter toodeliver high availability.</span></span> <span data-ttu-id="a3dbe-201">Hello *arbiterNodeInstallCommand* è stato aggiunto troppo*vmScripts* analisi hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-201">hello *arbiterNodeInstallCommand* has been added too*vmScripts* tooinstall hello arbiter.</span></span>

<span data-ttu-id="a3dbe-202">sezione variabili Hello è riportate le variabili di hello che definiscono hello testo specifico tooexecute hello lo script con i valori appropriati di hello.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-202">hello variables section is where you find hello variables that define hello specific text tooexecute hello script with hello proper values.</span></span>

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a><span data-ttu-id="a3dbe-203">Restituzione dello stato da un modello</span><span class="sxs-lookup"><span data-stu-id="a3dbe-203">Return state from a template</span></span>
<span data-ttu-id="a3dbe-204">Non solo può passare i dati in un modello, è anche possibile chiamata modello di condivisione dati toohello indietro.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-204">Not only can you pass data into a template, you can also share data back toohello calling template.</span></span> <span data-ttu-id="a3dbe-205">In hello **restituisce** sezione di un modello collegato, è possibile specificare le coppie chiave/valore che possono essere utilizzate dal modello di origine hello.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-205">In hello **outputs** section of a linked template, you can provide key/value pairs that can be consumed by hello source template.</span></span>

<span data-ttu-id="a3dbe-206">Hello esempio seguente viene illustrato come toopass hello indirizzo IP privato generato in un modello collegato.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-206">hello following example shows how toopass hello private IP address generated in a linked template.</span></span>

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

<span data-ttu-id="a3dbe-207">Nel modello principale hello, è possibile utilizzare tali dati con hello la seguente sintassi:</span><span class="sxs-lookup"><span data-stu-id="a3dbe-207">Within hello main template, you can use that data with hello following syntax:</span></span>

    "[reference('master-node').outputs.masterip.value]"

<span data-ttu-id="a3dbe-208">È possibile utilizzare l'espressione seguente nella sezione di output di hello o la sezione relativa alle risorse hello del modello principale hello.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-208">You can use this expression in either hello outputs section or hello resources section of hello main template.</span></span> <span data-ttu-id="a3dbe-209">È possibile utilizzare l'espressione hello nella sezione variabili hello perché si basa sullo stato del runtime di hello.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-209">You cannot use hello expression in hello variables section because it relies on hello runtime state.</span></span> <span data-ttu-id="a3dbe-210">tooreturn questo valore dal modello principale hello, usare:</span><span class="sxs-lookup"><span data-stu-id="a3dbe-210">tooreturn this value from hello main template, use:</span></span>

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

<span data-ttu-id="a3dbe-211">Per un esempio di utilizzo hello restituisce una sezione di un modello collegato tooreturn di dischi di dati per una macchina virtuale, vedere [la creazione di più dischi dati per una macchina virtuale](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="a3dbe-211">For an example of using hello outputs section of a linked template tooreturn data disks for a virtual machine, see [Creating multiple data disks for a Virtual Machine](resource-group-create-multiple.md).</span></span>

## <a name="define-authentication-settings-for-virtual-machine"></a><span data-ttu-id="a3dbe-212">Definizione delle impostazioni di autenticazione per la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a3dbe-212">Define authentication settings for virtual machine</span></span>
<span data-ttu-id="a3dbe-213">È possibile utilizzare hello stesso modello illustrato in precedenza per la configurazione delle impostazioni toospecify hello impostazioni di autenticazione per una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-213">You can use hello same pattern shown previously for configuration settings toospecify hello authentication settings for a virtual machine.</span></span> <span data-ttu-id="a3dbe-214">Creare un parametro per il passaggio in tipo di hello di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-214">You create a parameter for passing in hello type of authentication.</span></span>

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

<span data-ttu-id="a3dbe-215">Aggiungere le variabili per i tipi di autenticazione diversi hello e una variabile toostore quale tipo viene usato per la distribuzione in base al valore di hello del parametro hello.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-215">You add variables for hello different authentication types, and a variable toostore which type is used for this deployment based on hello value of hello parameter.</span></span>

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

<span data-ttu-id="a3dbe-216">Quando si definisce una macchina virtuale hello, si imposta hello **osProfile** toohello variabile creata.</span><span class="sxs-lookup"><span data-stu-id="a3dbe-216">When defining hello virtual machine, you set hello **osProfile** toohello variable you created.</span></span>

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a><span data-ttu-id="a3dbe-217">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a3dbe-217">Next steps</span></span>
* <span data-ttu-id="a3dbe-218">toolearn sulle sezioni hello hello del modello di, vedere [la creazione di modelli di gestione risorse di Azure](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="a3dbe-218">toolearn about hello sections of hello template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="a3dbe-219">le funzioni hello toosee disponibili all'interno di un modello, vedere [funzioni di modello di gestione risorse di Azure](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="a3dbe-219">toosee hello functions that are available within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md)</span></span>
