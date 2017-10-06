---
title: "aaaWhat è Self-Service Signup per Azure? | Microsoft Docs"
description: Un abbonamento self-service di panoramica per Azure, come toomanage hello di iscrizione e come tootake su un nome di dominio DNS.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: b9f01876-29d1-4ab8-8b74-04d43d532f4b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: dbf3b59e3807e98f7bf39f3d5591fcde01667323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-self-service-signup-for-azure"></a>Informazioni sull'iscrizione self-service per Azure
Questo argomento viene illustrato il processo di iscrizione self-service di hello e come tootake su un nome di dominio DNS.  

## <a name="why-use-self-service-signup"></a>Perché usare l'iscrizione self-service?
* Get tooservices di clienti che vogliono più velocemente.
* Creare offerte basate sulla posta elettronica per un servizio.
* Creare flussi di iscrizione basata sulla posta elettronica che rapidamente consentono agli utenti delle identità di toocreate tramite i relativi alias di posta elettronica di lavoro da ricordare.
* Le directory di Azure non gestite possono essere trasformate in directory gestite in un secondo momento ed essere riutilizzate per altri servizi.

## <a name="terms-and-definitions"></a>Termini e definizioni
* **Iscrizione self-service**: si tratta di hello metodo mediante il quale un utente effettua l'iscrizione per un servizio cloud e ha un'identità creata automaticamente in Azure Active Directory (Azure AD) dipende dal relativo dominio di posta elettronica.
* **Directory di Azure non gestiti**: si tratta di hello directory in cui è stata creata tale identità. È una directory priva di un amministratore globale.
* **Utente verificato per la posta elettronica**: si tratta di un tipo di account utente in Azure AD. Un utente che dispone di un'identità creata automaticamente a seguito dell'iscrizione per un'offerta self-service è noto come utente di posta elettronica verificato. Un utente di posta elettronica verificato è un membro regolare di una directory contrassegnata con creationmethod=EmailVerified.

## <a name="user-experience"></a>Esperienza utente
Si supponga, ad esempio, un utente il cui indirizzo di posta elettronica Dan@BellowsCollege.com riceve file riservati tramite posta elettronica. file Hello protetti da Azure Rights Management (Azure RMS). Tuttavia l'organizzazione di Dan, Bellows College, non è iscritta ad Azure RMS né ha distribuito Active Directory RMS. In questo caso, Dan possano iscriversi tooRMS una sottoscrizione gratuita per utenti singoli nei file di ordine tooread hello protetto.

Se Dan utente prima di hello con un indirizzo di posta elettronica da toosign BellowsCollege.com per questa offerta di funzionalità Self-Service, quindi una directory non gestita verrà creata per BellowsCollege.com in Azure AD. Se altri utenti dal dominio BellowsCollege.com hello iscriversi a questa offerta o un'offerta simile di self-service, avranno anche verificato tramite posta elettronica gli account utente creati in hello stesso non gestita directory in Azure.

## <a name="admin-experience"></a>Esperienza amministratore
Un amministratore proprietario nome di dominio DNS hello di una directory di Azure non gestita può assumere o directory hello dopo dimostra la proprietà di tipo merge. Nelle sezioni successive di Hello verrà hello esperienza dell'amministratore in modo più dettagliato, ma di seguito è riportato un riepilogo:

* Quando si acquisisce una directory di Azure non gestita, è semplicemente acquisire messaggio per l'amministratore globale della directory di hello non gestito. In alcuni casi si tratta di un'acquisizione interna.
* Quando si unione una directory di Azure non gestita, aggiungere nome di dominio DNS hello della directory Azure gestito tooyour hello directory non gestito e viene creato un mapping per gli utenti a risorse in modo che gli utenti possono continuare tooaccess servizi senza interruzioni. In alcuni casi si tratta di un'acquisizione esterna.

## <a name="what-gets-created-in-azure-active-directory"></a>Cosa viene creato in Azure Active Directory?
#### <a name="directory"></a>Directory
* Viene creata una directory di Azure Active Directory per il dominio hello, una directory per ogni dominio.
* directory di Azure AD Hello non ha amministratore globale.

#### <a name="users"></a>Utenti
* Per ogni utente che effettua l'iscrizione, viene creato un oggetto utente nella directory di Azure AD hello.
* Ogni oggetto utente viene contrassegnato come esterno.
* il servizio toohello di accesso che sono iscritti a ciascun utente.

### <a name="how-do-i-claim-a-self-service-azure-ad-directory-for-a-domain-i-own"></a>Come si richiede una directory di Azure AD self-service per un dominio di cui si è proprietari?
È possibile richiedere una directory di Azure AD self-service eseguendo la convalida del dominio. Convalida del dominio dimostra dominio hello personalizzate tramite la creazione di record DNS.

Esistono due modi toodo acquisizioni DNS di una directory di Azure AD:

* acquisizione interno (Admin individua una directory di Azure non gestita e vuole tooturn in una directory gestita)
* acquisizione esterno (Admin tenta tooadd una nuovo dominio tootheir gestito directory di Azure)

Potrebbe essere interessante in fase di convalida che si è proprietari di un dominio perché si prevede di mettere in una directory non gestita dopo che un utente ha eseguito abbonamento self-service o aggiunta di una nuovo dominio tooan gestito directory esistente. Ad esempio, si dispone di un dominio denominato contoso.com e si desidera un nuovo dominio denominato contoso.co.uk o contoso.uk tooadd.

## <a name="what-is-domain-takeover"></a>Che cos'è l'acquisizione di dominio?
Questa sezione vengono trattati come toovalidate che si è proprietari di un dominio

### <a name="what-is-domain-validation-and-why-is-it-used"></a>Cos'è la convalida del dominio e perché viene usata?
Nelle operazioni di tooperform ordine in una directory, Azure AD richiede la convalida di proprietà del dominio DNS hello.  Convalida del dominio hello consente si tooclaim hello directory e alzare di livello hello self-service directory tooa gestito directory o directory merge di hello self-service in un oggetto esistente gestiti directory.

## <a name="examples-of-domain-validation"></a>Esempi di convalida del dominio
Esistono due modi toodo acquisizioni DNS di una directory:

* acquisizione interno (ad esempio, un amministratore individua una directory di self-service e non gestita e desidera tooturn nella directory gestito)
* acquisizione esterno (ad esempio, un amministratore tenta tooadd una nuova directory gestito tooa di dominio)

### <a name="internal-takeover---promote-a-self-service-unmanaged-directory-toobe-a-managed-directory"></a>Acquisizione interno - alzare di livello un toobe directory self-service e non gestite, una directory gestita
Quando si esegue l'operazione di acquisizione interno, directory hello viene convertito da una directory di gestito tooa directory non gestito. È necessario toocomplete DNS dominio convalida del nome, in cui creare un record MX o un record TXT nella zona DNS hello. Questa azione:

* Convalida che si è proprietari di dominio hello
* Rende directory hello gestiti
* Rende hello amministratore globale della directory hello

Si supponga che un amministratore IT di scuola soffietto rileva che gli utenti dall'istituto di istruzione hello hanno effettuato l'iscrizione per le offerte di self-service. Hello registrato proprietario di hello DNS nome BellowsCollege.com, hello amministratore IT può convalidare la proprietà del nome DNS hello in Azure e quindi assumere la directory di hello non gestito. Hello directory diventa quindi gestita e hello amministratore IT viene assegnato il ruolo di amministratore globale hello per directory BellowsCollege.com hello.

### <a name="external-takeover---merge-a-self-service-directory-into-an-existing-managed-directory"></a>Acquisizione della proprietà esterna: unione di una directory self-service in una directory gestita esistente
In un contenuto esterno, si dispone già di una directory gestita e si desidera che tutti gli utenti e gruppi da un toojoin non gestito directory gestiti directory, anziché due proprie directory separano.

Come amministratore di una directory gestito, si aggiunta un dominio, e tale dominio toohave una directory non gestita associata.

Si supponga, ad esempio, un amministratore IT e si dispone già di una directory gestita per Contoso.com, un nome di dominio organizzazione tooyour registrati. Si rileva che gli utenti dell'organizzazione hanno eseguito l'iscrizione self-service per un'offerta usando il nome di dominio di posta elettronica user@contoso.co.uk, ovvero un altro nome di dominio dell'organizzazione. Attualmente gli utenti hanno account in una directory contoso.co.uk non gestita.

Non si desidera toomanage due directory distinte, in modo da unire directory non gestita di hello contoso.co.uk directory IT gestiti esistenti per contoso.com.

Segue acquisizione della proprietà esterni hello stesso processo di convalida DNS come contenuto interno.  Differenza being: gli utenti e i servizi sono toohello rimappato IT directory gestito.

#### <a name="whats-hello-impact-of-performing-an-external-takeover"></a>Che cos'è l'impatto di hello dell'esecuzione di un'acquisizione esterno?
Con un contenuto esterno, viene creato un mapping per gli utenti a risorse in modo che gli utenti possono continuare tooaccess servizi senza interruzioni. Molte applicazioni, incluso RMS per utenti singoli, gestiscono automaticamente i mapping di hello per gli utenti a risorse e gli utenti possono continuare tooaccess tali servizi senza alcuna modifica. Se un'applicazione gestisce in modo efficace il mapping di hello per gli utenti-risorse, acquisizione esterno potrebbe essere utenti tooprevent bloccato in modo esplicito dal provider.

#### <a name="directory-takeover-support-by-service"></a>Supporto dell'acquisizione della proprietà di directory in base al servizio
Attualmente hello seguenti servizi di supporto di acquisizione:

* RMS

Hello seguenti servizi appena supporto di acquisizione:

* PowerBI

di seguito Hello non e richiede che i dati utente di amministrazione aggiuntive azione toomigrate dopo un contenuto esterno.

* SharePoint/OneDrive

## <a name="how-tooperform-a-dns-domain-name-takeover"></a>Come assegnare un nome acquisizione tooperform un dominio DNS
Sono disponibili alcune opzioni per come tooperform una convalida del dominio (ed eseguire un'acquisizione, se si desidera):

1. Portale di gestione di Azure

   Un'acquisizione viene attivata eseguendo l'aggiunta di un dominio.  Se esiste già una directory per il dominio hello, sarà necessario hello opzione tooperform un contenuto esterno.

   Accedi toohello portale di Azure utilizzando le credenziali.  Passare una directory esistente tooyour e quindi troppo**Aggiungi dominio**.
2. Office 365

   È possibile utilizzare opzioni hello hello [gestire domini](https://support.office.com/article/Navigate-to-the-Office-365-Manage-domains-page-026af1f2-0e6d-4f2d-9b33-fd147420fac2/) pagina toowork di Office 365 con i domini e i record DNS. Vedere [Verificare il dominio in Office 365](https://support.office.com/article/Verify-your-domain-in-Office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611/).
3. Windows PowerShell

   Hello seguendo i passaggi è necessari tooperform una convalida mediante Windows PowerShell.

   | Passaggio | Cmdlet toouse |
   | --- | --- |
   | Creare un oggetto credential |Get-Credential |
   | Connettersi AD tooAzure |Connect-MsolService |
   | Ottenere un elenco di domini |Get-MsolDomain |
   | Creare una richiesta di verifica |Get-MsolDomainVerificationDns |
   | Creare record DNS |Eseguire questa operazione sul server DNS |
   | Verificare la sfida hello |Confirm-MsolEmailVerifiedDomain |

ad esempio:

1. Connettersi AD tooAzure utilizzando le credenziali di hello che sono stati utilizzati toorespond toohello self-service offerta:

        import-module MSOnline
        $msolcred = get-credential
        connect-msolservice -credential $msolcred
2. Ottenere un elenco di domini:

    Get-MsolDomain
3. Eseguire quindi toocreate di cmdlet Get-MsolDomainVerificationDns hello una richiesta di verifica:

    Get-MsolDomainVerificationDns –DomainName *your_domain_name* –Mode DnsTxtRecord

    ad esempio:

    Get-MsolDomainVerificationDns –DomainName contoso.com –Mode DnsTxtRecord
4. Copiare il valore di hello (verifica hello) restituito da questo comando.

    ad esempio:

    MS=32DD01B82C05D27151EA9AE93C5890787F0E65D9
5. Nello spazio dei nomi pubblico DNS, creare un record txt DNS che contiene il valore hello copiata nel passaggio precedente hello.

    nome Hello per questo record è hello nome del dominio padre hello, pertanto se si crea questo record di risorse con il ruolo DNS hello da Windows Server, lasciare il nome di Record hello vuoto e incollare il valore di hello nella casella di testo hello
6. Eseguire una richiesta di verifica hello Confirm-MsolDomain cmdlet tooverify hello:

    Confirm-MsolEmailVerifiedDomain -DomainName *your_domain_name*

    ad esempio:

    Confirm-MsolEmailVerifiedDomain -DomainName contoso.com

Una richiesta di verifica ha esito positivo restituisce si toohello prompt senza errori.

## <a name="how-do-i-control-self-service-settings"></a>Come controllare le impostazioni di self-service?
Gli amministratori attualmente dispongono di due controlli self-service. Possono controllare:

* Se gli utenti possono partecipare directory hello tramite posta elettronica.
* Se gli utenti possono ottenere autonomamente una licenza per applicazioni e servizi.

### <a name="how-can-i-control-these-capabilities"></a>Come è possibile controllare queste funzionalità?
Un amministratore può configurare queste funzionalità usando questi parametri del cmdlet Set-MsolCompanySettings di Azure AD:

* **AllowEmailVerifiedUsers** controlla se un utente può essere aggiunto a una directory non gestita o crearne una. Se si imposta tale parametro troppo$ false, non verificato tramite posta elettronica agli utenti possono aggiungere directory di hello.
* **AllowAdHocSubscriptions** controlla hello possibilità per gli utenti self-service tooperform effettuare l'iscrizione. Se si imposta tale parametro troppo$ false, non gli utenti possono eseguire abbonamento self-service.

### <a name="how-do-hello-controls-work-together"></a>Come controlli hello funzionano insieme?
Questi due parametri possono essere utilizzati in combinazione toodefine iscriversi controllo più preciso Self-Service. Ad esempio, hello comando seguente consentirà agli utenti tooperform iscrizione self-service, ma solo se tali utenti dispongano già di un account di Azure AD (in altre parole, gli utenti che sarebbe necessario un account di posta elettronica con verifica di toobe creato non è possibile eseguire accesso self-service di):

    Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true

Hello diagramma di flusso seguente illustra tutte le combinazioni diverse di hello per questi parametri e le condizioni di risultante hello per directory hello e iscrizione self-service.

![][1]

Per ulteriori informazioni ed esempi di come toouse questi parametri, vedere [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).

## <a name="see-also"></a>Vedere anche
* [Come tooinstall e configurare Azure PowerShell](/powershell/azure/overview)
* [Azure PowerShell](/powershell/azure/overview)
* [Informazioni di riferimento sui cmdlet di Azure](/powershell/azure/get-started-azureps)
* [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)

<!--Image references-->
[1]: ./media/active-directory-self-service-signup/SelfServiceSignUpControls.png
