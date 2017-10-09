---
title: Cenni preliminari sul Provider di risorse aaaNetwork | Documenti Microsoft
description: Informazioni su hello nuovo Provider di risorse di rete in Gestione risorse di Azure
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 79bf09da-4809-45cb-8d21-705616ef24dc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 81b8f51fe8ee180d8f7885c6e04eb953904d7be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="network-resource-provider"></a><span data-ttu-id="67f65-103">Provider di risorse di rete</span><span class="sxs-lookup"><span data-stu-id="67f65-103">Network Resource Provider</span></span>
<span data-ttu-id="67f65-104">Un'esigenza supplementare in successo aziendale attuali, è hello toobuild possibilità e gestire applicazioni di rete su larga scala in un modo agile, flessibile, sicuro e ripetibile.</span><span class="sxs-lookup"><span data-stu-id="67f65-104">An underpinning need in today’s business success, is hello ability toobuild and manage large scale network aware applications in an agile, flexible, secure and repeatable way.</span></span> <span data-ttu-id="67f65-105">Gestione risorse di Azure consente si toocreate tali applicazioni, come un unico insieme di risorse in gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="67f65-105">Azure Resource Manager enables you toocreate such applications, as a single collection of resources in resource groups.</span></span> <span data-ttu-id="67f65-106">Tali risorse vengono gestite tramite diversi provider in Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="67f65-106">Such resources are managed through various resource providers under Resource Manager.</span></span>

<span data-ttu-id="67f65-107">Gestione risorse di Azure si basa su diversi provider tooprovide accesso tooyour di risorse.</span><span class="sxs-lookup"><span data-stu-id="67f65-107">Azure Resource Manager relies on different resource providers tooprovide access tooyour resources.</span></span> <span data-ttu-id="67f65-108">Sono disponibili tre provider di risorse principali: Rete, Archiviazione e Calcolo.</span><span class="sxs-lookup"><span data-stu-id="67f65-108">There are three main resource providers: Network, Storage and Compute.</span></span> <span data-ttu-id="67f65-109">Questo documento vengono illustrate le caratteristiche di hello e i vantaggi di hello Provider di risorse di rete, tra cui:</span><span class="sxs-lookup"><span data-stu-id="67f65-109">This document discusses hello characteristics and benefits of hello Network Resource Provider, including:</span></span>

* <span data-ttu-id="67f65-110">**Metadati** : è possibile aggiungere informazioni tooresources tramite tag.</span><span class="sxs-lookup"><span data-stu-id="67f65-110">**Metadata** – you can add information tooresources using tags.</span></span> <span data-ttu-id="67f65-111">Questi tag possono essere utilizzato tootrack l'utilizzo delle risorse tra le sottoscrizioni e i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="67f65-111">These tags can be used tootrack resource utilization across resource groups and subscriptions.</span></span>
* <span data-ttu-id="67f65-112">**Maggior controllo della rete** : le risorse di rete sono a regime di controllo libero ed è possibile controllarle in modo più granulare.</span><span class="sxs-lookup"><span data-stu-id="67f65-112">**Greater control of your network** - network resources are loosely coupled and you can control them in a more granular fashion.</span></span> <span data-ttu-id="67f65-113">Ciò significa che si dispone di maggiore flessibilità nella gestione delle risorse di rete hello.</span><span class="sxs-lookup"><span data-stu-id="67f65-113">This means you have more flexibility in managing hello networking resources.</span></span>
* <span data-ttu-id="67f65-114">**Configurazione più veloce** : grazie al regime di controllo libero, è possibile creare e orchestrare in parallelo le risorse di rete.</span><span class="sxs-lookup"><span data-stu-id="67f65-114">**Faster configuration** - because network resources are loosely coupled, you can create and orchestrate network resources in parallel.</span></span> <span data-ttu-id="67f65-115">Il tempo di configurazione viene ridotto drasticamente.</span><span class="sxs-lookup"><span data-stu-id="67f65-115">This has drastically reduced configuration time.</span></span>
* <span data-ttu-id="67f65-116">**Controllo di accesso basato su ruoli** -RBAC fornisce i ruoli predefiniti, con ambito di protezione specifiche, nella creazione di hello tooallowing aggiunta di ruoli personalizzati per la gestione della protezione.</span><span class="sxs-lookup"><span data-stu-id="67f65-116">**Role Based Access Control** - RBAC provides default roles, with specific security scope, in addition tooallowing hello creation of custom roles for secure management.</span></span>
* <span data-ttu-id="67f65-117">**Gestione più semplice e distribuzione** -è più facile toodeploy e gestire applicazioni, poiché è possibile creare uno stack di tutta l'applicazione come un unico insieme di risorse in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="67f65-117">**Easier management and deployment** - it’s easier toodeploy and manage applications since you can can create an entire application stack as a single collection of resources in a resource group.</span></span> <span data-ttu-id="67f65-118">E toodeploy più veloce, poiché è possibile distribuire fornendo semplicemente un payload JSON del modello.</span><span class="sxs-lookup"><span data-stu-id="67f65-118">And faster toodeploy, since you can deploy by simply providing a template JSON payload.</span></span>
* <span data-ttu-id="67f65-119">**Personalizzazione rapida** -è possibile utilizzare modelli di uno stile dichiarativo tooenable ripetibili e rapida la personalizzazione delle distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="67f65-119">**Rapid customization** - you can use declarative-style templates tooenable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="67f65-120">**Personalizzazione REPEATABLE** -è possibile utilizzare modelli di uno stile dichiarativo tooenable ripetibili e rapida la personalizzazione delle distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="67f65-120">**Repeatable customization** - you can use declarative-style templates tooenable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="67f65-121">**Le interfacce di gestione** -è possibile utilizzare una delle seguenti interfacce toomanage hello delle risorse:</span><span class="sxs-lookup"><span data-stu-id="67f65-121">**Management interfaces** - you can use any of hello following interfaces toomanage your resources:</span></span>
  * <span data-ttu-id="67f65-122">API basata su REST</span><span class="sxs-lookup"><span data-stu-id="67f65-122">REST based API</span></span>
  * <span data-ttu-id="67f65-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="67f65-123">PowerShell</span></span>
  * <span data-ttu-id="67f65-124">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="67f65-124">.NET SDK</span></span>
  * <span data-ttu-id="67f65-125">Node.JS SDK</span><span class="sxs-lookup"><span data-stu-id="67f65-125">Node.JS SDK</span></span>
  * <span data-ttu-id="67f65-126">SDK per Java</span><span class="sxs-lookup"><span data-stu-id="67f65-126">Java SDK</span></span>
  * <span data-ttu-id="67f65-127">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="67f65-127">Azure CLI</span></span>
  * <span data-ttu-id="67f65-128">Portale di anteprima</span><span class="sxs-lookup"><span data-stu-id="67f65-128">Preview Portal</span></span>
  * <span data-ttu-id="67f65-129">Linguaggio del modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="67f65-129">Resource Manager template language</span></span>

## <a name="network-resources"></a><span data-ttu-id="67f65-130">Risorse di rete</span><span class="sxs-lookup"><span data-stu-id="67f65-130">Network resources</span></span>
<span data-ttu-id="67f65-131">Ora è possibile gestire le risorse di rete in modo indipendente, anziché tutte insieme mediante un'unica risorsa di calcolo (una macchina virtuale).</span><span class="sxs-lookup"><span data-stu-id="67f65-131">You can now manage network resources independently, instead of having them all managed through a single compute resource (a virtual machine).</span></span> <span data-ttu-id="67f65-132">Ciò garantisce una maggiore flessibilità durante la creazione di un'infrastruttura complessa e su larga scala in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="67f65-132">This ensures a higher degree of flexibility and agility in composing a complex and large scale infrastructure in a resource group.</span></span>

<span data-ttu-id="67f65-133">Di seguito è riportata una visualizzazione concettuale di una distribuzione di esempio che interessa un'applicazione multilivello.</span><span class="sxs-lookup"><span data-stu-id="67f65-133">A conceptual view of a sample deployment involving a multi-tiered application is presented below.</span></span> <span data-ttu-id="67f65-134">È possibile gestire in modo indipendente ciascuna risorsa visualizzata, ad esempio schede di rete, indirizzi IP pubblici e VM.</span><span class="sxs-lookup"><span data-stu-id="67f65-134">Each resource you see, such as NICs, public IP addresses, and VMs, can be managed independently.</span></span>

![Modello di risorsa di rete](./media/resource-groups-networking/Figure2.png)

<span data-ttu-id="67f65-136">Ogni risorsa prevede un set comune di proprietà e il proprio set di proprietà.</span><span class="sxs-lookup"><span data-stu-id="67f65-136">Every resource contains a common set of properties, and their individual property set.</span></span> <span data-ttu-id="67f65-137">proprietà comuni Hello sono:</span><span class="sxs-lookup"><span data-stu-id="67f65-137">hello common properties are:</span></span>

| <span data-ttu-id="67f65-138">Proprietà</span><span class="sxs-lookup"><span data-stu-id="67f65-138">Property</span></span> | <span data-ttu-id="67f65-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="67f65-139">Description</span></span> | <span data-ttu-id="67f65-140">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="67f65-140">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="67f65-141">**nome**</span><span class="sxs-lookup"><span data-stu-id="67f65-141">**name**</span></span> |<span data-ttu-id="67f65-142">Nome univoco per le risorse.</span><span class="sxs-lookup"><span data-stu-id="67f65-142">Unique resource name.</span></span> <span data-ttu-id="67f65-143">Ogni tipo di risorsa dispone delle proprie restrizioni di denominazione.</span><span class="sxs-lookup"><span data-stu-id="67f65-143">Each resource type has its own naming restrictions.</span></span> |<span data-ttu-id="67f65-144">PIP01, VM01, NIC01</span><span class="sxs-lookup"><span data-stu-id="67f65-144">PIP01, VM01, NIC01</span></span> |
| <span data-ttu-id="67f65-145">**location**</span><span class="sxs-lookup"><span data-stu-id="67f65-145">**location**</span></span> |<span data-ttu-id="67f65-146">Area di Azure in cui hello risiede risorsa</span><span class="sxs-lookup"><span data-stu-id="67f65-146">Azure region in which hello resource resides</span></span> |<span data-ttu-id="67f65-147">westus, eastus</span><span class="sxs-lookup"><span data-stu-id="67f65-147">westus, eastus</span></span> |
| <span data-ttu-id="67f65-148">**id**</span><span class="sxs-lookup"><span data-stu-id="67f65-148">**id**</span></span> |<span data-ttu-id="67f65-149">Identificazione univoca basata su URI</span><span class="sxs-lookup"><span data-stu-id="67f65-149">Unique URI based identification</span></span> |<span data-ttu-id="67f65-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span><span class="sxs-lookup"><span data-stu-id="67f65-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span></span> |

<span data-ttu-id="67f65-151">È possibile verificare le singole proprietà hello di risorse disponibili nelle sezioni hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="67f65-151">You can check hello individual properties of resources in hello sections below.</span></span>

[!INCLUDE [virtual-networks-nrp-pip-include](../../includes/virtual-networks-nrp-pip-include.md)]

[!INCLUDE [virtual-networks-nrp-nic-include](../../includes/virtual-networks-nrp-nic-include.md)]

[!INCLUDE [virtual-networks-nrp-nsg-include](../../includes/virtual-networks-nrp-nsg-include.md)]

[!INCLUDE [virtual-networks-nrp-udr-include](../../includes/virtual-networks-nrp-udr-include.md)]

[!INCLUDE [virtual-networks-nrp-vnet-include](../../includes/virtual-networks-nrp-vnet-include.md)]

[!INCLUDE [virtual-networks-nrp-dns-include](../../includes/virtual-networks-nrp-dns-include.md)]

[!INCLUDE [virtual-networks-nrp-lb-include](../../includes/virtual-networks-nrp-lb-include.md)]

[!INCLUDE [virtual-networks-nrp-appgw-include](../../includes/virtual-networks-nrp-appgw-include.md)]

[!INCLUDE [virtual-networks-nrp-vpn-include](../../includes/virtual-networks-nrp-vpn-include.md)]

[!INCLUDE [virtual-networks-nrp-tm-include](../../includes/virtual-networks-nrp-tm-include.md)]

## <a name="management-interfaces"></a><span data-ttu-id="67f65-152">Interfacce di gestione</span><span class="sxs-lookup"><span data-stu-id="67f65-152">Management interfaces</span></span>
<span data-ttu-id="67f65-153">È possibile gestire le risorse di rete Azure tramite interfacce diverse.</span><span class="sxs-lookup"><span data-stu-id="67f65-153">You can manage your Azure networking resources using different interfaces.</span></span> <span data-ttu-id="67f65-154">Questo documento è dedicato a tali interfacce: API REST e modelli.</span><span class="sxs-lookup"><span data-stu-id="67f65-154">In this document we will focus on tow of those interfaces: REST API, and templates.</span></span>

### <a name="rest-api"></a><span data-ttu-id="67f65-155">API REST</span><span class="sxs-lookup"><span data-stu-id="67f65-155">REST API</span></span>
<span data-ttu-id="67f65-156">Come accennato in precedenza, le risorse di rete possono essere gestite tramite un'ampia gamma di interfacce, tra cui API REST,.NET SDK, Node.JS SDK, Java SDK, PowerShell, l'interfaccia della riga di comando, il portale di Azure e i modelli.</span><span class="sxs-lookup"><span data-stu-id="67f65-156">As mentioned earlier, network resources can be managed via a variety of interfaces, including REST API,.NET SDK, Node.JS SDK, Java SDK, PowerShell, CLI, Azure Portal and templates.</span></span>

<span data-ttu-id="67f65-157">API Rest di Hello conforme toohello specifica del protocollo HTTP 1.1.</span><span class="sxs-lookup"><span data-stu-id="67f65-157">hello Rest API’s conform toohello HTTP 1.1 protocol specification.</span></span> <span data-ttu-id="67f65-158">struttura URI generale Hello di hello API viene presentata di seguito:</span><span class="sxs-lookup"><span data-stu-id="67f65-158">hello general URI structure of hello API is presented below:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

<span data-ttu-id="67f65-159">Hello parametri e parentesi graffe rappresentano hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="67f65-159">And hello parameters in braces represent hello following elements:</span></span>

* <span data-ttu-id="67f65-160">**subscription-id** : ID sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="67f65-160">**subscription-id** - your Azure subscription id.</span></span>
* <span data-ttu-id="67f65-161">**Resource-provider-namespace** -spazio dei nomi per i provider di hello in uso.</span><span class="sxs-lookup"><span data-stu-id="67f65-161">**resource-provider-namespace** - namespace for hello provider being used.</span></span> <span data-ttu-id="67f65-162">il valore di Hello per provider di risorse di rete hello è *Network*.</span><span class="sxs-lookup"><span data-stu-id="67f65-162">hello value for hello network resource provider is *Microsoft.Network*.</span></span>
* <span data-ttu-id="67f65-163">**nome dell'area** -nome dell'area di Azure hello</span><span class="sxs-lookup"><span data-stu-id="67f65-163">**region-name** - hello Azure region name</span></span>

<span data-ttu-id="67f65-164">metodi HTTP seguenti Hello sono supportati quando si apportano toohello chiamate API REST:</span><span class="sxs-lookup"><span data-stu-id="67f65-164">hello following HTTP methods are supported when making calls toohello REST API:</span></span>

* <span data-ttu-id="67f65-165">**INSERIRE** : utilizzato toocreate una risorsa di un determinato tipo, modificare una proprietà della risorsa o modificare un'associazione tra le risorse.</span><span class="sxs-lookup"><span data-stu-id="67f65-165">**PUT** - used toocreate a resource of a given type, modify a resource property or change an association between resources.</span></span>
* <span data-ttu-id="67f65-166">**OTTENERE** -usare tooretrieve informazioni per una risorsa di provisioning.</span><span class="sxs-lookup"><span data-stu-id="67f65-166">**GET** - used tooretrieve information for a provisioned resource.</span></span>
* <span data-ttu-id="67f65-167">**ELIMINARE** -utilizzato toodelete una risorsa esistente.</span><span class="sxs-lookup"><span data-stu-id="67f65-167">**DELETE** - used toodelete an existing resource.</span></span>

<span data-ttu-id="67f65-168">Richiesta di hello e di risposta conforme tooa formato di payload JSON.</span><span class="sxs-lookup"><span data-stu-id="67f65-168">Both hello request and response conform tooa JSON payload format.</span></span> <span data-ttu-id="67f65-169">Per altre informazioni, vedere [API di gestione delle risorse di Azure](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span><span class="sxs-lookup"><span data-stu-id="67f65-169">For more details, see [Azure Resource Management APIs](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span></span>

### <a name="resource-manager-template-language"></a><span data-ttu-id="67f65-170">Linguaggio del modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="67f65-170">Resource Manager template language</span></span>
<span data-ttu-id="67f65-171">Nelle risorse di toomanaging aggiunta in modo imperativo (tramite le API o il SDK), è inoltre possibile utilizzare un toobuild di stile di programmazione dichiarativa e gestire le risorse di rete tramite hello linguaggio del modello di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="67f65-171">In addition toomanaging resources imperatively (via APIs or SDK), you can also use a declarative programming style toobuild and manage network resources by using hello Resource Manager Template Language.</span></span>

<span data-ttu-id="67f65-172">Di seguito viene fornita una rappresentazione di un modello:</span><span class="sxs-lookup"><span data-stu-id="67f65-172">A sample representation of a template is provided below –</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

<span data-ttu-id="67f65-173">modello di Hello è principalmente una descrizione JSON delle risorse di hello e i valori delle istanze hello inseriti tramite i parametri.</span><span class="sxs-lookup"><span data-stu-id="67f65-173">hello template is primarily a JSON description of hello resources and hello instance values injected via parameters.</span></span> <span data-ttu-id="67f65-174">esempio Hello seguente può essere utilizzato toocreate una rete virtuale con 2 subnet.</span><span class="sxs-lookup"><span data-stu-id="67f65-174">hello example below can be used toocreate a virtual network with 2 subnets.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/VNET.json",
        "contentVersion": "1.0.0.0",
        "parameters" : {
          "location": {
            "type": "String",
            "allowedValues": ["East US", "West US", "West Europe", "East Asia", "South East Asia"],
            "metadata" : {
              "Description" : "Deployment location"
            }
          },
          "virtualNetworkName":{
            "type" : "string",
            "defaultValue":"myVNET",
            "metadata" : {
              "Description" : "VNET name"
            }
          },
          "addressPrefix":{
            "type" : "string",
            "defaultValue" : "10.0.0.0/16",
            "metadata" : {
              "Description" : "Address prefix"
            }

          },
          "subnet1Name": {
            "type" : "string",
            "defaultValue" : "Subnet-1",
            "metadata" : {
              "Description" : "Subnet 1 Name"
            }
          },
          "subnet2Name": {
            "type" : "string",
            "defaultValue" : "Subnet-2",
            "metadata" : {
              "Description" : "Subnet 2 name"
            }
          },
          "subnet1Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.0.0/24",
            "metadata" : {
              "Description" : "Subnet 1 Prefix"
            }
          },
          "subnet2Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.1.0/24",
            "metadata" : {
              "Description" : "Subnet 2 Prefix"
            }
          }
        },
        "resources": [
        {
          "apiVersion": "2015-05-01-preview",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "[parameters('virtualNetworkName')]",
          "location": "[parameters('location')]",
          "properties": {
            "addressSpace": {
              "addressPrefixes": [
                "[parameters('addressPrefix')]"
              ]
            },
            "subnets": [
              {
                "name": "[parameters('subnet1Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet1Prefix')]"
                }
              },
              {
                "name": "[parameters('subnet2Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet2Prefix')]"
                }
              }
            ]
          }
        }
        ]
    }

<span data-ttu-id="67f65-175">È possibile hello fornendo i valori dei parametri hello manualmente quando si utilizza un modello oppure è possibile utilizzare un file di parametri.</span><span class="sxs-lookup"><span data-stu-id="67f65-175">You have hello option of providing hello parameter values manually when using a template, or you can use a parameter file.</span></span> <span data-ttu-id="67f65-176">esempio Hello seguente mostra un possibile insieme di toobe di valori di parametro utilizzato con il modello di hello precedente:</span><span class="sxs-lookup"><span data-stu-id="67f65-176">hello example below shows a possible set of parameter values toobe used with hello template above:</span></span>

    {
      "location": {
          "value": "East US"
      },
      "virtualNetworkName": {
          "value": "VNET1"
      },
      "subnet1Name": {
          "value": "Subnet1"
      },
      "subnet2Name": {
          "value": "Subnet2"
      },
      "addressPrefix": {
          "value": "192.168.0.0/16"
      },
      "subnet1Prefix": {
          "value": "192.168.1.0/24"
      },
      "subnet2Prefix": {
          "value": "192.168.2.0/24"
      }
    }


<span data-ttu-id="67f65-177">vantaggi principali di Hello dell'utilizzo di modelli sono:</span><span class="sxs-lookup"><span data-stu-id="67f65-177">hello main advantages of using templates are:</span></span>

* <span data-ttu-id="67f65-178">È possibile compilare un'infrastruttura complessa in un gruppo di risorse con uno stile dichiarativo.</span><span class="sxs-lookup"><span data-stu-id="67f65-178">You can build a complex infrastructure in a resource group in a declarative style.</span></span> <span data-ttu-id="67f65-179">Hello orchestrazione di creazione di risorse di hello, incluse la gestione delle dipendenze, viene gestita dal gestore delle risorse.</span><span class="sxs-lookup"><span data-stu-id="67f65-179">hello orchestration of creating hello resources, including dependency management, is handled by Resource Manager.</span></span>
* <span data-ttu-id="67f65-180">infrastruttura Hello può essere creata in modo ripetibile in diverse aree geografiche e all'interno di un'area semplicemente modificando i parametri.</span><span class="sxs-lookup"><span data-stu-id="67f65-180">hello infrastructure can be created in a repeatable way across various regions and within a region by simply changing parameters.</span></span>
* <span data-ttu-id="67f65-181">uno stile dichiarativo Hello lead tooshorter lead time di compilazione di modelli hello e il rollout infrastruttura hello.</span><span class="sxs-lookup"><span data-stu-id="67f65-181">hello declarative style leads tooshorter lead time in building hello templates and rolling out hello infrastructure.</span></span>

<span data-ttu-id="67f65-182">Per i modelli di esempio, vedere i [modelli della guida introduttiva di Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="67f65-182">For sample templates, see [Azure quickstart templates](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="67f65-183">Per ulteriori informazioni su hello linguaggio del modello di gestione risorse, vedere [linguaggio del modello di gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="67f65-183">For more information on hello Resource Manager Template Language, see [Azure Resource Manager Template Language](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="67f65-184">modello di esempio Hello precedente Usa la rete virtuale hello e le risorse subnet.</span><span class="sxs-lookup"><span data-stu-id="67f65-184">hello sample template above uses hello virtual network and subnet resources.</span></span> <span data-ttu-id="67f65-185">È possibile usare altre risorse di rete, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="67f65-185">There are other network resources you can use as listed below:</span></span>

### <a name="using-a-template"></a><span data-ttu-id="67f65-186">Uso di un modello</span><span class="sxs-lookup"><span data-stu-id="67f65-186">Using a template</span></span>
<span data-ttu-id="67f65-187">È possibile distribuire servizi tooAzure da un modello usando PowerShell, AzureCLI, oppure eseguendo un toodeploy fare clic su da GitHub.</span><span class="sxs-lookup"><span data-stu-id="67f65-187">You can deploy services tooAzure from a template by using PowerShell, AzureCLI, or by performing a click toodeploy from GitHub.</span></span> <span data-ttu-id="67f65-188">servizi toodeploy da un modello in GitHub, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="67f65-188">toodeploy services from a template in GitHub, execute hello following steps:</span></span>

1. <span data-ttu-id="67f65-189">Aprire il file di template3 hello da GitHub.</span><span class="sxs-lookup"><span data-stu-id="67f65-189">Open hello template3 file from GitHub.</span></span> <span data-ttu-id="67f65-190">Come esempio, aprire [Rete virtuale con due subnet](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="67f65-190">As an example, open [Virtual network with two subnets](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span></span>
2. <span data-ttu-id="67f65-191">Fare clic su **distribuire tooAzure**e quindi accedere a toohello portale di Azure con le credenziali.</span><span class="sxs-lookup"><span data-stu-id="67f65-191">Click on **Deploy tooAzure**, and then sign in on toohello Azure portal with your credentials.</span></span>
3. <span data-ttu-id="67f65-192">Verificare il modello di hello e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="67f65-192">Verify hello template, and then click **Save**.</span></span>
4. <span data-ttu-id="67f65-193">Fare clic su **modificare parametri** e selezionare un percorso, ad esempio *Stati Uniti occidentali*, per la rete virtuale hello e le subnet.</span><span class="sxs-lookup"><span data-stu-id="67f65-193">Click **Edit parameters** and select a location, such as *West US*, for hello vnet and subnets.</span></span>
5. <span data-ttu-id="67f65-194">Se necessario, modificare hello **ADDRESSPREFIX** e **SUBNETPREFIX** parametri e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="67f65-194">If necessary, change hello **ADDRESSPREFIX** and **SUBNETPREFIX** parameters, and then click **OK**.</span></span>
6. <span data-ttu-id="67f65-195">Fare clic su **selezionare un gruppo di risorse** e quindi fare clic sul gruppo di risorse hello da rete virtuale hello tooadd e subnet ai.</span><span class="sxs-lookup"><span data-stu-id="67f65-195">Click **Select a resource group** and then click on hello resource group you want tooadd hello vnet and subnets to.</span></span> <span data-ttu-id="67f65-196">In alternativa, è possibile creare un nuovo gruppo di risorse facendo clic su **Crea nuovo**.</span><span class="sxs-lookup"><span data-stu-id="67f65-196">Alternatively, you can create a new resource group by clicking **Or create new**.</span></span>
7. <span data-ttu-id="67f65-197">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="67f65-197">Click **Create**.</span></span> <span data-ttu-id="67f65-198">Si noti hello riquadro visualizzazione **distribuzione del modello di Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="67f65-198">Notice hello tile displaying **Provisioning Template deployment**.</span></span> <span data-ttu-id="67f65-199">Una volta hello distribuzione viene eseguita, si noterà tooone simile a schermata riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="67f65-199">Once hello deployment is done, you will see a screen similar tooone below.</span></span>

![Distribuzione del modello di esempio](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a><span data-ttu-id="67f65-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="67f65-201">Next steps</span></span>
[<span data-ttu-id="67f65-202">Linguaggio del modello di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="67f65-202">Azure Resource Manager Template Language</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[<span data-ttu-id="67f65-203">Rete di Azure: modelli di uso comune</span><span class="sxs-lookup"><span data-stu-id="67f65-203">Azure Networking – commonly used templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

[<span data-ttu-id="67f65-204">Distribuzione Azure Resource Manager o classica</span><span class="sxs-lookup"><span data-stu-id="67f65-204">Azure Resource Manager vs. classic deployment</span></span>](../azure-resource-manager/resource-manager-deployment-model.md)

[<span data-ttu-id="67f65-205">Panoramica di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="67f65-205">Azure Resource Manager Overview</span></span>](../azure-resource-manager/resource-group-overview.md)

