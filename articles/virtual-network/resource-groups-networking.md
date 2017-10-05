---
title: Panoramica di Provider di risorse di rete | Documentazione Microsoft
description: Introduzione al nuovo Provider di risorse di rete in Gestione risorse di Azure
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
ms.openlocfilehash: 2428c707ddeed281fddd1e57bc5574603f0b9b1c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="network-resource-provider"></a><span data-ttu-id="fa6b0-103">Provider di risorse di rete</span><span class="sxs-lookup"><span data-stu-id="fa6b0-103">Network Resource Provider</span></span>
<span data-ttu-id="fa6b0-104">Un fattore essenziale per il successo di un'azienda è la possibilità di creare e gestire applicazioni presenti in rete su larga scala in modo agile, flessibile, sicuro e ripetibile.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-104">An underpinning need in today’s business success, is the ability to build and manage large scale network aware applications in an agile, flexible, secure and repeatable way.</span></span> <span data-ttu-id="fa6b0-105">Azure Resource Manager consente di creare tali applicazioni come unica raccolta di risorse nei gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-105">Azure Resource Manager enables you to create such applications, as a single collection of resources in resource groups.</span></span> <span data-ttu-id="fa6b0-106">Tali risorse vengono gestite tramite diversi provider in Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-106">Such resources are managed through various resource providers under Resource Manager.</span></span>

<span data-ttu-id="fa6b0-107">Gestione risorse di Azure si basa su diversi provider di risorse per fornire l'accesso alle risorse.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-107">Azure Resource Manager relies on different resource providers to provide access to your resources.</span></span> <span data-ttu-id="fa6b0-108">Sono disponibili tre provider di risorse principali: Rete, Archiviazione e Calcolo.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-108">There are three main resource providers: Network, Storage and Compute.</span></span> <span data-ttu-id="fa6b0-109">In questo documento vengono illustrate le caratteristiche e i vantaggi del Provider di risorse di rete, tra cui:</span><span class="sxs-lookup"><span data-stu-id="fa6b0-109">This document discusses the characteristics and benefits of the Network Resource Provider, including:</span></span>

* <span data-ttu-id="fa6b0-110">**Metadati** : le informazioni alle risorse possono essere aggiunte usando i tag.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-110">**Metadata** – you can add information to resources using tags.</span></span> <span data-ttu-id="fa6b0-111">Questi tag possono essere usati per tenere traccia dell'utilizzo delle risorse tra le sottoscrizioni e i gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-111">These tags can be used to track resource utilization across resource groups and subscriptions.</span></span>
* <span data-ttu-id="fa6b0-112">**Maggior controllo della rete** : le risorse di rete sono a regime di controllo libero ed è possibile controllarle in modo più granulare.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-112">**Greater control of your network** - network resources are loosely coupled and you can control them in a more granular fashion.</span></span> <span data-ttu-id="fa6b0-113">Questo consente una maggiore flessibilità nella gestione delle risorse di rete.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-113">This means you have more flexibility in managing the networking resources.</span></span>
* <span data-ttu-id="fa6b0-114">**Configurazione più veloce** : grazie al regime di controllo libero, è possibile creare e orchestrare in parallelo le risorse di rete.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-114">**Faster configuration** - because network resources are loosely coupled, you can create and orchestrate network resources in parallel.</span></span> <span data-ttu-id="fa6b0-115">Il tempo di configurazione viene ridotto drasticamente.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-115">This has drastically reduced configuration time.</span></span>
* <span data-ttu-id="fa6b0-116">**Controllo degli accessi in base al ruolo** : questa funzionalità fornisce ruoli predefiniti con uno specifico ambito di sicurezza, oltre a consentire la creazione di ruoli personalizzati per una gestione sicura.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-116">**Role Based Access Control** - RBAC provides default roles, with specific security scope, in addition to allowing the creation of custom roles for secure management.</span></span>
* <span data-ttu-id="fa6b0-117">**Gestione e distribuzione più semplice** : la distribuzione e la gestione delle applicazioni è più semplice perché è possibile creare un intero stack di applicazioni sotto forma di un'unica raccolta di risorse in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-117">**Easier management and deployment** - it’s easier to deploy and manage applications since you can can create an entire application stack as a single collection of resources in a resource group.</span></span> <span data-ttu-id="fa6b0-118">Inoltre, la distribuzione risulta più rapida perché è possibile eseguirla semplicemente fornendo un payload JSON del modello.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-118">And faster to deploy, since you can deploy by simply providing a template JSON payload.</span></span>
* <span data-ttu-id="fa6b0-119">**Personalizzazione rapida** : è possibile usare modelli con stile dichiarativo per abilitare la personalizzazione ripetibile e rapida delle distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-119">**Rapid customization** - you can use declarative-style templates to enable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="fa6b0-120">**Personalizzazione ripetibile** : è possibile usare modelli con stile dichiarativo per abilitare la personalizzazione ripetibile e rapida delle distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-120">**Repeatable customization** - you can use declarative-style templates to enable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="fa6b0-121">**Interfacce di gestione** - è possibile gestire le risorse usando una delle seguenti interfacce:</span><span class="sxs-lookup"><span data-stu-id="fa6b0-121">**Management interfaces** - you can use any of the following interfaces to manage your resources:</span></span>
  * <span data-ttu-id="fa6b0-122">API basata su REST</span><span class="sxs-lookup"><span data-stu-id="fa6b0-122">REST based API</span></span>
  * <span data-ttu-id="fa6b0-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa6b0-123">PowerShell</span></span>
  * <span data-ttu-id="fa6b0-124">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="fa6b0-124">.NET SDK</span></span>
  * <span data-ttu-id="fa6b0-125">Node.JS SDK</span><span class="sxs-lookup"><span data-stu-id="fa6b0-125">Node.JS SDK</span></span>
  * <span data-ttu-id="fa6b0-126">SDK per Java</span><span class="sxs-lookup"><span data-stu-id="fa6b0-126">Java SDK</span></span>
  * <span data-ttu-id="fa6b0-127">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="fa6b0-127">Azure CLI</span></span>
  * <span data-ttu-id="fa6b0-128">Portale di anteprima</span><span class="sxs-lookup"><span data-stu-id="fa6b0-128">Preview Portal</span></span>
  * <span data-ttu-id="fa6b0-129">Linguaggio del modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fa6b0-129">Resource Manager template language</span></span>

## <a name="network-resources"></a><span data-ttu-id="fa6b0-130">Risorse di rete</span><span class="sxs-lookup"><span data-stu-id="fa6b0-130">Network resources</span></span>
<span data-ttu-id="fa6b0-131">Ora è possibile gestire le risorse di rete in modo indipendente, anziché tutte insieme mediante un'unica risorsa di calcolo (una macchina virtuale).</span><span class="sxs-lookup"><span data-stu-id="fa6b0-131">You can now manage network resources independently, instead of having them all managed through a single compute resource (a virtual machine).</span></span> <span data-ttu-id="fa6b0-132">Ciò garantisce una maggiore flessibilità durante la creazione di un'infrastruttura complessa e su larga scala in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-132">This ensures a higher degree of flexibility and agility in composing a complex and large scale infrastructure in a resource group.</span></span>

<span data-ttu-id="fa6b0-133">Di seguito è riportata una visualizzazione concettuale di una distribuzione di esempio che interessa un'applicazione multilivello.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-133">A conceptual view of a sample deployment involving a multi-tiered application is presented below.</span></span> <span data-ttu-id="fa6b0-134">È possibile gestire in modo indipendente ciascuna risorsa visualizzata, ad esempio schede di rete, indirizzi IP pubblici e VM.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-134">Each resource you see, such as NICs, public IP addresses, and VMs, can be managed independently.</span></span>

![Modello di risorsa di rete](./media/resource-groups-networking/Figure2.png)

<span data-ttu-id="fa6b0-136">Ogni risorsa prevede un set comune di proprietà e il proprio set di proprietà.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-136">Every resource contains a common set of properties, and their individual property set.</span></span> <span data-ttu-id="fa6b0-137">Ecco le proprietà comuni:</span><span class="sxs-lookup"><span data-stu-id="fa6b0-137">The common properties are:</span></span>

| <span data-ttu-id="fa6b0-138">Proprietà</span><span class="sxs-lookup"><span data-stu-id="fa6b0-138">Property</span></span> | <span data-ttu-id="fa6b0-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="fa6b0-139">Description</span></span> | <span data-ttu-id="fa6b0-140">Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="fa6b0-140">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fa6b0-141">**nome**</span><span class="sxs-lookup"><span data-stu-id="fa6b0-141">**name**</span></span> |<span data-ttu-id="fa6b0-142">Nome univoco per le risorse.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-142">Unique resource name.</span></span> <span data-ttu-id="fa6b0-143">Ogni tipo di risorsa dispone delle proprie restrizioni di denominazione.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-143">Each resource type has its own naming restrictions.</span></span> |<span data-ttu-id="fa6b0-144">PIP01, VM01, NIC01</span><span class="sxs-lookup"><span data-stu-id="fa6b0-144">PIP01, VM01, NIC01</span></span> |
| <span data-ttu-id="fa6b0-145">**Località**</span><span class="sxs-lookup"><span data-stu-id="fa6b0-145">**location**</span></span> |<span data-ttu-id="fa6b0-146">Area di Azure in cui sarà creata la VM.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-146">Azure region in which the resource resides</span></span> |<span data-ttu-id="fa6b0-147">westus, eastus</span><span class="sxs-lookup"><span data-stu-id="fa6b0-147">westus, eastus</span></span> |
| <span data-ttu-id="fa6b0-148">**id**</span><span class="sxs-lookup"><span data-stu-id="fa6b0-148">**id**</span></span> |<span data-ttu-id="fa6b0-149">Identificazione univoca basata su URI</span><span class="sxs-lookup"><span data-stu-id="fa6b0-149">Unique URI based identification</span></span> |<span data-ttu-id="fa6b0-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span><span class="sxs-lookup"><span data-stu-id="fa6b0-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span></span> |

<span data-ttu-id="fa6b0-151">È possibile controllare le proprietà delle singole risorse nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-151">You can check the individual properties of resources in the sections below.</span></span>

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

## <a name="management-interfaces"></a><span data-ttu-id="fa6b0-152">Interfacce di gestione</span><span class="sxs-lookup"><span data-stu-id="fa6b0-152">Management interfaces</span></span>
<span data-ttu-id="fa6b0-153">È possibile gestire le risorse di rete Azure tramite interfacce diverse.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-153">You can manage your Azure networking resources using different interfaces.</span></span> <span data-ttu-id="fa6b0-154">Questo documento è dedicato a tali interfacce: API REST e modelli.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-154">In this document we will focus on tow of those interfaces: REST API, and templates.</span></span>

### <a name="rest-api"></a><span data-ttu-id="fa6b0-155">API REST</span><span class="sxs-lookup"><span data-stu-id="fa6b0-155">REST API</span></span>
<span data-ttu-id="fa6b0-156">Come accennato in precedenza, le risorse di rete possono essere gestite tramite un'ampia gamma di interfacce, tra cui API REST,.NET SDK, Node.JS SDK, Java SDK, PowerShell, l'interfaccia della riga di comando, il portale di Azure e i modelli.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-156">As mentioned earlier, network resources can be managed via a variety of interfaces, including REST API,.NET SDK, Node.JS SDK, Java SDK, PowerShell, CLI, Azure Portal and templates.</span></span>

<span data-ttu-id="fa6b0-157">L'API REST è conforme alla specifica del protocollo HTTP 1.1.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-157">The Rest API’s conform to the HTTP 1.1 protocol specification.</span></span> <span data-ttu-id="fa6b0-158">La struttura generale degli URI dell'API viene presentata di seguito:</span><span class="sxs-lookup"><span data-stu-id="fa6b0-158">The general URI structure of the API is presented below:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

<span data-ttu-id="fa6b0-159">E i parametri tra parentesi graffe rappresentano gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa6b0-159">And the parameters in braces represent the following elements:</span></span>

* <span data-ttu-id="fa6b0-160">**subscription-id** : ID sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-160">**subscription-id** - your Azure subscription id.</span></span>
* <span data-ttu-id="fa6b0-161">**resource-provider-namespace** : spazio dei nomi per il provider usato.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-161">**resource-provider-namespace** - namespace for the provider being used.</span></span> <span data-ttu-id="fa6b0-162">Il valore per il provider di risorse di rete è *Microsoft.Network*.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-162">THe value for the network resource provider is *Microsoft.Network*.</span></span>
* <span data-ttu-id="fa6b0-163">**region-name** : nome dell'area di Azure</span><span class="sxs-lookup"><span data-stu-id="fa6b0-163">**region-name** - the Azure region name</span></span>

<span data-ttu-id="fa6b0-164">Quando si effettuano chiamate all'API REST sono supportati i seguenti metodi HTTP:</span><span class="sxs-lookup"><span data-stu-id="fa6b0-164">The following HTTP methods are supported when making calls to the REST API:</span></span>

* <span data-ttu-id="fa6b0-165">**PUT** : usato per creare una risorsa di un determinato tipo, modificare una proprietà della risorsa o modificare un'associazione tra le risorse.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-165">**PUT** - used to create a resource of a given type, modify a resource property or change an association between resources.</span></span>
* <span data-ttu-id="fa6b0-166">**GET** : usato per recuperare le informazioni per una risorsa con provisioning.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-166">**GET** - used to retrieve information for a provisioned resource.</span></span>
* <span data-ttu-id="fa6b0-167">**DELETE** : usato per eliminare una risorsa esistente.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-167">**DELETE** - used to delete an existing resource.</span></span>

<span data-ttu-id="fa6b0-168">Richiesta e risposta sono conformi a un formato di payload JSON.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-168">Both the request and response conform to a JSON payload format.</span></span> <span data-ttu-id="fa6b0-169">Per altre informazioni, vedere [API di gestione delle risorse di Azure](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span><span class="sxs-lookup"><span data-stu-id="fa6b0-169">For more details, see [Azure Resource Management APIs](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span></span>

### <a name="resource-manager-template-language"></a><span data-ttu-id="fa6b0-170">Linguaggio del modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fa6b0-170">Resource Manager template language</span></span>
<span data-ttu-id="fa6b0-171">Oltre a gestire le risorse in modo imperativo (tramite API o SDK), è anche possibile usare uno stile di programmazione dichiarativo per compilare e gestire le risorse di rete tramite il linguaggio del modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-171">In addition to managing resources imperatively (via APIs or SDK), you can also use a declarative programming style to build and manage network resources by using the Resource Manager Template Language.</span></span>

<span data-ttu-id="fa6b0-172">Di seguito viene fornita una rappresentazione di un modello:</span><span class="sxs-lookup"><span data-stu-id="fa6b0-172">A sample representation of a template is provided below –</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

<span data-ttu-id="fa6b0-173">Il modello è principalmente una descrizione JSON delle risorse e dei valori dell'istanza inseriti tramite i parametri.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-173">The template is primarily a JSON description of the resources and the instance values injected via parameters.</span></span> <span data-ttu-id="fa6b0-174">L'esempio seguente può essere usato per creare una rete virtuale con due subnet.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-174">The example below can be used to create a virtual network with 2 subnets.</span></span>

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

<span data-ttu-id="fa6b0-175">Quando si usa un modello è possibile specificare manualmente i valori dei parametri oppure usare un file dei parametri.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-175">You have the option of providing the parameter values manually when using a template, or you can use a parameter file.</span></span> <span data-ttu-id="fa6b0-176">L'esempio seguente mostra un possibile set di valori dei parametri da usare con il modello precedente:</span><span class="sxs-lookup"><span data-stu-id="fa6b0-176">The example below shows a possible set of parameter values to be used with the template above:</span></span>

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


<span data-ttu-id="fa6b0-177">I principali vantaggi associati all'uso dei modelli sono:</span><span class="sxs-lookup"><span data-stu-id="fa6b0-177">The main advantages of using templates are:</span></span>

* <span data-ttu-id="fa6b0-178">È possibile compilare un'infrastruttura complessa in un gruppo di risorse con uno stile dichiarativo.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-178">You can build a complex infrastructure in a resource group in a declarative style.</span></span> <span data-ttu-id="fa6b0-179">L'orchestrazione per la creazione delle risorse, inclusa la gestione delle dipendenze, viene gestita da Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-179">The orchestration of creating the resources, including dependency management, is handled by Resource Manager.</span></span>
* <span data-ttu-id="fa6b0-180">È possibile creare l'infrastruttura in modo ripetibile in diverse aree e all'interno di una sola area modificando semplicemente i parametri.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-180">The infrastructure can be created in a repeatable way across various regions and within a region by simply changing parameters.</span></span>
* <span data-ttu-id="fa6b0-181">Lo stile dichiarativo consente tempi più brevi per la compilazione dei modelli e la distribuzione dell'infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-181">The declarative style leads to shorter lead time in building the templates and rolling out the infrastructure.</span></span>

<span data-ttu-id="fa6b0-182">Per i modelli di esempio, vedere i [modelli della guida introduttiva di Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="fa6b0-182">For sample templates, see [Azure quickstart templates](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="fa6b0-183">Per altre informazioni sul linguaggio del modello di Resource Manager, vedere [Azure Resource Manager Template Language](../azure-resource-manager/resource-group-authoring-templates.md) (Linguaggio del modello di Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="fa6b0-183">For more information on the Resource Manager Template Language, see [Azure Resource Manager Template Language](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="fa6b0-184">Il modello di esempio precedente usa la rete virtuale e le risorse della subnet.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-184">The sample template above uses the virtual network and subnet resources.</span></span> <span data-ttu-id="fa6b0-185">È possibile usare altre risorse di rete, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="fa6b0-185">There are other network resources you can use as listed below:</span></span>

### <a name="using-a-template"></a><span data-ttu-id="fa6b0-186">Uso di un modello</span><span class="sxs-lookup"><span data-stu-id="fa6b0-186">Using a template</span></span>
<span data-ttu-id="fa6b0-187">È possibile distribuire servizi ad Azure da un modello tramite PowerShell, l'interfaccia della riga di comando di Azure oppure tramite clic per la distribuzione da GitHub.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-187">You can deploy services to Azure from a template by using PowerShell, AzureCLI, or by performing a click to deploy from GitHub.</span></span> <span data-ttu-id="fa6b0-188">Per distribuire servizi da un modello in GitHub, eseguire i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="fa6b0-188">To deploy services from a template in GitHub, execute the following steps:</span></span>

1. <span data-ttu-id="fa6b0-189">Aprire il file template3 da GitHub.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-189">Open the template3 file from GitHub.</span></span> <span data-ttu-id="fa6b0-190">Come esempio, aprire [Rete virtuale con due subnet](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="fa6b0-190">As an example, open [Virtual network with two subnets](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span></span>
2. <span data-ttu-id="fa6b0-191">Fare clic su **Distribuisci in Azure**, quindi accedere al portale di Azure con le proprie credenziali.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-191">Click on **Deploy to Azure**, and then sign in on to the Azure portal with your credentials.</span></span>
3. <span data-ttu-id="fa6b0-192">Verificare il modello e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-192">Verify the template, and then click **Save**.</span></span>
4. <span data-ttu-id="fa6b0-193">Fare clic su **Modifica parametri** e selezionare una località, ad esempio *West US*, per la rete virtuale e le subnet.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-193">Click **Edit parameters** and select a location, such as *West US*, for the vnet and subnets.</span></span>
5. <span data-ttu-id="fa6b0-194">Se necessario, modificare i parametri **ADDRESSPREFIX** e **SUBNETPREFIX** e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-194">If necessary, change the **ADDRESSPREFIX** and **SUBNETPREFIX** parameters, and then click **OK**.</span></span>
6. <span data-ttu-id="fa6b0-195">Fare clic su **Seleziona un gruppo di risorse** e quindi fare clic sul gruppo di risorse a cui si desidera aggiungere la rete virtuale e le subnet.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-195">Click **Select a resource group** and then click on the resource group you want to add the vnet and subnets to.</span></span> <span data-ttu-id="fa6b0-196">In alternativa, è possibile creare un nuovo gruppo di risorse facendo clic su **Crea nuovo**.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-196">Alternatively, you can create a new resource group by clicking **Or create new**.</span></span>
7. <span data-ttu-id="fa6b0-197">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-197">Click **Create**.</span></span> <span data-ttu-id="fa6b0-198">Si noti il riquadro che visualizza la **distribuzione del modello di provisioning**.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-198">Notice the tile displaying **Provisioning Template deployment**.</span></span> <span data-ttu-id="fa6b0-199">Dopo aver eseguito la distribuzione, viene visualizzata una schermata simile alla seguente.</span><span class="sxs-lookup"><span data-stu-id="fa6b0-199">Once the deployment is done, you will see a screen similar to one below.</span></span>

![Distribuzione del modello di esempio](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a><span data-ttu-id="fa6b0-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fa6b0-201">Next steps</span></span>
[<span data-ttu-id="fa6b0-202">Linguaggio del modello di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="fa6b0-202">Azure Resource Manager Template Language</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[<span data-ttu-id="fa6b0-203">Rete di Azure: modelli di uso comune</span><span class="sxs-lookup"><span data-stu-id="fa6b0-203">Azure Networking – commonly used templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

[<span data-ttu-id="fa6b0-204">Distribuzione Azure Resource Manager o classica</span><span class="sxs-lookup"><span data-stu-id="fa6b0-204">Azure Resource Manager vs. classic deployment</span></span>](../azure-resource-manager/resource-manager-deployment-model.md)

[<span data-ttu-id="fa6b0-205">Panoramica di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fa6b0-205">Azure Resource Manager Overview</span></span>](../azure-resource-manager/resource-group-overview.md)

