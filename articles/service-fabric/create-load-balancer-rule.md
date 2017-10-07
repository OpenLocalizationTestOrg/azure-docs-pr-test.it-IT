---
title: aaaCreate una regola per un cluster di bilanciamento del carico di Azure
description: Configurare le porte tooopen un bilanciamento del carico di Azure per il cluster di Azure Service Fabric.
services: service-fabric
documentationcenter: na
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: adegeo
ms.openlocfilehash: 4a40f62422bd895d782be8cbaace5f4e1af81db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a>Aprire le porte per un cluster di Service Fabric

bilanciamento del carico Hello distribuito con il cluster di Azure Service Fabric indirizza il traffico tooyour app in esecuzione in un nodo. Se si modifica il toouse app una porta diversa, è necessario esporre tale porta (o indirizzare una porta diversa) in hello bilanciamento del carico di Azure.

Quando è stato distribuito il tooAzure di servizio dell'infrastruttura cluster, è stato creato automaticamente un servizio di bilanciamento del carico. Se non è disponibile un servizio di bilanciamento del carico, vedere l'articolo su come [configurare un servizio di bilanciamento del carico con connessione Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).

## <a name="configure-service-fabric"></a>Configurare Service Fabric

L'applicazione di Service Fabric **ServiceManifest.xml** file di configurazione definisce gli endpoint hello l'applicazione prevede toouse. Al termine del file di configurazione hello è stata aggiornata toodefine un endpoint, bilanciamento del carico hello deve essere aggiornato tooexpose tale (o una diversa) porta. Per ulteriori informazioni su come toocreate hello endpoint dell'infrastruttura del servizio, vedere [un Endpoint del programma di installazione](service-fabric-service-manifest-resources.md).

## <a name="create-a-load-balancer-rule"></a>Creare una regola di bilanciamento del carico

Una regola di bilanciamento del carico viene aperta una porta con connessione internet e inoltra porta traffico toohello interno del nodo utilizzata dall'applicazione. Se non è disponibile un servizio di bilanciamento del carico, vedere l'articolo su come [configurare un servizio di bilanciamento del carico con connessione Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).

regola toocreate un bilanciamento del carico, è necessario hello toocollect le seguenti informazioni:

- Nome del servizio di bilanciamento del carico.
- Gruppo di risorse di hello bilanciamento del carico e cluster di service fabric.
- Porta esterna.
- Porta interna.

## <a name="azure-cli"></a>Interfaccia della riga di comando di Azure
>[!NOTE]
>Se è necessario il nome hello toodetermine di bilanciamento del carico hello, utilizzare un elenco di tutti i servizi di bilanciamento del carico e i gruppi di risorse hello associata get di tooquickly questo comando.
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

È sufficiente un singolo comando toocreate una regola di bilanciamento del carico con hello **CLI di Azure**. È sufficiente tooknow sia nome hello del carico hello bilanciamento e risorse toocreate gruppo una nuova regola.

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

Hello comando CLI di Azure dispone di alcuni parametri descritti nella seguente tabella hello:

| . | Descrizione |
| --------- | ----------- |
| `--backend-port`  | applicazione di Hello porta hello service fabric è in ascolto. |
| `--frontend-port` | hello porta Hello caricare espone di bilanciamento del carico per le connessioni esterne. |
| `-lb-name` | nome Hello di hello caricare toochange di bilanciamento del carico. |
| `-g`       | gruppo di risorse Hello con bilanciamento del carico hello sia cluster di service fabric. |
| `-n`       | Hello scelto il nome della regola hello. |


>[!NOTE]
>Per ulteriori informazioni su come toocreate un bilanciamento del carico con hello CLI di Azure, vedere [creare un servizio di bilanciamento del carico con hello Azure CLI](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).

## <a name="powershell"></a>PowerShell

>[!NOTE]
>Se è necessario il nome hello toodetermine di bilanciamento del carico hello, utilizzare un elenco di tutti i servizi di bilanciamento del carico e i gruppi di risorse associati get di tooquickly questo comando.
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

PowerShell è leggermente più complicato hello CLI di Azure. Concettualmente, eseguire hello seguendo i passaggi toocreate una regola.

1. Ottenere bilanciamento del carico hello da Azure.
2. Creare una regola.
3. Aggiungere toohello hello regola il bilanciamento del carico.
4. Aggiorna bilanciamento del carico di hello.

```powershell
# Get hello load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create hello rule based on information from hello load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add hello rule toohello load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update hello load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

Riguardanti hello `New-AzureRmLoadBalancerRuleConfig` comando hello `-FrontendPort` espone rappresenta hello porta hello bilanciamento del carico per le connessioni esterne e hello `-BackendPort` rappresenta hello porta hello service fabric app è in ascolto.

>[!NOTE]
>Per ulteriori informazioni su come toocreate un bilanciamento del carico con PowerShell, vedere [creare un servizio di bilanciamento del carico con PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).

