---
title: 'Azure AD Connect: Cronologia delle versioni | Microsoft Docs'
description: Questo articolo elenca tutte le versioni di Azure AD Connect e Azure AD Sync
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: ef2797d7-d440-4a9a-a648-db32ad137494
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: d55cecf20abdf1637f0537e63a3dba5992a68741
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-version-release-history"></a>Azure AD Connect: Cronologia delle versioni
Il team di Azure Active Directory (Azure AD) aggiorna regolarmente Azure AD Connect con nuove funzionalità. Le nuove funzionalità potrebbero non essere disponibili in tutti i paesi.

Lo scopo di questo articolo è consentire agli utenti di esaminare le versioni rilasciate e verificare l'opportunità di effettuare l'aggiornamento alla versione più recente.

Di seguito è riportato un elenco degli argomenti correlati:


Argomento |  Dettagli
--------- | --------- |
Passaggi da eseguire per l'aggiornamento da Azure AD Connect | Metodi per [eseguire l'aggiornamento da una versione precedente alla versione più recente](active-directory-aadconnect-upgrade-previous-version.md) di Azure AD Connect.
Autorizzazioni necessarie | Per le autorizzazioni necessarie per applicare un aggiornamento, vedere [account e autorizzazioni](./active-directory-aadconnect-accounts-permissions.md#upgrade).
Scaricare| [Scaricare Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771).

## <a name="115610"></a>1.1.561.0
Stato: 23 luglio 2017

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Problema risolto

* È stato risolto un problema che causava la rimozione della regola di sincronizzazione predefinita "Uscita ad Active Directory - Utente ImmutableId":

  * Il problema si verifica quando viene aggiornato Azure AD Connect o quando l'opzione dell’attività *Aggiorna configurazione di sincronizzazione* nella procedura guidata di AD Azure Connect viene usata per aggiornare la configurazione di sincronizzazione di Azure AD Connect.
  
  * Questa regola di sincronizzazione è applicabile ai clienti che hanno attivato la [funzione msDS-ConsistencyGuid come ancoraggio di origine](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). Questa funzione è stata introdotta nella versione 1.1.524.0 e successive. Quando la regola di sincronizzazione viene rimossa, Azure AD Connect non può più popolare l'attributo locale ms-DS-ConsistencyGuid di Active Directory con il valore dell'attributo ObjectGuid. Ciò non impedisce il provisioning di nuovi utenti in Azure AD.
  
  * La correzione assicura che la regola di sincronizzazione non venga più rimossa durante l'aggiornamento o durante la modifica della configurazione, purché la funzione sia abilitata. Per i clienti esistenti interessati da questo problema, la correzione assicura inoltre che la regola di sincronizzazione venga nuovamente aggiunta dopo l'aggiornamento a questa versione di Azure AD Connect.

* È stato risolto un problema che imposta la precedenza delle regole di sincronizzazione predefinite a un valore minore di 100:

  * in generale, i valori di priorità 0 - 99 sono riservati alle regole di sincronizzazione personalizzate. Durante l'aggiornamento, vengono aggiornati i valori di precedenza delle regole di sincronizzazione predefinite per implementare le modifiche alle regole di sincronizzazione. A causa di questo problema, può essere assegnato un valore di precedenza alle regole di sincronizzazione predefinite minore di 100.
  
  * La correzione impedisce che il problema si verifichi durante l'aggiornamento. Tuttavia, non verranno ripristinati i valori di priorità per i clienti esistenti che sono stati interessati dal problema. Verrà fornita in futuro una correzione separata per facilitare il ripristino.

* È stato risolto un problema che nella [schermata di dominio e filtro dell’unità organizzativa](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) della procedura guidata di AD Azure Connect mostra l’opzione *Sincronizza tutti i domini e le unità organizzative* come selezionata, anche se è abilitato il filtro basato sulle unità organizzative.

*   È stato risolto un problema che causava la comparsa di un errore nella [schermata Configura partizioni di Directory](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) all’interno del Synchronization Service Manager quando si faceva clic sul pulsante *Aggiorna*. Il messaggio di errore è *"Si è verificato un errore durante l'aggiornamento dei domini: impossibile eseguire il cast dell'oggetto di tipo 'System.Collections.ArrayList' al tipo 'Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject'."* L'errore si verifica quando il nuovo dominio di Active Directory è stato aggiunto a una foresta di Active Directory esistente e si sta tentando di aggiornare Azure AD Connect con il pulsante Aggiorna.

#### <a name="new-features-and-improvements"></a>Miglioramenti e nuove funzionalità

* La [funzionalità di aggiornamento automatico](active-directory-aadconnect-feature-automatic-upgrade.md) è stata ampliata per supportare i clienti con le seguenti configurazioni:
  * È stata abilitata la funzionalità di writeback dei dispositivi.
  * È stata abilitata la funzionalità di writeback dei gruppi.
  * L'installazione non è un aggiornamento delle impostazioni rapide o di DirSync.
  * Il metaverse include più di 100.000 oggetti.
  * Viene stabilita la connessione a più foreste. L'installazione rapida si connette a una sola foresta.
  * L'account AD Connect non è più l'account MSOL_ predefinito.
  * Il server è in modalità di staging.
  * È stata abilitata la funzionalità di writeback degli utenti.
  
  >[!NOTE]
  >L'espansione dell'ambito di applicazione della funzionalità di aggiornamento automatico interessa i clienti di Azure AD Connect con build 1.1.105.0 e successive. Se non si desidera l'aggiornamento automatico del server di Azure AD Connect, è necessario eseguire il seguente cmdlet nel server di Azure AD Connect: `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`. Per maggiori informazioni su come abilitare/disabilitare l'aggiornamento automatico, vedere l'articolo [Azure AD Connect: aggiornamento automatico](active-directory-aadconnect-feature-automatic-upgrade.md).

## <a name="115580"></a>1.1.558.0
Stato: non verrà rilasciato. Le modifiche apportate a questa build sono incluse nella versione 1.1.561.0.

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Problema risolto

* È stato risolto un problema che causava la rimozione della regola di sincronizzazione predefinita "Uscita ad Active Directory - Utente ImmutableId" in caso di aggiornamento della configurazione del filtro basato sulle unità organizzative. Questa regola di sincronizzazione è richiesta per la [funzione msDS-ConsistencyGuid come ancoraggio di origine](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor).

* È stato risolto un problema che nella [schermata di dominio e filtro dell’unità organizzativa](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) della procedura guidata di AD Azure Connect mostra l’opzione *Sincronizza tutti i domini e le unità organizzative* come selezionata, anche se è abilitato il filtro basato sulle unità organizzative.

*   È stato risolto un problema che causava la comparsa di un errore nella [schermata Configura partizioni di Directory](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) all’interno del Synchronization Service Manager quando si faceva clic sul pulsante *Aggiorna*. Il messaggio di errore è *"Si è verificato un errore durante l'aggiornamento dei domini: impossibile eseguire il cast dell'oggetto di tipo 'System.Collections.ArrayList' al tipo 'Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject'."* L'errore si verifica quando il nuovo dominio di Active Directory è stato aggiunto a una foresta di Active Directory esistente e si sta tentando di aggiornare Azure AD Connect con il pulsante Aggiorna.

#### <a name="new-features-and-improvements"></a>Miglioramenti e nuove funzionalità

* La [funzionalità di aggiornamento automatico](active-directory-aadconnect-feature-automatic-upgrade.md) è stata ampliata per supportare i clienti con le seguenti configurazioni:
  * È stata abilitata la funzionalità di writeback dei dispositivi.
  * È stata abilitata la funzionalità di writeback dei gruppi.
  * L'installazione non è un aggiornamento delle impostazioni rapide o di DirSync.
  * Il metaverse include più di 100.000 oggetti.
  * Viene stabilita la connessione a più foreste. L'installazione rapida si connette a una sola foresta.
  * L'account AD Connect non è più l'account MSOL_ predefinito.
  * Il server è in modalità di staging.
  * È stata abilitata la funzionalità di writeback degli utenti.
  
  >[!NOTE]
  >L'espansione dell'ambito di applicazione della funzionalità di aggiornamento automatico interessa i clienti di Azure AD Connect con build 1.1.105.0 e successive. Se non si desidera l'aggiornamento automatico del server di Azure AD Connect, è necessario eseguire il seguente cmdlet nel server di Azure AD Connect: `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`. Per maggiori informazioni su come abilitare/disabilitare l'aggiornamento automatico, vedere l'articolo [Azure AD Connect: aggiornamento automatico](active-directory-aadconnect-feature-automatic-upgrade.md).

## <a name="115570"></a>1.1.557.0
Stato: luglio 2017

>[!NOTE]
>Questa build non è disponibile ai clienti tramite la funzionalità di aggiornamento automatico di Azure AD Connect.

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Problema risolto
* È stato risolto un problema relativo al cmdlet Initialize-ADSyncDomainJoinedComputerSync a causa del quale il dominio verificato configurato nell'oggetto del punto di connessione del servizio esistente viene modificato anche se è ancora un dominio valido. Questo problema si verifica quando il tenant di Azure AD ha più domini verificati che possono essere usati per configurare il punto di connessione del servizio.

#### <a name="new-features-and-improvements"></a>Miglioramenti e nuove funzionalità
* Il writeback delle password è ora disponibile per l'anteprima con il cloud di Microsoft Azure per enti pubblici e Microsoft Cloud Germany. Per altre informazioni sul supporto di Azure AD Connect per le diverse istanze del servizio, vedere l'articolo [Azure AD Connect: Considerazioni speciali per le istanze](active-directory-aadconnect-instances.md).

* Il cmdlet Initialize-ADSyncDomainJoinedComputerSync include ora un nuovo parametro facoltativo denominato AzureADDomain che consente di specificare il dominio verificato da usare per configurare il punto di connessione del servizio.

### <a name="pass-through-authentication"></a>Autenticazione pass-through

#### <a name="new-features-and-improvements"></a>Miglioramenti e nuove funzionalità
* Il nome dell'agente necessario per l'autenticazione pass-through è stato modificato da *connettore del proxy di applicazione di Microsoft Azure AD* ad *agente di autenticazione di Microsoft Azure AD Connect*.

* Quando si abilita l'autenticazione pass-through, la sincronizzazione degli hash delle password non viene più abilitata per impostazione predefinita.


## <a name="115530"></a>1.1.553.0
Stato: giugno 2017

> [!IMPORTANT]
> Questa build introduce modifiche alle regole dello schema e della sincronizzazione. Il servizio di sincronizzazione Azure AD Connect attiva i passaggi di importazione e sincronizzazione completa dopo l'aggiornamento. Di seguito vengono descritti i dettagli delle modifiche. Per rinviare temporaneamente i passaggi di importazione e sincronizzazione completa dopo l'aggiornamento, vedere l'articolo [How to defer full synchronization after upgrade](active-directory-aadconnect-upgrade-previous-version.md#how-to-defer-full-synchronization-after-upgrade) (Come rinviare la sincronizzazione completa dopo l'aggiornamento).
>
>

### <a name="azure-ad-connect-sync"></a>Servizio di sincronizzazione Azure AD Connect

#### <a name="known-issue"></a>Problema noto
* Un problema interessa i clienti che usano il [filtro basato su unità organizzativa](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) con il servizio di sincronizzazione Azure AD Connect. Quando si accede alla [pagina Filtro di domini e unità organizzative](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) della procedura guidata di Azure AD Connect, è previsto il comportamento seguente:
  * Se il filtro basato su unità organizzativa è abilitato, è selezionata l'opzione **Sincronizza le unità organizzative e i domini selezionati**.
  * In caso contrario, è selezionata l'opzione **Sincronizza tutti i domini e le unità organizzative**.

A causa del problema, l'opzione **Sincronizza tutti i domini e le unità organizzative** rimane sempre selezionata quando si esegue la procedura guidata.  Ciò si verifica anche se in precedenza è stato configurato il filtro basato su unità organizzativa. Prima di salvare le modifiche alla configurazione di AAD Connect, assicurarsi che l'opzione **Sincronizza le unità organizzative e i domini selezionati** sia selezionata e verificare che tutte le unità organizzative da sincronizzare siano nuovamente abilitate. In caso contrario, il filtro basato su unità organizzativa verrà disabilitato.

#### <a name="fixed-issues"></a>Problemi risolti

* È stato risolto un problema relativo al writeback delle password che consente a un amministratore di Azure AD di reimpostare la password di un account utente AD locale con privilegi. Il problema si verifica quando ad Azure AD Connect viene concessa l'autorizzazione di reimpostare la password per l'account con privilegi. Il problema viene risolto in questa versione di Azure AD Connect consentendo a un amministratore di Azure AD di reimpostare la password di un account utente AD locale con privilegi solo se è il proprietario di tale account. Per altre informazioni, vedere [Security Advisory 4033453](https://technet.microsoft.com/library/security/4033453) (Avviso di sicurezza 4033453).

* È stato risolto un problema relativo alla funzionalità [msDS-ConsistencyGuid come sourceAnchor](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) per cui Azure AD Connect non esegue il writeback nell'attributo msDS-ConsistencyGuid di Active Directory locale. Il problema si verifica quando sono state aggiunte più foreste di Active Directory locali ad Azure AD Connect e l'opzione *Le identità utente sono presenti in più directory* è selezionata. Quando viene usato questo tipo di configurazione, le regole di sincronizzazione risultanti non popolano l'attributo sourceAnchorBinary nel metaverse. L'attributo sourceAnchorBinary viene usato come origine per l'attributo msDS-ConsistencyGuid. Il writeback nell'attributo ms-DSConsistencyGuid non viene pertanto eseguito. Per risolvere il problema, le regole di sincronizzazione seguenti sono state aggiornate in modo da garantire che l'attributo sourceAnchorBinary nel metaverse sia sempre popolato:
  * In from AD - InetOrgPerson AccountEnabled.xml
  * In from AD - InetOrgPerson Common.xml
  * In from AD - User AccountEnabled.xml
  * In from AD - User Common.xml
  * In from AD - User Join SOAInAAD.xml

* Nelle versioni precedenti, anche se la funzionalità [msDS-ConsistencyGuid come sourceAnchor](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) non è abilitata, la regola di sincronizzazione "Out to AD - User ImmutableId" viene comunque aggiunta ad Azure AD Connect. L'effetto non è grave e il writeback dell'attributo msDS-ConsistencyGuid non viene eseguito. Per evitare confusione, è stata introdotta la logica per garantire che la regola di sincronizzazione venga aggiunta solo quando la funzionalità è abilitata.

* È stato risolto un problema che non consente la sincronizzazione degli hash delle password generando l'evento di errore 611. Questo problema si verifica dopo che uno o più controller di dominio sono stati rimossi dall'istanza di AD locale. Alla fine di ogni ciclo di sincronizzazione delle password, il cookie di sincronizzazione emesso dall'istanza di AD locale contiene gli ID di chiamata dei controller di dominio rimossi con numero di sequenza di aggiornamento (USN) pari a 0. Gestione sincronizzazione password non è in grado di salvare in modo permanente il cookie di sincronizzazione contenente il valore USN 0 e quindi la sincronizzazione non riesce con evento di errore 611. Durante il successivo ciclo di sincronizzazione, Gestione sincronizzazione password riutilizza l'ultimo cookie di sincronizzazione persistente che non contiene il valore USN 0. In questo modo vengono sincronizzate nuovamente le stesse modifiche alle password. Con questa correzione, Gestione sincronizzazione password salva correttamente il cookie di sincronizzazione in modo permanente.

* Nelle versioni precedenti, anche se l'aggiornamento automatico è stato disabilitato tramite il cmdlet Set-ADSyncAutoUpgrade, il processo di aggiornamento automatico continua a verificare periodicamente la presenza di aggiornamenti e si basa sul programma di installazione scaricato per rispettare lo stato di disabilitazione. Con questa correzione, il processo di aggiornamento automatico non esegue più il controllo periodico degli aggiornamenti. La correzione viene applicata quando viene eseguito il programma di installazione degli aggiornamenti per la versione corrente di Azure AD Connect.

#### <a name="new-features-and-improvements"></a>Miglioramenti e nuove funzionalità

* Nelle versioni precedenti la funzionalità [msDS-ConsistencyGuid come sourceAnchor](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) è disponibile solo per le nuove distribuzioni. Ora questa funzionalità è disponibile per le distribuzioni esistenti. Più in particolare:
  * Per accedere alla funzionalità, avviare la procedura guidata di Azure AD Connect e scegliere l'opzione *Update Source Anchor* (Aggiorna ancoraggio di origine).
  * Questa opzione è visibile solo per le distribuzioni esistenti che usano objectGuid come attributo sourceAnchor.
  * Quando si configura l'opzione, la procedura guidata controlla lo stato dell'attributo msDS-ConsistencyGuid nell'istanza di Active Directory locale. Se l'attributo non è configurato in nessun oggetto utente nella directory, la procedura usa l'attributo msDS-ConsistencyGuid come attributo sourceAnchor. Se invece l'attributo è configurato in uno o più oggetti utente nella directory, la procedura deduce che l'attributo è usato da altre applicazioni e non è adatto come attributo sourceAnchor e quindi impedisce la modifica dell'ancoraggio di origine. Se si è certi che l'attributo non è usato dalle applicazioni esistenti, è necessario contattare il supporto tecnico per informazioni su come eliminare l'errore.

* Per quanto riguarda l'attributo **userCertificate** degli oggetti dispositivo, Azure AD Connect esegue ora la ricerca dei valori di certificato necessari per [Connettere dispositivi aggiunti a un dominio ad Azure AD in ambiente Windows 10](https://docs.microsoft.com/azure/active-directory/active-directory-azureadjoin-devices-group-policy) ed esclude i valori restanti prima della sincronizzazione con Azure AD. Per abilitare questo comportamento, è stata aggiornata la regola di sincronizzazione predefinita "Out to AAD - Device Join SOAInAD".

* Azure AD Connect supporta ora il writeback dell'attributo **cloudPublicDelegates** di Exchange Online nell'attributo **publicDelegates** di Active Directory locale. Per effetto di questo aggiornamento, in una cassetta postale di Exchange Online possono essere concessi i diritti SendOnBehalfTo agli utenti con cassette postali di Exchange locali. Per supportare questa funzionalità, è stata introdotta una nuova regola di sincronizzazione predefinita "Out to AD - User Exchange Hybrid PublicDelegates writeback". Questa regola di sincronizzazione viene aggiunta ad Azure AD Connect solo quando la funzionalità di distribuzione ibrida di Exchange è abilitata.

*   Azure AD Connect supporta ora la sincronizzazione dell'attributo **altRecipient** da Azure AD. Per supportare questa modifica, sono state aggiornate le regole di sincronizzazione predefinite seguenti in modo da includere il flusso di attributi necessario:
  * In from AD – User Exchange
  * Out to AAD - User ExchangeOnline
  
* L'attributo **cloudSOAExchMailbox** nel metaverse indica se un determinato utente dispone di una cassetta postale di Exchange Online. La relativa definizione è stata aggiornata in modo da includere altri RecipientDisplayTypes di Exchange Online come cassette postali di sala conferenze e attrezzature. Per abilitare questa modifica, la definizione dell'attributo cloudSOAExchMailbox, presente nella regola di sincronizzazione predefinita "In from AAD - User Exchange Hybrid" è stata aggiornata da:

```
CBool(IIF(IsNullOrEmpty([cloudMSExchRecipientDisplayType]),NULL,BitAnd([cloudMSExchRecipientDisplayType],&amp;HFF) = 0))
```

... a:

```
CBool(
  IIF(IsPresent([cloudMSExchRecipientDisplayType]),(
    IIF([cloudMSExchRecipientDisplayType]=0,True,(
      IIF([cloudMSExchRecipientDisplayType]=2,True,(
        IIF([cloudMSExchRecipientDisplayType]=7,True,(
          IIF([cloudMSExchRecipientDisplayType]=8,True,(
            IIF([cloudMSExchRecipientDisplayType]=10,True,(
              IIF([cloudMSExchRecipientDisplayType]=16,True,(
                IIF([cloudMSExchRecipientDisplayType]=17,True,(
                  IIF([cloudMSExchRecipientDisplayType]=18,True,(
                    IIF([cloudMSExchRecipientDisplayType]=1073741824,True,(
                       IF([cloudMSExchRecipientDisplayType]=1073741840,True,False)))))))))))))))))))),False))

```

* È stato aggiunto il set seguente di funzioni compatibili con X509Certificate2 per la creazione di espressioni di regole di sincronizzazione per gestire i valori di certificato nell'attributo userCertificate:

    ||||
    | --- | --- | --- |
    |CertSubject|CertIssuer|CertKeyAlgorithm|
    |CertSubjectNameDN|CertIssuerOid|CertNameInfo|
    |CertSubjectNameOid|CertIssuerDN|IsCert|
    |CertFriendlyName|CertThumbprint|CertExtensionOids|
    |CertFormat|CertNotAfter|CertPublicKeyOid|
    |CertSerialNumber|CertNotBefore|CertPublicKeyParametersOid|
    |CertVersion|CertSignatureAlgorithmOid|Select|
    |CertKeyAlgorithmParams|CertHashString|Where|
    |||With|

* Le modifiche seguenti dello schema sono state introdotte per consentire ai clienti di creare regole di sincronizzazione personalizzate per includere nel flusso gli attributi sAMAccountName, domainNetBios e domainFQDN per gli oggetti gruppo e l'attributo distinguishedName per gli oggetti utente:

  * Gli attributi seguenti sono stati aggiunti allo schema Metaverse:
    * Group: AccountName
    * Group: domainNetBios
    * Group: domainFQDN
    * Person: distinguishedName

  * Gli attributi seguenti sono stati aggiunti allo schema di Azure AD Connector:
    * Group: OnPremisesSamAccountName
    * Group: NetBiosName
    * Group: DnsDomainName
    * User: OnPremisesDistinguishedName

* Lo script del cmdlet ADSyncDomainJoinedComputerSync include ora un nuovo parametro facoltativo denominato AzureEnvironment. Il parametro viene usato per specificare l'area in cui è ospitato il tenant di Azure Active Directory corrispondente. I valori validi includono:
  * AzureCloud (predefinito)
  * AzureChinaCloud
  * AzureGermanyCloud
  * USGovernment
 
* L'editor delle regole di sincronizzazione è stato aggiornato in modo da usare Join (anziché Provision) come valore predefinito del tipo di collegamento durante la creazione di regole di sincronizzazione.

### <a name="ad-fs-management"></a>Gestione di AD FS

#### <a name="issues-fixed"></a>Problemi risolti

* Gli URL seguenti sono nuovi endpoint di WS-Federation introdotti da Azure AD per migliorare la resilienza in caso di interruzione dell'autenticazione e verranno aggiunti alla configurazione locale del trust della relying party di AD FS:
  * https://ests.login.microsoftonline.com/login.srf
  * https://stamp2.login.microsoftonline.com/login.srf
  * https://ccs.login.microsoftonline.com/login.srf
  * https://ccs-sdf.login.microsoftonline.com/login.srf
  
* È stato risolto un problema a causa del quale AD FS genera un valore di attestazione non corretto per IssuerID. Il problema si verifica se sono presenti più domini verificati nel tenant di Azure AD e il suffisso di dominio dell'attributo userPrincipalName usato per generare l'attestazione IssuerID include almeno 3 livelli, ad esempio johndoe@us.contoso.com. Il problema viene risolto aggiornando l'espressione regolare usata dalle regole di attestazione.

#### <a name="new-features-and-improvements"></a>Miglioramenti e nuove funzionalità
* Nelle versioni precedenti la funzionalità di gestione dei certificati AD FS fornita da Azure AD Connect può essere usata solo con farm AD FS gestite tramite Azure AD Connect. È ora possibile usare la funzionalità con farm AD FS che non sono gestite tramite Azure AD Connect.

## <a name="115240"></a>1.1.524.0
Data di rilascio: maggio 2017

> [!IMPORTANT]
> Questa build introduce modifiche alle regole dello schema e della sincronizzazione. Dopo l'aggiornamento, il servizio di sincronizzazione Azure AD Connect attiva i passaggi di importazione e sincronizzazione completa. Di seguito vengono descritti i dettagli delle modifiche.
>
>

**Problemi risolti:**

Servizio di sincronizzazione Azure AD Connect

* È stato risolto il problema che causa l'aggiornamento automatico sul server di Azure AD Connect, anche se l'utente ha disabilitato la funzionalità usando il cmdlet Set-ADSyncAutoUpgrade. Con questa correzione, il processo di aggiornamento automatico sul server controlla periodicamente la presenza di aggiornamenti, ma il programma di installazione scaricato rispetta la configurazione di Aggiornamento automatico.
* Durante l'aggiornamento sul posto di DirSync, Azure AD Connect crea un account di servizio Azure AD che viene usato dal connettore Azure AD per la sincronizzazione con Azure AD. Dopo aver creato l'account, Azure AD Connect esegue l'autenticazione in Azure AD tramite l'account. In alcuni casi, l'autenticazione non riesce a causa di problemi temporanei, che a loro volta, durante l'aggiornamento sul posto di DirSync, causano l'errore: *"Errore di l'esecuzione dell'attività di configurazione della sincronizzazione AAD: AADSTS50034. Per accedere a questa applicazione, l'account deve essere aggiunto alla directory xxx.onmicrosoft.com."* Per migliorare la flessibilità dell'aggiornamento di DirSync, Azure AD Connect ritenta il passaggio di autenticazione.
* Un problema con la build 443 causa la riuscita dell'aggiornamento sul posto di DirSync, ma i profili di esecuzione necessari per la sincronizzazione delle directory non vengono creati. La logica di correzione è inclusa in questa build di Azure AD Connect. Quando si esegue l'aggiornamento a questa build, Azure AD Connect rileva i profili di esecuzione mancanti e li crea.
* È stato risolto il problema che non consente la riuscita del processo di sincronizzazione delle password di avvio con ID evento 6900. Viene visualizzato l'errore *"È già stato aggiunto un elemento con la stessa chiave"*. Questo problema si verifica quando si aggiorna la configurazione del filtro dell'unità organizzativa per includere una partizione di configurazione di AD. Per risolvere il problema, il processo di sincronizzazione delle password ora sincronizza le modifiche delle password solo dalle partizioni di dominio di AD. Le partizioni non di dominio, come la partizione di configurazione, vengono ignorate.
* Durante l'installazione rapida, Azure AD Connect crea un account AD DS locale usato dal connettore AD per comunicare con AD locale. In precedenza, veniva creato l'account con il flag PASSWD_NOTREQD impostato sull'attributo user-Account-Control e veniva impostata una password casuale per l'account. Ora Azure AD Connect rimuove in modo esplicito il flag PASSWD_NOTREQD dopo aver impostato la password dell'account.
* È stato risolto il problema che causa l'esito negativo dell'aggiornamento di DirSync. Viene visualizzato l'errore *"Si è verificato un deadlock in SQL Server mentre si tenta di acquisire un blocco di applicazione"* quando l'attributo mailNickname viene trovato nello schema di AD locale, ma non è limitato alla classe di oggetti utente di AD.
* È stato risolto il problema che causa la disattivazione automatica della funzionalità Writeback dispositivi quando un amministratore aggiorna la configurazione della sincronizzazione di Azure AD Connect usando la procedura guidata di Azure AD Connect. Ciò è causato dalla procedura guidata che esegue la verifica dei prerequisiti della configurazione della funzione Writeback dispositivi esistente in AD locale. La verifica ha esito negativo. La correzione ignora la verifica se Writeback dispositivi è stata abilitata in precedenza.
* Per configurare il filtro dell'unità organizzativa, è possibile usare la procedura guidata di Azure AD Connect oppure Synchronization Service Manager. In precedenza, se si usava la procedura guidata di Azure AD Connect per configurare il filtro dell'unità organizzativa, le nuove unità organizzative create in un secondo momento venivano incluse nella sincronizzazione delle directory. Se non si intende includere le nuove unità organizzative nella sincronizzazione, è necessario configurare il filtro delle unità usando Synchronization Service Manager. Ora è possibile ottenere lo stesso comportamento con la procedura guidata di Azure AD Connect.
* È stato risolto il problema che causa la creazione delle stored procedure necessarie da Azure AD Connect nello schema dell'amministratore dell'installazione, invece che nello schema dbo.
* È stato risolto il problema che causa l'omissione dell'attributo TrackingId restituito da Azure AD dai registri eventi del server di Azure AD Connect. Il problema si verifica se Azure AD Connect riceve un messaggio di reindirizzamento da Azure AD e non è in grado di connettersi all'endpoint specificato. TrackingId viene usato dal personale del supporto tecnico per la correlazione con i registri sul lato servizio durante la risoluzione dei problemi.
* Quando Azure AD Connect riceve l'errore LargeObject da Azure AD, genera un evento con ID evento 6941. Viene visualizzato il messaggio *"L'oggetto di cui è stato eseguito il provisioning presenta dimensioni troppo elevate. Ridurre il numero di valori attributo dell'oggetto."* Al contempo Azure AD Connect genera anche un evento fuorviante con ID evento 6900. Viene visualizzato il messaggio: *"Microsoft.Online.Coexistence.ProvisionRetryException: Impossibile comunicare con il servizio Windows Azure Active Directory."* Per evitare possibili confusioni, Azure AD Connect non genera più l'ultimo evento quando riceve l'errore LargeObject.
* È stato risolto il problema di Synchronization Service Manager che non risponde durante il tentativo di aggiornamento della configurazione del connettore LDAP generico.

**Nuove funzionalità o miglioramenti:**

Servizio di sincronizzazione Azure AD Connect
* Modifiche alle regole di sincronizzazione. Sono state implementate le modifiche alle regole di sincronizzazione seguenti:
  * È stata aggiornata la regola di sincronizzazione predefinita affinché non esporti gli attributi **userCertificate** e **userSMIMECertificate** se gli attributi hanno più di 15 valori.
  * Gli attributi di AD **employeeID** e **msExchBypassModerationLink** sono ora inclusi nel set di regole di sincronizzazione predefinito.
  * L'attributo di AD **photo** è stato rimosso dal set di regole di sincronizzazione predefinito.
  * **preferredDataLocation** è stato aggiunto allo schema di Metaverse e allo schema di AAD Connector. Gli utenti che intendono aggiornare entrambi gli attributi in Azure AD possono a tal fine implementare regole di sincronizzazione personalizzate. Per altre informazioni sull'attributo, leggere l'articolo [Servizio di sincronizzazione Azure AD Connect: procedure consigliate per modificare la configurazione predefinita. Abilitare la sincronizzazione di PreferredDataLocation](active-directory-aadconnectsync-change-the-configuration.md#enable-synchronization-of-preferreddatalocation).
  * **userType** è stato aggiunto allo schema di Metaverse e allo schema di AAD Connector. Gli utenti che intendono aggiornare entrambi gli attributi in Azure AD possono a tal fine implementare regole di sincronizzazione personalizzate.

* Azure AD Connect abilita ora automaticamente l'uso dell'attributo ConsistencyGuid come l'attributo sourceAnchor per gli oggetti AD locali. Inoltre, Azure AD Connect popola l'attributo ConsistencyGuid con il valore dell'attributo objectGuid se è vuoto. Questa funzionalità è applicabile soltanto alla nuova distribuzione. Per altre informazioni su questa funzionalità, consultare la sezione [Azure AD Connect: Concetti relativi alla progettazione - Uso di msDS-ConsistencyGuid come sourceAnchor](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor).
* È stato aggiunto il nuovo cmdlet di risoluzione dei problemi Invoke-ADSyncDiagnostics. Il cmdlet facilita la diagnosi dei problemi relativi alla sincronizzazione dell'hash delle password. Per informazioni sull'uso del cmdlet, vedere l'articolo [Risolvere i problemi di sincronizzazione della password con il servizio di sincronizzazione Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-troubleshoot-password-synchronization).
* Azure AD Connect supporta ora la sincronizzazione delle cartelle pubbliche abilitate alla posta elettronica da AD locale ad Azure AD. È possibile abilitare la funzionalità tramite la procedura guidata di Azure AD Connect, in Funzionalità facoltative. Per altre informazioni su questa funzionalità, vedere l'articolo [Office 365 Directory Based Edge Blocking support for on-premises Mail Enabled Public Folders](https://blogs.technet.microsoft.com/exchange/2017/05/19/office-365-directory-based-edge-blocking-support-for-on-premises-mail-enabled-public-folders) (Supporto del blocco Edge basato sulla directory di Office 365 per le cartelle pubbliche abilitate alla posta elettronica in locale).
* Azure AD Connect richiede un account AD DS per la sincronizzazione da AD locale. In precedenza, se era stato installato Azure AD Connect usando la modalità rapida, era possibile fornire le credenziali di un account amministratore Enterprise e Azure AD Connect creava quindi l'account Active Directory Domain Services necessario. Tuttavia, per le installazioni personalizzate e per l'aggiunta di foreste a una distribuzione esistente, era necessario invece fornire l'account Active Directory Domain Services. Ora è possibile specificare le credenziali di un account amministratore Enterprise durante un'installazione personalizzata e lasciare che Azure AD Connect crei l'account di AD DS necessario.
* Azure AD Connect supporta ora SQL AOA. È necessario abilitare SQL AOA prima di installare Azure AD Connect. Durante l'installazione, Azure AD Connect rileva se l'istanza SQL specificata è abilitata per SQL AOA oppure no. Se SQL AOA è abilitato, Azure AD Connect rileva quindi se SQL AOA è configurato per usare la replica sincrona o asincrona. Quando si configura il listener del gruppo di disponibilità, è consigliabile impostare la proprietà RegisterAllProvidersIP su 0. Ciò perché Azure AD Connect usa il client nativo di SQL per connettersi a SQL e il client nativo SQL non supporta l'uso della proprietà MultiSubNetFailover.
* Se si usa LocalDB come database di Azure AD Connect ed è stato raggiunto il limite di 10 GB, il servizio di sincronizzazione non si avvia. In precedenza, era necessario eseguire l'operazione ShrinkDatabase su LocalDB per recuperare lo spazio sufficiente per l'avvio del servizio di sincronizzazione. Dopo questa operazione, era possibile usare Synchronization Service Manager per eliminare la cronologia dell'esecuzione e recuperare spazio per il database. Ora è possibile usare il cmdlet ADSyncPurgeRunHistory per eseguire la pulizia dei dati della cronologia di esecuzione da LocalDB e recuperare spazio per il database. Questo cmdlet supporta una modalità offline (specificando il parametro -offline) che può essere usata quando il servizio di sincronizzazione non è in esecuzione. Nota: la modalità offline può essere usata solo se il servizio di sincronizzazione non è in esecuzione e se il database in uso è LocalDB.
* Per ridurre lo spazio di archiviazione necessario, Azure AD Connect consente ora di comprimere i dettagli degli errori di sincronizzazione prima di archiviarli nei database LocalDB/SQL. Durante l'aggiornamento da una versione precedente di Azure AD Connect a questa versione, Azure AD Connect esegue una singola compressione dei dettagli di errore di sincronizzazione esistenti.
* In precedenza, dopo l'aggiornamento della configurazione del filtro dell'unità organizzativa, era necessario eseguire manualmente l'importazione completa per verificare che gli oggetti esistenti fossero correttamente inclusi/esclusi dalla sincronizzazione della directory. Ora Azure AD Connect attiva automaticamente l'importazione completa durante il ciclo di sincronizzazione successivo. Inoltre, l'importazione completa viene applicata soltanto ai connettori AD interessati dall'aggiornamento. Nota: questo miglioramento è applicabile agli aggiornamenti del filtro dell'unità organizzativa, eseguiti soltanto con la procedura guidata di Azure AD Connect. Non è applicabile all'aggiornamento del filtro dell'unità organizzativa eseguito tramite Synchronization Service Manager.
* In precedenza, il filtro basato sui gruppi supportava soltanto oggetti utenti, gruppi e contatti. Ora il filtro supporta anche gli oggetti computer.
* In precedenza, era possibile eliminare i dati nello spazio connettore senza disabilitare l'utilità di pianificazione della sincronizzazione di Azure AD Connect. Ora Synchronization Service Manager blocca l'eliminazione dei dati nello spazio connettore se rileva che l'utilità di pianificazione è abilitata. Viene inoltre inviato un avviso che informa i clienti di potenziali perdite di dati se i dati nello spazio connettore vengono eliminati.
* In precedenza, era necessario disattivare la trascrizione di PowerShell affinché la procedura guidata di Azure AD Connect funzionasse correttamente. Questo problema è stato risolto parzialmente. Se si usa la procedura guidata di Azure AD Connect per gestire la configurazione della sincronizzazione, è possibile abilitare la trascrizione di PowerShell. Se si usa la procedura guidata di Azure AD Connect per gestire la configurazione di AD FS, è necessario disabilitare la trascrizione di PowerShell.



## <a name="114860"></a>1.1.486.0
Data di rilascio: aprile 2017

**Problemi risolti:**
* È stato risolto il problema di Azure AD Connect che non veniva installato correttamente nella versione localizzata di Windows Server.

## <a name="114840"></a>1.1.484.0
Data di rilascio: aprile 2017

**Problemi noti:**

* Questa versione di Azure AD Connect non viene installa correttamente se le condizioni seguenti sono tutte vere:
   1. Si sta eseguendo l'aggiornamento sul posto di DirSync o una nuova installazione di Azure AD Connect.
   2. Si sta usando una versione localizzata di Windows Server in cui il nome del gruppo Amministratori predefinito nel server non è "Administrators".
   3. Si sta usando l'istanza predefinita di SQL Server 2012 Express LocalDB installata con Azure AD Connect anziché la versione di SQL completa.

**Problemi risolti:**

Servizio di sincronizzazione Azure AD Connect
* È stato risolto il problema dell'utilità di pianificazione della sincronizzazione che ignora l'intero passaggio di sincronizzazione se a uno o più connettori manca il profilo di esecuzione della sincronizzazione. Ad esempio, tramite Synchronization Service Manager è stato aggiunto manualmente un connettore per il quale non è stato creato un profilo di importazione delta. Grazie a questa correzione si garantisce che l'utilità di pianificazione della sincronizzazione continui a eseguire l'importazione delta per gli altri connettori.
* È stato risolto il problema del servizio di sincronizzazione che arresta immediatamente l'elaborazione di un profilo di esecuzione in caso si verifichi un problema con uno dei passaggi di esecuzione. Grazie a questa correzione si garantisce che il servizio di sincronizzazione ignori il passaggio interessato e continui a elaborare il resto. Ad esempio, il profilo d'importazione delta per il connettore di Active Directory contiene più passaggi di esecuzione, uno per ogni dominio locale di Active Directory. Il servizio di sincronizzazione esegue l'importazione delta con gli altri domini di Active Directory anche se uno di essi presenta problemi di connettività di rete.
* È stato risolto un problema che ignora l'aggiornamento del connettore di Azure AD durante l'aggiornamento automatico.
* È stato risolto un problema di Azure AD Connect che determina in modo non corretto se il server è un controller di dominio durante l'installazione e che a su volta non completa l'aggiornamento di DirSync.
* È stato risolto un problema dell'aggiornamento di DirSync locale che non crea un profilo di esecuzione per il connettore di Azure AD.
* È stato risolto un problema dell'interfaccia utente di Synchronization Service Manager che non risponde durante la configurazione del connettore LDAP generico.

Gestione di AD FS.
* È stato risolto un problema della procedura guidata di Azure AD Connect che ha esito negativo se il nodo primario di AD FS è stato spostato in un altro server.

Desktop SSO
* È stato risolto un problema della procedura guidata di Azure AD Connect in cui la schermata di accesso non consente di abilitare la funzionalità Desktop SSO se è stata selezionata la sincronizzazione password come opzione di accesso durante la nuova installazione.

**Nuove funzionalità o miglioramenti:**

Servizio di sincronizzazione Azure AD Connect
* Il servizio di sincronizzazione Azure AD supporta ora l'uso di account del servizio virtuale, account del servizio gestito e account del servizio gestito del gruppo come account del servizio stesso. Si applica solo alla nuova installazione di Azure AD Connect. Durante l'installazione di Azure AD Connect:
    * Per impostazione predefinita, la procedura guidata di Azure AD Connect crea un account del servizio virtuale che usa come account del servizio.
    * Se l'installazione viene eseguita in un controller di dominio, Azure AD Connect ripete il comportamento precedente durante il quale crea una account utente di dominio e lo usa come account del servizio.
    * È possibile sostituire il comportamento predefinito specificando una delle opzioni seguenti:
      * Account del servizio gestito del gruppo
      * Account del servizio gestito
      * Account utente di dominio
      * Account utente locale
* In passato, se si eseguiva l'aggiornamento a una nuova build di Azure AD Connect contenente modifiche alle regole di aggiornamento o di sincronizzazione dei connettori, Azure AD Connect attivava un ciclo completo di sincronizzazione. Ora Azure AD Connect attiva in modo selettivo il passaggio di importazione completa solo per i connettori con modifiche alle regole di aggiornamento e il passaggio di sincronizzazione completa solo per i connettori con modifiche alle regole di sincronizzazione.
* In passato la soglia di eliminazione delle esportazioni veniva applicava solo alle esportazioni attivate tramite l'utilità di pianificazione della sincronizzazione. Ora la funzionalità è estesa e include le esportazioni che l'utente ha attivato manualmente tramite Synchronization Service Manager.
* Il tenant di Azure AD contiene una configurazione del servizio che indica se la funzionalità Sincronizzazione password è abilitata o meno per il tenant. In passato poteva capitare facilmente che Azure AD Connect eseguisse la configurazione del servizio in modo non corretto se era presente un server attivo e di gestione temporanea. Ora Azure AD Connect tenta di mantenere la configurazione del servizio coerente solo con il server di Azure AD Connect.
* Ora la procedura guidata di Azure AD Connect rileva e restituisce un avviso se in Active Directory locale non è abilitato il Cestino di AD.
* In passato, l'esportazione in Azure AD si interrompeva e non veniva completata se le dimensioni totali degli oggetti nel batch superavano una certa soglia. Ora, se si verifica tale problema, il servizio di sincronizzazione tenta di inviare nuovamente gli oggetti in batch più piccoli e separati.
* L'applicazione Synchronization Service Key Management (Gestione delle chiavi del servizio di sincronizzazione) è stata rimossa dal menu Start di Windows. La gestione della chiave di crittografia continua a essere supportata tramite l'interfaccia della riga di comando usando miiskmu.exe. Per informazioni sulla gestione della chiave di crittografia, fare riferimento all'articolo [Abandoning the Azure AD Connect Sync encryption key](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-change-serviceacct-pass#abandoning-the-azure-ad-connect-sync-encryption-key) (Abbandono della chiave di crittografia del servizio di sincronizzazione Azure AD Connect).
* In passato, se si modificava la password dell'account del servizio di sincronizzazione Azure AD Connect, il servizio di sincronizzazione non veniva avviato correttamente finché non si abbandonava la chiave di crittografia e non si reinizializzava la password dell'account del servizio. Ora non è più necessario.

Desktop SSO

* Durante la procedura guidata di Azure AD Connect non è più necessario che la porta 9090 sia aperta in rete quando si configura l'autenticazione pass-through e Desktop SSO. È necessaria solo la porta 443. 

## <a name="114430"></a>1.1.443.0
Data di rilascio: marzo 2017

**Problemi risolti:**

Servizio di sincronizzazione Azure AD Connect
* Risolto un problema che causava un errore nella procedura guidata di Azure AD Connect se il nome visualizzato di Azure AD Connector non conteneva il dominio onmicrosoft.com iniziale assegnato al tenant di Azure AD.
* Risolto un problema che causava un errore nella procedura guidata di Azure AD Connect durante la connessione al database SQL quando la password dell'account del servizio di sincronizzazione conteneva caratteri speciali come apostrofi, due punti e spazi.
* Risolto un problema che causava l'errore "The dimage has an anchor that is different than the image" (Dimage contiene un ancoraggio diverso dall'immagine) in un server Azure AD Connect in modalità di gestione temporanea, dopo aver escluso temporaneamente un oggetto AD locale dalla sincronizzazione e averlo nuovamente incluso.
* Risolto un problema che causava l'errore "The object located by DN is a phantom" (L'oggetto localizzato da DN è un fantasma) in un server Azure AD Connect in modalità di gestione temporanea, dopo aver escluso temporaneamente un oggetto AD locale dalla sincronizzazione e averlo nuovamente incluso.

Gestione di AD FS.
* Risolto un problema per cui la procedura guidata di Azure AD Connect non aggiornava la configurazione di AD FS e non impostava le attestazioni corrette nel trust della relying party dopo aver configurato un ID di accesso alternativo.
* Risolto un problema per cui la procedura guidata di Azure AD Connect non era in grado di gestire correttamente i server AD FS con account di servizio configurati usando il formato userPrincipalName invece del formato sAMAccountName.

Autenticazione pass-through
* Risolto un problema che causava un errore nella procedura guidata di Azure AD Connect se si selezionava Autenticazione pass-through ma la registrazione del relativo connettore aveva esito negativo.
* Risolto un problema che causava il bypass dei controlli di convalida da parte di Azure AD Connect sul metodo di accesso selezionato con la funzionalità Desktop SSO attivata.

Reimpostazione delle password
* Correzione di un problema che potrebbe causare il mancato tentativo di riconnessione da parte del server Azure AAD Connect, se la connessione è stata terminata da un firewall o un proxy.

**Nuove funzionalità o miglioramenti:**

Servizio di sincronizzazione Azure AD Connect
* Il cmdlet Get-ADSyncScheduler restituisce ora una nuova proprietà booleana denominata SyncCycleInProgress. Se il valore restituito è true, significa che è in corso un ciclo di sincronizzazione pianificato.
* La cartella di destinazione per archiviare i log di installazione e configurazione di Azure AD Connect è stata modificata da %localappdata%\AADConnect a %programdata%\AADConnect per migliorare l'accessibilità.

Gestione di AD FS.
* Aggiunto il supporto per l'aggiornamento del certificato SSL Farm AD FS.
* Aggiunto il supporto per la gestione di AD FS 2016.
* È ora possibile specificare un gMSA (account del servizio gestito di gruppo) durante l'installazione di AD FS.
* È ora possibile configurare SHA-256 come algoritmo di hash della firma per il trust della relying party di Azure AD.

Reimpostazione delle password
* Miglioramenti per consentire al prodotto di funzionare in ambienti con regole più severe del firewall.
* Migliore affidabilità della connessione al bus di servizio.

## <a name="113800"></a>1.1.380.0
Data di rilascio: dicembre 2016

**Problema risolto:**

* Risolto il problema secondo cui in questa build manca la regola di attestazione issuerid per Active Directory Federation Services (AD FS).

>[!NOTE]
>Questa build non è disponibile ai clienti tramite la funzionalità di aggiornamento automatico di Azure AD Connect.

## <a name="113710"></a>1.1.371.0
Data di rilascio: dicembre 2016

**Problema noto:**

* La regola di attestazione issuerid per AD FS manca in questa build. La regola di attestazione issuerid è obbligatoria se si esegue la federazione di più domini con Azure Active Directory (Azure AD). Se si utilizza Azure AD Connect per gestire la distribuzione di AD FS in locale, l'aggiornamento a questa build rimuoverà la regola di attestazione issuerid esistente dalla configurazione di AD FS. È possibile risolvere il problema aggiungendo la regola dopo l'installazione o l'aggiornamento. Per altre informazioni sull'aggiunta della regola di attestazione issuerid, fare riferimento a questo articolo in [Supporto di più domini per la federazione con Azure AD](active-directory-aadconnect-multiple-domains.md).

**Problema risolto:**

* L'installazione o l'aggiornamento di Azure AD Connect ha esito negativo se la porta 9090 non è aperta per la connessione in uscita.

>[!NOTE]
>Questa build non è disponibile ai clienti tramite la funzionalità di aggiornamento automatico di Azure AD Connect.

## <a name="113700"></a>1.1.370.0
Data di rilascio: dicembre 2016

**Problemi noti:**

* La regola di attestazione issuerid per AD FS manca in questa build. La regola di attestazione issuerid è obbligatoria se si esegue la federazione di più domini con Azure AD. Se si utilizza Azure AD Connect per gestire la distribuzione di AD FS in locale, l'aggiornamento a questa build rimuoverà la regola di attestazione issuerid esistente dalla configurazione di AD FS. È possibile risolvere il problema aggiungendo la regola dopo l'installazione o l'aggiornamento. Per altre informazioni sull'aggiunta della regola di attestazione issuerid, fare riferimento a questo articolo in [Supporto di più domini per la federazione con Azure AD](active-directory-aadconnect-multiple-domains.md).
* La porta 9090 deve essere aperta in uscita per completare l'installazione.

**Nuove funzionalità:**

* Autenticazione pass-through (anteprima).

>[!NOTE]
>Questa build non è disponibile ai clienti tramite la funzionalità di aggiornamento automatico di Azure AD Connect.

## <a name="113430"></a>1.1.343.0
Data di rilascio: novembre 2016

**Problema noto:**

* La regola di attestazione issuerid per AD FS manca in questa build. La regola di attestazione issuerid è obbligatoria se si esegue la federazione di più domini con Azure AD. Se si utilizza Azure AD Connect per gestire la distribuzione di AD FS in locale, l'aggiornamento a questa build rimuoverà la regola di attestazione issuerid esistente dalla configurazione di AD FS. È possibile risolvere il problema aggiungendo la regola dopo l'installazione o l'aggiornamento. Per altre informazioni sull'aggiunta della regola di attestazione issuerid, fare riferimento a questo articolo in [Supporto di più domini per la federazione con Azure AD](active-directory-aadconnect-multiple-domains.md).

**Problemi risolti:**

* In alcuni casi, l'installazione di Azure AD Connect, ha esito negativo perché non è possibile creare un account di servizio locale la cui password soddisfi il livello di complessità specificato dai criteri di password aziendale.
* È stato risolto un problema in cui le regole di unione non vengono rivalutate quando un oggetto nello spazio connettore viene contemporaneamente esce dall'ambito di una regola di unione ed nell'ambito di un'altra. Questa situazione può verificarsi se sono presenti due o più regole di unione, le cui condizioni di unione si escludono a vicenda.
* È stato risolto un problema in cui le regole di sincronizzazione in ingresso (di Azure AD), che non contengono regole di unione, non vengono elaborate se dispongono di valori di precedenza inferiori rispetto a quelle contenenti le regole di unione.

**Miglioramenti:**

* Aggiunta del supporto per l'installazione di Azure AD Connect in Windows Server 2016 Standard o versione successiva.
* Aggiunta del supporto per l'uso di SQL Server 2016 come database remoto per Azure AD Connect.

## <a name="112810"></a>1.1.281.0
Data di rilascio: agosto 2016

**Problemi risolti:**

* Le modifiche apportate all'intervallo di sincronizzazione non vengono applicate fino al termine del ciclo di sincronizzazione successivo.
* La procedura guidata di Azure AD Connect non accetta un account di Azure AD il cui nome utente inizi con un carattere di sottolineatura (\_).
* La procedura guidata di Azure AD Connect non riesce ad autenticare l'account Azure AD specificato se la password dell'account contiene troppi caratteri speciali. Viene visualizzato il messaggio di errore "La convalida delle credenziali non è riuscita. Si è verificato un errore imprevisto".
* La disinstallazione del server di gestione temporanea disabilita la sincronizzazione delle password nel tenant Azure AD e rende impossibile la sincronizzazione delle password con il server attivo.
* In casi rari, la sincronizzazione delle password ha esito negativo quando non sono archiviati hash password per l'utente.
* Quando il server Azure AD Connect è abilitato per la modalità di gestione temporanea, il writeback delle password non viene temporaneamente disabilitato.
* La procedura guidata di Azure AD Connect non visualizza l'effettiva configurazione della sincronizzazione delle password e del writeback delle password quando il server è in modalità di gestione temporanea. Indica sempre le due funzionalità come disabilitate.
* Le modifiche apportate alla configurazione della sincronizzazione delle password e del writeback delle password non vengono salvate in modo permanente dalla procedura guidata di Azure AD Connect quando il server è in modalità di gestione temporanea.

**Miglioramenti:**

* Aggiornamento del cmdlet Start-ADSyncSyncCycle per indicare se può avviare o meno un nuovo ciclo di sincronizzazione.
* Aggiunta del cmdlet Stop-ADSyncSyncCycle per terminare il ciclo di sincronizzazione e l'operazione in corso.
* Aggiornamento del cmdlet Stop-ADSyncScheduler per terminare il ciclo di sincronizzazione e l'operazione in corso.
* Quando si configura [Estensioni della directory](active-directory-aadconnectsync-feature-directory-extensions.md) nella procedura guidata di Azure AD Connect, è ora possibile selezionare l'attributo Azure AD di tipo "Teletex string".

## <a name="111890"></a>1.1.189.0
Data di rilascio: giugno 2016

**Problemi risolti e miglioramenti:**

* Ora Azure AD Connect può essere installato su un server conforme a FIPS.
  * Per la sincronizzazione della password, vedere [Sincronizzazione password e FIPS](active-directory-aadconnectsync-implement-password-synchronization.md#password-synchronization-and-fips).
* Risolto un problema in cui un nome NetBIOS non poteva essere risolto nel FQDN in Active Directory Connector.

## <a name="111800"></a>1.1.180.0
Data di rilascio: maggio 2016

**Nuove funzionalità:**

* Visualizza avvisi e indicazioni riguardo alla verifica dei domini se la verifica non è stata effettuata prima di eseguire Azure AD Connect.
* Aggiunto il supporto per [Microsoft Cloud Germany](active-directory-aadconnect-instances.md#microsoft-cloud-germany).
* Aggiunto il supporto per la versione più recente dell'infrastruttura [cloud di Microsoft Azure per enti pubblici](active-directory-aadconnect-instances.md#microsoft-azure-government-cloud) con nuovi requisiti per gli URL.

**Problemi risolti e miglioramenti:**

* Aggiunti i filtri all'editor delle regole di sincronizzazione per semplificare il reperimento delle regole.
* Miglioramento delle prestazioni quando si elimina uno spazio connettore.
* Risolto un problema che si verificava quando lo stesso oggetto veniva sia eliminato che aggiunto nella stessa esecuzione (elimina/aggiungi).
* Una regola di sincronizzazione disabilitata ora non riattiva più gli oggetti e gli attributi inclusi all'aggiornamento del sistema o dello schema della directory.

## <a name="111300"></a>1.1.130.0
Data di rilascio: aprile 2016

**Nuove funzionalità:**

* Aggiunto il supporto per gli attributi multivalore alle [estensioni della directory](active-directory-aadconnectsync-feature-directory-extensions.md).
* Aggiunto il supporto per altre varianti di configurazione dell' [aggiornamento automatico](active-directory-aadconnect-feature-automatic-upgrade.md) da considerare idonee per l'aggiornamento.
* Aggiunti alcuni cmdlet per l' [utilità di pianificazione personalizzata](active-directory-aadconnectsync-feature-scheduler.md#custom-scheduler).

## <a name="111190"></a>1.1.119.0
Data di rilascio: marzo 2016

**Problemi risolti:**

* È stato verificato che non sia possibile usare l'installazione rapida in Windows Server 2008 (pre-R2), poiché la sincronizzazione delle password non è supportata in questo sistema operativo.
* L'aggiornamento da DirSync con una configurazione personalizzata del filtro non funzionava come previsto.
* Durante l'aggiornamento a una versione più recente, senza modifiche alla configurazione, è consigliabile non pianificare una importazione/sincronizzazione completa.

## <a name="111100"></a>1.1.110.0
Data di rilascio: febbraio 2016

**Problemi risolti:**

* L'aggiornamento da versioni precedenti non funziona se l'installazione non viene eseguita nella cartella predefinita C:\Programmi.
* Se si esegue l'installazione e si deseleziona **Avvia il processo di sincronizzazione** al termine dell'Installazione guidata, una nuova esecuzione dell'Installazione guidata non abiliterà l'utilità di pianificazione.
* L'utilità di pianificazione non funzionerà come previsto nei server in cui il formato di data/ora non è US-en. `Get-ADSyncScheduler` non potrà restituire gli orari corretti.
* Se è stata installata una versione precedente di Azure AD Connect con AD FS come opzione di accesso e aggiornamento, non è possibile eseguire nuovamente l'installazione guidata.

## <a name="111050"></a>1.1.105.0
Data di rilascio: febbraio 2016

**Nuove funzionalità:**

* [Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) per i clienti con impostazioni rapide.
* Supporto per l'amministratore globale mediante Azure Multi-Factor Authentication e Privileged Identity Management nell'installazione guidata.
  * Se si usa Multi-Factor Authentication, è necessario impostare il proxy in modo che consenta il traffico per https://secure.aadcdn.microsoftonline-p.com.
  * Per il corretto funzionamento di Multi-Factor Authentication, è necessario aggiungere https://secure.aadcdn.microsoftonline-p.com all'elenco di siti attendibili.
* Possibilità di modificare il metodo di accesso dell'utente dopo l'installazione iniziale.
* Possibilità di usare i [filtri basati su dominio e unità organizzativa](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) nell'Installazione guidata. Ciò consente anche la connessione a foreste in cui non sono disponibili tutti i domini.
* L'[Utilità di pianificazione](active-directory-aadconnectsync-feature-scheduler.md) è incorporata nel motore di sincronizzazione.

**Funzionalità passate dal livello di anteprima al livello di disponibilità generale:**

* [Writeback dei dispositivi](active-directory-aadconnect-feature-device-writeback.md).
* [Estensioni della directory](active-directory-aadconnectsync-feature-directory-extensions.md).

**Nuove funzionalità di anteprima:**

* Il nuovo intervallo predefinito per i cicli di sincronizzazione è pari a 30 minuti. In tutte le versioni precedenti è pari a tre ore. Aggiunge il supporto per la modifica del comportamento dell' [utilità di pianificazione](active-directory-aadconnectsync-feature-scheduler.md) .

**Problemi risolti:**

* La pagina di verifica dei domini DNS non riconosceva sempre i domini.
* Richiesta di credenziali di amministratore del dominio durante la configurazione di AD FS.
* Gli account AD locali non vengono riconosciuti dall'installazione guidata se si trovano in un dominio con un albero DNS diverso da quello del dominio radice.

## <a name="1091310"></a>1.0.9131.0
Data di rilascio: dicembre 2015

**Problemi risolti:**

* La sincronizzazione delle password potrebbe non funzionare quando si modificano le password in Active Directory Domain Services (AD DS), ma funziona quando si imposta la password.
* Quando si dispone di un server proxy, l'autenticazione ad Azure AD potrebbe non riuscire durante l'installazione o se viene annullato un aggiornamento nella pagina di configurazione.
* L'aggiornamento da una versione precedente di Azure AD Connect con un'istanza completa di SQL Server avrà esito negativo se non si è SA (amministratore di sistema) in SQL Server.
* L'aggiornamento da una versione precedente di Azure AD Connect con una versione remota di SQL Server mostrerà il messaggio di errore "Impossibile accedere al database SQL di ADSync".

## <a name="1091250"></a>1.0.9125.0
Data di rilascio: novembre 2015

**Nuove funzionalità:**

* È possibile riconfigurare AD FS a trust AD Azure.
* È possibile aggiornare lo schema di Active Directory e rigenerare le regole di sincronizzazione.
* È possibile disattivare una regola di sincronizzazione.
* È possibile definire "AuthoritativeNull" come un nuovo valore letterale in una regola di sincronizzazione.

**Nuove funzionalità di anteprima:**

* [Azure AD Connect Health per la sincronizzazione](../connect-health/active-directory-aadconnect-health-sync.md).
* Supporto per la sincronizzazione della password dei [Servizi di dominio di Azure AD](../active-directory-passwords-update-your-own-password.md)

**Nuovo scenario supportato:**

* Supporta più organizzazioni di Exchange locali Per altre informazioni, vedere [Distribuzioni ibride con più foreste di Active Directory](https://technet.microsoft.com/library/jj873754.aspx).

**Problemi risolti:**

* Problemi sulla sincronizzazione delle password:
  * Un oggetto spostato dal all’esterno all’interno dell’ambito non avrà la password sincronizzata. Questo include unità Organizzativa e filtro attributi.
  * Selezione di una nuova unità Organizzativa da includere nella sincronizzazione non richiede una sincronizzazione completa della password.
  * Quando un utente disabilitato è abilitato la password non viene sincronizzata.
  * La coda di tentativi di password è infinita e il limite precedente di 5.000 oggetti da ritirare è stato rimosso.
* Impossibile connettersi ad Active Directory con livello di funzionalità foresta Windows Server 2016.
* Impossibile modificare il gruppo usato per il filtro di gruppo dopo l'installazione iniziale.
* Non si creerà un nuovo profilo utente nel server di Azure AD Connect per ogni utente che effettua una modifica della password con attivato il writeback delle password.
* Non è possibile usare valori Intero lungo negli ambiti di regole di sincronizzazione.
* La casella di controllo "writeback dispositivi" rimane disabilitata se sono presenti controller di dominio non raggiungibili.

## <a name="1086670"></a>1.0.8667.0
Data di rilascio: agosto 2015

**Nuove funzionalità:**

* L'installazione guidata di Azure AD Connect è ora localizzata in tutte le lingue in cui è disponibile Windows Server.
* È stato aggiunto il supporto per lo sblocco dell'account quando si usa la gestione delle password di Azure AD.

**Problemi risolti:**

* Si verifica un arresto anomalo dell'installazione guidata di Azure AD Connect se l'installazione viene continuata da un utente diverso da quello che l'ha avviata.
* Se una disinstallazione precedente di Azure AD Connect non riesce a disinstallare completamente il servizio di sincronizzazione Azure AD Connect, non sarà possibile effettuare la reinstallazione.
* Non è possibile installare Azure AD Connect usando l'installazione rapida se l'utente non si trova nel dominio radice della foresta o se viene usata una versione di Active Directory in una lingua diversa dall'inglese.
* Se il nome di dominio completo dell'account utente di Active Directory non può essere risolto, verrà visualizzato un messaggio di errore fuorviante analogo a "Commit dello schema non riuscito".
* Se l'account usato in Active Directory Connector viene modificato all'esterno della procedura guidata, le esecuzioni successive della procedura guidata avranno esito negativo.
* A volte non è possibile installare Azure AD Connect in un controller di dominio.
* Non è possibile abilitare e disabilitare la "Modalità di gestione temporanea" se sono stati aggiunti attributi di estensione.
* Il writeback delle password ha esito negativo in alcune configurazioni a causa di una password non valida in Active Directory Connector.
* Non è possibile aggiornare DirSync se si usa un nome distinto (DN) nel filtro di attributi.
* Utilizzo eccessivo della CPU quando si utilizza la reimpostazione della password.

**Funzionalità di anteprima rimosse:**

* La funzionalità di anteprima [Utente writeback](active-directory-aadconnect-feature-preview.md#user-writeback) è stata temporaneamente rimossa in base ai suggerimenti espressi dai clienti dell’anteprima. Verrà aggiunto di nuovo in un secondo momento, una volta valutato il feedback fornito.

## <a name="1086410"></a>1.0.8641.0
Data di rilascio: giugno 2015

**Rilascio iniziale di Azure AD Connect.**

Il nome è stato modificato da Azure AD Sync ad Azure AD Connect.

**Nuove funzionalità:**

* Installazione mediante le [impostazioni rapide](active-directory-aadconnect-get-started-express.md)
* È possibile [configurare la farm AD FS](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs)
* È possibile [aggiornare da DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md)
* [Impedire eliminazioni accidentali](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)
* Introdotta la [modalità di gestione temporanea](active-directory-aadconnectsync-operations.md#staging-mode)

**Nuove funzionalità di anteprima:**

* [Writeback degli utenti](active-directory-aadconnect-feature-preview.md#user-writeback)
* [Writeback dei gruppi](active-directory-aadconnect-feature-preview.md#group-writeback)
* [Writeback dei dispositivi](active-directory-aadconnect-feature-device-writeback.md)
* [Estensioni della directory](active-directory-aadconnect-feature-preview.md)

## <a name="104940501"></a>1.0.494.0501
Data di rilascio: maggio 2015

**Nuovo requisito:**

* Azure AD Sync richiede ora .NET Framework versione 4.5.1 per l'installazione.

**Problemi risolti:**

* Il writeback delle password da Azure AD ha esito negativo con un errore di connettività del bus di servizio.

## <a name="104910413"></a>1.0.491.0413
Data di rilascio: aprile 2015

**Problemi risolti e miglioramenti:**

* Active Directory Connector non elabora correttamente le eliminazioni se il Cestino è abilitato e sono presenti più domini nella foresta.
* Le prestazioni delle operazioni di importazione sono state migliorate per Azure Active Directory Connector.
* Quando un gruppo supera il limite per le appartenenze (per impostazione predefinita, il limite è impostato su 50.000 oggetti), viene eliminato in Azure Active Directory. Con il nuovo comportamento, il gruppo non viene eliminato, viene generato un errore e le nuove modifiche alle appartenenze non vengono esportate.
* Non è possibile effettuare il provisioning di un nuovo oggetto se nello spazio del connettore è già presente un'eliminazione a fasi con lo stesso nome di dominio.
* Alcuni oggetti sono contrassegnati per la sincronizzazione durante una sincronizzazione Delta, anche se non sono previste modifiche a fasi sull'oggetto.
* La forzatura della sincronizzazione delle password rimuove anche l'elenco dei controller di dominio preferiti.
* Si sono verificati problemi di CSExportAnalyzer con alcuni stati degli oggetti.

**Nuove funzionalità:**

* Un join può ora connettersi al tipo di oggetto "ANY" nel metaverse.

## <a name="104850222"></a>1.0.485.0222
Data di rilascio: febbraio 2015

**Miglioramenti:**

* Prestazioni migliorate per l'importazione.

**Problemi risolti:**

* La sincronizzazione delle password rispetta l'attributo cloudFiltered usato dal filtro di attributi. Gli oggetti filtrati non sono più inclusi nell'ambito per la sincronizzazione delle password.
* Nelle rare situazioni in cui la topologia include un numero elevato di controller di dominio, la sincronizzazione delle password non funziona.
* Errore di tipo "server arrestato" durante l'importazione da Azure AD Connector dopo l'abilitazione della gestione dei dispositivi in Azure AD/Intune.
* L'aggiunta di entità di protezione esterne da più domini nella stessa foresta provoca un errore di join ambiguo.

## <a name="104751202"></a>1.0.475.1202
Data di rilascio: dicembre 2014

**Nuove funzionalità:**

* È ora supportata l'esecuzione della sincronizzazione delle password con filtri basati sugli attributi. Per informazioni dettagliate, vedere [Sincronizzazione delle password con i filtri](active-directory-aadconnectsync-configure-filtering.md).
* L'attributo msDS-ExternalDirectoryObjectID viene scritto di nuovo in Active Directory. Questa funzionalità aggiunge il supporto per applicazioni di Office 365. Usa OAuth2 per accedere alle cassette postali online e locali in una distribuzione ibrida di Exchange.

**Problemi di aggiornamento risolti:**

* Nel server è disponibile una versione più recente dell'Assistente per l'accesso.
* Per l'installazione di Azure AD Sync è stato usato un percorso di installazione personalizzato.
* Un criterio di join personalizzato non valido blocca l'aggiornamento.

**Altre correzioni:**

* I problemi dei modelli per Office Pro Plus sono stati risolti.
* I problemi di installazione provocati dai nomi utente che iniziano con un trattino sono stati risolti.
* Il problema relativo alla perdita dell'impostazione sourceAnchor durante la seconda esecuzione dell'Installazione guidata è stato risolto.
* Il problema relativo alla traccia ETW per la sincronizzazione delle password è stato risolto.

## <a name="104701023"></a>1.0.470.1023
Data di rilascio: ottobre 2014

**Nuove funzionalità:**

* Sincronizzazione delle password da più istanze di Active Directory locali ad Azure AD.
* Interfaccia utente di installazione localizzata per tutte le lingue in cui è disponibile Windows Server.

**Aggiornamento da AADSync 1.0 GA**

Se è già stato installato Azure AD Sync, è necessario eseguire un'altra operazione nel caso in cui siano state modificate le regole di sincronizzazione predefinite. In seguito all'aggiornamento alla versione 1.0.470.1023, le regole di sincronizzazione modificate vengono duplicate. Per ogni regola di sincronizzazione modificata eseguire le operazioni seguenti:

1.  Trovare la regola di sincronizzazione modificata e prendere nota delle modifiche.
* Eliminare la regola di sincronizzazione.
* Trovare la nuova regola di sincronizzazione creata da Azure AD Sync e riapplicare le modifiche.

**Autorizzazioni per l'account Active Directory**

Per poter leggere gli hash delle password da Active Directory, è necessario concedere autorizzazioni aggiuntive all'account di Active Directory. Le autorizzazioni da concedere sono "Replica modifiche directory" e "Replica di tutte le modifiche directory". Per poter leggere gli hash delle password, sono necessarie entrambe le autorizzazioni.

## <a name="104190911"></a>1.0.419.0911
Data di rilascio: settembre 2014

**Rilascio iniziale di Azure AD Sync.**

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
