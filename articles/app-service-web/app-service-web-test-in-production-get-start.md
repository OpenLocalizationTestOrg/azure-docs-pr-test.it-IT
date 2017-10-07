---
title: aaaGet avviato con test nell'ambiente di produzione per le app Web
description: "Informazioni sulle funzionalità di produzione (TiP) nelle App Web di Azure App Service Ciao Test."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 4623468d-886e-4203-8012-8f86deb2790b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: cephalin
ms.openlocfilehash: 2ddbd532ffe2a4f3e07fd386d9741a3fde3639ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-test-in-production-for-web-apps"></a>Introduzione al test in ambiente di produzione per le app Web
Il test in ambiente di produzione, ovvero il test in diretta dell'app Web con il traffico dei clienti live, è una strategia di test che gli sviluppatori di app integrano sempre più spesso nella metodologia di [sviluppo Agile](https://en.wikipedia.org/wiki/Agile_software_development) . Consente di qualità hello tootest delle App con il traffico utente in tempo reale nell'ambiente di produzione, come dati toosynthesized anziché in un ambiente di test. Per esporre i nuovi utenti tooreal app, possono essere informati sui problemi relativi alle reali hello che può incontrare l'app dopo la distribuzione. È possibile verificare la funzionalità di hello, prestazioni e valore gli aggiornamenti di app su volume hello, velocità e la varietà del traffico utente reale, in cui non è mai simile in un ambiente di test.

## <a name="traffic-routing-in-app-service-web-apps"></a>Routing del traffico in app Web del servizio app
Con il Routing del traffico hello funzionalità in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), è possibile indirizzare una parte di tooone traffico utente in tempo reale o più [gli slot di distribuzione](web-sites-staged-publishing.md)e quindi analizzare l'app con [l'applicazione Azure Insights](/services/application-insights/) o [Azure HDInsight](/services/hdinsight/), o uno strumento di terze parti, ad esempio [New Relic](/marketplace/partners/newrelic/newrelic/) toovalidate la modifica. Ad esempio, è possibile implementare hello seguenti scenari con il servizio App:

* Individuare bug funzionale o individuare eventuali colli di bottiglia nella distribuzione di aggiornamenti precedenti toosite wide
* Eseguire "test controllato voli" delle modifiche misurando le metriche di usabilità per app di hello beta
* Gradualmente salita tooa nuovo aggiornamento e normalmente nuovamente verso il basso la versione corrente di toohello se si verifica un errore 
* Ottimizzare i risultati aziendali dell'app eseguendo [test A/B](https://en.wikipedia.org/wiki/A/B_testing) o [test multivariati](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing) in più slot di distribuzione

### <a name="requirements-for-using-traffic-routing-in-web-apps"></a>Requisiti per l'uso di Routing del traffico nelle app Web
* L'app Web deve essere eseguita nel piano **Standard** o **Premium**, come richiesto per slot di distribuzione multipli.
* In ordine toowork correttamente, il Routing del traffico richiede toobe i cookie abilitati nel browser degli utenti hello. Routing del traffico utilizza cookie toopin uno slot di distribuzione tooa browser client per la sessione di hello vita hello client.
* Routing del traffico supporta scenari di test in ambiente di produzione avanzati grazie ai cmdlet di Azure PowerShell.

## <a name="route-traffic-segment-tooa-deployment-slot"></a>Slot di distribuzione di route del traffico segmento tooa
A livello di base hello in ogni scenario di suggerimento, si distribuisce una percentuale predefinita dello slot di distribuzione non di produzione tooa traffico in tempo reale. toodo, questa procedura hello seguire seguente:

> [!NOTE]
> Hello questa procedura si presuppone che sia già un [slot di distribuzione non di produzione](web-sites-staged-publishing.md) e lo si desidera che hello contenuti dell'app web sono già [distribuito](web-sites-deploy.md) tooit.
> 
> 

1. Accedere al hello [portale Azure](https://portal.azure.com/).
2. Nel pannello dell'app Web fare clic su **Impostazioni** > **Routing del traffico**.
   ![](./media/app-service-web-test-in-production/01-traffic-routing.png)
3. Slot selezionare hello che si desidera che tooroute traffico tooand hello percentuale di traffico totale di hello è desiderato, quindi fare clic su **salvare**.
   
    ![](./media/app-service-web-test-in-production/02-select-slot.png)
4. Andare a pannello dello slot di distribuzione toohello. Viene visualizzato in tempo reale del traffico viene indirizzato tooit.
   
    ![](./media/app-service-web-test-in-production/03-traffic-routed.png)

Dopo aver configurato il Routing del traffico, hello specificati percentuale di client sarà slot non di produzione tooyour indirizzato in modo casuale. Tuttavia, è importante toonote che un client viene automaticamente indirizzato tooa specifico slot, sarà "bloccato" toothat slot per ciclo di vita di hello di tale sessione client. L'operazione viene eseguita tramite una sessione utente di cookie toopin hello. Se si osservano le richieste HTTP hello, si noterà un `TipMix` cookie in tutte le richieste successive.

![](./media/app-service-web-test-in-production/04-tip-cookie.png)

## <a name="force-client-requests-tooa-specific-slot"></a>Forzare slot specifico tooa di richieste client
In aggiunta tooautomatic il routing del traffico, servizio App è slot specifico di tooroute in grado di richieste tooa. Ciò è utile quando si desidera che il toobe di utenti in grado di tooopt-in o rifiutare esplicitamente l'app beta. toodo, utilizzare hello `x-ms-routing-name` parametro di query.

tooreroute utenti tooa slot specifico usando `x-ms-routing-name`, è necessario assicurarsi che tale slot hello è già stato aggiunto l'elenco di Routing del traffico toohello. Poiché si desidera tooroute tooa slot in modo esplicito, non è rilevante percentuale routing con hello effettiva che è impostata. Se si desidera, è possibile elaborare un "collegamento a beta" che consente agli utenti tooaccess hello app beta.

![](./media/app-service-web-test-in-production/06-enable-x-ms-routing-name.png)

### <a name="opt-users-out-of-beta-app"></a>Consentire agli utenti di rifiutare esplicitamente l'app beta
gli utenti toolet rifiutare esplicitamente l'app beta, ad esempio, è possibile inserire questo collegamento nella pagina web:

    <a href="<webappname>.azurewebsites.net/?x-ms-routing-name=self">Go back tooproduction app</a>

stringa Hello `x-ms-routing-name=self` specifica hello slot di produzione. Una volta hello collegamento hello accesso al browser client, non solo è reindirizzarlo toohello slot di produzione, ma tutte le richieste successive conterrà hello `x-ms-routing-name=self` cookie che blocca slot di produzione toohello sessione hello.

![](./media/app-service-web-test-in-production/05-access-production-slot.png)

### <a name="opt-users-in-toobeta-app"></a>Scegliere gli utenti nell'app toobeta
gli utenti toolet tooyour beta app consente di partecipare, set hello stessa query toohello nome del parametro dello slot di hello non di produzione, ad esempio:

        <webappname>.azurewebsites.net/?x-ms-routing-name=staging

## <a name="more-resources"></a>Altre risorse
* [Configurare ambienti di staging per le app Web nel servizio app di Azure](web-sites-staged-publishing.md)
* [Distribuire un'applicazione complessa in modo prevedibile in Azure](app-service-deploy-complex-application-predictably.md)
* [Agile Software Development con il servizio app di Azure](app-service-agile-software-development.md)
* [Usare efficacemente gli ambienti DevOps per le app Web](app-service-web-staged-publishing-realworld-scenarios.md)

