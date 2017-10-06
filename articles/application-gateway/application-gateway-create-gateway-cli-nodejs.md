---
title: aaaCreate un Gateway di applicazione di Azure - CLI di Azure 1.0 | Documenti Microsoft
description: Informazioni su come toocreate un Gateway applicazione utilizzando hello Azure CLI 1.0 in Gestione risorse
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3c0d2d96b6be404d0372d00f0deb2a32959ca419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a>Creare un gateway applicazione hello CLI di Azure

> [!div class="op_single_selector"]
> * [Portale di Azure](application-gateway-create-gateway-portal.md)
> * [PowerShell per Azure Resource Manager](application-gateway-create-gateway-arm.md)
> * [PowerShell per Azure classico](application-gateway-create-gateway.md)
> * [Modello di Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [Interfaccia della riga di comando di Azure 1.0](application-gateway-create-gateway-cli.md)
> * [Interfaccia della riga di comando di Azure 2.0](application-gateway-create-gateway-cli.md)
> 
> 

Il gateway applicazione di Azure è un dispositivo di bilanciamento del carico di livello 7. Fornisce il failover, le prestazioni di routing di richieste HTTP tra server diversi, che si trovino in locale o cloud hello. Gateway applicazione ha seguendo le funzionalità di recapito dell'applicazione hello: caricare probe di integrità personalizzato di bilanciamento del carico, l'affinità di sessione basato su cookie e offload Secure Sockets Layer (SSL), HTTP e il supporto per più siti.

## <a name="prerequisite-install-hello-azure-cli"></a>Prerequisito: Installare hello CLI di Azure

hello tooperform i passaggi in questo articolo, è necessario troppo[installare hello interfaccia della riga di comando di Azure per Mac, Linux e Windows (Azure CLI)](../xplat-cli-install.md) ed è necessario troppo[accedere tooAzure](../xplat-cli-connect.md). 

> [!NOTE]
> Se non si dispone di un account Azure, è necessario procurarsene uno. Usare la [versione di valutazione gratuita](../active-directory/sign-up-organization.md).

## <a name="scenario"></a>Scenario

In questo scenario viene illustrato come gateway un'applicazione utilizzando toocreate hello portale di Azure.

Questo scenario illustrerà come:

* Creare un gateway applicazione Medium con due istanze.
* Creare una rete virtuale denominata ContosoVNET con un blocco CIDR riservato di 10.0.0.0/16.
* Creare una subnet denominata subnet01 che usa 10.0.0.0/28 come blocco CIDR.

> [!NOTE]
> Le ricerche di configurazione aggiuntiva di gateway applicazione hello, inclusi stato personalizzato, gli indirizzi del pool back-end e regole aggiuntive vengono configurati dopo la configurazione di gateway applicazione hello e non durante la distribuzione iniziale.

## <a name="before-you-begin"></a>Prima di iniziare

Il gateway applicazione di Azure richiede una propria subnet. Quando si crea una rete virtuale, assicurarsi di lasciare sufficiente toohave spazio di indirizzi più subnet. Dopo aver distribuito una subnet tooa di gateway applicazione, gateway di applicazione solo aggiuntive sono in grado di toobe aggiunto toohello subnet.

## <a name="log-in-tooazure"></a>Accedi tooAzure

Aprire hello **prompt dei comandi di Microsoft Azure**ed effettuare l'accesso. 

```azurecli-interactive
azure login
```

Una volta digitato hello sopra riportato, viene fornito un codice. Spostarsi in un processo di accesso browser hello toocontinue toohttps://aka.ms/devicelogin.

![Comando che illustra l'accesso al dispositivo][1]

Nel browser hello immettere codice hello ricevuto. Si è reindirizzato tooa nella pagina di accesso.

![codice tooenter browser][2]

Dopo aver immesso il codice hello si è connessi, hello Chiudi browser toocontinue scenario hello.

![Accesso eseguito][3]

## <a name="switch-tooresource-manager-mode"></a>Passare tooResource modalità di gestione

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a>Creare il gruppo di risorse hello

Prima di creare i gateway applicazione hello, un gruppo di risorse viene creato toocontain gateway di applicazione hello. Hello seguito è riportato il comando hello.

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a>Crea rete virtuale

Una volta creato il gruppo di risorse hello, viene creata una rete virtuale per il gateway applicazione hello.  Nell'esempio seguente di hello, spazio degli indirizzi di hello era come 10.0.0.0/16 come definito in hello note scenario precedente.

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a>Creare una subnet

Dopo aver creata la rete virtuale hello, viene aggiunta una subnet per il gateway applicazione hello.  Se si prevede di gateway applicazione toouse con un'app web ospitato in hello stesso virtuale come gateway applicazione hello di rete, tooleave che lo spazio sia sufficiente per un'altra subnet.

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a>Creare il gateway applicazione hello

Dopo aver creati la rete virtuale hello e subnet, siano soddisfatti i prerequisiti per il gateway applicazione hello hello. Inoltre, una password di hello e di certificato PFX esportato in precedenza per il certificato di hello sono richieste per hello seguente passaggio: hello indirizzi utilizzati per back-end hello sono gli indirizzi IP hello del server back-end. Questi valori possono essere entrambi indirizzi IP privati nella rete virtuale hello, gli indirizzi IP pubblici o nomi di dominio completo per i server back-end.

```azurecli-interactive
azure network application-gateway create \
--name AdatumAppGateway \
--location eastus \
--resource-group ContosoRG \
--vnet-name ContosoVNET \
--subnet-name subnet01 \
--servers 134.170.185.46,134.170.188.221,134.170.185.50 \
--capacity 2 \
--sku-tier Standard \
--routing-rule-type Basic \
--frontend-port 80 \
--http-settings-cookie-based-affinity Enabled \
--http-settings-port 80 \
--http-settings-protocol http \
--frontend-port http \
--sku-name Standard_Medium
```

> [!NOTE]
> Per un elenco di parametri che possono essere forniti durante la creazione eseguire hello comando seguente: **creare applicazione-gateway di rete di azure - Guida**.

Questo esempio crea un gateway applicazione basic con le impostazioni predefinite per il listener hello, pool back-end, le impostazioni http back-end e regole. È possibile modificare la distribuzione toosuit queste impostazioni dopo il provisioning di hello ha esito positivo.
Se si dispone già di un'applicazione web definita con il pool back-end hello in hello precedenti passaggi, una volta creati, il bilanciamento del carico ha inizio.

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come probe di integrità personalizzato toocreate visitando [per creare un probe di integrità personalizzato](application-gateway-create-probe-portal.md)

Informazioni su come tooconfigure offload SSL e la decrittografia SSL costosa di intraprendere hello off i server web, visitare il sito [configurare Offload SSL](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
