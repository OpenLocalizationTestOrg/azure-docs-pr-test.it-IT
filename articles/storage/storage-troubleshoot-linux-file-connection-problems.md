---
title: Risolvere i problemi di archiviazione file di Azure in Linux | Microsoft Docs
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
ms.openlocfilehash: 62cd62ec3a2900f06acacc0852a48b5e3ff1c8cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a><span data-ttu-id="b2b7e-103">Risolvere i problemi di archiviazione file di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="b2b7e-103">Troubleshoot Azure File storage problems in Linux</span></span>

<span data-ttu-id="b2b7e-104">Questo articolo elenca i problemi comuni correlati all'archiviazione file di Microsoft Azure quando si esegue la connessione da client Linux.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-104">This article lists common problems that are related to Microsoft Azure File storage when you connect from Linux clients.</span></span> <span data-ttu-id="b2b7e-105">L'articolo descrive anche le possibili cause e risoluzioni per tali problemi.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-105">It also provides possible causes and resolutions for these problems.</span></span>

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-to-open-a-file"></a><span data-ttu-id="b2b7e-106">"[accesso negato] Quota disco superata" quando si tenta di aprire un file</span><span class="sxs-lookup"><span data-stu-id="b2b7e-106">"[permission denied] Disk quota exceeded" when you try to open a file</span></span>

<span data-ttu-id="b2b7e-107">In Linux si riceve un messaggio di errore simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b2b7e-107">In Linux, you receive an error message that resembles the following:</span></span>

<span data-ttu-id="b2b7e-108">**<filename> [accesso negato] Quota disco superata**</span><span class="sxs-lookup"><span data-stu-id="b2b7e-108">**<filename> [permission denied] Disk quota exceeded**</span></span>

### <a name="cause"></a><span data-ttu-id="b2b7e-109">Causa</span><span class="sxs-lookup"><span data-stu-id="b2b7e-109">Cause</span></span>

<span data-ttu-id="b2b7e-110">È stato raggiunto il limite massimo di handle aperti simultaneamente consentito per un file.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-110">You have reached the upper limit of concurrent open handles that are allowed for a file.</span></span>

### <a name="solution"></a><span data-ttu-id="b2b7e-111">Soluzione</span><span class="sxs-lookup"><span data-stu-id="b2b7e-111">Solution</span></span>

<span data-ttu-id="b2b7e-112">Ridurre il numero di handle aperti simultaneamente chiudendone alcuni e quindi riprovare.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-112">Reduce the number of concurrent open handles by closing some handles, and then retry the operation.</span></span> <span data-ttu-id="b2b7e-113">Per altre informazioni, vedere [Elenco di controllo di prestazioni e scalabilità per Archiviazione di Microsoft Azure](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="b2b7e-113">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-to-and-from-azure-file-storage-in-linux"></a><span data-ttu-id="b2b7e-114">Rallentamento della copia del file da e verso l'archiviazione file di Azure in Linux</span><span class="sxs-lookup"><span data-stu-id="b2b7e-114">Slow file copying to and from Azure File storage in Linux</span></span>

-   <span data-ttu-id="b2b7e-115">In assenza di un requisito minimo specifico per la dimensione di I/O, è consigliabile usare 1 MB per assicurare prestazioni ottimali.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-115">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as the I/O size for optimal performance.</span></span>
-   <span data-ttu-id="b2b7e-116">Se si conosce la dimensione finale del file che si vuole estendere con operazioni di scrittura e il software non presenta problemi di compatibilità se la parte finale del file non ancora scritta contiene zeri, impostare la dimensione del file in fase preliminare anziché lasciare che ogni operazione di scrittura venga considerata un'estensione.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-116">If you know the final size of a file that you are extending by using writes, and your software doesn’t experience compatibility problems when an unwritten tail on the file contains zeros, then set the file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="b2b7e-117">Usare il metodo di copia corretto:</span><span class="sxs-lookup"><span data-stu-id="b2b7e-117">Use the right copy method:</span></span>
    -   <span data-ttu-id="b2b7e-118">Usare [AzCopy](storage-use-azcopy.md#file-copy) per i trasferimenti tra due condivisioni file.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-118">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="b2b7e-119">Usare [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) tra condivisioni file in un computer locale.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-119">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a><span data-ttu-id="b2b7e-120">"Errore di montaggio (112): Host inattivo" perché la riconnessione è scaduta</span><span class="sxs-lookup"><span data-stu-id="b2b7e-120">"Mount error(112): Host is down" because of a reconnection time-out</span></span>

<span data-ttu-id="b2b7e-121">Un errore di montaggio "112" si verifica nel client Linux quando il client è stato inattivo per lungo tempo.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-121">A "112" mount error occurs on the Linux client when the client has been idle for a long time.</span></span> <span data-ttu-id="b2b7e-122">Dopo un lungo tempo di inattività, il client si disconnette e la connessione scade.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-122">After extended idle time, the client disconnects and the connection times out.</span></span>  

### <a name="cause"></a><span data-ttu-id="b2b7e-123">Causa</span><span class="sxs-lookup"><span data-stu-id="b2b7e-123">Cause</span></span>

<span data-ttu-id="b2b7e-124">La connessione può rimanere inattiva per i motivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2b7e-124">The connection can be idle for the following reasons:</span></span>

-   <span data-ttu-id="b2b7e-125">Errori di comunicazione della rete che impediscono di ristabilire una connessione TCP al server quando viene usata l'opzione di montaggio predefinita "soft".</span><span class="sxs-lookup"><span data-stu-id="b2b7e-125">Network communication failures that prevent re-establishing a TCP connection to the server when the default “soft” mount option is used</span></span>
-   <span data-ttu-id="b2b7e-126">Correzioni di riconnessione recenti che non sono presenti in kernel precedenti</span><span class="sxs-lookup"><span data-stu-id="b2b7e-126">Recent reconnection fixes that are not present in older kernels</span></span>

### <a name="solution"></a><span data-ttu-id="b2b7e-127">Soluzione</span><span class="sxs-lookup"><span data-stu-id="b2b7e-127">Solution</span></span>

<span data-ttu-id="b2b7e-128">Questo problema di riconnessione nel kernel Linux è stato corretto nell'ambito delle modifiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2b7e-128">This reconnection problem in the Linux kernel is now fixed as part of the following changes:</span></span>

- <span data-ttu-id="b2b7e-129">[Fix reconnect to not defer smb3 session reconnect long after socket reconnect](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93) (Correggere la funzionalità di riconnessione in modo da non rinviare la riconnessione della sessione smb3 a molto tempo dopo la riconnessione del socket)</span><span class="sxs-lookup"><span data-stu-id="b2b7e-129">[Fix reconnect to not defer smb3 session reconnect long after socket reconnect](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)</span></span>
-   <span data-ttu-id="b2b7e-130">[Call echo service immediately after socket reconnect](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7) (Chiamare il servizio echo immediatamente dopo la riconnessione del socket)</span><span class="sxs-lookup"><span data-stu-id="b2b7e-130">[Call echo service immediately after socket reconnect](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)</span></span>
-   <span data-ttu-id="b2b7e-131">[CIFS: Fix a possible memory corruption during reconnect](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b) (CIFS: correggere un possibile danneggiamento della memoria dopo la riconnessione)</span><span class="sxs-lookup"><span data-stu-id="b2b7e-131">[CIFS: Fix a possible memory corruption during reconnect](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)</span></span>
-   <span data-ttu-id="b2b7e-132">[CIFS: Fix a possible double locking of mutex during reconnect - for kernels v4.9 and later](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183) (CIFS: Correggere un possibile doppio blocco del mutex durante la riconnessione, per i kernel 4.9 e versioni successive)</span><span class="sxs-lookup"><span data-stu-id="b2b7e-132">[CIFS: Fix a possible double locking of mutex during reconnect (for kernel v4.9 and later)](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)</span></span>

<span data-ttu-id="b2b7e-133">È tuttavia possibile che queste modifiche non siano state ancora trasferite a tutte le distribuzioni di Linux.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-133">However, these changes might not be ported yet to all the Linux distributions.</span></span> <span data-ttu-id="b2b7e-134">Questa e altre correzioni di riconnessione sono state apportate nei kernel Linux di uso più comune seguenti: 4.4.40, 4.8.16 e 4.9.1.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-134">This fix and other reconnection fixes are made in the following popular Linux kernels: 4.4.40, 4.8.16, and 4.9.1.</span></span> <span data-ttu-id="b2b7e-135">Per ottenere questa correzione, eseguire l'aggiornamento a una di queste versioni del kernel consigliate.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-135">You can get this fix by upgrading to one of these recommended kernel versions.</span></span>

### <a name="workaround"></a><span data-ttu-id="b2b7e-136">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="b2b7e-136">Workaround</span></span>

<span data-ttu-id="b2b7e-137">È possibile ovviare a questo problema specificando un hard mount.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-137">You can work around this problem by specifying a hard mount.</span></span> <span data-ttu-id="b2b7e-138">L'hard mount forza il client ad attendere fino a quando la connessione non viene stabilita o non viene interrotta in modo esplicito e può essere usato per evitare gli errori causati dai timeout di rete.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-138">This forces the client to wait until a connection is established or until it’s explicitly interrupted and can be used to prevent errors because of network time-outs.</span></span> <span data-ttu-id="b2b7e-139">Questa soluzione può tuttavia causare attese interminabili.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-139">However, this workaround might cause indefinite waits.</span></span> <span data-ttu-id="b2b7e-140">Occorre quindi essere pronti a interrompere la connessione se necessario.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-140">Be prepared to stop connections as necessary.</span></span>

<span data-ttu-id="b2b7e-141">Se non è possibile eseguire l'aggiornamento alle versioni del kernel più recenti, si può ovviare a questo problema conservando un file nella condivisione file di Azure in cui scrivere ogni 30 secondi o meno.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-141">If you cannot upgrade to the latest kernel versions, you can work around this problem by keeping a file in the Azure file share that you write to every 30 seconds or less.</span></span> <span data-ttu-id="b2b7e-142">Deve trattarsi di un'operazione di scrittura, ad esempio la riscrittura della data di creazione o di modifica del file.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-142">This must be a write operation, such as rewriting the created or modified date on the file.</span></span> <span data-ttu-id="b2b7e-143">In caso contrario, i risultati verrebbero memorizzati nella cache e l'operazione potrebbe non attivare la riconnessione.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-143">Otherwise, you might get cached results, and your operation might not trigger the reconnection.</span></span>

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a><span data-ttu-id="b2b7e-144">"Errore di montaggio (115): L'operazione è in corso" quando si esegue il montaggio dell'archiviazione file di Azure usando SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="b2b7e-144">"Mount error(115): Operation now in progress" when you mount Azure File storage by using SMB 3.0</span></span>

### <a name="cause"></a><span data-ttu-id="b2b7e-145">Causa</span><span class="sxs-lookup"><span data-stu-id="b2b7e-145">Cause</span></span>

<span data-ttu-id="b2b7e-146">Alcune distribuzioni Linux non supportano le funzionalità di crittografia in SMB 3.0 e gli utenti potrebbero ricevere un messaggio di errore "115" se tentano di eseguire il montaggio dell'archiviazione file di Azure usando SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-146">Some Linux distributions do not yet support encryption features in SMB 3.0 and users might receive a "115" error message if they try to mount Azure File storage by using SMB 3.0 because of a missing feature.</span></span>

### <a name="solution"></a><span data-ttu-id="b2b7e-147">Soluzione</span><span class="sxs-lookup"><span data-stu-id="b2b7e-147">Solution</span></span>

<span data-ttu-id="b2b7e-148">La funzionalità di crittografia per SMB 3.0 per Linux è stata introdotta nel kernel 4.11.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-148">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="b2b7e-149">Questa funzionalità consente di montare la condivisione file di Azure in locale o in un'altra area di Azure.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-149">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="b2b7e-150">Al momento della pubblicazione, di questa funzionalità è stato eseguito il backport in Ubuntu 17.04 e Ubuntu 16.10.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-150">At the time of publishing, this functionality has been backported to Ubuntu 17.04 and Ubuntu 16.10.</span></span> <span data-ttu-id="b2b7e-151">Se il client Linux SMB non supporta la crittografia, montare l'archiviazione file di Azure usando SMB 2.1 da una VM Linux di Azure presente nello stesso data center dell'account di archiviazione file.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-151">If your Linux SMB client does not support encryption, mount Azure File storage by using SMB 2.1 from an Azure Linux VM that's in the same datacenter as the File storage account.</span></span>

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a><span data-ttu-id="b2b7e-152">Rallentamento delle prestazioni in una condivisione file di Azure montata in una VM Linux</span><span class="sxs-lookup"><span data-stu-id="b2b7e-152">Slow performance on an Azure file share mounted on a Linux VM</span></span>

### <a name="cause"></a><span data-ttu-id="b2b7e-153">Causa</span><span class="sxs-lookup"><span data-stu-id="b2b7e-153">Cause</span></span>

<span data-ttu-id="b2b7e-154">Una possibile causa del rallentamento delle prestazioni è la disattivazione della memorizzazione nella cache.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-154">One possible cause of slow performance is disabled caching.</span></span>

### <a name="solution"></a><span data-ttu-id="b2b7e-155">Soluzione</span><span class="sxs-lookup"><span data-stu-id="b2b7e-155">Solution</span></span>

<span data-ttu-id="b2b7e-156">Per controllare se la memorizzazione nella cache è disattivata, cercare la voce **cache =**.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-156">To check whether caching is disabled, look for the **cache=** entry.</span></span> 

<span data-ttu-id="b2b7e-157">**cache=none** indica che la memorizzazione nella cache è disattivata.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-157">**Cache=none** indicates that caching is disabled.</span></span>  <span data-ttu-id="b2b7e-158">Eseguire nuovamente il montaggio della condivisione usando il comando di montaggio predefinito o aggiungendo esplicitamente l'opzione **cache=strict** al comando di montaggio per assicurarsi che la modalità di memorizzazione nella cache predefinita o "strict" sia attivata.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-158">Remount the share by using the default mount command or by explicitly adding the **cache=strict** option to the mount command to ensure that default caching or "strict" caching mode is enabled.</span></span>

<span data-ttu-id="b2b7e-159">In alcuni scenari, l'opzione di montaggio **serverino** può far sì che il comando **ls** esegua stat rispetto a ogni voce di directory.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-159">In some scenarios, the **serverino** mount option can cause the **ls** command to run stat against every directory entry.</span></span> <span data-ttu-id="b2b7e-160">Questo comportamento determina un calo delle prestazioni quando si elenca una directory di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-160">This behavior results in performance degradation when you're listing a big directory.</span></span> <span data-ttu-id="b2b7e-161">È possibile controllare le opzioni di montaggio nella voce **/etc/fstab**:</span><span class="sxs-lookup"><span data-stu-id="b2b7e-161">You can check the mount options in your **/etc/fstab** entry:</span></span>

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

<span data-ttu-id="b2b7e-162">È inoltre possibile controllare se vengono usate le opzioni corrette eseguendo il comando **sudo mount | grep cifs** e controllandone l'output, ad esempio l'output dell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="b2b7e-162">You can also check whether the correct options are being used by running the  **sudo mount | grep cifs** command and checking its output, such as the following example output:</span></span>

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

<span data-ttu-id="b2b7e-163">Se l'opzione **cache=strict** o **serverino** non è presente, smontare e montare nuovamente l'archiviazione file di Azure eseguendo il comando di montaggio dalla [documentazione](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b2b7e-163">If the **cache=strict** or **serverino** option is not present, unmount and mount Azure File storage again by running the mount command from the [documentation](storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="b2b7e-164">Verificare quindi di nuovo che la voce **/etc/fstab** disponga delle opzioni corrette.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-164">Then, recheck that the **/etc/fstab** entry has the correct options.</span></span>

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-to-linux"></a><span data-ttu-id="b2b7e-165">I timestamp sono andati persi durante la copia dei file da Windows a Linux</span><span class="sxs-lookup"><span data-stu-id="b2b7e-165">Time stamps were lost in copying files from Windows to Linux</span></span>

<span data-ttu-id="b2b7e-166">Nelle piattaforme Linux/Unix il comando **cp -p** ha esito negativo se file 1 e file 2 sono di proprietà di utenti diversi.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-166">On Linux/Unix platforms, the **cp -p** command fails if file 1 and file 2 are owned by different users.</span></span>

### <a name="cause"></a><span data-ttu-id="b2b7e-167">Causa</span><span class="sxs-lookup"><span data-stu-id="b2b7e-167">Cause</span></span>

<span data-ttu-id="b2b7e-168">Il flag force **f** in COPYFILE determina l'esecuzione di **cp -p -f** in Unix.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-168">The force flag **f** in COPYFILE results in executing **cp -p -f** on Unix.</span></span> <span data-ttu-id="b2b7e-169">Questo comando non riesce anche a mantenere il timestamp del file di cui non si è proprietari.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-169">This command also fails to preserve the time stamp of the file that you don't own.</span></span>

### <a name="workaround"></a><span data-ttu-id="b2b7e-170">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="b2b7e-170">Workaround</span></span>

<span data-ttu-id="b2b7e-171">Usare l'account utente di archiviazione per copiare i file:</span><span class="sxs-lookup"><span data-stu-id="b2b7e-171">Use the storage account user for copying the files:</span></span>

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a><span data-ttu-id="b2b7e-172">Richiesta di assistenza</span><span class="sxs-lookup"><span data-stu-id="b2b7e-172">Need help?</span></span> <span data-ttu-id="b2b7e-173">Contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-173">Contact support.</span></span>

<span data-ttu-id="b2b7e-174">Se si necessita ancora di assistenza, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) per ottenere una rapida risoluzione del problema.</span><span class="sxs-lookup"><span data-stu-id="b2b7e-174">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your problem resolved quickly.</span></span>
