---
title: avvisi di sicurezza aaaHandling nel Centro protezione di Azure | Documenti Microsoft
description: "Questo documento consente di eventi di sicurezza toohandle funzionalità toouse Centro sicurezza di Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: e8feb669-8f30-49eb-ba38-046edf3f9656
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: edb911c298a2ce93cd0ea5b22ce002005040090f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a>Gestione degli eventi imprevisti della sicurezza nel Centro sicurezza di Azure
Valutazione e analisi degli avvisi di sicurezza può richiedere molto tempo per gli analisti della sicurezza più esperti anche hello e per molti è tooeven rigido sapere dove toobegin. Utilizzando [analitica](security-center-detection-capabilities.md) informazioni hello tooconnect tra distinct [degli avvisi di sicurezza](security-center-managing-and-responding-alerts.md), centro di sicurezza può offrire una visualizzazione singola di una campagna di attacco e tutte di hello correlate avvisi: è possibile Consente di comprendere rapidamente ha richiesto l'autore dell'attacco hello quali azioni e le risorse che sono state interessate.

Questo documento vengono illustrate la modalità sicurezza toouse avviso capacità nel Centro sicurezza PC tooassist gestione degli eventi di sicurezza.

## <a name="what-is-a-security-incident"></a>Che cos'è un evento imprevisto della sicurezza?
Nel Centro sicurezza un evento imprevisto della sicurezza è un'aggregazione di tutti gli avvisi relativi a una risorsa, in linea con i modelli delle [catene di attacco](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) . Eventi imprevisti sono visualizzati in hello [degli avvisi di sicurezza](security-center-managing-and-responding-alerts.md) riquadro e blade. Un evento imprevisto riveleranno hello elenco avvisi correlati, che consente di tooobtain ulteriori informazioni su ogni occorrenza.

## <a name="managing-security-incidents"></a>Gestione degli eventi imprevisti della sicurezza
È possibile esaminare i problemi di protezione corrente controllando riquadro avvisi di sicurezza hello. Accesso hello portale di Azure e seguire passaggi hello sotto toosee ulteriori dettagli su ciascun evento imprevisto di sicurezza:

1. Nel dashboard del Centro sicurezza PC hello, verrà visualizzato hello **degli avvisi di sicurezza** riquadro.

    ![Riquadro Avvisi di sicurezza nel Centro sicurezza di Azure](./media/security-center-incident/security-center-incident-fig1.png)

2. Fare clic su questo tooexpand riquadro e se viene rilevato un problema di sicurezza, verrà visualizzato nel grafico di avvisi di sicurezza di hello come illustrato di seguito:

    ![Evento imprevisto della sicurezza](./media/security-center-incident/security-center-incident-fig2.png)

3. Si noti che Descrizione evento imprevisto di hello sicurezza ha un'icona diversa rispetto a tooother avvisi. Fare clic su di esso tooview ulteriori dettagli sull'evento imprevisto.

    ![Evento imprevisto della sicurezza](./media/security-center-incident/security-center-incident-fig3.png)

4. In hello **incidente** pannello visualizzato più informazioni dettagliate su questo evento imprevisto di sicurezza, che include la descrizione completa, la gravità (che in questo caso è elevata), lo stato corrente (in questo caso è comunque *attivo*, che implica utente hello non è stata eseguita un'azione tooit - questa operazione può essere eseguita facendo clic per l'evento imprevisto di hello in hello **degli avvisi di sicurezza** pannello), hello attaccata di risorse (in questo caso *VM1*), la procedura di correzione per l'evento imprevisto di hello hello e nel riquadro inferiore hello è avvisi hello che sono stati inclusi nell'evento imprevisto. Se si desiderano tooobtain ulteriori informazioni su ogni avviso, fare clic sul insieme a un altro pannello verrà aperta, come illustrato di seguito:

    ![Evento imprevisto della sicurezza](./media/security-center-incident/security-center-incident-fig4.png)

informazioni Hello in questo pannello variano in base toohello avviso. Lettura [toosecurity risponda e gestire gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) per ulteriori informazioni su come toomanage questi avvisi. Alcune considerazioni importanti in merito a questa funzionalità:

* Un nuovo filtro consente di toocustomize che tooincident la visualizzazione, solo gli avvisi solo o entrambi.
* Hello stesso avviso può esistere come parte di un evento imprevisto (se applicabile), nonché toobe visibile come un avviso autonomo.

## <a name="see-also"></a>Vedere anche
In questo documento è stato descritto come toouse hello funzionalità degli eventi imprevisti di protezione del Centro sicurezza PC. toolearn ulteriori informazioni su Centro di sicurezza, vedere l'esempio hello:

* [La gestione e risponde avvisi toosecurity nel Centro protezione di Azure](security-center-managing-and-responding-alerts.md)
* [Funzionalità di rilevamento del Centro sicurezza di Azure](security-center-detection-capabilities.md)
* [Guida alla pianificazione e alla gestione del Centro sicurezza di Azure](security-center-planning-and-operations-guide.md)
* [La gestione e risponde avvisi toosecurity nel Centro protezione di Azure](security-center-managing-and-responding-alerts.md)
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md)-domande frequenti sull'utilizzo di hello servizio di ricerca.
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/): post di blog sulla sicurezza e sulla conformità in Azure.
