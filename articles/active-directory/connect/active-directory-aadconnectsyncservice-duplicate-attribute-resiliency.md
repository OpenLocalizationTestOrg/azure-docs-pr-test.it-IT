---
title: resilienza di attributo duplicato e sincronizzazione aaaIdentity | Documenti Microsoft
description: "Nuovo comportamento della modalità toohandle gli oggetti con UPN o ProxyAddress conflitti durante la sincronizzazione della directory con Azure AD Connect."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 537a92b7-7a84-4c89-88b0-9bce0eacd931
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.openlocfilehash: e27dcbf9d71f83fa9566cae2fd99350297d1cd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="identity-synchronization-and-duplicate-attribute-resiliency"></a>Sincronizzazione delle identità e resilienza degli attributi duplicati
La resilienza degli attributi duplicati è una funzionalità di Azure Active Directory che consente di eliminare i problemi causati dai conflitti tra **UserPrincipalName** e **ProxyAddress** durante l'esecuzione di uno degli strumenti di sincronizzazione di Microsoft.

Questi due attributi vengono in genere necessario toobe univoco in tutti **utente**, **gruppo**, o **contatto** gli oggetti in un determinato tenant di Azure Active Directory.

> [!NOTE]
> Solo gli oggetti User possono avere UPN.
> 
> 

nuovo comportamento Hello che questa funzionalità consente è in parte cloud hello della pipeline di sincronizzazione hello, pertanto è client indipendente e rilevante per i prodotti di sincronizzazione di Microsoft tra cui Azure AD Connect, DirSync e MIM + connettore. termine generico Hello "client di sincronizzazione" viene utilizzato in questo documento toorepresent uno di questi prodotti.

## <a name="current-behavior"></a>Comportamento attuale
Se si verifica un tentativo tooprovision un nuovo oggetto con un valore UPN o ProxyAddress che viola il vincolo di univocità, Azure Active Directory blocca l'oggetto non verrà creato. Analogamente, se un oggetto viene aggiornato con un UPN o un ProxyAddress non univoco, hello aggiornamento non riesce. Hello provisioning tentativo o update viene ripetuta dal client di sincronizzazione hello durante ogni ciclo di esportazione e continua toofail fino alla risoluzione dei conflitti hello. Un messaggio di posta elettronica report di errore viene generato dopo ogni tentativo e dal client di sincronizzazione hello viene registrato un errore.

## <a name="behavior-with-duplicate-attribute-resiliency"></a>Comportamento con resilienza degli attributi duplicati
Anziché completamente non superati tooprovision o aggiornare un oggetto con un attributo duplicato, Azure Active Directory "vengono messi in quarantena" attributo duplicato hello violerebbe il vincolo di univocità hello. Se questo attributo è obbligatorio per il provisioning, ad esempio UserPrincipalName, servizio hello assegna un valore di segnaposto. formato Hello di questi valori temporanei  
“***<OriginalPrefix>+<4DigitNumber>@<InitialTenantDomain>.onmicrosoft.com***”.  
Se l'attributo hello non è necessaria, ad esempio un **ProxyAddress**, Azure Active Directory semplicemente mette attributo conflitto hello e procede con la creazione di oggetti hello o un aggiornamento.

Al momento la messa in quarantena attributo hello, informazioni sui conflitti hello viene inviate nella hello stesso messaggio di posta elettronica report di errore utilizzato nel comportamento precedente hello. Tuttavia, queste informazioni viene visualizzato solo nella segnalazione errori hello una sola volta, in caso di quarantena hello, non continua toobe in futuro registrati messaggi di posta elettronica. Inoltre, poiché esportazione hello per questo oggetto ha avuto esito positivo, il client di sincronizzazione hello non registra un errore e non hello di tentativi non creare o aggiornare l'operazione su cicli di sincronizzazione successivo.

toosupport che un nuovo attributo di questo comportamento è stato aggiunto le classi di oggetti User, Group e Contact toohello:  
**DirSyncProvisioningErrors**

Questo è un attributo multivalore che toostore utilizzati hello attributi in conflitto che violano il vincolo di univocità hello devono essere aggiunti normalmente. Un'attività in background timer è stata abilitata in Azure Active Directory che esegue toolook ogni ora per i conflitti di attributo duplicate che sono stati risolti e gli attributi di hello in questione viene rimosso automaticamente dalla quarantena.

### <a name="enabling-duplicate-attribute-resiliency"></a>Abilitazione della resilienza degli attributi duplicati
Resilienza di attributo duplicati saranno nuovo comportamento predefinito di hello tra tutti i tenant di Azure Active Directory. Verrà visualizzato su per impostazione predefinita per tutti i tenant che è abilitata la sincronizzazione per hello prima volta il 22 agosto 2016 o versione successiva. Tenant che abilitato sincronizzazione precedente toothis data avrà attivato hello in batch. Questa implementazione inizierà settembre 2016, e verrà inviata una notifica di posta elettronica contatto tecnico notifica tooeach del tenant con data di hello specifica quando verrà abilitata la funzionalità hello.

> [!NOTE]
> Dopo che è stata attivata, la resilienza degli attributi duplicati non può essere disabilitata.

toocheck se hello funzionalità è abilitata per il tenant, è possibile farlo scaricando più recente del modulo di Azure Active Directory PowerShell hello hello e in esecuzione:

`Get-MsolDirSyncFeatures -Feature DuplicateUPNResiliency`

`Get-MsolDirSyncFeatures -Feature DuplicateProxyAddressResiliency`

> [!NOTE]
> Non è più, è possibile utilizzare funzionalità resilienza di attributo duplicato di comando Set-MsolDirSyncFeature cmdlet tooproactively Abilita hello prima è attivata per il tenant. funzionalità di hello in grado di tootest toobe, sarà necessario toocreate un nuovo tenant di Azure Active Directory.

## <a name="identifying-objects-with-dirsyncprovisioningerrors"></a>Identificazione di oggetti con DirSyncProvisioningErrors
Esistono attualmente due metodi tooidentify oggetti che contengono questi errori a causa di conflitti di proprietà tooduplicate, Azure Active Directory PowerShell e hello portale di amministrazione di Office 365. Sono disponibili piani tooextend tooadditional portale basato su reporting in hello future.

### <a name="azure-active-directory-powershell"></a>Azure Active Directory PowerShell
Per i cmdlet di PowerShell in questo argomento hello, di seguito hello è true:

* Tutti i seguenti cmdlet hello sono tra maiuscole e minuscole.
* Hello **– ErrorCategory PropertyConflict** deve essere sempre incluso. Non sono attualmente disponibili altri tipi di **ErrorCategory**, ma ciò può essere esteso in hello future.

Per iniziare, eseguire prima di tutto **Connect-MsolService** e immettere le credenziali di amministratore tenant.

Usare quindi hello gli errori di tooview di cmdlet e gli operatori seguenti in modi diversi:

1. [Visualizzare tutto](#see-all)
2. [Per tipo di proprietà](#by-property-type)
3. [Per valore in conflitto](#by-conflicting-value)
4. [Tramite una stringa di ricerca](#using-a-string-search)
5. [Ordinati](#sorted)
6. [Una quantità limitata o tutti](#in-a-limited-quantity-or-all)

#### <a name="see-all"></a>Visualizzare tutto
Una volta connessi, toosee eseguire un elenco generale di attributo nel tenant di hello errori di provisioning:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict`

Ciò produce un risultato simile hello seguente:  
 ![Get-MsolDirSyncProvisioningError](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1.png "Get MsolDirSyncProvisioningError")  

#### <a name="by-property-type"></a>Per tipo di proprietà
errori toosee dal tipo di proprietà, aggiungere hello **- PropertyName** flag con hello **UserPrincipalName** o **ProxyAddresses** argomento:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName UserPrincipalName`

Or

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName ProxyAddresses`

#### <a name="by-conflicting-value"></a>Per valore in conflitto
errori di toosee relativi tooa specifiche proprietà aggiungere hello **- PropertyValue** flag (**- PropertyName** deve essere utilizzato anche quando si aggiunge questo flag):

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyValue User@domain.com -PropertyName UserPrincipalName`

#### <a name="using-a-string-search"></a>Tramite una stringa di ricerca
toodo ricerca di una stringa ampie utilizzare hello **- SearchString** flag. Può essere utilizzato in modo indipendente da tutti i hello sopra flag, con l'eccezione hello di **- ErrorCategory PropertyConflict**, che è sempre necessario:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -SearchString User`

#### <a name="in-a-limited-quantity-or-all"></a>Una quantità limitata o tutti
1. **MaxResults <Int>**  può essere utilizzato toolimit hello query tooa numero specifico di valori.
2. **Tutti i** può essere utilizzato tooensure tutti i risultati vengono recuperati hello nel caso in cui è presente un numero elevato di errori.

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -MaxResults 5`

## <a name="office-365-admin-portal"></a>Portale di amministrazione di Office 365
È possibile visualizzare gli errori di sincronizzazione della directory nel centro di amministrazione di Office 365 hello. Hello report viene visualizzato solo portale di Office 365 hello **utente** gli oggetti che contengono questi errori. Non vengono visualizzate informazioni sui conflitti tra **Gruppi** e **Contatti**.

![Utenti attivi](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1234.png "Utenti attivi")

Per istruzioni su come gli errori di sincronizzazione della directory tooview in Office 365 salve center, vedere [identificare gli errori di sincronizzazione della directory in Office 365](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067).

### <a name="identity-synchronization-error-report"></a>Segnalazione dell'errore di sincronizzazione delle identità
Quando un oggetto con un conflitto di attributo duplicato viene gestito con questo nuovo comportamento in che è inclusa una notifica standard hello segnalazione sincronizzazione delle identità di posta elettronica che viene inviato il contatto tecnico notifica toohello per tenant hello. Questo comportamento include tuttavia una modifica importante. In hello precedente, informazioni su un conflitto di attributo duplicato sono incluso in ogni report di errore successivo fino a quando non è stato risolto il conflitto hello. Con questo nuovo comportamento notifica di errore hello per un determinato conflitto vengono visualizzate solo una volta - fase hello attributo in conflitto hello viene messo in quarantena.

Di seguito è riportato un esempio di notifica di posta elettronica quali hello è simile per un conflitto di ProxyAddress:  
    ![Utenti attivi](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "Utenti attivi")  

## <a name="resolving-conflicts"></a>Risoluzione dei conflitti
Strategie di strategia e la risoluzione degli errori di risoluzione dei problemi non devono essere diversi da modo hello gli errori di attributo duplicati sono stati gestiti in hello precedente. Hello unica differenza è che hello timer attività sweep tramite tenant hello su hello lato servizio tooautomatically aggiungere attributo hello domanda toohello corretto oggetto una volta risolto il conflitto hello.

Hello articolo vengono descritte diverse strategie di risoluzione dei problemi: [duplicato o attributi non validi impediscono la sincronizzazione delle directory in Office 365](https://support.microsoft.com/kb/2647098).

## <a name="known-issues"></a>Problemi noti
Nessuno di questi problemi noti causa perdite di dati o la riduzione delle prestazioni del servizio. Alcuni di essi sono estetici, altre causano standard "*pre-resilienza*" toobe errori attributo duplicati generato anziché la messa in quarantena hello conflitto attributo e un altro fa sì che alcuni errori toorequire extra manuale correzione.

**Comportamento di base:**

1. Gli oggetti con configurazioni di attributo specifico continuano tooreceive esportazione errori come toohello anziché duplicati attributi messi in quarantena.  
   ad esempio:
   
    a. In AD viene creato un nuovo utente con un UPN **Joe@contoso.com** e ProxyAddress **smtp:Joe@contoso.com**
   
    b. Hello proprietà dell'oggetto in conflitto con un gruppo esistente, in cui è ProxyAddress  **SMTP:Joe@contoso.com** .
   
    c. Al momento dell'esportazione, un **conflitto ProxyAddress** viene generato l'errore anziché gli attributi di conflitto hello in quarantena. operazione Hello viene ritentata durante ogni ciclo di sincronizzazione successivo, come sarebbe stato prima è stata abilitata la funzionalità di resilienza hello.
2. Se vengono creati due gruppi locali con hello stesso indirizzo SMTP, tooprovision ha esito negativo di un primo tentativo di hello con standard duplicati **ProxyAddress** errore. Tuttavia, valore duplicato hello viene correttamente messo in quarantena su hello successivo ciclo di sincronizzazione.

**Report del portale di Office**:

1. messaggio di errore dettagliato Hello per due oggetti in un set di conflitto di nome UPN è hello stesso. Ciò indica che per entrambi l'UPN è stato modificato o messo in quarantena, mentre in realtà i dati sono stati modificati solo per uno di essi.
2. messaggio di errore dettagliato Hello per un conflitto di nome UPN Mostra hello displayName errato per un utente che ha il nome dell'entità modificata/messi in quarantena. ad esempio:
   
    a. **User A** viene sincronizzato prima con **UPN = User@contoso.com**.
   
    b. **L'utente B** viene tentata toobe sincronizzata la prossima con **UPN = User@contoso.com** .
   
    c. **Dell'utente B** UPN è stato modificato anche **User1234@contoso.onmicrosoft.com**  e  **User@contoso.com**  viene aggiunto troppo**DirSyncProvisioningErrors**.
   
    d. messaggio di errore Hello per **utente B** dovrebbe indicare che **utente** dispone già di  **User@contoso.com**  come mostrato un UPN, ma **dell'utente B** personalizzate displayName.

**Segnalazione dell'errore di sincronizzazione delle identità**:

collegamento Hello per *procedura tooresolve questo problema* non è corretto:  
    ![Utenti attivi](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "Utenti attivi")  

Deve fare riferimento troppo[https://aka.ms/duplicateattributeresiliency](https://aka.ms/duplicateattributeresiliency).

## <a name="see-also"></a>Vedere anche
* [Servizio di sincronizzazione Azure AD Connect](active-directory-aadconnectsync-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
* [Identificare gli errori di sincronizzazione della directory in Office 365](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067)

