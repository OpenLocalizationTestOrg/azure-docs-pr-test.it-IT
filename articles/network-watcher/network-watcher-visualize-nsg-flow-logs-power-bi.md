---
title: flusso di Azure Network Security Group aaaVisualizing registra con Power BI | Documenti Microsoft
description: Questa pagina vengono descritti come flusso NSG toovisualize registra con Power BI.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d9adcf256df8fed68c39be1a026ca64cc6b5c6d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a>Visualizzare i log dei flussi dei gruppi di sicurezza di rete con Power BI

I registri del flusso di gruppo di sicurezza di rete consentono di tooview informazioni sul traffico IP in ingresso e uscita sui gruppi di sicurezza di rete. Questi log flusso mostrano in uscita e i flussi in ingresso per ogni regola, hello flusso hello NIC applica, 5 tuple informazioni flusso hello (origine/destinazione IP, porta di origine/destinazione, Protocol), e se il traffico hello consentito o negato.

Può essere difficile toogain approfondite del flusso di registrazione dei dati tramite la ricerca di file di log hello manualmente. In questo articolo è fornire una soluzione toovisualize più recente del flusso di log e apprendere il traffico di rete.

## <a name="scenario"></a>Scenario

Connessione è hello seguente scenario, è stato configurato come sink hello per i dati di flusso di registrazione NSG account di archiviazione di Power BI desktop toohello. Dopo la connessione di account di archiviazione tooour, Power BI Scarica e analizza hello registri tooprovide una rappresentazione visiva del traffico hello che viene registrato tramite gruppi di sicurezza di rete.

Utilizzo di oggetti visivi hello forniti nel modello di hello che è possibile esaminare:

* Talker principali
* Dati di flusso della serie temporale in base alla direzione e alla regola decisa
* Flussi in base all'indirizzo MAC dell'interfaccia di rete
* Flussi in base al gruppo di sicurezza di rete e alla regola
* Flussi in base alla porta di destinazione

modello di Hello fornito non è modificabile in modo è possibile modificarlo tooadd nuovi dati, gli oggetti visivi, o modificare query toosuit le proprie esigenze.

## <a name="setup"></a>Configurazione

Prima di iniziare, è necessario abilitare la registrazione dei flussi dei gruppi di sicurezza di rete in uno o più gruppi di sicurezza di rete nell'account usato. Flusso di log per istruzioni sull'abilitazione di sicurezza di rete, consultare l'articolo seguente toohello: [registrazione tooflow introduzione per gruppi di sicurezza di rete](network-watcher-nsg-flow-logging-overview.md).

È inoltre necessario il client di Power BI Desktop hello installato nel computer in uso e sufficiente spazio libero nel computer toodownload e carico hello log dati che è presente nell'account di archiviazione.

![Diagramma di Visio][1]

### <a name="steps"></a>Passi

1. Scaricare e aprire hello segue il modello di Power BI in Power BI Desktop applicazione hello [flusso PowerBI Watcher di rete registri modello](https://aka.ms/networkwatcherpowerbiflowlogstemplate)
1. Immettere i parametri di Query hello richiesto
    1. **StorageAccountName** – toohello specifica il nome dell'account di archiviazione hello contenente il flusso NSG hello log che si desideri tooload e visualizzare.
    1. **NumberOfLogFiles** : Specifica il numero di hello del file di log che desideri toodownload e visualizzare in Power BI. Ad esempio, se si specifica 50, hello 50 file di log più recenti. Abbiamo 2 NSGs FF abilitata e configurata toosend NSG flusso registri toothis account, quindi hello nelle ultime 25 ore dei log possono essere visualizzate.

    ![schermata principale di Power BI][2]

1. Immettere la chiave di accesso dell'account di archiviazione hello. È possibile trovare le chiavi di accesso valido passando tooyour account di archiviazione in Azure nel portale e selezionando hello **chiavi di accesso** dal menu Impostazioni hello. Fare clic su **Connetti** e quindi applicare le modifiche.

    ![chiavi di accesso][3]

    ![chiave di accesso 2][4]

4.  I log sono scaricare e analizzato e ora è possibile utilizzare gli oggetti visivi creati in precedenza hello.

## <a name="understanding-hello-visuals"></a>Comprendere gli oggetti visivi hello

Condizione in hello modello sono un set di oggetti visivi che consentono di senso di hello dati gruppo flusso di Log. Hello immagini seguenti mostrano un esempio dell'aspetto quando popolata con dati quale dashboard hello. Di seguito vengono esaminati in dettaglio i singoli oggetti visivi 

![Power BI][5]
 
Talkers Top Hello Mostra visual hello gli indirizzi IP che hanno avviato hello la maggior parte delle connessioni su hello periodo specificato. dimensioni di Hello delle caselle hello corrispondono toohello numero di connessioni. 

![Top Talkers][6]

Hello grafici di serie temporali seguente mostrano il numero di hello di flussi periodo hello. grafico superiore Hello è segmentata per la direzione di flusso hello e hello inferiore è segmentata per decisione hello (Consenti o Nega). Con questo oggetto visivo è possibile esaminare le tendenze relative al traffico nel tempo e identificare eventuali cali o picchi anomali nel traffico o nella sua segmentazione.

![flussi nel periodo][7]

Hello seguenti grafici mostrano flussi hello per ogni interfaccia di rete, con segmentate per la direzione di flusso hello superiore e inferiore hello segmentate per decisione presa. Con queste informazioni, è possibile ottenere informazioni approfondite che delle macchine virtuali comunicate hello tooothers relativo la maggior parte delle e se il traffico tooa macchina virtuale specifica viene consentito o negato.

![flussi per scheda di rete][8]

Hello seguente grafico rotellina ad anello mostri una suddivisione di flussi dalla porta di destinazione. Con queste informazioni, è possibile visualizzare le porte di destinazione hello usato più comunemente utilizzate all'interno di hello specificato periodo.

![grafico ad anello][9]

Hello seguente grafico a barre mostra hello flusso dal gruppo e regola. Con queste informazioni, è possibile vedere hello NSGs responsabile hello la maggior parte del traffico e suddivisione hello del traffico in un gruppo dalla regola.

![grafico a barre][10]
 
Hello seguenti grafici informativo visualizzato informazioni sulla NSGs hello presenti nei registri hello, hello numero di flussi acquisite nel periodo di hello e data hello del log primo di hello acquisiti. Queste informazioni consentono un'idea dei quali NSGs vengono registrate e hello intervallo di date di flussi.

![grafico informativo 1][11]

![grafico informativo 2][12]

Questo modello include hello tooallow i filtri dei dati in seguito si tooview solo hello i dati è interessati. È possibile applicare filtri ai gruppi di risorse, ai gruppi di sicurezza di rete e alle regole. È anche possibile filtrare informazioni 5 tuple, delle decisioni e ora di hello log hello è stato scritto.

![filtri dei dati][13]

## <a name="conclusion"></a>Conclusioni

Abbiamo anche mostrato in questo scenario che utilizzando i registri di gruppo di sicurezza di rete flusso forniti da Watcher di rete e di Power BI, è sono in grado di toovisualize e comprendere il traffico di hello. Power BI usando il modello di hello fornito, il download dei log hello direttamente dall'archivio e li elabora in locale. Modello di tempo impiegato tooload hello varia a seconda numero hello di file richiesti e le dimensioni totali dei file scaricati.

È gratuito toocustomize questo modello per le proprie esigenze. Power BI e i log dei flussi dei gruppi di sicurezza di rete possono essere usati in molti modi diversi. 

## <a name="notes"></a>Note

* Per impostazione predefinita, i log vengono archiviati in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`

    * Se esistono altri dati in un'altra directory sono hello toopull query e dati hello processo devono essere modificati.

* modello Hello fornito non è consigliabile usare con più di 1 GB di log.

* In presenza di una grande quantità di log, è consigliabile prendere in considerazione una soluzione con un altro archivio dati, come Data Lake o SQL Server.

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come toovisualize il flusso di gruppo Registra con hello Elastick Stack visitando [visualizzare tooand di modelli di traffico di rete dalle macchine virtuali utilizzando strumenti open source](network-watcher-using-open-source-tools.md)

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png
