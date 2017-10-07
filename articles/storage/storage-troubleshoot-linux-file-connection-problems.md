---
title: problemi di archiviazione di File di Azure aaaTroubleshoot in Linux | Documenti Microsoft
description: Risoluzione dei problemi di archiviazione file di Azure in Linux
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
ms.date: 07/11/2017
ms.author: genli
ms.openlocfilehash: 3dc537d714244451a5ff8e01f4a27f03873cf2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a>Risolvere i problemi di archiviazione file di Azure in Linux

Questo articolo vengono elencati i problemi comuni che sono correlati tooMicrosoft archiviazione di File di Azure per la connessione dal client Linux. L'articolo descrive anche le possibili cause e risoluzioni per tali problemi.

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-tooopen-a-file"></a>"quota [autorizzazione negata] del disco superata" quando si tenta di tooopen un file

In Linux, viene visualizzato un messaggio di errore simile al seguente hello:

**<filename> [accesso negato] Quota disco superata**

### <a name="cause"></a>Causa

È stato raggiunto limite massimo di hello di handle aperti simultanei consentite per un file.

### <a name="solution"></a>Soluzione

Ridurre il numero di hello di handle aperti simultanei chiudendo alcuni handle e quindi ripetere l'operazione di hello. Per altre informazioni, vedere [Elenco di controllo di prestazioni e scalabilità per Archiviazione di Microsoft Azure](storage-performance-checklist.md).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-linux"></a>File lenta copia tooand dall'archiviazione di File di Azure in Linux

-   Se non si dispone di un requisito delle dimensioni i/o minimo specifico, è consigliabile utilizzare 1 MB come hello dimensioni i/o per ottenere prestazioni ottimali.
-   Se si conosce hello dimensione finale di un file che si estende per l'utilizzo di scritture e del software non riscontrare problemi di compatibilità quando una coda non scritta nel file hello contiene zeri, quindi impostare la dimensione del file hello in anticipo anziché eseguire ogni operazione di scrittura di un'estensione scrittura.
-   Utilizzare il metodo di copia destra hello:
    -   Usare [AzCopy](storage-use-azcopy.md#file-copy) per i trasferimenti tra due condivisioni file.
    -   Usare [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) tra condivisioni file in un computer locale.

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a>"Errore di montaggio (112): Host inattivo" perché la riconnessione è scaduta

Quando il client di hello è rimasto inattivo per un lungo periodo, nel client Linux hello si verifica un errore di montaggio "112". Dopo il tempo di inattività esteso, timeout della connessione hello hello client si disconnette.  

### <a name="cause"></a>Causa

Hello connessione può rimanere inattiva per hello seguenti motivi:

-   Errori di comunicazione di rete che impediscono la ristabilire un server di toohello connessione TCP quando viene utilizzata l'opzione di montaggio "soft" hello predefinita
-   Correzioni di riconnessione recenti che non sono presenti in kernel precedenti

### <a name="solution"></a>Soluzione

Questo problema di riconnessione del kernel Linux hello è stato ora corretto come parte di hello seguenti modifiche:

- [Correzione di riconnettersi toonot rinviare smb3 sessione riconnettersi molto tempo dopo la riconnessione socket](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [Call echo service immediately after socket reconnect](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7) (Chiamare il servizio echo immediatamente dopo la riconnessione del socket)
-   [CIFS: Fix a possible memory corruption during reconnect](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b) (CIFS: correggere un possibile danneggiamento della memoria dopo la riconnessione)
-   [CIFS: Fix a possible double locking of mutex during reconnect - for kernels v4.9 and later](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183) (CIFS: Correggere un possibile doppio blocco del mutex durante la riconnessione, per i kernel 4.9 e versioni successive)

Tuttavia, queste modifiche potrebbero non essere trasferite ancora tooall hello distribuzioni di Linux. Sono state questa correzione e altre correzioni di riconnessione in seguito diffusi kernel Linux hello: 4.4.40 4.8.16 e 4.9.1. È possibile ottenere questa correzione aggiornando tooone di queste versioni del kernel consigliato.

### <a name="workaround"></a>Soluzione alternativa

È possibile ovviare a questo problema specificando un hard mount. In questo modo hello client toowait fino a quando non viene stabilita una connessione o fino a quando non viene interrotto in modo esplicito e può essere utilizzato tooprevent errori a causa di timeout di rete. Questa soluzione può tuttavia causare attese interminabili. Essere preparata toostop le connessioni in base alle esigenze.

Se non è possibile aggiornare versioni kernel più recenti toohello, è possibile utilizzare questo problema, mantenendo un file nella condivisione di file di Azure hello scrivere tooevery 30 secondi o meno. Deve trattarsi di un'operazione di scrittura, ad esempio la riscrittura hello creato o modificato data nel file hello. In caso contrario, si potrebbero ottenere risultati memorizzati nella cache e l'operazione potrebbe non generare riconnessione hello.

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a>"Errore di montaggio (115): L'operazione è in corso" quando si esegue il montaggio dell'archiviazione file di Azure usando SMB 3.0

### <a name="cause"></a>Causa

Alcune distribuzioni di Linux non supporta ancora le funzionalità di crittografia SMB 3.0 e gli utenti potrebbero ricevere un messaggio di errore "115" se tentano di archiviazione di File di Azure toomount tramite SMB 3.0 a causa di una caratteristica mancante.

### <a name="solution"></a>Soluzione

La funzionalità di crittografia per SMB 3.0 per Linux è stata introdotta nel kernel 4.11. Questa funzionalità consente di montare la condivisione file di Azure in locale o in un'altra area di Azure. In fase di hello della pubblicazione, questa funzionalità è stata backported tooUbuntu 17.04 e Ubuntu 16.10. Se il client SMB Linux non supporta la crittografia, montare l'archiviazione di File di Azure tramite SMB 2.1 da una macchina virtuale Linux di Azure in hello stesso Data Center come account di archiviazione di File hello.

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a>Rallentamento delle prestazioni in una condivisione file di Azure montata in una VM Linux

### <a name="cause"></a>Causa

Una possibile causa del rallentamento delle prestazioni è la disattivazione della memorizzazione nella cache.

### <a name="solution"></a>Soluzione

toocheck se la memorizzazione nella cache è disabilitata, cercare hello **cache =** voce. 

**cache=none** indica che la memorizzazione nella cache è disattivata.  Rimontaggio hello condivisione utilizzando il comando di montaggio predefinito di hello o aggiungendo in modo esplicito hello **cache = strict** è abilitata l'opzione toohello montaggio comando tooensure che utilizza l'impostazione predefinita in modalità di memorizzazione nella cache di memorizzazione nella cache o "strict".

In alcuni scenari, hello **serverino** opzione di montaggio può provocare hello **ls** stat toorun comando su ogni voce della directory. Questo comportamento determina un calo delle prestazioni quando si elenca una directory di grandi dimensioni. È possibile verificare le opzioni di montaggio hello nel **/e così via/fstab** voce:

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

È inoltre possibile verificare se le opzioni corrette hello in uso eseguendo hello **sudo montaggio | grep cifs** comando e archiviare l'output, ad esempio hello output di esempio riportato di seguito:

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

Se hello **cache = strict** o **serverino** opzione è non presentare, disinstallare e installare nuovamente la memorizzazione dei File di Azure eseguendo il comando di montaggio hello da hello [documentazione](storage-how-to-use-files-linux.md). Quindi, verificare di nuovo tale hello **/e così via/fstab** voce contiene opzioni corrette hello.

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-toolinux"></a>Timestamp sono andati persi nella copia dei file da Windows tooLinux

Sulle piattaforme Linux/Unix hello **cp -p** comando non riesce se il file di 1 e 2 file sono di proprietà da utenti diversi.

### <a name="cause"></a>Causa

Hello flag force **f** in COPYFILE comporta l'esecuzione di **cp -p -f** su Unix. Questo comando ha esito negativo anche timestamp hello toopreserve, del file hello che non si è proprietari.

### <a name="workaround"></a>Soluzione alternativa

Utilizzare account utente di hello archiviazione per la copia dei file hello:

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a>Richiesta di assistenza Contattare il supporto tecnico.

Se è ancora necessario della Guida, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema.
