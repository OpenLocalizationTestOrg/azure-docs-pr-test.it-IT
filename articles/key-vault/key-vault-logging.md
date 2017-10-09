---
title: Registrazione dell'insieme di credenziali chiave aaaAzure | Documenti Microsoft
description: Utilizzare questa esercitazione toohelp iniziare a usare Azure insieme di credenziali chiave di registrazione.
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 43f96a2b-3af8-4adc-9344-bc6041fface8
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 38a173297948748bef45e3d857c06b50b3e21e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-logging"></a>Registrazione dell'insieme di credenziali delle chiavi di Azure
L'insieme di credenziali delle chiavi di Azure è disponibile nella maggior parte delle aree. Per ulteriori informazioni, vedere hello [insieme di credenziali chiave pagina dei prezzi](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Introduzione
Dopo aver creato uno o più insiemi di credenziali chiave, probabilmente si desidererà toomonitor come e quando la chiave di insiemi di credenziali vengono usati e da chi. A questo scopo è possibile abilitare la registrazione per l'insieme di credenziali delle chiavi, che salva le informazioni in un account di archiviazione di Azure specificato. Per tale account di archiviazione viene creato automaticamente un contenitore denominato **insights-log-auditevent** , che può essere usato per raccogliere i log relativi a più insiemi di credenziali delle chiavi.

È possibile accedere al massimo le informazioni di registrazione, 10 minuto dopo chiave hello insieme di credenziali di operazione. ma nella maggior parte dei casi si potrà farlo prima.  È attivo tooyou toomanage i log nell'account di archiviazione:

* Utilizzare toosecure metodi di controllo di accesso di Azure standard dei registri da limitare chi può accedervi.
* Eliminare i log che non si desidera più tookeep nell'account di archiviazione.

Utilizzare questa esercitazione toohelp iniziare a usare Azure insieme di credenziali chiave di registrazione, toocreate l'account di archiviazione, abilitare la registrazione e interpretare le informazioni di registrazione hello raccolti.  

> [!NOTE]
> In questa esercitazione sono incluse istruzioni per la modalità toocreate chiave gli insiemi di credenziali, chiavi o i segreti. Per altre informazioni, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure](key-vault-get-started.md). In alternativa, per le istruzioni relative all'interfaccia della riga di comando multipiattaforma, vedere [questa esercitazione equivalente](key-vault-manage-with-cli2.md).
>
> Attualmente, non è possibile configurare l'insieme di credenziali chiave di Azure nel portale di Azure hello. Usare invece queste istruzioni per Azure PowerShell.
>
>

Per informazioni generali sull'insieme di credenziali di Azure, vedere [Cos'è l'insieme di credenziali chiave di Azure?](key-vault-whatis.md)

## <a name="prerequisites"></a>Prerequisiti
toocomplete questa esercitazione, è necessario disporre di hello seguenti:

* Insieme di credenziali delle chiavi esistente e già in uso.  
* Azure PowerShell **versione minima 1.0.1**. tooinstall Azure PowerShell e associarlo a una sottoscrizione di Azure, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview). Se già stato installato Azure PowerShell e non conosce la versione di hello, dalla console di hello Azure PowerShell, digitare `(Get-Module azure -ListAvailable).Version`.  
* Spazio di archiviazione sufficiente in Azure per i log dell'insieme di credenziali delle chiavi.

## <a id="connect"></a>Connettersi tooyour sottoscrizioni
Avviare una sessione di Azure PowerShell e accedere con il comando seguente hello tooyour account Azure:  

    Login-AzureRmAccount

Nella finestra popup del browser hello, immettere il nome utente dell'account Azure e la password. Azure PowerShell recupera tutte le sottoscrizioni di hello che sono associate a questo account e per impostazione predefinita, utilizza hello prima.

Se si dispone di più sottoscrizioni, potrebbe essere toospecify uno specifico a cui è stato utilizzato toocreate l'insieme di credenziali chiave di Azure. Digitare hello sottoscrizioni hello toosee per l'account di seguito:

    Get-AzureRmSubscription

Quindi, toospecify hello sottoscrizione associato a credenziali delle chiavi che effettuerà l'accesso, tipo:

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> Si tratta di un passaggio importante e risulta particolarmente utile se si hanno più sottoscrizioni associate all'account. Si potrebbe ricevere un tooregister errore Insights se questo passaggio viene ignorato.
>   
>

Per ulteriori informazioni sulla configurazione di Azure PowerShell, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

## <a id="storage"></a>Creare un nuovo account di archiviazione per i log
Sebbene sia possibile utilizzare un account di archiviazione esistente per i log, si creerà un nuovo account di archiviazione che saranno i log dell'insieme di credenziali tooKey dedicato. Per praticità per quando è necessario toospecify questo è in un secondo momento, sarà archiviare dettagli hello in una variabile denominata **sa**.

Per ulteriori facilità di gestione, verrà utilizzata anche hello stesso gruppo di risorse come hello uno che contiene la chiave dell'insieme di credenziali. Da hello [esercitazione introduttiva](key-vault-get-started.md), questo gruppo di risorse denominato **ContosoResourceGroup** e continueremo percorso di toouse hello Asia orientale. Sostituire questi valori con i propri, a seconda dei casi:

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> Se si decide di toouse un account di archiviazione esistente, è necessario utilizzare hello stessa sottoscrizione, come necessario usare l'insieme di credenziali chiave e il modello di distribuzione di gestione risorse di hello, anziché come modello di distribuzione classica hello.
>
>

## <a id="identify"></a>Identificare hello chiave dell'insieme di credenziali per i log
L'esercitazione introduttiva, è il nome della chiave dell'insieme di credenziali **ContosoKeyVault**, pertanto continueremo toouse che denominare e salvare i dettagli di hello in una variabile denominata **kv**:

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <a id="enable"></a>Abilitare la registrazione
tooenable per l'insieme di credenziali chiave di registrazione, verrà usato il cmdlet Set-AzureRmDiagnosticSetting hello, insieme alle variabili hello creato per il nuovo account di archiviazione e la chiave dell'insieme di credenziali. Verranno inoltre stabilite hello **-abilitato** flag troppo**$true** e impostare hello categoria tooAuditEvent (hello solo categoria per la registrazione insieme credenziali chiavi):

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

output di Hello per questo oggetto include:

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


Questo conferma che è ora abilitata per l'insieme di credenziali chiave, il salvataggio di account di archiviazione di informazioni tooyour.

Facoltativamente è possibile impostare criteri di conservazione per i log, in modo che i log meno recenti vengano eliminati automaticamente. Ad esempio, impostare criteri di conservazione mediante **- RetentionEnabled** flag troppo**$true** e impostare **- RetentionInDays** parametro troppo**90** in modo che verranno eliminati automaticamente i log antecedenti a 90 giorni.

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

Informazioni registrate:

* Vengono registrate tutte le richieste API REST autenticate, incluse le richieste non riuscite a causa di autorizzazioni di accesso, errori di sistema o richieste non valide.
* Aggiornamento degli attributi di chiave dell'insieme di credenziali, ad esempio tag e operazioni chiave hello stesso, che include la creazione, eliminazione, impostazione di criteri di accesso dell'insieme di credenziali chiave, dell'insieme di credenziali.
* Operazioni sulle chiavi e segreti nell'hello insieme di credenziali, che include la creazione, modifica o eliminazione di queste chiavi o i segreti; operazioni quali l'accesso, verificare, crittografare, decrittografare, eseguire il wrapping e annullare il wrapping di chiavi, ottenere i segreti, le chiavi di elenco e i segreti e le relative versioni.
* Richieste non autenticate che generano una risposta 401. Ad esempio, richieste che non hanno un token di connessione, hanno un formato non valido, sono scadute o hanno un token non valido.  

## <a id="access"></a>Accedere ai log
Insieme di credenziali chiave log vengono archiviati in hello **insights-log-auditevent** contenitore nell'account di archiviazione hello fornito. toolist tutti i BLOB hello in questo contenitore, digitare:

Innanzitutto, creare una variabile per il nome di contenitore hello. Verrà utilizzato in tutto il resto di hello di hello procedura dettagliata.

    $container = 'insights-logs-auditevent'

toolist tutti i BLOB hello in questo contenitore, digitare:

    Get-AzureStorageBlob -Container $container -Context $sa.Context
output di Hello avrà un aspetto simile toothis:

**Uri contenitore: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**

**Nome**

- - -
**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****

Come si può notare da questo output, BLOB hello seguire una convenzione di denominazione: **resourceId =<ARM resource ID>/y =<year>/m =<month>/d =<day of month>/h =<hour>/m =<minute>/filename.json**

i valori di data e ora Hello usare UTC.

Poiché hello stesso account di archiviazione possono essere utilizzati toocollect registri per più risorse, hello ID completo della risorsa nome di blob hello è molto utile tooaccess o BLOB hello solo download necessari. Ma prima che, prima ci occuperemo come toodownload tutti hello BLOB.

Creare innanzitutto un hello toodownload cartella BLOB. ad esempio:

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

Ottenere quindi un elenco di tutti i BLOB:  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

Inviare tramite pipe questo elenco tramite i BLOB hello toodownload 'Get-AzureStorageBlobContent' la cartella di destinazione:

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

Quando si esegue il secondo comando, hello  **/**  delimitatore nei nomi di blob hello creerà una struttura di cartella completo nella cartella di destinazione hello, che questa struttura utilizzati toodownload e archivio hello BLOB come file.

tooselectively scaricare BLOB, utilizzare i caratteri jolly. ad esempio:

* Se si dispone di più insiemi di credenziali chiave, registri toodownload per un unico insieme di credenziali chiave denominata CONTOSOKEYVAULT3:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* Se si dispone di più gruppi di risorse e si desidera registri toodownload per un solo gruppo di risorse, utilizzare `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* Se si desidera toodownload tutti i log di hello per mese hello di gennaio 2016, utilizzare `-Blob '*/year=2016/m=01/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

Si è ora pronto toostart esaminando novità in hello Registra. Ma prima di procedere al che due ulteriori parametri per Get-AzureRmDiagnosticSetting che potrebbe essere necessario tooknow:

* stato di hello tooquery delle impostazioni di diagnostica per la risorsa dell'insieme di credenziali chiave:`Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`
* registrazione toodisable per la risorsa dell'insieme di credenziali chiave:`Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`

## <a id="interpret"></a>Interpretare i log dell'insieme di credenziali delle chiavi
I singoli BLOB vengono archiviati come testo, formattati come BLOB JSON. Questo è un esempio di voce di log generata dall'esecuzione di `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:

    {
        "records":
        [
            {
                "time": "2016-01-05T01:32:01.2691226Z",
                "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
                "operationName": "VaultGet",
                "operationVersion": "2015-06-01",
                "category": "AuditEvent",
                "resultType": "Success",
                "resultSignature": "OK",
                "resultDescription": "",
                "durationMs": "78",
                "callerIpAddress": "104.40.82.76",
                "correlationId": "",
                "identity": {"claim":{"http://schemas.microsoft.com/identity/claims/objectidentifier":"d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn":"live.com#username@outlook.com","appid":"1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},
                "properties": {"clientInfo":"azure-resource-manager/2.0","requestUri":"https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id":"https://contosokeyvault.vault.azure.net/","httpStatusCode":200}
            }
        ]
    }


Hello nella tabella seguente elenca le descrizioni e i nomi dei campi di hello.

| Nome campo | Descrizione |
| --- | --- |
| time |Data e ora (in formato UTC). |
| resourceId |ID della risorsa Gestione risorse di Azure. Per i registri di insieme di credenziali chiave, questa è sempre ID risorsa dell'insieme di credenziali chiave di hello. |
| operationName |Nome dell'operazione di hello, come illustrato nella seguente tabella hello. |
| operationVersion |Si tratta di versione dell'API REST hello richiesto da client hello. |
| category |Per i registri di insieme di credenziali chiave, AuditEvent è hello singolo disponibili valore. |
| resultType |Risultato della richiesta API REST. |
| resultSignature |Stato HTTP. |
| resultDescription |Descrizione aggiuntiva sul risultato di hello, se disponibile. |
| durationMs |Tempo impiegato richiesta dell'API REST hello tooservice, in millisecondi. Questo non include la latenza di rete hello, pertanto ora hello che è misurare sul lato client hello potrebbe non corrispondere a questo momento. |
| callerIpAddress |Indirizzo IP del client hello che ha effettuato la richiesta hello. |
| correlationId |Un GUID facoltativo che hello client può passare toocorrelate log lato client con i registri dal lato del servizio (insieme di credenziali chiave). |
| identity |Identità da token hello presentato nella richiesta di API REST hello. In genere si tratta di un "utente", una "entità servizio" o una combinazione "utente+appId" come nel caso di una richiesta generata da un cmdlet di Azure PowerShell. |
| properties |Questo campo conterrà informazioni diverse in base a operazione hello (operationName). Nella maggior parte dei casi, contiene informazioni sul client (hello useragent string passati dal client hello), hello esatta URI della richiesta API REST e codice di stato HTTP. Inoltre, quando un oggetto viene restituito come risultato di una richiesta (ad esempio, KeyCreate o VaultGet) anche conterrà hello URI con chiave (come "id"), l'URI dell'insieme di credenziali o URI segreto. |

Hello **operationName** i valori dei campi sono in formato ObjectVerb. ad esempio:

* Tutte le operazioni dell'insieme di credenziali chiave hanno hello ' insieme di credenziali`<action>`' formato, ad esempio `VaultGet` e `VaultCreate`.
* Tutte le operazioni chiave hanno hello ' chiave`<action>`' formato, ad esempio `KeySign` e `KeyList`.
* Tutte le operazioni secret hanno hello ' segreto`<action>`' formato, ad esempio `SecretGet` e `SecretListVersions`.

Hello nella tabella seguente sono elencati operationName hello e comando di API REST corrispondente.

| operationName | Comando API REST |
| --- | --- |
| Authentication |Tramite l'endpoint di Azure Active Directory |
| VaultGet |[Ottenere informazioni su un insieme di credenziali delle chiavi](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| VaultPut |[Creare o aggiornare un insieme di credenziali delle chiavi](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| VaultDelete |[Eliminare un insieme di credenziali delle chiavi](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| VaultPatch |[Aggiornare un insieme di credenziali delle chiavi](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| VaultList |[Elencare tutti gli insiemi di credenziali delle chiavi in un gruppo di risorse](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| KeyCreate |[Creare una chiave](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| KeyGet |[Ottenere informazioni su una chiave](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| KeyImport |[Importare una chiave in un insieme di credenziali](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| KeyBackup |[Eseguire il backup di una chiave](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx) |
| KeyDelete |[Eliminare una chiave](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| KeyRestore |[Ripristinare una chiave](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| KeySign |[Firmare con una chiave](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| KeyVerify |[Verificare con una chiave](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| KeyWrap |[Eseguire il wrapping di una chiave](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| KeyUnwrap |[Annullare il wrapping di una chiave](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| KeyEncrypt |[Crittografare con una chiave](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| KeyDecrypt |[Decrittografare con una chiave](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| KeyUpdate |[Aggiornare una chiave](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| KeyList |[Elenco di chiavi hello in un insieme di credenziali](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| KeyListVersions |[Elenco delle versioni di una chiave hello](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| SecretSet |[Creare un segreto](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| SecretGet |[Ottenere informazioni su un segreto](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| SecretUpdate |[Aggiornare un segreto](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| SecretDelete |[Eliminare un segreto](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| SecretList |[Elencare i segreti in un insieme di credenziali](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| SecretListVersions |[Elencare le versioni di un segreto](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <a id="loganalytics"></a>Usare Log Analytics

È possibile utilizzare soluzioni insieme credenziali chiavi Azure hello in tooreview Analitica Log che registra AuditEvent insieme di credenziali chiave di Azure. Per ulteriori informazioni, incluso come tooset, vedere [soluzione insieme credenziali chiavi Azure in Log Analitica](../log-analytics/log-analytics-azure-key-vault.md). In questo articolo contiene inoltre le istruzioni, se è necessario toomigrate dalla soluzione di insieme di credenziali chiave precedente hello che fosse disponibile durante l'anteprima di Log Analitica hello, in cui è indirizzato il tooan registri account di archiviazione di Azure e configurato per Log Analitica tooread da lì.

## <a id="next"></a>Passaggi successivi
Per un'esercitazione sull'uso dell'insieme di credenziali delle chiavi di Azure in un'applicazione Web, vedere [Usare l'insieme di credenziali delle chiavi di Azure da un'applicazione Web](key-vault-use-from-web-application.md).

Per i riferimenti di programmazione, vedere [hello Guida per gli sviluppatori insieme credenziali chiavi Azure](key-vault-developers-guide.md).

Per un elenco di cmdlet di Azure PowerShell 1.0 per l'insieme di credenziali delle chiavi di Azure, vedere [Cmdlet per l'insieme di credenziali delle chiavi di Azure](/powershell/module/azurerm.keyvault/#key_vault).

Per un'esercitazione sul rotazione della chiave e il controllo del registro insieme di credenziali chiave di Azure, vedere [come toosetup insieme di credenziali chiave con fine tooend chiave rotazione e il controllo](key-vault-key-rotation-log-monitoring.md).
