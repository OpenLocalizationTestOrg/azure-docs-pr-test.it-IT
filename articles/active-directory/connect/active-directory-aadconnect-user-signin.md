---
title: Azure AD Connect - Accesso utente | Microsoft Docs
description: Accesso utente Azure Connect AD per le impostazioni personalizzate.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 547b118e-7282-4c7f-be87-c035561001df
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 7848b419f3855b25cfa074a46779d258bd534bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-user-sign-in-options"></a>Opzioni di accesso utente di Azure AD Connect
Connect di Azure Active Directory (Azure AD) consente il toosign gli utenti nel cloud tooboth e alle risorse locali utilizzando hello stesse password. Questo articolo descrive i concetti chiave per ogni toohelp modello di identità che è scegliere hello identità che si desidera toouse per la firma in tooAzure Active Directory.

Se si ha già familiarità con il modello di identità hello Azure AD e si desidera toolearn informazioni su un metodo specifico, fare clic sul collegamento appropriato hello:

* [Sincronizzazione delle password](#password-synchronization) con [accesso Single Sign-On (SSO)](active-directory-aadconnect-sso.md)
* [Autenticazione pass-through](active-directory-aadconnect-pass-through-authentication.md)
* [SSO federato (con Active Directory Federation Services, AD FS)](#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)

## <a name="choosing-hello-user-sign-in-method-for-your-organization"></a>Scelta di hello utente metodo di accesso per l'organizzazione
Per la maggior parte delle organizzazioni che si desidera tooenable utente Accedi tooOffice 365 applicazioni SaaS e altre risorse di Azure basato su Active Directory, è consigliabile l'opzione di sincronizzazione password predefinito hello. Alcune organizzazioni, tuttavia, dispongono di un motivo specifico che non sono in grado di toouse questa opzione. Queste organizzazioni possono scegliere un'opzione di accesso federato come AD FS oppure l'autenticazione pass-through. È possibile utilizzare hello seguente toohelp tabella hello destra scelta.

È necessario troppo| PS con SSO| PA con SSO| AD FS |
 --- | --- | --- | --- |
Sincronizza automaticamente nuovo utente, contatti e gli account di gruppo nel cloud toohello di Active Directory locale.|x|x|x|
Configurare il tenant per scenari ibridi di Office 365.|x|x|x|
Abilitare i toosign gli utenti in e i servizi cloud di accesso utilizzando la password locale.|x|x|x|
Implementare l'accesso Single Sign-On usando le credenziali aziendali.|x|x|x|
Verificare che nessuna password viene archiviata nel cloud hello.||x*|x|
Abilitare soluzioni di autenticazione a più fattori locali.|||x|

* Tramite un connettore leggero.

>[!NOTE]
> L'autenticazione pass-through presenta attualmente alcune limitazioni con i rich client. Per altre informazioni, vedere [Autenticazione pass-through](active-directory-aadconnect-pass-through-authentication.md).

### <a name="password-synchronization"></a>Sincronizzazione delle password
Con la sincronizzazione delle password, gli hash delle password utente vengono sincronizzati da tooAzure di Active Directory locale AD. Quando le password vengono modificate o reimpostare locale, le nuove password hello vengono sincronizzati tooAzure AD immediatamente in modo che gli utenti possono sempre utilizzare hello stessa password per le risorse del cloud e locali. password di Hello vengono mai inviate AD tooAzure o archiviate in Azure AD in testo non crittografato. È possibile utilizzare la sincronizzazione delle password con password tooenable writeback self-service la reimpostazione della password in Azure AD.

Inoltre, è possibile abilitare [SSO](active-directory-aadconnect-sso.md) per gli utenti del computer appartenenti a un dominio sulla rete aziendale hello. Single sign-on, è abilitati solo con utenti necessario tooenter toohelp un nome utente loro in modo sicuro l'accesso alle risorse cloud.

![Sincronizzazione delle password](./media/active-directory-aadconnect-user-signin/passwordhash.png)

Per ulteriori informazioni, vedere hello [la sincronizzazione delle password](active-directory-aadconnectsync-implement-password-synchronization.md) articolo.

### <a name="pass-through-authentication"></a>Autenticazione pass-through
Con l'autenticazione pass-through, viene convalidata la password dell'utente hello sul controller di Active Directory locale hello. password Hello non deve necessariamente toobe presente in Azure Active Directory in qualsiasi forma. In questo modo per i criteri locali, ad esempio restrizioni sugli orari di accesso toobe valutata durante servizi toocloud di autenticazione.

L'autenticazione pass-through viene utilizzato un agente semplice in un computer aggiunto al dominio Windows Server 2012 R2 in hello nell'ambiente locale. che resta in attesa di richieste di convalida delle password. Non richiede le porte in ingresso toobe aprire toohello Internet.

Inoltre, è possibile abilitare single sign-on per gli utenti di computer appartenenti a un dominio sulla rete aziendale hello. Single sign-on, è abilitati solo con utenti necessario tooenter toohelp un nome utente loro in modo sicuro l'accesso alle risorse cloud.
![Autenticazione pass-through](./media/active-directory-aadconnect-user-signin/pta.png)

Per altre informazioni, vedere:
- [Autenticazione pass-through](active-directory-aadconnect-pass-through-authentication.md)
- [Single Sign-On](active-directory-aadconnect-sso.md)

### <a name="federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2"></a>Federazione che usa una farm nuova o esistente con AD FS in Windows Server 2012 R2
Con federato accesso, gli utenti possono accedere tooAzure servizi basati su Active Directory e le relative password locale. Mentre si trovano nella rete aziendale hello, non ancora hanno tooenter le proprie password. Utilizzando l'opzione di federazione hello con AD FS, è possibile distribuire una farm nuova o esistente con AD FS in Windows Server 2012 R2. Se si sceglie toospecify una farm esistente, Azure AD Connect Configura hello trust tra la farm e Azure AD in modo che gli utenti possono accedere.

<center>![Federazione con AD FS in Windows Server 2012 R2](./media/active-directory-aadconnect-user-signin/federatedsignin.png)</center>

#### <a name="deploy-federation-with-ad-fs-in-windows-server-2012-r2"></a>Distribuire la federazione con AD FS in Windows Server 2012 R2

Se si distribuisce una nuova farm, è necessario quanto segue:

* Un server di Windows Server 2012 R2 per server federativo hello.
* Un server di Windows Server 2012 R2 per hello Proxy applicazione Web.
* Un file PFX con un certificato SSL per il nome del servizio federativo desiderato, ad esempio fs.contoso.com.

Se si distribuisce una nuova farm o si usa una farm esistente, è necessario quanto segue:

* Credenziali di amministratore locale nei server federativi in uso.
* Credenziali di amministratore locale su tutti i server del gruppo di lavoro (non appartenenti a un dominio) che si desidera toodeploy hello ruolo Proxy applicazione Web in.
* Hello computer che si esegue la procedura guidata hello in toobe tooconnect in grado di tooany altri computer che si desidera tooinstall ADFS o Proxy applicazione Web in tramite Gestione remota Windows.

Per altre informazioni, vedere [Configurazione di SSO con AD FS](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs).

#### <a name="sign-in-by-using-an-earlier-version-of-ad-fs-or-a-third-party-solution"></a>Accedere usando una versione precedente di AD FS o una soluzione di terze parti
Se è già stato configurato Accedi cloud utilizzando una versione precedente di ADFS (ad esempio AD FS 2.0) o un provider di terze parti federazione, è possibile scegliere tooskip Accedi configurazione utente tramite Azure AD Connect. Ciò consentirà la sincronizzazione più recente di tooget hello e altre funzionalità di Azure AD Connect pur continuando a utilizzare la soluzione esistente per l'accesso.

Per ulteriori informazioni, vedere hello [elenco di compatibilità di Azure AD federativi di terze parti](active-directory-aadconnect-federation-compatibility.md).


## <a name="user-sign-in-and-user-principal-name"></a>Accesso utente e nome dell'entità utente
### <a name="understanding-user-principal-name"></a>Informazioni sul nome dell'entità utente
In Active Directory, suffisso del nome principale (UPN) utente predefinito hello è il nome DNS hello del dominio hello in cui è stato creato l'account utente di hello. Nella maggior parte dei casi, si tratta di nome di dominio hello è registrato come dominio enterprise hello hello Internet. Tuttavia, è possibile aggiungere altri suffissi UPN usando Domini e trust di Active Directory.

UPN dell'utente hello Hello è formato hello username@domain. Per un dominio di Active Directory denominato "contoso.com", ad esempio, un utente denominato John potrebbe essere hello UPN "john@contoso.com". UPN dell'utente hello Hello è basato su RFC 822. Sebbene hello UPN e condivisione di posta elettronica hello stesso formato, il valore di hello di hello UPN per un utente può o potrebbe non essere hello stesso come indirizzo di posta elettronica hello dell'utente hello.

### <a name="user-principal-name-in-azure-ad"></a>Nome dell'entità utente in Azure AD
procedura guidata di Azure AD Connect Hello utilizza l'attributo userPrincipalName hello o consente di che specificare hello toobe attributo (in un'installazione personalizzata) usate da locale come nome dell'entità utente hello in Azure AD. Questo è il valore hello che viene utilizzato per la firma in tooAzure Active Directory. Se il valore di hello dell'attributo userPrincipalName hello non corrisponde tooa verificato dominio in Azure AD, quindi Azure AD lo sostituisce con un valore predefinito. il valore di c o m.

Tutte le directory in Azure Active Directory viene fornito con un nome di dominio predefinito, con hello formato contoso.onmicrosoft.com, che consente iniziare a usare Azure o altri servizi Microsoft. È possibile migliorare e semplificare l'esperienza di accesso hello utilizzando domini personalizzati. Per informazioni sui nomi di dominio personalizzato in Azure AD e tooverify un dominio, vedere [aggiungere tooAzure di nome Active Directory del dominio personalizzato](../add-custom-domain.md#add-your-custom-domain).

## <a name="azure-ad-sign-in-configuration"></a>Configurazione dell'accesso ad Azure AD
### <a name="azure-ad-sign-in-configuration-with-azure-ad-connect"></a>Configurazione dell'accesso ad Azure AD con Azure AD Connect
esperienza di accesso AD Azure Hello dipende dal fatto può corrispondere a hello suffisso di un utente che viene sincronizzato tooone di domini personalizzati hello che vengono verificate nella directory di Azure AD hello Azure AD. Azure AD Connect Guida durante la configurazione di Azure AD impostazioni di accesso, in modo che sia di hello Accedi esperienza utente nel cloud hello esperienza di on-premise toohello simile.

Gli elenchi di Azure AD Connect hello suffissi UPN definiti per hello toomatch di domini e i tentativi con un dominio personalizzato in Azure AD. Quindi consente con l'azione appropriata hello necessarie toobe eseguita.
Hello Azure AD nella pagina di accesso sono elencati i suffissi UPN hello definiti per Active Directory locale e visualizza lo stato corrispondente hello su ogni suffisso. i valori di stato Hello possono essere uno dei seguenti hello:

| Stato | Descrizione | Azione necessaria |
|:--- |:--- |:--- |
| Verified |Azure AD Connect ha rilevato un dominio verificato in Azure AD. Tutti gli utenti di questo dominio possono accedere usando le credenziali locali. |Non è richiesto alcun intervento. |
| Non verificato |Azure AD Connect ha rilevato un dominio corrispondente in Azure AD ma tale dominio non è verificato. il suffisso UPN Hello di utenti hello di questo dominio sarà modificato toohello predefinito. il suffisso onmicrosoft.com dopo la sincronizzazione se non viene verificato il dominio di hello. | [Verificare di dominio personalizzato hello in Azure AD.](../add-custom-domain.md#verify-the-domain-name-with-azure-ad) |
| Non aggiunto |Azure AD Connect non viene trovato un dominio personalizzato al suffisso UPN toohello corrispondeva. il suffisso UPN Hello di utenti hello di questo dominio sarà modificato predefinito toohello. suffisso onmicrosoft.com se dominio hello non è aggiunto e verificato in Azure. | [Aggiungere e verificare un dominio personalizzato che corrisponde a un suffisso UPN toohello.](../add-custom-domain.md) |

Hello Azure AD nella pagina di accesso sono elencati i suffissi UPN hello definiti per Active Directory locale e hello corrispondente dominio personalizzato in Azure AD con stato verifica corrente hello. In un'installazione personalizzata, è ora possibile selezionare attributo hello per nome dell'entità utente di hello in hello **Accedi AD Azure** pagina.

![Pagina di accesso di Azure AD](./media/active-directory-aadconnect-user-signin/custom_azure_sign_in.png)

È possibile fare clic su hello aggiornamento pulsante toore-fetch hello stato più recente di domini personalizzati di hello da Azure AD.

### <a name="selecting-hello-attribute-for-hello-user-principal-name-in-azure-ad"></a>Selezionare l'attributo di hello per nome dell'entità utente hello in Azure AD
Hello attributo userPrincipalName è l'attributo hello utilizzato dagli utenti quando accedono tooAzure AD e Office 365. È necessario verificare i domini hello (noto anche come suffissi UPN) utilizzati in Azure AD prima di hello utenti sono sincronizzati.

È consigliabile mantenere hello predefinito attributo userPrincipalName. Se questo attributo è nonroutable e non è possibile verificare, quindi è possibile tooselect (posta elettronica, ad esempio) a un altro attributo come attributo hello contenente hello ID di accesso. Questo è noto come hello ID alternativo. valore dell'attributo ID alternativo Hello deve seguire hello RFC 822 standard. È possibile utilizzare un ID alternativo con federazione SSO come soluzione di accesso hello e la password SSO.

> [!NOTE]
> L'uso di un ID alternativo non è compatibile con tutti i carichi di lavoro di Office 365. Per altre informazioni, vedere [Configurazione dell'ID di accesso alternativo](https://technet.microsoft.com/library/dn659436.aspx).
>
>

#### <a name="different-custom-domain-states-and-their-effect-on-hello-azure-sign-in-experience"></a>Stati di dominio personalizzato diverso e il relativo effetto sull'esperienza hello Accedi Azure
È molto importante toounderstand hello relazione tra gli stati di dominio personalizzato hello nella directory di Azure AD e suffissi UPN che sono hello definito in locale. Verrà ora analizzato hello possibili Azure Accedi esperienze diverse quando si sta configurando la sincronizzazione con Azure AD Connect.

Hello le seguenti informazioni, si supponga ad esempio che si è interessati a contoso.com suffisso UPN di hello, che viene utilizzata nella directory locale hello come parte del nome UPN, ad esempio user@contoso.com.

###### <a name="express-settingspassword-synchronization"></a>Impostazioni rapide / Sincronizzazione delle password
| Stato | Effetto sull'esperienza di accesso degli utenti in Azure |
|:---:|:--- |
| Non aggiunto |In questo caso, nessun dominio personalizzato per contoso.com è stato aggiunto nella directory di Azure AD hello. Gli utenti che dispongono di UPN locale con il suffisso hello @contoso.com non sarà in grado di toouse loro toosign UPN locale in tooAzure. Invece hanno toouse un nuovo nome UPN che ha fornito toothem da Azure AD mediante l'aggiunta di suffisso hello per directory di Azure AD predefinito hello. Ad esempio, se si esegue la sincronizzazione utenti toohello Azure Active directory azurecontoso.onmicrosoft.com, quindi hello utente locale user@contoso.com verrà assegnato un UPN di user@azurecontoso.onmicrosoft.com. |
| Non verificato |In questo caso, è necessario contoso.com un dominio personalizzato che viene aggiunto nella directory hello Azure AD. ma non è ancora verificato. Se procedere con la sincronizzazione di utenti senza verifica dominio hello, quindi gli utenti di hello verrà assegnato un UPN di nuovo da Azure AD, esattamente come in uno scenario "Non aggiungere" hello. |
| Verified |In questo caso, si dispone di un dominio personalizzato contoso.com già aggiunto e verificato in Azure AD per hello suffisso UPN. Gli utenti sarà in grado di toouse nome entità utente locale, ad esempio user@contoso.com, toosign in tooAzure al termine della sincronizzazione di cui si tooAzure Active Directory. |

###### <a name="ad-fs-federation"></a>Federazione AD FS
È possibile creare una federazione con valore predefinito di hello. dominio onmicrosoft.com in Azure AD o a un dominio personalizzato non verificato in Azure AD. Quando si eseguono procedura guidata di hello Azure AD Connect, se si seleziona un dominio non verificato di toocreate una federazione con, Azure AD Connect richiede quindi è necessario hello registra toobe creato in cui il DNS è ospitato per il dominio hello. Per ulteriori informazioni, vedere [dominio hello Azure AD verifica selezionato per la federazione](active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation).

Se è selezionata l'opzione di accesso utente hello **federazione con ADFS**, quindi è necessario disporre di un dominio personalizzato di toocontinue creazione di una federazione in Azure AD. Per la discussione, ciò significa che dovremmo già contoso.com un dominio personalizzato aggiunto nella directory hello Azure AD.

| Stato | Effetto sull'esperienza di accesso degli utenti Azure hello |
|:---:|:--- |
| Non aggiunto |In questo caso, Azure AD Connect non trova un dominio personalizzato corrispondente per contoso.com suffisso UPN di hello nella directory di Azure AD hello. Se è necessario toosign gli utenti in tramite AD FS con il relativo UPN locale, è necessario tooadd contoso.com un dominio personalizzato (ad esempio user@contoso.com). |
| Non verificato |In questo caso Azure AD Connect richiederà i dettagli appropriati sul modo in cui si potrà verificare il dominio in una fase successiva. |
| Verified |In questo caso, è possibile procedere con la configurazione di hello senza ulteriori azioni. |

## <a name="changing-hello-user-sign-in-method"></a>Modifica il metodo di accesso utente hello
È possibile modificare il metodo di accesso utente hello da autenticazione pass-through, la sincronizzazione delle password o federazione tramite le attività disponibili in Azure AD Connect dopo la configurazione iniziale di Azure AD Connect hello con la procedura guidata hello hello. Eseguire di nuovo guidata di Azure AD Connect hello e verrà visualizzato un elenco di attività che è possibile eseguire. Selezionare **modificare account utente** elenco hello delle attività.

![Cambia l'accesso utente](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

Nella pagina successiva di hello, verrà chiesto credenziali hello tooprovide per Azure AD.

![Connettersi AD tooAzure](./media/active-directory-aadconnect-user-signin/changeusersignin2.png)

In hello **account utente** selezionare hello desiderato accesso dell'utente.

![Connettersi AD tooAzure](./media/active-directory-aadconnect-user-signin/changeusersignin2a.png)

> [!NOTE]
> Se si desidera apportare solo una sincronizzazione toopassword commutatore temporaneo, quindi selezionare hello **non vengono convertiti gli account utente** casella di controllo. Non si seleziona opzione hello convertirà toofederated ogni utente e può richiedere diverse ore.
>
>

## <a name="next-steps"></a>Passaggi successivi
- Altre informazioni sull'[integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
- Per altre informazioni, vedere [Concetti relativi alla progettazione per Azure AD Connect](active-directory-aadconnect-design-concepts.md).
