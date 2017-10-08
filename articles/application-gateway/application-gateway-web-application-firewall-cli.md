---
title: firewall di applicazione web aaaConfigure - Gateway applicazione Azure | Documenti Microsoft
description: In questo articolo vengono fornite indicazioni su come toostart tramite web firewall applicazione su un gateway applicazione nuova o esistente.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: gwallace
ms.openlocfilehash: d5354984760ceab12ed49efa9e18836e9f1d3c96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a>Configurare un web application firewall in un gateway applicazione nuovo o esistente con l'interfaccia della riga di comando di Azure

> [!div class="op_single_selector"]
> * [Portale di Azure](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Interfaccia della riga di comando di Azure](application-gateway-web-application-firewall-cli.md)

Informazioni su come toocreate un firewall applicazione web abilitata gateway applicazione oppure aggiungere web application firewall tooan applicazione gateway esistente.

firewall applicazione web di Hello (WAF) nel Gateway di applicazione di Azure consente di proteggere le applicazioni web da attacchi basati sul web comuni quali attacchi SQL injection, attacchi di script e assume il controllo di sessione.

Il gateway applicazione di Azure è un dispositivo di bilanciamento del carico di livello 7. Fornisce il failover, le prestazioni di routing di richieste HTTP tra server diversi, che si trovino in locale o cloud hello. Il gateway applicazione offre numerose funzionalità di controller per la distribuzione di applicazioni (ADC, Application Delivery Controller), tra cui bilanciamento del carico HTTP, affinità di sessione basata su cookie, offload SSL (Secure Sockets Layer), probe di integrità personalizzati, supporto per più siti e altro ancora. toofind un elenco completo delle funzionalità supportate, visitare: [Panoramica del Gateway applicazione](application-gateway-introduction.md).

Hello articolo seguente viene illustrato come troppo[aggiungere web application firewall tooan esistente gateway applicazione](#add-web-application-firewall-to-an-existing-application-gateway) e [creare un gateway di applicazione che utilizza firewall applicazione web](#create-an-application-gateway-with-web-application-firewall).

![immagine dello scenario][scenario]

## <a name="prerequisite-install-hello-azure-cli-20"></a>Prerequisito: Installare hello Azure CLI 2.0

hello tooperform i passaggi in questo articolo, è necessario troppo[installare hello interfaccia della riga di comando di Azure per Mac, Linux e Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="waf-configuration-differences"></a>Differenze di configurazione dei WAF

Se si è letto [creare un Gateway applicazione con Azure CLI](application-gateway-create-gateway-cli.md), comprendere hello SKU impostazioni tooconfigure durante la creazione di un gateway applicazione. WAF fornisce toodefine impostazioni aggiuntive quando si configurano hello SKU di gateway applicazione. Non sono presenti modifiche aggiuntive che verranno apportate gateway applicazione hello stesso.

| **Impostazione** | **Dettagli**
|---|---|
|**SKU** |Un gateway applicazione normale senza WAF supporta le dimensioni **Standard\_Small**, **Standard\_Medium** e **Standard\_Large**. Introduzione di hello di WAF, non vi sono due SKU aggiuntive, **WAF\_Media** e **WAF\_grande**. WAF non è supportato sui gateway applicazione di piccole dimensioni.|
|**Modalità** | Questa impostazione è la modalità di WAF hello. I valori consentiti sono **Rilevamento** e **Prevenzione**. Quando il firewall WAF è configurato in modalità di rilevamento, tutte le minacce vengono archiviate in un file di log. In modalità di prevenzione, gli eventi vengono comunque registrati ma autore dell'attacco hello riceve una risposta di non autorizzato 403 dal gateway applicazione hello.|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a>Aggiungere web application firewall tooan esistente gateway applicazione

Hello seguire le modifiche dei comandi di un gateway applicazione abilitato tooa WAF di gateway applicazione standard esistente.

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

Questo comando Aggiorna gateway applicazione hello con firewall applicazione web. Visitare [diagnostica del Gateway applicazione](application-gateway-diagnostics.md) toounderstand come tooview Registra per il gateway applicazione. A causa di toohello sicurezza natura WAF, registri necessità toobe rivisto regolarmente condizioni di sicurezza hello toounderstand delle applicazioni web.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Creare un gateway applicazione con il web application firewall

Hello comando seguente crea un Gateway applicazione con firewall applicazione web.

```azurecli-interactive
#!/bin/bash

az network application-gateway create \
  --name "AdatumAppGateway2" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet2" \
  --subnet-address-prefix "10.0.0.0/28" \
 --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 
  --sku "WAF_Medium" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip2" \
  --public-ip-address-allocation "dynamic" \
  --tags "cli[2] owner[administrator]"
```

> [!NOTE]
> Gateway applicazione creati con configurazione del firewall applicazione web di base hello sono configurati con CRS 3.0 per la protezione.

## <a name="get-application-gateway-dns-name"></a>Ottenere il nome DNS del gateway applicazione

Una volta creato il gateway hello passaggio successivo hello è tooconfigure hello front-end per la comunicazione. Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo. gli utenti finali tooensure possibile raggiungere il gateway di applicazione hello, un record CNAME può essere utilizzati toopoint endpoint pubblico di toohello di gateway applicazione hello. [Configurazione di un nome di dominio personalizzato in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure un record CNAME, recuperare i dettagli del gateway applicazione hello e il relativo nome IP/DNS associato usando hello PublicIPAddress elemento collegato toohello applicazioni gateway. nome DNS del gateway applicazione Hello deve essere utilizzato toocreate un record CNAME, il nome DNS punti hello due web applicazioni toothis. utilizzo di Hello del record non è consigliato poiché hello VIP potrebbe cambiare al riavvio del gateway applicazione.

```azurecli-interactive
#!/bin/bash

az network public-ip show \
  --name pip2 \
  --resource-group "AdatumAppGatewayRG"
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

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come toocustomize WAF regole visitando: [personalizzare le regole di firewall applicazione web mediante Azure CLI 2.0 hello](application-gateway-customize-waf-rules-cli.md).

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
