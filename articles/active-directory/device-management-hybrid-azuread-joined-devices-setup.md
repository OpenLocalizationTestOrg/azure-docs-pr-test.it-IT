---
title: dispositivi aggiunti a un aaaHow tooconfigure ibrida Azure Active Directory | Documenti Microsoft
description: "Informazioni su modalità ibrida tooconfigure Azure Active Directory unite in join i dispositivi."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: f97ea436eca2833d8a9843acd19e5c633bc0fc07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-hybrid-azure-active-directory-joined-devices"></a>Modalità ibrida tooconfigure Azure Active Directory unite in join i dispositivi

Tramite la gestione dei dispositivi in Azure Active Directory (Azure AD) è possibile garantire che gli utenti accedano alle risorse da dispositivi che soddisfano gli standard di sicurezza e conformità. Per ulteriori informazioni, vedere [gestione toodevice introduzione in Azure Active Directory](device-management-introduction.md).

Se si dispone di un ambiente Active Directory locale e si desidera toojoin il tooAzure dispositivi appartenenti a un dominio Active Directory, è possibile eseguire tramite la configurazione di dispositivi AD Azure unita in join ibrido. Hello argomento vengono fornite hello relativi passaggi. 


## <a name="before-you-begin"></a>Prima di iniziare

Prima di iniziare la configurazione ibrida di Azure AD i dispositivi appartenenti nell'ambiente in uso, è consigliabile acquisire familiarità con i vincoli di hello e scenari di hello è supportato.  

migliorare la leggibilità hello tooimprove delle descrizioni di hello, in questo argomento utilizza hello seguenti termini: 

- **Dispositivi di Windows correnti** -questo termine si riferisce unita toodomain dispositivi che eseguono Windows 10 o Windows Server 2016.
- **Dispositivi di livello inferiore Windows** -questo termine si riferisce tooall **supportati** dispositivi Windows aggiunti a un dominio che non sono in esecuzione Windows 10 o Windows Server 2016.  


### <a name="windows-current-devices"></a>Dispositivi Windows correnti

- Per i dispositivi che eseguono il sistema operativo desktop di hello Windows, è consigliabile utilizzare aggiornamento Aniversary di Windows 10 (versione 1607) o versione successiva. 
- registrazione di dispositivi corrente di Windows Hello **è** supportato in ambienti non federati, ad esempio configurazioni di sincronizzazione di hash di password.  


### <a name="windows-down-level-devices"></a>Dispositivi Windows di livello inferiore

- è supportato i seguenti dispositivi di livello inferiore di Windows Hello:
    - Windows 8.1
    - Windows 7
    - Windows Server 2012 R2
    - Windows Server 2012
    - Windows Server 2008 R2
- registrazione dei dispositivi legacy di Windows Hello **è** supportato in ambienti non federato tramite l'accesso Single Sign On [Azure Active Directory trasparente Single Sign-On](https://aka.ms/hybrid/sso).
- registrazione dei dispositivi legacy di Windows Hello **non** supportati per i dispositivi con i profili. In caso di roaming delle impostazioni o dei profili, usare Windows 10.



## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare l'attivazione ibrida Azure AD aggiunti nei dispositivi dell'organizzazione, è necessario assicurarsi che si esegue una versione aggiornata di Azure AD toomake connettersi.

Azure AD Connect:

- Consente di mantenere associazione hello tra account di computer hello in locale di Active Directory (AD) e oggetto dispositivo hello in Azure AD. 
- Abilita altre funzionalità correlate al dispositivo come Windows Hello for Business.



## <a name="configuration-steps"></a>Procedura di configurazione

È possibile configurare dispositivi aggiunti all'identità ibrida di Azure AD per diversi tipi di piattaforme di dispositivi Windows. In questo argomento include i passaggi di hello necessarie per tutti gli scenari di configurazione tipica.  

Utilizzare hello tabella tooget una panoramica dei passaggi di hello necessari per lo scenario seguente:  



| Passi                                      | Dispositivi Windows correnti e sincronizzazione dell'hash delle password | Dispositivi Windows correnti e federazione | Dispositivi Windows di livello inferiore |
| :--                                        | :-:                                    | :-:                            | :-:                |
| Passaggio 1: Configurare il punto di connessione del servizio | ![Controllo][1]                            | ![Controllo][1]                    | ![Controllo][1]        |
| Passaggio 2: Configurare il rilascio delle attestazioni           |                                        | ![Controllo][1]                    | ![Controllo][1]        |
| Passaggio 3: Abilitare dispositivi non Windows 10      |                                        |                                | ![Controllo][1]        |
| Passaggio 4: Controllare la distribuzione e l'implementazione     | ![Controllo][1]                            | ![Controllo][1]                    | ![Controllo][1]        |
| Passaggio 5: Verificare i dispositivi aggiunti          | ![Controllo][1]                            | ![Controllo][1]                    | ![Controllo][1]        |



## <a name="step-1-configure-service-connection-point"></a>Passaggio 1: Configurare il punto di connessione del servizio

oggetto di Hello service connection point (SCP) viene utilizzato dai dispositivi durante la registrazione di hello toodiscover informazioni sul tenant di Azure AD. In locale Active Directory (AD), l'oggetto di hello SCP per i dispositivi di Azure AD unita in join ibrido hello deve esistere nella partizione denominazione contesto hello configurazione di foresta hello del computer. Esiste un solo contesto dei nomi di configurazione per foresta. In una configurazione di Active Directory a più foreste, punto di connessione del servizio hello deve esistere in tutte le foreste contenente i computer appartenenti a un dominio.

È possibile utilizzare hello [ **Get ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello contesto dei nomi configurazione della foresta.  

Per una foresta con nome di dominio Active Directory hello *fabrikam.com*, contesto dei nomi di configurazione hello è:

`CN=Configuration,DC=fabrikam,DC=com`

In una foresta, l'oggetto hello SCP per hello la registrazione automatica dei dispositivi appartenenti a un dominio si trova in:  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

A seconda di come è stato distribuito Azure AD Connect, oggetto SCP hello potrebbe sono già stata configurata.
È possibile verificare l'esistenza di hello dell'oggetto hello e recuperare i valori di individuazione di hello mediante hello lo script di Windows PowerShell seguente: 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

Hello **$scp. Parole chiave** output mostra le informazioni sul tenant hello Azure AD, ad esempio:

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

Se il punto di connessione servizio hello non esiste, è possibile creare eseguendo hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet nel server di Azure AD Connect. Credenziali di amministratore dell'organizzazione è necessario toorun questo cmdlet.  
cmdlet di Hello:

- Crea punto di connessione del servizio hello in Azure AD Connect è connesso alla foresta di Active Directory hello. 
- È necessario hello toospecify `AdConnectorAccount` parametro. Si tratta di account hello è configurato come account connettore di Azure AD connect di Active Directory. 


Hello script riportato di seguito viene illustrato un esempio per l'utilizzo di cmdlet hello. In questo script `$aadAdminCred = Get-Credential` richiede tootype un nome utente. È necessario tooprovide hello utente nome nel formato di hello user principal name (UPN) (`user@example.com`). 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

Hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:

- Usa il modulo Active Directory PowerShell hello, che si basa su servizi Web Active Directory in esecuzione in un controller di dominio. Il servizio Servizi Web Active Directory è supportato nei controller di dominio che eseguono Windows Server 2008 R2 e versioni successive.
- È supportato solo da hello **MSOnline PowerShell versione del modulo 1.1.166.0**. toodownload questo modulo, utilizzare questo [collegamento](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).   

Per i controller di dominio che eseguono Windows Server 2008 o versioni precedenti, utilizzare script hello seguente punto di connessione del servizio toocreate hello.

In una configurazione a più foreste, è consigliabile utilizzare hello script toocreate hello servizio punto di connessione in ogni foresta in cui sono presenti computer seguenti:
 
    $verifiedDomain = "contoso.com"    # Replace this with any of your verified domain names in Azure AD
    $tenantID = "72f988bf-86f1-41af-91ab-2d7cd011db47"    # Replace this with you tenant ID
    $configNC = "CN=Configuration,DC=corp,DC=contoso,DC=com"    # Replace this with your AD configuration naming context

    $de = New-Object System.DirectoryServices.DirectoryEntry
    $de.Path = "LDAP://CN=Services," + $configNC

    $deDRC = $de.Children.Add("CN=Device Registration Configuration", "container")
    $deDRC.CommitChanges()

    $deSCP = $deDRC.Children.Add("CN=62a0ff2e-97b9-4513-943f-0d221bd30080", "serviceConnectionPoint")
    $deSCP.Properties["keywords"].Add("azureADName:" + $verifiedDomain)
    $deSCP.Properties["keywords"].Add("azureADId:" + $tenantID)

    $deSCP.CommitChanges()


## <a name="step-2-setup-issuance-of-claims"></a>Passaggio 2: Configurare il rilascio delle attestazioni

Di Azure federato configurazione di Active Directory, i dispositivi si basano su Active Directory Federation Services (ADFS) o un'entità 3 federation service tooauthenticate tooAzure AD in locale. I dispositivi si autenticano tooget un tooregister del token di accesso su hello Azure Active Directory Device Registration Service (Azure DRS).

Dispositivi correnti l'autenticazione tramite autenticazione integrata di Windows tooan active endpoint WS-Trust (versione 1.3 o 2005) ospitato nel servizio federativo di hello locale di Windows.

> [!NOTE]
> Quando si usa AD FS, è necessario abilitare **adfs/services/trust/13/windowstransport** o **adfs/services/trust/2005/windowstransport**. Se si utilizza il Proxy di autenticazione Web hello, assicurarsi anche che questo endpoint verrà pubblicato tramite proxy hello. È possibile vedere quali gli endpoint sono abilitati tramite la console di gestione AD FS hello in **servizio > endpoint**.
>
>Se non si dispone di AD FS come il servizio federativo locale, istruzioni hello di toomake del fornitore che supportano WS-Trust 1.3 o gli endpoint 2005 e che questi sono pubblicati tramite hello file di scambio di metadati (MEX).

Hello attestazioni riportate di seguito devono essere presente nel token hello ricevuti dal servizio di Azure DRS per toocomplete registrazione dispositivo. Azure DRS creerà un oggetto dispositivo in Azure AD con alcune di queste informazioni che viene quindi utilizzate dall'oggetto dispositivo di Azure AD Connect tooassociate hello appena creato con hello computer account locale.

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

Se si dispone di più di un nome di dominio verificato, è necessario hello tooprovide attestazioni per i computer seguenti:

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

Se già si emette un'attestazione ImmutableID (ad esempio, un ID di accesso alternativo) è necessario tooprovide un'attestazione corrispondente per i computer:

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

In hello le sezioni seguenti, reperire informazioni relative a:
 
- i valori Hello deve avere ogni attestazione
- Come si presenta una definizione in AD FS

definizione di Hello consente tooverify se sono presenti valori hello o se è necessario toocreate li.

> [!NOTE]
> Se non si utilizza ADFS per il server federativo locale, seguire queste attestazioni tooissue del fornitore istruzioni toocreate hello configurazione appropriata.

### <a name="issue-account-type-claim"></a>Rilasciare l'attestazione del tipo di account

**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-Questa attestazione deve contenere un valore di **dispositivo**, che identifica il dispositivo hello come un computer aggiunto al dominio. In AD FS, è possibile aggiungere una regola di trasformazione rilascio simile alla seguente:

    @RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a>Problema objectGUID di hello computer account locale

**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-Questa attestazione deve contenere hello **objectGUID** valore hello locale account computer. In AD FS, è possibile aggiungere una regola di trasformazione rilascio simile alla seguente:

    @RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a>Problema objectSID hello computer account locale

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-Questa attestazione deve contenere hello hello **objectSid** valore hello locale account computer. In AD FS, è possibile aggiungere una regola di trasformazione rilascio simile alla seguente:

    @RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a>Rilasciare l'attestazione issuerID per il computer in presenza di più nomi di dominio verificati in Azure AD

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-Questa attestazione deve contenere hello identificatore URI (Uniform Resource) di uno qualsiasi dei hello verificare i nomi di dominio che si connettono hello locale federation service (AD FS o parte 3) il rilascio hello del token. In ADFS, è possibile aggiungere regole di trasformazione rilascio come quelli hello seguente in un ordine specifico dopo hello quelli precedenti. Si noti che una regola tooexplicitly problema hello regola per gli utenti è necessario. In regole hello indicate di seguito, viene aggiunto una prima regola che identifica l'utente e l'autenticazione del computer.

    @RuleName = "Issue account type with hello value User when its not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://<verified-domain-name>/adfs/services/trust/"
    );


Nell'attestazione hello precedente,

- `$<domain>`URL del servizio hello AD FS
- `<verified-domain-name>`è un segnaposto, è necessario tooreplace con uno dei nomi di dominio verificato in Azure AD



Per ulteriori informazioni sui nomi di dominio verificato, vedere [aggiungere tooAzure di nome Active Directory un dominio personalizzato](active-directory-add-domain.md).  
tooget un elenco dei domini aziendali verificati, è possibile utilizzare hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet. 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a>Rilasciare l'attestazione ImmutableID per il computer quando ne esiste una per gli utenti (ad esempio, è impostato un ID di accesso alternativo)

**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**: questa attestazione deve contenere un valore valido per i computer. In AD FS, è possibile creare una regola di trasformazione rilascio come segue:

    @RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a>Regole di trasformazione di helper script toocreate hello AD FS rilascio

Hello lo script seguente consente di creazione hello dell'emissione hello trasformare le regole descritte sopra.

    $multipleVerifiedDomainNames = $false
    $immutableIDAlreadyIssuedforUsers = $false
    $oneOfVerifiedDomainNames = 'example.com'   # Replace example.com with one of your verified domains
    
    $rule1 = '@RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );'

    $rule2 = '@RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'

    $rule3 = '@RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);'

    $rule4 = ''
    if ($multipleVerifiedDomainNames -eq $true) {
    $rule4 = '@RuleName = "Issue account type with hello value User when it is not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://' + $oneOfVerifiedDomainNames + '/adfs/services/trust/"
    );'
    }

    $rule5 = ''
    if ($immutableIDAlreadyIssuedforUsers -eq $true) {
    $rule5 = '@RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'
    }

    $existingRules = (Get-ADFSRelyingPartyTrust -Identifier urn:federation:MicrosoftOnline).IssuanceTransformRules 

    $updatedRules = $existingRules + $rule1 + $rule2 + $rule3 + $rule4 + $rule5

    $crSet = New-ADFSClaimRuleSet -ClaimRule $updatedRules 

    Set-AdfsRelyingPartyTrust -TargetIdentifier urn:federation:MicrosoftOnline -IssuanceTransformRules $crSet.ClaimRulesString 

### <a name="remarks"></a>Osservazioni 

- Questo script aggiunge hello toohello esistente regole. Script hello non vengono eseguite due volte perché hello set di regole è necessario aggiungere due volte. Verificare che nessuna regola corrispondente esistenza per queste attestazioni (condizioni hello corrispondente) prima di eseguire script hello nuovamente.

- Se si dispongono di più nomi di dominio verificato (come mostrato nel portale di Azure AD hello o tramite il cmdlet Get-MsolDomains hello), impostare il valore di hello di **$multipleVerifiedDomainNames** in hello di script troppo**$true**. Assicurarsi anche di rimuovere qualsiasi attestazione issuerid esistente che potrebbe essere stata creata da Azure AD Connect o con altri mezzi. Di seguito è riportato un esempio di questa regola:


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- Se è già stata eseguita un' **ImmutableID** attestazioni per gli account utente, impostare il valore di hello di **$immutableIDAlreadyIssuedforUsers** in hello di script troppo**$true**.

## <a name="step-3-enable-windows-down-level-devices"></a>Passaggio 3: Abilitare dispositivi Windows di livello inferiore

Se alcuni dei dispositivi aggiunti a un dominio sono dispositivi Windows di livello inferiore, è necessario eseguire queste operazioni:

- Impostare un criterio in Azure AD tooenable dispositivi tooregister utenti.
 
- Configurare il toosupport di attestazioni locale federation service tooissue **l'autenticazione integrata di Windows (IWA)** per la registrazione del dispositivo.
 
- Aggiungere hello Azure AD dispositivo autenticazione endpoint toohello locale nelle zone Intranet tooavoid certificato richiesto per l'autenticazione dispositivo hello.

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a>Impostare i criteri in Azure AD tooenable dispositivi tooregister utenti

tooregister dispositivi di livello inferiore di Windows, è necessario che tale hello impostazione utenti tooallow tooregister dispositivi in Azure AD sia impostato toomake. Nel portale di Azure hello, è possibile trovare questa impostazione in:

`Azure Active Directory > Users and groups > Device settings`
    
Hello criterio seguente deve essere impostato troppo**tutti**: **gli utenti possono registrare i propri dispositivi con Azure AD**

![Registrare i dispositivi](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a>Configurare il servizio federativo locale 

Il servizio federativo locale deve supportare hello emittente **authenticationmehod** e **wiaormultiauthn** attestazioni durante la ricezione di un tipo di autenticazione richiesta componente toohello Azure Active Directory che contiene un resouce_params parametri con un valore codificato come illustrato qui di seguito:

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

Quando arriva una richiesta di questo tipo, servizio federativo locale di hello deve autenticare l'utente di hello utilizzando l'autenticazione integrata di Windows e al completamento dell'operazione, è necessario emettere hello due attestazioni di seguito:

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

In ADFS, è necessario aggiungere una regola di trasformazione rilascio tale metodo di autenticazione hello passate-through.  

**tooadd questa regola:**

1. Nella console di gestione ADFS hello AD andare troppo`AD FS > Trust Relationships > Relying Party Trusts`.
2. Oggetto di relazione di trust relying party di hello piattaforma delle identità di Microsoft Office 365 e quindi scegliere **Modifica regole attestazione**.
3. In hello **regole di trasformazione rilascio** , selezionare **Aggiungi regola**.
4. In hello **regola attestazione** elenco modello, selezionare **inviare attestazioni mediante una regola personalizzata**.
5. Selezionare **Avanti**.
6. In hello **nome regola attestazione** digitare **Auth Method Claim Rule**.
7. In hello **regola attestazione** casella, hello tipo seguente regola:

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. Nel server federativo, digitare il comando PowerShell hello seguente dopo la sostituzione  **\<RPObjectName\>**  hello relying party nome di oggetto per l'oggetto di relazione di trust AD Azure relying party. Tale oggetto è solitamente denominato **Piattaforma delle identità di Microsoft Office 365**.
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a>Aggiungere zone Intranet locale di hello Azure AD dispositivo autenticazione endpoint toohello

certificato tooavoid richiede quando gli utenti di registrare dispositivi autenticano tooAzure AD è possibile distribuire un hello tooadd di criteri tooyour dispositivi appartenenti a un dominio seguente URL toohello Intranet locale in Internet Explorer:

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a>Passaggio 4: Controllare la distribuzione e l'implementazione

Quando sono stati completati i passaggi di hello necessario, i dispositivi appartenenti a un dominio sono join tooautomatically pronto AD Azure:

- Tutti i dispositivi aggiunti a un dominio che eseguono la versione Aggiornamento dell'anniversario di Windows 10 e Windows Server 2016 vengono registrati automaticamente in Azure AD al riavvio del dispositivo o all'accesso dell'utente. 

- I nuovi dispositivi registrare con Azure AD al dispositivo hello riavvio al termine dell'operazione di aggiunta dominio hello.

- I dispositivi che erano in precedenza Azure AD registrati (ad esempio, per Intune) transizione troppo "*aggiunti a un dominio, AAD registrato*"; tuttavia comporta un tempo per toocomplete questo processo per tutti i dispositivi a causa di toohello normale flusso di attività utente e dominio.

### <a name="remarks"></a>Osservazioni

- È possibile utilizzare un'implementazione di hello toocontrol oggetto Criteri di gruppo registrazione automatica di Windows 10 e i computer appartenenti a un dominio di Windows Server 2016.

- Windows 10 novembre 2015 aggiornamento aggiunge automaticamente con Azure AD **solo** se è impostato l'oggetto Criteri di gruppo di distribuzione hello.

- toorollout dei computer di livello inferiore di Windows, è possibile distribuire un [pacchetto Windows Installer](#windows-installer-packages-for-non-windows-10-computers) toocomputers selezionato.

- Se si esegue il push hello criteri di gruppo oggetto tooWindows 8.1 appartenenti a un dominio, i dispositivi, viene eseguito un tentativo di un join; Tuttavia, è consigliabile utilizzare hello [pacchetto Windows Installer](#windows-installer-packages-for-non-windows-10-computers) toojoin tutti i dispositivi di livello inferiore di Windows. 

### <a name="create-a-group-policy-object"></a>Creare un oggetto Criteri di gruppo 

implementazione di hello toocontrol del computer corrente di Windows, è consigliabile distribuire hello **registrare i computer del dominio come dispositivi** dispositivi toohello di oggetto Criteri di gruppo da tooregister. Ad esempio, è possibile distribuire hello criteri tooan unità organizzativa o gruppo di sicurezza tooa.

**criteri di hello tooset:**

1. Aprire **Server Manager**, quindi andare troppo`Tools > Group Policy Management`.
2. Passare nodo toohello corrispondente toohello dominio in cui si desidera tooactivate la registrazione automatica dei computer di Windows corrente.
3. Fare clic con il pulsante destro del mouse su **Oggetti Criteri di gruppo** e quindi scegliere **Nuovo**.
4. Immettere un nome da assegnare all'oggetto Criteri di gruppo. Ad esempio, *Aggiunta a identità ibrida di Azure AD. 
5. Fare clic su **OK**.
6. Fare clic con il pulsante destro del mouse sul nuovo oggetto Criteri di gruppo e scegliere **Modifica**.
7. Andare troppo**configurazione Computer** > **criteri** > **modelli amministrativi** > **Windows Componenti** > **registrazione dispositivo**. 
8. Fare clic con il pulsante destro del mouse su **Registra i computer aggiunti a un dominio come dispositivi** e quindi scegliere **Modifica**.
   
   > [!NOTE]
   > Questo modello di criteri di gruppo è stato rinominato da versioni precedenti di console Gestione criteri di gruppo hello. Se si utilizza una versione precedente della console hello, andare troppo`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`. 

7. Selezionare **Abilitato** e quindi fare clic su **Applica**.
8. Fare clic su **OK**.
9. Hello collegamento posizione tooa dell'oggetto Criteri di gruppo di propria scelta. Ad esempio, è possibile collegarlo tooa specifica unità organizzativa. È anche possibile collegarlo tooa gruppo di sicurezza specifico di computer che uniscono in join automaticamente con Azure AD. tooset questo criterio per tutti aggiunti a un dominio Windows 10 e Windows Server 2016 i computer nell'organizzazione, l'oggetto toohello dominio del collegamento hello criteri di gruppo.

### <a name="windows-installer-packages-for-non-windows-10-computers"></a>Pacchetti di Windows Installer per i computer non Windows 10

toojoin dominio legacy i computer Windows in un ambiente federato, è possibile scaricare e installare questi pacchetti Windows Installer (MSI) dall'area Download a hello [all'area di lavoro Microsoft per i computer a Windows 10](https://www.microsoft.com/en-us/download/details.aspx?id=53554)pagina.

È possibile distribuire il pacchetto di hello mediante un sistema di distribuzione software come System Center Configuration Manager. pacchetto Hello supporta opzioni di installazione invisibile all'utente standard hello con hello *quiet* parametro. System Center Configuration Manager Current Branch offre ulteriori vantaggi rispetto alle versioni precedenti, ad esempio hello possibilità tootrack completato registrazioni. Per altre informazioni, vedere [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).

programma di installazione Hello crea un'attività pianificata nel sistema hello che viene eseguito nel contesto dell'utente hello. attività Hello viene attivata quando effettua l'accesso utente hello tooWindows. attività Hello aggiunge automaticamente il dispositivo di hello con Azure AD con le credenziali utente hello dopo l'autenticazione utilizzando l'autenticazione integrata di Windows. toosee attività pianificata di hello, nel dispositivo hello, andare troppo**Microsoft** > **all'area di lavoro**, quindi andare libreria utilità di pianificazione toohello.

## <a name="step-5-verify-joined-devices"></a>Passaggio 5: Verificare i dispositivi aggiunti

È possibile controllare i dispositivi aggiunti a un esito positivo nell'organizzazione utilizzando hello [Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [modulo PowerShell di Azure Active Directory](/powershell/azure/install-msonlinev1?view=azureadps-2.0).

output di Hello di questo cmdlet vengono visualizzati i dispositivi registrati e aggiunti con Azure AD. tooget tutti i dispositivi, usare hello **-tutti** parametro, quindi filtro loro utilizzando hello **deviceTrustType** proprietà. I dispositivi aggiunti a un dominio hanno il valore **Domain Joined**.

## <a name="next-steps"></a>Passaggi successivi

* [Gestione toodevice introduzione in Azure Active Directory](device-management-introduction.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
