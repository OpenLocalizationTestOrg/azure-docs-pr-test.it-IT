---
title: aaaConfigure un nome di dominio personalizzato per un'app web in Azure App Service che Usa gestione traffico per il bilanciamento del carico.
description: Usare un nome di dominio personalizzato per un'app Web nel servizio app di Azure che usa Gestione traffico per il bilanciamento del carico.
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 0f96c0e7-0901-489b-a95a-e3b66ca0a1c2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: dfde5fc6b445b30b10e03dcb03e8d072130d9377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a>Configurazione di un nome di dominio personalizzato per un'app Web nel servizio app di Azure con Gestione traffico
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

Questo articolo fornisce istruzioni generiche sull'uso di un nome di dominio personalizzato con il servizio app di Azure in cui viene usato Gestione traffico per il bilanciamento del carico.

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>Informazioni sui record DNS
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a>Configurare le app Web per la modalità standard
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>Aggiunta di un record DNS per il dominio personalizzato
> [!NOTE]
> Se si hanno acquistato dominio tramite l'App Web di servizio App di Azure quindi passare alla procedura seguente fanno riferimento toohello passaggio finale della [acquistare dominio per le app Web](custom-dns-web-site-buydomains-web-app.md) articolo.
> 
> 

tooassociate il dominio personalizzato con un'app web nel servizio App di Azure, è necessario aggiungere una nuova voce nella tabella di hello DNS per il dominio personalizzato tramite gli strumenti forniti da hello registrar che è stato acquistato il nome del dominio. Utilizzare i seguenti passaggi toolocate hello e utilizzare gli strumenti per DNS hello.

1. Eseguire l'accesso account tooyour presso un registrar di dominio e cercare una pagina di gestione dei record DNS. Cercare i collegamenti o aree del sito hello etichettata come **nome di dominio**, **DNS**, o **denomina Gestione Server**. Spesso un collegamento toothis pagina sono disponibili da visualizzare le informazioni sull'account e quindi cercando, ad esempio un collegamento **My domains**.
2. Dopo aver trovato la pagina di gestione hello del nome di dominio, cercare un collegamento che consente i record DNS di tooedit hello. Questo collegamento può essere denominato **Zone file** o **DNS Records** oppure figurare come collegamento di configurazione in **Advanced**.
   
   * pagina Hello più probabile che abbiano già creato, ad esempio un'associazione di voce di alcuni record '**@**'o'\*' con una pagina 'parcheggio dominio'. Può anche contenere record per sottodomini comuni, ad esempio **www**.
   * pagina Hello verrà menzionato **record CNAME**, o fornire un elenco a discesa tooselect un tipo di record. È anche possibile che siano presenti voci per altri record, ad esempio **record A** e **record MX**. In alcuni casi, i record CNAME avranno una denominazione diversa, come ad esempio nel caso dei record **Alias**.
   * pagina Hello disporrà di campi che consentono di troppo**mappa** da un **nome Host** o **nome di dominio** tooanother nome di dominio.
3. Mentre specifiche hello di ogni registrar variano, in genere si esegue il mapping *da* nome di dominio personalizzato (ad esempio **contoso.com**,) *a* nome di dominio di Traffic Manager hello (**contoso.trafficmanager.net**) che viene utilizzato per l'app web.
   
   > [!NOTE]
   > In alternativa, se un record è già in uso ed è necessario toopreemptively associare tooit l'App, è possibile creare un record CNAME aggiuntivo. Ad esempio, l'associazione toopreemptively **www.contoso.com** tooyour app web, creare un record CNAME da **awverify.www** troppo**contoso.trafficmanager.net**. È quindi possibile aggiungere tooyour "www.contoso.com" App Web senza modificare i record CNAME di hello "www". Per altre informazioni, vedere [Creare record DNS per un'app Web in un dominio personalizzato][CREATEDNS].
   > 
   > 
4. Una volta completata l'aggiunta o la modifica di record DNS nel registrar, salvare le modifiche di hello.

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a>Abilitare Gestione traffico
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere hello [Centro per sviluppatori di Node.js](/develop/nodejs/).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
