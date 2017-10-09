---
title: problemi comuni di automazione di Azure aaaTroubleshooting | Documenti Microsoft
description: "Questo articolo fornisce informazioni toohelp identificare e risolvere gli errori più comuni di automazione di Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
tags: top-support-issue
keywords: errore di automazione, risoluzione dei problemi, problema
ms.assetid: 5f3cfe61-70b0-4e9c-b892-d02daaeee07d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: sngun; v-reagie
ms.openlocfilehash: eb7d1cc5726f2b7a86c860e8f0c8340fa4221b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-common-issues-in-azure-automation"></a>Risoluzione dei problemi comuni in Automazione di Azure 
Questo articolo vengono fornite indicazioni sulla risoluzione di errori comuni si possono verificarsi in automazione di Azure e vengono suggerite le possibili soluzioni tooresolve li.

## <a name="authentication-errors-when-working-with-azure-automation-runbooks"></a>Errori di autenticazione durante l'utilizzo di runbook di Automazione di Azure
### <a name="scenario-sign-in-tooazure-account-failed"></a>Scenario: Accesso tooAzure Account non è riuscita
**Errore:** errore hello "Unknown_user_type: utente tipo sconosciuto" quando si lavora con i cmdlet Add-AzureAccount o account di accesso AzureRmAccount hello.

**Motivo dell'errore hello:** questo errore si verifica se il nome dell'asset credenziali hello non è valido o se hello nome utente e password utilizzati asset credenziali di automazione hello toosetup non sono validi.

**Risoluzione dei problemi di suggerimenti:** In ordine toodetermine qual è il problema, richiedere hello alla procedura seguente:  

1. Assicurarsi che non si dispone di tutti i caratteri speciali, tra cui hello  **@**  carattere nel nome asset credenziali automazione hello che si sta utilizzando tooconnect tooAzure.  
2. Verificare che è possibile utilizzare hello username e password archiviati in credenziali di automazione di Azure hello nell'editor di PowerShell ISE locale. È possibile farlo eseguendo i seguenti cmdlet di PowerShell ISE hello hello:  

        $Cred = Get-Credential  
        #Using Azure Service Management   
        Add-AzureAccount –Credential $Cred  
        #Using Azure Resource Manager  
        Login-AzureRmAccount –Credential $Cred
3. Se l'autenticazione non riesce in locale, significa che le credenziali di Azure Active Directory non sono state configurate correttamente. Fare riferimento troppo[l'autenticazione tramite Azure Active Directory tooAzure](https://azure.microsoft.com/blog/azure-automation-authenticating-to-azure-using-azure-active-directory/) account blog post tooget hello Azure Active Directory configurato correttamente.  

### <a name="scenario-unable-toofind-hello-azure-subscription"></a>Scenario: Hello toofind non è possibile sottoscrizione di Azure
**Errore:** errore hello "hello sottoscrizione denominata ``<subscription name>`` non è stato trovato" quando si lavora con i cmdlet Select-AzureSubscription o selezionare AzureRmSubscription hello.

**Motivo dell'errore hello:** questo errore si verifica se il nome di sottoscrizione hello non è valido o se hello Azure Active Directory gli utenti i dettagli della sottoscrizione hello tooget sta cercando non sono configurato come un amministratore della sottoscrizione hello.

**Risoluzione dei problemi di suggerimenti:** In ordine toodetermine se si hanno eseguito correttamente l'autenticazione tooAzure e dispone di accesso toohello sottoscrizione che si sta tentando di tooselect, eseguire hello alla procedura seguente:  

1. Assicurarsi di eseguire hello **Add-AzureAccount** prima di eseguire hello **Select-AzureSubscription** cmdlet.  
2. Se viene ancora visualizzato questo messaggio di errore, modificare il codice aggiungendo hello **Get-AzureSubscription** cmdlet seguenti hello **Add-AzureAccount** cmdlet e quindi eseguire il codice hello.  A questo punto, verificare se l'output di hello di Get-AzureSubscription contiene i dettagli della sottoscrizione.  

   * Se tutti i dettagli della sottoscrizione nell'output di hello non viene visualizzato, significa che la sottoscrizione hello non è ancora inizializzata.  
   * Se è possibile visualizzare i dettagli della sottoscrizione hello nell'output di hello, confermare che si utilizza nome sottoscrizione corretta hello o un ID con hello **Select-AzureSubscription** cmdlet.   

### <a name="scenario-authentication-tooazure-failed-because-multi-factor-authentication-is-enabled"></a>Scenario: TooAzure di autenticazione non riuscita perché è abilitata l'autenticazione a più fattori
**Errore:** errore hello "Add-AzureAccount: AADSTS50079: registrazione di autenticazione avanzata (proof-alto) è necessario" per l'autenticazione tooAzure con il nome utente di Azure e la password.

**Motivo dell'errore hello:** se si dispone di multi-factor authentication nel proprio account Azure, è possibile utilizzare un tooAzure tooauthenticate utente di Azure Active Directory.  In alternativa, è necessario toouse un certificato o una tooAzure tooauthenticate dell'entità servizio.

**Risoluzione dei problemi di suggerimenti:** toouse un certificato con hello i cmdlet di gestione dei servizi Azure, vedere troppo[creando e aggiungendo un toomanage certificato Azure servizi.](http://blogs.technet.com/b/orchestrator/archive/2014/04/11/managing-azure-services-with-the-microsoft-azure-automation-preview-service.aspx) toouse un'entità servizio con i cmdlet di gestione risorse di Azure, fare riferimento troppo[creazione servizio principale tramite il portale di Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md) e [l'autenticazione di un'entità servizio con Azure Resource Manager.](../azure-resource-manager/resource-group-authenticate-service-principal.md)

## <a name="common-errors-when-working-with-runbooks"></a>Errori comuni durante l'utilizzo di runbook
### <a name="scenario-hello-runbook-job-start-was-attempted-three-times-but-it-failed-toostart-each-time"></a>Scenario: avvio del processo di runbook hello è stata tentata tre volte, ma non è riuscito toostart ogni ora
**Errore:** il runbook ha esito negativo con errore hello "" processo hello è tentato di tre volte, ma non è riuscito."

**Motivo dell'errore hello:** questo errore può dipendere da hello seguenti motivi:  

1. Limite di memoria.  È stato documentato limiti sulla quantità di memoria allocata tooa Sandbox [i limiti del servizio di automazione](../azure-subscription-service-limits.md#automation-limits) pertanto un processo potrebbe non riuscire, se si utilizza più di 400 MB di memoria. 

2. Modulo incompatibile.  Ciò può verificarsi se le dipendenze del modulo non sono corrette, e se non lo sono il runbook restituisce in genere il messaggio "Comando non trovato" o "Non è possibile associare il parametro". 

**Risoluzione dei problemi di suggerimenti:** una delle seguenti soluzioni hello risolverà il problema di hello:  

* Metodi consigliati toowork entro il limite di memoria hello sono il carico di lavoro di toosplit hello tra più runbook, non elaborare tutti i dati in memoria, toowrite output non necessari dal runbook o considerare quanti checkpoint scritto nel PowerShell runbook del flusso di lavoro.  

* È necessario tooupdate i moduli di Azure seguendo i passaggi di hello [come moduli di Azure PowerShell tooupdate in automazione di Azure](automation-update-azure-modules.md).  


### <a name="scenario-runbook-fails-because-of-deserialized-object"></a>Scenario: Runbook con esito negativo a causa di un oggetto deserializzato
**Errore:** il runbook ha esito negativo con errore hello "non è possibile associare il parametro ``<ParameterName>``. Non è possibile convertire hello ``<ParameterType>`` valore di tipo Deserialized ``<ParameterType>`` tootype ``<ParameterType>``".

**Motivo dell'errore hello:** se il runbook è un flusso di lavoro di PowerShell, archivia gli oggetti complessi in un formato deserializzato in ordine toopersist lo stato del runbook se il flusso di lavoro di hello è sospeso.  

**Suggerimenti per la risoluzione dei problemi:**  
Uno dei seguenti tre soluzioni hello risolverà il problema:

1. Se l'invio tramite pipe di oggetti complessi da un cmdlet tooanother, eseguire il wrapping di questi cmdlet in un InlineScript.  
2. Passare il nome di hello o un valore che è necessario dall'oggetto complesso di hello anziché passare l'intero oggetto hello.  
3. Usare un runbook di PowerShell invece di un runbook del flusso di lavoro PowerShell.  

### <a name="scenario-runbook-job-failed-because-hello-allocated-quota-exceeded"></a>Scenario: Il processo di Runbook non riuscito perché hello allocata quota superata
**Errore:** il processo del runbook ha esito negativo con errore hello "hello quota hello mensile totale per processi runtime è stato raggiunto per questa sottoscrizione".

**Motivo dell'errore hello:** questo errore si verifica quando hello l'esecuzione del processo supera la quota disponibile di hello 500 minuti per l'account. Questa quota si applica a tipi tooall esecuzione delle attività di processo, ad esempio un processo di test, avviare un processo dal portale di hello, l'esecuzione di un processo usando webhook e tooexecute un processo di pianificazione utilizzando entrambi hello portale di Azure o nel Data Center. informazioni sui prezzi per l'automazione, vedere toolearn [automazione prezzi](https://azure.microsoft.com/pricing/details/automation/).

**Risoluzione dei problemi di suggerimenti:** se si desidera toouse più di 500 minuti di elaborazione al mese, sarà necessario toochange la sottoscrizione dal livello Basic toohello livello gratuito di hello. È possibile aggiornare livello Basic toohello da hello richiede alla procedura seguente:  

1. Accedi tooyour sottoscrizione di Azure  
2. Selezionare l'account di automazione hello desiderato tooupgrade  
3. Fare clic su **Impostazioni** > **Piano tariffario e utilizzo** > **Piano tariffario**  
4. In hello **scegliere il piano tariffario** pannello seleziona **base**    

### <a name="scenario-cmdlet-not-recognized-when-executing-a-runbook"></a>Scenario: Cmdlet non riconosciuto durante l'esecuzione di un runbook
**Errore:** il processo del runbook ha esito negativo con errore hello "``<cmdlet name>``: termine hello ``<cmdlet name>`` non è riconosciuto come nome di un cmdlet, funzione, file di script, programma eseguibile o di hello."

**Motivo dell'errore hello:** questo errore si verifica quando il motore di PowerShell hello Impossibile trovare il cmdlet hello in uso nel runbook.  È possibile che il modulo di hello contenente hello cmdlet mancano dall'account hello, si verifica un conflitto di nome con un nome di runbook, o cmdlet hello è presente anche in un altro modulo e automazione non è possibile risolvere il nome di hello.

**Risoluzione dei problemi di suggerimenti:** una delle seguenti soluzioni hello risolverà il problema di hello:  

* Verificare di avere immesso il nome di cmdlet hello correttamente.  
* Assicurarsi che il cmdlet hello esista nell'account di automazione e che non sono presenti conflitti. tooverify se cmdlet hello è presente, aprire un runbook in modalità di modifica e ricerca per i cmdlet hello toofind nella libreria hello desiderato oppure eseguire **Get-Command ``<CommandName>``** .  Dopo aver verificato che cmdlet hello è account toohello disponibili, e che non sono presenti conflitti di nome con altri cmdlet o i runbook, aggiungerlo toohello area di disegno, assicurarsi che si sta utilizzando un parametro valido impostato nel runbook.  
* Se si dispone di un conflitto di nomi e i cmdlet di hello è disponibile in due moduli diversi, è possibile risolvere questo problema utilizzando hello il nome completo di cmdlet hello. Ad esempio, usare **ModuleName\CmdletName**.  
* Se si eseguono hello runbook locale in un gruppo di lavoro ibridi, assicurarsi che tale hello modulo/cmdlet viene installato nel computer di hello che ospita il ruolo di lavoro di hello ibrido.

### <a name="scenario-a-long-running-runbook-consistently-fails-with-hello-exception-hello-job-cannot-continue-running-because-it-was-repeatedly-evicted-from-hello-same-checkpoint"></a>Scenario: Un runbook con esecuzione prolungata non riesce con eccezione hello: "il processo di hello può continuare a eseguire perché è stato rimosso ripetutamente da hello stesso checkpoint".
**Motivo dell'errore hello:** questo è il comportamento di progettazione a causa di toohello "Condivisione equa" monitoraggio dei processi all'interno di automazione di Azure, che sospende automaticamente un runbook se viene eseguito più di 3 ore. Tuttavia, hello messaggio di errore restituito non fornisce "passaggi successivi" Opzioni. Un runbook può essere sospeso per una serie di motivi. Sospende verificarsi principalmente tooerrors scadenza. Ad esempio, un'eccezione non rilevata in un runbook, un errore di rete o un arresto anomalo in hello Runbook Worker in esecuzione il runbook hello, tutti causerà hello runbook toobe sospeso e avviare dall'ultimo checkpoint alla ripresa.

**Suggerimenti di risoluzione dei problemi:** hello documentato tooavoid soluzione questo problema è toouse checkpoint in un flusso di lavoro.  toolearn più fare riferimento troppo[flussi di lavoro PowerShell Learning](automation-powershell-workflow.md#checkpoints).  Una spiegazione più completa della "condivisione equa" e dei checkpoint è disponibile nell'articolo del blog dedicato all'[uso dei checkpoint nei runbook](https://azure.microsoft.com/en-us/blog/azure-automation-reliable-fault-tolerant-runbook-execution-using-checkpoints/).

## <a name="common-errors-when-importing-modules"></a>Errori comuni durante l'importazione di moduli
### <a name="scenario-module-fails-tooimport-or-cmdlets-cant-be-executed-after-importing"></a>Scenario: Modulo tooimport ha esito negativo o i cmdlet non possono essere eseguiti dopo l'importazione
**Errore:** un modulo ha esito negativo tooimport o importati correttamente, ma nessun cmdlet vengono estratti.

**Motivo dell'errore hello:** alcuni comuni motivi che un modulo potrà non importare tooAzure automazione sono:  

* struttura Hello corrisponde struttura hello che automazione ha bisogno toobe in.  
* modulo Hello è dipendente da un altro modulo che non è stato distribuito tooyour account di automazione.  
* modulo Hello mancante nella cartella hello relative dipendenze.  
* Hello **New AzureRmAutomationModule** cmdlet è in corso modulo hello tooupload utilizzato e non è stato assegnato il percorso di archiviazione completa hello o non sono caricati modulo hello tramite un URL accessibile pubblicamente.  

**Suggerimenti per la risoluzione dei problemi:**  
Una delle seguenti soluzioni hello risolverà il problema di hello:  

* Verificare che tale modulo hello segue hello seguente formato:  
  ModuleName.Zip **->** Nome modulo o numero versione **->** (ModuleName.psm1, ModuleName.psd1)
* Aprire il file con estensione psd1 hello e se il modulo hello dispone di tutte le dipendenze.  In caso affermativo, è possibile caricare queste toohello moduli account di automazione.  
* Assicurarsi che siano presenti nella cartella del modulo hello qualsiasi file con estensione DLL a cui fa riferimento.  

## <a name="common-errors-when-working-with-desired-state-configuration-dsc"></a>Errori comuni durante l'utilizzo di Desired State Configuration (DSC)
### <a name="scenario-node-is-in-failed-status-with-a-not-found-error"></a>Scenario: Lo stato di Node risulta non riuscito con un errore "Non trovato"
**Errore:** hello nodo dispone di un report con **Failed** lo stato e contenente l'errore hello "hello tentativo tooget hello azione dal server https://``<url>``//accounts/``<account-id>``/Nodes(AgentId=``<agent-id>``) / GetDscAction non è riuscita perché una configurazione valida ``<guid>`` non è stata trovata. "

**Motivo dell'errore hello:** questo errore si verifica in genere quando hello nodo viene assegnato il nome di configurazione tooa (ad esempio, ABC) anziché un nome di configurazione del nodo (ad esempio, ABC. Server Web).  

**Suggerimenti per la risoluzione dei problemi:**  

* Assicurarsi che si sta assegnando nodo hello non hello "nome di configurazione" e "Nome configurazione del nodo".  
* È possibile assegnare un nodo tooa di configurazione utilizzando portale di Azure o con un cmdlet di PowerShell.

  * In ordine tooassign un nodo tooa di configurazione tramite il portale di Azure, aprire hello **i nodi DSC** pannello, quindi selezionare un nodo e fare clic su **configurazione nodo assegnare** pulsante.  
  * In ordine tooassign un nodo tooa di configurazione utilizzando i cmdlet di PowerShell, usare **Set AzureRmAutomationDscNode** cmdlet

### <a name="scenario--no-node-configurations-mof-files-were-produced-when-a-configuration-is-compiled"></a>Scenario: non sono state prodotte configurazioni di nodo (file con estensione MOF) durante la compilazione di una configurazione
**Errore:** sospende il processo di compilazione DSC con errore hello: "compilazione completata, ma sono stati generati non MOF di configurazione del nodo".

**Motivo dell'errore hello:** hello quando l'espressione riportata di seguito hello **nodo** parola chiave nella configurazione DSC hello valuta troppo$ null, quindi non verranno prodotto alcun configurazioni del nodo.    

**Suggerimenti per la risoluzione dei problemi:**  
Una delle seguenti soluzioni hello risolverà il problema di hello:  

* Verificare che tale espressione di hello Avanti toohello **nodo** parola chiave nella definizione della configurazione hello non valuta troppo null$.  
* Se si passa ConfigurationData durante la compilazione di configurazione di hello, assicurarsi che si siano passando i valori previsti hello richiede che la configurazione di hello da [ConfigurationData](automation-dsc-compile.md#configurationdata).

### <a name="scenario--hello-dsc-node-report-becomes-stuck-in-progress-state"></a>Scenario: hello report nodi DSC rimane bloccato "in corso"
**Errore:** l'agente DSC restituisce un errore simile al seguente "Nessuna istanza trovata con i valori di proprietà specificati".

**Motivo dell'errore hello:** sono stati aggiornati alla versione WMF e hanno danneggiato WMI.  

**Risoluzione dei problemi di suggerimenti:** seguire le istruzioni hello hello [DSC problemi noti e limitazioni](https://msdn.microsoft.com/powershell/wmf/5.0/limitation_dsc) problema hello toofix.

### <a name="scenario--unable-toouse-a-credential-in-a-dsc-configuration"></a>Scenario: Impossibile toouse una credenziale in una configurazione DSC
**Errore:** il processo di compilazione DSC è stato sospeso con errore hello: "errore System. InvalidOperationException 'Credenziale' di tipo di proprietà di elaborazione ``<some resource name>``: la conversione e archiviazione di una password crittografata come testo normale è consentita solo se PSDscAllowPlainTextPassword è impostato tootrue".

**Motivo dell'errore hello:** è stata utilizzata una credenziale in una configurazione ma non forniva corretto **ConfigurationData** tooset **PSDscAllowPlainTextPassword** tootrue per ogni nodo configurazione.  

**Suggerimenti per la risoluzione dei problemi:**  

* Apportare toopass che hello corretto **ConfigurationData** tooset **PSDscAllowPlainTextPassword** tootrue per ogni configurazione del nodo indicato nella configurazione di hello. Per ulteriori informazioni, vedere troppo[asset di automazione di Azure DSC](automation-dsc-compile.md#assets).

## <a name="next-steps"></a>Passaggi successivi
Se si hanno seguito hello risoluzione dei problemi di passaggi precedenti e non è possibile trovare risposte hello, è possibile esaminare le opzioni di supporto aggiuntive hello seguenti.

* Ottenere assistenza dagli esperti di Azure. Inviare il problema toohello [forum MSDN di Azure o di Overflow dello Stack.](https://azure.microsoft.com/support/forums/).
* Archiviare un incidente del supporto tecnico di Azure. Passare toohello [sito del supporto di Azure](https://azure.microsoft.com/support/options/) e fare clic su **ottenere supporto** in **tecnici e il supporto di fatturazione**.
* Se si sta cercando una soluzione per i runbook oppure un modulo di integrazione di Automazione di Azure, inviare una richiesta di script a [Script Center](https://azure.microsoft.com/documentation/scripts/) .
* Inviare commenti o suggerimenti oppure richieste di funzionalità per Automazione di Azure al forum dedicato ai [suggerimenti degli utenti](https://feedback.azure.com/forums/34192--general-feedback).
