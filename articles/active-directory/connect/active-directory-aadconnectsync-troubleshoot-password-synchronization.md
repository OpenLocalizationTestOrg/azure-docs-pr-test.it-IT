---
title: sincronizzazione delle password aaaTroubleshoot con sincronizzazione di Azure AD Connect | Documenti Microsoft
description: In questo articolo fornisce informazioni su come i problemi di sincronizzazione password tootroubleshoot.
services: active-directory
documentationcenter: 
author: AndKjell
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
ms.openlocfilehash: 390eafec792cb39251627c14cb754f8bb30035b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a>Risolvere i problemi di sincronizzazione della password con il servizio di sincronizzazione Azure AD Connect
Questo argomento illustra i passaggi per la modalità tootroubleshoot problemi con la sincronizzazione delle password. Se le password non vengono sincronizzate come previsto, il problema può riguardare un subset di utenti o tutti gli utenti. Per Azure Active Directory (Azure AD) connettere distribuzione con la versione 1.1.524.0 o versioni successive, è ora disponibile un cmdlet di diagnostica che è possibile utilizzare tootroubleshoot problemi di sincronizzazione password:

* Se si dispone di un problema in cui non vengono sincronizzati alcuna password, consultare toohello [non le password vengono sincronizzate: risolvere i problemi utilizzando i cmdlet di diagnostica hello](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) sezione.

* Se si dispone di un problema con i singoli oggetti, consultare toohello [un oggetto è non in sincronizzazione password: risolvere i problemi utilizzando i cmdlet di diagnostica hello](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) sezione.

Per le versioni precedenti della distribuzione di Azure AD Connect:

* Se si dispone di un problema in cui non vengono sincronizzati alcuna password, consultare toohello [non le password vengono sincronizzate: risoluzione manuale](#no-passwords-are-synchronized-manual-troubleshooting-steps) sezione.

* Se si dispone di un problema con i singoli oggetti, consultare toohello [un oggetto è non in sincronizzazione password: risoluzione manuale](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) sezione.

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-hello-diagnostic-cmdlet"></a>Nessun password vengono sincronizzate: risolvere i problemi utilizzando i cmdlet di diagnostica hello
È possibile utilizzare hello `Invoke-ADSyncDiagnostics` toofigure cmdlet out perché nessuna password è sincronizzata.

> [!NOTE]
> Hello `Invoke-ADSyncDiagnostics` cmdlet è disponibile solo per la versione di Azure AD Connect 1.1.524.0 o versione successiva.

### <a name="run-hello-diagnostics-cmdlet"></a>Eseguire i cmdlet di diagnostica hello
problemi di tootroubleshoot in cui non vengono sincronizzati alcuna password:

1. Aprire una nuova sessione di Windows PowerShell nel server di Azure AD Connect con hello **Esegui come amministratore** opzione.

2. Eseguire `Set-ExecutionPolicy RemoteSigned` o `Set-ExecutionPolicy Unrestricted`.

3. Eseguire `Import-Module ADSyncDiagnostics`.

4. Eseguire `Invoke-ADSyncDiagnostics -PasswordSync`.

### <a name="understand-hello-results-of-hello-cmdlet"></a>Comprendere i risultati di hello del cmdlet hello
cmdlet di diagnostica Hello esegue hello seguenti controlli:

* Convalida che hello funzionalità di sincronizzazione password è abilitata per il tenant di Azure AD.

* Convalida che hello Azure AD Connect, server non è in modalità di gestione temporanea.

* Per ogni esistente locali di Active Directory connector (che corrisponde a foresta Active Directory esistente tooan):

   * Convalida che hello è abilitata la funzionalità di sincronizzazione password.
   
   * Cerca gli eventi di heartbeat di sincronizzazione password in hello registri eventi applicazioni di Windows.

   * Per ogni dominio di Active Directory in connettore di Active Directory locale hello:

      * Convalida che hello dominio sia raggiungibile dal server di hello Azure AD Connect.

      * Verifica che gli account di servizi di dominio Active Directory (AD DS) hello usati dal connettore di Active Directory locale hello è hello correttezza del nome utente, password e delle autorizzazioni necessarie per la sincronizzazione delle password.

Hello seguente diagramma illustra i risultati di hello del cmdlet hello per una topologia di Active Directory locale a dominio singolo:

![Output di diagnostica per la sincronizzazione delle password](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

Hello in questa sezione descrive i risultati specifici che vengono restituiti dal cmdlet hello e problemi corrispondenti.

#### <a name="password-synchronization-feature-isnt-enabled"></a>La funzionalità di sincronizzazione delle password non è abilitata
Se è stata abilitata la sincronizzazione delle password utilizzando la procedura guidata di hello Azure AD Connect, viene restituito il seguente errore hello:

![La sincronizzazione delle password non è abilitata](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a>Il server di Azure AD Connect è in modalità di gestione temporanea
Se il server di Azure AD Connect hello è in modalità di gestione temporanea, la sincronizzazione delle password è temporaneamente disabilitata e hello seguente errore:

![Il server di Azure AD Connect è in modalità di gestione temporanea](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a>Eventi heartbeat di mancata sincronizzazione delle password
Ogni istanza locale di Active Directory Connector ha uno specifico canale di sincronizzazione delle password. Quando viene stabilito canale di sincronizzazione password hello e non vi sono eventuali toobe modifiche password sincronizzate, un evento di heartbeat (EventId 654) viene generato una volta ogni 30 minuti nel registro eventi applicazioni di Windows hello. Per ogni connettore di Active Directory locale, hello cmdlet Cerca eventi heartbeat corrispondenti in hello ultime tre ore. Se non viene trovato alcun evento di heartbeat, hello seguente errore:

![Evento heartbeat di mancata sincronizzazione delle password](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a>L'account di Active Directory Domain Services non ha le autorizzazioni corrette
Se l'account di hello di dominio Active Directory che viene usato da hello locale hash delle password di Active Directory connector toosynchronize non dispone delle autorizzazioni appropriate di hello, hello seguente errore:

![Credenziali non corrette](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a>La password o il nome utente dell'account di Active Directory Domain Services non è corretto
Se hello account di dominio Active Directory utilizzata da hello gli hash delle password locali Active Directory connector toosynchronize ha un nome utente non corretto o la password, hello seguente errore:

![Credenziali non corrette](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-hello-diagnostic-cmdlet"></a>Un oggetto è non in sincronizzazione password: risolvere i problemi utilizzando i cmdlet di diagnostica hello
È possibile utilizzare hello `Invoke-ADSyncDiagnostics` toodetermine cmdlet perché un oggetto è non in sincronizzazione delle password.

> [!NOTE]
> Hello `Invoke-ADSyncDiagnostics` cmdlet è disponibile solo per la versione di Azure AD Connect 1.1.524.0 o versione successiva.

### <a name="run-hello-diagnostics-cmdlet"></a>Eseguire i cmdlet di diagnostica hello
problemi di tootroubleshoot in cui non vengono sincronizzati alcuna password:

1. Aprire una nuova sessione di Windows PowerShell nel server di Azure AD Connect con hello **Esegui come amministratore** opzione.

2. Eseguire `Set-ExecutionPolicy RemoteSigned` o `Set-ExecutionPolicy Unrestricted`.

3. Eseguire `Import-Module ADSyncDiagnostics`.

4. Eseguire hello seguente cmdlet:
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   ad esempio:
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-hello-results-of-hello-cmdlet"></a>Comprendere i risultati di hello del cmdlet hello
cmdlet di diagnostica Hello esegue hello seguenti controlli:

* Esamina lo stato di hello dell'oggetto di Active Directory hello spazio connettore di Active Directory hello Metaverse e Azure spazio connettore di Active Directory.

* Convalida che non esistono regole di sincronizzazione con la sincronizzazione delle password è abilitata e applicata toohello oggetto di Active Directory.

* Prova tooretrieve e visualizzare risultati hello di hello ultimo tentativo toosynchronize hello password per l'oggetto hello.

Hello seguente diagramma illustra i risultati di hello del cmdlet hello quando la risoluzione dei problemi di sincronizzazione delle password per un singolo oggetto:

![Output di diagnostica per la sincronizzazione delle password: singolo oggetto](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

Hello in questa sezione descrive i risultati specifici restituiti dal cmdlet hello e problemi corrispondenti.

#### <a name="hello-active-directory-object-isnt-exported-tooazure-ad"></a>oggetto di Active Directory Hello non esportati tooAzure AD
La sincronizzazione delle password per l'account di Active Directory locale non riesce perché è presente alcun oggetto corrispondente nel tenant di Azure AD hello. viene restituito l'errore seguente Hello:

![Oggetto Azure AD mancante](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a>L'utente ha una password temporanea
Azure AD Connect non supporta attualmente la sincronizzazione delle password temporanee con Azure AD. Una password viene considerata toobe temporaneo se hello **Cambia password all'accesso successivo** opzione è impostata su utente di Active Directory locale hello. viene restituito l'errore seguente Hello:

![Password temporanea non esportata](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-toosynchronize-password-arent-available"></a>Risultati dell'ultimo tentativo toosynchronize password non sono disponibili
Per impostazione predefinita, Azure AD Connect archivia i risultati di hello dei tentativi di sincronizzazione password per sette giorni. Se non sono disponibili per l'oggetto di Active Directory hello selezionato alcun risultato, viene restituito hello seguente avviso:

![Output di diagnostica per un singolo oggetto: cronologia di mancata sincronizzazione delle password](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a>Nessuna password viene sincronizzata: passaggi per la risoluzione manuale dei problemi
Seguire questi passaggi toodetermine perché nessuna password venga sincronizzata:

1. È il server di connessione hello in [modalità di gestione temporanea](active-directory-aadconnectsync-operations.md#staging-mode)? Un server in modalità di gestione temporanea non sincronizza le password.

2. Eseguire script hello in hello [ottenere lo stato di hello di impostazioni di sincronizzazione password](#get-the-status-of-password-sync-settings) sezione. Fornisce una panoramica della configurazione di sincronizzazione password hello.  

    ![Output dello script di PowerShell dalle impostazioni di sincronizzazione password](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. Se la funzione hello non è abilitata in Azure AD o hello sincronizzazione canale stato non è abilitato, eseguire hello Connetti installazione guidata. Selezionare **Personalizzazione delle opzioni di sincronizzazione** e deselezionare l'opzione di sincronizzazione delle password. Questa modifica Disabilita temporaneamente funzionalità hello. Quindi eseguire nuovamente la procedura guidata hello e riattivare la sincronizzazione delle password. Eseguire script hello nuovamente tooverify che hello configurazione sia corretto.

4. Cercare nel registro eventi di hello per gli errori. Cercare hello eventi, che potrebbe indicare un problema di seguito:
    * Origine: ID "Sincronizzazione della directory": 0, 611, 652, 655 Se vengono visualizzati eventi di questo tipo, c'è un problema di connettività. messaggio registro eventi contiene informazioni relative alla foresta in cui si verifica un problema. Per altre informazioni, vedere [Problemi di connettività](#connectivity problem).

5. Se non viene visualizzato alcun heartbeat o non si sono trovate altre soluzioni al problema, eseguire lo script riportato in [Attivare una sincronizzazione completa di tutte le password](#trigger-a-full-sync-of-all-passwords). Eseguire script hello una sola volta.

6. Vedere hello [risolvere i problemi relativi a un oggetto che è non in sincronizzazione password](#one-object-is-not-synchronizing-passwords) sezione.

### <a name="connectivity-problems"></a>Problemi di connettività

La connettività con Azure AD è presente?

Account hello sono richieste autorizzazioni tooread hello gli hash delle password in tutti i domini? Se è stato installato utilizzando le impostazioni rapide Connect, le autorizzazioni di hello dovrebbero già essere corrette. 

Se si utilizza l'installazione personalizzata, impostare manualmente le autorizzazioni di hello eseguendo hello seguenti:
    
1. account di hello toofind utilizzato dal connettore di Active Directory hello, inizio **Synchronization Service Manager**. 
 
2. Andare troppo**connettori**e quindi cercare nella foresta di Active Directory locale hello risoluzione. 
 
3. Selezionare il connettore hello e quindi fare clic su **proprietà**. 
 
4. Andare troppo**connettersi foresta Directory tooActive**.  
    
    ![Account usato da Active Directory Connector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    Si noti username hello e dominio hello account hello in cui si trova.
    
5. Avviare **Active Directory Users and Computers**, quindi verificare che account hello individuati in precedenza disponga delle autorizzazioni di seguire hello impostata nella radice di hello di tutti i domini della foresta:
    * Replica modifiche directory
    * Replica modifiche directory - Tutto

6. È hello controller di dominio raggiungibile da Azure AD Connect? Se il server di connessione hello è possibile connettersi tooall i controller di dominio, configurare **utilizzare solo i controller di dominio preferito**.  
    
    ![Controller di dominio usato da Active Directory Connector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. Tornare indietro troppo**Synchronization Service Manager** e **configurare partizione di Directory**. 
 
8. Selezionare il dominio in **seleziona partizioni di directory**selezionare hello **utilizzare solo i controller di dominio preferito** casella di controllo e quindi fare clic su **configura**. 

9. Nell'elenco di hello, immettere i controller di dominio hello Connetti devono utilizzare per la sincronizzazione delle password. Hello stesso elenco viene utilizzato per importare ed esportare anche. Eseguire questi passaggi per tutti i domini.

10. Se uno script hello mostra che non è stato rilevato alcun heartbeat, è possibile eseguire script di hello in [attivare una sincronizzazione completa di tutte le password](#trigger-a-full-sync-of-all-passwords).

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a>Un oggetto non sincronizza le password: passaggi per la risoluzione manuale dei problemi
Esaminando hello lo stato di un oggetto, è possibile risolvere facilmente i problemi di sincronizzazione password.

1. In **Active Directory Users and Computers**, cercare hello utente e quindi verificare che hello **cambiamento obbligatorio password all'accesso successivo** casella di controllo è deselezionata.  

    ![Password per la produttività di Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    Se è selezionata la casella di controllo hello, porre toosign utente hello in e modificare la password di hello. Le password temporanee non vengono sincronizzate con Azure AD.

2. Se la password di hello corretto in Active Directory, seguire utente hello nel motore di sincronizzazione hello. Utente seguente hello tooAzure di Active Directory locale AD, consente di visualizzare se si verifica un errore descrittivo sull'oggetto hello.

    a. Avviare hello [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).

    b. Fare clic su **Connectors**(Connettori).

    c. Seleziona hello **Active Directory Connector** utente hello in cui si trova.

    d. Selezionare **Search Connector Space**(Cerca spazio connettore).

    e. In hello **ambito** , quindi selezionare **DN o ancoraggio**, quindi immettere hello DN completo dell'utente hello risoluzione.

    ![Cercare l'utente nello spazio connettore con nome distinto](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    f. Individuare hello utente che si sta cercando, quindi fare clic su **proprietà** toosee tutti gli attributi di hello. Se è presente nei risultati di ricerca hello utente hello, verificare il [le regole di filtro](active-directory-aadconnectsync-configure-filtering.md) e accertarsi di eseguire [applica e verificare le modifiche](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) per tooappear utente hello nella connessione.

    g. Fare clic su dettagli di sincronizzazione password hello toosee dell'oggetto hello per hello settimana precedente, **Log**.  

    ![Dettagli del log dell'oggetto](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    Se il log di oggetto hello è vuoto, Azure AD Connect è stato Impossibile tooread hash della password hello da Active Directory. Continuare la risoluzione dei problemi con [Errori di connettività](#connectivity-errors). Se viene visualizzato un valore diverso da **successo**, fare riferimento a tabella toohello [log di sincronizzazione Password](#password-sync-log).

    h. Seleziona hello **derivazione** scheda e verificare che tale regola di almeno sincronizzazione hello **PasswordSync** colonna **True**. Nella configurazione predefinita di hello, hello regola di sincronizzazione hello è denominato **In ingresso da AD – User AccountEnabled**.  

    ![Informazioni sulla derivazione relative a un utente](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    i. Fare clic su **proprietà oggetto Metaverse** toodisplay un elenco di attributi utente.  

    ![Informazioni del metaverse](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    Verificare che non sia presente alcun attributo **cloudFiltered**. Assicurarsi che gli attributi di dominio di hello (domainFQDN e domainNetBios) hanno valori previsti hello.

    j. Fare clic su hello **connettori** scheda. Verificare che sia visualizzato tooboth connettori Active Directory locale e Azure AD.

    ![Informazioni del metaverse](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    k. Riga selezionare hello che rappresenta AD Azure, fare clic su **proprietà**, quindi fare clic su hello **derivazione** oggetto spazio connettore hello di scheda deve disporre di una regola in uscita in hello **PasswordSync** set di colonne troppo**True**. Nella configurazione predefinita di hello, hello regola di sincronizzazione hello è denominato **Out tooAAD - aggiunta utente**.  

    ![Finestra di dialogo Proprietà dell'oggetto spazio connettore](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a>Log di sincronizzazione delle password
Nella colonna Stato Hello può avere hello seguenti valori:

| Stato | Descrizione |
| --- | --- |
| Success |La password è stata sincronizzata. |
| FilteredByTarget |La password è troppo**cambiamento obbligatorio password all'accesso successivo**. La password non è stata sincronizzata. |
| NoTargetConnection |Nessun oggetto nel metaverse hello o nello spazio connettore hello Azure AD. |
| SourceConnectorNotPresent |Nessun oggetto trovato nello spazio connettore Active Directory locale di hello. |
| TargetNotExportedToDirectory |oggetto Hello in hello spazio connettore Azure AD non è ancora stato esportato. |
| MigratedCheckDetailsForMoreInfo |La voce di log è stata creata prima della compilazione 1.0.9125.0 e viene visualizzata nello stato precedente. |
| Errore |Il servizio ha restituito un errore sconosciuto. |
| Sconosciuto |Si è verificato un errore durante il tentativo di tooprocess un batch degli hash delle password.  |
| MissingAttribute |Gli attributi specifici (ad esempio hash Kerberos) richiesti da Azure AD Domain Services non sono disponibili. |
| RetryRequestedByTarget |Gli attributi specifici (ad esempio hash Kerberos) richiesti da Azure AD Domain Services non erano disponibili in precedenza. Hash della password dell'utente un tentativo tooresynchronize hello viene eseguita. |

## <a name="scripts-toohelp-troubleshooting"></a>Risoluzione dei problemi degli script toohelp

### <a name="get-hello-status-of-password-sync-settings"></a>Ottenere lo stato di hello di impostazioni di sincronizzazione password
```
Import-Module ADSync
$connectors = Get-ADSyncConnector
$aadConnectors = $connectors | Where-Object {$_.SubType -eq "Windows Azure Active Directory (Microsoft)"}
$adConnectors = $connectors | Where-Object {$_.ConnectorTypeName -eq "AD"}
if ($aadConnectors -ne $null -and $adConnectors -ne $null)
{
    if ($aadConnectors.Count -eq 1)
    {
        $features = Get-ADSyncAADCompanyFeature -ConnectorName $aadConnectors[0].Name
        Write-Host
        Write-Host "Password sync feature enabled in your Azure AD directory: "  $features.PasswordHashSync
        foreach ($adConnector in $adConnectors)
        {
            Write-Host
            Write-Host "Password sync channel status BEGIN ------------------------------------------------------- "
            Write-Host
            Get-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector.Name
            Write-Host
            $pingEvents =
                Get-EventLog -LogName "Application" -Source "Directory Synchronization" -InstanceId 654  -After (Get-Date).AddHours(-3) |
                    Where-Object { $_.Message.ToUpperInvariant().Contains($adConnector.Identifier.ToString("D").ToUpperInvariant()) } |
                    Sort-Object { $_.Time } -Descending
            if ($pingEvents -ne $null)
            {
                Write-Host "Latest heart beat event (within last 3 hours). Time " $pingEvents[0].TimeWritten
            }
            else
            {
                Write-Warning "No ping event found within last 3 hours."
            }
            Write-Host
            Write-Host "Password sync channel status END ------------------------------------------------------- "
            Write-Host
        }
    }
    else
    {
        Write-Warning "More than one Azure AD Connectors found. Please update hello script toouse hello appropriate Connector."
    }
}
Write-Host
if ($aadConnectors -eq $null)
{
    Write-Warning "No Azure AD Connector was found."
}
if ($adConnectors -eq $null)
{
    Write-Warning "No AD DS Connector was found."
}
Write-Host
```

#### <a name="trigger-a-full-sync-of-all-passwords"></a>Attivare una sincronizzazione completa di tutte le password
> [!NOTE]
> Eseguire questo script una sola volta. Se è necessario toorun più di una volta, un altro elemento è il problema di hello. problema di hello tootroubleshoot, contattare il supporto tecnico Microsoft.

È possibile attivare una sincronizzazione completa di tutte le password utilizzando hello lo script seguente:

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"
$aadConnector = "<CASE SENSITIVE AAD CONNECTOR NAME>"
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true
```

## <a name="next-steps"></a>Passaggi successivi
* [Implementazione della sincronizzazione password con il servizio di sincronizzazione Azure AD Connect](active-directory-aadconnectsync-implement-password-synchronization.md)
* [Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione](active-directory-aadconnectsync-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
