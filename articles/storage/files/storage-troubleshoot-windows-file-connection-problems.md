---
title: Risolvere i problemi di archiviazione file di Azure in Windows | Microsoft Docs
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
ms.openlocfilehash: daaf7d0589f5e2d82b43dad879bffd23370a2c81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a><span data-ttu-id="de1b1-103">Risolvere i problemi di archiviazione file di Azure in Windows</span><span class="sxs-lookup"><span data-stu-id="de1b1-103">Troubleshoot Azure File storage problems in Windows</span></span>

<span data-ttu-id="de1b1-104">Questo articolo elenca i problemi comuni correlati all'archiviazione file di Microsoft Azure quando si effettua la connessione da client Windows.</span><span class="sxs-lookup"><span data-stu-id="de1b1-104">This article lists common problems that are related to Microsoft Azure File storage when you connect from Windows clients.</span></span> <span data-ttu-id="de1b1-105">L'articolo descrive anche le possibili cause e risoluzioni per tali problemi.</span><span class="sxs-lookup"><span data-stu-id="de1b1-105">It also provides possible causes and resolutions for these problems.</span></span> <span data-ttu-id="de1b1-106">Oltre ai passaggi di risoluzione dei problemi in questo articolo, si può anche usare [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) per verificare che l'ambiente client Windows abbia prerequisiti corretti.</span><span class="sxs-lookup"><span data-stu-id="de1b1-106">In addition to the troubleshooting steps in this article, you can also use [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) to ensure that the Windows client environment has correct prerequisites.</span></span> <span data-ttu-id="de1b1-107">AzFileDiagnostics automatizza il rilevamento della maggior parte dei sintomi indicati in questo articolo e consente di configurare l'ambiente in modo da ottenere prestazioni ottimali.</span><span class="sxs-lookup"><span data-stu-id="de1b1-107">AzFileDiagnostics automates detection of most of the symptoms mentioned in this article and helps set up your environment to get optimal performance.</span></span> <span data-ttu-id="de1b1-108">È anche possibile trovare queste informazioni nell'articolo che illustra come [risolvere i problemi delle condivisioni File di Azure](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) e indica i passaggi per risolvere problemi di connessione, mapping e montaggio delle condivisioni file di Azure.</span><span class="sxs-lookup"><span data-stu-id="de1b1-108">You can also find this information in the [Azure Files shares Troubleshooter](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) that provides steps to assist you with problems connecting/mapping/mounting Azure Files shares.</span></span>


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a><span data-ttu-id="de1b1-109">Errore 53, Errore 67 o Errore 87 quando si prova a montare o smontare una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="de1b1-109">Error 53, Error 67, or Error 87 when you mount or unmount an Azure file share</span></span>

<span data-ttu-id="de1b1-110">Quando si prova a montare una condivisione file da locale o da un data center diverso, potrebbero verificarsi gli errori seguenti:</span><span class="sxs-lookup"><span data-stu-id="de1b1-110">When you try to mount a file share from on-premises or from a different datacenter, you might receive the following errors:</span></span>

- <span data-ttu-id="de1b1-111">Errore di sistema 53.</span><span class="sxs-lookup"><span data-stu-id="de1b1-111">System error 53 has occurred.</span></span> <span data-ttu-id="de1b1-112">Impossibile trovare il percorso di rete.</span><span class="sxs-lookup"><span data-stu-id="de1b1-112">The network path was not found.</span></span>
- <span data-ttu-id="de1b1-113">Errore di sistema 67.</span><span class="sxs-lookup"><span data-stu-id="de1b1-113">System error 67 has occurred.</span></span> <span data-ttu-id="de1b1-114">Impossibile trovare il nome della rete.</span><span class="sxs-lookup"><span data-stu-id="de1b1-114">The network name cannot be found.</span></span>
- <span data-ttu-id="de1b1-115">Errore di sistema 87.</span><span class="sxs-lookup"><span data-stu-id="de1b1-115">System error 87 has occurred.</span></span> <span data-ttu-id="de1b1-116">Parametro non corretto.</span><span class="sxs-lookup"><span data-stu-id="de1b1-116">The parameter is incorrect.</span></span>

### <a name="cause-1-unencrypted-communication-channel"></a><span data-ttu-id="de1b1-117">Causa 1: canale di comunicazione non crittografato</span><span class="sxs-lookup"><span data-stu-id="de1b1-117">Cause 1: Unencrypted communication channel</span></span>

<span data-ttu-id="de1b1-118">Per motivi di sicurezza, le connessioni alle condivisioni file di Azure vengono bloccate se il canale di comunicazione non è crittografato e il tentativo di connessione non viene effettuato dallo stesso data center in cui si trovano tali condivisioni.</span><span class="sxs-lookup"><span data-stu-id="de1b1-118">For security reasons, connections to Azure file shares are blocked if the communication channel isn’t encrypted and if the connection attempt isn't made from the same datacenter where the Azure file shares reside.</span></span> <span data-ttu-id="de1b1-119">La crittografia del canale di comunicazione è disponibile solo se il sistema operativo del client dell'utente supporta la crittografia SMB.</span><span class="sxs-lookup"><span data-stu-id="de1b1-119">Communication channel encryption is provided only if the user’s client OS supports SMB encryption.</span></span>

<span data-ttu-id="de1b1-120">Windows 8, Windows Server 2012 e le versioni successive di ciascuno dei due sistemi operativi negoziano richieste comprendenti SMB 3.0, che supporta la crittografia.</span><span class="sxs-lookup"><span data-stu-id="de1b1-120">Windows 8, Windows Server 2012, and later versions of each system negotiate requests that include SMB 3.0, which supports encryption.</span></span>

### <a name="solution-for-cause-1"></a><span data-ttu-id="de1b1-121">Soluzione per la causa 1</span><span class="sxs-lookup"><span data-stu-id="de1b1-121">Solution for cause 1</span></span>

<span data-ttu-id="de1b1-122">Connettersi da un client che soddisfa uno dei requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="de1b1-122">Connect from a client that does one of the following:</span></span>

- <span data-ttu-id="de1b1-123">Soddisfa i requisiti di Windows 8 e Windows Server 2012 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="de1b1-123">Meets the requirements of Windows 8 and Windows Server 2012 or later versions</span></span>
- <span data-ttu-id="de1b1-124">Effettua la connessione da una macchina virtuale nello stesso data center dell'account di archiviazione di Azure usato per la condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="de1b1-124">Connects from a virtual machine in the same datacenter as the Azure storage account that is used for the Azure file share</span></span>

### <a name="cause-2-port-445-is-blocked"></a><span data-ttu-id="de1b1-125">Causa 2: la porta 445 è bloccata</span><span class="sxs-lookup"><span data-stu-id="de1b1-125">Cause 2: Port 445 is blocked</span></span>

<span data-ttu-id="de1b1-126">L'errore di sistema 53 o 67 può verificarsi se la comunicazione in uscita dalla porta 445 verso un data center di archiviazione file di Azure è bloccata.</span><span class="sxs-lookup"><span data-stu-id="de1b1-126">System error 53 or system error 67 can occur if port 445 outbound communication to an Azure File storage datacenter is blocked.</span></span> <span data-ttu-id="de1b1-127">Passare a [TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx) per visualizzare un riepilogo degli ISP in grado di consentire o proibire l'accesso dalla porta 445.</span><span class="sxs-lookup"><span data-stu-id="de1b1-127">To see the summary of ISPs that allow or disallow access from port 445, go to [TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span></span>

<span data-ttu-id="de1b1-128">Per comprendere se l'errore di sistema 53 viene visualizzato per questo motivo, è possibile eseguire una query sull'endpoint TCP:445 mediante Portqry.</span><span class="sxs-lookup"><span data-stu-id="de1b1-128">To understand whether this is the reason behind the "System error 53" message, you can use Portqry to query the TCP:445 endpoint.</span></span> <span data-ttu-id="de1b1-129">Se l'endpoint TCP:445 risulta filtrato, la porta TCP è bloccata.</span><span class="sxs-lookup"><span data-stu-id="de1b1-129">If the TCP:445 endpoint is displayed as filtered, the TCP port is blocked.</span></span> <span data-ttu-id="de1b1-130">Di seguito è fornito un esempio di query:</span><span class="sxs-lookup"><span data-stu-id="de1b1-130">Here is an example query:</span></span>

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

<span data-ttu-id="de1b1-131">Se la porta TCP 445 è bloccata da una regola del percorso di rete, verrà visualizzato l'output seguente:</span><span class="sxs-lookup"><span data-stu-id="de1b1-131">If TCP port 445 is blocked by a rule along the network path, you will see the following output:</span></span>

  `TCP port 445 (microsoft-ds service): FILTERED`

<span data-ttu-id="de1b1-132">Per altre informazioni sull'uso di Portqry, vedere [Descrizione dell'utilità della riga di comando Portqry.exe](https://support.microsoft.com/help/310099).</span><span class="sxs-lookup"><span data-stu-id="de1b1-132">For more information about how to use Portqry, see [Description of the Portqry.exe command-line utility](https://support.microsoft.com/help/310099).</span></span>

### <a name="solution-for-cause-2"></a><span data-ttu-id="de1b1-133">Soluzione per la causa 2</span><span class="sxs-lookup"><span data-stu-id="de1b1-133">Solution for cause 2</span></span>

<span data-ttu-id="de1b1-134">Collaborare con il reparto IT per aprire la porta 445 in uscita verso gli [intervalli IP di Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="de1b1-134">Work with your IT department to open port 445 outbound to [Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="cause-3-ntlmv1-is-enabled"></a><span data-ttu-id="de1b1-135">Causa 3: è abilitata la comunicazione NTLMv1</span><span class="sxs-lookup"><span data-stu-id="de1b1-135">Cause 3: NTLMv1 is enabled</span></span>

<span data-ttu-id="de1b1-136">L'errore di sistema 53 o 87 può verificarsi se sul client è abilitata la comunicazione NTLMv1.</span><span class="sxs-lookup"><span data-stu-id="de1b1-136">System error 53 or system error 87 can occur if NTLMv1 communication is enabled on the client.</span></span> <span data-ttu-id="de1b1-137">L'archiviazione file di Azure supporta solo l'autenticazione NTLMv2.</span><span class="sxs-lookup"><span data-stu-id="de1b1-137">Azure File storage supports only NTLMv2 authentication.</span></span> <span data-ttu-id="de1b1-138">Con la comunicazione NTLMv1 abilitata, il client è meno sicuro.</span><span class="sxs-lookup"><span data-stu-id="de1b1-138">Having NTLMv1 enabled creates a less-secure client.</span></span> <span data-ttu-id="de1b1-139">Di conseguenza, la comunicazione viene bloccata per l'archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="de1b1-139">Therefore, communication is blocked for Azure File storage.</span></span> 

<span data-ttu-id="de1b1-140">Per determinare se questa è la causa dell'errore, assicurarsi che la sottochiave seguente del Registro di sistema sia impostata su 3:</span><span class="sxs-lookup"><span data-stu-id="de1b1-140">To determine whether this is the cause of the error, verify that the following registry subkey is set to a value of 3:</span></span>

<span data-ttu-id="de1b1-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span><span class="sxs-lookup"><span data-stu-id="de1b1-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span></span>

<span data-ttu-id="de1b1-142">Per altre informazioni, vedere l'argomento [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) su TechNet.</span><span class="sxs-lookup"><span data-stu-id="de1b1-142">For more information, see the [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span></span>

### <a name="solution-for-cause-3"></a><span data-ttu-id="de1b1-143">Soluzione per la causa 3</span><span class="sxs-lookup"><span data-stu-id="de1b1-143">Solution for cause 3</span></span>

<span data-ttu-id="de1b1-144">Ripristinare **LmCompatibilityLevel** sul valore predefinito 3 nella sottochiave seguente del Registro di sistema:</span><span class="sxs-lookup"><span data-stu-id="de1b1-144">Revert the **LmCompatibilityLevel** value to the default value of 3 in the following registry subkey:</span></span>

  <span data-ttu-id="de1b1-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span><span class="sxs-lookup"><span data-stu-id="de1b1-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span></span>

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-to-process-this-command-when-you-copy-to-an-azure-file-share"></a><span data-ttu-id="de1b1-146">Errore 1816 "Non c'è abbastanza disponibilità per elaborare il comando" quando si esegue la copia in una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="de1b1-146">Error 1816 “Not enough quota is available to process this command” when you copy to an Azure file share</span></span>

### <a name="cause"></a><span data-ttu-id="de1b1-147">Causa</span><span class="sxs-lookup"><span data-stu-id="de1b1-147">Cause</span></span>

<span data-ttu-id="de1b1-148">L'errore 1816 si verifica quando si raggiunge il limite massimo di handle aperti simultanei consentito per un file nel computer in cui si sta montando la condivisione file.</span><span class="sxs-lookup"><span data-stu-id="de1b1-148">Error 1816 happens when you reach the upper limit of concurrent open handles that are allowed for a file on the computer where the file share is being mounted.</span></span>

### <a name="solution"></a><span data-ttu-id="de1b1-149">Soluzione</span><span class="sxs-lookup"><span data-stu-id="de1b1-149">Solution</span></span>

<span data-ttu-id="de1b1-150">Chiudere alcuni degli handle aperti simultaneamente per ridurne il numero e quindi riprovare.</span><span class="sxs-lookup"><span data-stu-id="de1b1-150">Reduce the number of concurrent open handles by closing some handles, and then retry.</span></span> <span data-ttu-id="de1b1-151">Per altre informazioni, vedere [Elenco di controllo di prestazioni e scalabilità per Archiviazione di Microsoft Azure](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="de1b1-151">For more information, see [Microsoft Azure Storage performance and scalability checklist](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-to-and-from-azure-file-storage-in-windows"></a><span data-ttu-id="de1b1-152">Rallentamento della copia del file da e verso l'archiviazione file di Azure in Windows</span><span class="sxs-lookup"><span data-stu-id="de1b1-152">Slow file copying to and from Azure File storage in Windows</span></span>

<span data-ttu-id="de1b1-153">Si potrebbe verificare un rallentamento delle prestazioni quando si prova a trasferire file nel servizio File di Azure.</span><span class="sxs-lookup"><span data-stu-id="de1b1-153">You might see slow performance when you try to transfer files to the Azure File service.</span></span>

- <span data-ttu-id="de1b1-154">In assenza di un requisito minimo specifico per la dimensione di I/O, è consigliabile usare 1 MB per assicurare prestazioni ottimali.</span><span class="sxs-lookup"><span data-stu-id="de1b1-154">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as the I/O size for optimal performance.</span></span>
-   <span data-ttu-id="de1b1-155">Se si conosce la dimensione finale del file che si vuole estendere con operazioni di scrittura e il software non ha problemi di compatibilità se la parte finale del file non ancora scritta contiene zeri, impostare le dimensioni del file in fase preliminare anziché lasciare che ogni operazione di scrittura venga considerata un'estensione.</span><span class="sxs-lookup"><span data-stu-id="de1b1-155">If you know the final size of a file that you are extending with writes, and your software doesn’t have compatibility problems when the unwritten tail on the file contains zeros, then set the file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="de1b1-156">Usare il metodo di copia corretto:</span><span class="sxs-lookup"><span data-stu-id="de1b1-156">Use the right copy method:</span></span>
    -   <span data-ttu-id="de1b1-157">Usare [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) per i trasferimenti tra due condivisioni file.</span><span class="sxs-lookup"><span data-stu-id="de1b1-157">Use [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="de1b1-158">Usare [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) tra condivisioni file in un computer locale.</span><span class="sxs-lookup"><span data-stu-id="de1b1-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a><span data-ttu-id="de1b1-159">Considerazioni per Windows 8.1 o Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="de1b1-159">Considerations for Windows 8.1 or Windows Server 2012 R2</span></span>

<span data-ttu-id="de1b1-160">Per i client che eseguono Windows 8.1 o Windows Server 2012 R2, assicurarsi che sia installata la hotfix [KB3114025](https://support.microsoft.com/help/3114025).</span><span class="sxs-lookup"><span data-stu-id="de1b1-160">For clients that are running Windows 8.1 or Windows Server 2012 R2, make sure that the [KB3114025](https://support.microsoft.com/help/3114025) hotfix is installed.</span></span> <span data-ttu-id="de1b1-161">Questa hotfix consente di migliorare le prestazioni durante la creazione e la chiusura degli handle.</span><span class="sxs-lookup"><span data-stu-id="de1b1-161">This hotfix improves the performance of create and close handles.</span></span>

<span data-ttu-id="de1b1-162">Per verificare se la hotfix è stata installata, è possibile eseguire lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="de1b1-162">You can run the following script to check whether the hotfix has been installed:</span></span>

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

<span data-ttu-id="de1b1-163">Se la hotfix è installata, viene visualizzato l'output seguente:</span><span class="sxs-lookup"><span data-stu-id="de1b1-163">If hotfix is installed, the following output is displayed:</span></span>

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> <span data-ttu-id="de1b1-164">Da dicembre 2015 la hotfix KB3114025 è installata per impostazione predefinita nelle immagini di Windows Server 2012 R2 presenti in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="de1b1-164">Windows Server 2012 R2 images in Azure Marketplace have hotfix KB3114025 installed by default, starting in December 2015.</span></span>

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a><span data-ttu-id="de1b1-165">Nessuna cartella con una lettera di unità in **Computer locale**</span><span class="sxs-lookup"><span data-stu-id="de1b1-165">No folder with a drive letter in **My Computer**</span></span>

<span data-ttu-id="de1b1-166">Se si esegue il mapping di una condivisione di file di Azure come amministratore tramite il comando net use, la condivisione risulta mancante.</span><span class="sxs-lookup"><span data-stu-id="de1b1-166">If you map an Azure file share as an administrator by using net use, the share appears to be missing.</span></span>

### <a name="cause"></a><span data-ttu-id="de1b1-167">Causa</span><span class="sxs-lookup"><span data-stu-id="de1b1-167">Cause</span></span>

<span data-ttu-id="de1b1-168">Per impostazione predefinita, Esplora file di Windows non viene eseguito come amministratore.</span><span class="sxs-lookup"><span data-stu-id="de1b1-168">By default, Windows File Explorer does not run as an administrator.</span></span> <span data-ttu-id="de1b1-169">Se si esegue net use da un prompt dei comandi amministrativo, il mapping dell'unità di rete viene eseguito come amministratore.</span><span class="sxs-lookup"><span data-stu-id="de1b1-169">If you run net use from an administrative command prompt, you map the network drive as an administrator.</span></span> <span data-ttu-id="de1b1-170">Poiché le unità mappate sono incentrate sull'utente, l'account utente usato per la connessione non ne consente la visualizzazione se tali unità sono state montate con un account utente diverso.</span><span class="sxs-lookup"><span data-stu-id="de1b1-170">Because mapped drives are user-centric, the user account that is logged in does not display the drives if they are mounted under a different user account.</span></span>

### <a name="solution"></a><span data-ttu-id="de1b1-171">Soluzione</span><span class="sxs-lookup"><span data-stu-id="de1b1-171">Solution</span></span>
<span data-ttu-id="de1b1-172">Montare la condivisione da una riga di comando senza privilegi di amministratore.</span><span class="sxs-lookup"><span data-stu-id="de1b1-172">Mount the share from a non-administrator command line.</span></span> <span data-ttu-id="de1b1-173">In alternativa, è possibile seguire la procedura descritta in [questo argomento di TechNet](https://technet.microsoft.com/library/ee844140.aspx) per configurare il valore del Registro di sistema **EnableLinkedConnections**.</span><span class="sxs-lookup"><span data-stu-id="de1b1-173">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) to configure the **EnableLinkedConnections** registry value.</span></span>

<a id="netuse"></a>
## <a name="net-use-command-fails-if-the-storage-account-contains-a-forward-slash"></a><span data-ttu-id="de1b1-174">Il comando net use non viene eseguito se l'account di archiviazione contiene una barra</span><span class="sxs-lookup"><span data-stu-id="de1b1-174">Net use command fails if the storage account contains a forward slash</span></span>

### <a name="cause"></a><span data-ttu-id="de1b1-175">Causa</span><span class="sxs-lookup"><span data-stu-id="de1b1-175">Cause</span></span>

<span data-ttu-id="de1b1-176">Il comando net use interpreta una barra (/) come un'opzione della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="de1b1-176">The net use command interprets a forward slash (/) as a command-line option.</span></span> <span data-ttu-id="de1b1-177">Se il nome dell'account utente inizia con una barra, il mapping dell'unità ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="de1b1-177">If your user account name starts with a forward slash, the drive mapping fails.</span></span>

### <a name="solution"></a><span data-ttu-id="de1b1-178">Soluzione</span><span class="sxs-lookup"><span data-stu-id="de1b1-178">Solution</span></span>

<span data-ttu-id="de1b1-179">Per risolvere il problema, è possibile attenersi a una delle procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="de1b1-179">You can use either of the following steps to work around the problem:</span></span>

- <span data-ttu-id="de1b1-180">Eseguire il seguente comando PowerShell:</span><span class="sxs-lookup"><span data-stu-id="de1b1-180">Run the following PowerShell command:</span></span>

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  <span data-ttu-id="de1b1-181">Da un file batch, si può eseguire il comando in questo modo:</span><span class="sxs-lookup"><span data-stu-id="de1b1-181">From a batch file, you can run the command this way:</span></span>

  `Echo new-smbMapping ... | powershell -command –`

- <span data-ttu-id="de1b1-182">Racchiudere la chiave tra virgolette doppie, a meno che la barra non sia il primo carattere.</span><span class="sxs-lookup"><span data-stu-id="de1b1-182">Put double quotation marks around the key to work around this problem--unless the forward slash is the first character.</span></span> <span data-ttu-id="de1b1-183">Se è il primo carattere, usare la modalità interattiva e immettere la password separatamente oppure rigenerare le chiavi per ottenere una chiave che non inizi con una barra.</span><span class="sxs-lookup"><span data-stu-id="de1b1-183">If it is, either use the interactive mode and enter your password separately or regenerate your keys to get a key that doesn't start with a forward slash.</span></span>

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a><span data-ttu-id="de1b1-184">L'applicazione o il servizio non può accedere a un'unità di archiviazione file di Azure montata</span><span class="sxs-lookup"><span data-stu-id="de1b1-184">Application or service cannot access a mounted Azure File storage drive</span></span>

### <a name="cause"></a><span data-ttu-id="de1b1-185">Causa</span><span class="sxs-lookup"><span data-stu-id="de1b1-185">Cause</span></span>

<span data-ttu-id="de1b1-186">Le unità vengono montate per utente.</span><span class="sxs-lookup"><span data-stu-id="de1b1-186">Drives are mounted per user.</span></span> <span data-ttu-id="de1b1-187">Se l'applicazione o il servizio viene eseguito con un account utente diverso da quello che ha montato l'unità, l'unità non sarà visibile.</span><span class="sxs-lookup"><span data-stu-id="de1b1-187">If your application or service is running under a different user account than the one that mounted the drive, the application will not see the drive.</span></span>

### <a name="solution"></a><span data-ttu-id="de1b1-188">Soluzione</span><span class="sxs-lookup"><span data-stu-id="de1b1-188">Solution</span></span>

<span data-ttu-id="de1b1-189">Usare una delle soluzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="de1b1-189">Use one of the following solutions:</span></span>

-   <span data-ttu-id="de1b1-190">Montare l'unità dallo stesso account utente che contiene l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="de1b1-190">Mount the drive from the same user account that contains the application.</span></span> <span data-ttu-id="de1b1-191">Si può usare uno strumento come PsExec.</span><span class="sxs-lookup"><span data-stu-id="de1b1-191">You can use a tool such as PsExec.</span></span>
- <span data-ttu-id="de1b1-192">Passare il nome e la chiave dell'account di archiviazione nei parametri di nome utente e password del comando net use.</span><span class="sxs-lookup"><span data-stu-id="de1b1-192">Pass the storage account name and key in the user name and password parameters of the net use command.</span></span>

<span data-ttu-id="de1b1-193">Dopo aver seguito le istruzioni, è possibile che venga visualizzato il messaggio di errore seguente quando si esegue net use per l'account del servizio di sistema/rete: "Errore di sistema 1312.</span><span class="sxs-lookup"><span data-stu-id="de1b1-193">After you follow these instructions, you might receive the following error message when you run net use for the system/network service account: "System error 1312 has occurred.</span></span> <span data-ttu-id="de1b1-194">Una sessione di accesso specificata non esiste.</span><span class="sxs-lookup"><span data-stu-id="de1b1-194">A specified logon session does not exist.</span></span> <span data-ttu-id="de1b1-195">Potrebbe essere già stata terminata."</span><span class="sxs-lookup"><span data-stu-id="de1b1-195">It may already have been terminated."</span></span> <span data-ttu-id="de1b1-196">In questo caso, assicurarsi che il nome utente passato a net use includa informazioni di dominio (ad esempio: "[nome account archiviazione].file.core.windows.net").</span><span class="sxs-lookup"><span data-stu-id="de1b1-196">If this occurs, make sure that the username that is passed to net use includes domain information (for example: "[storage account name].file.core.windows.net").</span></span>

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-to-a-destination-that-does-not-support-encryption"></a><span data-ttu-id="de1b1-197">Errore "You are copying a file to a destination that does not support encryption" (La destinazione in cui si sta copiando il file non supporta la crittografia)</span><span class="sxs-lookup"><span data-stu-id="de1b1-197">Error "You are copying a file to a destination that does not support encryption"</span></span>

<span data-ttu-id="de1b1-198">Quando un file viene copiato tramite la rete, viene decrittografato nel computer di origine, trasmesso in testo non crittografato e crittografato nuovamente nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="de1b1-198">When a file is copied over the network, the file is decrypted on the source computer, transmitted in plaintext, and re-encrypted at the destination.</span></span> <span data-ttu-id="de1b1-199">Tuttavia, quando si prova a copiare un file crittografato potrebbe essere visualizzato l'errore seguente: "La destinazione in cui si sta copiando il file non supporta la crittografia."</span><span class="sxs-lookup"><span data-stu-id="de1b1-199">However, you might see the following error when you're trying to copy an encrypted file: "You are copying the file to a destination that does not support encryption."</span></span>

### <a name="cause"></a><span data-ttu-id="de1b1-200">Causa</span><span class="sxs-lookup"><span data-stu-id="de1b1-200">Cause</span></span>
<span data-ttu-id="de1b1-201">Questo problema può verificarsi se si usa EFS (Encrypting File System).</span><span class="sxs-lookup"><span data-stu-id="de1b1-201">This problem can occur if you are using Encrypting File System (EFS).</span></span> <span data-ttu-id="de1b1-202">I file crittografati con BitLocker possono essere copiati nell'archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="de1b1-202">BitLocker-encrypted files can be copied to Azure File storage.</span></span> <span data-ttu-id="de1b1-203">Tuttavia, l'archiviazione file di Azure non supporta NTFS EFS.</span><span class="sxs-lookup"><span data-stu-id="de1b1-203">However, Azure File storage does not support NTFS EFS.</span></span>

### <a name="workaround"></a><span data-ttu-id="de1b1-204">Soluzione alternativa</span><span class="sxs-lookup"><span data-stu-id="de1b1-204">Workaround</span></span>
<span data-ttu-id="de1b1-205">Per copiare un file tramite rete, è necessario prima decrittografarlo.</span><span class="sxs-lookup"><span data-stu-id="de1b1-205">To copy a file over the network, you must first decrypt it.</span></span> <span data-ttu-id="de1b1-206">Usare uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="de1b1-206">Use one of the following methods:</span></span>

- <span data-ttu-id="de1b1-207">Usare il comando **copy /d**.</span><span class="sxs-lookup"><span data-stu-id="de1b1-207">Use the **copy /d** command.</span></span> <span data-ttu-id="de1b1-208">Questo consente di salvare i file crittografati come file decrittografati nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="de1b1-208">It allows the encrypted files to be saved as decrypted files at the destination.</span></span>
- <span data-ttu-id="de1b1-209">Impostare la chiave del Registro di sistema seguente:</span><span class="sxs-lookup"><span data-stu-id="de1b1-209">Set the following registry key:</span></span>
  - <span data-ttu-id="de1b1-210">Percorso = HKLM\Software\Policies\Microsoft\Windows\System</span><span class="sxs-lookup"><span data-stu-id="de1b1-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span></span>
  - <span data-ttu-id="de1b1-211">Tipo valore = DWORD</span><span class="sxs-lookup"><span data-stu-id="de1b1-211">Value type = DWORD</span></span>
  - <span data-ttu-id="de1b1-212">Nome = CopyFileAllowDecryptedRemoteDestination</span><span class="sxs-lookup"><span data-stu-id="de1b1-212">Name = CopyFileAllowDecryptedRemoteDestination</span></span>
  - <span data-ttu-id="de1b1-213">Valore = 1</span><span class="sxs-lookup"><span data-stu-id="de1b1-213">Value = 1</span></span>

<span data-ttu-id="de1b1-214">Si noti che l'impostazione della chiave del Registro di sistema influisce su tutte le operazioni di copia eseguite nelle condivisioni di rete.</span><span class="sxs-lookup"><span data-stu-id="de1b1-214">Be aware that setting the registry key affects all copy operations that are made to network shares.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="de1b1-215">Richiesta di assistenza</span><span class="sxs-lookup"><span data-stu-id="de1b1-215">Need help?</span></span> <span data-ttu-id="de1b1-216">Contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="de1b1-216">Contact support.</span></span>
<span data-ttu-id="de1b1-217">Se si necessita ancora di assistenza, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) per ottenere una rapida risoluzione del problema.</span><span class="sxs-lookup"><span data-stu-id="de1b1-217">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your problem resolved quickly.</span></span>
