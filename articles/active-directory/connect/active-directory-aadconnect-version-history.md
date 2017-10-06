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
ms.openlocfilehash: b55e0f2d426e34ceef9869d5a6d1b0956d8bd076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-version-release-history"></a>Azure AD Connect: Cronologia delle versioni
il team di Azure Active Directory (Azure AD) Hello aggiorna regolarmente Azure AD Connect con nuove caratteristiche e funzionalità. Non tutti i componenti aggiuntivi sono gruppi di destinatari tooall applicabile.

Questo articolo è toohelp progettato tenere traccia delle versioni di hello che sono state rilasciate e toounderstand necessità di versione più recente di tooupdate toohello o non.

Di seguito è riportato un elenco degli argomenti correlati:


Argomento |  Dettagli
--------- | --------- |
Passaggi tooupgrade da Azure AD Connect | Diversi metodi troppo[l'aggiornamento da una precedente toohello versione più recente](active-directory-aadconnect-upgrade-previous-version.md) versione di Azure AD Connect.
Autorizzazioni necessarie | Per le autorizzazioni necessarie tooapply un aggiornamento, vedere [account e autorizzazioni](./active-directory-aadconnect-accounts-permissions.md#upgrade).
Scaricare| [Scaricare Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771).

## <a name="115610"></a>1.1.561.0
Stato: 23 luglio 2017

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Problema risolto

* Risolto un problema che ha causato il regola di sincronizzazione di out-of-box hello "Out tooAD - utente ImmutableId" toobe rimosso:

  * Hello problema si verifica quando viene aggiornato Azure AD Connect, o quando hello opzione attività *configurazione di sincronizzazione aggiornamento* in hello Azure AD Connect è configurazione di sincronizzazione tooupdate usato Azure AD Connect.
  
  * Questa regola di sincronizzazione è applicabile toocustomers che hanno attivato hello [msDS-ConsistencyGuid come funzionalità di ancoraggio di origine](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). Questa funzione è stata introdotta nella versione 1.1.524.0 e successive. Quando viene rimossa la regola di sincronizzazione hello, Azure AD Connect non è più possibile popolare locale attributo ms-DS-ConsistencyGuid di Active Directory con valore dell'attributo ObjectGuid hello. Ciò non impedisce il provisioning di nuovi utenti in Azure AD.
  
  * correzione di Hello assicura che tale regola di sincronizzazione hello non verrà rimosso durante l'aggiornamento o durante la modifica della configurazione, fino a quando è abilitata la funzionalità di hello. Per i clienti esistenti interessati da questo problema, correggere hello garantisce anche la regola di sincronizzazione hello viene aggiunto dopo l'aggiornamento di versione toothis di Azure AD Connect.

* Risolto un problema che determina le regole di sincronizzazione out-of-box toohave valore di precedenza che è minore di 100:

  * in generale, i valori di priorità 0 - 99 sono riservati alle regole di sincronizzazione personalizzate. Durante l'aggiornamento, i valori di precedenza hello per le regole di sincronizzazione out-of-box sono le modifiche alle regole di sincronizzazione tooaccommodate aggiornato. A causa di problema toothis, regole di sincronizzazione out-of-box è possibile assegnare il valore di precedenza che è minore di 100.
  
  * correzione di Hello impedisce il problema hello durante l'aggiornamento. Tuttavia, non ripristina i valori di precedenza hello per clienti esistenti che sono stati interessati dal problema hello. Verrà fornito in hello toohelp future con ripristino hello separata.

* Risolto un problema in cui hello [schermata di dominio e unità Organizzativa filtro](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) in Azure AD Connect hello risulta guidata *sincronizzare tutti i domini e unità organizzative* opzione selezionata, anche se è abilitato il filtro basato su unità Organizzativa.

*   Risolto un problema che ha provocato un hello [schermata Configura partizioni di Directory](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) in hello tooreturn Synchronization Service Manager un errore se hello *aggiornamento* si fa clic sul pulsante. messaggio di errore Hello *"si è verificato un errore durante l'aggiornamento di domini: non è possibile toocast oggetto di tipo 'ArrayList' tootype ' Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject."* Hello errore si verifica quando il nuovo dominio di Active Directory è stato aggiunto l'insieme di strutture Active Directory esistente tooan e che si sta tentando di tooupdate Azure AD Connect usando hello pulsante Aggiorna.

#### <a name="new-features-and-improvements"></a>Miglioramenti e nuove funzionalità

* [Funzionalità di aggiornamento automatico](active-directory-aadconnect-feature-automatic-upgrade.md) è stato espanso toosupport clienti con hello seguenti configurazioni:
  * È stata abilitata la funzionalità di writeback dispositivi hello.
  * È stato abilitato funzionalità di writeback gruppo hello.
  * installazione di Hello non è un oggetto impostazioni Express o un aggiornamento di DirSync.
  * Si dispone più di 100.000 oggetti nel metaverse hello.
  * Si è connessi toomore rispetto a un insieme di strutture. L'installazione rapida consente di connettersi solo tooone foresta.
  * Hello account Active Directory Connector non è più account MSOL_ hello predefinito.
  * server Hello è toobe nella modalità di gestione temporanea.
  * È stato abilitato funzionalità di writeback delle hello utente.
  
  >[!NOTE]
  >espansione di Hello ambito della funzionalità di aggiornamento automatico hello interessa i clienti di Azure AD Connect compilazione 1.1.105.0 e after. Se non si desidera il toobe di server di Azure AD Connect aggiornato automaticamente, è necessario eseguire cmdlet in seguito nel server di Azure AD Connect: `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`. Per ulteriori informazioni sull'abilitazione/disabilitazione aggiornamento automatico, vedere tooarticle [Azure AD Connect: l'aggiornamento automatico](active-directory-aadconnect-feature-automatic-upgrade.md).

## <a name="115580"></a>1.1.558.0
Stato: non verrà rilasciato. Le modifiche apportate a questa build sono incluse nella versione 1.1.561.0.

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Problema risolto

* Risolto un problema che ha causato hello out-of-box sincronizzazione regola "Out tooAD - utente ImmutableId" toobe rimosso quando viene aggiornato di configurazione del filtro basato su unità Organizzativa. Questa regola di sincronizzazione è necessaria per hello [msDS-ConsistencyGuid come funzionalità di ancoraggio di origine](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor).

* Risolto un problema in cui hello [schermata di dominio e unità Organizzativa filtro](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) in Azure AD Connect hello risulta guidata *sincronizzare tutti i domini e unità organizzative* opzione selezionata, anche se è abilitato il filtro basato su unità Organizzativa.

*   Risolto un problema che ha provocato un hello [schermata Configura partizioni di Directory](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) in hello tooreturn Synchronization Service Manager un errore se hello *aggiornamento* si fa clic sul pulsante. messaggio di errore Hello *"si è verificato un errore durante l'aggiornamento di domini: non è possibile toocast oggetto di tipo 'ArrayList' tootype ' Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject."* Hello errore si verifica quando il nuovo dominio di Active Directory è stato aggiunto l'insieme di strutture Active Directory esistente tooan e che si sta tentando di tooupdate Azure AD Connect usando hello pulsante Aggiorna.

#### <a name="new-features-and-improvements"></a>Miglioramenti e nuove funzionalità

* [Funzionalità di aggiornamento automatico](active-directory-aadconnect-feature-automatic-upgrade.md) è stato espanso toosupport clienti con hello seguenti configurazioni:
  * È stata abilitata la funzionalità di writeback dispositivi hello.
  * È stato abilitato funzionalità di writeback gruppo hello.
  * installazione di Hello non è un oggetto impostazioni Express o un aggiornamento di DirSync.
  * Si dispone più di 100.000 oggetti nel metaverse hello.
  * Si è connessi toomore rispetto a un insieme di strutture. L'installazione rapida consente di connettersi solo tooone foresta.
  * Hello account Active Directory Connector non è più account MSOL_ hello predefinito.
  * server Hello è toobe nella modalità di gestione temporanea.
  * È stato abilitato funzionalità di writeback delle hello utente.
  
  >[!NOTE]
  >espansione di Hello ambito della funzionalità di aggiornamento automatico hello interessa i clienti di Azure AD Connect compilazione 1.1.105.0 e after. Se non si desidera il toobe di server di Azure AD Connect aggiornato automaticamente, è necessario eseguire cmdlet in seguito nel server di Azure AD Connect: `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`. Per ulteriori informazioni sull'abilitazione/disabilitazione aggiornamento automatico, vedere tooarticle [Azure AD Connect: l'aggiornamento automatico](active-directory-aadconnect-feature-automatic-upgrade.md).

## <a name="115570"></a>1.1.557.0
Stato: luglio 2017

>[!NOTE]
>Questa compilazione non è disponibile toocustomers tramite funzionalità di aggiornamento automatico di connettersi hello Azure AD.

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Problema risolto
* Risolto un problema con il cmdlet Initialize-ADSyncDomainJoinedComputerSync hello che ha causato dominio verificato di hello configurato nel hello esistente servizio connessione punto oggetto toobe modificato anche se si tratta comunque di un dominio valido. Questo problema si verifica quando il tenant di Azure AD dispone di più domini verificati che possono essere utilizzato per la configurazione del punto di connessione del servizio hello.

#### <a name="new-features-and-improvements"></a>Miglioramenti e nuove funzionalità
* Il writeback delle password è ora disponibile per l'anteprima con il cloud di Microsoft Azure per enti pubblici e Microsoft Cloud Germany. Per ulteriori informazioni sul supporto di Azure AD Connect per hello diverse istanze del servizio, vedere tooarticle [Azure AD Connect: considerazioni speciali per le istanze](active-directory-aadconnect-instances.md).

* il cmdlet Initialize-ADSyncDomainJoinedComputerSync Hello ha ora un nuovo parametro opzionale denominato AzureADDomain. Questo parametro consente di specificare che verificare toobe dominio utilizzato per la configurazione del punto di connessione del servizio hello.

### <a name="pass-through-authentication"></a>Autenticazione pass-through

#### <a name="new-features-and-improvements"></a>Miglioramenti e nuove funzionalità
* nome Hello dell'agente di hello necessario per l'autenticazione pass-through è stato modificato da *connettore Proxy dell'applicazione di Microsoft Azure AD* troppo*agente autenticazione di Microsoft Azure AD Connect*.

* Quando si abilita l'autenticazione pass-through, la sincronizzazione degli hash delle password non viene più abilitata per impostazione predefinita.


## <a name="115530"></a>1.1.553.0
Stato: giugno 2017

> [!IMPORTANT]
> Questa build introduce modifiche alle regole dello schema e della sincronizzazione. Il servizio di sincronizzazione Azure AD Connect attiva i passaggi di importazione e sincronizzazione completa dopo l'aggiornamento. Dettagli delle modifiche hello è descritto di seguito. tootemporarily rinviare passaggi importazione completa e la sincronizzazione completa dopo l'aggiornamento, fare riferimento tooarticle [come toodefer completa la sincronizzazione dopo l'aggiornamento](active-directory-aadconnect-upgrade-previous-version.md#how-to-defer-full-synchronization-after-upgrade).
>
>

### <a name="azure-ad-connect-sync"></a>Servizio di sincronizzazione Azure AD Connect

#### <a name="known-issue"></a>Problema noto
* Un problema interessa i clienti che usano il [filtro basato su unità organizzativa](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) con il servizio di sincronizzazione Azure AD Connect. Quando ci si sposta toohello [dominio e unità Organizzativa filtro pagina](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) nella procedura guidata Connetti hello Azure AD, è previsto hello seguente comportamento:
  * Se è abilitato il filtro basato su unità Organizzativa, hello **di sincronizzazione selezionati domini e unità organizzative** opzione è selezionata.
  * In caso contrario, hello **sincronizzare tutti i domini e unità organizzative** opzione è selezionata.

problema che si verifichi Hello è tale hello **sincronizzare tutti i domini e unità organizzative opzione** è sempre selezionata quando si esegue hello procedura guidata.  Ciò si verifica anche se in precedenza è stato configurato il filtro basato su unità organizzativa. Prima di salvare le modifiche alla configurazione di AAD Connect, assicurarsi che hello **sincronizzazione domini selezionati ed è selezionata l'opzione di unità organizzative** e verificare che tutte le unità organizzative necessarie toosynchronize sono abilitate di nuovo. In caso contrario, il filtro basato su unità organizzativa verrà disabilitato.

#### <a name="fixed-issues"></a>Problemi risolti

* Risolto un problema con il writeback delle Password che consente un tooreset amministratore AD Azure password hello un locale AD account utente con privilegi. Quando Azure AD Connect viene concessa l'autorizzazione di hello reimpostare la Password di account con privilegiata hello problema Hello. Hello problema viene risolto in questa versione di Azure AD Connect, non consentendo un' tooreset amministratore AD Azure password hello un locale non autorizzato AD account con privilegi utente, a meno che l'amministratore hello è proprietario di hello di tale account. Per ulteriori informazioni, vedere troppo[Security Advisory 4033453](https://technet.microsoft.com/library/security/4033453).

* Risolto un problema correlato toohello [msDS-ConsistencyGuid come ancoraggio di origine](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) funzionalità in Azure AD Connect non non writeback tooon locali attributo msDS-ConsistencyGuid di Active Directory. Hello problema si verifica quando sono presenti locale più foreste Active Directory aggiunti tooAzure AD Connect e hello *le identità utente presenti in più opzione Directory* è selezionata. Quando viene utilizzato questo tipo di configurazione, le regole di sincronizzazione risultante hello non popolano attributo sourceAnchorBinary hello in hello Metaverse. attributo di sourceAnchorBinary Hello viene utilizzato come attributo di origine hello per l'attributo msDS-ConsistencyGuid. Di conseguenza, non viene eseguito il writeback toohello ms DSConsistencyGuid attributo. problema hello toofix, regole di sincronizzazione seguenti sono stati aggiornati tooensure che hello sourceAnchorBinary attributo Metaverse è sempre popolato hello:
  * In from AD - InetOrgPerson AccountEnabled.xml
  * In from AD - InetOrgPerson Common.xml
  * In from AD - User AccountEnabled.xml
  * In from AD - User Common.xml
  * In from AD - User Join SOAInAAD.xml

* In precedenza, anche se hello [msDS-ConsistencyGuid come ancoraggio di origine](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) funzionalità non è abilitata, hello "Out tooAD – utente ImmutableId" regola di sincronizzazione risulta ancora aggiunto tooAzure AD Connect. effetto Hello è grave e non provoca il writeback di toooccur attributo msDS-ConsistencyGuid. tooavoid confusione, è stata aggiunta logica tooensure che hello regola di sincronizzazione viene aggiunto solo quando è abilitata la funzionalità di hello.

* Risolto un problema che ha causato toofail sincronizzazione hash di password con l'evento di errore 611. Questo problema si verifica dopo che uno o più controller di dominio sono stati rimossi dall'istanza di AD locale. Alla fine di hello di ogni ciclo di sincronizzazione password, hello cookie di sincronizzazione emesso da locale AD contiene l'ID di chiamata hello rimosso dei controller di dominio con il valore di USN (Update Sequence Number) pari a 0. Hello Gestione sincronizzazione Password è Impossibile toopersist sincronizzazione cookie contenente USN valore pari a 0 e ha esito negativo con l'evento di errore 611. Durante la sincronizzazione successiva hello ciclo, hello Gestione sincronizzazione Password riutilizza hello ultima sincronizzazione persistente cookie che contiene il valore di USN pari a 0. In questo modo hello stesse modifiche alla password toobe risincronizzata. Con questa correzione, Gestione sincronizzazione Password hello mantiene il cookie di sincronizzazione hello correttamente.

* In precedenza, anche se l'aggiornamento automatico è stato disabilitato usando il cmdlet Set-ADSyncAutoUpgrade hello, il processo di aggiornamento automatico hello continua periodicamente toocheck per l'aggiornamento e si basa su hello scaricato installer toohonor disabilitazione. Con questa correzione, il processo di aggiornamento automatico di hello non controlla più per l'aggiornamento periodicamente. correzione di Hello viene applicata automaticamente quando il programma di installazione dell'aggiornamento per questa versione di Azure AD Connect viene eseguita una volta.

#### <a name="new-features-and-improvements"></a>Miglioramenti e nuove funzionalità

* In precedenza, hello [msDS-ConsistencyGuid come ancoraggio di origine](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) funzionalità è stata toonew disponibile solo per distribuzioni. Ora è disponibile tooexisting distribuzioni. Più in particolare:
  * tooaccess hello funzionalità, avviare la procedura guidata di hello Azure AD Connect e scegliere hello *ancoraggio di origine aggiornamento* opzione.
  * Questa opzione è tooexisting visibili solo le distribuzioni che usano objectGuid come attributo sourceAnchor.
  * Quando si configura l'opzione hello, la procedura guidata hello convalida stato hello dell'attributo msDS-ConsistencyGuid hello in Active Directory locale. Se non è configurata per attributo hello in qualsiasi oggetto utente nella directory di hello, guidata hello utilizza hello msDS-ConsistencyGuid come attributo sourceAnchor hello. Se l'attributo hello è configurata su uno o più oggetti utente nella directory di hello, guidata hello conclude attributo hello è utilizzato da altre applicazioni non supporta hello ancoraggio di origine modifica tooproceed e non è adatto come attributo sourceAnchor. Se si è certi che tale attributo hello non sia utilizzato da applicazioni esistenti, è necessario toocontact il supporto per informazioni su come toosuppress hello errore.

* Specifiche troppo**userCertificate** attributo per gli oggetti dispositivo, Azure AD Connect ora consente di cercare i valori dei certificati necessari per [connessione tooAzure dispositivi appartenenti a un dominio Active Directory per Windows 10 esperienza](https://docs.microsoft.com/azure/active-directory/active-directory-azureadjoin-devices-group-policy) ed esclude quelli rest hello prima della sincronizzazione tooAzure Active Directory. tooenable questo comportamento, regola di sincronizzazione di out-of-box hello "Out tooAAD - dispositivo Join SOAInAD" è stato aggiornato.

* Azure AD Connect ora supporta il writeback di Exchange Online **cloudPublicDelegates** tooon locale dell'attributo AD **publicDelegates** attributo. Ciò rende hello scenario in cui una cassetta postale di Exchange Online può essere concesse SendOnBehalfTo diritti toousers con cassetta postale di Exchange locale. toosupport questa funzionalità, una nuova regola di sincronizzazione out-of-box "Out tooAD – utente Exchange ibrido PublicDelegates writeback" è stato aggiunto. Questa regola di sincronizzazione viene aggiunto solo tooAzure AD Connect quando è abilitata la funzionalità ibride di Exchange.

*   Azure AD Connect ora supporta la sincronizzazione hello **altRecipient** attributo da Azure AD. toosupport questa modifica, alle regole di sincronizzazione out-of-box sono stati aggiornati il flusso di attributi tooinclude hello necessarie:
  * In from AD – User Exchange
  * Out tooAAD – ExchangeOnline utente
  
* Hello **cloudSOAExchMailbox** attributo Metaverse hello indica se un utente specificato dispone di cassette postali di Exchange Online o meno. La definizione è stata aggiornata tooinclude aggiuntive RecipientDisplayTypes in linea di Exchange come tali cassette postali sala conferenze e di attrezzature. tooenable questa modifica, la definizione hello di attributo di cloudSOAExchMailbox hello, che è stato trovato nella regola di sincronizzazione di out-of-box "In da Azure ad – utente ibrida di Exchange", non è stata aggiornata:

```
CBool(IIF(IsNullOrEmpty([cloudMSExchRecipientDisplayType]),NULL,BitAnd([cloudMSExchRecipientDisplayType],&amp;HFF) = 0))
```

... toohello seguenti:

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

* Esempio hello aggiunto set di funzioni X509Certificate2 compatibile per la creazione di sincronizzazione i valori del certificato toohandle espressioni regola nell'attributo userCertificate hello:

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

* Dopo le modifiche dello schema è stati introdotti tooallow clienti toocreate sincronizzazione personalizzato regole tooflow sAMAccountName domainNetBios e domainFQDN per gli oggetti di gruppo, nonché di nome distinto per gli oggetti utente:

  * Gli attributi seguenti sono state aggiunte tooMV schema:
    * Group: AccountName
    * Group: domainNetBios
    * Group: domainFQDN
    * Person: distinguishedName

  * Gli attributi seguenti sono state aggiunte tooAzure dello schema di Active Directory Connector:
    * Group: OnPremisesSamAccountName
    * Group: NetBiosName
    * Group: DnsDomainName
    * User: OnPremisesDistinguishedName

* script di cmdlet ADSyncDomainJoinedComputerSync Hello ha ora un nuovo parametro opzionale denominato AzureEnvironment. il parametro Hello è usato toospecify hello quale area a cui è ospitato nel tenant di Azure Active Directory corrispondente. I valori validi includono:
  * AzureCloud (predefinito)
  * AzureChinaCloud
  * AzureGermanyCloud
  * USGovernment
 
* Editor regole di sincronizzazione Toouse aggiornato Join (invece di effettuare il provisioning) come valore predefinito di hello del tipo di collegamento durante la creazione di regole di sincronizzazione.

### <a name="ad-fs-management"></a>Gestione di AD FS.

#### <a name="issues-fixed"></a>Problemi risolti

* Sono dovuti a garantire la resilienza tooimprove AD Azure in un'interruzione dell'autenticazione nuovi endpoint di WS-Federation seguenti URL e saranno aggiunti tooon locale ADFS risposta configurazione trust di terze parti:
  * https://ests.login.microsoftonline.com/login.srf
  * https://stamp2.login.microsoftonline.com/login.srf
  * https://ccs.login.microsoftonline.com/login.srf
  * https://ccs-sdf.login.microsoftonline.com/login.srf
  
* Risolto un problema che ha determinato valore di attestazione non corretta di ADFS toogenerate per IssuerID. problema di Hello si verifica se sono presenti più domini verificati nel tenant di Azure AD hello e suffisso di dominio hello di hello userPrincipalName attributo utilizzato toogenerate hello IssuerID attestazione è almeno 3 livelli completa (ad esempio, johndoe@us.contoso.com). Hello viene risolto mediante l'aggiornamento di regex hello utilizzato dalle regole attestazione hello.

#### <a name="new-features-and-improvements"></a>Miglioramenti e nuove funzionalità
* In precedenza, funzionalità di gestione dei certificati ADFS hello fornita da Azure AD Connect sono utilizzabili solo con una farm ADFS gestite tramite Azure AD Connect. A questo punto, è possibile utilizzare la funzionalità hello con le farm ADFS che non sono gestite con Azure AD Connect.

## <a name="115240"></a>1.1.524.0
Data di rilascio: maggio 2017

> [!IMPORTANT]
> Questa build introduce modifiche alle regole dello schema e della sincronizzazione. Dopo l'aggiornamento, il servizio di sincronizzazione Azure AD Connect attiva i passaggi di importazione e sincronizzazione completa. Dettagli delle modifiche hello è descritto di seguito.
>
>

**Problemi risolti:**

Servizio di sincronizzazione Azure AD Connect

* Risolto un problema che causa l'aggiornamento automatico toooccur nel server di Azure AD Connect hello anche se customer è disabilitato funzionalità hello utilizzando cmdlet Set-ADSyncAutoUpgrade hello. Con questa correzione, processo di aggiornamento automatico sul server di hello hello comunque eseguita una verifica per l'aggiornamento periodicamente, ma programma di installazione scaricato hello rispetta configurazione aggiornamento automatico di hello.
* Durante l'aggiornamento sul posto di DirSync, Azure AD Connect crea un toobe di account di servizio di Azure AD usato dal connettore hello Azure AD per la sincronizzazione con Azure AD. Dopo aver creato l'account di hello, Azure AD Connect esegue l'autenticazione con Azure AD usando account hello. In alcuni casi, l'autenticazione non riesce a causa di errori temporanei, che a sua volta comporta toofail aggiornamento sul posto di DirSync con errore *"si è verificato un errore in esecuzione attività di configurazione AAD Sync: AADSTS50034: toosign a questa applicazione, l'account di hello è necessario aggiungere directory xxx.onmicrosoft.com toohello."* resilienza di hello tooimprove di aggiornamento di DirSync, Azure AD Connect ora tentativi hello passaggio di autenticazione.
* Si è verificato un problema che causa toosucceed aggiornamento sul posto di DirSync con compilazione 443, ma non vengono creati i profili di esecuzione richiesto per la sincronizzazione delle directory. La logica di correzione è inclusa in questa build di Azure AD Connect. Quando cliente viene aggiornato compilazione toothis, Azure AD Connect rileva mancante profili di esecuzione e li crea.
* Risolto un problema che causa toostart toofail processo di sincronizzazione delle Password con 6900 ID evento e di errore *"Con hello stessa chiave è già stato aggiunto un elemento"*. Questo problema si verifica se si aggiorna l'unità Organizzativa filtro partizione di configurazione tooinclude Active Directory di configurazione. Questo problema, la sincronizzazione delle Password elabora ora toofix Sincronizza dalle partizioni di dominio Active Directory solo le modifiche delle password. Le partizioni non di dominio, come la partizione di configurazione, vengono ignorate.
* Durante l'installazione rapida, Azure AD Connect crea una locale toobe utilizzato da toocommunicate connettore hello Active Directory locale dell'account di dominio Active directory Active Directory. In precedenza, hello account viene creato con il flag PASSWD_NOTREQD hello impostato sull'attributo di controllo dell'Account utente di hello e una password casuale è impostata sull'account hello. A questo punto, Azure AD Connect in modo esplicito rimuove flag PASSWD_NOTREQD hello hello password viene impostata sull'account hello.
* Risolto un problema che causa toofail aggiornamento di DirSync con errore *"un deadlock durante l'esecuzione in sql server quali tooacquire durante un blocco dell'applicazione"* quando attributo mailNickname hello è stato trovato in hello schema di Active Directory locale, ma non è limitato toohello classe dell'oggetto utente di Active Directory.
* Fissa un problema che causa tooautomatically funzionalità di dispositivo writeback disabilitato quando un amministratore Aggiorna configurazione di sincronizzazione Azure AD Connect usando la procedura guidata Azure AD Connect. Ciò è dovuto verifica dei prerequisiti esecuzione guidata hello per hello esistente writeback della configurazione del dispositivo in AD locale e controllo hello ha esito negativo. correzione di Hello è controllo hello tooskip se writeback dei dispositivi è già abilitato in precedenza.
* tooconfigure OU filtro, è possibile utilizzare Creazione guidata di Azure AD Connect hello o hello Synchronization Service Manager. In precedenza, se si utilizza il filtro di hello Azure AD Connect guidata tooconfigure unità Organizzativa, nuove unità organizzative create in un secondo momento sono incluse la sincronizzazione delle directory. Se si preferisce non inclusi nuovi toobe di unità organizzative, è necessario configurare l'unità Organizzativa filtro utilizzando hello Synchronization Service Manager. A questo punto, è possibile ottenere hello stesso comportamento utilizzando la procedura guidata Azure AD Connect.
* Risolto un problema che causa una stored procedure necessarie per Azure AD Connect toobe creato in schema di hello di installazione di amministrazione, anziché in schema dbo hello hello.
* Risolto un problema che causa l'attributo ID traccia hello restituito da Azure AD toobe omesso in hello AAD Connect Server i registri eventi. problema di Hello si verifica se Azure AD Connect riceve un messaggio di reindirizzamento da Azure AD e Azure AD Connect non è possibile tooconnect toohello endpoint fornito. ID traccia Hello viene utilizzato toocorrelate tecnici del supporto tecnico con i log sul lato servizio durante la risoluzione dei problemi.
* Quando Azure AD Connect riceve l'errore LargeObject da Azure AD, Azure AD Connect genera un evento con ID evento 6941 e messaggio *"oggetto provisioning hello è troppo grande. Trim numero hello dei valori di attributo per l'oggetto".* In hello stesso tempo, Azure AD Connect anche genera un evento con ID evento 6900 e messaggio fuorviante *"Microsoft.Online.Coexistence.ProvisionRetryException: Impossibile toocommunicate con Windows hello servizio Azure Active Directory."* toominimize confusione, Azure AD Connect non genera l'errore hello quest'ultimo caso quando viene ricevuto l'errore LargeObject.
* Risolto un problema che causa hello toobecome Synchronization Service Manager non risponde durante il tentativo di configurazione di hello tooupdate per connettore LDAP generico.

**Nuove funzionalità o miglioramenti:**

Servizio di sincronizzazione Azure AD Connect
* Sono state implementate le modifiche alle regole di sincronizzazione: hello dopo le modifiche alle regole di sincronizzazione:
  * Set di regole di sincronizzazione predefinito aggiornato toonot gli attributi di esportazione **userCertificate** e **userSMIMECertificate** se gli attributi di hello hanno valori di più di 15.
  * Attributi di Active Directory **employeeID** e **msExchBypassModerationLink** sono ora incluse nel set di regole di sincronizzazione predefinito hello.
  * L'attributo di AD **photo** è stato rimosso dal set di regole di sincronizzazione predefinito.
  * Aggiunto **preferredDataLocation** toohello Metaverse schema e connettore AAD. Clienti che desiderano personalizzato tooupdate che entrambi gli attributi in Azure AD è possono implementare la sincronizzazione in modo toodo regole. toofind altre informazioni sull'attributo hello, vedere la sezione tooarticle [sincronizzazione di Azure AD Connect: la modalità di configurazione - Abilita sincronizzazione di PreferredDataLocation predefinite toomake toohello una modifica](active-directory-aadconnectsync-change-the-configuration.md#enable-synchronization-of-preferreddatalocation).
  * Aggiunto **userType** toohello Metaverse schema e connettore AAD. Clienti che desiderano personalizzato tooupdate che entrambi gli attributi in Azure AD è possono implementare la sincronizzazione in modo toodo regole.

* Azure AD Connect ora automaticamente Abilita hello di utilizzo dell'attributo ConsistencyGuid come attributo di ancoraggio di origine hello per on-premise oggetti Active Directory. Inoltre, Azure AD Connect popola attributo ConsistencyGuid hello con valore dell'attributo objectGuid hello se è vuota. Questa funzionalità è applicabile toonew solo alla distribuzione. toofind ulteriori informazioni su questa funzionalità, fare riferimento a sezione tooarticle [Azure AD Connect: concetti - utilizzando l'attributo msDS-ConsistencyGuid come sourceAnchor progettare](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor).
* Nuovi cmdlet Invoke-ADSyncDiagnostics è stato di risoluzione dei problemi toohelp aggiunto diagnosticare la sincronizzazione dell'Hash Password problemi correlati. Per informazioni sull'utilizzo di cmdlet hello, consultare tooarticle [risolvere i problemi di sincronizzazione delle password con sincronizzazione di Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-troubleshoot-password-synchronization).
* Azure AD Connect ora supporta oggetti di sincronizzazione cartelle pubbliche di impostazioni locali tooAzure AD Active Directory. È possibile abilitare le funzionalità di hello utilizzando Creazione guidata di Azure AD Connect in funzionalità facoltative. toofind ulteriori informazioni su questa funzionalità, vedere tooarticle [il supporto di Office 365 Directory base Edge di blocco per cartelle pubbliche locale abilitate alla posta elettronica](https://blogs.technet.microsoft.com/exchange/2017/05/19/office-365-directory-based-edge-blocking-support-for-on-premises-mail-enabled-public-folders).
* Azure AD Connect richiede un toosynchronize di account di dominio Active Directory locale AD. Se è installato Azure AD Connect in precedenza, modalità hello Express, è possibile fornire credenziali hello di un account di amministratore dell'organizzazione e Azure AD Connect è necessario creare account di dominio Active Directory hello richiesto. Tuttavia, per un'installazione personalizzata e l'aggiunta di distribuzione esistente di foreste tooan, sono stati necessari tooprovide hello account di dominio Active Directory. A questo punto, è inoltre hello opzione tooprovide hello credenziali di un account amministratore dell'organizzazione durante un'installazione personalizzata e Azure AD Connect crea account di dominio Active Directory hello richiesto.
* Azure AD Connect supporta ora SQL AOA. È necessario abilitare SQL AOA prima di installare Azure AD Connect. Durante l'installazione, Azure AD Connect rileva se istanza SQL hello fornita è abilitato per SQL AOA o meno. Se SQL AOA è abilitata, Azure AD Connect ulteriormente determina se SQL AOA è toouse configurato di replica sincrona o asincrona. Quando si configurano hello listener del gruppo di disponibilità, è consigliabile impostare hello RegisterAllProvidersIP proprietà too0. In questo modo Azure AD Connect utilizza attualmente tooSQL tooconnect SQL Native Client e SQL Native Client non supporta l'utilizzo di hello della proprietà MultiSubNetFailover.
* Se si utilizza LocalDB come database hello del server di Azure AD Connect e ha raggiunto il limite di dimensioni di 10 GB, hello servizio di sincronizzazione non verrà avviato. In precedenza, è necessario tooperform operazione ShrinkDatabase su hello LocalDB tooreclaim sufficiente spazio per hello toostart di servizio di sincronizzazione. Dopo la quale, è possibile utilizzare hello toodelete Synchronization Service Manager spazio di esecuzione tooreclaim cronologia più DB. A questo punto, è possibile utilizzare toopurge cmdlet Start-ADSyncPurgeRunHistory dati di cronologia viene eseguito dallo spazio di DB tooreclaim di LocalDB. Inoltre, questo cmdlet supporta una modalità offline (specificando hello - parametro non in linea) che può essere utilizzato quando hello servizio di sincronizzazione non è in esecuzione. Nota: la modalità offline hello utilizzabile solo se hello servizio di sincronizzazione non è in esecuzione e il database di hello utilizzato è LocalDB.
* quantità di hello tooreduce di spazio di archiviazione necessaria, Azure AD Connect ora consente di comprimere i dettagli dell'errore di sincronizzazione prima di archiviarli nel database LocalDB o SQL. Durante l'aggiornamento da una versione precedente di Azure AD Connect toothis, Azure AD Connect esegue una sola volta compressione sui dettagli di errore di sincronizzazione esistente.
* In precedenza, dopo aver aggiornato l'unità Organizzativa di configurazione del filtro, è necessario eseguire manualmente un'importazione completa tooensure oggetti esistenti sono correttamente incluso/escluso dalla sincronizzazione delle directory. A questo punto, Azure AD Connect attiva automaticamente importazione completa durante la sincronizzazione successiva hello del ciclo. Importazione, inoltre, completo può essere solo connettori toohello applicati AD interessati dall'aggiornamento hello. Nota: questo miglioramento è applicabile tooOU filtro gli aggiornamenti eseguiti tramite procedura guidata solo di hello Azure AD Connect. Non è applicabile tooOU filtro aggiornamenti eseguiti utilizzando hello Synchronization Service Manager.
* In precedenza, il filtro basato sui gruppi supportava soltanto oggetti utenti, gruppi e contatti. Ora il filtro supporta anche gli oggetti computer.
* In precedenza, era possibile eliminare i dati nello spazio connettore senza disabilitare l'utilità di pianificazione della sincronizzazione di Azure AD Connect. A questo punto, l'eliminazione di hello blocchi di gestione del servizio di sincronizzazione dei dati di spazio connettore hello se rileva l'utilità di pianificazione di hello è abilitata. Inoltre, viene restituito un avviso tooinform clienti potenziali perdite di dati se hello dati spazio connettore viene eliminato.
* In precedenza, è necessario disabilitare la funzionalità di trascrizione di PowerShell per Azure AD Connect guidata toorun correttamente. Questo problema è stato risolto parzialmente. Se si utilizza Configurazione sincronizzazione toomanage della procedura guidata Azure AD Connect, è possibile abilitare la funzionalità di trascrizione di PowerShell. Se si utilizza configurazione ADFS toomanage della procedura guidata Azure AD Connect, è necessario disabilitare la funzionalità di trascrizione di PowerShell.



## <a name="114860"></a>1.1.486.0
Data di rilascio: aprile 2017

**Problemi risolti:**
* Risolto il problema di hello in Azure AD Connect non verranno installati correttamente nella versione localizzata di Windows Server.

## <a name="114840"></a>1.1.484.0
Data di rilascio: aprile 2017

**Problemi noti:**

* Questa versione di Azure AD Connect non verrà installata correttamente se hello seguenti condizioni è soddisfatte:
   1. Si sta eseguendo l'aggiornamento sul posto di DirSync o una nuova installazione di Azure AD Connect.
   2. Si utilizza una versione localizzata di Windows Server in cui non è il nome di hello del gruppo Administrators predefinito nel server di hello "Administrators".
   3. Si utilizza hello predefinito installato con Azure AD Connect, invece di fornire la propria SQL completa SQL Server 2012 Express LocalDB.

**Problemi risolti:**

Servizio di sincronizzazione Azure AD Connect
* Risolto un problema in utilità di pianificazione sincronizzazione hello hello sincronizzazione intero passaggio ignorato se uno o più connettori mancante per il passaggio di sincronizzazione del profilo di esecuzione. Ad esempio, sono stati aggiunti manualmente un connettore utilizzando hello Synchronization Service Manager senza creare un'importazione Delta per il profilo di esecuzione. Questa correzione assicura che l'utilità di pianificazione di sincronizzazione hello continua toorun importazione Delta per altri connettori.
* Risolto un problema in cui hello servizio di sincronizzazione si arresta immediatamente l'elaborazione di un profilo di esecuzione quando rileva un problema con uno dei passaggi eseguito hello. Questa correzione assicura che hello ignora il servizio di sincronizzazione che eseguono passaggio e continua tooprocess hello rest. Ad esempio, il profilo d'importazione delta per il connettore di Active Directory contiene più passaggi di esecuzione, uno per ogni dominio locale di Active Directory. Hello servizio di sincronizzazione verrà eseguita importazione Delta con hello altri domini di Active Directory anche se uno di essi ha problemi di connettività di rete.
* Risolto un problema che causa hello connettore Azure AD aggiornamento toobe ignorato durante l'aggiornamento automatico.
* Risolto un problema che tooincorrectly Connect di Azure AD le cause determinare se il server di hello è un controller di dominio durante l'installazione, che in attiva causerà DirSync toofail l'aggiornamento.
* Fissa un problema che causa DirSync toonot aggiornamento sul posto creare qualsiasi profilo per hello Azure Active Directory Connector di esecuzione.
* Risolto un problema in interfaccia utente di hello Synchronization Service Manager non risponde durante il tentativo di tooconfigure connettore LDAP generico.

Gestione di AD FS.
* Risolto un problema in Creazione guidata di Azure AD Connect hello ha esito negativo se il nodo primario di hello AD FS è stato spostato tooanother server.

Desktop SSO
* Risolto un problema nella creazione guidata di Azure AD Connect hello in hello schermata di accesso non è possibile abilitare la funzionalità Desktop SSO se si sceglie la sincronizzazione delle Password come opzione di accesso durante l'installazione di nuovo.

**Nuove funzionalità o miglioramenti:**

Servizio di sincronizzazione Azure AD Connect
* Sincronizzazione di connettersi AD Azure supporta ora l'utilizzo di hello di Account servizio virtuale, l'Account del servizio gestito e Account del servizio gestito del gruppo come account del servizio. Si applica toonew installazione di Azure AD Connect solo. Durante l'installazione di Azure AD Connect:
    * Per impostazione predefinita, la procedura guidata di Azure AD Connect crea un account del servizio virtuale che usa come account del servizio.
    * Se si sta installando un controller di dominio, Azure AD Connect fallback comportamento tooprevious in cui verrà creato un account utente di dominio e utilizzarla come account del servizio.
    * È possibile eseguire l'override di comportamento predefinito di hello fornendo uno dei seguenti hello:
      * Account del servizio gestito del gruppo
      * Account del servizio gestito
      * Account utente di dominio
      * Account utente locale
* In precedenza, se si esegue l'aggiornamento tooa nuova compilazione di Azure AD Connect contenente connettori aggiornare o modifiche alle regole di sincronizzazione, Azure AD Connect attiverà un ciclo di sincronizzazione completa. Ora Azure AD Connect attiva in modo selettivo il passaggio di importazione completa solo per i connettori con modifiche alle regole di aggiornamento e il passaggio di sincronizzazione completa solo per i connettori con modifiche alle regole di sincronizzazione.
* In precedenza, hello esportare soglia di eliminazione viene applicata solo tooexports attivati mediante l'utilità di pianificazione sincronizzazione hello. A questo punto, funzionalità hello viene estesa esportazioni tooinclude attivate manualmente dal cliente hello utilizzando hello Synchronization Service Manager.
* Il tenant di Azure AD contiene una configurazione del servizio che indica se la funzionalità Sincronizzazione password è abilitata o meno per il tenant. In precedenza, è facile per hello toobe di configurazione di servizio configurato in modo non corretto da Azure AD Connect quando è attivo e un server di gestione temporanea. A questo punto, Azure AD Connect verrà eseguito un tentativo configurazione del servizio hello tookeep coerenza con attive solo i server di Azure AD Connect.
* Ora la procedura guidata di Azure AD Connect rileva e restituisce un avviso se in Active Directory locale non è abilitato il Cestino di AD.
* In precedenza, esportazione tooAzure AD scade e non riesce se hello combinati dimensione degli oggetti hello in batch hello supera determinata soglia. A questo punto, hello servizio di sincronizzazione tenterà oggetti hello tooresend in batch più piccoli, separato se viene rilevato il problema di hello.
* applicazione di gestione delle chiavi del servizio sincronizzazione Hello è stata rimossa dal Menu Start di Windows. Gestione della chiave di crittografia continuerà toobe supportati tramite l'interfaccia della riga di comando utilizzando miiskmu.exe. Per informazioni sulla gestione di chiave di crittografia, vedere tooarticle [chiave di crittografia Abandoning hello Azure AD Sync connettersi](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-change-serviceacct-pass#abandoning-the-azure-ad-connect-sync-encryption-key).
* In precedenza, se si modifica password account del servizio sincronizzazione hello Azure AD Connect, hello servizio di sincronizzazione non sarà in grado di avviare correttamente finché non si hanno abbandonato la chiave di crittografia hello e reinizializzata password account del servizio sincronizzazione hello Azure AD Connect. Ora non è più necessario.

Desktop SSO

* Procedura guidata di Azure AD Connect non richiede più toobe 9090 porta aperta sulla rete hello quando si configura l'autenticazione pass-through e SSO Desktop. È necessaria solo la porta 443. 

## <a name="114430"></a>1.1.443.0
Data di rilascio: marzo 2017

**Problemi risolti:**

Servizio di sincronizzazione Azure AD Connect
* Risolto un problema determinando toofail procedura guidata di Azure AD Connect, se il nome visualizzato hello di hello Azure Active Directory Connector non contiene hello onmicrosoft.com iniziale dominio assegnato toohello AD Azure tenant.
* Risolto un problema determinando toofail procedura guidata di Azure AD Connect durante la creazione del database tooSQL connessione quando la password di hello dell'Account del servizio di sincronizzazione hello contiene caratteri speciali, ad esempio l'apostrofo, due punti e lo spazio.
* Risolto un problema che causa errore hello toooccur "hello dimage ha un ancoraggio che è diverso da image hello" in un server di Azure AD Connect in modalità di gestione temporanea, dopo che è stato temporaneamente escluso un locale di Active Directory dalla sincronizzazione dell'oggetto e quindi si nuovamente per esegue la sincronizzazione.
* Risolto un problema che causa errore hello toooccur "dal DN oggetto hello è fantasma" in un server di Azure AD Connect in modalità di gestione temporanea, dopo che è stato temporaneamente escluso un locale di Active Directory dalla sincronizzazione dell'oggetto e quindi si nuovamente per la sincronizzazione.

Gestione di AD FS.
* Risolto un problema in cui la procedura guidata Azure AD Connect non aggiornare la configurazione di ADFS e impostare hello destra attestazioni hello trust della relying party dopo aver configurato l'ID di accesso alternativo.
* Risolto un problema in cui la procedura guidata Azure AD Connect è Impossibile toocorrectly server ADFS di handle AD i cui account del servizio sono configurati utilizzando il formato di userPrincipalName anziché il formato di nome account SAM.

Autenticazione pass-through
* Risolto un problema che causa toofail procedura guidata di Azure AD Connect, se è selezionata passare tramite l'autenticazione, ma si verifica un errore di registrazione del connettore corrispondente.
* Risolto un problema che causa la convalida toobypass procedura guidata controlla nel metodo di accesso selezionato quando è abilitata la funzionalità SSO Desktop di Azure AD Connect.

Reimpostazione delle password
* Risolto un problema che potrebbe essere hello Azure AAD Connect server toonot tentativo toore-connettersi se hello connessione è stata terminata da un firewall o proxy.

**Nuove funzionalità o miglioramenti:**

Servizio di sincronizzazione Azure AD Connect
* Il cmdlet Get-ADSyncScheduler restituisce ora una nuova proprietà booleana denominata SyncCycleInProgress. Se hello ha restituito il valore è true, che significa che sia presente un ciclo di sincronizzazione pianificato in corso.
* Cartella di destinazione per l'archiviazione di Azure AD Connect installazione e i log di installazione è stato spostato dal file di log toohello %localappdata%\AADConnect too%programdata%\AADConnect tooimprove accessibilità.

Gestione di AD FS.
* Aggiunto il supporto per l'aggiornamento del certificato SSL Farm AD FS.
* Aggiunto il supporto per la gestione di AD FS 2016.
* È ora possibile specificare un gMSA (account del servizio gestito di gruppo) durante l'installazione di AD FS.
* È ora possibile configurare SHA-256 come algoritmo hash della firma hello per trust della relying party Azure AD.

Reimpostazione delle password
* I miglioramenti introdotti tooallow hello prodotto toofunction in ambienti con più severi regole del firewall.
* Connessione migliorata affidabilità tooAzure Bus di servizio.

## <a name="113800"></a>1.1.380.0
Data di rilascio: dicembre 2016

**Problema risolto:**

* Problema di hello predefinito in cui hello issuerid di regole attestazioni per Active Directory Federation Services (ADFS) è manca in questa compilazione.

>[!NOTE]
>Questa compilazione non è disponibile toocustomers tramite funzionalità di aggiornamento automatico di connettersi hello Azure AD.

## <a name="113710"></a>1.1.371.0
Data di rilascio: dicembre 2016

**Problema noto:**

* regola di attestazione issuerid Hello per AD FS è manca in questa compilazione. regola di attestazione issuerid Hello è obbligatorio se federazione più domini con Azure Active Directory (Azure AD). Se si utilizza Azure AD Connect toomanage locale regola attestazione issuerid esistente di hello distribuzione di ADFS, l'aggiornamento di compilazione toothis rimuove la configurazione di ADFS. È possibile risolvere il problema di hello mediante l'aggiunta di regole attestazioni di hello issuerid dopo l'installazione/aggiornamento hello. Per ulteriori informazioni sull'aggiunta di hello issuerid di regole attestazioni, vedere toothis articolo su [supporto di più domini per la federazione con Azure AD](active-directory-aadconnect-multiple-domains.md).

**Problema risolto:**

* Se 9090 porta non è aperto per la connessione in uscita hello, hello Azure AD Connect installazione o aggiornamento ha esito negativo.

>[!NOTE]
>Questa compilazione non è disponibile toocustomers tramite funzionalità di aggiornamento automatico di connettersi hello Azure AD.

## <a name="113700"></a>1.1.370.0
Data di rilascio: dicembre 2016

**Problemi noti:**

* regola di attestazione issuerid Hello per AD FS è manca in questa compilazione. regola di attestazione issuerid Hello è obbligatorio se federazione più domini con Azure AD. Se si utilizza Azure AD Connect toomanage locale regola attestazione issuerid esistente di hello distribuzione di ADFS, l'aggiornamento di compilazione toothis rimuove la configurazione di ADFS. È possibile risolvere il problema di hello mediante l'aggiunta di regole attestazioni di hello issuerid dopo l'installazione/aggiornamento. Per ulteriori informazioni sull'aggiunta di issuerid di regole attestazioni, vedere toothis articolo su [supporto di più domini per la federazione con Azure AD](active-directory-aadconnect-multiple-domains.md).
* Porta 9090 deve essere installazione aprire toocomplete in uscita.

**Nuove funzionalità:**

* Autenticazione pass-through (anteprima).

>[!NOTE]
>Questa compilazione non è disponibile toocustomers tramite funzionalità di aggiornamento automatico di connettersi hello Azure AD.

## <a name="113430"></a>1.1.343.0
Data di rilascio: novembre 2016

**Problema noto:**

* regola di attestazione issuerid Hello per AD FS è manca in questa compilazione. regola di attestazione issuerid Hello è obbligatorio se federazione più domini con Azure AD. Se si utilizza Azure AD Connect toomanage locale regola attestazione issuerid esistente di hello distribuzione di ADFS, l'aggiornamento di compilazione toothis rimuove la configurazione di ADFS. È possibile risolvere il problema di hello mediante l'aggiunta di regole attestazioni di hello issuerid dopo l'installazione/aggiornamento. Per ulteriori informazioni sull'aggiunta di issuerid di regole attestazioni, vedere toothis articolo su [supporto di più domini per la federazione con Azure AD](active-directory-aadconnect-multiple-domains.md).

**Problemi risolti:**

* In alcuni casi, l'installazione di Azure AD Connect, ha esito negativo perché è Impossibile toocreate cui la password soddisfi il livello di hello di complessità specificati dai criteri di password dell'organizzazione hello un account di servizio locale.
* Risolto un problema in regole di unione non vengono rivalutate quando un oggetto di nello spazio connettore hello diventa contemporaneamente out-of-scope per una regola di join e diventano nell'ambito di un altro. Questa situazione può verificarsi se sono presenti due o più regole di unione, le cui condizioni di unione si escludono a vicenda.
* È stato risolto un problema in cui le regole di sincronizzazione in ingresso (di Azure AD), che non contengono regole di unione, non vengono elaborate se dispongono di valori di precedenza inferiori rispetto a quelle contenenti le regole di unione.

**Miglioramenti:**

* Aggiunta del supporto per l'installazione di Azure AD Connect in Windows Server 2016 Standard o versione successiva.
* Aggiunta del supporto per l'utilizzo di SQL Server 2016 come database remoto hello per Azure AD Connect.

## <a name="112810"></a>1.1.281.0
Data di rilascio: agosto 2016

**Problemi risolti:**

* Intervallo toosync le modifiche non possono essere hello dopo il successivo ciclo di sincronizzazione è stata completata.
* La procedura guidata di Azure AD Connect non accetta un account di Azure AD il cui nome utente inizi con un carattere di sottolineatura (\_).
* Procedura guidata di Azure AD Connect ha esito negativo di account di Azure AD hello tooauthenticate se hello password dell'account contiene troppi caratteri speciali. Messaggio di errore "Impossibile toovalidate credenziali. Si è verificato un errore imprevisto".
* La disinstallazione di server di gestione temporanea disabilita la sincronizzazione delle password nel tenant di Azure AD e causa toofail sincronizzazione password con server attivo.
* In casi rari, la sincronizzazione delle password ha esito negativo quando è presente alcun hash della password archiviate per utente hello.
* Quando il server Azure AD Connect è abilitato per la modalità di gestione temporanea, il writeback delle password non viene temporaneamente disabilitato.
* Procedura guidata di Azure AD Connect non mostra la sincronizzazione delle password effettiva hello e la configurazione di writeback delle password quando il server è in modalità di gestione temporanea. Indica sempre le due funzionalità come disabilitate.
* Sincronizzazione toopassword modifiche di configurazione e il writeback delle password non vengono mantenuti dalla procedura guidata di Azure AD Connect quando il server è in modalità di gestione temporanea.

**Miglioramenti:**

* Aggiornato tooindicate cmdlet Start-ADSyncSyncCycle hello se non è in grado di toosuccessfully inizio un nuovo ciclo di sincronizzazione o non.
* Ciclo di sincronizzazione tooterminate cmdlet aggiunti hello ADSyncSyncCycle di arresto e l'operazione, che sono attualmente in corso.
* Ciclo di sincronizzazione aggiornato hello Stop ADSyncScheduler cmdlet tooterminate e operazione, che sono attualmente in corso.
* Quando si configura [le estensioni di Directory](active-directory-aadconnectsync-feature-directory-extensions.md) nella procedura guidata di Azure AD Connect, ora è possibile selezionare l'attributo hello Azure AD di tipo "string Teletex".

## <a name="111890"></a>1.1.189.0
Data di rilascio: giugno 2016

**Problemi risolti e miglioramenti:**

* Ora Azure AD Connect può essere installato su un server conforme a FIPS.
  * Per la sincronizzazione della password, vedere [Sincronizzazione password e FIPS](active-directory-aadconnectsync-implement-password-synchronization.md#password-synchronization-and-fips).
* Risolto un problema in cui un nome NetBIOS non è stato risolto toohello FQDN in hello Active Directory Connector.

## <a name="111800"></a>1.1.180.0
Data di rilascio: maggio 2016

**Nuove funzionalità:**

* Visualizza avvisi e indicazioni riguardo alla verifica dei domini se la verifica non è stata effettuata prima di eseguire Azure AD Connect.
* Aggiunto il supporto per [Microsoft Cloud Germany](active-directory-aadconnect-instances.md#microsoft-cloud-germany).
* Aggiunto il supporto per la versione più recente hello [cloud di Microsoft Azure per enti pubblici](active-directory-aadconnect-instances.md#microsoft-azure-government-cloud) infrastruttura con i nuovi requisiti di URL.

**Problemi risolti e miglioramenti:**

* Toohello filtro aggiunto Editor regole di sincronizzazione toomake è facile toofind regole di sincronizzazione.
* Miglioramento delle prestazioni quando si elimina uno spazio connettore.
* Risolto un problema quando hello stesso oggetto è stato eliminato sia aggiunto in hello stessa esecuzione (chiamati delete/Aggiungi).
* Una regola di sincronizzazione disabilitata ora non riattiva più gli oggetti e gli attributi inclusi all'aggiornamento del sistema o dello schema della directory.

## <a name="111300"></a>1.1.130.0
Data di rilascio: aprile 2016

**Nuove funzionalità:**

* Aggiunto il supporto per gli attributi multivalore troppo[le estensioni di Directory](active-directory-aadconnectsync-feature-directory-extensions.md).
* Aggiunto il supporto per altre varianti di configurazione per [l'aggiornamento automatico](active-directory-aadconnect-feature-automatic-upgrade.md) toobe considerati idonei per l'aggiornamento.
* Aggiunti alcuni cmdlet per l' [utilità di pianificazione personalizzata](active-directory-aadconnectsync-feature-scheduler.md#custom-scheduler).

## <a name="111190"></a>1.1.119.0
Data di rilascio: marzo 2016

**Problemi risolti:**

* È stato verificato che non sia possibile usare l'installazione rapida in Windows Server 2008 (pre-R2), poiché la sincronizzazione delle password non è supportata in questo sistema operativo.
* L'aggiornamento da DirSync con una configurazione personalizzata del filtro non funzionava come previsto.
* Quando si aggiorna la versione più recente di tooa e sono non presenti alcuna configurazione toohello modifiche, non deve essere pianificata un'importazione o la sincronizzazione completa.

## <a name="111100"></a>1.1.110.0
Data di rilascio: febbraio 2016

**Problemi risolti:**

* L'aggiornamento da versioni precedenti non funziona se l'installazione di hello non è presente nella cartella C:\Program Files di hello predefinita.
* Se si installa e cancellare **avviare il processo di sincronizzazione hello** alla fine di hello dell'installazione guidata di hello, installazione guidata di hello in esecuzione una seconda volta non consentiranno l'utilità di pianificazione hello.
* utilità di pianificazione Hello non funziona come previsto nei server in hello formato di data e ora US-en non viene utilizzato. Non viene interrotto anche `Get-ADSyncScheduler` orari corretti tooreturn.
* Se è installata una versione precedente di Azure AD Connect con AD FS come hello aggiornamento e l'opzione di accesso, è possibile eseguire nuovamente l'installazione guidata di hello.

## <a name="111050"></a>1.1.105.0
Data di rilascio: febbraio 2016

**Nuove funzionalità:**

* [Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) per i clienti con impostazioni rapide.
* Supporto per l'amministratore globale di hello tramite Azure multi-Factor Authentication e Privileged Identity Management nell'installazione guidata di hello.
  * È necessario tooallow tooalso il proxy consentire il traffico toohttps://secure.aadcdn.microsoftonline-p.com se si utilizza l'autenticazione a più fattori.
  * È necessario l'elenco dei siti attendibili di tooadd https://secure.aadcdn.microsoftonline-p.com tooyour per lavoro tooproperly multi-Factor Authentication.
* Consente la modifica metodo di accesso dell'utente hello dopo l'installazione iniziale.
* Consenti [dominio e unità Organizzativa filtro](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) nell'installazione guidata di hello. Ciò consente anche di connessione tooforests in cui non tutti i domini sono disponibili.
* [Utilità di pianificazione](active-directory-aadconnectsync-feature-scheduler.md) viene compilato nel motore di sincronizzazione toohello.

**Funzionalità promozione dalla tooGA anteprima:**

* [Writeback dei dispositivi](active-directory-aadconnect-feature-device-writeback.md).
* [Estensioni della directory](active-directory-aadconnectsync-feature-directory-extensions.md).

**Nuove funzionalità di anteprima:**

* Hello nuovo predefinito ciclo di sincronizzazione intervallo è 30 minuti. Utilizzato toobe tre ore per tutte le versioni precedenti. Aggiunge il supporto toochange hello [dell'utilità di pianificazione](active-directory-aadconnectsync-feature-scheduler.md) comportamento.

**Problemi risolti:**

* Hello verificare pagina domini DNS non riconosciuta sempre domini hello.
* Richiesta di credenziali di amministratore del dominio durante la configurazione di AD FS.
* Hello locale gli account di Active Directory non sono riconosciuti dalla procedura guidata di installazione hello se si trova in un dominio con una struttura DNS differente dominio radice hello.

## <a name="1091310"></a>1.0.9131.0
Data di rilascio: dicembre 2015

**Problemi risolti:**

* La sincronizzazione delle password potrebbe non funzionare quando si modificano le password in Active Directory Domain Services (AD DS), ma funziona quando si imposta la password.
* Nella pagina Configurazione hello viene annullata quando si dispone di un server proxy, l'autenticazione tooAzure AD potrebbe non riuscire durante l'installazione, oppure se un aggiornamento.
* L'aggiornamento da una versione precedente di Azure AD Connect con un'istanza completa di SQL Server avrà esito negativo se non si è SA (amministratore di sistema) in SQL Server.
* L'aggiornamento da una versione precedente di Azure AD Connect, con un Server SQL remoto Mostra l'errore "Impossibile tooaccess hello database SQL di ADSync" hello.

## <a name="1091250"></a>1.0.9125.0
Data di rilascio: novembre 2015

**Nuove funzionalità:**

* Possibile riconfigurare la relazione di trust tooAzure AD ADFS.
* Puoi aggiornare lo schema di Active Directory hello e rigenerare le regole di sincronizzazione.
* È possibile disattivare una regola di sincronizzazione.
* È possibile definire "AuthoritativeNull" come un nuovo valore letterale in una regola di sincronizzazione.

**Nuove funzionalità di anteprima:**

* [Azure AD Connect Health per la sincronizzazione](../connect-health/active-directory-aadconnect-health-sync.md).
* Supporto per la sincronizzazione della password dei [Servizi di dominio di Azure AD](../active-directory-passwords-update-your-own-password.md)

**Nuovo scenario supportato:**

* Supporta più organizzazioni di Exchange locali Per altre informazioni, vedere [Distribuzioni ibride con più foreste di Active Directory](https://technet.microsoft.com/library/jj873754.aspx).

**Problemi risolti:**

* Problemi sulla sincronizzazione delle password:
  * Oggetto spostato dall'ambito tooin out-of-scope non avranno la sincronizzazione delle password. Questo include unità Organizzativa e filtro attributi.
  * Selezione di un nuovo tooinclude OU sincronizzati non richiede una sincronizzazione completa delle password.
  * Quando un utente disabilitato è abilitato la password di hello non vengono sincronizzati.
  * coda di tentativi di password Hello è infinita e hello precedente, pari a 5.000 toobe oggetti ritirato sono stato rimosso.
* Non è possibile tooconnect tooActive Directory con livello di funzionalità con l'insieme di strutture di Windows Server 2016.
* Gruppo di hello toochange non è possibile che viene utilizzato per il filtro di gruppo dopo l'installazione iniziale di hello.
* Non crea un nuovo profilo utente nel server di Azure AD Connect hello per ogni utente che esegue una modifica della password con writeback delle password abilitata.
* Non è possibile toouse Long Integer i valori degli ambiti delle regole di sincronizzazione.
* casella di controllo Hello "writeback dei dispositivi" rimane disabilitato se sono presenti controller di dominio non è raggiungibile.

## <a name="1086670"></a>1.0.8667.0
Data di rilascio: agosto 2015

**Nuove funzionalità:**

* Hello Azure AD Connect, installazione guidata è ora localizzate tooall lingue di Windows Server.
* È stato aggiunto il supporto per lo sblocco dell'account quando si usa la gestione delle password di Azure AD.

**Problemi risolti:**

* Installazione guidata di Azure AD Connect si blocca se un altro utente continua a installazione anziché persona hello iniziato installazione hello.
* Se una disinstallazione precedente di Azure AD Connect toouninstall sincronizzazione di Azure AD Connect non funziona correttamente, non è possibile tooreinstall.
* Non è possibile installare Azure AD Connect con installazione rapida, se l'utente di hello non è presente nel dominio radice hello della foresta hello o se viene utilizzata una versione inglese di Active Directory.
* Se non è possibile risolvere il FQDN di account utente di Active Directory hello hello, viene visualizzato un messaggio di errore fuorviante "Schema hello toocommit non riuscito".
* Se l'account hello utilizzato su hello Active Directory Connector è stato modificato all'esterno di guidata hello, la procedura guidata hello ha esito negativo nelle esecuzioni successive.
* Azure AD Connect non riesce a volte tooinstall in un controller di dominio.
* Non è possibile abilitare e disabilitare la "Modalità di gestione temporanea" se sono stati aggiunti attributi di estensione.
* Writeback delle password ha esito negativo in alcune configurazioni a causa di una password scorretta hello Active Directory Connector.
* Non è possibile aggiornare DirSync se si usa un nome distinto (DN) nel filtro di attributi.
* Utilizzo eccessivo della CPU quando si utilizza la reimpostazione della password.

**Funzionalità di anteprima rimosse:**

* funzionalità di anteprima Hello [writeback degli utenti](active-directory-aadconnect-feature-preview.md#user-writeback) temporaneamente è stato rimosso in base ai commenti e suggerimenti dai clienti di anteprima. Verranno aggiunti nuovamente in seguito dopo che è stato risolto hello fornito commenti e suggerimenti.

## <a name="1086410"></a>1.0.8641.0
Data di rilascio: giugno 2015

**Rilascio iniziale di Azure AD Connect.**

Nome modificato da Azure AD Sync tooAzure AD Connect.

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

* Azure AD Sync richiede ora hello .NET Framework versione 4.5.1 toobe installato.

**Problemi risolti:**

* Il writeback delle password da Azure AD ha esito negativo con un errore di connettività del bus di servizio.

## <a name="104910413"></a>1.0.491.0413
Data di rilascio: aprile 2015

**Problemi risolti e miglioramenti:**

* Hello Active Directory Connector non elabora correttamente le eliminazioni se è abilitato il Cestino hello e sono presenti più domini nella foresta hello.
* Hello prestazioni delle operazioni di importazione sono state migliorate per hello Azure Active Directory Connector.
* Quando un gruppo ha superato il limite di appartenenza hello (per impostazione predefinita, hello limite too50, oggetti 000), gruppo hello è stato eliminato in Azure Active Directory. Con nuovi comportamenti hello, hello gruppo non viene eliminato, viene generato un errore e non vengono esportate le nuove modifiche di appartenenza.
* Un nuovo oggetto non è possibile eseguirne il provisioning se un'operazione di eliminazione gestione temporanea con hello che DN stesso è già presente nello spazio connettore hello.
* Alcuni oggetti sono contrassegnati per la sincronizzazione durante una sincronizzazione delta anche se è presente alcuna modifica pre-installata nei oggetto hello.
* Forzare una sincronizzazione password rimuove anche l'elenco di controller di dominio hello preferito.
* Si sono verificati problemi di CSExportAnalyzer con alcuni stati degli oggetti.

**Nuove funzionalità:**

* Un join è ora possibile connettersi in hello MV troppo "ANY" tipo di oggetto.

## <a name="104850222"></a>1.0.485.0222
Data di rilascio: febbraio 2015

**Miglioramenti:**

* Prestazioni migliorate per l'importazione.

**Problemi risolti:**

* Sincronizzazione delle password rispetta l'attributo cloudFiltered hello utilizzato dal filtro di attributi. Gli oggetti filtrati non sono più inclusi nell'ambito per la sincronizzazione delle password.
* In rare situazioni in cui la topologia hello ha molti controller di dominio, non viene eseguita la sincronizzazione delle password.
* "Stopped-server" durante l'importazione da Azure Active Directory Connector hello dopo la gestione dei dispositivi è stata abilitata in Azure AD/Intune.
* L'aggiunta di entità di protezione esterne da più domini nella stessa foresta provoca un errore di join ambiguo.

## <a name="104751202"></a>1.0.475.1202
Data di rilascio: dicembre 2014

**Nuove funzionalità:**

* È ora supportata l'esecuzione della sincronizzazione delle password con filtri basati sugli attributi. Per informazioni dettagliate, vedere [Sincronizzazione delle password con i filtri](active-directory-aadconnectsync-configure-filtering.md).
* attributo msDS-ExternalDirectoryObjectID Hello verrà riscritti tooActive Directory. Questa funzionalità aggiunge il supporto per applicazioni di Office 365. Usa OAuth2 tooaccess cassette postali Online e locali in una distribuzione ibrida di Exchange.

**Problemi di aggiornamento risolti:**

* Una versione più recente dell'Assistente per l'accesso hello è disponibile nel server di hello.
* Un percorso di installazione personalizzato è stato utilizzato tooinstall Azure AD Sync.
* Un aggiornamento di hello blocchi criterio di join personalizzato non valido.

**Altre correzioni:**

* Modelli di hello fissa per Office Pro Plus.
* I problemi di installazione provocati dai nomi utente che iniziano con un trattino sono stati risolti.
* Correzione dell'impostazione sourceAnchor hello perdente durante l'installazione guidata di hello una seconda volta.
* Il problema relativo alla traccia ETW per la sincronizzazione delle password è stato risolto.

## <a name="104701023"></a>1.0.470.1023
Data di rilascio: ottobre 2014

**Nuove funzionalità:**

* La sincronizzazione delle password da più locale tooAzure Active Directory Active Directory.
* Lingue di Windows Server tooall dell'interfaccia utente di installazione localizzato.

**Aggiornamento da AADSync 1.0 GA**

Se hai già installato Azure AD Sync, è un passaggio aggiuntivo è tootake nel caso in cui sono state modificate le hello out-of-box delle regole di sincronizzazione. Dopo aver aggiornato la versione toohello 1.0.470.1023, le regole di sincronizzazione hello modificate vengono duplicate. Per ogni regola di sincronizzazione modificata, hello seguenti:

1.  Individuare una regola di sincronizzazione hello è stata modificata e prendere nota delle modifiche di hello.
* Eliminare la regola di sincronizzazione hello.
* Individuare hello nuova regola di sincronizzazione creata da Azure AD Sync e riapplicare le modifiche di hello.

**Autorizzazioni per hello account Active Directory**

Hello account Active Directory deve essere concesse hash delle password di ulteriori autorizzazioni toobe tooread in grado di hello da Active Directory. Hello autorizzazioni toogrant sono denominati "Replica modifiche Directory" e "Replica di tutte modifiche Directory." Entrambe le autorizzazioni sono gli hash delle password necessarie toobe tooread in grado di hello.

## <a name="104190911"></a>1.0.419.0911
Data di rilascio: settembre 2014

**Rilascio iniziale di Azure AD Sync.**

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
