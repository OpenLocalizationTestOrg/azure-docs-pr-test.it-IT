---
title: Profili di gestione traffico aaaNested | Documenti Microsoft
description: "In questo articolo vengono illustrate funzionalità 'Profili nidificati' hello di Traffic Manager di Azure"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f1b112c4-a3b1-496e-90eb-41e235a49609
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: e476d58a82ed94d12731156280c9665f980de0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="nested-traffic-manager-profiles"></a>Profili nidificati di Gestione traffico

Traffic Manager include una gamma di metodi di routing del traffico che consentono di toocontrol come gestione traffico sceglie quale endpoint deve ricevere il traffico da ogni utente finale. Per altre informazioni, vedere [Metodi di routing del traffico di Gestione traffico](traffic-manager-routing-methods.md).

Ciascun profilo di Gestione traffico specifica un solo metodo di routing del traffico. Esistono tuttavia scenari che richiedono più sofisticato il routing del traffico di routing hello fornito da un unico profilo di Traffic Manager. È possibile nidificare i vantaggi di gestione traffico profili toocombine hello di più di un metodo di routing del traffico. Profili nidificati consentono toooverride hello predefinito Traffic Manager comportamento toosupport maggiori e le distribuzioni di applicazioni più complesse.

Hello seguenti esempi illustrano come toouse annidati i profili di Traffic Manager in vari scenari.

## <a name="example-1-combining-performance-and-weighted-traffic-routing"></a>Esempio 1: Combinazione di metodi di routing del traffico "Prestazioni" e "Ponderato"

Si supponga che un'applicazione hello seguenti aree di Azure è stato distribuito: Stati Uniti occidentali, Europa occidentale e dell'Asia orientale. È usare di gestione traffico 'Prestazioni' routing del traffico metodo toodistribute traffico toohello area più vicina toohello utente.

![Profilo singolo di Gestione traffico][4]

A questo punto, si supponga che si desidera un servizio di aggiornamento tooyour tootest prima di distribuirlo più ampiamente. Si desidera toouse hello 'ponderata' routing del traffico metodo toodirect una piccola percentuale di traffico tooyour della distribuzione di test. Impostare la distribuzione dei test hello insieme distribuzione di produzione esistente hello in Europa occidentale.

Con un singolo profilo non è possibile combinare i metodi di routing del traffico "Ponderato" e "Prestazioni". toosupport questo scenario, si crea un profilo di Traffic Manager utilizzando gli endpoint Europa occidentale hello due e il metodo di routing del traffico "Weighted" hello. Aggiungere quindi questo profilo 'child' come profilo padre' endpoint toohello'. il profilo padre Hello utilizza ancora hello metodo di routing del traffico di prestazioni e contiene hello altre distribuzioni globale come endpoint.

Hello seguente diagramma vengono illustrate in questo esempio:

![Profili nidificati di Gestione traffico][2]

In questa configurazione, il traffico diretto tramite profilo padre hello distribuisce il traffico tra le aree normalmente. Europa occidentale, all'interno di hello profilo annidato distribuisce il traffico toohello produzione endpoint e di test in base a un peso toohello.

Quando il profilo di padre hello Usa metodo di routing del traffico "Prestazioni" hello, ogni endpoint deve essere assegnato a un percorso. percorso Hello viene assegnato quando si configura hello endpoint. Scegliere la distribuzione tooyour di hello regione di Azure più vicina. Hello aree di Azure sono valori di percorso hello è supportati dalla tabella di latenza Internet hello. Per altre informazioni, vedere [Metodo di routing del traffico Prestazioni](traffic-manager-routing-methods.md#performance).

## <a name="example-2-endpoint-monitoring-in-nested-profiles"></a>Esempio 2: Monitoraggio degli endpoint nei profili nidificati

Gestione traffico monitora attivamente integrità hello di ogni endpoint del servizio. Se un endpoint non è integro, gestione traffico indirizza gli utenti tooalternative endpoint toopreserve hello disponibilità del servizio. Questo comportamento dell'endpoint di monitoraggio e il failover si applica tooall metodi di routing del traffico. Per altre informazioni, vedere [Informazioni sul monitoraggio di Gestione traffico](traffic-manager-monitoring.md). Il monitoraggio degli endpoint è differente nei profili annidati. Con i profili nidificati, profilo padre hello non esegue controlli di integrità sul figlio hello direttamente. Integrità hello degli endpoint del profilo figlio hello è invece utilizzato toocalculate hello integrità complessiva del profilo figlio hello. Informazioni sull'integrità viene propagate gerarchia profilo hello annidato. Hello profilo padre Usa questo toodetermine di integrità aggregato se il profilo toodirect traffico toohello figlio. Vedere hello [domande frequenti su](traffic-manager-FAQs.md#traffic-manager-nested-profiles) per informazioni dettagliate sul monitoraggio dello stato di profili nidificati.

Restituzione di toohello di esempio precedente, si supponga che si verifica un errore di distribuzione di produzione hello in Europa occidentale. Per impostazione predefinita, il profilo di 'child' hello indirizza tutte le distribuzioni di test toohello traffico. Se anche la distribuzione dei test di hello non riesce, profilo padre hello determina che il traffico non dovrebbe essere visualizzato in profilo figlio hello poiché tutti gli endpoint figlio non sono integri. Quindi, profilo padre hello distribuisce il traffico toohello altre aree.

![Failover dei profili nidificati (comportamento predefinito)][3]

È possibile che questa soluzione risulti soddisfacente, O potrebbe essere interessata che tutto il traffico di Europa occidentale verrà ora la distribuzione dei test toohello anziché il traffico di un sottoinsieme limitato. Indipendentemente dall'integrità hello di hello distribuzione di test, si desidera toofail sulla toohello altre aree quando si verifica un errore di distribuzione di produzione hello in Europa occidentale. tooenable questo failover, è possibile specificare il parametro 'MinChildEndpoints' hello durante la configurazione del profilo figlio hello come un endpoint nel profilo padre hello. il parametro Hello determina numero minimo di hello di endpoint disponibili nel profilo figlio hello. valore predefinito di Hello è '1'. Per questo scenario è impostare hello MinChildEndpoints valore too2. Sotto questa soglia, profilo padre hello considera hello figlio intero profilo toobe disponibile e indirizza il traffico toohello altri endpoint.

Hello figura seguente viene illustrata questa configurazione:

![Failover dei profili annidati con 'MinChildEndpoints' = 2][4]

> [!NOTE]
> il metodo di routing del traffico "Priority" Hello distribuisce tutti singolo endpoint tooa traffico. In questo caso è quindi inutile impostare MinChildEndpoints su un valore diverso da 1 per il profilo figlio.

## <a name="example-3-prioritized-failover-regions-in-performance-traffic-routing"></a>Esempio 3: Aree di failover con priorità con metodo di routing del traffico "Prestazioni"

comportamento predefinito di Hello per il metodo di routing del traffico "Prestazioni" hello è progettato tooavoid eccessivo caricamento accanto hello più vicino di endpoint e causando una serie di propagazione degli errori. Quando un endpoint non riesce, tutto il traffico che sarebbe stato indirizzato toothat endpoint è uniformemente distribuite toohello altri endpoint di tutte le aree.

![Routing del traffico "Prestazioni" con failover predefinito][5]

Tuttavia, si supponga che si preferisce hello Europa occidentale traffico failover tooWest US e diretta aree tooother traffico quando entrambi gli endpoint non sono disponibili. È possibile creare questa soluzione con un profilo per bambini hello il metodo di routing del traffico 'Priority'.

![Routing del traffico "Prestazioni" con failover preferenziale][6]

Poiché endpoint Europa occidentale hello ha priorità maggiore rispetto a endpoint di Stati Uniti occidentali hello, tutto il traffico viene inviato endpoint Europa occidentale toohello quando entrambi gli endpoint sono in linea. Se ha esito negativo Europa occidentale, il traffico è indirizzato tooWest Stati Uniti. Profilo hello annidato, il traffico è diretto tooEast Asia solo quando sia Europa occidentale e Stati Uniti occidentali esito negativo.

È possibile ripetere questo modello per tutte le aree, Sostituire tutti e tre gli endpoint nel profilo padre hello con tre profili figlio, ognuno dei quali fornisce una sequenza in ordine di priorità di failover.

## <a name="example-4-controlling-performance-traffic-routing-between-multiple-endpoints-in-hello-same-region"></a>Esempio 4: Controllare il traffico di 'Prestazioni' routing tra più endpoint in hello stessa area geografica

Si supponga che hello 'Prestazioni' viene utilizzato il metodo di routing del traffico in un profilo che ha più di un endpoint in una determinata area. Per impostazione predefinita, il traffico diretto toothat area viene distribuito equamente tra tutti gli endpoint disponibili in tale area.

![Routing del traffico "Prestazioni" con distribuzione del traffico nell'area (comportamento predefinito)][7]

Anziché aggiungere più endpoint in Europa occidentale, gli endpoint possono essere inclusi in un profilo figlio separato profilo figlio Hello viene aggiunto toohello padre come endpoint solo di hello in Europa occidentale. le impostazioni di Hello nel profilo figlio hello possono controllare la distribuzione del traffico hello con Europa occidentale, consentendo il routing del traffico basato sulla priorità o ponderati definito all'interno di tale area.

![Routing del traffico "Prestazioni" con distribuzione personalizzata del traffico nell'area][8]

## <a name="example-5-per-endpoint-monitoring-settings"></a>Esempio 5: Impostazioni di monitoraggio per ogni endpoint

Si supponga che si utilizza Traffic Manager toosmoothly migrate traffico da una locale legacy sito web tooa nuovo basato su Cloud versione ospitato in Azure. Per sito legacy hello, si desidera l'integrità del sito di toouse hello homepage URI toomonitor. Ma per hello nuova basato su Cloud versione, si implementa una pagina di monitoraggio personalizzata (percorso ' / monitor.aspx') che include controlli aggiuntivi.

![Monitoraggio degli endpoint di Gestione traffico (comportamento predefinito)][9]

le impostazioni di monitoraggio Hello in un profilo di gestione traffico applicano tooall endpoint all'interno di un unico profilo. Con i profili nidificati, si utilizza un profilo figlio diverso per ogni sito toodefine diverse impostazioni di monitoraggio.

![Monitoraggio degli endpoint di Gestione traffico con impostazioni per ogni endpoint][10]

## <a name="next-steps"></a>Passaggi successivi

Altre informazioni sui [profili di Gestione traffico](traffic-manager-overview.md)

Informazioni su come troppo[creare un profilo di Traffic Manager](traffic-manager-create-profile.md)

<!--Image references-->
[1]: ./media/traffic-manager-nested-profiles/figure-1.png
[2]: ./media/traffic-manager-nested-profiles/figure-2.png
[3]: ./media/traffic-manager-nested-profiles/figure-3.png
[4]: ./media/traffic-manager-nested-profiles/figure-4.png
[5]: ./media/traffic-manager-nested-profiles/figure-5.png
[6]: ./media/traffic-manager-nested-profiles/figure-6.png
[7]: ./media/traffic-manager-nested-profiles/figure-7.png
[8]: ./media/traffic-manager-nested-profiles/figure-8.png
[9]: ./media/traffic-manager-nested-profiles/figure-9.png
[10]: ./media/traffic-manager-nested-profiles/figure-10.png
