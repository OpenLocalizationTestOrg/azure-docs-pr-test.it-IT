---
title: aaaHow toouse una panoramica di directory tenant di Azure Active Direcory | Documenti Microsoft
description: "Spiega che cos'è un tenant di Azure AD e come toomanage Azure tramite Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: it-pro;oldportal
ms.openlocfilehash: ddb16d89bf06a3753ed5106bd95162130ad51b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-azure-ad-directory"></a>Gestire la directory di Azure AD

## <a name="what-is-an-azure-ad-tenant"></a>Che cos'è un tenant di Azure AD?
In Azure Active Directory (Azure AD), un tenant è un'istanza dedicata di Azure Active Directory che l'organizzazione riceve quando effettua l'iscrizione a un servizio cloud Microsoft, ad esempio Azure oppure Office 365. Ogni directory di Azure AD è distinta e separata dalle altre directory di Azure AD. Come un edificio ufficio aziendale è un tooonly di bene sicuro specifico dell'organizzazione, una directory di Azure AD è stato inoltre progettato toobe un bene sicuro per l'utilizzo da sola organizzazione. Hello architettura di Azure AD isola le informazioni di identità e i dati cliente in modo che gli utenti e amministratori di una directory di Azure AD non possono accidentalmente o intenzionalmente accedere ai dati in un'altra directory.

![Gestire Azure Active Directory](./media/active-directory-administer/aad_portals.png)

## <a name="how-can-i-get-an-azure-ad-directory"></a>Come è possibile ottenere una directory di Azure AD?
Azure Active Directory fornisce identità e directory principale di hello funzionalità di gestione dietro la maggior parte dei servizi cloud Microsoft, tra cui:

* Azure
* Microsoft Office 365
* Microsoft Dynamics CRM Online
* Microsoft Intune

Quando si effettua l'iscrizione a uno di questi servizi cloud Microsoft, si ottiene una directory di Azure AD. È possibile creare altre directory, se necessario. Ad esempio, è possibile usare la prima directory come directory di produzione e quindi crearne un'altra per le attività di testing o di gestione temporanea.

### <a name="using-hello-azure-ad-directory-that-comes-with-a-new-azure-subscription"></a>Utilizzo di directory di Azure AD hello fornita con una nuova sottoscrizione di Azure

È consigliabile utilizzare account di amministratore hello usato per il primo servizio quando ci si iscrive per altri servizi Microsoft. le informazioni fornite Hello hello prima volta che si effettua l'iscrizione per un servizio di Microsoft è toocreate utilizzato Azure un nuova istanza di Active directory per l'organizzazione. Se si utilizza che directory tooauthenticate tentativi di accesso quando si effettua la sottoscrizione tooother Microsoft services, possono usare hello integrazione della directory locale configurata nella directory predefinita, criteri, impostazioni o gli account utente esistenti.

Ad esempio, se si accede per una sottoscrizione di Microsoft Intune e quindi sincronizzare ulteriormente Active Directory locale con la directory di Azure AD, è possibile iscriversi a un altro servizio Microsoft, ad esempio Office 365 e ottenere facilmente hello stessa directory vantaggi di integrazione con Microsoft Intune.

Per altre informazioni sull'integrazione della directory locale con Azure AD, vedere l'articolo relativo all'[integrazione di directory con Azure AD Connect](active-directory-aadconnect.md).

### <a name="associate-an-existing-azure-ad-directory-with-a-new-azure-subscription"></a>Associare una directory di Azure AD esistente a una nuova sottoscrizione di Azure
È possibile associare una nuova sottoscrizione Azure hello stessa directory che autentica l'accesso in ingresso per una sottoscrizione Office 365 o Microsoft Intune esistente. Per ulteriori informazioni su tale scenario, vedere [trasferire la proprietà di un account di sottoscrizione di Azure tooanother](../billing/billing-subscription-transfer.md)

### <a name="create-an-azure-ad-directory-by-signing-up-for-a-microsoft-cloud-service-as-an-organization"></a>Creare una directory di Azure AD effettuando l'iscrizione a un servizio cloud Microsoft come organizzazione
Se non si dispone ancora tooa una sottoscrizione del servizio cloud Microsoft, è possibile utilizzare uno dei hello seguito toosign collegamenti. Con l'iscrizione al primo servizio verrà creata automaticamente una directory di Azure AD.

* [Microsoft Azure](https://account.azure.com/organization)
* [Office 365](http://products.office.com/business/compare-office-365-for-business-plans/)
* [Microsoft Intune](https://portal.office.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0%20)

### <a name="how-toochange-hello-default-directory-for-a-subscription"></a>Come toochange hello directory predefinita per una sottoscrizione

1. Accedi toohello [centro Account Azure](https://account.windowsazure.com/Home/Index) con un account amministratore dell'Account di proprietà delle sottoscrizioni tootransfer sottoscrizione hello hello.
2. Verificare che tale utente hello indicato come proprietario della sottoscrizione hello toobe si trova nella directory di destinazione hello.
3. Fare clic su **Trasferisci sottoscrizione**.
4. Consente di specificare il destinatario di hello. destinatario Hello ottiene automaticamente un messaggio di posta elettronica con un collegamento di accettazione.
5. destinatario Hello fa clic sul collegamento hello e segue le istruzioni di hello, inclusi immettendo le relative informazioni di pagamento. Quando il destinatario hello ha esito positivo, viene trasferita sottoscrizione hello. 
6. Hello directory predefinita della sottoscrizione hello viene modificato directory toohello hello utente è se trasferimento di proprietà di sottoscrizione hello ha esito positivo.

### <a name="manage-hello-default-directory-in-azure"></a>Gestire directory predefinita hello in Azure
Quando si effettua l'iscrizione ad Azure, alla sottoscrizione viene associata una directory di Azure AD predefinita. L'uso di Azure AD non comporta alcun costo e le directory sono una risorsa gratuita. Sono disponibili servizi di Azure AD a pagamento, concessi in licenza separatamente, che offrono funzionalità aggiuntive come le informazioni personalizzate distintive dell'azienda all'accesso e la reimpostazione password self-service. È inoltre possibile creare un dominio personalizzato utilizzando un nome DNS che si è proprietari anziché predefinito hello *. dominio onmicrosoft.com.

## <a name="how-can-i-manage-directory-data"></a>Come gestire i dati della directory
tooadminister uno o più sottoscrizioni a servizi cloud Microsoft, è possibile utilizzare hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com), hello portale account Microsoft Intune o hello [il centro di amministrazione di Office 365](https://portal.office.com/) toomanage il dati di directory dell'organizzazione. È inoltre possibile utilizzare [i cmdlet di Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory) toohelp gestire i dati archiviati in Azure AD.

Da uno qualsiasi di questi portali o cmdlet è possibile:

* Creare e gestire account di gruppi e utenti
* Gestire i servizi cloud correlati per le sottoscrizioni dell'organizzazione
* Configurare l'integrazione locale con i servizi di autenticazione e di gestione delle identità di Azure AD

centro di amministrazione di Azure AD Hello, centro di amministrazione di Office 365, il portale di account di Microsoft Intune e hello i cmdlet di Azure AD lettura e scrittura tooa singola istanza condivisa di Azure Active Directory associato alla directory dell'organizzazione. Ognuno di questi strumenti funge da interfaccia front-end che esegue il pull o la modifica dei dati della directory.

Quando si modificano i dati dell'organizzazione utilizzando uno dei portali hello o i cmdlet mantenendo l'accesso nel contesto di hello di uno di questi servizi, hello modifiche vengono inoltre illustrate nell'hello altri portali hello successivo che accesso. Questi dati viene condivisa tra hello Microsoft cloud services toowhich che si effettua la sottoscrizione.

Ad esempio, se si utilizza hello centro di amministrazione di Office 365 tooblock un utente di effettuare l'accesso, che i blocchi di azione hello accesso tooany utente altri toowhich servizio l'organizzazione attualmente sottoscritto. Se si visualizza hello stesso account utente nel portale di account di Microsoft Intune hello, viene anche visualizzato tale utente hello è bloccato.

## <a name="how-can-i-add-and-manage-multiple-directories"></a>Come è possibile aggiungere e gestire più directory?
È possibile [aggiungere una directory di Azure AD nel portale di Azure hello](https://portal.azure.com/#create/Microsoft.AzureActiveDirectory). Immettere le informazioni di hello e selezionare **crea**.

È possibile gestire ogni directory come una risorsa completamente indipendente. Ogni directory è infatti un peer con funzionalità complete, indipendente dal punto di vista logico dalle altre directory gestite. Non esiste alcuna relazione padre-figlio tra le directory. Questa indipendenza tra le directory include l'indipendenza delle risorse, l'indipendenza amministrativa e l'indipendenza della sincronizzazione.

* **Indipendenza delle risorse**. Se si crea o si elimina una risorsa in una directory, ha alcun impatto sulle risorse in un'altra directory, con l'eccezione parziale di hello di utenti esterni. Se si usa un dominio personalizzato "contoso.com" con una directory, non è possibile usarlo con altre directory.
* **Indipendenza amministrativa**.  Se un utente non amministratore della directory "Contoso" crea una directory di test denominata "Test":
  
  * gli amministratori di Hello della directory 'Contoso' non possono toodirectory di privilegi amministrativi diretti 'Test' a meno che un amministratore di "Test" vengono loro concessi specificamente questi privilegi. Gli amministratori di 'Contoso' possono controllare l'accesso toodirectory 'Test' per il controllo dell'account utente di hello creato 'Test'.
    
  * Se è possibile assegnare o rimuovere un ruolo di amministratore per un utente in una directory, modifica hello non influisce sul ruolo di amministratore che l'utente potrebbe essere in un'altra directory.
* **Indipendenza della sincronizzazione**. È possibile configurare ogni Azure Active Directory del tenant in modo indipendente tooget sincronizzare i dati da uno strumento di sincronizzazione directory di singola istanza hello Azure AD Connect.

A differenza di altre risorse di Azure, le proprie directory non sono risorse figlio di una sottoscrizione di Azure. Pertanto, se si annulla o consentire tooexpire la sottoscrizione di Azure, è comunque possibile accedere ai dati della directory con Azure AD PowerShell, hello API Graph di Azure o altre interfacce, ad esempio amministrazione hello Office 365. È anche possibile associare un'altra sottoscrizione con directory hello.

## <a name="how-tooprepare-toodelete-an-azure-ad-directory"></a>Come tooprepare toodelete una directory di Azure AD
Un amministratore globale può eliminare una directory di Azure AD dal portale hello. Quando viene eliminata una directory, vengono eliminate anche tutte le risorse che sono contenute nella directory hello. Verificare che non necessario hello directory prima di eliminarlo.

> [!NOTE]
> Se l'utente hello è firmato con un account aziendale o dell'istituto di istruzione, utente hello non deve tentare toodelete la home directory. Ad esempio, se hello utente è connesso come joe@contoso.onmicrosoft.com, tale utente non è possibile eliminare la directory di hello che ha contoso.onmicrosoft.com come dominio predefinito.

Azure AD richiede che determinate condizioni siano soddisfatte toodelete una directory. Questo riduce i rischi che l'eliminazione di una directory negativamente influisce su utenti o applicazioni, ad esempio hello possibilità di utenti toosign in tooOffice 365 o di accedere alle risorse in Azure. Ad esempio, se una directory per una sottoscrizione viene inavvertitamente eliminata, quindi gli utenti non possono accedere hello risorse per la sottoscrizione di Azure.

è stato selezionato Hello seguenti condizioni:

* Hello solo utente nella directory hello deve essere amministratore globale di hello che toodelete hello directory. Prima di poter eliminare la directory hello, è necessario eliminare qualsiasi altro utente. Se gli utenti vengono sincronizzati da locale, quindi su cui è necessario disattivare la sincronizzazione e utenti di hello devono essere eliminati nella directory cloud hello utilizzando hello portale di Azure o i cmdlet PowerShell di Azure. Non è presente alcun gruppi toodelete requisito o contatti, ad esempio contatti aggiunti dall'amministrazione hello Office 365.
* Non può esistere alcuna applicazione nella directory hello. Tutte le applicazioni devono essere eliminate prima di poter eliminare la directory hello.
* Nessun provider di autenticazione a più fattori può essere collegato toohello directory.
* Non può esistere alcuna sottoscrizione per i Microsoft Online Services come Microsoft Azure, Office 365 o Azure AD Premium associata hello directory. Se, ad esempio, in Azure è stata creata una directory predefinita, non è possibile eliminare la directory se la propria sottoscrizione di Azure si basa ancora su di essa per l'autenticazione. Analogamente, non è possibile eliminare una directory se la sottoscrizione di un altro utente è associata a tale directory. 


## <a name="next-steps"></a>Passaggi successivi
* [Forum di Azure AD](https://social.msdn.microsoft.com/Forums/home?forum=WindowsAzureAD)
* [Forum di Azure Multi-Factor Authentication](https://social.msdn.microsoft.com/Forums/home?forum=windowsazureactiveauthentication)
* [Domande per Azure in Stack Overflow](http://stackoverflow.com/questions/tagged/azure)
* [Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory)
* [Assegnazione dei ruoli di amministratore in Azure AD](active-directory-assign-admin-roles.md)
