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
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a><span data-ttu-id="af484-103">Risolvere i problemi di archiviazione file di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="af484-103">Troubleshoot Azure File storage problems in Linux</span></span>

<span data-ttu-id="af484-104">Questo articolo vengono elencati i problemi comuni che sono correlati tooMicrosoft archiviazione di File di Azure per la connessione dal client Linux.</span><span class="sxs-lookup"><span data-stu-id="af484-104">This article lists common problems that are related tooMicrosoft Azure File storage when you connect from Linux clients.</span></span> <span data-ttu-id="af484-105">L'articolo descrive anche le possibili cause e risoluzioni per tali problemi.</span><span class="sxs-lookup"><span data-stu-id="af484-105">It also provides possible causes and resolutions for these problems.</span></span>

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-tooopen-a-file"></a><span data-ttu-id="af484-106">"quota [autorizzazione negata] del disco superata" quando si tenta di tooopen un file</span><span class="sxs-lookup"><span data-stu-id="af484-106">"[permission denied] Disk quota exceeded" when you try tooopen a file</span></span>

<span data-ttu-id="af484-107">In Linux, viene visualizzato un messaggio di errore simile al seguente hello:</span><span class="sxs-lookup"><span data-stu-id="af484-107">In Linux, you receive an error message that resembles hello following:</span></span>

<span data-ttu-id="af484-108">**<filename> [accesso negato] Quota disco superata**</span><span class="sxs-lookup"><span data-stu-id="af484-108">**<filename> [permission denied] Disk quota exceeded**</span></span>

### <a name="cause"></a><span data-ttu-id="af484-109">Causa</span><span class="sxs-lookup"><span data-stu-id="af484-109">Cause</span></span>

<span data-ttu-id="af484-110">È stato raggiunto limite massimo di hello di handle aperti simultanei consentite per un file.</span><span class="sxs-lookup"><span data-stu-id="af484-110">You have reached hello upper limit of concurrent open handles that are allowed for a file.</span></span>

### <a name="solution"></a><span data-ttu-id="af484-111">Soluzione</span><span class="sxs-lookup"><span data-stu-id="af484-111">Solution</span></span>

<span data-ttu-id="af484-112">Ridurre il numero di hello di handle aperti simultanei chiudendo alcuni handle e quindi ripetere l'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="af484-112">Reduce hello number of concurrent open handles by closing some handles, and then retry hello operation.</span></span> <span data-ttu-id="af484-113">Per altre informazioni, vedere [Elenco di controllo di prestazioni e scalabilità per Archiviazione di Microsoft Azure](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="af484-113">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-linux"></a><span data-ttu-id="af484-114">File lenta copia tooand dall'archiviazione di File di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="af484-114">Slow file copying tooand from Azure File storage in Linux</span></span>

-   <span data-ttu-id="af484-115">Se non si dispone di un requisito delle dimensioni i/o minimo specifico, è consigliabile utilizzare 1 MB come hello dimensioni i/o per ottenere prestazioni ottimali.</span><span class="sxs-lookup"><span data-stu-id="af484-115">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as hello I/O size for optimal performance.</span></span>
-   <span data-ttu-id="af484-116">Se si conosce hello dimensione finale di un file che si estende per l'utilizzo di scritture e del software non riscontrare problemi di compatibilità quando una coda non scritta nel file hello contiene zeri, quindi impostare la dimensione del file hello in anticipo anziché eseguire ogni operazione di scrittura di un'estensione scrittura.</span><span class="sxs-lookup"><span data-stu-id="af484-116">If you know hello final size of a file that you are extending by using writes, and your software doesn’t experience compatibility problems when an unwritten tail on hello file contains zeros, then set hello file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="af484-117">Utilizzare il metodo di copia destra hello:</span><span class="sxs-lookup"><span data-stu-id="af484-117">Use hello right copy method:</span></span>
    -   <span data-ttu-id="af484-118">Usare [AzCopy](storage-use-azcopy.md#file-copy) per i trasferimenti tra due condivisioni file.</span><span class="sxs-lookup"><span data-stu-id="af484-118">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="af484-119">Usare [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) tra condivisioni file in un computer locale.</span><span class="sxs-lookup"><span data-stu-id="af484-119">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a><span data-ttu-id="af484-120">"Errore di montaggio (112): Host inattivo" perché la riconnessione è scaduta</span><span class="sxs-lookup"><span data-stu-id="af484-120">"Mount error(112): Host is down" because of a reconnection time-out</span></span>

<span data-ttu-id="af484-121">Quando il client di hello è rimasto inattivo per un lungo periodo, nel client Linux hello si verifica un errore di montaggio "112".</span><span class="sxs-lookup"><span data-stu-id="af484-121">A "112" mount error occurs on hello Linux client when hello client has been idle for a long time.</span></span> <span data-ttu-id="af484-122">Dopo il tempo di inattività esteso, timeout della connessione hello hello client si disconnette.</span><span class="sxs-lookup"><span data-stu-id="af484-122">After extended idle time, hello client disconnects and hello connection times out.</span></span>  

### <a name="cause"></a><span data-ttu-id="af484-123">Causa</span><span class="sxs-lookup"><span data-stu-id="af484-123">Cause</span></span>

<span data-ttu-id="af484-124">Hello connessione può rimanere inattiva per hello seguenti motivi:</span><span class="sxs-lookup"><span data-stu-id="af484-124">hello connection can be idle for hello following reasons:</span></span>

-   <span data-ttu-id="af484-125">Errori di comunicazione di rete che impediscono la ristabilire un server di toohello connessione TCP quando viene utilizzata l'opzione di montaggio "soft" hello predefinita</span><span class="sxs-lookup"><span data-stu-id="af484-125">Network communication failures that prevent re-establishing a TCP connection toohello server when hello default “soft” mount option is used</span></span>
-   <span data-ttu-id="af484-126">Correzioni di riconnessione recenti che non sono presenti in kernel precedenti</span><span class="sxs-lookup"><span data-stu-id="af484-126">Recent reconnection fixes that are not present in older kernels</span></span>

### <a name="solution"></a><span data-ttu-id="af484-127">Soluzione</span><span class="sxs-lookup"><span data-stu-id="af484-127">Solution</span></span>

<span data-ttu-id="af484-128">Questo problema di riconnessione del kernel Linux hello è stato ora corretto come parte di hello seguenti modifiche:</span><span class="sxs-lookup"><span data-stu-id="af484-128">This reconnection problem in hello Linux kernel is now fixed as part of hello following changes:</span></span>

- [<span data-ttu-id="af484-129">Correzione di riconnettersi toonot rinviare smb3 sessione riconnettersi molto tempo dopo la riconnessione socket</span><span class="sxs-lookup"><span data-stu-id="af484-129">Fix reconnect toonot defer smb3 session reconnect long after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   <span data-ttu-id="af484-130">[Call echo service immediately after socket reconnect](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7) (Chiamare il servizio echo immediatamente dopo la riconnessione del socket)</span><span class="sxs-lookup"><span data-stu-id="af484-130">[Call echo service immediately after socket reconnect](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)</span></span>
-   <span data-ttu-id="af484-131">[CIFS: Fix a possible memory corruption during reconnect](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b) (CIFS: correggere un possibile danneggiamento della memoria dopo la riconnessione)</span><span class="sxs-lookup"><span data-stu-id="af484-131">[CIFS: Fix a possible memory corruption during reconnect](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)</span></span>
-   <span data-ttu-id="af484-132">[CIFS: Fix a possible double locking of mutex during reconnect - for kernels v4.9 and later](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183) (CIFS: Correggere un possibile doppio blocco del mutex durante la riconnessione, per i kernel 4.9 e versioni successive)</span><span class="sxs-lookup"><span data-stu-id="af484-132">[CIFS: Fix a possible double locking of mutex during reconnect (for kernel v4.9 and later)](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)</span></span>

<span data-ttu-id="af484-133">Tuttavia, queste modifiche potrebbero non essere trasferite ancora tooall hello distribuzioni di Linux.</span><span class="sxs-lookup"><span data-stu-id="af484-133">However, these changes might not be ported yet tooall hello Linux distributions.</span></span> <span data-ttu-id="af484-134">Sono state questa correzione e altre correzioni di riconnessione in seguito diffusi kernel Linux hello: 4.4.40 4.8.16 e 4.9.1.</span><span class="sxs-lookup"><span data-stu-id="af484-134">This fix and other reconnection fixes are made in hello following popular Linux kernels: 4.4.40, 4.8.16, and 4.9.1.</span></span> <span data-ttu-id="af484-135">È possibile ottenere questa correzione aggiornando tooone di queste versioni del kernel consigliato.</span><span class="sxs-lookup"><span data-stu-id="af484-135">You can get this fix by upgrading tooone of these recommended kernel versions.</span></span>

### <a name="workaround"></a><span data-ttu-id="af484-136">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="af484-136">Workaround</span></span>

<span data-ttu-id="af484-137">È possibile ovviare a questo problema specificando un hard mount.</span><span class="sxs-lookup"><span data-stu-id="af484-137">You can work around this problem by specifying a hard mount.</span></span> <span data-ttu-id="af484-138">In questo modo hello client toowait fino a quando non viene stabilita una connessione o fino a quando non viene interrotto in modo esplicito e può essere utilizzato tooprevent errori a causa di timeout di rete.</span><span class="sxs-lookup"><span data-stu-id="af484-138">This forces hello client toowait until a connection is established or until it’s explicitly interrupted and can be used tooprevent errors because of network time-outs.</span></span> <span data-ttu-id="af484-139">Questa soluzione può tuttavia causare attese interminabili.</span><span class="sxs-lookup"><span data-stu-id="af484-139">However, this workaround might cause indefinite waits.</span></span> <span data-ttu-id="af484-140">Essere preparata toostop le connessioni in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="af484-140">Be prepared toostop connections as necessary.</span></span>

<span data-ttu-id="af484-141">Se non è possibile aggiornare versioni kernel più recenti toohello, è possibile utilizzare questo problema, mantenendo un file nella condivisione di file di Azure hello scrivere tooevery 30 secondi o meno.</span><span class="sxs-lookup"><span data-stu-id="af484-141">If you cannot upgrade toohello latest kernel versions, you can work around this problem by keeping a file in hello Azure file share that you write tooevery 30 seconds or less.</span></span> <span data-ttu-id="af484-142">Deve trattarsi di un'operazione di scrittura, ad esempio la riscrittura hello creato o modificato data nel file hello.</span><span class="sxs-lookup"><span data-stu-id="af484-142">This must be a write operation, such as rewriting hello created or modified date on hello file.</span></span> <span data-ttu-id="af484-143">In caso contrario, si potrebbero ottenere risultati memorizzati nella cache e l'operazione potrebbe non generare riconnessione hello.</span><span class="sxs-lookup"><span data-stu-id="af484-143">Otherwise, you might get cached results, and your operation might not trigger hello reconnection.</span></span>

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a><span data-ttu-id="af484-144">"Errore di montaggio (115): L'operazione è in corso" quando si esegue il montaggio dell'archiviazione file di Azure usando SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="af484-144">"Mount error(115): Operation now in progress" when you mount Azure File storage by using SMB 3.0</span></span>

### <a name="cause"></a><span data-ttu-id="af484-145">Causa</span><span class="sxs-lookup"><span data-stu-id="af484-145">Cause</span></span>

<span data-ttu-id="af484-146">Alcune distribuzioni di Linux non supporta ancora le funzionalità di crittografia SMB 3.0 e gli utenti potrebbero ricevere un messaggio di errore "115" se tentano di archiviazione di File di Azure toomount tramite SMB 3.0 a causa di una caratteristica mancante.</span><span class="sxs-lookup"><span data-stu-id="af484-146">Some Linux distributions do not yet support encryption features in SMB 3.0 and users might receive a "115" error message if they try toomount Azure File storage by using SMB 3.0 because of a missing feature.</span></span>

### <a name="solution"></a><span data-ttu-id="af484-147">Soluzione</span><span class="sxs-lookup"><span data-stu-id="af484-147">Solution</span></span>

<span data-ttu-id="af484-148">La funzionalità di crittografia per SMB 3.0 per Linux è stata introdotta nel kernel 4.11.</span><span class="sxs-lookup"><span data-stu-id="af484-148">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="af484-149">Questa funzionalità consente di montare la condivisione file di Azure in locale o in un'altra area di Azure.</span><span class="sxs-lookup"><span data-stu-id="af484-149">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="af484-150">In fase di hello della pubblicazione, questa funzionalità è stata backported tooUbuntu 17.04 e Ubuntu 16.10.</span><span class="sxs-lookup"><span data-stu-id="af484-150">At hello time of publishing, this functionality has been backported tooUbuntu 17.04 and Ubuntu 16.10.</span></span> <span data-ttu-id="af484-151">Se il client SMB Linux non supporta la crittografia, montare l'archiviazione di File di Azure tramite SMB 2.1 da una macchina virtuale Linux di Azure in hello stesso Data Center come account di archiviazione di File hello.</span><span class="sxs-lookup"><span data-stu-id="af484-151">If your Linux SMB client does not support encryption, mount Azure File storage by using SMB 2.1 from an Azure Linux VM that's in hello same datacenter as hello File storage account.</span></span>

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a><span data-ttu-id="af484-152">Rallentamento delle prestazioni in una condivisione file di Azure montata in una VM Linux</span><span class="sxs-lookup"><span data-stu-id="af484-152">Slow performance on an Azure file share mounted on a Linux VM</span></span>

### <a name="cause"></a><span data-ttu-id="af484-153">Causa</span><span class="sxs-lookup"><span data-stu-id="af484-153">Cause</span></span>

<span data-ttu-id="af484-154">Una possibile causa del rallentamento delle prestazioni è la disattivazione della memorizzazione nella cache.</span><span class="sxs-lookup"><span data-stu-id="af484-154">One possible cause of slow performance is disabled caching.</span></span>

### <a name="solution"></a><span data-ttu-id="af484-155">Soluzione</span><span class="sxs-lookup"><span data-stu-id="af484-155">Solution</span></span>

<span data-ttu-id="af484-156">toocheck se la memorizzazione nella cache è disabilitata, cercare hello **cache =** voce.</span><span class="sxs-lookup"><span data-stu-id="af484-156">toocheck whether caching is disabled, look for hello **cache=** entry.</span></span> 

<span data-ttu-id="af484-157">**cache=none** indica che la memorizzazione nella cache è disattivata.</span><span class="sxs-lookup"><span data-stu-id="af484-157">**Cache=none** indicates that caching is disabled.</span></span>  <span data-ttu-id="af484-158">Rimontaggio hello condivisione utilizzando il comando di montaggio predefinito di hello o aggiungendo in modo esplicito hello **cache = strict** è abilitata l'opzione toohello montaggio comando tooensure che utilizza l'impostazione predefinita in modalità di memorizzazione nella cache di memorizzazione nella cache o "strict".</span><span class="sxs-lookup"><span data-stu-id="af484-158">Remount hello share by using hello default mount command or by explicitly adding hello **cache=strict** option toohello mount command tooensure that default caching or "strict" caching mode is enabled.</span></span>

<span data-ttu-id="af484-159">In alcuni scenari, hello **serverino** opzione di montaggio può provocare hello **ls** stat toorun comando su ogni voce della directory.</span><span class="sxs-lookup"><span data-stu-id="af484-159">In some scenarios, hello **serverino** mount option can cause hello **ls** command toorun stat against every directory entry.</span></span> <span data-ttu-id="af484-160">Questo comportamento determina un calo delle prestazioni quando si elenca una directory di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="af484-160">This behavior results in performance degradation when you're listing a big directory.</span></span> <span data-ttu-id="af484-161">È possibile verificare le opzioni di montaggio hello nel **/e così via/fstab** voce:</span><span class="sxs-lookup"><span data-stu-id="af484-161">You can check hello mount options in your **/etc/fstab** entry:</span></span>

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

<span data-ttu-id="af484-162">È inoltre possibile verificare se le opzioni corrette hello in uso eseguendo hello **sudo montaggio | grep cifs** comando e archiviare l'output, ad esempio hello output di esempio riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="af484-162">You can also check whether hello correct options are being used by running hello  **sudo mount | grep cifs** command and checking its output, such as hello following example output:</span></span>

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

<span data-ttu-id="af484-163">Se hello **cache = strict** o **serverino** opzione è non presentare, disinstallare e installare nuovamente la memorizzazione dei File di Azure eseguendo il comando di montaggio hello da hello [documentazione](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="af484-163">If hello **cache=strict** or **serverino** option is not present, unmount and mount Azure File storage again by running hello mount command from hello [documentation](storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="af484-164">Quindi, verificare di nuovo tale hello **/e così via/fstab** voce contiene opzioni corrette hello.</span><span class="sxs-lookup"><span data-stu-id="af484-164">Then, recheck that hello **/etc/fstab** entry has hello correct options.</span></span>

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-toolinux"></a><span data-ttu-id="af484-165">Timestamp sono andati persi nella copia dei file da Windows tooLinux</span><span class="sxs-lookup"><span data-stu-id="af484-165">Time stamps were lost in copying files from Windows tooLinux</span></span>

<span data-ttu-id="af484-166">Sulle piattaforme Linux/Unix hello **cp -p** comando non riesce se il file di 1 e 2 file sono di proprietà da utenti diversi.</span><span class="sxs-lookup"><span data-stu-id="af484-166">On Linux/Unix platforms, hello **cp -p** command fails if file 1 and file 2 are owned by different users.</span></span>

### <a name="cause"></a><span data-ttu-id="af484-167">Causa</span><span class="sxs-lookup"><span data-stu-id="af484-167">Cause</span></span>

<span data-ttu-id="af484-168">Hello flag force **f** in COPYFILE comporta l'esecuzione di **cp -p -f** su Unix.</span><span class="sxs-lookup"><span data-stu-id="af484-168">hello force flag **f** in COPYFILE results in executing **cp -p -f** on Unix.</span></span> <span data-ttu-id="af484-169">Questo comando ha esito negativo anche timestamp hello toopreserve, del file hello che non si è proprietari.</span><span class="sxs-lookup"><span data-stu-id="af484-169">This command also fails toopreserve hello time stamp of hello file that you don't own.</span></span>

### <a name="workaround"></a><span data-ttu-id="af484-170">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="af484-170">Workaround</span></span>

<span data-ttu-id="af484-171">Utilizzare account utente di hello archiviazione per la copia dei file hello:</span><span class="sxs-lookup"><span data-stu-id="af484-171">Use hello storage account user for copying hello files:</span></span>

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a><span data-ttu-id="af484-172">Richiesta di assistenza</span><span class="sxs-lookup"><span data-stu-id="af484-172">Need help?</span></span> <span data-ttu-id="af484-173">Contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="af484-173">Contact support.</span></span>

<span data-ttu-id="af484-174">Se è ancora necessario della Guida, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema.</span><span class="sxs-lookup"><span data-stu-id="af484-174">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your problem resolved quickly.</span></span>
