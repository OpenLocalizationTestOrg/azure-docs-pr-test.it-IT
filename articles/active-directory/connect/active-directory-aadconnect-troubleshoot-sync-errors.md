---
title: 'Azure AD Connect: Risoluzione dei problemi durante la sincronizzazione | Microsoft Docs'
description: Viene illustrato come tootroubleshoot errori rilevati durante la sincronizzazione con Azure AD Connect.
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 2209d5ce-0a64-447b-be3a-6f06d47995f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: af262dfe95d686e34697454c0dfe8b4a6d8693c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-errors-during-synchronization"></a>Risoluzione degli problemi durante la sincronizzazione
Quando i dati di identità vengono sincronizzati da Windows Server Active Directory (AD DS) tooAzure Active Directory (Azure AD), potrebbero verificarsi errori. In questo articolo viene fornita una panoramica dei diversi tipi di errori di sincronizzazione, alcuni degli scenari possibili hello che causano tali errori e i potenziali errori di hello toofix modi. In questo articolo include tipi di errore comuni hello e non può coprire tutti i possibili errori hello.

 In questo articolo presuppone hello familiarità con hello sottostante [progettare i concetti di Azure AD e Azure AD Connect](active-directory-aadconnect-design-concepts.md).

Con la versione più recente di hello di Azure AD Connect \(agosto 2016 o versioni successiva\), un report di errori di sincronizzazione è disponibile in hello [portale Azure](https://aka.ms/aadconnecthealth) come parte di Azure AD Connect Health per la sincronizzazione.

A partire da 1 settembre 2016 [Azure Active Directory duplicato attributo resilienza](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) funzionalità verrà abilitata per impostazione predefinita per tutti i hello *nuova* tenant di Azure Active Directory. Questa funzionalità verrà abilitata automaticamente per i tenant esistenti nei prossimi mesi di hello.

Azure AD Connect esegue 3 tipi di operazioni da directory hello mantiene sincronizzato: importazione, sincronizzazione e l'esportazione. Errori possono avvenire in tutte le operazioni hello. Questo articolo è incentrato principalmente in caso di errori durante l'esportazione tooAzure Active Directory.

## <a name="errors-during-export-tooazure-ad"></a>Errori durante l'esportazione tooAzure AD
Sezione di seguito vengono descritti diversi tipi di sincronizzazione, gli errori che possono verificarsi durante hello esportazione operazione tooAzure Active Directory utilizzando hello connettore Azure AD. Questo connettore può essere identificato dal formato del nome hello in "contoso. *onmicrosoft.com*".
Errori durante l'esportazione tooAzure AD indicano tale operazione hello \(aggiunta, aggiornamento, eliminazione e così via\) tentato da Azure AD Connect \(motore di sincronizzazione\) su Azure Active Directory non è riuscita.

![Panoramica degli errori di esportazione](./media/active-directory-aadconnect-troubleshoot-sync-errors/Export_Errors_Overview_01.png)

## <a name="data-mismatch-errors"></a>Errori di mancata corrispondenza dei dati
### <a name="invalidsoftmatch"></a>InvalidSoftMatch
#### <a name="description"></a>Descrizione
* Quando Azure AD Connect \(motore di sincronizzazione\) indica a Azure tooadd o aggiornamento oggetti di Active Directory, Azure AD corrispondenze hello oggetto in ingresso utilizzando hello **sourceAnchor** attributo toohello  **immutableId** attributo degli oggetti in Azure AD. Tale corrispondenza viene detta **corrispondenza rigida**.
* Quando Azure AD **non trova** qualsiasi oggetto che trova la corrispondenza hello **immutableId** attributo con hello **sourceAnchor** attributo dell'oggetto in ingresso hello, prima del provisioning di un nuovo oggetto, viene utilizzata la cartella toouse hello ProxyAddresses e toofind gli attributi UserPrincipalName una corrispondenza. Tale corrispondenza viene detta **corrispondenza flessibile**. Corrispondenza Soft Hello è toomatch progettato oggetti già presenti in Azure AD (che sono distribuiti in Azure AD) con hello nuovi oggetti viene aggiunto o aggiornato durante la sincronizzazione che rappresentano hello stessa entità (utenti, gruppi) in locale.
* **InvalidSoftMatch** errore si verifica quando hello rigido corrispondenza non viene trovato alcun oggetto corrispondente **AND** soft match trova un oggetto corrispondente, ma tale oggetto ha un valore diverso di *immutableId* rispetto a hello in arrivo oggetto *SourceAnchor*, suggerendo che hello corrispondono all'oggetto è stato sincronizzato con un altro oggetto in Active Directory locale.

In altre parole, affinché toowork corrispondenza soft hello, hello oggetto toobe soft-associati non deve avere qualsiasi valore per hello *immutableId*. Se qualsiasi oggetto con *immutableId* set con un valore non è possibile eseguire criteri di soft-match hello hello rigido corrispondenza ma soddisfacente, hello operazione provocherebbe un errore di sincronizzazione InvalidSoftMatch.

Gli attributi di Azure Active Directory schema non consente due o più oggetti toohave hello dello stesso valore di hello seguente. \)L'elenco è incompleto.\(

* ProxyAddresses
* UserPrincipalName
* onPremisesSecurityIdentifier
* ObjectId

> [!NOTE]
> [Azure AD attributi duplicati attributo resilienza](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) funzionalità è anche in fase di implementazione come comportamento predefinito di hello di Azure Active Directory.  Ciò consente di ridurre il numero di hello di errori di sincronizzazione rilevato da Azure AD Connect (così come altri client di sincronizzazione), eseguendo AD Azure più resiliente in modo hello che Gestione duplicati ProxyAddresses e UserPrincipalName degli attributi presenti in Active Directory locale ambienti. Questa funzionalità non correggere gli errori di duplicazione di hello. Pertanto, hello ancora dati toobe fissa. Ma consente il provisioning di nuovi oggetti che sono bloccati in caso contrario da in corso il provisioning a causa di valori tooduplicated in Azure AD. Ciò riduce anche numero hello del client di sincronizzazione toohello restituiti gli errori di sincronizzazione.
> Se questa funzionalità è abilitata per il Tenant, non verranno visualizzati errori di sincronizzazione di InvalidSoftMatch hello visualizzati durante il provisioning di nuovi oggetti.
>
>

#### <a name="example-scenarios-for-invalidsoftmatch"></a>Scenari di esempio per InvalidSoftMatch
1. Due o più oggetti con hello dello stesso valore di attributo ProxyAddresses esiste Active Directory locale. ma il provisioning viene eseguito in Azure AD soltanto per un oggetto.
2. Due o più oggetti con hello dello stesso valore di userPrincipalName esiste Active Directory locale. ma il provisioning viene eseguito in Azure AD soltanto per un oggetto.
3. Un oggetto è stato aggiunto in hello in Active Directory locale con hello stesso valore dell'attributo ProxyAddresses a quello di un oggetto esistente in Azure Active Directory. oggetto Hello aggiunto in locale non è recupero disponibile in Azure Active Directory.
4. Un oggetto è stato aggiunto in locale Active Directory con hello stesso valore dell'attributo userPrincipalName come quella di un account in Azure Active Directory. oggetto Hello non è ottenere il provisioning in Azure Active Directory.
5. Un account sincronizzato è stato spostato da tooForest A foresta b. Azure AD Connect (motore di sincronizzazione) è stato utilizzando hello toocompute di ObjectGUID attributo SourceAnchor. Dopo lo spostamento di foresta hello, hello valore SourceAnchor hello è diverso. nuovo oggetto di Hello (dalla foresta B) non riesce a toosync con l'oggetto esistente hello in Azure AD.
6. Un oggetto sincronizzato sono stati accidentalmente eliminato in Active Directory locale e un nuovo oggetto creato in Active Directory per hello stessa entità (ad esempio, utente) senza eliminare l'account di hello in Azure Active Directory. nuovo account Hello ha esito negativo toosync con l'oggetto di Azure AD esistente hello.
7. Azure AD Connect è stato disinstallato e reinstallato. Nel corso della reinstallazione hello è stato scelto un altro attributo come hello SourceAnchor. Tutti gli oggetti di hello che avevano in precedenza è stata sincronizzata interrotto la sincronizzazione con errore InvalidSoftMatch.

#### <a name="example-case"></a>Caso di esempio:
1. **Bob Smith** è un utente sincronizzato in Azure Active Directory da un'Active Directory locale di *contoso.com*
2. Il parametro **UserPrincipalName** di Bob Smith viene configurato come **bobs@contoso.com**.
3. **"abcdefghijklmnopqrstuv = ="** è hello **SourceAnchor** calcolato da Azure AD Connect usando Bob Smith **objectGUID** da in locale di Active Directory, ovvero hello **immutableId** per Bob Smith in Azure Active Directory.
4. Bob presenta anche seguenti valori per hello **proxyAddresses** attributo:
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
5. Un nuovo utente **Bob Taylor**, viene aggiunto toohello in Active Directory locale.
6. Il parametro **UserPrincipalName** di Bob Taylor viene configurato come **bobt@contoso.com**.
7. **"abcdefghijkl0123456789 = =" "** è hello **sourceAnchor** calcolato da Azure AD Connect usando di Bob Taylor **objectGUID** dal locali Active Directory. Oggetto di Bob Taylor ha non tooAzure Active Directory è ancora sincronizzato.
8. Bob Taylor è hello seguenti valori per l'attributo proxyAddresses hello
   * smtp:bobt@contoso.com
   * smtp:bob.taylor@contoso.com
   * **smtp:bob@contoso.com**
9. Durante la sincronizzazione, Azure AD Connect riconoscerà aggiunta hello di Bob Taylor in Active Directory locale e chiedere di Azure AD toomake hello stessa modifica.
10. Azure AD eseguirà prima una corrispondenza rigida, Vale a dire eseguirà la ricerca nel caso di qualsiasi oggetto hello immutableId uguale troppo "abcdefghijkl0123456789 = =". La corrispondenza rigida avrà esito negativo se nessun altro oggetto in Azure AD avrà quell'attributo immutableId.
11. Azure Active Directory tenterà quindi toosoft-match Bob Taylor. Ovvero, eseguirà la ricerca se è presente alcun oggetto con toohello uguale proxyAddresses tre valori, inclusismtp:bob@contoso.com
12. Azure AD troverà oggetto Bob Smith toomatch hello soft-corrispondenza di criteri. Ma questo oggetto ha valore hello immutableId = "abcdefghijklmnopqrstuv = =". il quale indica che l'oggetto è stato sincronizzato da un altro oggetto presente nell'Active Directory locale. Di conseguenza, Azure AD non può eseguire la corrispondenza flessibile di questi oggetti e viene restituito l'errore di sincronizzazione **InvalidSoftMatch**.

#### <a name="how-toofix-invalidsoftmatch-error"></a>Come toofix InvalidSoftMatch errore
la causa più comune per hello InvalidSoftMatch errore Hello è due oggetti con diversi SourceAnchor \(immutableId\) hanno hello stesso valore per hello ProxyAddresses e/o UserPrincipalName attributi, che vengono utilizzati durante hello processo di corrispondenza di soft su Azure AD. In ordine toofix hello corrispondenza software non valido

1. Identificare proxyAddresses hello duplicato, userPrincipalName o un altro valore di attributo che ha causato l'errore hello. Inoltre di identificare quali due \(più\) gli oggetti coinvolti in conflitto hello. report generato da Hello [Azure AD Connect Health per la sincronizzazione](https://aka.ms/aadchsyncerrors) consentono di identificare hello due oggetti.
2. Identificare l'oggetto deve continuare valore hello duplicato toohave e non l'oggetto.
3. Rimuovere il valore di hello duplicata dall'oggetto hello che non dovrebbe essere tale valore. Si noti che sarà necessario apportare hello nella directory hello in oggetto hello proviene da modificare. In alcuni casi, potrebbe essere toodelete uno degli oggetti hello in conflitto.
4. Se sono state hello modificare in hello in Active Directory locale, consentire modificare hello sincronizzazione Azure AD Connect.

Si noti che segnalazione errori di sincronizzazione all'interno di Azure AD Connect Health per la sincronizzazione viene aggiornato ogni 30 minuti e include gli errori di hello dal tentativo di sincronizzazione più recente di hello.

> [!NOTE]
> ImmutableId, per definizione, non modificare la durata hello dell'oggetto hello. Se Azure AD Connect non è stato configurato con alcuni degli scenari di hello in considerazione da hello sopra l'elenco, potrebbero finire in una situazione in cui Azure AD Connect calcola un valore diverso di hello SourceAnchor per l'oggetto hello Active Directory che rappresenta hello stessa entità (utente stesso / gruppo o contatto (e così via) che dispone di un oggetto di Active Directory di Azure esistente che si intende procedere utilizzando toocontinue.
>
>

#### <a name="related-articles"></a>Articoli correlati
* [Gli attributi duplicati o non validi impediscono la sincronizzazione delle directory in Office 365](https://support.microsoft.com/en-us/kb/2647098)

### <a name="objecttypemismatch"></a>ObjectTypeMismatch
#### <a name="description"></a>Descrizione
Quando Azure AD tenta toosoft corrispondenza due oggetti, è possibile che due oggetti di tipo diverso "tipo di oggetto" (ad esempio utente, gruppo, contatto e così via.) hanno hello stessi valori per gli attributi di hello utilizzati corrispondenza flessibile di tooperform hello. Come la duplicazione di questi attributi non è consentita in Azure AD, operazione hello può comportare errori di sincronizzazione "ObjectTypeMismatch".

#### <a name="example-scenarios-for-objecttypemismatch-error"></a>Scenari di esempio per l'errore ObjectTypeMismatch
* In Office 365 viene creato un gruppo di protezione abilitato alla posta elettronica. Amministratore aggiunge un nuovo utente o un contatto in locale Active Directory (che non è stato sincronizzato tooAzure AD ancora) con hello stesso valore di attributo ProxyAddresses hello a quella di Office 365 hello gruppo.

#### <a name="example-case"></a>Caso di esempio
1. Amministratore crea un nuovo gruppo di sicurezza abilitato alla posta in Office 365 per reparto Tax hello e fornisce un indirizzo di posta elettronica come tax@contoso.com. Consente di assegnare l'attributo ProxyAddresses hello per questo gruppo con valore hello**smtp:tax@contoso.com**
2. Un nuovo utente join Contoso.com e viene creato un account utente di hello in locale con proxyAddress hello come**smtp:tax@contoso.com**
3. Quando Azure AD Connect verrà sincronizzato nuovo account utente di hello, otterrà l'errore "ObjectTypeMismatch" hello.

#### <a name="how-toofix-objecttypemismatch-error"></a>Come toofix ObjectTypeMismatch errore
causa più comune di Hello per correggere l'errore ObjectTypeMismatch hello è hello stesso valore di attributo ProxyAddresses hello è per due oggetti di tipo diverso (utente, gruppo o contatto e così via.). In ordine toofix hello ObjectTypeMismatch:

1. Identificare hello duplicato proxyAddresses (o altri attributi) valore di questo errore hello ha causato. Inoltre di identificare quali due \(più\) gli oggetti coinvolti in conflitto hello. report generato da Hello [Azure AD Connect Health per la sincronizzazione](https://aka.ms/aadchsyncerrors) consentono di identificare hello due oggetti.
2. Identificare l'oggetto deve continuare valore hello duplicato toohave e non l'oggetto.
3. Rimuovere il valore di hello duplicata dall'oggetto hello che non dovrebbe essere tale valore. Si noti che sarà necessario apportare hello nella directory hello in oggetto hello proviene da modificare. In alcuni casi, potrebbe essere toodelete uno degli oggetti hello in conflitto.
4. Se sono state hello modificare in hello in Active Directory locale, consentire modificare hello sincronizzazione Azure AD Connect. Segnalazione di errori di sincronizzazione all'interno di Azure AD Connect Health per la sincronizzazione viene aggiornato ogni 30 minuti e include gli errori di hello dal tentativo di sincronizzazione più recente di hello.

## <a name="duplicate-attributes"></a>Attributi duplicati
### <a name="attributevaluemustbeunique"></a>AttributeValueMustBeUnique
#### <a name="description"></a>Descrizione
Gli attributi di Azure Active Directory schema non consente due o più oggetti toohave hello dello stesso valore di hello seguente. Che è forzato toohave un valore univoco di questi attributi in una determinata istanza di ogni oggetto in Azure AD.

* ProxyAddresses
* UserPrincipalName

Se Azure AD Connect tenta un nuovo oggetto tooadd o aggiornare un oggetto esistente con un valore per hello sopra gli attributi che è già stato assegnato l'oggetto tooanother in Azure Active Directory, operazione hello comporta errore di sincronizzazione "AttributeValueMustBeUnique" hello.

#### <a name="possible-scenarios"></a>Scenari possibili:
1. Valore duplicato è assegnato tooan già sincronizzati oggetto, che è in conflitto con un altro oggetto sincronizzato.

#### <a name="example-case"></a>Caso di esempio:
1. **Bob Smith** è un utente sincronizzato in Azure Active Directory da un'Active Directory locale di contoso.com
2. Il parametro **UserPrincipalName** di Bob Smith in locale è configurato come **bobs@contoso.com**.
3. Bob presenta anche seguenti valori per hello **proxyAddresses** attributo:
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
4. Un nuovo utente **Bob Taylor**, viene aggiunto toohello in Active Directory locale.
5. Il parametro **UserPrincipalName** di Bob Taylor viene configurato come **bobt@contoso.com**.
6. **Bob Taylor** è hello seguenti valori per hello **ProxyAddresses** attributo i. smtp:bobt@contoso.com ii. smtp:bob.taylor@contoso.com
7. L'oggetto di Bob Taylor viene sincronizzato correttamente con Azure AD.
8. Amministrazione deciso tooupdate Bob Taylor **ProxyAddresses** attributo con il valore seguente hello: i. **smtp:bob@contoso.com**
9. Azure Active Directory tenterà oggetto di tooupdate Bob Taylor in Azure AD con hello di sopra di valore, ma che operazione avrà esito negativo come valore ProxyAddresses è già assegnato tooBob Smith, risultante in errore "AttributeValueMustBeUnique".

#### <a name="how-toofix-attributevaluemustbeunique-error"></a>Come toofix AttributeValueMustBeUnique errore
la causa più comune per hello AttributeValueMustBeUnique errore Hello è due oggetti con diversi SourceAnchor \(immutableId\) hanno hello stesso valore per hello ProxyAddresses e/o gli attributi UserPrincipalName. In ordine toofix AttributeValueMustBeUnique errore

1. Identificare proxyAddresses hello duplicato, userPrincipalName o un altro valore di attributo che ha causato l'errore hello. Inoltre di identificare quali due \(più\) gli oggetti coinvolti in conflitto hello. report generato da Hello [Azure AD Connect Health per la sincronizzazione](https://aka.ms/aadchsyncerrors) consentono di identificare hello due oggetti.
2. Identificare l'oggetto deve continuare valore hello duplicato toohave e non l'oggetto.
3. Rimuovere il valore di hello duplicata dall'oggetto hello che non dovrebbe essere tale valore. Si noti che sarà necessario apportare hello nella directory hello in oggetto hello proviene da modificare. In alcuni casi, potrebbe essere toodelete uno degli oggetti hello in conflitto.
4. Se sono state hello modificare in hello in Active Directory locale, consentire hello sincronizzazione Azure AD Connect modificare per hello tooget di errore predefinito.

#### <a name="related-articles"></a>Articoli correlati
-[Gli attributi duplicati o non validi impediscono la sincronizzazione delle directory in Office 365](https://support.microsoft.com/en-us/kb/2647098)

## <a name="data-validation-failures"></a>Errori di convalida dei dati
### <a name="identitydatavalidationfailed"></a>IdentityDataValidationFailed
#### <a name="description"></a>Descrizione
Azure Active Directory applica diverse restrizioni sui dati hello stesso prima di consentire che toobe dati scritti nella directory hello. Si tratta di tooensure che gli utenti possono ottenere esperienze di possibili migliore hello durante l'utilizzo di applicazioni hello che dipendono da tali dati.

#### <a name="scenarios"></a>Scenari
a. valore dell'attributo UserPrincipalName Hello contiene caratteri non valido o supportato.
b. attributo UserPrincipalName Hello non segue il formato richiesto di hello.

#### <a name="how-toofix-identitydatavalidationfailed-error"></a>Come toofix IdentityDataValidationFailed errore
a. Verificare che tale attributo userPrincipalName hello è supportato caratteri e il formato richiesto.

#### <a name="related-articles"></a>Articoli correlati
* [Preparare gli utenti tooprovision tramite la sincronizzazione di directory tooOffice 365](https://support.office.com/en-us/article/Prepare-to-provision-users-through-directory-synchronization-to-Office-365-01920974-9e6f-4331-a370-13aea4e82b3e)

### <a name="federateddomainchangeerror"></a>FederatedDomainChangeError
#### <a name="description"></a>Descrizione
Questo è un caso specifico che comporta un **"FederatedDomainChangeError"** errore di sincronizzazione quando suffisso hello di UserPrincipalName dell'utente viene modificato da un dominio federato di tooanother dominio federato.

#### <a name="scenarios"></a>Scenari
Per un utente sincronizzato, il suffisso di UserPrincipalName hello è stato modificato da un dominio federato in tooanother dominio federato in locale. Ad esempio, *UserPrincipalName = bob@contoso.com*  è stato modificato troppo*UserPrincipalName = bob@fabrikam.com* .

#### <a name="example"></a>Esempio
1. Bob Smith, un account per Contoso.com, viene aggiunto come nuovo utente in Active Directory con hello UserPrincipalNamebob@contoso.com
2. Bob Sposta tooa diverse divisioni di Contoso.com denominato Fabrikam.com e il suo UserPrincipalName viene modificatotoobob@fabrikam.com
3. Entrambi i domini di contoso.com e fabrikam.com sono domini federati con Azure Active Directory.
4. L'attributo userPrincipalName di Bob non viene aggiornato e si verifica l'errore di sincronizzazione "FederatedDomainChangeError".

#### <a name="how-toofix"></a>Come toofix
Se il suffisso di UserPrincipalName dell'utente è stato aggiornato da bob @**contoso.com** toobob @**fabrikam.com**, dove entrambi **contoso.com** e **fabrikam.com** sono **domini federati**, seguire questi errori di sincronizzazione hello toofix passaggi

1. Aggiornamento UserPrincipalName dell'utente hello in Azure AD da bob@contoso.com toobob@contoso.onmicrosoft.com. È possibile utilizzare hello comando di PowerShell con hello modulo Azure AD PowerShell seguente:`Set-MsolUserPrincipalName -UserPrincipalName bob@contoso.com -NewUserPrincipalName bob@contoso.onmicrosoft.com`
2. Consente la sincronizzazione tooattempt ciclo hello successiva sincronizzazione. Questa sincronizzazione dell'ora correttamente e verrà effettuato l'aggiornamento hello UserPrincipalName di Bob toobob@fabrikam.com come previsto.

#### <a name="related-articles"></a>Articoli correlati
* [Le modifiche non sono sincronizzate dallo strumento di sincronizzazione di Azure Active Directory hello dopo aver modificato hello UPN di un toouse di account utente diverso dominio federato](https://support.microsoft.com/en-us/help/2669550/changes-aren-t-synced-by-the-azure-active-directory-sync-tool-after-you-change-the-upn-of-a-user-account-to-use-a-different-federated-domain)

## <a name="largeobject"></a>LargeObject
### <a name="description"></a>Descrizione
Quando un attributo supera hello consentito limite delle dimensioni, il limite di lunghezza o il limite di conteggio impostato dallo schema di Active Directory di Azure, hello sincronizzazione operazione comporta hello **LargeObject** o **ExceededAllowedLength** errore di sincronizzazione. Questo errore si verifica in genere per gli attributi seguenti hello

* userCertificate
* userSMIMECertificate
* thumbnailPhoto
* proxyAddresses

### <a name="possible-scenarios"></a>Scenari possibili
1. Attributo userCertificate Bob archivia troppi tooBob assegnare certificati. tra i quali possono esserci certificati scaduti o meno recenti. limite rigido Hello è 15 certificati. Per ulteriori informazioni su come toohandle LargeObject errori con userCertificate attributo, fare riferimento tooarticle [LargeObject gestione degli errori di attributo userCertificate](active-directory-aadconnectsync-largeobjecterror-usercertificate.md).
2. Attributo userSMIMECertificate Bob archivia troppi tooBob assegnare certificati. tra i quali possono esserci certificati scaduti o meno recenti. limite rigido Hello è 15 certificati.
3. ThumbnailPhoto Bob impostata in Active Directory è troppo grande toobe sincronizzati in Azure AD.
4. Durante il popolamento automatico dell'attributo ProxyAddresses hello in Active Directory, un oggetto ha troppi ProxyAddresses assegnato.

### <a name="how-toofix"></a>Come toofix
1. Verificare che tale attributo hello causa l'errore hello rientri hello limite consentito.

## <a name="related-links"></a>Collegamenti correlati
* [Individuare oggetti Active Directory in Centro di amministrazione di Active Directory](https://technet.microsoft.com/library/dd560661.aspx)
* [Come tooquery Azure Active Directory per un oggetto usando Azure Active Directory PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx)
