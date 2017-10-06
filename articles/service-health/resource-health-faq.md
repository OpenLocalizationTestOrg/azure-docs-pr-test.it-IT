---
title: "domande frequenti sull'integrità delle risorse aaaAzure | Documenti Microsoft"
description: "Panoramica su Integrità risorse di Azure"
services: Resource health
documentationcenter: dev-center-name
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/05/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: fe29b2df1f9fee4b77d0100c7d872df837dc4b4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-faq"></a>Domande frequenti su Integrità risorse di Azure
Informazioni su hello risponde a domande toocommon sull'integrità delle risorse di Azure.

## <a name="what-is-azure-resource-health"></a>Che cos'è Integrità risorse di Azure?
Integrità risorse consente di eseguire una diagnosi e di ottenere supporto quando un problema di Azure ha effetto sulle risorse. Informato dello stato corrente e precedenti hello delle risorse e consente di attenuare i problemi. Integrità risorse offre supporto tecnico quando è necessaria assistenza per problemi con i servizi di Azure.  

## <a name="what-is-hello-resource-health-intended-for"></a>Che cos'è integrità delle risorse destinate hello?
Una volta che è stato rilevato un problema con una risorsa, integrità delle risorse può aiutare a diagnosticare causa radice di hello. Fornisce problema hello toomitigate di Guida e supporto tecnico quando è necessario ulteriori informazioni su problemi del servizio di Azure.

## <a name="what-health-checks-are-performed-by-resource-health"></a>Quali controlli di integrità vengono eseguiti da Integrità risorse?
Integrità delle risorse esegue vari controlli in base a hello [tipo di risorsa](resource-health-checks-resource-types.md). Questi controlli sono progettate tooimplement tre tipi di problemi: 
- Eventi non pianificati, ad esempio un riavvio imprevisto dell'host
- Eventi pianificati, ad esempio aggiornamenti pianificati del sistema operativo host
- Eventi attivati dalle azioni dell'utente, ad esempio il riavvio di una macchina virtuale

## <a name="what-does-each-of-hello-health-status-mean"></a>Ogni stato di integrità hello cosa?
Esistono tre stati di integrità diversi:
- Disponibile: Non ci siano problemi noti nella piattaforma Azure che potrebbe incidere sulla risorsa hello
- Non disponibile: Integrità delle risorse ha rilevato problemi che influiscono negativamente sulla risorsa hello
- Sconosciuto: Integrità delle risorse può non determinare hello integrità di una risorsa perché ha interrotto la ricezione di informazioni su di esso. 

## <a name="what-does-hello-unknown-status-mean-is-something-wrong-with-my-resource"></a>Cosa hello Media uno stato sconosciuto. Indica un problema relativo alla risorsa?
lo stato di integrità Hello è impostato toounknown quando l'integrità delle risorse non riceve informazioni su una risorsa specifica. Questo stato non è un'indicazione dello stato di hello della risorsa hello, nei casi in cui si verificano problemi, definitiva potrebbe indicare che un problema di Azure.

## <a name="how-can-i-get-help-for-a-resource-that-is-unavailable"></a>Come è possibile ottenere supporto per una risorsa che non è disponibile?
È possibile inviare una richiesta di supporto dal Pannello di hello integrità delle risorse. Non è necessario un contratto con Microsoft tooopen una richiesta quando non è disponibile la risorsa hello perché gli eventi della piattaforma.

## <a name="does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did"></a>Integrità risorse è in grado di differenziare tra una mancata disponibilità dovuta a problemi della piattaforma e un'operazione eseguita dall'utente?
Sì, quando una risorsa è disponibile, l'integrità delle risorse identifica hello causa all'interno di una di queste categorie: 
-   Azione avviata dall'utente
-   Evento pianificato 
-   Evento non pianificato

Nel portale di hello avviata dall'utente sono riportate le azioni utilizzando l'icona di notifica blu, mentre gli eventi pianificati e sono visualizzati con un'icona di avviso rossa. Vengono forniti ulteriori dettagli in hello [Panoramica di integrità delle risorse](Resource-health-overview.md).  

## <a name="can-i-integrate-resource-health-with-my-monitoring-tools"></a>È possibile aggiungere Integrità risorse agli strumenti di monitoraggio personali?
Integrità delle risorse è un toohelp servizio progettato diagnosticare e attenuare i problemi del servizio Azure che influiscono le risorse. Sebbene sia possibile utilizzare hello API integrità risorse tooprogrammatically ottenere lo stato di integrità hello, si consiglia di che usare toomonitor le metriche delle risorse. Una volta che viene rilevato un problema, integrità delle risorse consente di determinare la causa principale di hello e in modo semplificato azioni tooaddress li. Visitare [Monitor Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) toolearn ulteriori informazioni sull'utilizzo di toocheck le metriche delle risorse.

## <a name="where-do-i-find-resource-health"></a>Dove si trova Integrità risorse?
Dopo l'accesso toohello portale di Azure, sono disponibili più modi per accedere integrità delle risorse:
- Passare tooyour risorse. Nella finestra di navigazione a sinistra di hello, selezionare **integrità delle risorse**
- Andare a pannello monitoraggio Azure toohello.  Nella finestra di navigazione a sinistra di hello, selezionare **integrità delle risorse**.
- Aprire hello **della Guida e supporto** pannello selezionando hello punto interrogativo in hello alto a destra del portale hello e quindi selezionando **della Guida e supporto**. Una volta aperto il pannello hello, selezionare **integrità delle risorse**

È possibile utilizzare anche hello API integrità risorse tooobtain informazioni sull'integrità hello delle risorse.

## <a name="is-resource-health-available-for-all-resource-types"></a>Integrità risorse è disponibile per tutti i tipi di risorse?
Hello elenco di tipi di risorsa supportati tramite l'integrità delle risorse e i controlli di integrità è reperibile [qui](resource-health-checks-resource-types.md).

## <a name="what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not"></a>Quale operazione è necessario eseguire se la risorsa risulta disponibile ma si ritiene che non lo sia?
Durante il controllo integrità hello di una risorsa, immediatamente sotto lo stato di integrità hello è possibile fare clic su **segnalare lo stato di integrità corretto**. Prima di inviare report hello, è possibile hello fornire ulteriori informazioni sul motivo per cui si ritiene che lo stato di integrità corrente hello è corretto.

## <a name="is-resource-health-available-for-all-azure-regions"></a>Integrità risorse è disponibile in tutte le aree di Azure? 
Integrità delle risorse è disponibile in tra geos Azure tutti tranne hello seguenti aree:
- US Gov Virginia
- Governo degli Stati Uniti - Iowa
- Dipartimento della difesa Stati Uniti orientali
- Dipartimento della difesa Stati Uniti centrali
- Germania centrale
- Germania nord-orientale
- Cina orientale
- Cina settentrionale

## <a name="how-is-resource-health-different-from-hello-service-health-dashboard-or-hello-azure-portal-service-notifications"></a>Come è diverso da notifiche del servizio del portale Azure Dashboard di integrità del servizio o hello hello integrità delle risorse?
informazioni di Hello fornite dall'integrità delle risorse sono più specifiche rispetto a quello fornito da hello Dashboard di integrità del servizio di Azure.

Mentre [stato Azure](https://status.azure.com) e notifiche del servizio portale hello informano i problemi del servizio che interessano una vasta gamma di clienti (ad esempio un'area di Azure), l'integrità delle risorse espone gli eventi più granulari che sono rilevanti solo toohello risorsa specifica. Se, ad esempio, un host viene riavviato in modo imprevisto, Integrità risorse avvisa solo i clienti le cui macchine virtuali sono in esecuzione nell'host.

È importante toonotice che tooprovide che completa visibilità degli eventi conseguenze per le risorse, anche gli eventi di superfici pubblicati nelle notifiche di servizio integrità delle risorse e hello Dashboard di integrità del servizio.

## <a name="do-i-need-tooactivate-resource-health-for-each-resource"></a>È necessario tooactivate integrità delle risorse per ogni risorsa?
No, le informazioni di integrità sono disponibili per tutti i tipi di risorse supportati da Integrità risorse. 

## <a name="do-we-need-tooenable-resource-health-for-my-organization"></a>È necessario tooenable integrità delle risorse per l'organizzazione?
No.  Integrità delle risorse di Azure è accessibile all'interno di hello portale di Azure senza alcun requisito di installazione.

## <a name="is-resource-health-available-free-of-charge"></a>Integrità risorse è disponibile gratuitamente?
Sì.  Integrità risorse di Azure è gratuito.

## <a name="what-are-hello-recommendations-that-resource-health-provides"></a>Quali sono i suggerimenti di hello che fornisce integrità delle risorse?
In base allo stato di integrità hello, integrità delle risorse vengono forniti consigli con l'obiettivo di hello di ridurre il tempo di hello è impiegato per la risoluzione dei problemi. Per le risorse disponibili, hello lo stato attivo per indicazioni su come toosolve hello più comuni problemi riscontrati. Se sono disponibile a causa di risorse hello tooan Azure evento non pianificato, lo stato attivo hello saranno per assistenza durante e dopo il processo di ripristino hello. 

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni su Integrità risorse:
-  [Panoramica su Integrità risorse di Azure](Resource-health-overview.md)
-  [Tipi di risorse e controlli integrità disponibili in Integrità risorse di Azure](resource-health-checks-resource-types.md)
