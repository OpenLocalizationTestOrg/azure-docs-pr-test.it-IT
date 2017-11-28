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
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a><span data-ttu-id="1d793-103">Risolvere i problemi di archiviazione file di Azure in Windows</span><span class="sxs-lookup"><span data-stu-id="1d793-103">Troubleshoot Azure File storage problems in Windows</span></span>

<span data-ttu-id="1d793-104">Questo articolo vengono elencati i problemi comuni che sono correlati tooMicrosoft archiviazione di File di Azure per la connessione dal client di Windows.</span><span class="sxs-lookup"><span data-stu-id="1d793-104">This article lists common problems that are related tooMicrosoft Azure File storage when you connect from Windows clients.</span></span> <span data-ttu-id="1d793-105">L'articolo descrive anche le possibili cause e risoluzioni per tali problemi.</span><span class="sxs-lookup"><span data-stu-id="1d793-105">It also provides possible causes and resolutions for these problems.</span></span> <span data-ttu-id="1d793-106">Risoluzione dei problemi toohello inoltre i passaggi in questo articolo, è inoltre possibile utilizzare [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) per verificare che Windows hello ambiente client dispone di prerequisiti corretti.</span><span class="sxs-lookup"><span data-stu-id="1d793-106">In addition toohello troubleshooting steps in this article, you can also use [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) to ensure that hello Windows client environment has correct prerequisites.</span></span> <span data-ttu-id="1d793-107">AzFileDiagnostics consente di automatizzare il rilevamento della maggior parte dei sintomi di hello indicati in questo articolo e consente di configurare le prestazioni ottimali tooget di ambiente.</span><span class="sxs-lookup"><span data-stu-id="1d793-107">AzFileDiagnostics automates detection of most of hello symptoms mentioned in this article and helps set up your environment tooget optimal performance.</span></span> <span data-ttu-id="1d793-108">È inoltre possibile trovare queste informazioni in hello [le condivisioni file di Azure di risoluzione dei problemi](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) che fornisce i passaggi tooassist si problemi le condivisioni file di connessione, mapping/montaggio Azure.</span><span class="sxs-lookup"><span data-stu-id="1d793-108">You can also find this information in hello [Azure Files shares Troubleshooter](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) that provides steps tooassist you with problems connecting/mapping/mounting Azure Files shares.</span></span>


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a><span data-ttu-id="1d793-109">Errore 53, Errore 67 o Errore 87 quando si prova a montare o smontare una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="1d793-109">Error 53, Error 67, or Error 87 when you mount or unmount an Azure file share</span></span>

<span data-ttu-id="1d793-110">Quando si tenta di toomount una condivisione di file locale o da un altro Data Center, è possibile ricevere hello gli errori seguenti:</span><span class="sxs-lookup"><span data-stu-id="1d793-110">When you try toomount a file share from on-premises or from a different datacenter, you might receive hello following errors:</span></span>

- <span data-ttu-id="1d793-111">Errore di sistema 53.</span><span class="sxs-lookup"><span data-stu-id="1d793-111">System error 53 has occurred.</span></span> <span data-ttu-id="1d793-112">percorso di rete Hello non trovato.</span><span class="sxs-lookup"><span data-stu-id="1d793-112">hello network path was not found.</span></span>
- <span data-ttu-id="1d793-113">Errore di sistema 67.</span><span class="sxs-lookup"><span data-stu-id="1d793-113">System error 67 has occurred.</span></span> <span data-ttu-id="1d793-114">Impossibile trovare il nome di rete Hello.</span><span class="sxs-lookup"><span data-stu-id="1d793-114">hello network name cannot be found.</span></span>
- <span data-ttu-id="1d793-115">Errore di sistema 87.</span><span class="sxs-lookup"><span data-stu-id="1d793-115">System error 87 has occurred.</span></span> <span data-ttu-id="1d793-116">il parametro Hello è corretto.</span><span class="sxs-lookup"><span data-stu-id="1d793-116">hello parameter is incorrect.</span></span>

### <a name="cause-1-unencrypted-communication-channel"></a><span data-ttu-id="1d793-117">Causa 1: canale di comunicazione non crittografato</span><span class="sxs-lookup"><span data-stu-id="1d793-117">Cause 1: Unencrypted communication channel</span></span>

<span data-ttu-id="1d793-118">Per motivi di sicurezza, le connessioni tooAzure condivisioni di file bloccate se il canale di comunicazione hello non è crittografato e non viene effettuato il tentativo di connessione di hello da hello stesso Data Center in cui si trovano hello condivisioni di file di Azure.</span><span class="sxs-lookup"><span data-stu-id="1d793-118">For security reasons, connections tooAzure file shares are blocked if hello communication channel isn’t encrypted and if hello connection attempt isn't made from hello same datacenter where hello Azure file shares reside.</span></span> <span data-ttu-id="1d793-119">Crittografia del canale di comunicazione è disponibile solo se il client dell'utente hello del sistema operativo supporta la crittografia SMB.</span><span class="sxs-lookup"><span data-stu-id="1d793-119">Communication channel encryption is provided only if hello user’s client OS supports SMB encryption.</span></span>

<span data-ttu-id="1d793-120">Windows 8, Windows Server 2012 e le versioni successive di ciascuno dei due sistemi operativi negoziano richieste comprendenti SMB 3.0, che supporta la crittografia.</span><span class="sxs-lookup"><span data-stu-id="1d793-120">Windows 8, Windows Server 2012, and later versions of each system negotiate requests that include SMB 3.0, which supports encryption.</span></span>

### <a name="solution-for-cause-1"></a><span data-ttu-id="1d793-121">Soluzione per la causa 1</span><span class="sxs-lookup"><span data-stu-id="1d793-121">Solution for cause 1</span></span>

<span data-ttu-id="1d793-122">Connettersi da un client che esegue uno dei seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="1d793-122">Connect from a client that does one of hello following:</span></span>

- <span data-ttu-id="1d793-123">Soddisfa i requisiti di hello di Windows 8 e Windows Server 2012 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="1d793-123">Meets hello requirements of Windows 8 and Windows Server 2012 or later versions</span></span>
- <span data-ttu-id="1d793-124">Si connette da una macchina virtuale in hello stesso Data Center come account di archiviazione di Azure che viene utilizzato per la condivisione di file di Azure hello hello</span><span class="sxs-lookup"><span data-stu-id="1d793-124">Connects from a virtual machine in hello same datacenter as hello Azure storage account that is used for hello Azure file share</span></span>

### <a name="cause-2-port-445-is-blocked"></a><span data-ttu-id="1d793-125">Causa 2: la porta 445 è bloccata</span><span class="sxs-lookup"><span data-stu-id="1d793-125">Cause 2: Port 445 is blocked</span></span>

<span data-ttu-id="1d793-126">Errore di sistema 53 o sistema 67 può verificarsi se la porta 445 le comunicazioni in uscita tooan Azure File archiviazione Data Center è bloccato.</span><span class="sxs-lookup"><span data-stu-id="1d793-126">System error 53 or system error 67 can occur if port 445 outbound communication tooan Azure File storage datacenter is blocked.</span></span> <span data-ttu-id="1d793-127">riepilogo di hello toosee di ISP che consente o impedisce l'accesso dalla porta 445, andare troppo[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d793-127">toosee hello summary of ISPs that allow or disallow access from port 445, go too[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span></span>

<span data-ttu-id="1d793-128">toounderstand se questo è il motivo di hello dietro il messaggio "Errore di sistema 53" hello, è possibile utilizzare l'endpoint di TCP:445 Portqry tooquery hello.</span><span class="sxs-lookup"><span data-stu-id="1d793-128">toounderstand whether this is hello reason behind hello "System error 53" message, you can use Portqry tooquery hello TCP:445 endpoint.</span></span> <span data-ttu-id="1d793-129">Se endpoint TCP:445 hello viene visualizzato come filtrati, la porta TCP hello viene bloccato.</span><span class="sxs-lookup"><span data-stu-id="1d793-129">If hello TCP:445 endpoint is displayed as filtered, hello TCP port is blocked.</span></span> <span data-ttu-id="1d793-130">Di seguito è fornito un esempio di query:</span><span class="sxs-lookup"><span data-stu-id="1d793-130">Here is an example query:</span></span>

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

<span data-ttu-id="1d793-131">Se la porta TCP 445 è bloccata da una regola di percorso di rete hello, si noterà hello seguente output:</span><span class="sxs-lookup"><span data-stu-id="1d793-131">If TCP port 445 is blocked by a rule along hello network path, you will see hello following output:</span></span>

  `TCP port 445 (microsoft-ds service): FILTERED`

<span data-ttu-id="1d793-132">Per ulteriori informazioni su come toouse Portqry, vedere [descrizione dell'utilità della riga di comando di hello Portqry.exe](https://support.microsoft.com/help/310099).</span><span class="sxs-lookup"><span data-stu-id="1d793-132">For more information about how toouse Portqry, see [Description of hello Portqry.exe command-line utility](https://support.microsoft.com/help/310099).</span></span>

### <a name="solution-for-cause-2"></a><span data-ttu-id="1d793-133">Soluzione per la causa 2</span><span class="sxs-lookup"><span data-stu-id="1d793-133">Solution for cause 2</span></span>

<span data-ttu-id="1d793-134">Utilizzare la porta di tooopen reparto IT in uscita 445 troppo[intervalli IP Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="1d793-134">Work with your IT department tooopen port 445 outbound too[Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="cause-3-ntlmv1-is-enabled"></a><span data-ttu-id="1d793-135">Causa 3: è abilitata la comunicazione NTLMv1</span><span class="sxs-lookup"><span data-stu-id="1d793-135">Cause 3: NTLMv1 is enabled</span></span>

<span data-ttu-id="1d793-136">Errore di sistema 53 o errore di sistema 87 può verificarsi se è attivata la comunicazione di NTLMv1 sul client hello.</span><span class="sxs-lookup"><span data-stu-id="1d793-136">System error 53 or system error 87 can occur if NTLMv1 communication is enabled on hello client.</span></span> <span data-ttu-id="1d793-137">L'archiviazione file di Azure supporta solo l'autenticazione NTLMv2.</span><span class="sxs-lookup"><span data-stu-id="1d793-137">Azure File storage supports only NTLMv2 authentication.</span></span> <span data-ttu-id="1d793-138">Con la comunicazione NTLMv1 abilitata, il client è meno sicuro.</span><span class="sxs-lookup"><span data-stu-id="1d793-138">Having NTLMv1 enabled creates a less-secure client.</span></span> <span data-ttu-id="1d793-139">Di conseguenza, la comunicazione viene bloccata per l'archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="1d793-139">Therefore, communication is blocked for Azure File storage.</span></span> 

<span data-ttu-id="1d793-140">toodetermine se questa è hello causa dell'errore hello, verificare che hello seguente sottochiave del Registro di sistema è impostato un valore tooa 3:</span><span class="sxs-lookup"><span data-stu-id="1d793-140">toodetermine whether this is hello cause of hello error, verify that hello following registry subkey is set tooa value of 3:</span></span>

<span data-ttu-id="1d793-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa &gt; LmCompatibilityLevel**</span><span class="sxs-lookup"><span data-stu-id="1d793-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span></span>

<span data-ttu-id="1d793-142">Per ulteriori informazioni, vedere hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) argomento su TechNet.</span><span class="sxs-lookup"><span data-stu-id="1d793-142">For more information, see hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span></span>

### <a name="solution-for-cause-3"></a><span data-ttu-id="1d793-143">Soluzione per la causa 3</span><span class="sxs-lookup"><span data-stu-id="1d793-143">Solution for cause 3</span></span>

<span data-ttu-id="1d793-144">Ripristinare hello **LmCompatibilityLevel** valore toohello valore predefinito 3 in hello seguente sottochiave del Registro di sistema:</span><span class="sxs-lookup"><span data-stu-id="1d793-144">Revert hello **LmCompatibilityLevel** value toohello default value of 3 in hello following registry subkey:</span></span>

  <span data-ttu-id="1d793-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span><span class="sxs-lookup"><span data-stu-id="1d793-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span></span>

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-tooprocess-this-command-when-you-copy-tooan-azure-file-share"></a><span data-ttu-id="1d793-146">Errore 1816 "non è sufficiente quota trova tooprocess disponibile il comando" quando si copia tooan condivisione di file di Azure</span><span class="sxs-lookup"><span data-stu-id="1d793-146">Error 1816 “Not enough quota is available tooprocess this command” when you copy tooan Azure file share</span></span>

### <a name="cause"></a><span data-ttu-id="1d793-147">Causa</span><span class="sxs-lookup"><span data-stu-id="1d793-147">Cause</span></span>

<span data-ttu-id="1d793-148">Errore 1816 si verifica quando si raggiunge hello limite superiore di handle aperti simultanei consentite per un file nel computer di hello in cui è viene montata condivisione file hello.</span><span class="sxs-lookup"><span data-stu-id="1d793-148">Error 1816 happens when you reach hello upper limit of concurrent open handles that are allowed for a file on hello computer where hello file share is being mounted.</span></span>

### <a name="solution"></a><span data-ttu-id="1d793-149">Soluzione</span><span class="sxs-lookup"><span data-stu-id="1d793-149">Solution</span></span>

<span data-ttu-id="1d793-150">Ridurre il numero di hello di handle aperti simultanei chiudendo gli handle di alcuni e riprovare.</span><span class="sxs-lookup"><span data-stu-id="1d793-150">Reduce hello number of concurrent open handles by closing some handles, and then retry.</span></span> <span data-ttu-id="1d793-151">Per altre informazioni, vedere [Elenco di controllo di prestazioni e scalabilità per Archiviazione di Microsoft Azure](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1d793-151">For more information, see [Microsoft Azure Storage performance and scalability checklist](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-windows"></a><span data-ttu-id="1d793-152">File lenta copia tooand dall'archivio di File di Azure in Windows</span><span class="sxs-lookup"><span data-stu-id="1d793-152">Slow file copying tooand from Azure File storage in Windows</span></span>

<span data-ttu-id="1d793-153">Quando si tenta di tootransfer file toohello servizio File di Azure, è possibile visualizzare un rallentamento delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="1d793-153">You might see slow performance when you try tootransfer files toohello Azure File service.</span></span>

- <span data-ttu-id="1d793-154">Se non si dispone di un requisito delle dimensioni i/o minimo specifico, è consigliabile utilizzare 1 MB come hello dimensioni i/o per ottenere prestazioni ottimali.</span><span class="sxs-lookup"><span data-stu-id="1d793-154">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as hello I/O size for optimal performance.</span></span>
-   <span data-ttu-id="1d793-155">Se si conosce dimensioni finali del hello di un file che si estende con scrive e il software privo di problemi di compatibilità quando la coda non scritta nel file hello hello contiene zeri, quindi set hello dimensioni del file in anticipo anziché eseguire ogni operazione di scrittura di un'operazione di scrittura estensione.</span><span class="sxs-lookup"><span data-stu-id="1d793-155">If you know hello final size of a file that you are extending with writes, and your software doesn’t have compatibility problems when hello unwritten tail on hello file contains zeros, then set hello file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="1d793-156">Utilizzare il metodo di copia destra hello:</span><span class="sxs-lookup"><span data-stu-id="1d793-156">Use hello right copy method:</span></span>
    -   <span data-ttu-id="1d793-157">Usare [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) per i trasferimenti tra due condivisioni file.</span><span class="sxs-lookup"><span data-stu-id="1d793-157">Use [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="1d793-158">Usare [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) tra condivisioni file in un computer locale.</span><span class="sxs-lookup"><span data-stu-id="1d793-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a><span data-ttu-id="1d793-159">Considerazioni per Windows 8.1 o Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="1d793-159">Considerations for Windows 8.1 or Windows Server 2012 R2</span></span>

<span data-ttu-id="1d793-160">Per i client che eseguono Windows 8.1 o Windows Server 2012 R2, verificare che tale hello [KB3114025](https://support.microsoft.com/help/3114025) è installato l'hotfix.</span><span class="sxs-lookup"><span data-stu-id="1d793-160">For clients that are running Windows 8.1 or Windows Server 2012 R2, make sure that hello [KB3114025](https://support.microsoft.com/help/3114025) hotfix is installed.</span></span> <span data-ttu-id="1d793-161">Questo hotfix migliora le prestazioni di hello di creare e chiudere gli handle.</span><span class="sxs-lookup"><span data-stu-id="1d793-161">This hotfix improves hello performance of create and close handles.</span></span>

<span data-ttu-id="1d793-162">È possibile eseguire i seguenti script toocheck se è stato installato l'hotfix hello hello:</span><span class="sxs-lookup"><span data-stu-id="1d793-162">You can run hello following script toocheck whether hello hotfix has been installed:</span></span>

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

<span data-ttu-id="1d793-163">Se è installato l'hotfix, hello output seguente viene visualizzato:</span><span class="sxs-lookup"><span data-stu-id="1d793-163">If hotfix is installed, hello following output is displayed:</span></span>

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> <span data-ttu-id="1d793-164">Da dicembre 2015 la hotfix KB3114025 è installata per impostazione predefinita nelle immagini di Windows Server 2012 R2 presenti in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1d793-164">Windows Server 2012 R2 images in Azure Marketplace have hotfix KB3114025 installed by default, starting in December 2015.</span></span>

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a><span data-ttu-id="1d793-165">Nessuna cartella con una lettera di unità in **Computer locale**</span><span class="sxs-lookup"><span data-stu-id="1d793-165">No folder with a drive letter in **My Computer**</span></span>

<span data-ttu-id="1d793-166">Se si esegue il mapping di una condivisione di file di Azure come amministratore tramite comando net use, condivisione hello viene visualizzato toobe mancante.</span><span class="sxs-lookup"><span data-stu-id="1d793-166">If you map an Azure file share as an administrator by using net use, hello share appears toobe missing.</span></span>

### <a name="cause"></a><span data-ttu-id="1d793-167">Causa</span><span class="sxs-lookup"><span data-stu-id="1d793-167">Cause</span></span>

<span data-ttu-id="1d793-168">Per impostazione predefinita, Esplora file di Windows non viene eseguito come amministratore.</span><span class="sxs-lookup"><span data-stu-id="1d793-168">By default, Windows File Explorer does not run as an administrator.</span></span> <span data-ttu-id="1d793-169">Se si esegue comando net use da un prompt dei comandi amministrativo, eseguire il mapping di unità di rete hello come amministratore.</span><span class="sxs-lookup"><span data-stu-id="1d793-169">If you run net use from an administrative command prompt, you map hello network drive as an administrator.</span></span> <span data-ttu-id="1d793-170">Poiché le unità mappate sono specifiche per l'utente, account utente di hello viene registrato non viene visualizzata hello unità se sono montati in un account utente diverso.</span><span class="sxs-lookup"><span data-stu-id="1d793-170">Because mapped drives are user-centric, hello user account that is logged in does not display hello drives if they are mounted under a different user account.</span></span>

### <a name="solution"></a><span data-ttu-id="1d793-171">Soluzione</span><span class="sxs-lookup"><span data-stu-id="1d793-171">Solution</span></span>
<span data-ttu-id="1d793-172">Montaggio hello condivisione dalla riga di comando senza privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="1d793-172">Mount hello share from a non-administrator command line.</span></span> <span data-ttu-id="1d793-173">In alternativa, è possibile seguire [in questo argomento TechNet](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** il valore del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="1d793-173">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** registry value.</span></span>

<a id="netuse"></a>
## <a name="net-use-command-fails-if-hello-storage-account-contains-a-forward-slash"></a><span data-ttu-id="1d793-174">Comando NET use non riesce se l'account di archiviazione hello contiene un carattere barra rovesciata</span><span class="sxs-lookup"><span data-stu-id="1d793-174">Net use command fails if hello storage account contains a forward slash</span></span>

### <a name="cause"></a><span data-ttu-id="1d793-175">Causa</span><span class="sxs-lookup"><span data-stu-id="1d793-175">Cause</span></span>

<span data-ttu-id="1d793-176">comando net use Hello interpreta una barra (/) come un'opzione della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="1d793-176">hello net use command interprets a forward slash (/) as a command-line option.</span></span> <span data-ttu-id="1d793-177">Se il nome dell'account utente deve iniziare con una barra, mapping delle unità hello ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="1d793-177">If your user account name starts with a forward slash, hello drive mapping fails.</span></span>

### <a name="solution"></a><span data-ttu-id="1d793-178">Soluzione</span><span class="sxs-lookup"><span data-stu-id="1d793-178">Solution</span></span>

<span data-ttu-id="1d793-179">È possibile utilizzare uno dei seguenti passaggi toowork problema hello hello:</span><span class="sxs-lookup"><span data-stu-id="1d793-179">You can use either of hello following steps toowork around hello problem:</span></span>

- <span data-ttu-id="1d793-180">Eseguire il comando PowerShell seguente hello:</span><span class="sxs-lookup"><span data-stu-id="1d793-180">Run hello following PowerShell command:</span></span>

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  <span data-ttu-id="1d793-181">Da un file batch, è possibile eseguire il comando hello in questo modo:</span><span class="sxs-lookup"><span data-stu-id="1d793-181">From a batch file, you can run hello command this way:</span></span>

  `Echo new-smbMapping ... | powershell -command –`

- <span data-ttu-id="1d793-182">Inserire virgolette doppie hello toowork chiave questo problema, a meno che non barra hello è hello primo carattere.</span><span class="sxs-lookup"><span data-stu-id="1d793-182">Put double quotation marks around hello key toowork around this problem--unless hello forward slash is hello first character.</span></span> <span data-ttu-id="1d793-183">Questo caso, utilizzare la modalità interattiva hello e immettere la password separatamente o rigenerare il tooget chiavi una chiave che non inizia con una barra rovesciata.</span><span class="sxs-lookup"><span data-stu-id="1d793-183">If it is, either use hello interactive mode and enter your password separately or regenerate your keys tooget a key that doesn't start with a forward slash.</span></span>

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a><span data-ttu-id="1d793-184">L'applicazione o il servizio non può accedere a un'unità di archiviazione file di Azure montata</span><span class="sxs-lookup"><span data-stu-id="1d793-184">Application or service cannot access a mounted Azure File storage drive</span></span>

### <a name="cause"></a><span data-ttu-id="1d793-185">Causa</span><span class="sxs-lookup"><span data-stu-id="1d793-185">Cause</span></span>

<span data-ttu-id="1d793-186">Le unità vengono montate per utente.</span><span class="sxs-lookup"><span data-stu-id="1d793-186">Drives are mounted per user.</span></span> <span data-ttu-id="1d793-187">Se l'applicazione o il servizio è in esecuzione con un account utente diverso rispetto hello che hello unità montata, un'applicazione hello non visualizzeranno unità hello.</span><span class="sxs-lookup"><span data-stu-id="1d793-187">If your application or service is running under a different user account than hello one that mounted hello drive, hello application will not see hello drive.</span></span>

### <a name="solution"></a><span data-ttu-id="1d793-188">Soluzione</span><span class="sxs-lookup"><span data-stu-id="1d793-188">Solution</span></span>

<span data-ttu-id="1d793-189">Utilizzare una delle seguenti soluzioni hello:</span><span class="sxs-lookup"><span data-stu-id="1d793-189">Use one of hello following solutions:</span></span>

-   <span data-ttu-id="1d793-190">Montare l'unità di hello da hello stesso account utente che contiene l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1d793-190">Mount hello drive from hello same user account that contains hello application.</span></span> <span data-ttu-id="1d793-191">Si può usare uno strumento come PsExec.</span><span class="sxs-lookup"><span data-stu-id="1d793-191">You can use a tool such as PsExec.</span></span>
- <span data-ttu-id="1d793-192">Passare parametri hello utente nome e la password del comando net use hello Nome account di archiviazione hello e la chiave.</span><span class="sxs-lookup"><span data-stu-id="1d793-192">Pass hello storage account name and key in hello user name and password parameters of hello net use command.</span></span>

<span data-ttu-id="1d793-193">Dopo aver eseguito queste operazioni, è possibile ricevere hello seguente messaggio di errore quando si esegue comando net use per account del servizio di rete del sistema/hello: "1312 errore di sistema.</span><span class="sxs-lookup"><span data-stu-id="1d793-193">After you follow these instructions, you might receive hello following error message when you run net use for hello system/network service account: "System error 1312 has occurred.</span></span> <span data-ttu-id="1d793-194">Una sessione di accesso specificata non esiste.</span><span class="sxs-lookup"><span data-stu-id="1d793-194">A specified logon session does not exist.</span></span> <span data-ttu-id="1d793-195">Potrebbe essere già stata terminata."</span><span class="sxs-lookup"><span data-stu-id="1d793-195">It may already have been terminated."</span></span> <span data-ttu-id="1d793-196">In questo caso, verificare che nome utente passato toonet utilizzare hello include informazioni sul dominio (ad esempio: "[nome account di archiviazione]. file.core.windows .net").</span><span class="sxs-lookup"><span data-stu-id="1d793-196">If this occurs, make sure that hello username that is passed toonet use includes domain information (for example: "[storage account name].file.core.windows.net").</span></span>

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-tooa-destination-that-does-not-support-encryption"></a><span data-ttu-id="1d793-197">Errore "Si copia una destinazione tooa di file che non supporta la crittografia"</span><span class="sxs-lookup"><span data-stu-id="1d793-197">Error "You are copying a file tooa destination that does not support encryption"</span></span>

<span data-ttu-id="1d793-198">Quando un file viene copiato attraverso la rete hello, è stato decrittografato nel computer di origine hello, trasmesso in testo non crittografato e crittografati nuovamente nella destinazione hello file hello.</span><span class="sxs-lookup"><span data-stu-id="1d793-198">When a file is copied over hello network, hello file is decrypted on hello source computer, transmitted in plaintext, and re-encrypted at hello destination.</span></span> <span data-ttu-id="1d793-199">Tuttavia, si potrebbe vedere il seguente errore durante il tentativo toocopy un file crittografato hello: "Si sta copiando destinazione di tooa file hello che non supporta la crittografia".</span><span class="sxs-lookup"><span data-stu-id="1d793-199">However, you might see hello following error when you're trying toocopy an encrypted file: "You are copying hello file tooa destination that does not support encryption."</span></span>

### <a name="cause"></a><span data-ttu-id="1d793-200">Causa</span><span class="sxs-lookup"><span data-stu-id="1d793-200">Cause</span></span>
<span data-ttu-id="1d793-201">Questo problema può verificarsi se si usa EFS (Encrypting File System).</span><span class="sxs-lookup"><span data-stu-id="1d793-201">This problem can occur if you are using Encrypting File System (EFS).</span></span> <span data-ttu-id="1d793-202">I file crittografati con BitLocker possono essere copiato tooAzure archiviazione di File.</span><span class="sxs-lookup"><span data-stu-id="1d793-202">BitLocker-encrypted files can be copied tooAzure File storage.</span></span> <span data-ttu-id="1d793-203">Tuttavia, l'archiviazione file di Azure non supporta NTFS EFS.</span><span class="sxs-lookup"><span data-stu-id="1d793-203">However, Azure File storage does not support NTFS EFS.</span></span>

### <a name="workaround"></a><span data-ttu-id="1d793-204">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="1d793-204">Workaround</span></span>
<span data-ttu-id="1d793-205">un file in rete hello toocopy, è necessario prima decrittografarlo.</span><span class="sxs-lookup"><span data-stu-id="1d793-205">toocopy a file over hello network, you must first decrypt it.</span></span> <span data-ttu-id="1d793-206">Utilizzare uno dei seguenti metodi hello:</span><span class="sxs-lookup"><span data-stu-id="1d793-206">Use one of hello following methods:</span></span>

- <span data-ttu-id="1d793-207">Hello utilizzare **copiare /d** comando.</span><span class="sxs-lookup"><span data-stu-id="1d793-207">Use hello **copy /d** command.</span></span> <span data-ttu-id="1d793-208">Consente di crittografato hello file toobe salvato come file decrittografati destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="1d793-208">It allows hello encrypted files toobe saved as decrypted files at hello destination.</span></span>
- <span data-ttu-id="1d793-209">Impostare hello seguente chiave del Registro di sistema:</span><span class="sxs-lookup"><span data-stu-id="1d793-209">Set hello following registry key:</span></span>
  - <span data-ttu-id="1d793-210">Percorso = HKLM\Software\Policies\Microsoft\Windows\System</span><span class="sxs-lookup"><span data-stu-id="1d793-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span></span>
  - <span data-ttu-id="1d793-211">Tipo valore = DWORD</span><span class="sxs-lookup"><span data-stu-id="1d793-211">Value type = DWORD</span></span>
  - <span data-ttu-id="1d793-212">Nome = CopyFileAllowDecryptedRemoteDestination</span><span class="sxs-lookup"><span data-stu-id="1d793-212">Name = CopyFileAllowDecryptedRemoteDestination</span></span>
  - <span data-ttu-id="1d793-213">Valore = 1</span><span class="sxs-lookup"><span data-stu-id="1d793-213">Value = 1</span></span>

<span data-ttu-id="1d793-214">Tenere presente tale chiave del Registro di sistema di hello impostazione influisce su tutte le operazioni di copia che vengono apportate toonetwork condivisioni.</span><span class="sxs-lookup"><span data-stu-id="1d793-214">Be aware that setting hello registry key affects all copy operations that are made toonetwork shares.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="1d793-215">Richiesta di assistenza</span><span class="sxs-lookup"><span data-stu-id="1d793-215">Need help?</span></span> <span data-ttu-id="1d793-216">Contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="1d793-216">Contact support.</span></span>
<span data-ttu-id="1d793-217">Se è ancora necessario della Guida, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema.</span><span class="sxs-lookup"><span data-stu-id="1d793-217">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your problem resolved quickly.</span></span>
