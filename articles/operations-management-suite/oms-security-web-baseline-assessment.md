---
title: Valutazione della linea di base in Operations Management Suite di protezione e controllo soluzione Baseline aaaWeb | Documenti Microsoft
description: "Questo documento illustra come toouse web la valutazione della linea di base in OMS Security and Audit tooperform soluzione una valutazione della linea di base di tutti i server web monitorati a scopo di conformità e sicurezza."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: dafa9d3d93fae31748306b60ee40b285dd59c802
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Valutazione baseline Web nella soluzione Sicurezza e controllo di Operations Management Suite
Questo documento consente di utilizzare la sicurezza di OMS e controllo web linea di base valutazione funzionalità tooaccess hello stato sicuro le risorse monitorati.

## <a name="what-is-web-baseline-assessment"></a>Informazioni sulla valutazione baseline Web
OMS Security offre attualmente la possibilità di eseguire una valutazione baseline della sicurezza dei sistemi operativi. Analizza le impostazioni del sistema operativo hello dei server ogni 24 ore e fornisce una visualizzazione a impostazioni potenzialmente vulnerabile. Per altre informazioni sull'argomento, vedere [Valutazione baseline nella soluzione Sicurezza e controllo di Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/oms-security-baseline).

obiettivo di Hello di valutazione di riferimento Web hello è toofind impostazioni del server web potenzialmente vulnerabile. Hello tre origini primarie per le configurazioni di base di hello web sono: configurazione di IIS, ASP.NET e .NET.  Solo come hello valutazione della linea di base di sistema operativo, sicurezza OMS verrà tooscan il server web ogni 24 ore e forniscono una visualizzazione in stato di sicurezza di essi.  In Internet Information Service (IIS), le configurazioni sono altamente personalizzabili, che consente di vari toobe livelli di applicazione e del sito sottoposto a override. scanner Hello controlla le impostazioni di hello a ogni livello di applicazione/sito di livello radice di addizione toohello predefinito. Ciò consente di impostazioni potenzialmente vulnerabile tooidentify e correggere rapidamente, insieme a questi consigli per tali impostazioni.

>[!NOTE] 
>È possibile scaricare gli identificatori di configurazione comuni hello e regole di linea di base utilizzate dalla sicurezza OMS in questo [pagina](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335?redir=0).


## <a name="web-security-baseline-assessment"></a>Valutazione baseline della sicurezza Web

Per questa versione di anteprima funzionalità hello sono accessibili tramite l'opzione di ricerca di OMS, hello e hello OMS sicurezza e controllo Dashboard. Seguire i passaggi di hello di sotto di tooperform hello attualmente utilizzato riferimento ad:

1. In hello **Microsoft Operations Management Suite** dashboard principale, fare clic su **Security and Audit** riquadro.
2. In hello **Security and Audit** dashboard, è possibile visualizzare hello linea di base Web prospettiva Avanti toohello del sistema operativo base prospettiva.
   
    ![Valutazione baseline della sicurezza Web di Sicurezza e controllo di OMS](./media/oms-security-web-baseline/oms-security-web-baseline-fig5.png)

3. riquadro di sinistra Hello Mostra il numero di hello del server Web rispetto toohello linea di base, hello percentuale media di regole che è passato in tutti i server hello valutata ed elenco hello del server che sono stati valutati.
4. Hello destra riquadro Elenca hello univoco delle regole non riuscita da *gravità*, e *RuleType*. Facendo clic su una delle regole di hello riquadro destro per visualizzare i dettagli di hello di tale regola. Viene illustrato un esempio in hello sotto l'immagine. regola di Hello che viene valutata è elencato in *impostazione delle regole*. Hello *AzId* campo che è un identificatore univoco per ogni regola utilizzata da Microsoft per tenere traccia delle regole di base hello. Inoltre gli utenti toothat possono visualizzare hello *risultato previsto* (valore consigliata da Microsoft), e altri dettagli relativo impatto sulla protezione hello della regola hello.
    
    ![Query](./media/oms-security-web-baseline/oms-security-web-baseline-fig6.png)

5. È possibile creare query personalizzate risultati hello tooreview. 

Hello prima query che è possibile utilizzare è hello **riepilogo di valutazione della linea di base Web**. In hello **Cerca qui** , digitare la query: *tipo = SecurityBaselineSummary BaselineType = Web*. di seguito Hello è un esempio di output:

![Risultato della query](./media/oms-security-web-baseline/oms-security-web-baseline-fig7.png)

>[!NOTE] 
>In questa query ogni record indica il riepilogo della valutazione in un singolo server.

Una volta nel hello **Log Search**, è possibile digitare ulteriori informazioni sulla valutazione della linea di base web hello tooobtain query diverse. Inoltre toohello query precedente, è possibile inoltre utilizzare hello dopo quelli appartenenti a questa versione di anteprima:

**Web Baseline Rule Assessment** (Valutazione regola baseline Web): ogni record rappresenta una singola valutazione della regola baseline Web in un server singolo. Include tutti i dati per una regola non riuscita, hello *SitePath* su quali hello regola è stata valutata, hello *risultato previsto*, hello e *risultato effettivo*.

Query: *Type=SecurityBaseline BaselineType=Web AnalyzeResult=Failed*

![Risultato della query 2](./media/oms-security-web-baseline/oms-security-web-baseline-fig8.png)

**Mostra tutti i risultati per un server specifico**: questa query Mostra la vista dei risultati toosee di un server specifico: Query: *tipo = SecurityBaseline BaselineType = Computer Web = BaselineTestVM1*

![Risultato della query 3](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

È possibile utilizzare questi toocreate record/query dashboard, report o avvisi. Di seguito è riportato un esempio di controllo dell'interfaccia utente che è possibile aggiungere tooyour dashboard. È possibile ottenere informazioni come toovisualize i dati mediante Progettazione vista OMS [qui](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/). schermata di Hello riportata di seguito è riportato un esempio di come hello affiancato avrà un aspetto simile dopo aver effettuato la personalizzazione.

![dashboard](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

## <a name="see-also"></a>Vedere anche
In questo documento sono state fornite informazioni sulla valutazione baseline Web di Sicurezza e controllo di OMS. toolearn più sulla sicurezza di OMS, vedere hello seguenti articoli:

* [Panoramica di Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Monitoraggio e risposta tooSecurity avvisi nella soluzione di controllo e protezione di Operations Management Suite](oms-security-responding-alerts.md)
* [Monitoraggio delle risorse nella soluzione Operations Management Suite per la sicurezza e il controllo](oms-security-monitoring-resources.md)

