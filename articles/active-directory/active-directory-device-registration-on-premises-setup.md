---
title: aaaSetting backup mediante registrazione dispositivo di Azure Active Directory l'accesso condizionale locale | Documenti Microsoft
description: Una Guida dettagliata tooenabling accesso condizionale locale tooon le applicazioni utilizzando Active Directory Federation Services (ADFS) in Windows Server 2012 R2.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6ae9df8b-31fe-4d72-9181-cf50cfebbf05
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 808e3b96873102aebae667153f588dcdb205e884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-on-premises-conditional-access-by-using-azure-active-directory-device-registration"></a>Configurazione dell'accesso condizionale locale usando il servizio Registrazione dispositivo di Azure Active Directory
Quando si richiede agli utenti tooworkplace-join loro toohello dispositivi personali, il servizio Registrazione dispositivi di Azure Active Directory (Azure AD), i dispositivi possono essere contrassegnati come noti tooyour organizzazione. Di seguito è una Guida dettagliata per consentire alle applicazioni locali tooon di accesso condizionale con Active Directory Federation Services (ADFS) in Windows Server 2012 R2.

> [!NOTE]
> Quando si usano dispositivi registrati nei criteri di accesso condizionale del servizio Registrazione dispositivo di Azure Active Directory, è necessaria una licenza di Office 365 o una licenza di Azure AD Premium. Sono inclusi i criteri applicati da AD FS nelle risorse locali.
> 
> Per ulteriori informazioni sugli scenari di accesso condizionale hello per le risorse locali, vedere [accedere tooworkplace da qualsiasi dispositivo per SSO e l'autenticazione a due fattori trasparente per tutte le applicazioni aziendali](https://technet.microsoft.com/library/dn280945.aspx).

Queste funzionalità sono disponibili toocustomers che acquistano una licenza di Azure Active Directory Premium.

## <a name="supported-devices"></a>Dispositivi supportati
* Dispositivi Windows 7 aggiunti a un dominio
* Dispositivi Windows 8.1 personali e aggiunti a un dominio
* iOS 6 e versioni successive per il browser Safari hello
* Android 4.0 o versioni successive, telefoni Samsung GS3 o successivi, tablet Samsung Galaxy Note 2 o successivi

## <a name="scenario-prerequisites"></a>Prerequisiti dello scenario
* Sottoscrizione tooOffice 365 o Azure Active Directory Premium
* Tenant di Azure Active Directory
* Windows Server Active Directory (Windows Server 2008 o versioni successive)
* Schema aggiornato in Windows Server 2012 R2
* Licenza di Azure Active Directory Premium
* Windows Server 2012 R2 Federation Services, configurato per SSO tooAzure AD
* Proxy applicazione Web di Windows Server 2012 R2 
* Microsoft Azure Active Directory Connect (Azure AD Connect) [(Download di Azure AD Connect)](http://www.microsoft.com/en-us/download/details.aspx?id=47594)
* Dominio verificato

## <a name="known-issues-in-this-release"></a>Problemi noti in questa versione
* Criteri di accesso condizionale basato su dispositivo richiedono dispositivo oggetto writeback tooActive Directory da Azure Active Directory. Può richiedere ore toothree per toobe gli oggetti dispositivo riscritti tooActive Directory.
* i dispositivi iOS 7 richiedono sempre hello utente tooselect un certificato durante l'autenticazione del certificato client.
* Alcune versioni di iOS 8 precedenti a iOS 8.3 non funzionano.

## <a name="scenario-assumptions"></a>Presupposti dello scenario
Questo scenario presuppone l'esistenza di un ambiente ibrido, costituito da un tenant di Azure AD e un'istanza di Active Directory locale. Questi tenant devono essere connessi con Azure AD Connect, con un dominio verificato e con AD FS per SSO. Utilizzare hello dopo avere configurato l'ambiente in base a requisiti toohello toohelp di elenco di controllo.

## <a name="checklist-prerequisites-for-conditional-access-scenario"></a>Elenco di controllo: prerequisiti per lo scenario di accesso condizionale
Connettere il tenant di Azure AD all'istanza di Active Directory locale.

## <a name="configure-azure-active-directory-device-registration-service"></a>Configurare il servizio Registrazione dispositivo di Azure Active Directory
Utilizzare questo toodeploy Guida e configurare hello servizio Registrazione dispositivi di Azure Active Directory per l'organizzazione.

Questa guida si presuppone di aver configurato Windows Server Active Directory e sottoscritti tooMicrosoft Azure Active Directory. Vedere la sezione Prerequisiti di hello descritti in precedenza.

hello toodeploy servizio Registrazione dispositivi di Azure Active Directory con Azure Active Directory del tenant, attività di completamento hello in hello controllo nell'ordine indicato di seguito. Quando un collegamento di riferimento porta argomento concettuale tooa, tornare in seguito, elenco di controllo toothis in modo da poter procedere con le attività rimanenti hello. Alcune attività includono un passaggio di convalida di uno scenario che consente di verificare se il passaggio di hello è stato completato correttamente.

## <a name="part-1-enable-azure-active-directory-device-registration"></a>Parte 1: Abilitare Registrazione dispositivo di Azure Active Directory
Procedura hello tooenable checklist hello e configurare il servizio Registrazione dispositivi di hello Azure Active Directory.

| Attività | riferimento | 
| --- | --- |
| Abilitare la registrazione del dispositivo in Azure Active Directory tenant tooallow dispositivi toojoin hello rete aziendale. Per impostazione predefinita, Azure multi-Factor Authentication non è abilitato per servizio hello. Tuttavia, è consigliabile usare l'autenticazione a più fattori quando si registra un dispositivo. Prima di abilitare Multi-Factor Authentication nel servizio Registrazione dispositivo di Active Directory, verificare che AD FS sia configurato per un provider di autenticazione a più fattori. |[Abilitare Registrazione dispositivo di Azure Active Directory](active-directory-device-registration-get-started.md)| 
|I dispositivi individuano il servizio Registrazione dispositivo di Azure Active Directory cercando record DNS noti. Configurare il DNS della società in modo che i dispositivi possano rilevare il servizio Registrazione dispositivo di Azure Active Directory. |[Configurare l'individuazione di Registrazione dispositivo di Azure Active Directory.](active-directory-device-registration-get-started.md)| 


## <a name="part-2-deploy-and-configure-windows-server-2012-r2-active-directory-federation-services-and-set-up-a-federation-relationship-with-azure-ad"></a>Parte 2: Distribuire e configurare Active Directory Federation Services con Windows Server 2012 R2 e configurare una relazione federativa con Azure AD

| Attività | riferimento |
| --- | --- |
| Distribuire servizi di dominio Active Directory con estensioni dello schema di Windows Server 2012 R2 hello. Non è necessario tooupgrade qualsiasi il tooWindows di controller di dominio Server 2012 R2. aggiornamento dello schema Hello è l'unico requisito hello. |[Aggiornare lo schema di Active Directory Domain Services](#upgrade-your-active-directory-domain-services-schema) |
| I dispositivi individuano il servizio Registrazione dispositivo di Azure Active Directory cercando record DNS noti. Configurare il DNS della società in modo che i dispositivi possano rilevare il servizio Registrazione dispositivo di Azure Active Directory. |[Preparare Active Directory per supportare i dispositivi](#prepare-your-active-directory-to-support-devices) |

## <a name="part-3-enable-device-writeback-in-azure-ad"></a>Parte 3: Abilitare il writeback dei dispositivi in Azure AD
| Attività | Riferimento |
| --- | --- |
| Completare la parte due di "Abilitazione del writeback dei dispositivi in Azure AD Connect". Al termine, viene restituito toothis Guida. |[Abilitazione del writeback dei dispositivi in Azure AD Connect](#upgrade-your-active-directory-domain-services-schema) |

## <a name="optional-part-4-enable-multi-factor-authentication"></a>[Facoltativo] Parte 4: Abilitazione di Multi-Factor Authentication
È consigliabile configurare uno dei hello diverse opzioni per l'autenticazione a più fattori. Se si desidera toorequire multi-Factor Authentication, vedere [scegliere una soluzione di sicurezza di multi-Factor Authentication hello è](../multi-factor-authentication/multi-factor-authentication-get-started.md). Include una descrizione di ogni soluzione e collegamenti toohelp si configura la soluzione hello di propria scelta.

## <a name="part-5-verification"></a>Parte 5: Verifica
distribuzione Hello è stata completata e che è possibile provare alcuni scenari. Utilizzare hello seguente collega tooexperiment con servizio hello e acquisire familiarità con le funzionalità.

| Attività | riferimento |
| --- | --- |
| Aggiungere all'area di lavoro tooyour alcuni dispositivi tramite il servizio Registrazione dispositivi di Azure Active Directory. È possibile aggiungere dispositivi iOS, Windows e Android. |[Aggiunta all'area di lavoro di dispositivi tooyour con Azure Active Directory device registration service](#join-devices-to-your-workplace-using-azure-active-directory-device-registration) |
| Visualizzare e abilitare o disabilitare i dispositivi registrati tramite il portale di amministrazione di hello. In questa attività si visualizzano alcuni dispositivi registrati tramite il portale di amministrazione di hello. |[Panoramica del servizio Registrazione dispositivo di Azure Active Directory](active-directory-device-registration-get-started.md) |
| Verificare che gli oggetti dispositivo vengono scritti nuovamente da Azure Active Directory tooWindows Server Active Directory. |[Verificare che i dispositivi registrati vengono scritte tooActive Directory](#verify-registered-devices-are-written-back-to-active-directory) |
| Ora che gli utenti possono registrare i propri dispositivi, è possibile creare criteri di accesso alle applicazioni in AD FS che consentano l'accesso solo a dispositivi registrati. In questa attività viene creata una regola di accesso alle applicazioni e un messaggio di accesso negato personalizzato. |[Creare un criterio di accesso alle applicazioni e un messaggio di accesso negato personalizzato](#create-an-application-access-policy-and-custom-access-denied-message) |

## <a name="integrate-azure-active-directory-with-on-premises-active-directory"></a>Integrare Azure Active Directory con l'istanza di Active Directory locale
Questo passaggio consente di integrare il tenant di Azure AD con l'istanza di Active Directory locale usando Azure AD Connect. Anche se i passaggi di hello sono disponibili nel portale di Azure classico hello, prendere nota di eventuali istruzioni presenti in questa sezione.

1. Accedi toohello portale di Azure classico utilizzando un account che sia un amministratore globale di Azure AD.
2. Nel riquadro sinistro di hello selezionare **Active Directory**.
3. In hello **Directory** scheda, selezionare la directory.
4. Seleziona hello **integrazione Directory** scheda.
5. In hello **distribuire e gestire** sezione, seguire i passaggi da 1 a 3 toointegrate Azure Active Directory con la directory locale.
   
   1. Aggiungere i domini.
   2. Installare ed eseguire Azure AD Connect tramite istruzioni hello in [installazione personalizzata di Azure AD Connect](connect/active-directory-aadconnect-get-started-custom.md).
   3. Verificare e gestire la sincronizzazione della directory. Le istruzioni per l'accesso Single Sign-On sono disponibili in questo passaggio.
   
   Configurare anche la federazione con AD FS come indicato in [Installazione personalizzata di Azure AD Connect](connect/active-directory-aadconnect-get-started-custom.md).

## <a name="upgrade-your-active-directory-domain-services-schema"></a>Aggiornare lo schema di Servizi di dominio Active Directory
> [!NOTE]
> Dopo aver aggiornato lo schema di Active Directory, il processo di hello non può essere annullato. È consigliabile eseguire prima l'aggiornamento di hello in un ambiente di test.
> 

1. Accedi tooyour i controller di dominio con un account che dispone sia di amministratore dell'organizzazione e dei diritti di amministratore di schema.
2. Hello copia **[supporto] \support\adprep** tooone directory e sottodirectory dei controller di dominio Active Directory (in cui **[media]** è supporti di installazione di Windows Server 2012 R2 di hello percorso toohello ).
4. Da un prompt dei comandi, passare toohello **adprep** directory ed eseguire **adprep.exe /forestprep**. Seguire l'aggiornamento dello schema di hello istruzioni visualizzate sullo schermo toocomplete hello.

## <a name="prepare-your-active-directory-toosupport-devices"></a>Preparare i dispositivi toosupport Active Directory
> [!NOTE]
> Questa è un'operazione occasionale che è necessario eseguire tooprepare i dispositivi toosupport foresta di Active Directory. toocomplete questa procedura, è necessario essere connessi con autorizzazioni di amministratore dell'organizzazione e la foresta Active Directory deve disporre dello schema di Windows Server 2012 R2 hello.
> 


### <a name="prepare-your-active-directory-forest"></a>Preparare la foresta Active Directory
1. Nel server federativo aprire una finestra di comando di Windows PowerShell e digitare **Initialize-ADDeviceRegistration**. 
2. Quando viene richiesto di **ServiceAccountName**, immettere il nome di hello hello dell'account di servizio è stato selezionato come account del servizio hello per AD FS. Se si tratta di un account gestito, è possibile immettere account hello in hello **domain\accountname$** formato. Per un account di dominio, utilizzare il formato di hello **dominio\nomeaccount**.

### <a name="enable-device-authentication-in-ad-fs"></a>Abilitare l'autenticazione dispositivo in AD FS
1. Nel server federativo, aprire la console di gestione hello ADFS e passare troppo**ADFS** > **criteri di autenticazione**.
2. In hello **azioni** riquadro, selezionare **Edit Global Primary Authentication**.
3. Selezionare **Abilita autenticazione dispositivo** e quindi **OK**.
4. Per impostazione predefinita, AD FS rimuove periodicamente da Active Directory i dispositivi inutilizzati. Disabilitare questa attività quando si usa il servizio Registrazione dispositivo di Azure Active Directory, in modo che i dispositivi possano essere gestiti in Azure.

### <a name="disable-unused-device-cleanup"></a>Disabilitare la pulizia dei dispositivi inutilizzati
Nel server federativo aprire una finestra di comando di Windows PowerShell e digitare **Set-AdfsDeviceRegistration -MaximumInactiveDays 0**.

### <a name="prepare-azure-ad-connect-for-device-writeback"></a>Preparare Azure AD Connect per il writeback dei dispositivi
Completare la parte 1: preparare Azure AD Connect.

## <a name="join-devices-tooyour-workplace-by-using-azure-active-directory-device-registration-service"></a>Creare un join all'area di lavoro di dispositivi tooyour utilizzando il servizio Registrazione dispositivi di Azure Active Directory

### <a name="join-an-ios-device-by-using-azure-active-directory-device-registration"></a>Aggiungere un dispositivo iOS con Registrazione dispositivo di Azure Active Directory
Registrazione dispositivo di Azure Active Directory utilizza processo di registrazione hello Over-the-Air profilo per i dispositivi iOS. Questo processo inizia quando l'utente hello collega l'URL del profilo di registrazione toohello con Safari. formato URL Hello è come segue:

    https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/"yourdomainname"

In questo caso, `yourdomainname` hello nome di dominio configurato con Azure Active Directory. Ad esempio, se il nome di dominio è contoso.com, URL hello è come segue:

    https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/contoso.com

Esistono molti modi diversi toocommunicate questo tooyour URL usato dagli utenti. Un metodo consigliato, ad esempio, consiste nel pubblicare l'URL in un messaggio personalizzato di accesso all'applicazione negato in AD FS. Queste informazioni viene descritta nella sezione successiva di hello [creare un criterio di accesso di applicazioni e un messaggio di accesso negato personalizzato](#create-an-application-access-policy-and-custom-access-denied-message).

### <a name="join-a-windows-81-device-by-using-azure-active-directory-device-registration"></a>Aggiungere un dispositivo Windows 8.1 con Registrazione dispositivo di Azure Active Directory
1. Nel dispositivo Windows 8.1 selezionare **Impostazioni PC** > **Rete** > **Area di lavoro**.
2. Immettere il proprio nome utente in formato UPN, ad esempio **dan@contoso.com**.
3. Selezionare **Aggiungi**.
4. Quando richiesto, accedere con le proprie credenziali. ora è stato aggiunto il dispositivo Hello.

### <a name="join-a-windows-7-device-by-using-azure-active-directory-device-registration"></a>Aggiungere un dispositivo Windows 7 con Registrazione dispositivo di Azure Active Directory
dispositivi appartenenti a un dominio di Windows 7 tooregister, è necessario toodeploy hello pacchetto software di registrazione. Hello pacchetto software viene chiamato all'area di lavoro Join per Windows 7 e le relative disponibili per il download all'indirizzo hello [sito Web Microsoft Connect](https://connect.microsoft.com/site1164). 

Le istruzioni su come toouse hello pacchetto sono disponibili in [come tooconfigure la registrazione automatica di Windows appartenenti a un dominio dispositivi con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).

## <a name="verify-that-registered-devices-are-written-back-tooactive-directory"></a>Verificare che i dispositivi registrati vengono scritte tooActive Directory
È possibile visualizzare e verificare che gli oggetti dispositivo sono stati scritti nuovamente tooyour Active Directory mediante LDP.exe o ADSI Edit. Entrambi sono disponibili con strumenti di amministrazione di Active Directory hello.

Per impostazione predefinita, gli oggetti dispositivo che vengono scritti nuovamente da Azure Active Directory vengono posizionati in hello stesso dominio della farm AD FS.

    CN=RegisteredDevices,defaultNamingContext

## <a name="create-an-application-access-policy-and-custom-access-denied-message"></a>Creare un criterio di accesso alle applicazioni e un messaggio di accesso negato personalizzato
Prendere in considerazione hello seguente scenario: si crea un'applicazione Trust della Relying Party in ADFS e configurare una regola di autorizzazione di rilascio che consente solo dispositivi registrati. Ora solo i dispositivi registrati possono tooaccess un'applicazione hello. 

toomake è più facile per gli utenti toogain access toohello, configuri un messaggio di accesso negato personalizzato che include istruzioni su come toojoin il dispositivo. Ora gli utenti devono tooregister un modo semplice i propri dispositivi per consentire di accedere a un'applicazione.

Hello passaggi seguenti viene illustrato come tooimplement questo scenario.

> [!NOTE]
> Questa sezione presuppone che sia già stato configurato un trust della relying party per l'applicazione in AD FS.
> 

1. Aprire hello strumento ADFS di MMC e quindi selezionare **ADFS** > **relazioni di Trust** > **Relying Party Trusts**.
2. Individuare toowhich applicazione hello che si applica questa nuova regola di accesso. Un'applicazione hello e quindi scegliere **Modifica regole attestazione**.
3. Seleziona hello **regole di autorizzazione rilascio** scheda e quindi selezionare **Aggiungi regola**.
4. Da hello **regola attestazione** modello-elenco a discesa Seleziona **consentire o negare agli utenti in base a un'attestazione in ingresso**. Quindi selezionare **Avanti**.
5. In hello **nome regola attestazione** digitare **consentano l'accesso da dispositivi registrati**.
6. Da hello **tipo di attestazione in ingresso** elenco a discesa, seleziona **Is Registered User**.
7. In hello **valore attestazione in ingresso** digitare **true**.
8. Seleziona hello **permesso di accesso toousers con questa attestazione in ingresso** pulsante di opzione.
9. Selezionare **Fine** e quindi **Applica**.
10. Rimuovere tutte le regole più permissive regola hello creato. Ad esempio, rimuovere la regola predefinita di hello **tooall Permit Access utenti**.

L'applicazione è ora configurato tooallow accedere solo quando l'utente hello proviene da un dispositivo che registrato e aggiunto all'area di lavoro toohello. Per i criteri di accesso più avanzati, vedere l'articolo relativo alla [gestione dei rischi con autenticazione a più fattori aggiuntiva per le applicazioni sensibili](https://technet.microsoft.com/library/dn280949.aspx).

Configurare quindi un messaggio di errore personalizzato per l'applicazione. messaggio di errore Hello fa sapere agli utenti che devono aggiungere il loro lavoro toohello dispositivo prima di poter accedere a un'applicazione hello. È possibile creare un messaggio personalizzato di accesso all'applicazione negato usando codice HTML personalizzato e PowerShell.

Nel server federativo, aprire una finestra di comando di PowerShell e quindi digitare hello comando seguente. Sostituire alcune parti del comando hello con gli elementi che sono tooyour specifici di sistema:

    Set-AdfsRelyingPartyWebContent -Name "relying party trust name" -ErrorPageAuthorizationErrorMessage
Prima di poter accedere all'applicazione, è necessario registrare il dispositivo.

**Se si utilizza un dispositivo iOS, selezionare il collegamento di toojoin il dispositivo**:

    a href='https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/yourdomain.com

Aggiungere all'area di lavoro tooyour dispositivo iOS.

Se si usa un dispositivo Windows 8.1, è possibile aggiungere il dispositivo selezionando **Impostazioni PC** > **Rete** > **Area di lavoro**.

In hello precedenti comandi, **nome relazione di trust di relying party** hello nome dell'oggetto Trust della Relying Party dell'applicazione in ADFS.
E **<sottodominio>.nomedominio.com** hello nome di dominio che è stato configurato con Azure Active Directory (ad esempio, contoso.com).
Essere tooremove verificare eventuali interruzioni di riga (se presente) da hello HTML contenuto che si passa toohello **Set-AdfsRelyingPartyWebContent** cmdlet.

Ora quando gli utenti accedono all'applicazione da un dispositivo che non è registrato con hello servizio Registrazione dispositivi di Azure Active Directory, vengono visualizzati una pagina simile toohello seguente schermata.

![Schermata di un errore visualizzato quando gli utenti non hanno registrato il dispositivo con Azure AD](./media/active-directory-conditional-access/error-azureDRS-device-not-registered.gif)


