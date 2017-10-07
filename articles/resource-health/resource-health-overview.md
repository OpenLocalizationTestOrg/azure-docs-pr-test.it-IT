---
title: Panoramica dello stato delle risorse aaaAzure | Documenti Microsoft
description: "Panoramica su Integrità risorse di Azure"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 06/01/2016
ms.author: BernardoAMunoz
ms.openlocfilehash: b920241b2f64a0695ba2c32e9ccb0c2c3739986d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-overview"></a>Panoramica su Integrità risorse di Azure
 
Integrità risorse consente di eseguire una diagnosi e di ottenere supporto quando un problema di Azure ha effetto sulle risorse. Informato dello stato corrente e precedenti hello delle risorse e consente di attenuare i problemi. Integrità risorse offre supporto tecnico quando è necessaria assistenza per problemi con i servizi di Azure.

Mentre [stato Azure](https://status.azure.com) informare sui problemi di servizio che interessano una vasta gamma di clienti di Azure, l'integrità delle risorse offre un dashboard di integrità hello delle risorse personalizzato. Integrità delle risorse viene sempre hello le risorse non sono disponibili in hello scaduta tooAzure i problemi del servizio. Questo rende semplice per è toounderstand se è stato violato un contratto di servizio. 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a>Qual è la definizione di "risorsa" e in che modo Integrità risorse stabilisce se una risorsa è integra o meno?
Una risorsa è un'istanza di un tipo di risorsa messo a disposizione da un servizio di Azure tramite Azure Resource Manager, ad esempio una macchina virtuale, un'app Web o un database SQL.

Integrità delle risorse si basa su segnali emessi da hello diversi servizi Azure tooassess se una risorsa è integro o non. Se una risorsa non è integra, integrità delle risorse analizza le informazioni aggiuntive toodetermine hello causa hello problema. Vengono inoltre identificati azioni che richiede Microsoft problema hello toofix o quali azioni da eseguire tooaddress hello causano del problema hello. 

Elenco completo di hello revisione dei tipi di risorse e l'integrità controlla [integrità delle risorse Azure](resource-health-checks-resource-types.md) per ulteriori informazioni sulle modalità di valutazione di integrità.

## <a name="health-status-provided-by-resource-health"></a>Stato di integrità indicato da Integrità risorse
integrità Hello di una risorsa è uno dei seguenti stati hello:

### <a name="available"></a>Disponibile
servizio Hello non è stata rilevata tutti gli eventi che hanno un impatto integrità hello della risorsa hello. Nei casi in cui risorse hello è stata ripristinata da tempi di inattività imprevisti durante hello ultime 24 ore, verrà visualizzato hello **ripristinato di recente** notifica.

![Integrità risorse: macchina virtuale con stato Disponibile](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a>Non disponibile
Hello servizio ha rilevato un evento di non piattaforma conseguenze integrità hello della risorsa hello o di piattaforma in corso.

#### <a name="platform-events"></a>Eventi piattaforma
Questi eventi vengono attivati da più componenti di infrastruttura di Azure hello e includono sia azioni pianificate come la manutenzione pianificata e gli eventi imprevisti imprevisti come il riavvio di un host non pianificato.

Integrità delle risorse sono disponibili ulteriori dettagli sull'evento hello, il processo di ripristino di hello e consente il supporto toocontact anche se non si dispone di Microsoft active contratto di supporto.

![Risorsa integrità disponibile macchina virtuale a causa di eventi tooplatform](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a>Eventi non piattaforma
Questi eventi vengono attivati da azioni eseguite dagli utenti, ad esempio l'arresto di una macchina virtuale o raggiungere hello il numero massimo di connessioni tooa Cache Redis.

![Risorsa integrità disponibile macchina virtuale a causa di evento toonon piattaforma](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a>Sconosciuto
Questo stato indica che Integrità risorse non ha ricevuto informazioni sulla risorsa per più di 10 minuti. Sebbene questo stato non è un'indicazione dello stato di hello della risorsa hello definitiva, è un punto dati importanti nel processo di risoluzione dei problemi di hello:
* Se la risorsa hello è in esecuzione allo stato previsto hello della risorsa hello aggiornerà tooAvailable dopo alcuni minuti.
* Se si verificano problemi con la risorsa hello, hello lo stato di integrità sconosciuto può suggerire risorse hello sono stata interessata da un evento nella piattaforma hello.

![Integrità risorse: macchina virtuale con stato Sconosciuto](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a>Segnalare uno stato non corretto
Se in qualsiasi momento si ritiene che lo stato di integrità corrente hello è corretto, è possibile segnalarlo facendo **segnalare lo stato di integrità corretto**. Nei casi in cui sono interessati da un problema di Azure, si consiglia di supporto toocontact dal pannello integrità della risorsa hello. 

![Integrità risorse: report di stato non corretto](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a>Informazioni sulla cronologia
I giorni too14 dei dati cronologici di integrità di cui è possibile accedere facendo clic su **Visualizza cronologia** nel Pannello di integrità risorsa hello. 

![Integrità risorse: report della cronologia](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a>introduttiva
tooopen integrità delle risorse per una risorsa
1.  Accedere in hello portale di Azure.
2.  Passare tooyour risorse.
3.  Scegliere dal menu risorse hello si trova nella parte sinistra hello **integrità delle risorse**.

![Aprire Integrità risorse dal pannello della risorsa](./media/resource-health-overview/from-resource-blade.png)

È inoltre possibile accedere integrità delle risorse facendo **più servizi**e digitando **integrità delle risorse** in hello tooopen casella testo di filtro **della Guida e supporto** blade. Infine fare clic su [**Integrità risorse**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).

![Aprire Integrità risorse da Altri servizi](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a>Passaggi successivi

Consultare queste risorse toolearn più sull'integrità delle risorse:
-  [Tipi di risorse e controlli di integrità in Integrità risorse di Azure](resource-health-checks-resource-types.md)
-  [Domande frequenti su Integrità risorse di Azure](resource-health-faq.md)




