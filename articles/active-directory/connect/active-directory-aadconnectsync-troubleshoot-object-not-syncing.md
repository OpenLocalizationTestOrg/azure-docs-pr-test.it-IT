---
title: "oggetto che è non in sincronizzazione tooAzure AD aaaTroubleshoot | Microsoft documenti"
description: "Risolvere il motivo per cui un oggetto è non in sincronizzazione tooAzure Active Directory."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 81e0a0793a1d5ec76cfcaec6e974726d7854f58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-an-object-that-is-not-synchronizing-tooazure-ad"></a>Risolvere i problemi relativi a un oggetto che è non in sincronizzazione tooAzure AD

Se un oggetto è non in sincronizzazione come previsto tooAzure Active Directory, è possibile a causa di motivi diversi. Se si hanno ricevuto un messaggio di errore da Azure AD o se viene visualizzato l'errore hello in Azure AD Connect Health, leggere [risolvere gli errori di esportazione](active-directory-aadconnect-troubleshoot-sync-errors.md) invece. Ma se si sta risolvendo un problema in oggetto hello non è in Azure AD, quindi in questo argomento per l'utente. Descrive la modalità di sincronizzazione toofind errori nel componente on-premise hello Azure AD Connect.

errori di hello toofind, si sta toolook in vari punti in hello seguente ordine:

1. Hello [registri operazioni](#operations) per la ricerca di errori identificati dal motore di sincronizzazione hello durante l'importazione e la sincronizzazione.
2. Hello [spazio connettore](#connector-space-object-properties) per trovare gli oggetti mancanti e gli errori di sincronizzazione.
3. Hello [metaverse](#metaverse-object-properties) per la ricerca di problemi relativi ai dati.

Avviare [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md) prima di iniziare questa procedura.

## <a name="operations"></a>Operazioni
scheda operazioni Hello in hello Synchronization Service Manager è in cui è necessario avviare la risoluzione dei problemi. scheda operazioni Hello Mostra i risultati di hello delle operazioni più recenti di hello.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/operations.png)  

Nella metà superiore Hello Mostra tutte le esecuzioni in ordine cronica. Per impostazione predefinita, i log di operazioni hello mantiene informazioni hello negli ultimi sette giorni, ma questa impostazione può essere modificata con hello [dell'utilità di pianificazione](active-directory-aadconnectsync-feature-scheduler.md). Si desidera toolook per qualsiasi esecuzione che mostrano uno stato di esito positivo. È possibile modificare l'ordinamento facendo clic sulle intestazioni hello hello.

Hello **stato** colonna è informazioni più importanti hello e Mostra hello problema più grave per l'esecuzione. Ecco un breve riepilogo di stato di hello più comuni in ordine di priorità tooinvestigate (dove * indicare diverse stringhe di messaggio di errore).

| Stato | Commento |
| --- | --- |
| stopped-* |non è stato possibile completare Hello eseguire. Ad esempio, se hello sistema remoto è inattivo e non può essere contattato. |
| stopped-error-limit |Sono presenti più di 5.000 errori. eseguire Hello automaticamente è stato arrestato a causa di toohello numero elevato di errori. |
| completato-\*-errori |Hello eseguire completata, ma sono presenti errori (meno di 5.000) che devono essere esaminati. |
| completato-\*-avvisi |eseguire Hello completata, ma alcuni dati non sono in stato di hello previsto. Se sono presenti errori, questo messaggio è in genere solo un sintomo. Evitare di analizzare gli avvisi fino a quando gli errori non sono stati risolti. |
| esito positivo |Non sono presenti problemi. |

Quando si seleziona una riga, nella parte inferiore di hello Aggiorna i dettagli di hello tooshow di esecuzione. toohello all'estrema sinistra della parte inferiore di hello, si potrebbe ricevere un detto elenco **passaggio #**. L'elenco è mostrato solo quando nella foresta sono presenti più domini e ogni dominio è rappresentato da un passaggio. è possibile trovare il nome di dominio Hello titolo hello **partizione**. In **le statistiche della sincronizzazione**, è possibile trovare altre informazioni sul numero di hello di modifiche che sono stati elaborati. È possibile fare clic su hello collegamenti tooget un elenco di oggetti hello modificato. Se alcuni oggetti presentano errori, questi verranno visualizzati in **Synchronization Errors**(Errori di sincronizzazione).

### <a name="troubleshoot-errors-in-operations-tab"></a>Risolvere gli errori nella scheda Operazioni
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/errorsync.png)  
Quando sono presenti errori, sia oggetto hello in errore ed errore hello stesso sono collegamenti che forniscono ulteriori informazioni.

Avvio, fare clic sulla stringa di errore hello (**attivato sincronizzazione-regola-errore-funzione** immagine hello). Innanzitutto viene visualizzata una panoramica dell'oggetto hello. toosee hello errore effettivo, fare clic sul pulsante hello **dello stack**. Questa traccia fornisce informazioni a livello di debug per correggere l'errore hello.

È possibile fare doppio clic in hello **informazioni sullo stack** scegliere **Seleziona tutto**, e **copia**. È quindi possibile copiare stack hello ed esaminare errore hello l'editor preferito, ad esempio Blocco note.

* Se l'errore hello è da **SyncRulesEngine**, informazioni sullo stack di chiamate hello innanzitutto ha un elenco di tutti gli attributi nell'oggetto hello. Scorrere verso il basso fino a visualizzare il titolo di hello **InnerException = >**.  
  ![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/errorinnerexception.png)  
  riga Hello dopo Mostra hello errore. Nella figura hello precedente, errore hello è da un Fabrikam regola di sincronizzazione personalizzato creato.

Se l'errore hello stesso non fornisce informazioni sufficienti, è ora toolook dati hello stesso. È possibile fare clic sul collegamento hello con l'identificatore di oggetto hello e continuare la risoluzione dei problemi hello [connettore spazio oggetto importato](#cs-import).

## <a name="connector-space-object-properties"></a>Proprietà dell’oggetto spazio connettore
Se non si dispone degli eventuali errori rilevati in hello [operazioni](#operations) scheda, il passaggio successivo hello è toofollow oggetto spazio connettore di hello da Active Directory e metaverse toohello tooAzure Active Directory. In questo percorso, è necessario trovare dove problema hello è.

### <a name="search-for-an-object-in-hello-cs"></a>Eseguire la ricerca di un oggetto in hello. CS

In **Synchronization Service Manager**, fare clic su **connettori**, selezionare il connettore di Active Directory, di hello e **spazio connettore ricerca**.

In **ambito**selezionare **RDN** (quando si desidera toosearch sull'attributo CN hello) o **DN o ancoraggio** (quando si desidera toosearch sull'attributo distinguishedName hello). Immettere un valore e fare clic su **Cerca**.  
![Ricerca spazio connettore](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssearch.png)  

Se non si trova l'oggetto hello si sta cercando, quindi potrebbe sono stati filtrato con [il filtro basato su dominio](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) o [il filtro basato su unità Organizzativa](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering). Hello lettura [configurare il filtro](active-directory-aadconnectsync-configure-filtering.md) tooverify argomento che hello filtro è configurato come previsto.

Un'altra ricerca utile è tooselect hello Azure Active Directory Connector, **ambito** selezionare **importazione in sospeso**e seleziona hello **Aggiungi** casella di controllo. Questa ricerca restituisce tutti gli oggetti sincronizzati in Azure AD che non possono essere associati a un oggetto locale.  
![Orfano ricerca spazio connettore](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssearchorphan.png)  
Tali oggetti sono stati creati da un altro motore di sincronizzazione o da un motore di sincronizzazione con una diversa configurazione filtro. Questa vista contiene un elenco di oggetti **orfani** non più gestiti. È necessario esaminare l'elenco e provare a rimuovere questi oggetti tramite hello [Azure AD PowerShell](http://aka.ms/aadposh) cmdlet.

### <a name="cs-import"></a>Importazione CS
Quando si apre un oggetto cs, esistono diverse schede nella parte superiore di hello. Hello **importare** scheda Mostra dati hello preconfigurato dopo un'importazione.  
![Oggetto CS](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/csobject.png)    
Hello **vecchio valore** Mostra il contenuto attualmente archiviato in Connetti ed hello **nuovo valore** cosa è stata ricevuta dal sistema di origine hello e non è stata ancora applicata. Se si verifica un errore nell'oggetto hello, le modifiche non vengono elaborate.

**Errore**  
![Oggetto CS](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssyncerror.png)  
Hello **errore di sincronizzazione** scheda è visibile solo se si è verificato un problema con l'oggetto hello. Per altre informazioni, vedere l'articolo su come [risolvere gli errori di sincronizzazione](#troubleshoot-errors-in-operations-tab).

### <a name="cs-lineage"></a>Derivazione CS
scheda derivazione Hello vengono illustrate oggetto spazio connettore di hello oggetto metaverse toohello correlati. È possibile visualizzare quando hello connettore ultima importato una modifica dal sistema connesso hello e quali dati toopopulate regole applicate hello metaverse.  
![Derivazione CS](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cslineage.png)  
In hello **azione** colonna, è possibile visualizzare presente **in ingresso** regola di sincronizzazione con azione hello **provisioning**. Che indica se questo oggetto spazio connettore è presente, oggetto metaverse hello rimane. Se elenco hello di regole di sincronizzazione viene invece una regola di sincronizzazione con direzione **in uscita** e **provisioning**, indica che questo oggetto viene eliminato quando viene eliminato l'oggetto metaverse hello.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cslineageout.png)  
È inoltre possibile visualizzare in hello **PasswordSync** colonna hello spazio connettore di ingresso può contribuire password toohello modifiche poiché una regola di sincronizzazione ha il valore di hello **True**. Questa password viene quindi inviata tooAzure Active Directory tramite la regola in uscita hello.

Dalla scheda derivazione hello, è possibile ottenere toohello metaverse facendo [proprietà oggetto Metaverse](#mv-attributes).

Nella parte inferiore di hello di tutte le schede sono due pulsanti: **anteprima** e **Log**.

### <a name="preview"></a>Preview
pagina di anteprima Hello è toosynchronize utilizzato un singolo oggetto. È utile se si siano cercando di risolvere alcune regole di sincronizzazione personalizzate e si desidera toosee hello effetto di una modifica in un singolo oggetto. È possibile scegliere tra **Sincronizzazione completa** e **Sincronizzazione delta**. È inoltre possibile selezionare tra **generare anteprima**, che mantiene solo le modifiche hello in memoria, e **anteprima Commit**, quale aggiornare metaverse hello e tutte le fasi modifiche spazi connettore tootarget.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/preview.png)  
È possibile esaminare l'oggetto hello e applicata la regola per un particolare flusso di attributi.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/previewresult.png)

### <a name="log"></a>Log
pagina Log Hello è stato di sincronizzazione password hello toosee usato e la cronologia. Per altre informazioni, vedere [Risolvere i problemi di sincronizzazione delle password](active-directory-aadconnectsync-troubleshoot-password-synchronization.md).

## <a name="metaverse-object-properties"></a>Proprietà dell'oggetto Metaverse
È in genere è preferibile toostart ricerca da Active Directory di origine hello [spazio connettore](#connector-space). Ma è anche possibile avviare la ricerca di metaverse hello.

### <a name="search-for-an-object-in-hello-mv"></a>Ricerca di un oggetto in hello MV
In **Synchronization Service Manager**, fare clic su **Metaverse Search** (Cerca Metaverse). Creare una query che si conosce trova hello utente. È possibile cercare gli attributi comuni, ad esempio accountName (sAMAccountName) e userPrincipalName. Per altre informazioni, vedere [Cerca Metaverse](active-directory-aadconnectsync-service-manager-ui-mvsearch.md).
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvsearch.png)  

In hello **risultati della ricerca** finestra, fare clic su oggetto hello.

Se l'oggetto hello non è disponibile, quindi non ha ancora raggiunto hello metaverse. Continuare toosearch per oggetto hello in Active Directory hello [spazio connettore](#connector-space-object-properties). Potrebbe esserci un errore di sincronizzazione che sta bloccando l'oggetto metaverse toohello prossimi hello o potrebbe essere presente un filtro applicato.

### <a name="mv-attributes"></a>Attributi MV
Nella scheda attributi hello, è possibile visualizzare i valori hello e hanno contribuito il connettore.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvobject.png)  

Se un oggetto non viene sincronizzato, quindi esaminare hello gli attributi nel metaverse hello seguenti:
- Attributo hello **cloudFiltered** presenti e impostate troppo**true**? Se è, quindi sono stati filtrato in base a passaggi toohello [filtro basato su attributo](active-directory-aadconnectsync-configure-filtering.md#attribute-based-filtering).
- Attributo hello **sourceAnchor** presente? Se non lo è, si dispone di una topologia di foresta account-risorse? Se un oggetto viene identificato come una cassetta postale collegata (attributo hello **msExchRecipientTypeDetails** hello valore 2), quindi sourceAnchor hello è fornita dalla foresta hello con un account di Active Directory abilitato. Verificare che l'account principale hello è stato importato e sincronizzati correttamente. Hello master deve essere elencato in hello [connettori](#mv-connectors) per oggetto hello.

### <a name="mv-connectors"></a>Connettori MV
scheda Connectors Hello Mostra tutti gli spazi connettore che dispongono di una rappresentazione dell'oggetto hello.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvconnectors.png)  
È necessario disporre di un connettore per:

- Ogni utente hello foresta di Active Directory viene rappresentato in. Questa rappresentazione può includere foreignSecurityPrincipals e gli oggetti Contatto.
- Un connettore in Azure AD.

Se mancano hello connettore tooAzure Active Directory, quindi leggere [attributi MV](#MV-attributes) criteri hello tooverify per essere eseguito il provisioning tooAzure Active Directory.

Questa scheda consente anche toonavigate toohello [oggetto spazio connettore](#connector-space-object-properties). Selezionare una riga e fare clic su **Proprietà**.

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su hello [sincronizzazione di Azure AD Connect](active-directory-aadconnectsync-whatis.md) configurazione.

Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
