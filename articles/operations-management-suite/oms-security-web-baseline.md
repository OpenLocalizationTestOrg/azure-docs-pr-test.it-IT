---
title: aaaOperations gestione gruppo di sicurezza e controllo soluzione Web Baseline | Documenti Microsoft
description: "Questo documento viene illustrato come toouse OMS Security and Audit soluzione tooperform una valutazione della linea di base di web di tutti i server web monitorati a scopo di conformità e sicurezza."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ROBOTS: NOINDEX
redirect_url: https://www.microsoft.com/cloud-platform/security-and-compliance
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: 8aa87fa404ff97ab549dda3f9bebb75766055963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Valutazione baseline Web nella soluzione Sicurezza e controllo di Operations Management Suite
Questo documento consente di toouse [soluzione di controllo e protezione di Operations Management Suite (OMS)](operations-management-suite-overview.md) web valutazione della linea di base tooaccess funzionalità hello stato sicuro le risorse monitorati.

## <a name="what-is-web-baseline-assessment"></a>Informazioni sulla valutazione baseline Web
OMS Security offre attualmente la possibilità di eseguire una valutazione baseline della sicurezza dei sistemi operativi. Analizza impostazioni del sistema operativo dei server hello ogni 24 ore e fornisce una visualizzazione a impostazioni potenzialmente vulnerabile. Per altre informazioni sull'argomento, vedere [Valutazione baseline nella soluzione Sicurezza e controllo di Operations Management Suite](oms-security-baseline.md).

obiettivo di Hello di valutazione di riferimento web hello è toofind impostazioni del server web potenzialmente vulnerabile. Hello tre origini primarie per le configurazioni di base di hello web sono: configurazione di IIS, ASP.NET e .NET.  Solo come hello valutazione della linea di base di sistema operativo, sicurezza OMS verrà tooscan il server web ogni 24 ore e forniscono una visualizzazione in stato di sicurezza di essi.  In Internet Information Service (IIS), le configurazioni sono altamente personalizzabili, che consente di vari toobe livelli di applicazione e del sito sottoposto a override. scanner Hello controlla le impostazioni di hello a ogni livello di applicazione/sito di livello radice di addizione toohello predefinito. Ciò consente di posizione delle impostazioni di vulnerabilità potenziale tooidentify e correggere rapidamente.


## <a name="web-security-baseline-assessment"></a>Valutazione baseline della sicurezza Web
Per questa versione di anteprima questa funzionalità è in corso toobe accedere utilizzando l'opzione di ricerca OMS hello. Seguire i passaggi di hello di sotto di tooperform hello attualmente utilizzato riferimento ad:

1. In hello **Microsoft Operations Management Suite** fare clic su dashboard principale **Security and Audit** riquadro.
2. In hello **Security and Audit** dashboard, fare clic su **ricerca nei Log** pulsante.
3. Hello prima query che è possibile utilizzare è hello **riepilogo di valutazione della linea di base Web**. In hello **Cerca qui** , digitare la query: tipo*= SecurityBaselineSummary BaselineType = web*. Hello schermata seguente è un esempio di output:

![Riepilogo valutazione baseline Web](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> In questa query ogni record indica il riepilogo della valutazione in un singolo server.

Una volta nel hello **Log Search**, è possibile digitare ulteriori informazioni sulla valutazione della linea di base web hello tooobtain query diverse. Inoltre toohello query precedente, è possibile inoltre utilizzare hello dopo quelli appartenenti a questa versione di anteprima.

**Web Baseline Rule Assessment** (Valutazione regola baseline Web): ogni record rappresenta una singola valutazione della regola baseline Web in un server singolo. Include tutti i dati per regola hello, percorso, il risultato previsto hello e risultato effettivo hello.

**Query**: Type*=SecurityBaseline BaselineType=web*

![Valutazione regola baseline Web](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

**Mostra tutti i risultati per un server specifico**: questa query Mostra la vista dei risultati toosee di un server specifico.

**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*

![Tutti i risultati](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

Inoltre, è possibile utilizzare questi toocreate record/query dashboard, report o avvisi. schermata di Hello riportata di seguito è un esempio di controllo dell'interfaccia utente che è possibile aggiungere tooyour dashboard. È possibile ottenere informazioni come toovisualize i dati mediante Progettazione vista OMS [qui](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/). schermata di Hello riportata di seguito è riportato un esempio di come hello affiancato avrà un aspetto simile dopo aver effettuato la personalizzazione.

![Interfaccia utente di esempio](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> Se si desidera che le impostazioni di hello tooknow selezionati per la valutazione della linea di base hello, è possibile scaricare [questo foglio di calcolo di Excel](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) che contiene queste impostazioni.

## <a name="see-also"></a>Vedere anche
In questo documento sono state fornite informazioni sulla valutazione baseline Web di Sicurezza e controllo di OMS. toolearn più sulla sicurezza di OMS, vedere hello seguenti articoli:

* [Panoramica di Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Monitoraggio e risposta tooSecurity avvisi nella soluzione di controllo e protezione di Operations Management Suite](oms-security-responding-alerts.md)
* [Monitoraggio delle risorse nella soluzione Operations Management Suite per la sicurezza e il controllo](oms-security-monitoring-resources.md)

