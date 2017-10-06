---
title: modelli di traffico di rete aaaVisualize con Watcher di rete di Azure e strumenti open source | Documenti Microsoft
description: Questa pagina vengono descritti come pacchetto Watcher di rete toouse capture Capanalysis toovisualize traffico modelli tooand dalle macchine virtuali.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a>Visualizzare tooand di modelli di traffico di rete dalle macchine virtuali utilizzando strumenti open source

Le acquisizioni di pacchetti contengono dati di rete che consentono di analisi forense rete tooperform e analisi approfondita dei pacchetti. Sono disponibili apre molti strumenti di origine è possibile utilizzare tooanalyze pacchetto acquisizioni toogain approfondimenti sulla rete. Uno di questi strumenti è CapAnalysis, uno strumento di visualizzazione dell'acquisizione pacchetti open source. Visualizzazione dei dati di acquisizione pacchetto è un modo utile tooquickly derivare informazioni dettagliate sui modelli e anomalie all'interno della rete. e di condividere tali informazioni in un modo facilmente utilizzabile.

Watcher di rete di Azure fornisce che si hello toocapture possibilità acquisisce dati importanti, consentendo tooperform pacchetti sulla rete. In questo articolo è fornire una procedura dettagliata di come toovisualize e ottenere informazioni dai pacchetti acquisisce con CapAnalysis Watcher di rete.

## <a name="scenario"></a>Scenario

Si dispone di un'applicazione web semplice distribuita in una macchina virtuale in Azure desidera toouse Apri origine strumenti toovisualize relativo tooquickly il traffico di rete identificare modelli di flusso e di eventuali anomalie possibili. Network Watcher permette di ottenere un'acquisizione pacchetti dell'ambiente di rete e di memorizzarla direttamente nell'account di archiviazione. CapAnalysis quindi inserimento hello acquisizione pacchetto direttamente dal blob di archiviazione hello e visualizzare il relativo contenuto.

![scenario][1]

## <a name="steps"></a>Passi

### <a name="install-capanalysis"></a>Installare CapAnalysis

tooinstall CapAnalysis in una macchina virtuale, è possibile fare riferimento le istruzioni ufficiale toohello https://www.capanalysis.net/ca/how-to-install-capanalysis qui.
In ordine di accesso CapAnalysis in modalità remota, è la porta tooopen 9877 nella VM aggiungendo una nuova regola di sicurezza in ingresso. Per ulteriori informazioni sulla creazione di regole nei gruppi di sicurezza di rete, fare riferimento troppo[creare regole in un gruppo esistente](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg). Una volta regola hello è stata aggiunta correttamente, dovrebbe essere in grado di tooaccess CapAnalysis da`http://<PublicIP>:9877`

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a>Utilizzare il Watcher di rete di Azure toostart sessione di acquisizione di un pacchetto

Watcher di rete consente il traffico di tootrack toocapture pacchetti da e verso una macchina virtuale. È possibile fare riferimento a istruzioni toohello [acquisizioni di pacchetti di gestione con Watcher di rete](network-watcher-packet-capture-manage-portal.md) toostart una sessione di acquisizione di pacchetti. Questa acquisizione pacchetto può essere archiviata in un toobe di archiviazione blob a cui accede CapAnalysis.

### <a name="upload-a-packet-capture-toocapanalysis"></a>Caricare un tooCapAnalysis acquisizione pacchetti
È possibile caricare direttamente un'acquisizione pacchetto eseguita dal controllo di rete utilizzando hello "importazione dalla scheda"URL e fornendo un blob di archiviazione toohello collegamento in cui è memorizzato l'acquisizione di pacchetti hello.

Se si fornisce un collegamento di tooCapAnalysis, assicurarsi che tooappend un URL di firma di accesso condiviso toohello token archiviazione blob.  toodo, passare la firma di accesso tooShared dall'account di archiviazione hello, designare hello consentita le autorizzazioni, quindi premere hello generare SAS pulsante toocreate un token. È quindi possibile aggiungere questo URL del blob archiviazione SAS toohello token pacchetto acquisizione.

Hello URL risultante avrà un aspetto simile al seguente: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere


### <a name="analyzing-packet-captures"></a>Analizzare le acquisizioni pacchetti

CapAnalysis offre varie opzioni toovisualize l'acquisizione pacchetto, ogni analisi fornita da una prospettiva diversa. Questi riepiloghi visivi permettono di comprendere le tendenze del traffico di rete e individuare rapidamente eventuali attività inconsuete. Alcune di queste funzionalità vengono visualizzate in hello seguente elenco:

1. Tabelle di flusso

    In questo modo tabella hello elenco di flussi di dati del pacchetto di hello, hello timestamp associato flussi hello e hello vari protocolli associati al flusso di hello, nonché di IP di origine e di destinazione.

    ![Pagina dei flussi di CapAnalysis][5]

1. Panoramica dei protocolli

    In questo riquadro consente tooquickly Vedere distribuzione hello del traffico di rete su hello diversi protocolli e aree geografiche.

    ![Panoramica dei protocolli di CapAnalysis][6]

1. Statistiche

    In questo riquadro consente alle statistiche sul traffico di rete di tooview: byte inviati e ricevuti dall'origine e destinazione IP, i flussi per ogni origine hello e di destinazione gli indirizzi IP, protocollo utilizzato per flussi diversi e la durata di hello dei flussi.

    ![Statistiche di CapAnalysis][7]

1. Mappa geografica

    Questo riquadro consente di visualizzare una mappa del traffico di rete, con colori scalabilità toohello volume di traffico da ogni paese. È possibile selezionare i paesi evidenziati tooview flusso ulteriori statistiche, ad esempio percentuale hello dei dati inviati e ricevuti da indirizzi IP in tale paese.

    ![Mappa geografica][8]

1. Filtri

    CapAnalysis include un set di filtri per l'analisi rapida di pacchetti specifici. Ad esempio, è possibile scegliere i dati di hello toofilter per informazioni dettagliate specifiche protocollo toogain a tale subset di traffico.

    ![filters][11]

    Visitare [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn ulteriori informazioni sulla funzionalità tutti CapAnalysis.

## <a name="conclusion"></a>Conclusioni

La funzionalità di acquisizione del Watcher di rete pacchetto consente toocapture hello tooperform necessario rete analisi forensi e comprendere meglio il traffico di rete. In questo scenario è stato illustrato come integrate facilmente le acquisizioni pacchetti di Network Watcher con strumenti di visualizzazione open source. Tramite strumenti open source, ad esempio acquisisce CapAnalysis toovisualize pacchetti, è possibile eseguire l'analisi approfondita dei pacchetti e identificare rapidamente le tendenze all'interno del traffico di rete.

## <a name="next-steps"></a>Passaggi successivi

toolearn ulteriori informazioni sui registri del flusso di gruppo, visitare [registra flusso NSG](network-watcher-nsg-flow-logging-overview.md)

Informazioni su come toovisualize il flusso di gruppo Registra con Power BI visitando [NSG visualizzare flussi di log con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png
