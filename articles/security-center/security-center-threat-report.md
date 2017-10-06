---
title: report sullo stato della minaccia di Centro sicurezza PC aaaAzure | Documenti Microsoft
description: Questo documento consente di toouse Azure sicurezza Center minaccia intelligente rapporti durante un'analisi toofind ulteriori informazioni su un avviso di sicurezza.
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5662e312-e8c2-4736-974e-576eeb333484
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: c888cfac1dd8b057616a6b8e6c6f6b67b552f2e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-threat-intelligence-report"></a>Report di intelligence per le minacce generato dal Centro sicurezza di Azure
Questo documento spiega come i report di intelligence per le minacce del Centro sicurezza di Azure possono essere utili per raccogliere informazioni più dettagliate su una minaccia che ha generato un avviso di sicurezza.

## <a name="what-is-a-threat-intelligence-report"></a>Informazioni sui report di intelligence per le minacce
Rilevamento minacce del Centro sicurezza PC funziona mediante il monitoraggio delle informazioni di protezione delle risorse di Azure, rete hello e soluzioni partner connesso. Viene avviata l'analisi di queste informazioni, correlazione spesso informazioni provenienti da più origini, tooidentify minacce. Questo processo è parte del Centro sicurezza PC hello [funzionalità di rilevamento](security-center-detection-capabilities.md).

Quando il Centro sicurezza identifica una minaccia, attiva un [avviso di sicurezza](security-center-managing-and-responding-alerts.md) contenente informazioni dettagliate su un evento specifico, inclusi i suggerimenti per la correzione. i team di risposta agli eventi imprevisti tooassist ricerca e correzione delle minacce, centro di sicurezza include un report sullo stato della minaccia che contiene informazioni sulla minaccia hello che è stato rilevato che include informazioni quali il:

* Identità o associazioni dell'utente malintenzionato, se queste informazioni sono disponibili
* Obiettivi degli utenti malintenzionati
* Campagne di attacco attuali e cronologiche, se queste informazioni sono disponibili
* Tattiche, strumenti e procedure usate dagli utenti malintenzionati
* Indicatori di compromissione (IoC) associati, ad esempio URL e hash file
* Victimology, ovvero hello e dell'industria, tooassist prevalenza geografica è determinare se le risorse di Azure sono esposti al rischio
* Informazioni sulla mitigazione dei rischi e correzione

> [!NOTE]
> quantità di Hello di informazioni in qualsiasi report particolare saranno diversi. il livello di dettaglio Hello è basato su attività e la prevalenza del malware hello.
>
>

Centro sicurezza PC sono disponibili tre tipi di report di minaccia, che può variare in base toohello attacco. report di Hello disponibili sono:

* **Report sui gruppi di attività**: fornisce approfondimenti sugli utenti malintenzionati e relativi obiettivi e strategie.
* **Report sulle campagne**: si concentra sui dettagli di specifiche campagne di attacco.
* **Report di riepilogo delle minacce**: copre tutti gli elementi hello in due report hello precedente.

Questo tipo di informazioni è molto utile durante hello [risposta agli eventi imprevisti](security-center-incident-response.md) processo in cui è presente un'origine di hello toounderstand analisi in corso di attacco hello, motivazioni dell'utente malintenzionato di hello e cosa toodo toomitigate questo problema in futuro.

## <a name="how-tooaccess-hello-threat-intelligence-report"></a>Come tooaccess hello report sullo stato della minaccia?
È possibile esaminare gli avvisi correnti esaminando hello **degli avvisi di sicurezza** riquadro. Aprire hello portale di Azure e seguire i passaggi di hello sotto toosee ulteriori dettagli su ogni avviso:

1. Nel dashboard del Centro sicurezza PC hello, verrà visualizzato hello **degli avvisi di sicurezza** riquadro.
2. Fare clic su hello di hello riquadro tooopen **degli avvisi di sicurezza** pannello che contiene ulteriori dettagli sugli avvisi di hello e fare clic su nell'avviso di sicurezza hello che si desidera tooobtain ulteriori informazioni su.

    ![Avvisi di sicurezza](./media/security-center-threat-report/security-center-threat-report-fig1.png)
3. In questo caso hello **sospetta processo eseguito** pannello mostra i dettagli di hello hello avviso come illustrato nella figura hello seguente:

    ![Dettagli dell'avviso di sicurezza](./media/security-center-threat-report/security-center-threat-report-fig2.png)
4. quantità di Hello di informazioni disponibili per ogni avviso di sicurezza variano in base toohello tipo di avviso. In hello **report** campo è disponibile un report di business intelligence di collegamento toohello minaccia. Fare clic su di esso; verrà visualizzata un'altra finestra del browser con un file PDF.

   ![Selezione dell'archiviazione](./media/security-center-threat-report/security-center-threat-report-fig3.png)

Da qui è possibile scaricare hello PDF per questo report e ulteriori informazioni sulla sicurezza hello problema di lettura è stato rilevato e intraprendere azioni in base alle informazioni di hello fornite.

## <a name="see-also"></a>Vedere anche
In questo documento è stata evidenziata l'importanza dei report di intelligence per le minacce generati dal Centro sicurezza di Azure nel corso di un'analisi degli avvisi di sicurezza. toolearn ulteriori informazioni su Centro sicurezza di Azure, vedere l'esempio hello:

* [Domande frequenti sul Centro sicurezza di Azure](security-center-faq.md). Trovare le domande frequenti sull'utilizzo del servizio hello.
* [Uso del Centro sicurezza di Azure per rispondere agli eventi imprevisti](security-center-incident-response.md)
* [Funzionalità di rilevamento del Centro sicurezza di Azure](security-center-detection-capabilities.md)
* [Guida alla pianificazione e alla gestione del Centro sicurezza di Azure](security-center-planning-and-operations-guide.md). Informazioni su come tooplan e comprendere considerazioni sulla progettazione hello tooadopt Centro sicurezza di Azure.
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md). Informazioni su come avvisi toosecurity toomanage e rispondere.
* [Gestione degli eventi imprevisti della sicurezza nel Centro sicurezza di Azure](security-center-incident.md)
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/). Post di blog sulla sicurezza e sulla conformità di Azure.
