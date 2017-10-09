---
title: Guida introduttiva rapida Centro sicurezza PC aaaAzure | Documenti Microsoft
description: "In questo articolo consente di iniziare rapidamente con Centro sicurezza di Azure mediante portata hello monitoraggio e criteri di Gestione componenti di protezione e il collegamento è toonext passaggi."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 61e95a87-39c5-48f5-aee6-6f90ddcd336e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 23b2444ba1ba30d0a1bd1a1afbc4fd0abfd0827c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-quick-start-guide"></a>Guida introduttiva per il Centro sicurezza di Azure
In questo articolo consente di iniziare rapidamente con Centro sicurezza di Azure mostrando hello sicurezza monitoraggio e criteri di Gestione componenti del Centro sicurezza PC.

> [!NOTE]
> A partire da anticipata giugno 2017, centro di sicurezza verrà utilizzata toocollect Microsoft Monitoring Agent hello e archiviare i dati. Vedere [migrazione della piattaforma Azure sicurezza Center](security-center-platform-migration.md) toolearn altre. informazioni di Hello in questo articolo rappresentano funzionalità Centro sicurezza dopo la transizione toohello Microsoft Monitoring Agent.
>
>

## <a name="prerequisites"></a>Prerequisiti
tooget avviato con il Centro sicurezza PC, è necessario disporre di un tooMicrosoft sottoscrizione Azure. Se non si ha una sottoscrizione, è possibile ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).

livello gratuito di Hello del Centro sicurezza PC viene abilitata automaticamente con la sottoscrizione e offre una visibilità in stato di sicurezza hello delle risorse di Azure. Offre la gestione di criteri di sicurezza di base, raccomandazioni sulla sicurezza e l'integrazione con prodotti e servizi dei partner di Azure.

Tramite il Centro sicurezza PC hello [portale di Azure](https://azure.microsoft.com/features/azure-portal/). toolearn ulteriori informazioni su hello portale di Azure, vedere hello [documentazione portale](https://azure.microsoft.com/documentation/services/azure-portal/).

## <a name="permissions"></a>Autorizzazioni
Centro sicurezza PC, visualizzare solo informazioni correlate tooan risorse di Azure quando si sono ruolo hello del proprietario, collaboratore o lettore per il gruppo hello sottoscrizione o la risorsa a cui appartiene una risorsa. Vedere [autorizzazioni nel Centro protezione Azure](security-center-permissions.md) toolearn informazioni sui ruoli e le operazioni consentite in Centro sicurezza PC.

## <a name="data-collection"></a>Raccolta dei dati
Centro sicurezza PC raccoglie i dati da tooassess le macchine virtuali (VM) lo stato di protezione, fornire consigli sulla sicurezza e ricevere un avviso toothreats. La prima volta che si accede al Centro sicurezza, la raccolta dati viene abilitata in tutte le macchine virtuali della sottoscrizione. Centro sicurezza PC disposizioni hello Microsoft Monitoring Agent esistente tutte supportate macchine virtuali di Azure e quelli nuovi creati. Vedere [Abilita raccolta dati](security-center-enable-data-collection.md) toolearn più sul funzionamento di raccolta dati.

È consigliabile eseguire la raccolta dei dati. Se si utilizza livello gratuito di hello del Centro sicurezza PC, è possibile disabilitare la raccolta dei dati da macchine virtuali disattivando la raccolta dei dati nei criteri di sicurezza hello. Raccolta dati è obbligatorio per le sottoscrizioni nel livello Standard di hello del Centro sicurezza PC. Vedere [Centro sicurezza PC prezzi](security-center-pricing.md) toolearn ulteriori informazioni sugli hello gratuita e livelli di prezzo Standard.

Hello alla procedura seguente viene descritto come tooaccess e utilizzare hello componenti del Centro sicurezza PC. Nei passaggi seguenti verrà illustrato come tooturn la raccolta di dati se si sceglie tooopt out.

> [!NOTE]
> Questo articolo descrive il servizio hello utilizzando un esempio di distribuzione. Non si tratta di una guida dettagliata.
>
>

## <a name="access-security-center"></a>Accedere al Centro sicurezza
Nel portale di hello, seguire questi tooaccess passaggi Centro sicurezza:

1. In hello **Microsoft Azure** dal menu **Centro sicurezza PC**.

   ![Menu di Azure][1]
2. Se si accede a Centro sicurezza PC per hello prima volta, hello **iniziale** apre blade. Selezionare **avvia il Centro sicurezza PC** tooopen hello **Centro sicurezza PC** blade e tooenable la raccolta dei dati.
   ![Schermata iniziale][10]
3. Dopo aver avviare centro di sicurezza dal Pannello di benvenuto hello o selezionare il Centro sicurezza PC dal menu di Microsoft Azure hello, hello **Centro sicurezza PC** apre blade. Per un facile accesso toohello **Centro sicurezza PC** pannello in prova futuri, selezionare prova **Pin pannello toodashboard** opzione (alto a destra).
   ![Opzione di toodashboard pannello pin][2]

## <a name="use-security-center"></a>Usare il Centro sicurezza
È possibile configurare criteri di sicurezza per le sottoscrizioni e i gruppi di risorse di Azure. Configurare i criteri di sicurezza per la sottoscrizione:

1. In hello **Centro sicurezza PC** blade, seleziona hello **criteri** riquadro.
2. In hello **criteri di sicurezza - definire criteri per ogni sottoscrizione** pannello, selezionare una sottoscrizione.
3. In hello **criteri di sicurezza** pannello **la raccolta dei dati** tooautomatically abilitato raccolta registri. monitoraggio estensione Hello è disponibile in tutte le macchine virtuali correnti e nuove nella sottoscrizione hello. (Nel livello gratuito di hello del Centro sicurezza PC, è possibile rifiutare esplicitamente la raccolta dei dati impostando **la raccolta dei dati** troppo**Off**. Impostazione **la raccolta dei dati** troppo**Off** impedisce che il Centro sicurezza PC fornendo gli avvisi di sicurezza e suggerimenti.)
4. In hello **criteri di sicurezza** pannello seleziona **criteri di prevenzione**. Verrà visualizzata hello **criteri di prevenzione** blade.
5. In hello **criteri di prevenzione** pannello accendere indicazioni hello che si vuole toosee come parte dei criteri di sicurezza. Esempi:

   * Impostazione **gli aggiornamenti del sistema** troppo**su** analisi tutte le macchine virtuali è supportata per privi di aggiornamenti del sistema operativo.
   * Impostazione **vulnerabilità del sistema operativo** troppo**su** analisi tutte supportate macchine virtuali tooidentify tutte le configurazioni del sistema operativo che potrebbero risultare hello VM tooattack più vulnerabile.

### <a name="view-recommendations"></a>Visualizzare raccomandazioni
1. Restituire toohello **Centro sicurezza PC** pannello e seleziona hello **indicazioni** riquadro. Centro sicurezza PC analizza periodicamente lo stato di sicurezza hello delle risorse di Azure. Quando il Centro sicurezza PC identifica potenziali vulnerabilità di sicurezza, viene visualizzato indicazioni su hello **indicazioni** blade.
   ![Raccomandazioni nel Centro sicurezza di Azure][5]
2. Selezionare una raccomandazione hello **indicazioni** rilasciare più i hello azione tooresolve informazioni e/o tootake tooview blade.

### <a name="view-hello-security-state-of-your-resources"></a>Visualizzare lo stato di sicurezza hello delle risorse
1. Restituire toohello **Centro sicurezza PC** blade. Hello **prevenzione** sezione dashboard hello contiene gli indicatori di stato di sicurezza hello per le macchine virtuali, rete, dati e alle applicazioni.
2. Selezionare **calcolo** tooview ulteriori informazioni. Hello **calcolo** pannello apre con tre schede:

  - **Panoramica**: contiene consigli sul monitoraggio e sulle macchine virtuali.
  - **Macchine virtuali**: elenca tutte le macchine virtuali e il rispettivo stato di sicurezza corrente.
  - **Servizi cloud**: elenca di tutti i ruoli Web e di lavoro monitorati dal Centro sicurezza.

    ![riquadro di stato risorse Hello in Centro sicurezza di Azure][6]

3. In hello **Panoramica** , selezionare un'indicazione in **indicazioni di macchine VIRTUALI** tooview ulteriori informazioni e/o eseguire azioni tooconfigure controlli necessari.
4. In hello **macchine virtuali** , selezionare una VM tooview i dettagli aggiuntivi.

### <a name="view-security-alerts"></a>Visualizzare avvisi di sicurezza
1. Restituire toohello **Centro sicurezza PC** pannello e seleziona hello **degli avvisi di sicurezza** riquadro. Hello **degli avvisi di sicurezza** pannello apre e visualizza un elenco di avvisi. Hello analysis Centro sicurezza di attività di rete e i registri di protezione delle genera gli avvisi. Sono inclusi gli avvisi generati da soluzioni partner integrate.
   ![Avvisi di sicurezza nel Centro sicurezza di Azure][7]

   > [!NOTE]
   > Avvisi di sicurezza sono disponibili solo se è abilitato il livello Standard di hello del Centro sicurezza PC. Una versione di valutazione gratuita di 60 giorni del livello Standard hello è disponibile. Vedere [passaggi successivi](#next-steps) per informazioni su come tooget hello Standard del livello.
   >
   >
2. Selezionare un avviso tooview ulteriori informazioni. In questo esempio verrà selezionato **Modified system binary discovered** (Individuato file binario di sistema modificato). Si aprirà pannelli che forniscono ulteriori dettagli sull'avviso hello.
   ![Dettagli degli avvisi di sicurezza nel Centro sicurezza di Azure][8]

### <a name="view-hello-health-of-your-partner-solutions"></a>Visualizza stato hello partner delle soluzioni dell'utente
1. Restituire toohello **Centro sicurezza PC** blade. Hello **soluzioni Partner** riquadro consente di monitorare, a colpo d'occhio, hello lo stato di integrità delle soluzioni di partner integrato con la sottoscrizione di Azure.
2. Seleziona hello **soluzioni Partner** riquadro. Apre un pannello e visualizza un elenco di partner delle soluzioni dell'utente connesso tooSecurity Center.
   ![soluzioni partner][9]
3. Selezionare una soluzione dei partner. In questo esempio, è possibile selezionare hello **QualysVa1** soluzione.  Un pannello apre e Mostra lo stato di hello della soluzione di partner hello e della soluzione hello le risorse associate. Selezionare **console soluzione** esperienza di gestione dei partner hello tooopen per questa soluzione.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo ha introdotto toohello sicurezza monitoraggio e criteri di Gestione componenti del Centro sicurezza PC. Ora che si ha familiarità con il Centro sicurezza PC, provare a hello alla procedura seguente:

* Configurare i criteri di sicurezza per la sottoscrizione di Azure. vedere, più toolearn [l'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md).
* Usare le raccomandazioni relative hello in toohelp Centro sicurezza PC proteggere le risorse di Azure. vedere, più toolearn [gestione consigli relativi alla sicurezza nel Centro protezione Azure](security-center-recommendations.md).
* Esaminare e gestire gli avvisi di sicurezza correnti. vedere, più toolearn [toosecurity risponda e gestire gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md).
- [Sicurezza dei dati nel Centro sicurezza di Azure](security-center-data-security.md): informazioni sulla gestione e la protezione dei dati nel Centro sicurezza.
* Altre informazioni su hello [advanced threat le funzionalità di rilevazione](security-center-detection-capabilities.md) disponibili hello [livello Standard](security-center-pricing.md) del Centro sicurezza PC. livello Standard Hello viene offerto gratuitamente per hello 60 giorni prima.
* Nel caso di domande sull'utilizzo di centro di sicurezza, vedere hello [domande frequenti su Centro protezione di Azure](security-center-faq.md).

<!--Image references-->
[1]: ./media/security-center-get-started/azure-menu.png
[2]: ./media/security-center-get-started/security-center-pin.png
[3]: ./media/security-center-get-started/security-policy.png
[4]: ./media/security-center-get-started/prevention-policy.png
[5]: ./media/security-center-get-started/recommendations.png
[6]: ./media/security-center-get-started/resources-health.png
[7]: ./media/security-center-get-started/security-alert.png
[8]: ./media/security-center-get-started/security-alert-detail.png
[9]: ./media/security-center-get-started/partner-solutions.png
[10]: ./media/security-center-get-started/welcome.png
