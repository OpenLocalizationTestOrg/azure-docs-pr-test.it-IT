---
title: aaaHow toouse hello Azure Active Directory Power BI pacchetto di contenuto | Documenti Microsoft
description: Informazioni su come toouse hello Azure Active Directory Power BI pacchetto di contenuto
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d07d678aedbe3089c4ea5f981f72311bdb389a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-active-directory-power-bi-content-pack"></a>Come toouse hello Azure Active Directory Power BI pacchetto di contenuto

Comprendere in che modo gli utenti adottano e usano le funzionalità di Azure Active Directory è fondamentale per l'amministratore IT. Consente l'utilizzo di tooincrease di comunicazione e l'infrastruttura IT e tooget hello più fuori funzionalità AAD tooplan. Il contenuto di Power BI Pack per Azure Active Directory hello toofurther possibilità consente di analizzare toounderstand i dati come è possibile utilizzare questo dati toogather più approfondite cosa accade in Azure Active Directory per hello diverse capacità è molto si basano su.  Con l'integrazione di hello delle API di Azure Active Directory in Power BI, è possibile scaricare i pacchetti di contenuto preesistente hello facilmente e informazioni approfondite attività hello tooall all'interno di Azure Active Directory utilizzando l'esperienza di visualizzazione avanzata che offre Power BI. È possibile creare dashboard personalizzati e condividerli con altri utenti nell'organizzazione. 

In questo argomento fornisce si con istruzioni dettagliate su come tooinstall e utilizzare hello contenuto pack nell'ambiente in uso.

## <a name="installation"></a>Installazione  

**hello tooinstall pacchetto di contenuto di Power BI:**

1. Accedere a [Power BI](https://app.powerbi.com/groups/me/getdata/services) con l'Account di Power BI (si tratta di hello stesso account utilizzato per l'Account di Active Directory di Azure o Office 365).

2. Nella parte inferiore di hello del riquadro di spostamento a sinistra di hello, selezionare **recupera dati**.

    ![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/01.png)
 
3. In hello **servizi** fare clic su **ottenere**.
   
    ![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/02.png)

4.  Cercare **Azure Active Directory**.

    ![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/03.png)
 
5.  Quando richiesto, digitare l'ID tenant di Azure AD e quindi fare clic su **Avanti**.

    > [!TIP] 
    > Un hello tooget rapidamente Id Tenant per il tenant di Office 365 / Azure AD è toologin toohello portale di Azure AD, il drill-down directory toohello e copiare ID hello dal seguente URL hello: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ ActiveDirectoryExtension/Directory/<tenantid>/directoryQuickStart

    ![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/04.png) 

6.  Fare clic su **Accedi**. 
 
    ![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/05.png) 



7.  Immettere il nome utente e la password, quindi fare clic su **Accedi**.
 
    ![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/06.png) 

8.  Nella finestra di dialogo di consenso hello app, fare clic su **Accept**.
 
9.  Fare clic sul dashboard dei log attività di Azure Active Directory, dopo che è stato creato.
 
    ![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/08.png) 

## <a name="what-can-i-do-with-this-content-pack"></a>Operazioni eseguibili con il pacchetto di contenuto

Prima di passare è possibile procedere con questo pacchetto di contenuto, visualizzare in anteprima Ecco hello vari report nel contenuto hello pack. Report dati torna toohello **ultimi 30 giorni**.

### <a name="reports-included-in-this-version-of-azure-active-directory-logs-content-pack"></a>Report inclusi in questa versione del pacchetto di contenuto dei log di Azure Active Directory

**Report di utilizzo delle App e di tendenza**: ottenere informazioni approfondite App hello nell'organizzazione e quelle che vengono utilizzate più hello e quando. È possibile utilizzare questo report toogather approfondite sull'utilizzo di un'app è stato implementato all'interno dell'organizzazione o scoprire quali App vengono utilizzati di frequente. In questo modo, è possibile migliorare l'utilizzo se viene visualizzato se hello app non è in uso.

**Accessi dagli utenti e posizione**: ottenere informazioni approfondite tutti hello accessi eseguiti utilizzando l'identità di Azure e fornisce informazioni in identità hello hello utenti. È così possibile esaminare in dettaglio i singoli accessi e rispondere a domande come:

- Da dove ha effettuato l'accesso questo utente?
- L'utente che ha hello la maggior parte degli accessi e in cui sono Accedi da? 
- Completata Accedi hello?  
 
È possibile esaminare i dettagli facendo clic su una data o posizione specifica.

**Utenti univoci per ogni app**: ottenere una visualizzazione di tutti gli utenti univoci che usano un'app specifica. Comprende solo gli utenti che hanno completato "*correttamente*" l'accesso a un'applicazione.

**Dispositivo accessi**: ottenere una visualizzazione di tipo hello del sistema operativo e browser in uso da parte degli utenti dell'organizzazione con informazioni dettagliate sugli utenti hello tra cui:

- User Name
- Indirizzo IP
- Località 
- Stato accesso 

Con questo report, è possibile comprendere hello diversi profili di dispositivo utilizzato all'interno dell'organizzazione e determinano i criteri per i dispositivi in base a ciò che viene utilizzato

**Grafico a imbuto SSPR**: informazioni su come vengono reimpostate le password all'interno dell'organizzazione. Inserire una finestra Visualizza il numero di password Reimposta tentate tramite lo strumento SSPR hello e quanti di essi hanno avuto esito positivo. Un'analisi più approfondita in errore di reimpostazione Password di hello utilizzando a imbuto SSPR hello e capire perché alcuni errori si sono verificati. Questo report offre una comprensione più approfondita della modalità di utilizzo dello strumento SSPR hello all'interno dell'organizzazione in modo da prendere decisioni circostanziate hello.

## <a name="customizing-azure-ad-activity-content-pack"></a>Personalizzazione del pacchetto di contenuto per le attività di Azure AD

**Cambiare visualizzazione**: È possibile modificare una visualizzazione del report, fare clic su **Modifica Report** e visualizzazione di hello da selezionare.
 
![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/09.png) 
 
![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/10.png) 

**Includere campi aggiuntivi**: È possibile aggiungere un report toohello campo o rimuoverlo selezionando toowhich visual di hello si desidera che il campo di hello tooadd/Rimuovi. Nell'esempio hello seguente, si sta aggiungendo "stato di accesso" campo toohello tabella vista. 
 
![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/11.png) 

**Dashboard di pin visualizzazioni tooyour**: È possibile personalizzare il dashboard e includere visualizzazioni toohello un report personalizzato e aggiungerlo toohello dashboard. Nel seguente esempio hello aggiunto un nuovo filtro denominato "stato di accesso" e viene incluso nel report hello. Inoltre modificato visualizzazione hello da grafico a linee tooa grafico a barre e può aggiungere questo nuovo dashboard toohello visual.

![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/12.png) 

![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/13.png) 
 

 


**La condivisione di dashboard**: dopo aver creato il contenuto di hello che si desidera, è possibile condividere il dashboard di hello con utenti hello all'interno dell'organizzazione. Si tenga presente che quando si condividono i report di hello, possono essere visualizzate campi hello selezionati nel report hello.
 
![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/14.png) 



## <a name="scheduling-a-daily-refresh-of-your-power-bi-report"></a>Pianificazione di un aggiornamento giornaliero dei report di Power BI

tooschedule un aggiornamento giornaliero dei report di Power BI, andare troppo**set di dati > Impostazioni > pianificazione dell'aggiornamento** e impostarlo come illustrato di seguito.
 
![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/15.png) 

## <a name="updating-toonewer-version-of-content-pack"></a>L'aggiornamento di versione toonewer del pacchetto di contenuto

Se si desidera tooupdate il pacchetto di contenuto tooget una versione più recente:

- Scaricare di nuovo pacchetto di contenuto hello e configurarlo in base alle istruzioni riportate in questo articolo.

- Dopo aver impostato il, andare troppo**origine dati > Impostazioni > le credenziali dell'origine dati** e immettere nuovamente le credenziali, come illustrato di seguito

    ![Pacchetto di contenuto Power BI di Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/16.png) 

Come nuova versione di hello del pacchetto di contenuto hello funziona, è possibile rimuovere la versione precedente di hello se necessario, l'eliminazione di report sottostanti hello e set di dati associata a tale pacchetto di contenuto.

## <a name="still-having-issues"></a>Se i problemi persistono 

Vedere la [Guida per la risoluzione dei problemi](active-directory-reporting-troubleshoot-content-pack.md). Per informazioni generali su Power BI, vedere questi [articoli della Guida](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/).
 

## <a name="next-steps"></a>Passaggi successivi

Per una panoramica di gestione di report, vedere hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).
