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
# <a name="network-resource-provider"></a>Provider di risorse di rete
Un'esigenza supplementare in successo aziendale attuali, è hello toobuild possibilità e gestire applicazioni di rete su larga scala in un modo agile, flessibile, sicuro e ripetibile. Gestione risorse di Azure consente si toocreate tali applicazioni, come un unico insieme di risorse in gruppi di risorse. Tali risorse vengono gestite tramite diversi provider in Resource Manager.

Gestione risorse di Azure si basa su diversi provider tooprovide accesso tooyour di risorse. Sono disponibili tre provider di risorse principali: Rete, Archiviazione e Calcolo. Questo documento vengono illustrate le caratteristiche di hello e i vantaggi di hello Provider di risorse di rete, tra cui:

* **Metadati** : è possibile aggiungere informazioni tooresources tramite tag. Questi tag possono essere utilizzato tootrack l'utilizzo delle risorse tra le sottoscrizioni e i gruppi di risorse.
* **Maggior controllo della rete** : le risorse di rete sono a regime di controllo libero ed è possibile controllarle in modo più granulare. Ciò significa che si dispone di maggiore flessibilità nella gestione delle risorse di rete hello.
* **Configurazione più veloce** : grazie al regime di controllo libero, è possibile creare e orchestrare in parallelo le risorse di rete. Il tempo di configurazione viene ridotto drasticamente.
* **Controllo di accesso basato su ruoli** -RBAC fornisce i ruoli predefiniti, con ambito di protezione specifiche, nella creazione di hello tooallowing aggiunta di ruoli personalizzati per la gestione della protezione.
* **Gestione più semplice e distribuzione** -è più facile toodeploy e gestire applicazioni, poiché è possibile creare uno stack di tutta l'applicazione come un unico insieme di risorse in un gruppo di risorse. E toodeploy più veloce, poiché è possibile distribuire fornendo semplicemente un payload JSON del modello.
* **Personalizzazione rapida** -è possibile utilizzare modelli di uno stile dichiarativo tooenable ripetibili e rapida la personalizzazione delle distribuzioni.
* **Personalizzazione REPEATABLE** -è possibile utilizzare modelli di uno stile dichiarativo tooenable ripetibili e rapida la personalizzazione delle distribuzioni.
* **Le interfacce di gestione** -è possibile utilizzare una delle seguenti interfacce toomanage hello delle risorse:
  * API basata su REST
  * PowerShell
  * .NET SDK
  * Node.JS SDK
  * SDK per Java
  * Interfaccia della riga di comando di Azure
  * Portale di anteprima
  * Linguaggio del modello di Resource Manager

## <a name="network-resources"></a>Risorse di rete
Ora è possibile gestire le risorse di rete in modo indipendente, anziché tutte insieme mediante un'unica risorsa di calcolo (una macchina virtuale). Ciò garantisce una maggiore flessibilità durante la creazione di un'infrastruttura complessa e su larga scala in un gruppo di risorse.

Di seguito è riportata una visualizzazione concettuale di una distribuzione di esempio che interessa un'applicazione multilivello. È possibile gestire in modo indipendente ciascuna risorsa visualizzata, ad esempio schede di rete, indirizzi IP pubblici e VM.

![Modello di risorsa di rete](./media/resource-groups-networking/Figure2.png)

Ogni risorsa prevede un set comune di proprietà e il proprio set di proprietà. proprietà comuni Hello sono:

| Proprietà | Descrizione | Valori di esempio |
| --- | --- | --- |
| **nome** |Nome univoco per le risorse. Ogni tipo di risorsa dispone delle proprie restrizioni di denominazione. |PIP01, VM01, NIC01 |
| **location** |Area di Azure in cui hello risiede risorsa |westus, eastus |
| **id** |Identificazione univoca basata su URI |/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP |

È possibile verificare le singole proprietà hello di risorse disponibili nelle sezioni hello riportato di seguito.

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

## <a name="management-interfaces"></a>Interfacce di gestione
È possibile gestire le risorse di rete Azure tramite interfacce diverse. Questo documento è dedicato a tali interfacce: API REST e modelli.

### <a name="rest-api"></a>API REST
Come accennato in precedenza, le risorse di rete possono essere gestite tramite un'ampia gamma di interfacce, tra cui API REST,.NET SDK, Node.JS SDK, Java SDK, PowerShell, l'interfaccia della riga di comando, il portale di Azure e i modelli.

API Rest di Hello conforme toohello specifica del protocollo HTTP 1.1. struttura URI generale Hello di hello API viene presentata di seguito:

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

Hello parametri e parentesi graffe rappresentano hello seguenti elementi:

* **subscription-id** : ID sottoscrizione di Azure.
* **Resource-provider-namespace** -spazio dei nomi per i provider di hello in uso. il valore di Hello per provider di risorse di rete hello è *Network*.
* **nome dell'area** -nome dell'area di Azure hello

metodi HTTP seguenti Hello sono supportati quando si apportano toohello chiamate API REST:

* **INSERIRE** : utilizzato toocreate una risorsa di un determinato tipo, modificare una proprietà della risorsa o modificare un'associazione tra le risorse.
* **OTTENERE** -usare tooretrieve informazioni per una risorsa di provisioning.
* **ELIMINARE** -utilizzato toodelete una risorsa esistente.

Richiesta di hello e di risposta conforme tooa formato di payload JSON. Per altre informazioni, vedere [API di gestione delle risorse di Azure](https://msdn.microsoft.com/library/azure/dn948464.aspx).

### <a name="resource-manager-template-language"></a>Linguaggio del modello di Resource Manager
Nelle risorse di toomanaging aggiunta in modo imperativo (tramite le API o il SDK), è inoltre possibile utilizzare un toobuild di stile di programmazione dichiarativa e gestire le risorse di rete tramite hello linguaggio del modello di gestione risorse.

Di seguito viene fornita una rappresentazione di un modello:

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

modello di Hello è principalmente una descrizione JSON delle risorse di hello e i valori delle istanze hello inseriti tramite i parametri. esempio Hello seguente può essere utilizzato toocreate una rete virtuale con 2 subnet.

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

È possibile hello fornendo i valori dei parametri hello manualmente quando si utilizza un modello oppure è possibile utilizzare un file di parametri. esempio Hello seguente mostra un possibile insieme di toobe di valori di parametro utilizzato con il modello di hello precedente:

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


vantaggi principali di Hello dell'utilizzo di modelli sono:

* È possibile compilare un'infrastruttura complessa in un gruppo di risorse con uno stile dichiarativo. Hello orchestrazione di creazione di risorse di hello, incluse la gestione delle dipendenze, viene gestita dal gestore delle risorse.
* infrastruttura Hello può essere creata in modo ripetibile in diverse aree geografiche e all'interno di un'area semplicemente modificando i parametri.
* uno stile dichiarativo Hello lead tooshorter lead time di compilazione di modelli hello e il rollout infrastruttura hello.

Per i modelli di esempio, vedere i [modelli della guida introduttiva di Azure](https://github.com/Azure/azure-quickstart-templates).

Per ulteriori informazioni su hello linguaggio del modello di gestione risorse, vedere [linguaggio del modello di gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).

modello di esempio Hello precedente Usa la rete virtuale hello e le risorse subnet. È possibile usare altre risorse di rete, come indicato di seguito:

### <a name="using-a-template"></a>Uso di un modello
È possibile distribuire servizi tooAzure da un modello usando PowerShell, AzureCLI, oppure eseguendo un toodeploy fare clic su da GitHub. servizi toodeploy da un modello in GitHub, eseguire hello alla procedura seguente:

1. Aprire il file di template3 hello da GitHub. Come esempio, aprire [Rete virtuale con due subnet](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).
2. Fare clic su **distribuire tooAzure**e quindi accedere a toohello portale di Azure con le credenziali.
3. Verificare il modello di hello e quindi fare clic su **salvare**.
4. Fare clic su **modificare parametri** e selezionare un percorso, ad esempio *Stati Uniti occidentali*, per la rete virtuale hello e le subnet.
5. Se necessario, modificare hello **ADDRESSPREFIX** e **SUBNETPREFIX** parametri e quindi fare clic su **OK**.
6. Fare clic su **selezionare un gruppo di risorse** e quindi fare clic sul gruppo di risorse hello da rete virtuale hello tooadd e subnet ai. In alternativa, è possibile creare un nuovo gruppo di risorse facendo clic su **Crea nuovo**.
7. Fare clic su **Crea**. Si noti hello riquadro visualizzazione **distribuzione del modello di Provisioning**. Una volta hello distribuzione viene eseguita, si noterà tooone simile a schermata riportata di seguito.

![Distribuzione del modello di esempio](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a>Passaggi successivi
[Linguaggio del modello di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md)

[Rete di Azure: modelli di uso comune](https://github.com/Azure/azure-quickstart-templates)

[Distribuzione Azure Resource Manager o classica](../azure-resource-manager/resource-manager-deployment-model.md)

[Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)

