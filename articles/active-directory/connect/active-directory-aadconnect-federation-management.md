---
title: Directory Federation Services aaaActive gestione e la personalizzazione con Azure AD Connect | Documenti Microsoft
description: Gestione di AD FS con Azure AD Connect e personalizzazione dell'esperienza utente di accesso ad AD FS con Azure AD Connect e PowerShell.
keywords: AD FS, ADFS, gestione di AD FS, AAD Connect, Connect, accesso, personalizzazione di AD FS, ripristino trust, O365, federazione, relying party
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 361a2bfd6d7a6993dbe773d6ea039ad1afc6346a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a>Gestire e personalizzare Active Directory Federation Services con Azure AD Connect
Questo articolo viene descritto come toomanage e personalizzare Active Directory Federation Services (ADFS) con Connect di Azure Active Directory (Azure AD). Include inoltre altre attività comuni di ADFS che toodo potrebbe essere necessario per completare la configurazione di una farm di ADFS.

| Argomento | Contenuto |
|:--- |:--- |
| **Gestire AD FS** | |
| [Ripristino hello trust](#repairthetrust) |Federazione hello toorepair come attendibile con Office 365. |
| [Attuare la federazione con Azure AD mediante l'ID di accesso alternativo ](#alternateid) | Configurazione della federazione usando l'ID di accesso alternativo  |
| [Aggiungere un server AD FS](#addadfsserver) |Come tooexpand ADFS farm con un server AD FS aggiuntivo. |
| [Aggiungere un server proxy applicazione Web AD FS](#addwapserver) |La modalità della farm con un server Proxy applicazione Web (WAP) aggiuntivo tooexpand AD FS. |
| [Aggiunta di un dominio federato](#addfeddomain) |Come tooadd un dominio federato. |
| [Aggiorna il certificato SSL hello](active-directory-aadconnectfed-ssl-update.md)| Hello tooupdate SSL come certificato per una farm ADFS. |
| **Personalizzare AD FS** | |
| [Aggiungere un'illustrazione o il logo personalizzato della società](#customlogo) |Come toocustomize AD FS sign-in di pagina con un logo della società e l'illustrazione. |
| [Aggiungere una descrizione di accesso](#addsignindescription) |Tooadd un Accedi alla pagina come descrizione. |
| [Modificare le regole attestazioni per AD FS](#modclaims) |Toomodify AD FS come attestazioni per vari scenari di federazione. |

## <a name="manage-ad-fs"></a>Gestire AD FS
È possibile eseguire varie attività AD FS correlati in Azure AD Connect, con un intervento minimo dell'utente tramite la procedura guidata di hello Azure AD Connect. Dopo aver completato l'installazione di Azure AD Connect dalla procedura guidata hello in esecuzione, è possibile eseguire la procedura guidata hello nuovamente tooperform altre attività.

## Ripristino hello trust<a name=repairthetrust></a>
È possibile utilizzare Azure AD Connect toocheck hello stato di integrità corrente di AD FS hello e trust di Azure AD e intraprendere le azioni appropriate toorepair hello trust. Seguire questi passaggi toorepair di Azure Active Directory e ADFS attendibile.

1. Selezionare **AAD di riparazione e considerare attendibile ADFS** dall'elenco di hello di attività aggiuntive.
   ![Ripristino del trust di AAD e AD FS](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)

2. In hello **connettersi AD tooAzure** pagina, fornire le credenziali di amministratore globale per Azure AD e fare clic su **Avanti**.
   ![Connettersi AD tooAzure](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)

3. In hello **credenziali di accesso remoto** pagina, immettere le credenziali di hello hello amministratore di dominio.

   ![Credenziali di accesso remoto](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    Dopo aver fatto clic su **Avanti**, Azure AD Connect verifica l'integrità del certificato e visualizza gli eventuali problemi.

    ![Stato dei certificati](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    Hello **tooconfigure pronto** pagina Mostra hello elenco di azioni che saranno eseguite trust hello toorepair.

    ![Tooconfigure pronto](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. Fare clic su **installare** trust hello toorepair.

> [!NOTE]
> Azure AD Connect può solo ripristinare o eseguire azioni sui certificati autofirmati. I certificati di terze parti non possono essere ripristinati da Azure AD Connect.

## Attuare la federazione con Azure AD mediante AlternateID <a name=alternateid></a>
È consigliabile che hello Name(UPN) dell'entità utente in locale e cloud hello Nome entità utente vengono mantenute hello stesso. Se hello locale UPN viene utilizzato un dominio non instradabile (ad esempio, Contoso. Local) o non può essere modificato a causa di dipendenze dell'applicazione toolocal, è consigliabile impostare l'ID di accesso alternativo. ID di accesso alternativo consente un'esperienza di accesso in cui gli utenti possono accedere con un attributo diverso dal relativo UPN, ad esempio mail tooconfigure. scelta di Hello per nome dell'entità utente in Azure AD Connect attributo userPrincipalName toohello di valori predefiniti in Active Directory. Se si sceglie qualsiasi altro attributo per il nome dell'entità utente e si sta eseguendo la federazione con AD FS, Azure AD Connect configurerà AD FS per l’ID di accesso alternativo. Di seguito è riportato un esempio della scelta di un attributo diverso per il nome dell'entità utente:

![Selezione dell’attributo ID alternativo](media/active-directory-aadconnect-federation-management/attributeselection.png)

La configurazione dell’ID di accesso alternativo per AD FS consiste in due passaggi principali:
1. **Configurare il set corretto di hello di attestazioni di rilascio**: regole attestazione di rilascio hello nel componente hello Azure AD attendibilità attributo UserPrincipalName di hello selezionato toouse modificato come hello ID alternativo dell'utente hello.
2. **Abilitare l'ID di accesso alternativo nella configurazione di ADFS hello**: la configurazione di ADFS hello Active Directory viene aggiornata in modo che ADFS è possibile cercare gli utenti nelle foreste di hello appropriata utilizzando ID alternativo di hello. Questa configurazione è supportata per AD FS in Windows Server 2012 R2 (con KB2919355) o versioni successive. Se hello AD FS Server 2012 R2, Azure AD Connect Verifica presenza di hello di hello necessario KB. Se hello KB non viene rilevato, un messaggio di avviso verrà visualizzato al termine della configurazione, come illustrato di seguito:

    ![Avviso per KB mancante su 2012 R2](media/active-directory-aadconnect-federation-management/kbwarning.png)

    configurazione di hello toorectify in caso di KB mancante, installare hello necessario [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) e quindi ripristinare hello trust utilizzando [ripristinare AAD e Trust di AD FS](#repairthetrust).

> [!NOTE]
> Per ulteriori informazioni su toomanually alternateID e passaggi di configurazione, leggere [la configurazione di ID di accesso alternativo](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)

## Aggiungere un server AD FS <a name=addadfsserver></a>

> [!NOTE]
> server AD FS tooadd, Azure AD Connect richiede un certificato PFX hello. Pertanto, è possibile eseguire questa operazione solo se è configurato farm ADFS hello Active Directory con Azure AD Connect.

1. Selezionare **Distribuzione di un server federativo aggiuntivo** e fare clic su **Avanti**.

   ![Server federativo aggiuntivo](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. In hello **connettersi AD tooAzure** pagina, immettere le credenziali di amministratore globale per Azure AD e fare clic su **Avanti**.

   ![Connettersi AD tooAzure](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. Fornire le credenziali di amministratore di dominio hello.

   ![Credenziali dell'amministratore di dominio](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. Azure AD Connect richiede password hello del file PFX hello fornito dall'utente durante la configurazione della nuova farm ADFS con Azure AD Connect. Fare clic su **immettere la Password** password hello tooprovide per il file PFX hello.

   ![Password certificato](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![Specificare il certificato SSL](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. In hello **server ADFS** pagina, immettere il nome di server hello o toobe di indirizzo IP aggiunto farm ADFS toohello Active Directory.

   ![Server AD FS](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. Fare clic su **Avanti**e passare a hello finale **configura** pagina. Al termine dell'aggiunta di farm di ADFS hello server toohello AD Azure AD Connect, si avrà la connettività di hello opzione tooverify hello.

   ![Tooconfigure pronto](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Installazione completata](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## Aggiungere un server WAP AD FS <a name=addwapserver></a>

> [!NOTE]
> tooadd un server WAP, Azure AD Connect richiede un certificato PFX hello. Pertanto, è possibile eseguire questa operazione solo se è configurato farm ADFS hello Active Directory con Azure AD Connect.

1. Selezionare **distribuire Proxy applicazione Web** dall'elenco di hello delle attività disponibili.

   ![Distribuire il Proxy applicazione Web](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. Fornire le credenziali di amministratore globale di Azure hello.

   ![Connettersi AD tooAzure](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. In hello **certificato SSL specificare** pagina, fornire la password di hello per il file PFX hello fornito con la farm di hello AD FS è stato configurato con Azure AD Connect.
   ![Password certificato](media/active-directory-aadconnect-federation-management/WapServer3.PNG)

    ![Specificare il certificato SSL](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. Aggiungere hello server toobe aggiunto come server WAP. Poiché il server WAP hello potrebbe non essere toohello aggiunti a un dominio, la procedura guidata hello richiede server toohello credenziali amministrative da aggiungere.

   ![Credenziali amministrative del server](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. In hello **credenziali trust Proxy** fornire proxy hello di credenziali amministrative tooconfigure trust e accesso hello server primario nella farm ADFS hello.

   ![Credenziali di attendibilità del proxy](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. In hello **tooconfigure pronto** pagina, la procedura guidata hello Mostra elenco hello di azioni che verranno eseguite.

   ![Tooconfigure pronto](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. Fare clic su **installare** configurazione hello toofinish. Al termine della configurazione di hello, hello guidata garantisce hello tooverify opzione hello server toohello di connettività. Fare clic su **verificare** toocheck connettività.

   ![Installazione completata](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## Aggiunta di un dominio federato <a name=addfeddomain></a>

È facile tooadd toobe un dominio federato con Azure AD mediante Azure AD Connect. Azure AD Connect aggiunge hello del dominio per la federazione e modifica attestazioni hello regole toocorrectly riflettere emittente hello quando si dispone di più domini federati con Azure AD.

1. tooadd un dominio federato, attività hello selezionare **aggiungere un altro dominio di Azure AD**.

   ![Dominio di Azure AD aggiuntivo](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. Nella pagina successiva di hello della procedura guidata hello, fornire le credenziali di amministratore globale di hello per Azure AD.

   ![Connettersi AD tooAzure](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. In hello **credenziali di accesso remoto** pagina, fornire le credenziali di amministratore di dominio hello.

   ![Credenziali di accesso remoto](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. Nella pagina successiva di hello, la procedura guidata hello fornisce un elenco di domini di Azure AD che si può creare la directory locale con una federazione. Scegliere il dominio hello dall'elenco di hello.

   ![Dominio di Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    Dopo aver scelto il dominio di hello, guidata hello offre le informazioni corrette su altre azioni che hello guidata verrà richiedere e hello impatto della configurazione di hello. In alcuni casi, se si seleziona un dominio che non è ancora verificato in Azure AD, la procedura guidata hello vengono fornite informazioni toohelp è verificare il dominio hello. Vedere [aggiungere tooAzure di nome Active Directory del dominio personalizzato](../active-directory-add-domain.md) per altri dettagli.

5. Fare clic su **Avanti**. Hello **tooconfigure pronto** pagina Mostra elenco hello di azioni che verranno eseguite di Azure AD Connect. Fare clic su **installare** configurazione hello toofinish.

   ![Tooconfigure pronto](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> Aggiungere utenti da hello dominio federato deve essere sincronizzato prima saranno in grado di toologin tooAzure Active Directory.

## <a name="ad-fs-customization"></a>Personalizzazione di AD FS
Hello sezioni seguenti forniscono informazioni dettagliate su alcune delle attività comuni di hello che potrebbe essere tooperform quando si personalizza la pagina di accesso di ADFS.

## Aggiungere un'illustrazione o il logo personalizzato della società <a name=customlogo></a>
logo di hello toochange della società hello che viene visualizzato in hello **Accedi** pagina, utilizzare i seguenti cmdlet di Windows PowerShell e la sintassi hello.

> [!NOTE]
> Hello consigliata dimensioni per il logo hello sono 260 x 35 96 DPI con dimensioni non superiori a 10 KB.

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> Hello *TargetName* parametro è obbligatorio. tema predefinito Hello che viene rilasciata con AD FS è denominato Default.

## Aggiungere una descrizione di accesso <a name=addsignindescription></a>
tooadd un toohello descrizione nella pagina di accesso **nella pagina di accesso**, utilizzare hello segue sintassi e i cmdlet di Windows PowerShell.

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in tooContoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## Modificare le regole attestazioni per AD FS <a name=modclaims></a>
ADFS supporta un linguaggio di attestazione completo che è possibile utilizzare regole attestazione toocreate personalizzato. Per ulteriori informazioni, vedere [hello ruolo del linguaggio delle regole attestazioni hello](https://technet.microsoft.com/library/dd807118.aspx).

Hello nelle sezioni seguenti viene illustrato come scrivere regole personalizzate per alcuni scenari correlati tooAzure Active Directory e la federazione ADFS.

### <a name="immutable-id-conditional-on-a-value-being-present-in-hello-attribute"></a>ID non modificabile condizionale su un valore presente nell'attributo hello
Azure AD Connect consente di specificare toobe un attributo utilizzato come un ancoraggio di origine quando gli oggetti sono sincronizzati tooAzure Active Directory. Se il valore di hello nell'attributo personalizzato di hello non è vuoto, è possibile tooissue un'attestazione ID non modificabile.

Ad esempio, è possibile selezionare **ms-ds-consistencyguid** attributo hello di ancoraggio di origine hello e problema **ImmutableID** come **ms-ds-consistencyguid** in case hello attributo ha un valore su di essa. Se è presente alcun valore rispetto a attributo hello, emettere **objectGuid** come hello ID non modificabile. È possibile costruire il set di hello di regole attestazioni personalizzate come descritto nella seguente sezione hello.

**Regola 1: Attributi della query**

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

In questa regola, si sta eseguendo la query valori hello di **ms-ds-consistencyguid** e **objectGuid** per utente hello da Active Directory. Modificare il nome hello archivio nome tooan archivio appropriato nella distribuzione di ADFS. Inoltre modificare il tipo hello attestazioni tipo tooa attestazioni appropriate per la federazione, come definito per **objectGuid** e **ms-ds-consistencyguid**.

Inoltre, tramite **aggiungere** e non **problema**, evitare di aggiungere un problema in uscita per l'entità hello e può utilizzare valori hello come valori intermedi. Attestazione hello in una regola successiva vengono emessi dopo aver stabilito quali toouse valore come hello ID non modificabile.

**Regola 2: Verificare che ms-ds-consistencyguid esista per l'utente hello**

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

Questa regola definisce un flag temporaneo denominato **idflag** impostato troppo**useguid** se è presente alcun **ms-ds-consistencyguid** popolata per utente hello. logica di Hello protetti da questo è il fatto di hello che ADFS non consentono le attestazioni vuote. Pertanto quando si aggiungono attestazioni http://contoso.com/ws/2016/02/identity/claims/objectguid e http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid nella regola 1, si otterrà un **msdsconsistencyguid** attestazione solo se il valore di Hello viene popolato per utente hello. Se non è popolato, AD FS rileva che avrà un valore vuoto e lo rimuove immediatamente. Tutti gli oggetti avranno **objectGuid**, quindi l'attestazione sarà sempre presente dopo l'esecuzione della regola 1.

**Regola 3: Rilasciare ms-ds-consistencyguid come ID non modificabile se presente**

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

Si tratta di un controllo **Exist** implicito. Se il valore di hello di attestazione hello esiste, quindi rilasciare che come non modificabile hello ID. esempio precedente Hello utilizza hello **nameidentifier** attestazione. È necessario toochange questo tipo di attestazione appropriate toohello per l'ID non modificabile hello nell'ambiente in uso.

**Regola 4: Rilasciare objectGuid come ID non modificabile se ms-ds-consistencyGuid non è presente**

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

In questa regola, si stia controllando semplicemente flag temporaneo hello **idflag**. È possibile decidere se tooissue hello attestazione in base al relativo valore.

> [!NOTE]
> sequenza di Hello di queste regole è importante.

### <a name="sso-with-a-subdomain-upn"></a>SSO con un UPN di sottodominio
È possibile aggiungere più toobe dominio federato con Azure AD Connect, come descritto in [aggiungere un nuovo dominio federato](active-directory-aadconnect-federation-management.md#addfeddomain). Attestazione del nome principale (UPN) utente hello è necessario modificare in modo che hello ID autorità di certificazione corrisponde dominio radice toohello e non a sottodominio hello, perché il dominio federato radice hello riguarda anche figlio hello.

Per impostazione predefinita, hello regola attestazione per l'ID viene impostato come autorità di certificazione:

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Attestazione predefinita per l'ID autorità di certificazione](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

regola predefinita Hello semplicemente accetta suffisso UPN hello e viene utilizzato in hello attestazione dell'ID dell'autorità di certificazione. Ad esempio, John è un utente in sub.contoso.com e contoso.com è federato con Azure AD. Immette John john@sub.contoso.com come hello nome utente durante la firma in tooAzure Active Directory. regola attestazione ID Hello predefinita dell'autorità di certificazione in ADFS viene gestito da hello seguente modo:

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

**Valore dell'attestazione:** http://sub.contoso.com/adfs/services/trust/

toohave solo hello dominio radice dell'autorità di certificazione hello il valore dell'attestazione, modificare hello attestazione regola toomatch hello seguenti:

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni sulle [opzioni di accesso utente](active-directory-aadconnect-user-signin.md).
