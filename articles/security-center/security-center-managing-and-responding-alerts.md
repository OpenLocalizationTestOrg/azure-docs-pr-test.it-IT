---
title: avvisi di sicurezza aaaManage nel Centro protezione di Azure | Documenti Microsoft
description: "Questo documento consente si toouse Centro sicurezza di Azure funzionalità toomanage e risposta toosecurity avvisi."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: f1cb7e4770776827b75ed15893914678c1f44216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-and-responding-toosecurity-alerts-in-azure-security-center"></a>La gestione e risponde avvisi toosecurity nel Centro protezione di Azure
Questo documento consente di utilizzare toomanage Centro sicurezza di Azure e rispondere toosecurity avvisi.

> [!NOTE]
> rilevamenti tooenable avanzate, aggiornamento tooAzure Security Center Standard. È disponibile una versione di valutazione gratuita di 60 giorni. tooupgrade, tariffario selezionare in hello [criteri di sicurezza](security-center-policies.md). Vedere [Centro sicurezza di Azure prezzi](security-center-pricing.md) toolearn altre.
>
>

## <a name="what-are-security-alerts"></a>Informazioni sugli avvisi di sicurezza
Centro sicurezza PC automaticamente raccoglie, analizza, integra i dati del log dalle risorse di Azure, rete hello e soluzioni partner, ad esempio soluzioni di protezione firewall ed endpoint, minacce reali toodetect connesse e ridurre i falsi positivi. Viene visualizzato un elenco di avvisi di sicurezza in ordine di priorità del Centro sicurezza PC insieme hello informazioni necessarie tooquickly analizzare problema hello e indicazioni sul tooremediate un attacco.


> [!NOTE]
> Per altre informazioni sulle funzionalità di rilevamento del Centro sicurezza, vedere [Funzionalità di rilevamento del Centro sicurezza di Azure](security-center-detection-capabilities.md).
>
>

## <a name="managing-security-alerts"></a>Gestire gli avvisi di sicurezza
È possibile esaminare gli avvisi correnti esaminando hello **degli avvisi di sicurezza** riquadro. Aprire il portale di Azure e seguire i passaggi di hello sotto toosee ulteriori dettagli su ogni avviso:

1. Nel dashboard del Centro sicurezza PC hello, verrà visualizzato hello **degli avvisi di sicurezza** riquadro.

    ![Riquadro Avvisi di sicurezza nel Centro sicurezza di Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. Fare clic su hello di hello riquadro tooopen **degli avvisi di sicurezza** pannello che contiene ulteriori dettagli sulle hello gli avvisi come mostrato di seguito.

   ![Pannello di avvisi di sicurezza Hello in Centro sicurezza PC](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

Nella parte inferiore di hello di questo pannello sono dettagli hello per ogni avviso. toosort, fare clic sulla colonna hello che si desidera toosort da. definizione di Hello per ogni colonna è indicato di seguito:

* **Descrizione**: una breve descrizione dell'avviso hello.
* **Conteggio**: elenco di tutti gli avvisi di questo tipo rilevati in un giorno specifico.
* **Viene rilevata da**: hello servizio che è responsabile per l'attivazione dell'avviso hello.
* **Data**: hello data che l'evento hello si è verificato.
* **Stato**: hello stato corrente per tale avviso. Esistono due tipi di stato:
  * **Attiva**: avviso di sicurezza hello è stata rilevata.
* **Gravità**: livello di gravità hello, che può essere alta, Media o bassa.

### <a name="filtering-alerts"></a>Filtro degli avvisi
È possibile filtrare gli avvisi in base a data, stato e gravità. Filtraggio degli avvisi può essere utile per scenari in cui è necessario ambito hello toonarrow di visualizzare gli avvisi di sicurezza. Ad esempio, si potrebbe si desidera che gli avvisi di sicurezza tooaddress che si è verificato in hello ultime 24 ore perché si sta analizzando una potenziale violazione nel sistema hello.

1. Fare clic su **filtro** su hello **degli avvisi di sicurezza** blade. Hello **filtro** pannello apre e si selezionano i valori di data, stato e gravità hello desiderato toosee.

    ![Filtro degli avvisi nel Centro sicurezza](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-toosecurity-alerts"></a>Rispondere toosecurity avvisi
Selezionare un toolearn avviso di sicurezza ulteriori informazioni su eventi hello che ha attivato avviso hello e cosa, se presente, i passaggi necessari per necessario tootake tooremediate un attacco. Gli avvisi di sicurezza sono raggruppati per tipo e data. Fare clic su un avviso di sicurezza verrà aperto un pannello contenente un elenco di avvisi hello raggruppato.

![Rispondere avvisi toosecurity nel Centro protezione di Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

In questo caso, sono stati generati gli avvisi hello consultare toosuspicious attività Remote Desktop Protocol (RDP). Hello prima colonna indica quali risorse sono state attaccate; in secondo luogo, Hello Mostra quante volte è stata attaccata risorse hello; Hello terzo Mostra ora hello dell'attacco hello. Hello quarto Mostra lo stato di avviso hello. e hello Mostra quinto gravità hello di attacco hello. Dopo aver esaminato queste informazioni, fare clic sulla risorsa hello che è stato attaccato e verrà aperto un nuovo pannello.

![Suggerimenti per la quale toodo sulla sicurezza gli avvisi in Centro sicurezza di Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

In hello **descrizione** campo di questo pannello sono disponibili ulteriori dettagli sull'evento. Tali dettagli supplementari offrono approfondite quali hello attivata sicurezza avviso, hello risorsa di destinazione, quando applicabile hello origine indirizzo IP e indicazioni su come tooremediate.  In alcuni casi, indirizzo IP di origine hello verrà essere svuotata (non disponibile) perché non tutti i registri di eventi di sicurezza di Windows includono l'indirizzo IP hello.

monitoraggio e aggiornamento Hello suggerita dal centro di sicurezza variano secondo avviso di sicurezza toohello. In alcuni casi, potrebbe essere toouse tooimplement altre funzionalità di Azure hello consigliato di monitoraggio e aggiornamento. Ad esempio, hello correzione per questo tipo di attacco è l'indirizzo IP di hello tooblacklist che genera questo attacco tramite un [ACL di rete](../virtual-network/virtual-networks-acl.md) o [il gruppo di sicurezza di rete](../virtual-network/virtual-networks-nsg.md) regola.

> [!NOTE]
> Per altre informazioni sui diversi tipi di hello degli avvisi, vedere [degli avvisi di sicurezza dal tipo nel Centro protezione Azure](security-center-alerts-type.md).
>
>

## <a name="see-also"></a>Vedere anche
In questo documento, si è appreso come criteri di sicurezza tooconfigure in Centro sicurezza PC. toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [Gestione degli eventi imprevisti della sicurezza nel Centro sicurezza di Azure](security-center-incident.md)
* [Funzionalità di rilevamento del Centro sicurezza di Azure](security-center-detection-capabilities.md)
* [Guida alla pianificazione e alla gestione del Centro sicurezza di Azure](security-center-planning-and-operations-guide.md)
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure.
