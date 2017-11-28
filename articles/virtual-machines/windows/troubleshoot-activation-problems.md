---
title: problemi di attivazione aaaTroubleshoot Windows macchina virtuale in Azure | Documenti Microsoft
description: Fornisce hello risolvere i passaggi per la risoluzione dei problemi di attivazione di Windows macchina virtuale in Azure
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 4ebdac66166e80dcd68cd9e2931b30a29ac01eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a><span data-ttu-id="f4500-103">Risolvere i problemi di attivazione della macchina virtuale Windows di Azure</span><span class="sxs-lookup"><span data-stu-id="f4500-103">Troubleshoot Azure Windows virtual machine activation problems</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="f4500-104">Se si verificano problemi durante l'attivazione della macchina virtuale Windows Azure (VM) che viene creato da un'immagine personalizzata, è possibile utilizzare le informazioni di hello fornite in questo numero di documento tootroubleshoot hello.</span><span class="sxs-lookup"><span data-stu-id="f4500-104">If you have trouble when activating Azure Windows virtual machine (VM) that is created from a custom image, you can use hello information provided in this document tootroubleshoot hello issue.</span></span> 

## <a name="symptom"></a><span data-ttu-id="f4500-105">Sintomo</span><span class="sxs-lookup"><span data-stu-id="f4500-105">Symptom</span></span>

<span data-ttu-id="f4500-106">Quando si tenta di tooactivate una macchina virtuale Windows Azure, viene visualizzato un errore simile a quello riportato hello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="f4500-106">When you try tooactivate an Azure Windows VM, you receive an error message resembles hello following sample:</span></span>

<span data-ttu-id="f4500-107">**Errore: hello 0xC004F074 LicensingService Software segnalato che non è possibile attivare i computer hello. Impossibile contattare un servizio di gestione delle chiavi. Vedere hello registro eventi dell'applicazione per ulteriori informazioni.**</span><span class="sxs-lookup"><span data-stu-id="f4500-107">**Error: 0xC004F074 hello Software LicensingService reported that hello computer could not be activated. No Key ManagementService (KMS) could be contacted. Please see hello Application Event Log for additional information.**</span></span>

## <a name="cause"></a><span data-ttu-id="f4500-108">Causa</span><span class="sxs-lookup"><span data-stu-id="f4500-108">Cause</span></span>
<span data-ttu-id="f4500-109">In genere, i problemi di attivazione di macchina virtuale di Azure verificano se hello macchina virtuale di Windows non è configurata per utilizzando hello chiave di configurazione client KMS appropriato, o macchina virtuale di Windows hello è un toohello problema di connettività del servizio di gestione delle CHIAVI di Azure (kms.core.windows.net, porta 1668).</span><span class="sxs-lookup"><span data-stu-id="f4500-109">Generally, Azure VM activation issues occur if hello Windows VM is not configured by using hello appropriate KMS client setup key, or hello Windows VM has a connectivity problem toohello Azure KMS service (kms.core.windows.net, port 1668).</span></span> 

## <a name="solution"></a><span data-ttu-id="f4500-110">Soluzione</span><span class="sxs-lookup"><span data-stu-id="f4500-110">Solution</span></span>

>[!NOTE]
><span data-ttu-id="f4500-111">Se si utilizza una VPN da sito a sito e, tunneling forzato vedere [utilizzare Azure personalizzato instrada tooenable KMS activation con il tunneling forzato](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4500-111">If you are using a site-to-site VPN and forced tunneling, see [Use Azure custom routes tooenable KMS activation with forced tunneling](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx).</span></span> 
>
><span data-ttu-id="f4500-112">Se si usa ExpressRoute e dispone di una route predefinita pubblicati, vedere [macchina virtuale di Azure potrebbe non riuscire tooactivate expressroute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4500-112">If you are using ExpressRoute and you have a default route published, see [Azure VM may fail tooactivate over ExpressRoute](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx).</span></span>

### <a name="step-1-configure-hello-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a><span data-ttu-id="f4500-113">Passaggio 1 Configura hello KMS client setup chiave appropriata (per Windows Server 2016 e Windows Server 2012 R2)</span><span class="sxs-lookup"><span data-stu-id="f4500-113">Step 1 Configure hello appropriate KMS client setup key (for Windows Server 2016 and Windows Server 2012 R2)</span></span>

<span data-ttu-id="f4500-114">Per hello macchina virtuale creata da un'immagine personalizzata di Windows Server 2016 o Windows Server 2012 R2, è necessario configurare hello KMS client setup chiave appropriata per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f4500-114">For hello VM that is created from a custom image of Windows Server 2016 or Windows Server 2012 R2, you must configure hello appropriate KMS client setup key for hello VM.</span></span>

<span data-ttu-id="f4500-115">Questo passaggio non è applicabile tooWindows 2012 o Windows 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="f4500-115">This step does not apply tooWindows 2012 or Windows 2008 R2.</span></span> <span data-ttu-id="f4500-116">Usa la funzionalità di automazione macchina virtuale di attivazione hello, che è supportata solo in Windows Server 2016 e Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="f4500-116">It uses hello Automation Virtual Machine Activation (AVMA) feature, which is supported only by Windows Server 2016 and Windows Server 2012 R2.</span></span>

1. <span data-ttu-id="f4500-117">Eseguire **slmgr.vbs /dlv** in un prompt dei comandi con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="f4500-117">Run **slmgr.vbs /dlv** at an elevated command prompt.</span></span> <span data-ttu-id="f4500-118">Controllare il valore di descrizione nell'output di hello hello e quindi determinare se è stato creato da (canale di vendita al dettaglio) delle vendite al dettaglio o un supporto licenza volume (VOLUME_KMSCLIENT):</span><span class="sxs-lookup"><span data-stu-id="f4500-118">Check hello Description value in hello output, and then determine whether it was created from retail (RETAIL channel) or volume (VOLUME_KMSCLIENT) license media:</span></span>
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. <span data-ttu-id="f4500-119">Se **slmgr.vbs /dlv** Mostra canale di vendita al dettaglio, eseguire hello seguente hello tooset comandi [chiave di configurazione client KMS](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) per la versione di hello del Server di Windows in uso e forza tooretry attivazione:</span><span class="sxs-lookup"><span data-stu-id="f4500-119">If **slmgr.vbs /dlv** shows RETAIL channel, run hello following commands tooset hello [KMS client setup key](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) for hello version of Windows Server being used, and force it tooretry activation:</span></span> 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    <span data-ttu-id="f4500-120">Ad esempio, per Data Center di Windows Server 2016, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f4500-120">For example, for Windows Server 2016 Datacenter, you would run hello following command:</span></span>

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-hello-connectivity-between-hello-vm-and-azure-kms-service"></a><span data-ttu-id="f4500-121">Passaggio 2 verificare la connettività hello tra hello macchina virtuale e servizio di gestione delle CHIAVI di Azure</span><span class="sxs-lookup"><span data-stu-id="f4500-121">Step 2 Verify hello connectivity between hello VM and Azure KMS service</span></span>

1. <span data-ttu-id="f4500-122">Scaricare ed estrarre hello [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) strumento tooa locale cartella hello macchina virtuale che non attiva.</span><span class="sxs-lookup"><span data-stu-id="f4500-122">Download and extract hello [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) tool tooa local folder in hello VM that does not activate.</span></span> 

2. <span data-ttu-id="f4500-123">Passare tooStart, eseguire una ricerca in Windows PowerShell, fare doppio clic su Windows PowerShell e quindi scegliere Esegui come amministratore.</span><span class="sxs-lookup"><span data-stu-id="f4500-123">Go tooStart, search on Windows PowerShell, right-click Windows PowerShell, and then select Run as administrator.</span></span>

3. <span data-ttu-id="f4500-124">Verificare che tale hello che macchina virtuale è configurata server di gestione delle CHIAVI di Azure toouse hello corretto.</span><span class="sxs-lookup"><span data-stu-id="f4500-124">Make sure that hello VM is configured toouse hello correct Azure KMS server.</span></span> <span data-ttu-id="f4500-125">toodo questa operazione, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f4500-125">toodo this, run the following command:</span></span>
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    <span data-ttu-id="f4500-126">comando Hello deve restituire: nome computer del servizio di gestione chiave imposta tookms.core.windows.net:1688 correttamente.</span><span class="sxs-lookup"><span data-stu-id="f4500-126">hello command should return: Key Management Service machine name set tookms.core.windows.net:1688 successfully.</span></span>

4. <span data-ttu-id="f4500-127">Verificare tramite Psping che si disponga della connettività toohello KMS server.</span><span class="sxs-lookup"><span data-stu-id="f4500-127">Verify by using Psping that you have connectivity toohello KMS server.</span></span> <span data-ttu-id="f4500-128">Passare toohello cartella in cui è stato estratto download Pstools.zip hello e quindi eseguire hello seguente:</span><span class="sxs-lookup"><span data-stu-id="f4500-128">Switch toohello folder where you extracted hello Pstools.zip download, and then run hello following:</span></span>
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  <span data-ttu-id="f4500-129">Nella riga di secondo penultima hello dell'output di hello, verificare che sia visualizzato: inviati = 4, ricevuti = 4, Lost = 0 (0% persi).</span><span class="sxs-lookup"><span data-stu-id="f4500-129">In hello second-to-last line of hello output, make sure that you see: Sent = 4, Received = 4, Lost = 0 (0% loss).</span></span>

  <span data-ttu-id="f4500-130">Se Lost è maggiore di 0 (zero), hello macchina virtuale non dispone di server di gestione delle CHIAVI toohello di connettività.</span><span class="sxs-lookup"><span data-stu-id="f4500-130">If Lost is greater than 0 (zero), hello VM does not have connectivity toohello KMS server.</span></span> <span data-ttu-id="f4500-131">In questo caso, se hello macchina virtuale si trova in una rete virtuale e dispone di un server DNS personalizzato, è necessario assicurarsi che il server DNS è in grado di tooresolve kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="f4500-131">In this situation, if hello VM is in a virtual network and has a custom DNS server specified, you must make sure that DNS server is able tooresolve kms.core.windows.net.</span></span> <span data-ttu-id="f4500-132">In alternativa, è possibile modificare hello DNS server tooone risolti kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="f4500-132">Or, change hello DNS server tooone that does resolve kms.core.windows.net.</span></span>

  <span data-ttu-id="f4500-133">Tenere presente che, se si rimuovono tutti i server DNS da una rete virtuale, le VM usano il servizio DNS interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="f4500-133">Notice that if you remove all DNS servers from a virtual network, VMs use Azure’s internal DNS service.</span></span> <span data-ttu-id="f4500-134">Questo servizio può risolvere kms.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="f4500-134">This service can resolve kms.core.windows.net.</span></span>
  
<span data-ttu-id="f4500-135">Verificare inoltre che il firewall hello guest non è stato configurato in modo che blocca i tentativi di attivazione.</span><span class="sxs-lookup"><span data-stu-id="f4500-135">Also verify that hello guest firewall has not been configured in a manner that would block activation attempts.</span></span>

5. <span data-ttu-id="f4500-136">Dopo aver verificato la connettività tookms.core.windows.net, eseguire hello seguente comando al prompt Windows PowerShell con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="f4500-136">After you verify successful connectivity tookms.core.windows.net, run hello following command at that elevated Windows PowerShell prompt.</span></span> <span data-ttu-id="f4500-137">Questo comando tenta l'attivazione più volte.</span><span class="sxs-lookup"><span data-stu-id="f4500-137">This command tries activation multiple times.</span></span>

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

<span data-ttu-id="f4500-138">L'attivazione restituisce informazioni che è simile al seguente hello:</span><span class="sxs-lookup"><span data-stu-id="f4500-138">A successful activation returns information that resembles hello following:</span></span>

<span data-ttu-id="f4500-139">**Attivazione di Windows(R), Server Datacenter Edition (12345678-1234-1234-1234-12345678) in corso… Attivazione prodotto completata.**</span><span class="sxs-lookup"><span data-stu-id="f4500-139">**Activating Windows(R), ServerDatacenter edition (12345678-1234-1234-1234-12345678) … Product activated successfully.**</span></span>

## <a name="faq"></a><span data-ttu-id="f4500-140">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="f4500-140">FAQ</span></span> 

### <a name="i-created-hello-windows-server-2016-from-azure-marketplace-do-i-need-tooconfigure-kms-key-for-activating-hello-windows-server-2016"></a><span data-ttu-id="f4500-141">Hello Windows Server 2016 è stata creata da Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f4500-141">I created hello Windows Server 2016 from Azure Marketplace.</span></span> <span data-ttu-id="f4500-142">È necessario tooconfigure codice Product key per l'attivazione di Windows Server 2016 hello?</span><span class="sxs-lookup"><span data-stu-id="f4500-142">Do I need tooconfigure KMS key for activating hello Windows Server 2016?</span></span> 
 
<span data-ttu-id="f4500-143">No.</span><span class="sxs-lookup"><span data-stu-id="f4500-143">No.</span></span> <span data-ttu-id="f4500-144">immagine di Hello in Azure Marketplace è hello KMS client setup chiave appropriata già configurato.</span><span class="sxs-lookup"><span data-stu-id="f4500-144">hello image in Azure Marketplace has hello appropriate KMS client setup key already configured.</span></span> 

### <a name="does-windows-activation-work-hello-same-way-regardless-if-hello-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a><span data-ttu-id="f4500-145">Lavoro attivazione di Windows hello stesso modo indipendentemente dal se hello VM utilizza Azure ibrida utilizzare vantaggio (HUB) o non?</span><span class="sxs-lookup"><span data-stu-id="f4500-145">Does Windows activation work hello same way regardless if hello VM is using Azure Hybrid Use Benefit (HUB) or not?</span></span> 
 
<span data-ttu-id="f4500-146">Sì.</span><span class="sxs-lookup"><span data-stu-id="f4500-146">Yes.</span></span> 
 
### <a name="what-happens-if-windows-activation-period-expires"></a><span data-ttu-id="f4500-147">Che cosa succede se il periodo di attivazione di Windows scade?</span><span class="sxs-lookup"><span data-stu-id="f4500-147">What happens if Windows activation period expires?</span></span> 
 
<span data-ttu-id="f4500-148">Se è scaduto il periodo di tolleranza hello e ancora non è attivato Windows, Windows Server 2008 R2 e versioni successive di Windows mostrerà ulteriori notifiche sull'attivazione.</span><span class="sxs-lookup"><span data-stu-id="f4500-148">When hello grace period has expired and Windows is still not activated, Windows Server 2008 R2 and later versions of Windows will show additional notifications about activating.</span></span> <span data-ttu-id="f4500-149">sfondo del desktop Hello rimane nero e Windows Update installerà sicurezza e gli aggiornamenti critici, ma gli aggiornamenti non è facoltativi.</span><span class="sxs-lookup"><span data-stu-id="f4500-149">hello desktop wallpaper remains black, and Windows Update will install security and critical updates only, but not optional updates.</span></span> <span data-ttu-id="f4500-150">Vedere le notifiche di hello hello ultima sezione di hello [condizioni di licenza](http://technet.microsoft.com/en-us/library/ff793403.aspx) pagina.</span><span class="sxs-lookup"><span data-stu-id="f4500-150">See  hello Notifications section at hello bottom of hello [Licensing Conditions](http://technet.microsoft.com/en-us/library/ff793403.aspx) page.</span></span>   

## <a name="need-help-contact-support"></a><span data-ttu-id="f4500-151">Richiesta di assistenza</span><span class="sxs-lookup"><span data-stu-id="f4500-151">Need help?</span></span> <span data-ttu-id="f4500-152">Contattare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="f4500-152">Contact support.</span></span>
<span data-ttu-id="f4500-153">Se è ancora necessario della Guida, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget risolta il problema.</span><span class="sxs-lookup"><span data-stu-id="f4500-153">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
