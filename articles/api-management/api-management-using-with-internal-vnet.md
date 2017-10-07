---
title: aaaHow toouse gestione API di Azure con la rete virtuale interna | Documenti Microsoft
description: Informazioni su come toosetup e configurare Gestione API di Azure in rete virtuale interna.
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: 
ms.assetid: dac28ccf-2550-45a5-89cf-192d87369bc3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8d25de14e0c0bebe7ba7b47ca432ea4e45dde312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a>Uso del servizio Gestione API di Azure con una rete virtuale interna
Con reti virtuali di Azure (Vnet), gestione API possono gestire le API non è accessibile su Internet hello. Una serie di tecnologie VPN è connessione hello toomake disponibili e gestione API può essere distribuito in due modalità principali all'interno di hello rete virtuale:
* Esterno
* Interno

## <a name="overview"> </a>Panoramica
Quando l'API di gestione viene distribuito in una modalità di rete virtuale interna, tutti gli endpoint servizio hello (gateway, portale per sviluppatori, portale di pubblicazione, la gestione diretta e Git) vengono solo all'interno di una rete virtuale che si controllano l'accesso a. Nessuno degli endpoint del servizio hello registrati nel Server DNS pubblico hello.

Utilizzo di gestione API in modalità interna, è possibile ottenere hello seguenti scenari
* Consentire un accesso esterno sicuro da parte di terzi alle API ospitate in un data center privato, tramite connessioni VPN da sito a sito o ExpressRoute.
* Abilitare scenari cloud ibrid esponendo le API basate su cloud e locali tramite un gateway comune.
* Gestire le API ospitate in più aree geografiche usando un singolo endpoint del gateway. 

## <a name="enable-vpn"> </a>Creazione di un servizio Gestione API in una rete virtuale interna
Servizio gestione API nella rete virtuale interna Hello è ospitato dietro un Balancer(ILB) carico interno. l'indirizzo IP del bilanciamento del carico interno hello Hello è hello [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) intervallo.  

### <a name="enable-vnet-connection-using-azure-portal"></a>Abilitare la connessione della rete virtuale usando il portale di Azure
Creare innanzitutto il servizio di gestione API hello seguendo i passaggi di hello [servizio Gestione API di creazione][Create API Management service]. Quindi configurazione Gestione API toobe distribuiti all'interno di una rete virtuale.

![Menu per la configurazione di Gestione API nella rete virtuale interna][api-management-using-internal-vnet-menu]

Dopo il completamento della distribuzione di hello, dovrebbe essere hello interno indirizzo IP virtuale del servizio nel dashboard di hello.

![Dashboard di gestione API con rete virtuale interna configurata][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a>Abilitare la connessione della rete virtuale usando i cmdlet di PowerShell
È inoltre possibile abilitare la connettività di rete virtuale utilizzando i cmdlet di PowerShell hello.

* **Creare un servizio di gestione API all'interno di una rete virtuale**: utilizzare i cmdlet di hello [New AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate una gestione API di Azure del servizio all'interno di una rete virtuale e configurarlo come tipo di rete virtuale interna toouse hello.

* **Distribuire un servizio di gestione API esistente all'interno di una rete virtuale**: utilizzare i cmdlet di hello [aggiornamento AzureRmApiManagementDeployment](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove una gestione API di Azure esistente all'interno di una rete virtuale del servizio e configurarlo toouse Tipo di rete virtuale interna.

## <a name="apim-dns-configuration"></a>Configurazione del DNS
Quando si usa Gestione API in modalità di rete virtuale esterna, il DNS è gestito da Azure. Modalità di rete virtuale interna, è possibile toomanage il proprio servizio DNS.

> [!NOTE]
> Servizio gestione API non è in ascolto toorequests presto agli indirizzi IP. Risponde solo toorequests toohello nome host configurato sui relativi endpoint di servizio (che include i gateway, portale per sviluppatori, server di pubblicazione portale, la gestione diretta endpoint e git).

### <a name="access-on-default-host-names"></a>Accesso ai nomi host predefiniti:
Quando si crea un servizio di gestione API in un cloud pubblico di Azure, denominato "contoso", ad esempio, hello seguenti endpoint di servizio sono configurati per impostazione predefinita.

>   Gateway o Proxy: contoso.azure-api.net

> Portale di pubblicazione portale per sviluppatori: contoso.portal.azure-api.net

> Endpoint di gestione diretta: contoso.management.azure-api.net

>   GIT: contoso.scm.azure-api.net

tooaccess questi endpoint del servizio Gestione API, è possibile creare una macchina virtuale in una rete virtuale di toohello subnet connesse in cui viene distribuito l'API di gestione. Supponendo che hello indirizzo IP virtuale interno per il servizio sia 10.0.0.5, è possibile eseguire hello mapping del file host (% SystemDrive%\drivers\etc\hosts) come indicato di seguito:

> 10.0.0.5    contoso.azure-api.net

> 10.0.0.5    contoso.portal.azure-api.net

> 10.0.0.5    contoso.management.azure-api.net

> 10.0.0.5    contoso.scm.azure-api.net

È possibile accedere tutti gli endpoint di servizio hello da hello macchina virtuale è stato creato. Se si usa un server DNS personalizzato in una rete virtuale, è anche possibile creare record DNS A e accedere agli endpoint da qualsiasi punto nella rete virtuale. 

### <a name="access-on-custom-domain-names"></a>Accedere a nomi di dominio personalizzati:
Se non si desidera tooaccess hello servizio Gestione API con i nomi host di hello predefiniti, è possibile configurare i nomi di dominio personalizzato per tutti gli endpoint del servizio come di seguito

![Configurazione di un dominio personalizzato per Gestione API][api-management-custom-domain-name]

È quindi possibile creare un record in tooaccess il Server DNS questi endpoint che sono accessibili solo da all'interno della rete virtuale.

## <a name="related-content"></a>Contenuti correlati
* [Problemi di configurazione di rete comuni durante la configurazione di Gestione API in una rete virtuale][Common Network Configuration Issues]
* [Domande frequenti sulle reti virtuali](../virtual-network/virtual-networks-faq.md)
* [Creazione di un record A in DNS](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
