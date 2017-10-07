---
title: Gestione API di Azure aaaDeploy services toomultiple Azure aree | Documenti Microsoft
description: Informazioni su come toodeploy un'API di Azure Management service toomultiple istanza Azure aree.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 47389ad6-f865-4706-833f-846115e22e4d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 04a3e762261237d73a769320a21363f99f1d20cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-an-azure-api-management-service-instance-toomultiple-azure-regions"></a>Come toodeploy un'API di Azure Management service toomultiple istanza Azure aree
API di gestione supporta la distribuzione di più aree che consente di API editori toodistribute un singolo servizio di gestione API in un numero qualsiasi di aree di Azure desiderate. Ciò consente di ridurre la latenza delle richieste percepita dagli utenti dell'API distribuiti geograficamente, oltre a migliorare la disponibilità del servizio se un'area viene portata offline. 

Quando viene creato inizialmente un servizio di gestione API, contiene solo una [unità] [ unit] e si trova in una singola regione di Azure, definita come hello area primaria. È possibile aggiungere facilmente aree aggiuntive tramite hello portale di Azure. Un server gateway di gestione API è distribuito tooeach area e chiamata traffico verrà indirizzato toohello più vicino gateway. Se un'area è offline, il traffico di hello è gateway più vicino successivo toohello reindirizzata automaticamente. 

> [!IMPORTANT]
> Distribuzione con più aree è disponibile solo in hello  **[Premium] [ Premium]**  livello.
> 
> 

## <a name="add-region"></a>Distribuire un'API Gestione servizio istanza tooa nuova area
> [!NOTE]
> Se non è ancora stato creato un'istanza del servizio Gestione API, vedere [creare un'istanza del servizio Gestione API] [ Create an API Management service instance] in hello [Introduzione a gestione API di Azure] [ Get started with Azure API Management] esercitazione.
> 
> 

Nel portale di Azure hello passare toohello **scala e prezzi** pagina per l'istanza del servizio Gestione API. 

![Scheda Scalabilità][api-management-scale-service]

nuova area tooa toodeploy, fare clic su **+ Aggiungi area** dalla barra degli strumenti hello.

![Aggiungere un'area][api-management-add-region]

Selezionare il percorso di hello dall'elenco a discesa hello e impostare il numero di hello di unità per con dispositivo di scorrimento hello.

![Specificare le unità][api-management-select-location-units]

Fare clic su **Aggiungi** tooplace la selezione nella tabella delle posizioni di hello. 

Ripetere questo processo fino a quando non si dispone di tutte le località configurate e fare clic su **salvare** dal processo di distribuzione hello toostart hello barra degli strumenti.

## <a name="remove-region"> </a>Eliminare un'istanza del servizio di Gestione API da una posizione
Nel portale di Azure hello passare toohello **scala e prezzi** pagina per l'istanza del servizio Gestione API. 

![Scheda Scalabilità][api-management-scale-service]

Per percorso hello desiderato tooremove aprire il menu di scelta rapida hello utilizzando hello **...**  pulsante all'hello estremità destra della tabella hello. Seleziona hello **eliminare** opzione.

![Rimuovere un'area][api-management-remove-region]

Confermare l'eliminazione di hello e fare clic su **salvare** modifiche hello tooapply.

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance tooa new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

