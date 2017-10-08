---
title: Tipi di Endpoint di gestione aaaTraffic | Documenti Microsoft
description: "Questo articolo illustra tipi diversi di endpoint che è possibile usare con Gestione traffico di Azure"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 4e506986-f78d-41d1-becf-56c8516e4d21
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: kumud
ms.openlocfilehash: 787412ac6207f76791bf3ff753d1df2767b1a964
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-endpoints"></a>Endpoint di Gestione traffico
Microsoft Azure Traffic Manager consente il traffico di rete è toocontrol distributed tooapplication distribuzioni in esecuzione in Data Center diversi. In Gestione traffico ogni distribuzione di applicazioni viene configurata come "endpoint". Quando Gestione traffico riceve una richiesta DNS, viene scelto un tooreturn endpoint disponibile in hello risposta DNS. Gestione traffico si basa sullo stato dell'endpoint corrente di hello e metodo di routing del traffico hello scelta hello. Per altre informazioni, vedere [Modalità di funzionamento di Gestione traffico](traffic-manager-how-traffic-manager-works.md).

Gli endpoint supportati da Gestione traffico sono di tre tipi:
* **Endpoint di Azure** , usati per i servizi ospitati in Azure.
* **Endpoint esterni** , usati per i servizi ospitati all'esterno di Azure, in locale o da un provider di hosting diverso.
* **Annidati endpoint** è toocreate i profili di Traffic Manager toocombine utilizzati più flessibile di routing del traffico schemi toosupport hello esigenze delle distribuzioni più grandi e complesse.

Non ci sono limitazioni al modo in cui è possibile combinare tipi di endpoint diversi in un unico profilo di Gestione traffico. Ogni profilo può contenere qualsiasi combinazione di tipi di endpoint.

Hello le sezioni seguenti vengono descritti ciascun tipo di endpoint in modo più approfondito.

## <a name="azure-endpoints"></a>Endpoint di Azure

In Gestione traffico gli endpoint di Azure vengono usati per i servizi basati su Azure. è supportato i seguenti tipi di risorse di Azure Hello:

* Macchine virtuali IaaS "classiche" e servizi cloud PaaS.
* App Web
* Risorse PublicIPAddress (che possono essere tooVMs connessi direttamente o tramite un servizio di bilanciamento del carico di Azure). Hello publicIpAddress deve avere un nome DNS assegnato toobe utilizzati in un profilo di Traffic Manager.

Le risorse PublicIPAddress sono risorse di Azure Resource Manager. Non esistono nel modello di distribuzione classica hello. Sono quindi supportate unicamente nelle esperienze di Gestione traffico di tipo Azure Resource Manager. altri tipi di endpoint Hello sono supportate tramite Gestione risorse sia hello modello di distribuzione classica.

Quando si usano gli endpoint di Azure, Gestione trafficorileva l'arresto o l'avvio di una macchina virtuale IaaS "classica", di un servizio cloud o di un'app Web. Questo stato si riflette in stato di endpoint hello. Per altri dettagli, vedere [Monitoraggio e failover degli endpoint di Gestione traffico](traffic-manager-monitoring.md#endpoint-and-profile-status). Quando viene arrestato il servizio sottostante hello, Traffic Manager non esegue controlli di integrità dell'endpoint o endpoint toohello il traffico diretto. Nessuna gestione traffico si verificano eventi di fatturazione per hello ha arrestato l'istanza. Quando si riavvia servizio hello, fatturazione riprende endpoint hello è traffico tooreceive idoneo. Questo rilevamento tooPublicIpAddress endpoint non è valida.

## <a name="external-endpoints"></a>Endpoint esterni

Gli endpoint esterni vengono usati per i servizi esterni a Azure. Può trattarsi, ad esempio, di un servizio ospitato in locale o da un provider diverso. Endpoint esterni possono essere usati singolarmente o combinati con gli endpoint di Azure in hello stesso profilo di Traffic Manager. La combinazione di endpoint di Azure con endpoint esterni consente un'ampia gamma di scenari:

* In entrambi un modello di failover attivo-attivo o attivo-passivo, utilizzare la ridondanza tooprovide Azure aumentato per un'applicazione locale esistente.
* latenza dell'applicazione tooreduce per gli utenti in tutto il mondo hello, estendere un esistente locale applicazione tooadditional posizioni geografiche in Azure. Per altre informazioni, vedere [Metodo di routing del traffico Prestazioni](traffic-manager-routing-methods.md#performance).
* Utilizzare Azure tooprovide capacità aggiuntiva per un'applicazione locale esistente, in modo continuato o come un toomeet soluzione 'burst-to-cloud' un picco nella richiesta.

In alcuni casi, è utile toouse endpoint esterni tooreference Azure servizi (per gli esempi, vedere hello [domande frequenti su](traffic-manager-faqs.md#traffic-manager-endpoints)). In questo caso, controlli di integrità vengono fatturati hello endpoint di Azure tasso, non hello endpoint esterni. Tuttavia, diversamente dagli endpoint di Azure, se si arresta o Elimina hello sottostante servizio, controllo di integrità fatturazione continua fino a quando non si disabilita o eliminare endpoint hello in Traffic Manager.

## <a name="nested-endpoints"></a>Endpoint annidati

Gli endpoint nidificati combinano più Traffic Manager profili toocreate flessibile routing del traffico schemi e supportano le esigenze di hello delle distribuzioni più grandi e complesse. Con gli endpoint annidate, viene aggiunto un profilo di 'child' come profilo endpoint tooa 'parent'. Entrambi i profili di hello padre e figlio possono contenere altri endpoint di qualsiasi tipo, inclusi altri profili nidificati. Per altre informazioni, vedere [nested Traffic Manager profiles](traffic-manager-nested-profiles.md)(Profili nidificati di Gestione traffico).

## <a name="web-apps-as-endpoints"></a>App Web come endpoint

Per la configurazione di app Web come endpoint in Gestione traffico si rendono necessarie alcune considerazioni aggiuntive:

1. App Web solo hello SKU 'Standard' o superiore sono idonee per l'utilizzo con gestione traffico. Prova tooadd un'App Web di un errore SKU inferiore. Downgrade hello SKU di un'App Web esistente comporta in Traffic Manager non è più l'invio di traffico toothat App Web.
2. Quando un endpoint riceve una richiesta HTTP, Usa intestazione 'host' hello in hello richiesta toodetermine quale App Web deve richiedere hello di servizio. intestazione host Hello contiene hello DNS utilizzato tooinitiate hello richiesta del nome, ad esempio 'contosoapp.azurewebsites.net'. un nome DNS diverso con l'App Web, nome DNS hello toouse deve essere registrato come un nome di dominio personalizzato per hello App. Quando si aggiunge un endpoint di App Web come un endpoint di Azure, nome DNS del profilo di Traffic Manager hello viene automaticamente registrato per hello App. Questa registrazione viene rimosso automaticamente quando endpoint hello viene eliminato.
3. Ogni profilo di Gestione traffico può avere al massimo un endpoint di app Web da ogni area di Azure. toowork intorno per questo vincolo, è possibile configurare un'App Web come endpoint esterno. Per ulteriori informazioni, vedere hello [domande frequenti su](traffic-manager-faqs.md#traffic-manager-endpoints).

## <a name="enabling-and-disabling-endpoints"></a>Abilitazione e disabilitazione di endpoint

Disabilitazione di un endpoint in Gestione traffico può essere utile tootemporarily remove traffico da un endpoint che è in modalità di manutenzione o in corso di ridistribuzione. Quando viene eseguito di nuovo endpoint hello, è possibile abilitarla di nuovo.

Gli endpoint possono essere abilitati e disabilitati tramite portale di gestione traffico hello, PowerShell, CLI o l'API REST, ognuno dei quali sono supportate in Gestione risorse sia il modello di distribuzione classica hello.

> [!NOTE]
> Disabilitazione di un endpoint di Azure non ha nulla toodo con lo stato di distribuzione in Azure. Un Azure del servizio (ad esempio una macchina virtuale o l'App Web rimane in esecuzione e in grado di traffico tooreceive anche se è disabilitato in Traffic Manager. Traffico può essere indirizzato direttamente toohello istanza del servizio anziché tramite Gestione traffico hello nome DNS del profilo. Per altre informazioni, vedere [Modalità di funzionamento di Gestione traffico](traffic-manager-how-traffic-manager-works.md).

idoneità al corrente di Hello del traffico di tooreceive ogni endpoint dipende da hello seguenti fattori:

* stato del profilo Hello (abilitato/disabilitato)
* stato endpoint Hello (abilitato/disabilitato)
* risultati Hello hello di controlli di integrità per l'endpoint

Per altre informazioni, vedere [Informazioni sul monitoraggio di Gestione traffico](traffic-manager-monitoring.md#endpoint-and-profile-status).

> [!NOTE]
> Poiché Traffic Manager funziona hello livello DNS, è Impossibile tooinfluence endpoint di tooany connessioni esistente. Quando un endpoint è disponibile, gestione traffico indirizza nuove connessioni tooanother disponibili dell'endpoint. Tuttavia, host hello dietro hello disabilitato o non integro endpoint possono continuare tooreceive traffico tramite le connessioni esistenti, fino a quando tali sessioni vengono terminate. Le applicazioni è consigliabile limitare hello sessione durata tooallow traffico toodrain da connessioni esistenti.

Se tutti gli endpoint in un profilo sono disabilitati o profilo hello stesso è disabilitato, verrà inviata un' 'NXDOMAIN' risposta tooa nuova query DNS.


## <a name="next-steps"></a>Passaggi successivi

* Informazioni sul [funzionamento di Gestione traffico](traffic-manager-how-traffic-manager-works.md).
* Informazioni sul [monitoraggio degli endpoint e sul failover automatico](traffic-manager-monitoring.md)di Gestione traffico.
* Informazioni sui [metodi di routing del traffico](traffic-manager-routing-methods.md)di Gestione traffico.
