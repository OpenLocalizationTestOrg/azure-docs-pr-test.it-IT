---
title: aaaCreate un modulo di integrazione di automazione di Azure | Documenti Microsoft
description: Esercitazione che illustra utilizzare hello di esempio, test e la creazione di moduli di integrazione in automazione di Azure.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 27798efb-08b9-45d9-9b41-5ad91a3df41e
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/13/2017
ms.author: magoedte
ms.openlocfilehash: d4064d8b106496f4dab442024131886c4affccab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-integration-modules"></a>Moduli di integrazione di Automazione di Azure
PowerShell è una tecnologia fondamentale di hello dietro l'automazione di Azure. Poiché automazione di Azure è basata su PowerShell, i moduli di PowerShell sono toohello chiave estendibilità di automazione di Azure. In questo articolo è guiderà specifiche hello dell'uso di automazione di Azure di moduli di PowerShell, cui tooas "Moduli di integrazione" e procedure consigliate per la creazione di propri toomake moduli di PowerShell che funzionano come moduli di integrazione all'interno di Automazione di Azure. 

## <a name="what-is-a-powershell-module"></a>Che cos'è un modulo di PowerShell
Un modulo di PowerShell è un gruppo di cmdlet di PowerShell come **Get-Date** o **Copy-Item**, che può essere utilizzato dalla console di PowerShell hello, script, flussi di lavoro, runbook e le risorse DSC PowerShell come WindowsFeature o File, che può essere utilizzato dalle configurazioni di PowerShell DSC. Le funzionalità di hello di PowerShell viene esposta tramite i cmdlet e le risorse DSC e tutte le risorse/DSC cmdlet sono supportata da un modulo di PowerShell, molti dei quali forniti con PowerShell. Ad esempio, hello **Get-Date** cmdlet fa parte del modulo di PowerShell Utility, hello e **Copy-Item** cmdlet fa parte del modulo PowerShell Microsoft hello e risorsa Package DSC Hello fa parte del modulo PSDesiredStateConfiguration PowerShell hello. Tutti questi moduli sono inclusi in PowerShell. Tuttavia, molti moduli di PowerShell non fanno parte di PowerShell e vengono invece distribuiti con i prodotti prima o di terze parti come System Center 2012 Configuration Manager o da una grande community PowerShell hello in luoghi come PowerShell Gallery.  i moduli di Hello sono utili perché rendono più semplice tramite la funzionalità incapsulata attività complesse.  Altre informazioni sui moduli di PowerShell sono disponibili in [MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx). 

## <a name="what-is-an-azure-automation-integration-module"></a>Che cos'è un modulo di integrazione di Automazione di Azure
Un modulo di integrazione è simile a un modulo di PowerShell. Il relativo semplicemente un modulo di PowerShell che contiene facoltativamente un file aggiuntivo - un file di metadati che specifica un toobe di tipo di connessione di automazione di Azure utilizzati con i cmdlet del modulo hello nei runbook. Facoltativo del file oppure No, questi moduli possono essere importati in automazione di Azure toomake dei cmdlet disponibili per utilizzano all'interno di runbook e le relative risorse DSC disponibili per l'utilizzo all'interno delle configurazioni DSC di PowerShell. Background hello, automazione di Azure archivia questi moduli e al processo del runbook e tempo di esecuzione processo di compilazione DSC, li carica in sandbox di automazione di Azure hello in cui vengono eseguiti i runbook e vengono compilate le configurazioni DSC.  Le risorse DSC nei moduli vengono inserite automaticamente anche nel server di pull DSC di automazione di hello, in modo che è possibile effettuare il pull da macchine tentando tooapply le configurazioni DSC.  

Forniti un numero di moduli di PowerShell di Azure predefinito hello in automazione di Azure per toouse è pertanto possibile iniziare subito l'automazione di gestione di Azure, ma è possibile importare i moduli di PowerShell per qualsiasi sistema, servizio o lo strumento desiderato toointegrate con. 

> [!NOTE]
> Alcuni moduli vengono forniti come "moduli globali" nel servizio di automazione hello. Questi moduli globali sono disponibili tooyou quando si crea un account di automazione, e viene aggiornato in alcuni casi che li automaticamente inserisce tooyour account di automazione. Se si vuole impedire toobe auto-aggiornato, è possibile importare sempre hello stesso modulo manualmente e che avrà la precedenza sulla versione del modulo globale hello del modulo forniti nel servizio hello. 

formato di Hello in cui importare un pacchetto di modulo di integrazione è un file compresso con hello stesso nome modulo hello e l'estensione. zip. Contiene il modulo di Windows PowerShell hello e qualsiasi file di supporto, tra cui un file manifesto (psd1) se nel modulo hello.

Se il modulo hello deve contenere un tipo di connessione di automazione di Azure, deve contenere anche un file con nome hello `<ModuleName>-Automation.json` che specifica le proprietà di tipo connessione hello. Questo è un file json inserito in una cartella del file zip del modulo hello e contiene i campi di hello di "connessione" che è necessario tooconnect toohello sistema o modulo hello servizio rappresenta. In questo modo viene creato un tipo di connessione in Automazione di Azure. Uso di questo file è possibile impostare i nomi dei campi hello, tipi, e se i campi di hello devono essere crittografati e / o facoltativi, per il tipo di connessione hello del modulo hello. di seguito Hello è un modello in formato json hello:

```
{ 
   "ConnectionFields": [
   {
      "IsEncrypted":  false,
      "IsOptional":  false,
      "Name":  "ComputerName",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  false,
      "IsOptional":  true,
      "Name":  "Username",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  true,
      "IsOptional":  false,
      "Name":  "Password",
   "TypeName":  "System.String"
   }],
   "ConnectionTypeName":  "DataProtectionManager",
   "IntegrationModuleName":  "DataProtectionManager"
}
```

Se è stato distribuito Service Management Automation e creare pacchetti di moduli di integrazione per i runbook di automazione, dovrebbe essere tooyou molto familiare. 

## <a name="authoring-best-practices"></a>Procedure consigliate per la creazione
Anche se i moduli di integrazione sono essenzialmente i moduli di PowerShell, sia ancora disponibile una serie di operazioni, è consigliabile durante la creazione di un modulo di PowerShell, toomake è più utilizzabile in automazione di Azure. Alcune di queste sono automazione di Azure specifico e alcuni di essi sono utili toomake solo i moduli funzionano correttamente in flusso di lavoro PowerShell, indipendentemente dal fatto se si utilizza l'automazione. 

1. Include un riepilogo, descrizione e l'URI della Guida per ogni cmdlet nel modulo hello. In PowerShell, è possibile definire alcune informazioni della Guida per la Guida dei cmdlet tooallow hello utente tooreceive per utilizzarli con hello **Get-Help** cmdlet. Di seguito, ad esempio, è illustrato come definire un riepilogo e un URI della Guida per un modulo di PowerShell scritto in un file con estensione psm1.<br>  
   
    ```
    <#
        .SYNOPSIS
         Gets all outgoing phone numbers for this Twilio account 
    #>
    function Get-TwilioPhoneNumbers {
    [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
    HelpUri='http://www.twilio.com/docs/api/rest/outgoing-caller-ids')]
    param(
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AccountSid,
   
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AuthToken,
   
       [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [Hashtable]
       $Connection
    )
   
    $cred = CreateTwilioCredential -Connection $Connection -AccountSid $AccountSid -AuthToken $AuthToken
   
    $uri = "$TWILIO_BASE_URL/Accounts/" + $cred.UserName + "/IncomingPhoneNumbers"
   
    $response = Invoke-RestMethod -Method Get -Uri $uri -Credential $cred
   
    $response.TwilioResponse.IncomingPhoneNumbers.IncomingPhoneNumber
    }
    ```
   <br> Fornire queste informazioni non visualizzerà soltanto i questa Guida utilizzando hello **Get-Help** hello di cmdlet nella console di PowerShell, perché verrà inoltre esporre questa funzionalità della Guida di automazione di Azure.  ad esempio quando si inseriscono attività durante la creazione di runbook. Fare clic su "Visualizza Guida dettagliata" verrà URI della Guida hello aperto in un'altra scheda di hello web browser in uso tooaccess automazione di Azure.<br>![Guida dei moduli di integrazione](media/automation-integration-modules/automation-integration-module-activitydesc.png)
2. Se il modulo hello viene eseguito in un sistema remoto,

    a. Deve contenere un file di metadati di modulo di integrazione che definisce hello informazioni necessarie tooconnect toothat sistema remoto, ovvero il tipo di connessione hello.  
    b. Ogni cmdlet nel modulo hello deve essere in grado di tootake in un oggetto di connessione (un'istanza di quel tipo di connessione) come parametro.  

    I cmdlet nel modulo hello diventano più facile toouse in automazione di Azure se si consente di passare un oggetto con i campi di hello hello del tipo di connessione come parametro toohello cmdlet. Questo consente agli utenti non dispone di parametri di toomap dei parametri corrispondenti del cmdlet di hello connessione asset toohello ogni volta che si chiama un cmdlet. In base a hello runbook di esempio precedente, utilizza un asset di connessione di Twilio denominato CorpTwilio tooaccess Twilio e restituire tutti i numeri di telefono hello in account hello.  Si noti la modalità è mapping dei campi di hello hello parametri di connessione toohello del cmdlet hello?<br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    Tooapproach un modo più semplice e più direttamente questo sta passando hello connessione oggetto toohello cmdlet-
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    È possibile abilitare il comportamento simile al seguente per i cmdlet, consentendo loro tooaccept un oggetto di connessione direttamente come parametro, anziché solo i campi di connessione per i parametri. In genere è opportuno un set di parametri per ognuno, in modo che un utente non utilizzando l'automazione di Azure è possibile chiamare il cmdlet senza creare una tabella hash tooact come oggetto di connessione hello. Set di parametri **SpecifyConnectionFields** di seguito è toopass usate le proprietà di campo connessione hello uno alla volta. **UseConnectionObject** consente di passare hello direttamente tramite connessione. Come si può notare, hello trasmissione TwilioSMS cmdlet in hello [modulo PowerShell di Twilio](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) consente di passare in entrambi i casi: 
   
    ```
    function Send-TwilioSMS {
      [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
      HelpUri='http://www.twilio.com/docs/api/rest/sending-sms')]
      param(
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AccountSid,
   
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AuthToken,
   
         [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [Hashtable]
         $Connection
   
       )
    }
    ```
   <br>
3. Definire il tipo di output per tutti i cmdlet nel modulo hello. Per un cmdlet consente di IntelliSense in fase di progettazione si definisce un tipo di output è determinare hello toohelp restituire proprietà del cmdlet hello, per l'utilizzo durante la creazione. È particolarmente utile durante l'automazione runbook grafici per la modifica, in cui knowledge fase di progettazione è l'esperienza utente semplice tooan chiave con il modulo.<br><br> ![Tipo di output di runbook grafici](media/automation-integration-modules/runbook-graphical-module-output-type.png)<br> Questa operazione è simile toohello "con tipo" funzionalità di un cmdlet di output in PowerShell ISE senza toorun.<br><br> ![PowerShell e IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)<br>
4. I cmdlet nel modulo hello è possibile utilizzare i tipi di oggetto complesso per i parametri. Flusso di lavoro PowerShell si differenzia da PowerShell perché archivia i tipi complessi in formato deserializzato. Tipi primitivi verranno mantenuta come primitivi, ma i tipi complessi sono versioni tootheir convertito deserializzato, che sono essenzialmente elenchi di proprietà. Ad esempio, se è stato utilizzato hello **Get-Process** cmdlet in un runbook, o un flusso di lavoro di PowerShell per questo scopo, potrebbe restituire un oggetto di tipo [Deserialized.System.Diagnostic.Process], non hello [previsto Tipo Diagnostic]. Questo tipo dispone di tutte hello stesse proprietà come hello non deserializzato tipo, ma nessuno dei metodi di hello. Se si tenta toopass questo valore come parametro tooa cmdlet, i cmdlet di hello in cui è previsto un valore di [Diagnostic] per questo parametro, viene visualizzato il seguente errore hello: *non è in grado di elaborare trasformazione argomento sul parametro 'process' . Errore: "non è possibile convertire il valore di"Diagnostics (CcmExec)"hello di tipo"Deserialized.System.Diagnostics.Process"tootype"Diagnostics".*   In questo modo è che un tipo non corrispondente tra hello previsto tipo [Diagnostic] e [Deserialized.System.Diagnostic.Process] tipo specificato di hello. Hello questo problema consiste tooensure hello cmdlet del modulo non accettano i tipi complessi per i parametri. Ecco toodo modo errato hello è.
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    Di seguito è hello destro, in una primitiva che può essere usata internamente dal cmdlet hello toograb hello oggetto complesso e utilizzarlo. Poiché i cmdlet eseguiti nel contesto di hello di PowerShell, non flusso di lavoro PowerShell, all'interno di cmdlet hello $process diventa hello corretto [Diagnostic] tipo.  
   
    ```
    function Get-ProcessDescription {
      param (
            [String] $processName
      )
      $process = Get-Process -Name $processName
   
      $process.Description
    }
    ```
   <br>
   Gli asset di connessione nel runbook sono tabelle hash, che sono un tipo complesso, e ancora queste tabelle hash sembra toobe in grado di toobe passato nel cmdlet per loro – parametro di connessione, perfettamente con alcuna eccezione di cast. Tecnicamente, alcuni tipi di PowerShell sono in grado di toocast correttamente dal modulo tootheir deserializzato formato serializzato e pertanto possono essere passati in cmdlet per i parametri che accetta il tipo non è stato deserializzato hello. La tabella hash è uno di questi tipi. È possibile che toobe di tipi definiti dell'autore del modulo implementata in modo che correttamente può deserializzare nonché, ma esistono alcune tooconsider compromessi. Hello toohave esigenze di tipo un costruttore predefinito, dispone di tutte le proprietà pubblici e avere un PSTypeConverter. Tuttavia, per i tipi già definiti dall'autore del modulo che hello non proprietari, è non troppo "correggerli", pertanto hello tipi complessi di raccomandazione tooavoid per i parametri tutti insieme. Creazione di runbook Suggerimento: se per qualche motivo il cmdlet necessario tootake un complesso il parametro di tipo, o se si utilizza un altro modulo che richiede un parametro di tipo complesso, con la soluzione alternativa hello nei runbook del flusso di lavoro di PowerShell e flussi di lavoro di PowerShell in locale PowerShell, è toowrap hello cmdlet che genera l'errore di tipo complesso hello e cmdlet hello che utilizza il tipo complesso di hello in hello stessa attività InlineScript. Poiché InlineScript viene eseguito il relativo contenuto come PowerShell anziché flusso di lavoro PowerShell, cmdlet hello la generazione di tipo complesso hello produrrebbe tale tipo corretto, non hello deserializzata il tipo complesso.
5. Verificare tutti i cmdlet nel modulo hello senza stato. Flusso di lavoro PowerShell viene eseguito ogni cmdlet denominato nel flusso di lavoro hello in un'altra sessione. Ciò significa che i cmdlet che variano a seconda dello stato della sessione creato / modificato da altri cmdlet di hello stesso modulo non funzionerà nei runbook del flusso di lavoro di PowerShell.  Di seguito è riportato un esempio di ciò che non toodo.
   
    ```
    $globalNum = 0
    function Set-GlobalNum {
       param(
           [int] $num
       )
   
       $globalNum = $num
    }
    function Get-GlobalNumTimesTwo {
       $output = $globalNum * 2
   
       $output
    }
    ```
   <br>
6. modulo Hello deve essere completamente contenuto in un pacchetto in grado di Xcopy. Poiché i moduli di automazione di Azure sono distribuite toohello automazione sandbox quando runbook necessario tooexecute, è necessario che toowork indipendentemente dall'host hello in che vengono eseguiti. Ciò significa che è necessario essere in grado di tooZip pacchetto modulo hello, spostarlo tooany altri host con hello uguale o più recente versione di PowerShell e fare in modo funzionano normalmente durante l'importazione in ambiente di PowerShell di tale host. Affinché tale toohappen, hello modulo deve non dipendono da tutti i file all'esterno di hello modulo (cartella hello che ottiene compressi quando si importano in automazione di Azure) o in una sola impostazione del Registro di sistema univoco in un host, ad esempio quelle impostate hello installare di un prodotto. Se non è seguita questa procedura consigliata, modulo hello non sarà utilizzabile in automazione di Azure.  

## <a name="next-steps"></a>Passaggi successivi

* tooget avviato con runbook del flusso di lavoro di PowerShell, vedere [il primo runbook del flusso di lavoro di PowerShell](automation-first-runbook-textual.md)
* toolearn informazioni sulla creazione di moduli di PowerShell, vedere [la scrittura di un modulo Windows PowerShell](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)

