---
title: Protezione dei dati di Centro protezione aaaAzure | Documenti Microsoft
description: Questo documento illustra come i dati vengono gestiti e protetti nel Centro sicurezza di Azure.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 33f2c9f4-21aa-4f0c-9e5e-4cd1223e39d7
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: yurid
ms.openlocfilehash: 30f8b11272dc5df6d485608abdaa62ba57e63f23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-data-security"></a>Sicurezza dei dati nel Centro sicurezza di Azure
i clienti toohelp impediranno, rilevano e rispondono toothreats, Centro sicurezza di Azure raccoglie ed elabora i dati relativi alla sicurezza, tra cui informazioni di configurazione, metadati, i registri eventi, i file di dump di arresto anomalo del sistema e altro ancora. Microsoft aderisce toostrict linee guida di conformità e sicurezza, dalla codifica toooperating un servizio.

Questo articolo illustra come i dati vengono gestiti e protetti nel Centro sicurezza di Azure.

>[!NOTE] 
>A partire da anticipata giugno 2017, centro di sicurezza verrà utilizzata toocollect Microsoft Monitoring Agent hello e archiviare i dati. Vedere [migrazione della piattaforma Azure sicurezza Center](security-center-platform-migration.md) toolearn altre. informazioni di Hello in questo articolo rappresentano funzionalità Centro sicurezza dopo la transizione toohello Microsoft Monitoring Agent.
>


## <a name="data-sources"></a>Origini dati
Centro sicurezza di Azure analizza i dati di hello seguente visibilità tooprovide origini nello stato di sicurezza, identificare le vulnerabilità consiglia le misure di attenuazione e rilevare minacce attive.

- Servizi di Azure: Utilizza le informazioni di configurazione hello di servizi di Azure è stata distribuita mediante la comunicazione con il provider di risorse del servizio.
- Traffico di rete: usa i metadati del traffico di rete campionati dall'infrastruttura di Microsoft, ad esempio l'IP/porta di origine/destinazione, le dimensioni del pacchetto e il protocollo di rete.
- Soluzioni partner: usa gli avvisi di sicurezza dalle soluzioni partner integrate, ad esempio firewall e soluzioni antimalware. 
- Macchine virtuali e server: usa informazioni sulla configurazione e sugli eventi di sicurezza, ad esempio log di controllo e log eventi di Windows, log di IIS, messaggi syslog e file di dump di arresto anomalo del sistema dalle macchine virtuali. Inoltre, quando viene creato un avviso, Centro sicurezza di Azure può generare uno snapshot del disco di macchina virtuale hello interessato ed estrarre di avviso toohello correlati elementi di computer dal disco di macchina virtuale hello, ad esempio un file di registro di sistema, per scopi di analisi forense.


## <a name="data-protection"></a>Protezione dati
**La separazione dei dati**: dati vengono mantenuti separati logicamente in ogni componente servizio hello. Tutti i dati vengono contrassegnati in base all'organizzazione. Tale contrassegno persiste per tutto hello del ciclo di vita dei dati e viene applicato a ogni livello del servizio hello.

**Accesso ai dati**: ordine tooprovide consigli sulla sicurezza e provare a potenziali minacce alla sicurezza, personale Microsoft possono accedere alle informazioni raccolte o analizzati da servizi di Azure, inclusi i file di dump di arresto anomalo del sistema, elaborare gli eventi di creazione, macchina virtuale gli snapshot del disco e gli elementi, che possono includere involontariamente i dati dei clienti o dati personali da quelli delle macchine virtuali. È conforme toohello [Microsoft Online Services termini e informativa sulla Privacy](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31), quale stato che Microsoft non utilizza i dati dei clienti o derivare da esso per scopi commerciali pubblicitari o simili. Utilizziamo solo i dati dei clienti come tooprovide necessari con Azure servizi, inclusi motivi compatibile con tali servizi. Mantenere tutti i diritti tooCustomer dati.

**Utilizzo di dati**: Microsoft utilizza i modelli e sulle minacce visualizzata in più tenant tooenhance la funzionalità di rilevamento e prevenzione; avviene in conformità con impegni di privacy hello descritto in questo [sulla Privacy Istruzione](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).

## <a name="data-location"></a>Posizione dei dati

**Le aree di lavoro**: un'area di lavoro è specificato per hello seguente Geos e i dati raccolti da macchine virtuali di Azure, inclusi i dump di arresto anomalo e alcuni tipi di dati di avviso, sono archiviati in hello più prossimo dell'area di lavoro. 

| Area geografica VM                        | Area geografica area di lavoro |
|-------------------------------|---------------|
| Stati Uniti, Brasile, Canada | Stati Uniti |
| Europa, Regno Unito        | Europa        |
| Asia Pacifico, Giappone, India    | Asia/Pacifico  |
| Australia                     | Australia     |

 
Gli snapshot del disco di macchina virtuale sono archiviati nel hello stesso account di archiviazione come disco di macchina virtuale hello.
 
Per le macchine virtuali e i server in esecuzione in altri ambienti, ad esempio, in locale, è possibile specificare dell'area di lavoro hello e area in cui vengono archiviati i dati raccolti. 

**Centro sicurezza di Azure Storage**: informazioni sugli avvisi di sicurezza, inclusi gli avvisi di partner, viene archiviate nella regione in base percorso toohello di hello relative risorse di Azure, mentre le informazioni sullo stato di integrità di protezione e indicazione verrà archiviate centralmente in Italia hello o in base percorso del toocustomer Europa.
Il Centro sicurezza di Azure raccoglie copie temporanee dei file di dump di arresto anomalo del sistema e le analizza per cercare le prove di tentativi di exploit e compromissioni riuscite. Centro sicurezza di Azure esegue l'analisi in hello stessa area geografica come hello dell'area di lavoro e le eliminazioni hello copie temporanee quando l'analisi sono stata completata.

Gli elementi di computer vengono archiviati centralmente in hello stessa area come hello macchina virtuale. 


## <a name="managing-data-collection-from-virtual-machines"></a>Gestione della raccolta dati da macchine virtuali

Quando si abilita il Centro sicurezza in Azure, viene attivata la raccolta dati per ogni sottoscrizione di Azure. È anche possibile attivare la raccolta dei dati per le sottoscrizioni in hello sezione criteri di sicurezza del Centro sicurezza di Azure. Quando è attivata la raccolta dei dati, è supportato Centro sicurezza di Azure esegue il provisioning hello Microsoft Monitoring Agent in tutte le macchine virtuali di Azure e quelli nuovi creati. Microsoft Monitoring agent di Hello esegue l'analisi per la sicurezza varie configurazioni e gli eventi correlati in [Event Tracing for Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) tracce (ETW). Inoltre, sistema operativo hello genererà eventi del registro eventi corso hello dell'esecuzione della macchina hello. Esempi di tali dati sono: tipo e versione del sistema operativo, log del sistema operativo (registri eventi di Windows), processi in esecuzione, nome computer, indirizzi IP, utente connesso e ID tenant. Microsoft Monitoring Agent Hello legge voci del registro eventi e tracce di ETW e li copia tooyour aree di lavoro per l'analisi. Microsoft Monitoring Agent Hello copia workspace tooyour file dump di arresto anomalo del sistema.

Se si utilizza Centro protezione Azure Free, è anche possibile disabilitare la raccolta dei dati da macchine virtuali in hello criteri di sicurezza. Raccolta dati è obbligatorio per le sottoscrizioni nel livello Standard hello. Gli snapshot dei dischi delle VM e la raccolta di elementi resteranno abilitati anche se la raccolta dati è stata disabilitata.


## <a name="see-also"></a>Vedere anche
Questo documento ha illustrato come i dati vengono gestiti e protetti nel Centro sicurezza di Azure. toolearn ulteriori informazioni su Centro sicurezza di Azure, vedere:

* [Centro sicurezza di Azure Guida alla pianificazione e le operazioni](security-center-planning-and-operations-guide.md) , informazioni come tooplan e comprendere considerazioni sulla progettazione hello tooadopt Centro sicurezza di Azure.
* [Il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md) : informazioni su come toomonitor hello integrità delle risorse di Azure
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) , informazioni come avvisi toosecurity toomanage e rispondere
* [Monitoraggio di soluzioni dei partner con Centro sicurezza di Azure](security-center-partner-solutions.md) : informazioni su come toomonitor hello lo stato di integrità delle soluzioni di partner.
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'utilizzo di hello servizio di ricerca
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure
