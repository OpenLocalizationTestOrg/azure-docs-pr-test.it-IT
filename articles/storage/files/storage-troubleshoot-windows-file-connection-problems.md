---
title: problemi di archiviazione di File di Azure aaaTroubleshoot Windows | Documenti Microsoft
description: Risoluzione dei problemi di archiviazione file di Azure in Windows
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: genli
ms.openlocfilehash: 19529d8af5d98790e2e381cd21ad4d0284acb124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a>Risolvere i problemi di archiviazione file di Azure in Windows

Questo articolo vengono elencati i problemi comuni che sono correlati tooMicrosoft archiviazione di File di Azure per la connessione dal client di Windows. L'articolo descrive anche le possibili cause e risoluzioni per tali problemi. Risoluzione dei problemi toohello inoltre i passaggi in questo articolo, è inoltre possibile utilizzare [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) per verificare che Windows hello ambiente client dispone di prerequisiti corretti. AzFileDiagnostics consente di automatizzare il rilevamento della maggior parte dei sintomi di hello indicati in questo articolo e consente di configurare le prestazioni ottimali tooget di ambiente. È inoltre possibile trovare queste informazioni in hello [le condivisioni file di Azure di risoluzione dei problemi](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) che fornisce i passaggi tooassist si problemi le condivisioni file di connessione, mapping/montaggio Azure.


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a>Errore 53, Errore 67 o Errore 87 quando si prova a montare o smontare una condivisione file di Azure

Quando si tenta di toomount una condivisione di file locale o da un altro Data Center, è possibile ricevere hello gli errori seguenti:

- Errore di sistema 53. percorso di rete Hello non trovato.
- Errore di sistema 67. Impossibile trovare il nome di rete Hello.
- Errore di sistema 87. il parametro Hello è corretto.

### <a name="cause-1-unencrypted-communication-channel"></a>Causa 1: canale di comunicazione non crittografato

Per motivi di sicurezza, le connessioni tooAzure condivisioni di file bloccate se il canale di comunicazione hello non è crittografato e non viene effettuato il tentativo di connessione di hello da hello stesso Data Center in cui si trovano hello condivisioni di file di Azure. Crittografia del canale di comunicazione è disponibile solo se il client dell'utente hello del sistema operativo supporta la crittografia SMB.

Windows 8, Windows Server 2012 e le versioni successive di ciascuno dei due sistemi operativi negoziano richieste comprendenti SMB 3.0, che supporta la crittografia.

### <a name="solution-for-cause-1"></a>Soluzione per la causa 1

Connettersi da un client che esegue uno dei seguenti hello:

- Soddisfa i requisiti di hello di Windows 8 e Windows Server 2012 o versioni successive
- Si connette da una macchina virtuale in hello stesso Data Center come account di archiviazione di Azure che viene utilizzato per la condivisione di file di Azure hello hello

### <a name="cause-2-port-445-is-blocked"></a>Causa 2: la porta 445 è bloccata

Errore di sistema 53 o sistema 67 può verificarsi se la porta 445 le comunicazioni in uscita tooan Azure File archiviazione Data Center è bloccato. riepilogo di hello toosee di ISP che consente o impedisce l'accesso dalla porta 445, andare troppo[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).

toounderstand se questo è il motivo di hello dietro il messaggio "Errore di sistema 53" hello, è possibile utilizzare l'endpoint di TCP:445 Portqry tooquery hello. Se endpoint TCP:445 hello viene visualizzato come filtrati, la porta TCP hello viene bloccato. Di seguito è fornito un esempio di query:

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

Se la porta TCP 445 è bloccata da una regola di percorso di rete hello, si noterà hello seguente output:

  `TCP port 445 (microsoft-ds service): FILTERED`

Per ulteriori informazioni su come toouse Portqry, vedere [descrizione dell'utilità della riga di comando di hello Portqry.exe](https://support.microsoft.com/help/310099).

### <a name="solution-for-cause-2"></a>Soluzione per la causa 2

Utilizzare la porta di tooopen reparto IT in uscita 445 troppo[intervalli IP Azure](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="cause-3-ntlmv1-is-enabled"></a>Causa 3: è abilitata la comunicazione NTLMv1

Errore di sistema 53 o errore di sistema 87 può verificarsi se è attivata la comunicazione di NTLMv1 sul client hello. L'archiviazione file di Azure supporta solo l'autenticazione NTLMv2. Con la comunicazione NTLMv1 abilitata, il client è meno sicuro. Di conseguenza, la comunicazione viene bloccata per l'archiviazione file di Azure. 

toodetermine se questa è hello causa dell'errore hello, verificare che hello seguente sottochiave del Registro di sistema è impostato un valore tooa 3:

**HKLM\SYSTEM\CurrentControlSet\Control\Lsa &gt; LmCompatibilityLevel**

Per ulteriori informazioni, vedere hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) argomento su TechNet.

### <a name="solution-for-cause-3"></a>Soluzione per la causa 3

Ripristinare hello **LmCompatibilityLevel** valore toohello valore predefinito 3 in hello seguente sottochiave del Registro di sistema:

  **HKLM\SYSTEM\CurrentControlSet\Control\Lsa**

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-tooprocess-this-command-when-you-copy-tooan-azure-file-share"></a>Errore 1816 "non è sufficiente quota trova tooprocess disponibile il comando" quando si copia tooan condivisione di file di Azure

### <a name="cause"></a>Causa

Errore 1816 si verifica quando si raggiunge hello limite superiore di handle aperti simultanei consentite per un file nel computer di hello in cui è viene montata condivisione file hello.

### <a name="solution"></a>Soluzione

Ridurre il numero di hello di handle aperti simultanei chiudendo gli handle di alcuni e riprovare. Per altre informazioni, vedere [Elenco di controllo di prestazioni e scalabilità per Archiviazione di Microsoft Azure](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-windows"></a>File lenta copia tooand dall'archivio di File di Azure in Windows

Quando si tenta di tootransfer file toohello servizio File di Azure, è possibile visualizzare un rallentamento delle prestazioni.

- Se non si dispone di un requisito delle dimensioni i/o minimo specifico, è consigliabile utilizzare 1 MB come hello dimensioni i/o per ottenere prestazioni ottimali.
-   Se si conosce dimensioni finali del hello di un file che si estende con scrive e il software privo di problemi di compatibilità quando la coda non scritta nel file hello hello contiene zeri, quindi set hello dimensioni del file in anticipo anziché eseguire ogni operazione di scrittura di un'operazione di scrittura estensione.
-   Utilizzare il metodo di copia destra hello:
    -   Usare [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) per i trasferimenti tra due condivisioni file.
    -   Usare [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) tra condivisioni file in un computer locale.

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a>Considerazioni per Windows 8.1 o Windows Server 2012 R2

Per i client che eseguono Windows 8.1 o Windows Server 2012 R2, verificare che tale hello [KB3114025](https://support.microsoft.com/help/3114025) è installato l'hotfix. Questo hotfix migliora le prestazioni di hello di creare e chiudere gli handle.

È possibile eseguire i seguenti script toocheck se è stato installato l'hotfix hello hello:

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

Se è installato l'hotfix, hello output seguente viene visualizzato:

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> Da dicembre 2015 la hotfix KB3114025 è installata per impostazione predefinita nelle immagini di Windows Server 2012 R2 presenti in Azure Marketplace.

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a>Nessuna cartella con una lettera di unità in **Computer locale**

Se si esegue il mapping di una condivisione di file di Azure come amministratore tramite comando net use, condivisione hello viene visualizzato toobe mancante.

### <a name="cause"></a>Causa

Per impostazione predefinita, Esplora file di Windows non viene eseguito come amministratore. Se si esegue comando net use da un prompt dei comandi amministrativo, eseguire il mapping di unità di rete hello come amministratore. Poiché le unità mappate sono specifiche per l'utente, account utente di hello viene registrato non viene visualizzata hello unità se sono montati in un account utente diverso.

### <a name="solution"></a>Soluzione
Montaggio hello condivisione dalla riga di comando senza privilegi di amministratore. In alternativa, è possibile seguire [in questo argomento TechNet](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** il valore del Registro di sistema.

<a id="netuse"></a>
## <a name="net-use-command-fails-if-hello-storage-account-contains-a-forward-slash"></a>Comando NET use non riesce se l'account di archiviazione hello contiene un carattere barra rovesciata

### <a name="cause"></a>Causa

comando net use Hello interpreta una barra (/) come un'opzione della riga di comando. Se il nome dell'account utente deve iniziare con una barra, mapping delle unità hello ha esito negativo.

### <a name="solution"></a>Soluzione

È possibile utilizzare uno dei seguenti passaggi toowork problema hello hello:

- Eseguire il comando PowerShell seguente hello:

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  Da un file batch, è possibile eseguire il comando hello in questo modo:

  `Echo new-smbMapping ... | powershell -command –`

- Inserire virgolette doppie hello toowork chiave questo problema, a meno che non barra hello è hello primo carattere. Questo caso, utilizzare la modalità interattiva hello e immettere la password separatamente o rigenerare il tooget chiavi una chiave che non inizia con una barra rovesciata.

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a>L'applicazione o il servizio non può accedere a un'unità di archiviazione file di Azure montata

### <a name="cause"></a>Causa

Le unità vengono montate per utente. Se l'applicazione o il servizio è in esecuzione con un account utente diverso rispetto hello che hello unità montata, un'applicazione hello non visualizzeranno unità hello.

### <a name="solution"></a>Soluzione

Utilizzare una delle seguenti soluzioni hello:

-   Montare l'unità di hello da hello stesso account utente che contiene l'applicazione hello. Si può usare uno strumento come PsExec.
- Passare parametri hello utente nome e la password del comando net use hello Nome account di archiviazione hello e la chiave.

Dopo aver eseguito queste operazioni, è possibile ricevere hello seguente messaggio di errore quando si esegue comando net use per account del servizio di rete del sistema/hello: "1312 errore di sistema. Una sessione di accesso specificata non esiste. Potrebbe essere già stata terminata." In questo caso, verificare che nome utente passato toonet utilizzare hello include informazioni sul dominio (ad esempio: "[nome account di archiviazione]. file.core.windows .net").

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-tooa-destination-that-does-not-support-encryption"></a>Errore "Si copia una destinazione tooa di file che non supporta la crittografia"

Quando un file viene copiato attraverso la rete hello, è stato decrittografato nel computer di origine hello, trasmesso in testo non crittografato e crittografati nuovamente nella destinazione hello file hello. Tuttavia, si potrebbe vedere il seguente errore durante il tentativo toocopy un file crittografato hello: "Si sta copiando destinazione di tooa file hello che non supporta la crittografia".

### <a name="cause"></a>Causa
Questo problema può verificarsi se si usa EFS (Encrypting File System). I file crittografati con BitLocker possono essere copiato tooAzure archiviazione di File. Tuttavia, l'archiviazione file di Azure non supporta NTFS EFS.

### <a name="workaround"></a>Soluzione alternativa
un file in rete hello toocopy, è necessario prima decrittografarlo. Utilizzare uno dei seguenti metodi hello:

- Hello utilizzare **copiare /d** comando. Consente di crittografato hello file toobe salvato come file decrittografati destinazione hello.
- Impostare hello seguente chiave del Registro di sistema:
  - Percorso = HKLM\Software\Policies\Microsoft\Windows\System
  - Tipo valore = DWORD
  - Nome = CopyFileAllowDecryptedRemoteDestination
  - Valore = 1

Tenere presente tale chiave del Registro di sistema di hello impostazione influisce su tutte le operazioni di copia che vengono apportate toonetwork condivisioni.

## <a name="need-help-contact-support"></a>Richiesta di assistenza Contattare il supporto tecnico.
Se è ancora necessario della Guida, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema.
