---
title: aaaStarting un runbook in automazione di Azure | Documenti Microsoft
description: Riepiloga hello diversi metodi che possono essere utilizzati toostart un runbook in automazione di Azure e fornisce informazioni dettagliate sull'utilizzo di entrambi hello portale di Azure e Windows PowerShell.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 6ee756b4-9200-4eb2-9bda-ec156853803b
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: e44bce5b56b8e803f9247fbb4f3d4db7ab35c913
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="starting-a-runbook-in-azure-automation"></a>Avvio di un Runbook in Automazione di Azure
Hello nella tabella seguente consentono di determinare hello metodo toostart un runbook in automazione di Azure che è più adatto tooyour particolare scenario. In questo articolo include informazioni dettagliate su come avviare un runbook con hello portale di Azure e con Windows PowerShell. Dettagli su hello altri metodi vengono forniti in altra documentazione di cui è possibile accedere dai collegamenti hello riportato di seguito.

| **METODO** | **CARATTERISTICHE** |
| --- | --- |
| [Portale di Azure](#starting-a-runbook-with-the-azure-portal) |<li>Metodo più semplice con interfaccia utente interattiva.<br> <li>I valori dei parametri semplice tooprovide del modulo.<br> <li>Facilità di controllo dello stato dei processi.<br> <li>Accesso autenticato con l'accesso di Azure. |
| [Windows PowerShell](https://msdn.microsoft.com/library/dn690259.aspx) |<li>Chiamata mediante cmdlet di Windows PowerShell nella riga di comandi.<br> <li>Possibilità di inclusione in una soluzione automatizzata con più passaggi.<br> <li>Autenticazione della richiesta con un certificato oppure con un'entità utente/entità servizio OAuth.<br> <li>Possibilità di specificare valori di parametri semplici e complessi.<br> <li>Possibilità di controllare lo stato dei processi.<br> <li>I cmdlet di PowerShell toosupport necessario client. |
| [API di Automazione di Azure](https://msdn.microsoft.com/library/azure/mt662285.aspx) |<li>Modalità più flessibile, ma anche più complessa.<br> <li>Possibilità di chiamata da qualsiasi codice personalizzato in grado di creare richieste HTTP.<br> <li>Autenticazione della richiesta con un certificato oppure con un'entità utente/entità servizio OAuth.<br> <li>Possibilità di specificare valori di parametri semplici e complessi.<br> <li>Possibilità di controllare lo stato dei processi. |
| [Webhook](automation-webhooks.md) |<li>Avvio di Runbook da una singola richiesta HTTP.<br> <li>Autenticazione con token di sicurezza nell'URL.<br> <li>Impossibilità per il client di eseguire l'override dei valori di parametri specificati al momento della creazione del webhook. Runbook può definire singolo parametro che viene popolata con i dettagli della richiesta HTTP hello.<br> <li>Stato del processo non tootrack possibilità tramite l'URL del webhook. |
| [Rispondere tooAzure avviso](../log-analytics/log-analytics-alerts.md) |<li>Avviare un runbook nell'avviso tooAzure di risposta.<br> <li>Configurare webhook per runbook e il collegamento tooalert.<br> <li>Autenticazione con token di sicurezza nell'URL. |
| [Pianificare](automation-schedules.md) |<li>Avvio automatico dei runbook in base a una pianificazione oraria, giornaliera, settimanale o mensile.<br> <li>Modifica della pianificazione tramite il portale di Azure, i cmdlet di PowerShell o l'API di Azure.<br> <li>Fornire toobe di valori di parametro utilizzato con una pianificazione. |
| [Da un altro Runbook](automation-child-runbooks.md) |<li>Uso di un Runbook come attività in un altro Runbook.<br> <li>Utile per funzionalità usate da più Runbook.<br> <li>Fornire runbook toochild valori di parametro e utilizzare l'output in runbook padre. |

Hello immagine seguente illustra procedura dettagliata hello ciclo di vita di un runbook. Offre diversi modi che viene avviato un runbook in automazione di Azure, i componenti necessari per i runbook di automazione di Azure di Runbook Worker ibrido tooexecute e le interazioni tra i diversi componenti. toolearn sull'esecuzione di runbook di automazione nel Data Center, fare riferimento troppo[ibridi per runbook](automation-hybrid-runbook-worker.md)

![Architettura dei runbook](media/automation-starting-runbook/runbooks-architecture.png)

## <a name="starting-a-runbook-with-hello-azure-portal"></a>Avvio di un runbook con hello portale di Azure
1. Nel portale di Azure hello, selezionare **automazione** e quindi scegliere il nome di hello di un account di automazione.
2. Nel menu Hub hello, selezionare **runbook**.
3. In hello **runbook** pannello selezionare un runbook e quindi fare clic su **avviare**.
4. Hello runbook include parametri, sarà richiesta tooprovide valori con una casella di testo per ogni parametro. Per altri dettagli sui parametri, vedere [Parametri di Runbook](#Runbook-parameters) più avanti.
5. In hello **processo** pannello, è possibile visualizzare lo stato di hello di processo del runbook hello.

## <a name="starting-a-runbook-with-windows-powershell"></a>Avvio di un Runbook con Windows PowerShell
È possibile utilizzare hello [inizio AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart un runbook con Windows PowerShell. Hello codice di esempio seguente avvia un runbook denominato Test-Runbook.

```
Start-AzureRmAutomationRunbook -AutomationAccountName "MyAutomationAccount" -Name "Test-Runbook" -ResourceGroupName "ResourceGroup01"
```

Inizio AzureRmAutomationRunbook restituisce un processo dell'oggetto che è possibile utilizzare tootrack lo stato dopo l'avvio del runbook hello. È quindi possibile utilizzare questo oggetto processo con [Get AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) stato hello toodetermine del processo di hello e [Get AzureRmAutomationJobOutput](https://msdn.microsoft.com/library/mt603476.aspx) tooget l'output. Hello codice di esempio seguente avvia un runbook denominato Test-Runbook, ne attende il completamento e quindi Visualizza il relativo output.

```
$runbookName = "Test-Runbook"
$ResourceGroup = "ResourceGroup01"
$AutomationAcct = "MyAutomationAccount"

$job = Start-AzureRmAutomationRunbook –AutomationAccountName $AutomationAcct -Name $runbookName -ResourceGroupName $ResourceGroup

$doLoop = $true
While ($doLoop) {
   $job = Get-AzureRmAutomationJob –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup
   $status = $job.Status
   $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped"))
}

Get-AzureRmAutomationJobOutput –AutomationAccountName $AutomationAcct -Id $job.JobId -ResourceGroupName $ResourceGroup –Stream Output
```

Se hello runbook richiede parametri, quindi sarà necessario fornirli come un [hashtable](http://technet.microsoft.com/library/hh847780.aspx) in chiave hello di hello hashtable corrisponde a nome di parametro hello e il valore di hello è il valore di parametro hello. Hello esempio seguente viene illustrato come toostart un runbook con due parametri stringa denominati FirstName e LastName, un numero intero denominato RepeatCount e un parametro booleano denominato Show. Per altre informazioni sui parametri, vedere [Parametri di Runbook](#Runbook-parameters) più avanti.

```
$params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook" -ResourceGroupName "ResourceGroup01" –Parameters $params
```

## <a name="runbook-parameters"></a>Parametri di Runbook
Quando si avvia un runbook da hello portale di Azure o Windows PowerShell, istruzione hello viene inviato tramite hello servizio web di automazione di Azure. Questo servizio non supporta i parametri con tipi di dati complessi. Se è necessario tooprovide un valore per un parametro complesso, è necessario chiamarlo inline da un altro runbook come descritto in [figlio runbook in automazione di Azure](automation-child-runbooks.md).

servizio web di automazione di Azure Hello fornirà funzionalità speciali per i parametri che usano determinati tipi di dati come descritto in hello le sezioni seguenti.

### <a name="named-values"></a>Valori denominati
Se il parametro hello è il tipo di dati [object], quindi è possibile utilizzare hello seguente toosend formato JSON è un elenco di valori denominati: *{nome1: 'Valore1', Nome2: 'Valore2', Nome3: 'Value3'}*. Questi valori devono essere tipi semplici. Hello runbook riceverà il parametro hello come un [PSCustomObject](https://msdn.microsoft.com/library/system.management.automation.pscustomobject%28v=vs.85%29.aspx) con proprietà corrispondenti tooeach denominato value.

Prendere in considerazione hello seguente runbook di test che accetta un parametro denominato utente.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][object]$user
   )
    $userObject = $user | ConvertFrom-JSON
    if ($userObject.Show) {
        foreach ($i in 1..$userObject.RepeatCount) {
            $userObject.FirstName
            $userObject.LastName
        }
    }
}
```

Hello testo seguente può essere utilizzato per il parametro utente hello.

```
{FirstName:'Joe',LastName:'Smith',RepeatCount:'2',Show:'True'}
```

Il risultato successivo output di hello.

```
Joe
Smith
Joe
Smith
```

### <a name="arrays"></a>Matrici
Se il parametro hello è una matrice, ad esempio [array] o [string []], è possibile utilizzare hello seguenti toosend formato JSON è un elenco di valori: *[valore1, valore2, valore3]*. Questi valori devono essere tipi semplici.

Prendere in considerazione hello seguente runbook di test che accetta un parametro denominato *utente*.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][array]$user
   )
    if ($user[3]) {
        foreach ($i in 1..$user[2]) {
            $ user[0]
            $ user[1]
        }
    }
}
```

Hello testo seguente può essere utilizzato per il parametro utente hello.

```
["Joe","Smith",2,true]
```

Il risultato successivo output di hello.

```
Joe
Smith
Joe
Smith
```

### <a name="credentials"></a>Credenziali
Se il parametro hello è di tipo di dati **PSCredential**, sarà possibile specificare il nome di hello di un'automazione di Azure [asset delle credenziali](automation-credentials.md). Hello runbook recupererà credenziale hello con nome hello specificato.

Prendere in considerazione hello seguente runbook di test che accetta un parametro denominato di credenziali.

```
Workflow Test-Parameters
{
   param (
      [Parameter(Mandatory=$true)][PSCredential]$credential
   )
   $credential.UserName
}
```

Hello seguente è possibile usare testo per il parametro utente hello supponendo che sia disponibile un asset credenziali denominato *My Credential*.

```
My Credential
```

Supponendo che sia nome utente hello nella credenziale hello *jsmith*, di conseguenza, dopo l'output di hello.

```
jsmith
```

## <a name="next-steps"></a>Passaggi successivi
* architettura di runbook Hello corrente dell'articolo fornisce una panoramica generale del runbook la gestione delle risorse in Azure e locali con hello Runbook Worker ibrido.  toolearn sull'esecuzione di runbook di automazione nel Data Center, fare riferimento troppo[Runbook worker ibridi](automation-hybrid-runbook-worker.md).
* toolearn ulteriori informazioni sulla creazione di runbook modulari toobe usata da altri runbook per le funzioni specifiche o comuni, hello vedere troppo[runbook figlio](automation-child-runbooks.md).

