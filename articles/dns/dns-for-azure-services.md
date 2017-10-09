---
title: aaaUsing DNS di Azure con altri servizi di Azure | Documenti Microsoft
description: Comprendere come toouse DNS di Azure tooresolve denominati per altri servizi di Azure
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure dns
ms.assetid: e9b5eb94-7984-4640-9930-564bb9e82b78
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 09/21/2016
ms.author: gwallace
ms.openlocfilehash: 791f93d6aff2c638c08518e9f1e8ab89ac8de3f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-dns-works-with-other-azure-services"></a>Funzionamento del servizio DNS di Azure con altri servizi di Azure

Il servizio DNS di Azure è un servizio ospitato di risoluzione nomi e di gestione DNS, In questo modo si toocreate pubblici nomi DNS per hello altre applicazioni e servizi che è stato distribuito in Azure. Creazione di un nome per un servizio di Azure nel dominio personalizzato è semplice come l'aggiunta di un record di tipo corretto di hello per il servizio.

* Per gli indirizzi IP allocati dinamicamente, è necessario creare un record DNS CNAME nome DNS toohello mappe Azure creato per il servizio. Standard DNS impedire l'utilizzo di un record CNAME per vertice zona hello.
* Per indirizzi IP statici, è possibile creare un record A DNS utilizzando un nome qualsiasi, incluso un *dominio naked* nome al vertice zona hello.

Hello seguente tabella vengono illustrati hello supportati i tipi di record che possono essere utilizzati per diversi servizi di Azure. Come si può vedere nella tabella, il servizio DNS di Azure supporta soltanto i record DNS per le risorse di rete con connessione Internet. Il servizio DNS di Azure non può essere usato per la risoluzione nomi degli indirizzi interni e privati.

| Servizio di Azure | Interfaccia di rete | Descrizione |
| --- | --- | --- |
| gateway applicazione |[IP pubblico front-end](dns-custom-domain.md#public-ip-address) |È possibile creare un record DNS A o CNAME. |
| Bilanciamento del carico |[IP pubblico front-end](dns-custom-domain.md#public-ip-address)  |È possibile creare un record DNS A o CNAME. Al servizio di bilanciamento del carico può essere assegnato dinamicamente un indirizzo PI pubblico IPv6. Di conseguenza, è necessario creare un record CNAME per un indirizzo IPv6. |
| Gestione traffico |Nome pubblico |È possibile creare solo un record CNAME che esegue il mapping al nome trafficmanager.net toohello assegnato tooyour profilo di gestione traffico. Per altre informazioni, vedere [Funzionamento di Gestione traffico](../traffic-manager/traffic-manager-overview.md#traffic-manager-example). |
| Servizio cloud |[IP pubblico](dns-custom-domain.md#public-ip-address) |Per gli indirizzi IP allocati staticamente, è possibile creare un record DNS A. Per gli indirizzi IP allocati dinamicamente, è necessario creare un record CNAME che esegue il mapping toohello *cloudapp.net* nome. Questa regola si applica tooVMs creato nel portale classico hello perché vengono distribuiti come un servizio cloud. Per altre informazioni, vedere [Configurare un nome di dominio personalizzato nei servizi cloud](../cloud-services/cloud-services-custom-domain-name-portal.md). |
| Servizio app | [IP esterno](dns-custom-domain.md#app-service-web-apps) |Per gli indirizzi IP esterni, è possibile creare un record DNS A. In caso contrario, è necessario creare un record CNAME che esegue il mapping nome azurewebsites.net toohello. Per ulteriori informazioni, vedere [mappare un tooan di nome di dominio personalizzato dell'app di Azure](../app-service-web/web-sites-custom-domain-name.md) |
| VM di Resource Manager |[IP pubblico](dns-custom-domain.md#public-ip-address) |Le VM di Resource Manager possono avere indirizzi IP pubblici. Una VM con un indirizzo IP pubblico può essere anche dietro a un servizio di bilanciamento del carico. È possibile creare un record DNS A o CNAME per hello indirizzo pubblico. Questo nome personalizzato può essere utilizzato toobypass hello VIP sul bilanciamento del carico hello. |
| Macchine virtuali classiche |[IP pubblico](dns-custom-domain.md#public-ip-address) |Le VM classiche create con PowerShell o l'interfaccia della riga di comando possono essere configurate con un indirizzo virtuale (riservato) dinamico o statico. È possibile creare rispettivamente un record DNS A o CNAME. |
