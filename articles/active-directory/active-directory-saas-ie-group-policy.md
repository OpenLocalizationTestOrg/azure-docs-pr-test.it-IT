---
title: Estensione del Pannello di accesso di Azure per Internet Explorer utilizzando un oggetto Criteri di gruppo aaaDeploy | Documenti Microsoft
description: Toouse come gruppo di criteri toodeploy hello Internet Explorer del componente aggiuntivo per il portale di My Apps hello.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 7c2d49c8-5be0-4e7e-abac-332f9dfda736
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 926f15950bbe81d2fbfe1b0b856470da40880d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-hello-access-panel-extension-for-internet-explorer-using-group-policy"></a>Come tooDeploy hello estensione del Pannello di accesso per Internet Explorer utilizzando criteri di gruppo
Questa esercitazione viene illustrato come tooremotely criteri di gruppo toouse installare estensione del Pannello di accesso hello per Internet Explorer nei computer degli utenti. Questa estensione è necessaria per gli utenti di Internet Explorer che richiedono toosign nelle App che vengono configurate utilizzando [basato su password single sign-on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).

È consigliabile che gli amministratori di automatizzare hello distribuzione di questa estensione. In caso contrario, gli utenti hanno toodownload e installano estensione hello se stessi, ovvero toouser soggetta a errori e le autorizzazioni di amministratore. Questa esercitazione descrive un metodo per automatizzare le distribuzioni software tramite Criteri di gruppo. [Altre informazioni su Criteri di gruppo](https://technet.microsoft.com/windowsserver/bb310732.aspx)

estensione del Pannello di accesso Hello è disponibile anche per [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) e [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), nessuno dei quali richiedono tooinstall le autorizzazioni di amministratore.

## <a name="prerequisites"></a>Prerequisiti
* È stato impostato [servizi di dominio Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), e sono stati aggiunti dominio tooyour di computer degli utenti.
* È necessario disporre di hello tooedit autorizzazione "Modifica impostazioni" hello oggetto Criteri di gruppo (GPO). Per impostazione predefinita, i membri di gruppi di sicurezza seguente hello dispongono di questa autorizzazione: Domain Administrators, Enterprise Administrators e Group Policy Creator Owners. [Altre informazioni.](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-hello-distribution-point"></a>Passaggio 1: Creare il punto di distribuzione hello
In primo luogo, è necessario inserire il pacchetto di installazione di hello in un percorso di rete che è possibile accedere dai computer hello da estensione di hello installazione tooremotely in. toodo, seguire questi passaggi:

1. Accedere come amministratore toohello server
2. In hello **Server Manager** finestra andare troppo**file e servizi di archiviazione**.
   
    ![Apertura di Servizi file e archiviazione](./media/active-directory-saas-ie-group-policy/files-services.png)
3. Passare toohello **condivisioni** scheda. Fare clic su **Attività** > **Nuova condivisione...**
   
    ![Apertura di Servizi file e archiviazione](./media/active-directory-saas-ie-group-policy/shares.png)
4. Hello completo **Creazione guidata nuova condivisione** e tooensure di set di autorizzazioni che è possibile accedere dai computer degli utenti. [Altre informazioni sulle condivisioni.](https://technet.microsoft.com/library/cc753175.aspx)
5. Scaricare il pacchetto di Microsoft Windows Installer (file con estensione msi) seguenti hello: [Extension.msi Pannello di accesso](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)
6. Copia hello installer pacchetto tooa desiderato percorso condivisione hello.
   
    ![Condivisione di toohello file con estensione msi hello copia.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. Verificare che i computer client siano in grado di tooaccess pacchetto di installazione di hello dalla condivisione hello. 

## <a name="step-2-create-hello-group-policy-object"></a>Passaggio 2: Creare hello oggetto Criteri di gruppo
1. Log toohello server che ospita l'installazione di servizi di dominio Active Directory (AD DS).
2. In Server Manager hello, andare troppo**strumenti** > **Gestione criteri di gruppo**.
   
    ![Passare tooTools > Gestione criteri di gruppo](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. Nel riquadro di sinistra hello di hello **Gestione criteri di gruppo** finestra, visualizzare la gerarchia di unità organizzativa (OU) e determinare in quale ambito si desidera tooapply criteri di gruppo hello. Ad esempio, è possibile scegliere alcuni utenti toopick un piccolo tooa toodeploy unità Organizzativa per il testing oppure si potrebbe scegliere una livello superiore dell'unità Organizzativa toodeploy tooyour intera organizzazione.
   
   > [!NOTE]
   > Se si sarebbe come toocreate o modificare le unità organizzative (OU), passa indietro toohello Server Manager e andare troppo**strumenti** > **Active Directory Users and Computers**.
   > 
   > 
4. Dopo aver selezionato un'unità organizzativa, fare clic con il pulsante destro del mouse su di essa e scegliere **Crea un oggetto Criteri di gruppo in questo dominio e crea qui un collegamento...**
   
    ![Creare un nuovo oggetto Criteri di gruppo](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. In hello **nuovo oggetto Criteri di gruppo** prompt dei comandi, digitare un nome per hello nuovo oggetto Criteri di gruppo.
   
    ![Nome hello criteri di gruppo](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. Pulsante destro del mouse hello oggetto Criteri di gruppo creato e selezionare **modifica**.
   
    ![Modifica hello nuovo oggetto Criteri di gruppo](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-hello-installation-package"></a>Passaggio 3: Assegnare hello pacchetto di installazione
1. Determinare se si desidera che l'estensione di hello toodeploy basata sul **configurazione Computer** o **configurazione utente**. Quando si utilizza [configurazione computer](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), hello estensione è installata nel computer hello indipendentemente dal fatto che gli utenti accedono tooit. Con [configurazione utente](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), gli utenti hanno estensione hello installato relativa indipendentemente dal computer che eseguono l'accesso.
2. Nel riquadro di sinistra hello di hello **Editor Gestione criteri di gruppo** finestra, passare tooeither di hello seguono percorsi di cartella, a seconda del tipo di configurazione scelto:
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. Fare clic con il pulsante destro del mouse su **Installazione software** e quindi scegliere **Nuovo** > **Pacchetto...**
   
    ![Creare un nuovo pacchetto di installazione software](./media/active-directory-saas-ie-group-policy/new-package.png)
4. Passare toohello la cartella condivisa che contiene il pacchetto di installazione hello dalla [passaggio 1: creare il punto di distribuzione hello](#step-1-create-the-distribution-point), selezionare i file con estensione msi hello e fare clic su **aprire**.
   
   > [!IMPORTANT]
   > Se la condivisione hello si trova nel server stesso, verificare che si accede con estensione msi hello tramite percorso del file hello rete anziché hello percorso del file locale.
   > 
   > 
   
    ![Selezionare il pacchetto di installazione di hello dalla cartella condivisa hello.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. In hello **distribuire Software** prompt dei comandi, selezionare **assegnato** per il metodo di distribuzione. Fare quindi clic su **OK**.
   
    ![Selezionare Assegnata e quindi fare clic su OK.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

estensione Hello è ora distribuito toohello unità Organizzativa selezionata. [Altre informazioni su Criteri di gruppo Installazione software](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-hello-extension-for-internet-explorer"></a>Passaggio 4: Hello Auto-Enable estensione per Internet Explorer
Inoltre installer hello toorunning, ogni estensione per Internet Explorer deve essere abilitato in modo esplicito prima che possa essere utilizzato. Seguire la procedura seguente hello sotto tooenable hello estensione del Pannello di accesso tramite criteri di gruppo:

1. In hello **Editor Gestione criteri di gruppo** tooeither andare di hello seguono percorsi, a seconda del tipo di configurazione prescelto nella finestra [passaggio 3: assegnare hello pacchetto di installazione](#step-3-assign-the-installation-package):
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. Fare clic con il pulsante destro del mouse su **Elenco componenti aggiuntivi** e scegliere **Modifica**.
    ![Modifica dell'elenco componenti aggiuntivi.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)
3. In hello **elenco dei componenti aggiuntivi** selezionare **abilitato**. Quindi, in hello **opzioni** fare clic su **Mostra...** .
   
    ![Fare clic su Abilita e quindi su Mostra...](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. In hello **Mostra contenuto** finestra, eseguire hello alla procedura seguente:
   
   1. Per la prima colonna hello (hello **nome valore** campo), copia e Incolla hello seguente ID di classe:`{030E9A3F-7B18-4122-9A60-B87235E4F59E}`
   2. Per la seconda colonna hello (hello **valore** campo), tipo di hello il valore seguente:`1`
   3. Fare clic su **OK** tooclose hello **Mostra contenuto** finestra.
      
      ![Compilare i valori hello come specificato in precedenza.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. Fare clic su **OK** tooapply delle modifiche e chiudere hello **elenco dei componenti aggiuntivi** finestra.

Hello estensione ora dovrebbe essere abilitata per le macchine hello in hello selezionata unità Organizzativa. [Ulteriori informazioni sull'utilizzo tooenable di criteri di gruppo o disabilitare i componenti aggiuntivi di Internet Explorer.](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a>Passaggio 5 (facoltativo): disabilitare la richiesta "Memorizza password"
Quando gli utenti accesso toowebsites utilizzando hello estensione del Pannello di accesso, Internet Explorer potrebbe seguente hello Mostra prompt in cui viene chiesto "sarebbe è ad esempio toostore la password?"

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

Se si desiderano tooprevent agli utenti di visualizzare il prompt dei comandi, quindi seguire i passaggi di hello sotto tooprevent completamento automatico dalla memorizzazione di password:

1. In hello **Editor Gestione criteri di gruppo** finestra, passare toohello percorso elencati di seguito. Questa impostazione di configurazione è disponibile solo in **Configurazione utente**.
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. Trovare l'impostazione di hello denominato **attivare la funzionalità di completamento automatico hello i nomi utente e password sui moduli**.
   
   > [!NOTE]
   > Le versioni precedenti di Active Directory possono elencare questa impostazione con nome hello **non consentire password di completamento automatico toosave**. configurazione Hello per tale impostazione è diverso dall'impostazione di hello descritta in questa esercitazione.
   > 
   > 
   
    ![Tenere presente toolook per questo gruppo impostazioni utente.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. Fare clic con il pulsante destro hello di sopra di impostazione e selezionare **modifica**.
4. Nella finestra di hello intitolata **attivare la funzionalità di completamento automatico hello i nomi utente e password sui moduli**selezionare **disabilitato**.
   
    ![Selezionare Disabilita](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. Fare clic su **OK** tooapply le modifiche apportate e finestra hello Chiudi.

Gli utenti verranno non toostore in grado delle proprie credenziali o utilizzare le credenziali di completamento automatico tooaccess archiviati in precedenza. Tuttavia, questo criterio consente a utenti toocontinue toouse completamento automatico per altri tipi di campi form, ad esempio i campi di ricerca.

> [!WARNING]
> Se questo criterio viene attivato dopo che l'utente ha deciso toostore alcune credenziali, questo criterio verrà *non* Cancella credenziali hello che sono già state archiviate.
> 
> 

## <a name="step-6-testing-hello-deployment"></a>Passaggio 6: Test hello distribuzione
Se la distribuzione di un'estensione hello ha avuto esito positivo, effettuare le operazioni di hello sotto tooverify:

1. Se è stata distribuita mediante **configurazione Computer**, sign in un computer client appartenente toohello unità Organizzativa selezionata nel [passaggio 2: creare l'oggetto Criteri di gruppo hello](#step-2-create-the-group-policy-object). Se è stata distribuita mediante **configurazione utente**, assicurarsi che toosign in come un utente che appartiene toothat unità Organizzativa.
2. Potrebbe richiedere un paio di accesso aggiuntivi per i criteri di gruppo hello modifica toofully aggiornamento con questo computer. aggiornamento di hello tooforce, aprire un **prompt dei comandi** finestra e hello esecuzione comando seguente:`gpupdate /force`
3. È necessario riavviare il computer di hello sul posto di hello installazione tootake. Avvio può richiedere molto più tempo del normale durante l'estensione hello installa.
4. Dopo aver riavviato, aprire **Internet Explorer**. Nell'angolo superiore destro di hello della finestra hello, fare clic su **strumenti** (sull'icona a forma di ingranaggio hello), quindi selezionare **Gestione componenti aggiuntivi**.
   
    ![Passare tooTools > Gestione componenti aggiuntivi](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. In hello **Gestione componenti aggiuntivi** finestra, verificare che hello **estensione del Pannello di accesso** è stato installato e che il relativo **stato** è stato impostato troppo**abilitato**.
   
    ![Verificare che hello estensione del Pannello di accesso viene installato e attivato.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a>Articoli correlati
* [Indice di articoli per la gestione di applicazioni in Azure Active Directory](active-directory-apps-index.md)
* [Accesso alle applicazioni e Single Sign-On con Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Risoluzione dei problemi di estensione del Pannello di accesso hello per Internet Explorer](active-directory-saas-ie-troubleshooting.md)

