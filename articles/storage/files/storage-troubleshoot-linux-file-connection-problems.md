---
title: Risolvere i problemi di File di Azure in Linux | Microsoft Docs
description: Risoluzione dei problemi di File di Azure in Linux
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
ms.date: 09/19/2017
ms.author: genli
ms.openlocfilehash: 8fd09c748786f0bfe070c3f41201eddc3d272116
ms.sourcegitcommit: 310748b6d66dc0445e682c8c904ae4c71352fef2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2017
---
# <a name="troubleshoot-azure-files-problems-in-linux"></a>Risolvere i problemi di File di Azure in Linux

Questo articolo elenca i problemi comuni correlati a File di Microsoft Azure quando si effettua la connessione da client Linux. L'articolo descrive anche le possibili cause e risoluzioni per tali problemi.

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-to-open-a-file"></a>"[accesso negato] Quota disco superata" quando si tenta di aprire un file

In Linux si riceve un messaggio di errore simile al seguente:

**<filename> [accesso negato] Quota disco superata**

### <a name="cause"></a>Causa

È stato raggiunto il limite massimo di handle aperti simultaneamente consentito per un file.

### <a name="solution"></a>Soluzione

Ridurre il numero di handle aperti simultaneamente chiudendone alcuni e quindi riprovare. Per altre informazioni, vedere [Elenco di controllo di prestazioni e scalabilità per Archiviazione di Microsoft Azure](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-to-and-from-azure-files-in-linux"></a>Rallentamento della copia del file da e verso File di Azure in Linux

-   In assenza di un requisito minimo specifico per la dimensione di I/O, è consigliabile usare 1 MB per assicurare prestazioni ottimali.
-   Se si conosce la dimensione finale del file che si vuole estendere con operazioni di scrittura e il software non presenta problemi di compatibilità se la parte finale del file non ancora scritta contiene zeri, impostare la dimensione del file in fase preliminare anziché lasciare che ogni operazione di scrittura venga considerata un'estensione.
-   Usare il metodo di copia corretto:
    -   Usare [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) per i trasferimenti tra due condivisioni file.
    -   Usare [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) tra condivisioni file in un computer locale.

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a>"Errore di montaggio (112): Host inattivo" perché la riconnessione è scaduta

Un errore di montaggio "112" si verifica nel client Linux quando il client è stato inattivo per lungo tempo. Dopo un lungo tempo di inattività, il client si disconnette e la connessione scade.  

### <a name="cause"></a>Causa

La connessione può rimanere inattiva per i motivi seguenti:

-   Errori di comunicazione della rete che impediscono di ristabilire una connessione TCP al server quando viene usata l'opzione di montaggio predefinita "soft".
-   Correzioni di riconnessione recenti che non sono presenti in kernel precedenti

### <a name="solution"></a>Soluzione

Questo problema di riconnessione nel kernel Linux è stato corretto nell'ambito delle modifiche seguenti:

- [Fix reconnect to not defer smb3 session reconnect long after socket reconnect](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93) (Correggere la funzionalità di riconnessione in modo da non rinviare la riconnessione della sessione smb3 a molto tempo dopo la riconnessione del socket)
-   [Call echo service immediately after socket reconnect](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7) (Chiamare il servizio echo immediatamente dopo la riconnessione del socket)
-   [CIFS: Fix a possible memory corruption during reconnect](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b) (CIFS: correggere un possibile danneggiamento della memoria dopo la riconnessione)
-   [CIFS: Fix a possible double locking of mutex during reconnect - for kernels v4.9 and later](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183) (CIFS: Correggere un possibile doppio blocco del mutex durante la riconnessione, per i kernel 4.9 e versioni successive)

È tuttavia possibile che queste modifiche non siano state ancora trasferite a tutte le distribuzioni di Linux. Questa e altre correzioni di riconnessione sono state apportate nei kernel Linux di uso più comune seguenti: 4.4.40, 4.8.16 e 4.9.1. Per ottenere questa correzione, eseguire l'aggiornamento a una di queste versioni del kernel consigliate.

### <a name="workaround"></a>Soluzione alternativa

È possibile ovviare a questo problema specificando un hard mount. L'hard mount forza il client ad attendere fino a quando la connessione non viene stabilita o non viene interrotta in modo esplicito e può essere usato per evitare gli errori causati dai timeout di rete. Questa soluzione può tuttavia causare attese interminabili. Occorre quindi essere pronti a interrompere la connessione se necessario.

Se non è possibile eseguire l'aggiornamento alle versioni del kernel più recenti, si può ovviare a questo problema conservando un file nella condivisione file di Azure in cui scrivere ogni 30 secondi o meno. Deve trattarsi di un'operazione di scrittura, ad esempio la riscrittura della data di creazione o di modifica del file. In caso contrario, i risultati verrebbero memorizzati nella cache e l'operazione potrebbe non attivare la riconnessione.

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-files-by-using-smb-30"></a>"Errore di montaggio (115): L'operazione è in corso" quando si esegue il montaggio di File di Azure usando SMB 3.0

### <a name="cause"></a>Causa

Alcune distribuzioni Linux non supportano ancora le funzionalità di crittografia in SMB 3.0 e gli utenti potrebbero ricevere un messaggio di errore "115" se tentano di montare File di Azure usando SMB 3.0 poiché manca una funzionalità. SMB 3.0 con crittografia completa è attualmente supportato solo quando si usa Ubuntu 16.04 o versioni successive.

### <a name="solution"></a>Soluzione

La funzionalità di crittografia per SMB 3.0 per Linux è stata introdotta nel kernel 4.11. Questa funzionalità consente di montare la condivisione file di Azure in locale o in un'altra area di Azure. Al momento della pubblicazione, di questa funzionalità è stato eseguito il backport in Ubuntu 17.04 e Ubuntu 16.10. Se il client Linux SMB non supporta la crittografia, montare File di Azure usando SMB 2.1 da una macchina virtuale Linux di Azure presente nello stesso data center dell'account di archiviazione file.

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a>Rallentamento delle prestazioni in una condivisione file di Azure montata in una VM Linux

### <a name="cause"></a>Causa

Una possibile causa del rallentamento delle prestazioni è la disattivazione della memorizzazione nella cache.

### <a name="solution"></a>Soluzione

Per controllare se la memorizzazione nella cache è disattivata, cercare la voce **cache =**. 

**cache=none** indica che la memorizzazione nella cache è disattivata.  Eseguire nuovamente il montaggio della condivisione usando il comando di montaggio predefinito o aggiungendo esplicitamente l'opzione **cache=strict** al comando di montaggio per assicurarsi che la modalità di memorizzazione nella cache predefinita o "strict" sia attivata.

In alcuni scenari, l'opzione di montaggio **serverino** può far sì che il comando **ls** esegua stat rispetto a ogni voce di directory. Questo comportamento determina un calo delle prestazioni quando si elenca una directory di grandi dimensioni. È possibile controllare le opzioni di montaggio nella voce **/etc/fstab**:

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=2.1,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

È inoltre possibile controllare se vengono usate le opzioni corrette eseguendo il comando **sudo mount | grep cifs** e controllandone l'output, ad esempio l'output dell'esempio seguente:

`//azureuser.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=2.1,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

Se l'opzione **cache=strict** o **serverino** non è presente, smontare e montare nuovamente File di Azure eseguendo il comando di montaggio dalla [documentazione](../storage-how-to-use-files-linux.md). Verificare quindi di nuovo che la voce **/etc/fstab** disponga delle opzioni corrette.

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-to-linux"></a>I timestamp sono andati persi durante la copia dei file da Windows a Linux

Nelle piattaforme Linux/Unix il comando **cp -p** ha esito negativo se file 1 e file 2 sono di proprietà di utenti diversi.

### <a name="cause"></a>Causa

Il flag force **f** in COPYFILE determina l'esecuzione di **cp -p -f** in Unix. Questo comando non riesce anche a mantenere il timestamp del file di cui non si è proprietari.

### <a name="workaround"></a>Soluzione alternativa

Usare l'account utente di archiviazione per copiare i file:

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="cannot-connect-or-mount-an-azure-file-share"></a>Non è possibile connettere o montare una condivisione file di Azure

### <a name="cause"></a>Causa

Le cause comuni di questo problema sono le seguenti:


- Si sta usando un client di distribuzione Linux incompatibile. Si consiglia di usare le distribuzioni Linux seguenti per connettersi alla condivisione file di Azure:

    - Ubuntu Server 14.04+ 
    - RHEL 7+ 
    - CentOS 7+ 
    - Debian 8 
    - openSUSE 13.2+ 
    - SUSE Linux Enterprise Server 12

- Il pacchetto di strumenti CIFS-utils non è installato nel client.
- La versione SMB/CIFS minima 2.1 non è installata nel client.
- La crittografia SMB 3.0 non è supportata nel client. La crittografia SMB 3.0 è disponibile in Ubuntu 16.4 e versione successiva, SUSE 12.3 e versione successiva. Altre distribuzioni richiedono kernel 4.11 e versione successiva.
- Si sta tentando di connettersi a un account di archiviazione tramite la porta TCP 445, che non è supportata.
- Si sta tentando di connettersi alla condivisione file di Azure da una macchina virtuale di Azure e la macchina virtuale non si trova nella stessa area dell'account di archiviazione.

### <a name="solution"></a>Soluzione

Per risolvere il problema, usare lo [strumento di risoluzione dei problemi per gli errori di montaggio di File di Azure in Linux](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-02184089). Questo strumento consente di convalidare l'ambiente che esegue il client, di rilevare la configurazione client incompatibile che provocherebbe un errore di accesso per File di Azure, fornisce indicazioni sulla correzione autonoma da parte dell'utente e raccoglie le tracce di diagnostica.

## <a name="ls-cannot-access-ltpathgt-inputoutput-error"></a>ls: non è possibile accedere a '&lt;percorso&gt;': errore di input/output

Quando si prova a elencare i file in una condivisione file di Azure tramite il comando ls, questo si blocca durante la generazione dell'elenco e viene visualizzato l'errore seguente:

**ls: cannot access '&lt;percorso&gt;': Input/output error** (IS: non è possibile accedere a 'percorso': errore di input/output)


### <a name="solution"></a>Soluzione
Aggiornare il kernel di Linux a una delle versioni seguenti che prevedono una correzione per questo problema:

- 4.4.87+
- 4.9.48+
- 4.12.11+
- Tutte le versioni successive o corrispondenti alla 4.13

## <a name="need-help-contact-support"></a>Richiesta di assistenza Contattare il supporto tecnico.

Se si necessita ancora di assistenza, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) per ottenere una rapida risoluzione del problema.
