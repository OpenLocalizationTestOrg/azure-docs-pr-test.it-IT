---
title: le informazioni aaaGet dai dati del Centro sicurezza di Azure con Power BI | Documenti Microsoft
description: "Hello pacchetto di contenuto Centro sicurezza di Azure Power BI rende facile toofind avvisi di sicurezza, indicazioni, attaccata di risorse e indica la tendenza, in base a un set di dati che è stato creato per la creazione di report."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 0ded6bc7-52e8-43b4-8940-0bee137526e3
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: af68aef626034fe03d793c36b515a3f26619e5f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-insights-from-azure-security-center-data-with-power-bi"></a>Ottenere informazioni dettagliate sui dati del Centro sicurezza di Azure con Power BI
Hello [Dashboard di Power BI](http://aka.ms/azure-security-center-power-bi) per Centro sicurezza di Azure consente toovisualize, analizzare e filtrare indicazioni e degli avvisi di sicurezza da qualsiasi posizione, tra cui il dispositivo mobile. Utilizzare le tendenze tooreveal dashboard di Power BI hello e attacchi motivi - vista degli avvisi di sicurezza da risorse o indirizzo IP di origine e giornalismo rischi di sicurezza per risorse o età.

È anche possibile combinare le raccomandazioni del Centro sicurezza con altri dati in modi interessanti, ad esempio usando i dati dei [log di controllo di Azure](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/) e l'[attività di controllo del database SQL di Azure](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/). Entrambi offrono dashboard di Power BI e, è inoltre possibile esportare questo tooExcel dati per la semplice di report sullo stato di sicurezza hello delle risorse cloud.

## <a name="using-azure-security-center-dashboard-tooaccess-power-bi"></a>Utilizzo di Centro protezione Azure dashboard tooaccess Power BI
È inoltre possibile utilizzare report di Power BI tooaccess dashboard hello Centro sicurezza di Azure. Seguire hello passaggi tooperform questa attività:

1. In hello **Centro sicurezza di Azure** dashboard, fare clic su **Power BI** pulsante.

    ![Connettere il Centro sicurezza PC tooAzure tramite Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-1-newUI-2017.png)
2. Hello **Power BI** pannello verrà visualizzata sul lato destro di hello, come illustrato nella seguente schermata hello:

    ![Connettere il Centro sicurezza PC tooAzure tramite Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-new11-2017.png)
3. Se si sta creando il dashboard di Power BI hello hello per la prima volta, è possibile scegliere una delle seguenti hello opzioni nell'hello **Esplora in Power BI** pannello:

   * **Dashboard di sicurezza insights**: scegliere questa opzione se si desidera toocreate un dashboard che include lo stato di protezione, thread e rilevamenti. Questa opzione è più comune per il ruolo DevOps responsabile dell'analisi del relativo stato di sicurezza e degli avvisi rilevati nelle sottoscrizioni.
   * **Dashboard di gestione di criteri**: scegliere questa opzione se si desidera che i criteri di gestione e l'applicazione tooexplore.  Questa opzione è più comune per il reparto IT centrale che è maggiormente focalizzato sulla governance. In conformità di criteri di sicurezza della propria azienda, possono utilizzare questo visibilità toogain dashboard e approfondimenti.
   * Se si dispone già di un dashboard di Power BI, fare clic su **dashboard di Power BI corrente Go tooyour**.
4. Ai fini di questo esempio, fare clic sull'opzione **Dashboard degli approfondimenti sulla sicurezza** . Se si tratta di hello prima volta, si crea un dashboard di Power BI per centro di sicurezza è richiesto tooinstall pacchetto di contenuto hello. Fare clic su **ottenere** pulsante hello **pacchetti di contenuto per Power BI** finestra come mostrato nella seguente schermata hello:

    ![Dashboard degli approfondimenti sulla sicurezza del Centro sicurezza di Azure](./media/security-center-powerbi/security-center-powerbi-fig1-new3.png)
5. Hello **connettersi tooAzure sicurezza Centro protezione Insights** finestra di dialogo. Verificare che hello **autenticazione** metodo **oAuth2** come illustrato di seguito e fare clic su **Accedi** pulsante.

    ![Autenticazione](./media/security-center-powerbi/security-center-powerbi-fig1-new4.png)
6. È possibile che venga richiesto tooauthenticate nuovamente con le credenziali di Azure. Dopo l'autenticazione verrà creato il dashboard. Dopo aver creato il dashboard di hello è visualizzato un rapporto con una struttura analoga hello, come illustrato nella seguente schermata hello:

    ![dashboard di Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-new5.png)

> [!NOTE]
> Un aggiornamento di report hello tootake pianificato è su base giornaliera. Nel caso in cui si verifica un errore in questo aggiornamento, leggere [potenziali problemi di aggiornamento con hello Azure sicurezza Center Power BI](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/), per ulteriori informazioni su come tootroubleshoot.
>
>

Qui è possibile visualizzare hello numerosi avvisi di sicurezza e suggerimenti, nonché il numero di hello di macchine virtuali, database SQL di Azure e risorse di rete monitorate da Centro sicurezza di Azure.

TooAzure un collegamento Centro sicurezza PC reindirizza si toohello portale di Azure. grafici di Hello rendono toovisualize semplice informazioni sulle indicazioni relative alla sicurezza e gli avvisi, inclusi:

* Stato della sicurezza delle risorse
* Raccomandazioni in attesa
* Raccomandazioni per le VM
* Avvisi nel tempo
* Risorse che hanno subito attacchi
* IP utenti malintenzionati

Per ogni grafico sono disponibili informazioni dettagliate aggiuntive. Selezionare un riquadro toosee per ulteriori informazioni. Ad esempio, hello **stato di sicurezza di risorse** riquadro Mostra dettagli aggiuntivi su in sospeso indicazioni dalle risorse come illustrato nella seguente schermata hello:

![Raccomandazioni](./media/security-center-powerbi/security-center-powerbi-fig1-new6.png)

Se si fa clic in qualsiasi riga di questo grafico, hello altri sta toogray out e lo stato attivo si solo su hello che è selezionata. tooreturn toohello dashboard, fare clic su **Centro sicurezza di Azure** in hello **dashboard** opzione hello riquadro a sinistra della pagina.

> [!NOTE]
> Se si desidera toocustomize report aggiungendo altri campi o modificando gli oggetti visivi esistenti, è possibile modificare report hello. Per altre informazioni, vedere [Interagire con un report nella Visualizzazione di modifica in Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/) .
>
>

Hello **avvisi nel tempo, le risorse ad attacchi** e **gli indirizzi IP utente malintenzionato** riquadri possono avere un output simile hello quando si fa clic su di esso ciascuna di esse. Ciò accade perché report hello vengono aggregate informazioni relative a tutte le tre variabili e chiama **risorse sotto attacco** come illustrato nella seguente schermata hello:

![Resources under Attack](./media/security-center-powerbi/security-center-powerbi-fig1-new7.png)

A questo punto è possibile inoltre salvare una copia di questo report, stamparlo o pubblicarlo nel web hello utilizzando hello opzioni disponibili in hello **File** menu.

![File menu](./media/security-center-powerbi/security-center-powerbi-fig8.png)

## <a name="exploring-your-azure-security-center-data-with-power-bi-services"></a>Esplorazione dei dati del Centro sicurezza di Azure con i servizi Power BI
Connettersi toohello [Content Pack Services di Power BI](https://msit.powerbi.com/groups/me/getdata/services) in Power BI ed eseguire hello alla procedura seguente:

1. In hello **pacchetto di contenuto per Power BI** finestra verranno visualizzate due opzioni, come illustrato di seguito.

    ![Content Pack for Power BI](./media/security-center-powerbi/security-center-powerbi-fig1-new.png)

   > [!NOTE]
   > Se è già stata eseguita prima parte di hello di questo articolo si visualizzeranno solo un'opzione, ovvero Gestione criteri di Centro protezione di Azure.
   >
   >
2. A scopo di hello di questo esempio, fare clic su **ottenere** in hello **Gestione criteri di Centro protezione Azure** riquadro.
3. In hello **connettersi tooAzure Gestione criteri di sicurezza Center** finestra, assicurarsi che tooselect **oAuth2** in **metodo di autenticazione** eliminare verso il basso, come illustrato di seguito e fare clic su **Accedi** pulsante.

    ![Finestra Gestione criteri](./media/security-center-powerbi/security-center-powerbi-fig1-new8.png)
4. Sarà reindirizzato tooan pagina di autenticazione in cui è necessario digitare le credenziali di hello che si sta utilizzando il Centro sicurezza PC tooAzure tooconnect. Una volta completato il processo di autenticazione hello, Power BI verrà avviata l'importazione di dati toobuild i report. Durante questo periodo potrebbe essere visualizzato hello segue messaggio nell'angolo destro di hello del browser:

    ![Connettere il Centro sicurezza PC tooAzure tramite Power BI](./media/security-center-powerbi/security-center-powerbi-fig4.png)

   > [!NOTE]
   > Quando il dashboard di hello viene creato per hello prima volta può richiedere più tempo del solito, principalmente per gli scenari in cui si dispone di più sottoscrizioni.
   >
   >
5. Una volta completato il processo di hello, il dashboard del Centro sicurezza di Azure Power BI verrà caricato con hello **Gestione criteri di** report simile toohello illustrato di seguito:

    ![Dashboard di gestione dei criteri](./media/security-center-powerbi/security-center-powerbi-fig1-new9.png)

## <a name="see-also"></a>Vedere anche
In questo documento, si è appreso toouse Power BI in Centro sicurezza di Azure. toolearn ulteriori informazioni su Centro sicurezza di Azure, vedere l'esempio hello:

* [Centro sicurezza di Azure Guida alla pianificazione e le operazioni](security-center-planning-and-operations-guide.md) , informazioni come tooplan adozione Centro sicurezza di Azure.
* [L'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md) , informazioni come le impostazioni di sicurezza tooconfigure nel Centro protezione di Azure
* [La gestione e risponde toosecurity gli avvisi in Centro sicurezza di Azure](security-center-managing-and-responding-alerts.md) , informazioni come avvisi toosecurity toomanage e rispondere
* [Domande frequenti su Centro sicurezza di Azure](security-center-faq.md) : domande frequenti sull'utilizzo di hello servizio di ricerca
* [Blog sulla sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/) : post di blog sulla sicurezza e sulla conformità di Azure
