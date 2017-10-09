---
title: aaaCreate un Gateway di applicazione di Azure - CLI di Azure 2.0 | Documenti Microsoft
description: Informazioni su come toocreate un Gateway applicazione utilizzando hello Azure CLI 2.0 in Gestione risorse
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 952065586cd87d253882438bb779b768d9fd59fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli-20"></a>Creare un gateway applicazione hello Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Portale di Azure](application-gateway-create-gateway-portal.md)
> * [PowerShell per Azure Resource Manager](application-gateway-create-gateway-arm.md)
> * [PowerShell per Azure classico](application-gateway-create-gateway.md)
> * [Modello di Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [Interfaccia della riga di comando di Azure 1.0](application-gateway-create-gateway-cli.md)
> * [Interfaccia della riga di comando di Azure 2.0](application-gateway-create-gateway-cli.md)

Il gateway applicazione è un'appliance virtuale dedicata che offre un servizio di controller per la distribuzione di applicazioni (ADC, Application Delivery Controller) e varie funzionalità di bilanciamento del carico di livello 7 per l'applicazione.

## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI

È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

* [Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) -nostri CLI per hello classic e risorse Gestione modelli di distribuzione.
* [Azure CLI 2.0](application-gateway-create-gateway-cli.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello

## <a name="prerequisite-install-hello-azure-cli-20"></a>Prerequisito: Installare hello Azure CLI 2.0

hello tooperform i passaggi in questo articolo, è necessario troppo[installare hello interfaccia della riga di comando di Azure per Mac, Linux e Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

> [!NOTE]
> Se non si dispone di un account Azure, è necessario procurarsene uno. Usare la [versione di valutazione gratuita](../active-directory/sign-up-organization.md).

## <a name="scenario"></a>Scenario

In questo scenario viene illustrato come gateway un'applicazione utilizzando toocreate hello portale di Azure.

Questo scenario illustrerà come:

* Creare un gateway applicazione Medium con due istanze.
* Creare una rete virtuale denominata AdatumAppGatewayVNET con un blocco CIDR riservato 10.0.0.0/16.
* Creare una subnet denominata Appgatewaysubnet che usa 10.0.0.0/28 come blocco CIDR.

> [!NOTE]
> Le ricerche di configurazione aggiuntiva di gateway applicazione hello, inclusi stato personalizzato, gli indirizzi del pool back-end e regole aggiuntive vengono configurati dopo la configurazione di gateway applicazione hello e non durante la distribuzione iniziale.

## <a name="before-you-begin"></a>Prima di iniziare

Il gateway applicazione di Azure richiede una propria subnet. Quando si crea una rete virtuale, assicurarsi di lasciare sufficiente toohave spazio di indirizzi più subnet. Dopo aver distribuito una subnet tooa di gateway applicazione, i gateway applicazione aggiuntiva solo è possibile aggiungere subnet toohello.

## <a name="log-in-tooazure"></a>Accedi tooAzure

Aprire hello **prompt dei comandi di Microsoft Azure**ed effettuare l'accesso. 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> È inoltre possibile utilizzare `az login` senza l'opzione per l'accesso di dispositivo che richiede l'immissione di un codice di aka.ms/devicelogin hello.

Una volta digitato hello sopra riportato, viene fornito un codice. Spostarsi in un processo di accesso browser hello toocontinue toohttps://aka.ms/devicelogin.

![Comando che illustra l'accesso al dispositivo][1]

Nel browser hello immettere codice hello ricevuto. Si è reindirizzato tooa nella pagina di accesso.

![codice tooenter browser][2]

Dopo aver immesso il codice hello si è connessi, hello Chiudi browser toocontinue scenario hello.

![Accesso eseguito][3]

## <a name="create-hello-resource-group"></a>Creare il gruppo di risorse hello

Prima di creare i gateway applicazione hello, un gruppo di risorse viene creato toocontain gateway di applicazione hello. Hello seguito è riportato il comando hello.

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-hello-application-gateway"></a>Creare il gateway applicazione hello

gli indirizzi IP di Hello usati per back-end hello sono gli indirizzi IP hello del server back-end. Questi valori possono essere entrambi indirizzi IP privati nella rete virtuale hello, gli indirizzi IP pubblici o nomi di dominio completo per i server back-end. Hello seguente viene creato un gateway applicazione con le impostazioni di configurazione aggiuntive per le impostazioni http, porte e le regole.

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet" \
--subnet-address-prefix "10.0.0.0/28" \
--servers 10.0.0.4 10.0.0.5 \
--capacity 2 \
--sku Standard_Small \
--http-settings-cookie-based-affinity Enabled \
--http-settings-protocol Http \
--frontend-port 80 \
--routing-rule-type Basic \
--http-settings-port 80 \
--public-ip-address "pip2" \
--public-ip-address-allocation "dynamic" \

```

Hello precedente esempio vengono illustrate molte proprietà che non sono necessari durante la creazione di un gateway applicazione hello. Hello esempio di codice seguente crea un gateway applicazione con le informazioni necessarie hello.

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet \
--subnet-address-prefix "10.0.0.0/28" \
--servers "10.0.0.5"  \
--public-ip-address pip
```
 
> [!NOTE]
> Per un elenco di parametri che possono essere forniti durante hello creazione eseguire comando seguente: `az network application-gateway create --help`.

Questo esempio crea un gateway applicazione basic con le impostazioni predefinite per il listener hello, pool back-end, le impostazioni http back-end e regole. È possibile modificare la distribuzione toosuit queste impostazioni dopo il provisioning di hello ha esito positivo.
Se si dispone già di un'applicazione web definita con il pool back-end hello in hello precedenti passaggi, una volta creati, il bilanciamento del carico ha inizio.

## <a name="get-application-gateway-dns-name"></a>Ottenere il nome DNS del gateway applicazione

Una volta creato il gateway hello passaggio successivo hello è tooconfigure hello front-end per la comunicazione. Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo. gli utenti finali tooensure possibile raggiungere il gateway di applicazione hello, un record CNAME può essere utilizzati toopoint endpoint pubblico di toohello di gateway applicazione hello. [Configurazione di un nome di dominio personalizzato in Azure](../dns/dns-custom-domain.md). tooconfigure un alias, recuperare i dettagli del gateway applicazione hello e il relativo nome IP/DNS associato usando hello PublicIPAddress elemento collegato toohello applicazioni gateway. nome DNS del gateway applicazione Hello deve essere utilizzato toocreate un record CNAME, il nome DNS punti hello due web applicazioni toothis. utilizzo di Hello del record non è consigliato poiché hello VIP potrebbe cambiare al riavvio del gateway applicazione.


```azurecli-interactive
az network public-ip show --name "pip" --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="delete-all-resources"></a>Eliminare tutte le risorse

toodelete tutte le risorse create in questo articolo, hello completo alla procedura seguente:

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a>Passaggi successivi

Informazioni su come probe di integrità personalizzato toocreate visitando [per creare un probe di integrità personalizzato](application-gateway-create-probe-portal.md)

Informazioni su come tooconfigure offload SSL e la decrittografia SSL costosa di intraprendere hello off i server web, visitare il sito [configurare Offload SSL](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
