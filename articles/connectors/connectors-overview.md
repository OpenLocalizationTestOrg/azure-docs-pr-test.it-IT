---
title: aaaOverview dei connettori App logica | Documenti Microsoft
description: Panoramica dei connettori utilizzabili in un'app per la logica
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: ca8dab2e-9b69-4b1e-865d-1facd9f0cdac
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan
ms.openlocfilehash: dc4cac4c0dfaa2f9fd218ffc04414fa8e52a91d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-in-a-logic-app"></a>Uso dei connettori in un'app per la logica
Connettori forniscono accesso rapido tooevents, dati e le azioni tra piattaforme, protocolli e servizi.  elenco completo di Hello di connettori che supporta le app di logica possibile [sono disponibili qui](apis-list.md).  Connettori può essere utilizzati come un trigger o un'azione in un'app di logica, è possibile che configurato *connessione* toouse (ad esempio: autorizzare un Twitter account tooaccess o post per conto dell'utente).

## <a name="basics"></a>Nozioni di base
I connettori sono servizi ospitati, è possibile accedere come parte di un toointegrate app logica con altri servizi come Dynamics, Azure, Salesforce, [e altre](apis-list.md).  Sono distribuiti e gestiti da Microsoft, pertanto è possibile creare flussi di lavoro di integrazione che prevedono scalabilità, velocità e sicurezza.  È possibile aggiungere un'app di logica tooa connettore, la ricerca e selezionare un'azione di connettore o attivare in **Mostra Microsoft API gestite**.

![Menu delle azioni per la selezione dei trigger][1]

Ogni azione connettore o un trigger sarà necessario un set di proprietà tooconfigure.  È possibile fare clic su hello info pulsanti toolearn ulteriori informazioni sull'azione o la documentazione di riferimento [toolearn più](apis-list.md).

Se si desidera toointegrate con un servizio o l'API che non è ancora un connettore, è anche possibile estendere la logica App tramite un [connettore personalizzato](../logic-apps/logic-apps-create-api-app.md) o semplicemente chiamare direttamente il servizio di toohello tramite un protocollo HTTP.

## <a name="triggers"></a>Trigger
Alcuni connettori dispongono di un trigger, ovvero un evento da tale connettore verrà generato una app per la logica e passare tutti i dati come parte del trigger hello.  Un trigger è sempre innanzitutto hello in un'app di logica.  Trigger comuni includono operazioni quali:

* Ricorrenza - da eseguire ogni ora
* Quando viene ricevuta una richiesta HTTP
* Quando un elemento viene aggiunto tooa coda
* Quando viene ricevuto un messaggio di posta elettronica

Alcuni trigger vengono attivati hello immediata si verifica un evento in una notifica toohello logica App e altri sarà necessario un intervallo di ricorrenza configurato nella frequenza hello logica app controllerà servizio hello per un evento (backup tooevery 15 secondi).  

Una volta ricevuto un evento, verrà attivati hello logica applicazione in esecuzione e azioni hello nel flusso di lavoro hello verranno avviata.  Sarà inoltre possibile tooaccess in grado di attivano i dati provenienti da hello nel corso del flusso di lavoro di hello (per hello esempio 'in un nuovo tweet' trigger verranno passate tweet hello in hello eseguire).

## <a name="actions"></a>Azioni
La maggior parte dei connettori dispongono di uno o più azioni che possono essere eseguite come parte del flusso di lavoro hello.  Le azioni sono operazioni che si verificano dopo l'esecuzione di hello generato da un trigger.  tooadd un'azione, fare clic su hello **nuovo passaggio** pulsante e cercare hello connettore desiderato toouse.  Una volta selezionato (e dopo la configurazione delle [connessioni](#connections) che potrebbe essere necessario) verrà visualizzato scheda azione hello è possibile configurare.  È possibile selezionare i dati nei passaggi precedenti, fare clic su uno dei token per gli output di hello o immettere in qualsiasi altra configurazione in base alle esigenze.

![Configurazione di un'azione connettore][2]

## <a name="connections"></a>Connessioni
La maggior parte dei connettori richiedono tooconfigure un *connessione* prima di poter usare il connettore di hello.  Oggetto *connessione* qualsiasi account di accesso o configurazione della connessione necessari connettore hello tooaccess.  Per i connettori che utilizza OAuth, creare una connessione significa che la firma nel servizio hello (ad esempio Office 365, Salesforce o GitHub) in cui il token di accesso possa essere crittografato e archiviato in modo sicuro in un archivio segreto di Azure.  Altri connettori (come SQL e FTP) richiedono una connessione che contenga una configurazione come l'indirizzo del server, il nome utente e la password.  Questi dettagli di configurazione della connessione vengono inoltre crittografati e archiviati in modo sicuro.  Connessioni saranno in grado di tooaccess servizio hello per come servizio hello consente.  Per le connessioni di OAuth di Azure Active Directory (ad esempio Office 365 e Dynamics) è possibile procedere in modo indefinito token di accesso toorefresh hello.  Altri servizi possono imporre limiti sul periodo di utilizzabilità di un token senza aggiornamento.  In genere determinate azioni quali la modifica di una password invalideranno tutti i token di accesso.  

Le connessioni possono essere visualizzate e gestite in Azure facendo clic su **Sfoglia** e selezionando **Connessioni API**.  Da hello risorsa API connessioni può visualizzare, modificare, aggiornare o autorizzare di nuovo tutte le connessioni create.

## <a name="next-steps"></a>Passaggi successivi
* [Creare la prima app per la logica](../logic-apps/logic-apps-create-a-logic-app.md)
* [Usi ed esempi comuni sulle app per la logica](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Introduzione ai trigger e alle azioni di integrazione aziendale](../logic-apps/logic-apps-enterprise-integration-overview.md)

<!--Image References -->
[1]: ./media/connectors-overview/addAction.png
[2]: ./media/connectors-overview/configureAction.png
