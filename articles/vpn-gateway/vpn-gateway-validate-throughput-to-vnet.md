---
title: "Convalidare la velocità effettiva VPN tooa rete virtuale di Microsoft Azure | Documenti Microsoft"
description: "scopo di questo documento Hello è toohelp velocità effettiva della rete hello da loro tooan risorse locali macchina virtuale di Azure di convalidare un utente."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: jasmc
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/10/2017
ms.author: radwiv;chadmat;genli
ms.openlocfilehash: 9cf0b67145645a3c2a9556b0cc910066cc62a9ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a><span data-ttu-id="d19aa-103">La rete virtuale tooa toovalidate VPN velocità effettiva</span><span class="sxs-lookup"><span data-stu-id="d19aa-103">How toovalidate VPN throughput tooa virtual network</span></span>

<span data-ttu-id="d19aa-104">Una connessione gateway VPN consente connettività cross-premise sicura, tooestablish tra la rete virtuale in Azure e locale infrastruttura IT.</span><span class="sxs-lookup"><span data-stu-id="d19aa-104">A VPN gateway connection enables you tooestablish secure, cross-premises connectivity between your Virtual Network within Azure and your on-premises IT infrastructure.</span></span>

<span data-ttu-id="d19aa-105">Questo articolo illustra come velocità effettiva della rete toovalidate da hello locale tooan risorse macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d19aa-105">This article shows how toovalidate network throughput from hello on-premises resources tooan Azure virtual machine.</span></span> <span data-ttu-id="d19aa-106">Fornisce inoltre informazioni aggiuntive sulla risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="d19aa-106">It also provides troubleshooting guidance.</span></span>

>[!NOTE]
><span data-ttu-id="d19aa-107">Questo articolo è dedicato toohelp diagnosticare e risolvere i problemi comuni.</span><span class="sxs-lookup"><span data-stu-id="d19aa-107">This article is intended toohelp diagnose and fix common issues.</span></span> <span data-ttu-id="d19aa-108">Se si problema hello toosolve Impossibile utilizzando le seguenti informazioni, hello [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="d19aa-108">If you're unable toosolve hello issue by using hello following information, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="d19aa-109">Panoramica</span><span class="sxs-lookup"><span data-stu-id="d19aa-109">Overview</span></span>

<span data-ttu-id="d19aa-110">connessione del gateway VPN Hello prevede hello seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="d19aa-110">hello VPN gateway connection involves hello following components:</span></span>

- <span data-ttu-id="d19aa-111">Dispositivo VPN locale (visualizzare un elenco di [dispositivi VPN convalidati](vpn-gateway-about-vpn-devices.md#devicetable)).</span><span class="sxs-lookup"><span data-stu-id="d19aa-111">On-premises VPN device (view a list of [validated VPN devices)](vpn-gateway-about-vpn-devices.md#devicetable).</span></span>
- <span data-ttu-id="d19aa-112">Internet pubblico</span><span class="sxs-lookup"><span data-stu-id="d19aa-112">Public Internet</span></span>
- <span data-ttu-id="d19aa-113">Gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="d19aa-113">Azure VPN gateway</span></span>
- <span data-ttu-id="d19aa-114">Macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="d19aa-114">Azure virtual machine</span></span>

<span data-ttu-id="d19aa-115">Hello seguente diagramma mostra la connettività logico hello di un tooan di rete locale rete virtuale di Azure tramite VPN.</span><span class="sxs-lookup"><span data-stu-id="d19aa-115">hello following diagram shows hello logical connectivity of an on-premises network tooan Azure virtual network through VPN.</span></span>

![Logica della connettività di rete del cliente tooMSFT rete tramite la VPN](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a><span data-ttu-id="d19aa-117">Calcolare hello massimo previsto in ingresso e uscita</span><span class="sxs-lookup"><span data-stu-id="d19aa-117">Calculate hello maximum expected ingress/egress</span></span>

1.  <span data-ttu-id="d19aa-118">Determinare i requisiti di velocità effettiva di base dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d19aa-118">Determine your application's baseline throughput requirements.</span></span>
2.  <span data-ttu-id="d19aa-119">Determinare i limiti di velocità effettiva del gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="d19aa-119">Determine your Azure VPN gateway throughput limits.</span></span> <span data-ttu-id="d19aa-120">Per informazioni, vedere la sezione hello "velocità effettiva aggregata dal tipo SKU e VPN" di [pianificazione e progettazione per il Gateway VPN](vpn-gateway-plan-design.md).</span><span class="sxs-lookup"><span data-stu-id="d19aa-120">For help, see hello "Aggregate throughput by SKU and VPN type" section of [Planning and design for VPN Gateway](vpn-gateway-plan-design.md).</span></span>
3.  <span data-ttu-id="d19aa-121">Determinare hello [indicazioni di velocità effettiva di macchina virtuale di Azure](../virtual-machines/virtual-machines-windows-sizes.md) per la dimensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d19aa-121">Determine hello [Azure VM throughput guidance](../virtual-machines/virtual-machines-windows-sizes.md) for your VM size.</span></span>
4.  <span data-ttu-id="d19aa-122">Determinare la larghezza di banda del provider di servizi Internet (ISP).</span><span class="sxs-lookup"><span data-stu-id="d19aa-122">Determine your Internet Service Provider (ISP) bandwidth.</span></span>
5.  <span data-ttu-id="d19aa-123">Eseguire il calcolo di velocità effettiva prevista - larghezza di banda minima di (macchina virtuale, gateway, ISP) * 0,8.</span><span class="sxs-lookup"><span data-stu-id="d19aa-123">Calculate your expected throughput - Least bandwidth of (VM, Gateway, ISP) * 0.8.</span></span>

<span data-ttu-id="d19aa-124">Se la velocità effettiva di calcolato non soddisfa i requisiti di velocità effettiva della linea di base dell'applicazione, è necessario tooincrease della larghezza di banda hello della risorsa hello identificato come collo di bottiglia hello.</span><span class="sxs-lookup"><span data-stu-id="d19aa-124">If your calculated throughput does not meet your application's baseline throughput requirements, you need tooincrease hello bandwidth of hello resource that you identified as hello bottleneck.</span></span> <span data-ttu-id="d19aa-125">tooresize un Gateway VPN di Azure, vedere [la modifica di un gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="d19aa-125">tooresize an Azure VPN Gateway, see [Changing a gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="d19aa-126">tooresize una macchina virtuale, vedere [ridimensiona una macchina virtuale](../virtual-machines/virtual-machines-windows-resize-vm.md).</span><span class="sxs-lookup"><span data-stu-id="d19aa-126">tooresize a virtual machine, see [Resize a VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span></span> <span data-ttu-id="d19aa-127">Se non si verificano previsto della larghezza di banda Internet, è inoltre possibile toocontact provider di servizi Internet.</span><span class="sxs-lookup"><span data-stu-id="d19aa-127">If you are not experiencing expected Internet bandwidth, you may also want toocontact your ISP.</span></span>

## <a name="validate-network-throughput-by-using-performance-tools"></a><span data-ttu-id="d19aa-128">Convalidare la velocità effettiva della rete mediante gli strumenti di prestazioni</span><span class="sxs-lookup"><span data-stu-id="d19aa-128">Validate network throughput by using performance tools</span></span>

<span data-ttu-id="d19aa-129">È consigliabile eseguire questa convalida al di fuori delle ore di punta, poiché la saturazione della velocità effettiva del tunnel VPN durante il test non fornisce risultati accurati.</span><span class="sxs-lookup"><span data-stu-id="d19aa-129">This validation should be performed during non-peak hours, as VPN tunnel throughput saturation during testing does not give accurate results.</span></span>

<span data-ttu-id="d19aa-130">lo strumento di Hello che viene usato per questo test è iPerf, che funziona in Windows e Linux e le modalità client e server.</span><span class="sxs-lookup"><span data-stu-id="d19aa-130">hello tool we use for this test is iPerf, which works on both Windows and Linux and has both client and server modes.</span></span> <span data-ttu-id="d19aa-131">È limitato too3 Gbps per macchine virtuali di Windows.</span><span class="sxs-lookup"><span data-stu-id="d19aa-131">It is limited too3 Gbps for Windows VMs.</span></span>

<span data-ttu-id="d19aa-132">Questo strumento non esegue qualsiasi toodisk di operazioni di lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="d19aa-132">This tool does not perform any read/write operations toodisk.</span></span> <span data-ttu-id="d19aa-133">Produce solo il traffico TCP generato automaticamente da un fine toohello altri.</span><span class="sxs-lookup"><span data-stu-id="d19aa-133">It solely produces self-generated TCP traffic from one end toohello other.</span></span> <span data-ttu-id="d19aa-134">Il metodo generato statistiche in base a sperimentazione che misura hello della larghezza di banda disponibile tra i nodi di client e server.</span><span class="sxs-lookup"><span data-stu-id="d19aa-134">It generated statistics based on experimentation that measures hello bandwidth available between client and server nodes.</span></span> <span data-ttu-id="d19aa-135">Durante il test tra due nodi, uno funge da server hello e hello altri come client.</span><span class="sxs-lookup"><span data-stu-id="d19aa-135">When testing between two nodes, one acts as hello server and hello other as a client.</span></span> <span data-ttu-id="d19aa-136">Una volta completato il test, è consigliabile che non è invertire hello ruoli tootest entrambi caricare e scaricare la velocità effettiva in entrambi i nodi.</span><span class="sxs-lookup"><span data-stu-id="d19aa-136">Once this test is completed, we recommend that you reverse hello roles tootest both upload and download throughput on both nodes.</span></span>

### <a name="download-iperf"></a><span data-ttu-id="d19aa-137">Scaricare iPerf</span><span class="sxs-lookup"><span data-stu-id="d19aa-137">Download iPerf</span></span>
<span data-ttu-id="d19aa-138">Eseguire il download di [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span><span class="sxs-lookup"><span data-stu-id="d19aa-138">Download [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span></span> <span data-ttu-id="d19aa-139">Per dettagli, vedere la [documentazione di iPerf](https://iperf.fr/iperf-doc.php).</span><span class="sxs-lookup"><span data-stu-id="d19aa-139">For details, see [iPerf documentation](https://iperf.fr/iperf-doc.php).</span></span>

 >[!NOTE]
 ><span data-ttu-id="d19aa-140">Hello terze parti citati in questo articolo prodotti da aziende indipendenti da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d19aa-140">hello third-party products that this article discusses are manufactured by companies that are independent of Microsoft.</span></span> <span data-ttu-id="d19aa-141">Microsoft non fornisce alcuna garanzia, implicita o esplicita, sulle prestazioni di hello o all'affidabilità di questi prodotti.</span><span class="sxs-lookup"><span data-stu-id="d19aa-141">Microsoft makes no warranty, implied or otherwise, about hello performance or reliability of these products.</span></span>
 >
 >

### <a name="run-iperf-iperf3exe"></a><span data-ttu-id="d19aa-142">Eseguire iPerf (iperf3.exe)</span><span class="sxs-lookup"><span data-stu-id="d19aa-142">Run iPerf (iperf3.exe)</span></span>
1. <span data-ttu-id="d19aa-143">Abilitare una regola ACL di NSG/consenta il traffico di hello (per l'indirizzo IP pubblico test nella macchina virtuale di Azure).</span><span class="sxs-lookup"><span data-stu-id="d19aa-143">Enable an NSG/ACL rule allowing hello traffic (for public IP address testing on Azure VM).</span></span>

2. <span data-ttu-id="d19aa-144">In entrambi i nodi abilitare un'eccezione firewall per la porta 5001.</span><span class="sxs-lookup"><span data-stu-id="d19aa-144">On both nodes, enable a firewall exception for port 5001.</span></span>

    <span data-ttu-id="d19aa-145">**Windows:** comando che segue hello di Esegui come amministratore:</span><span class="sxs-lookup"><span data-stu-id="d19aa-145">**Windows:** Run hello following command as an administrator:</span></span>

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    <span data-ttu-id="d19aa-146">regola di hello tooremove durante il test è stata completata, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="d19aa-146">tooremove hello rule when testing is complete, run this command:</span></span>

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    <span data-ttu-id="d19aa-147">**Linux di Azure**: le immagini Linux di Azure dispongono di firewall permissivi.</span><span class="sxs-lookup"><span data-stu-id="d19aa-147">**Azure Linux:**  Azure Linux images have permissive firewalls.</span></span> <span data-ttu-id="d19aa-148">Se è presente un'applicazione in attesa su una porta, è consentito il traffico hello attraverso.</span><span class="sxs-lookup"><span data-stu-id="d19aa-148">If there is an application listening on a port, hello traffic is allowed through.</span></span> <span data-ttu-id="d19aa-149">Per le immagini personalizzate protette potrebbero essere necessarie porte aperte in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="d19aa-149">Custom images that are secured may need ports opened explicitly.</span></span> <span data-ttu-id="d19aa-150">Firewall a livello di sistema operativo Linux comuni includono `iptables`, `ufw` o `firewalld`.</span><span class="sxs-lookup"><span data-stu-id="d19aa-150">Common Linux OS-layer firewalls include `iptables`, `ufw`, or `firewalld`.</span></span>

3. <span data-ttu-id="d19aa-151">Nel nodo server hello modificare toohello directory in cui viene estratto iperf3.exe.</span><span class="sxs-lookup"><span data-stu-id="d19aa-151">On hello server node, change toohello directory where iperf3.exe is extracted.</span></span> <span data-ttu-id="d19aa-152">Quindi eseguire iPerf in modalità server e impostare toolisten sulla porta 5001 come hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="d19aa-152">Then run iPerf in server mode and set it toolisten on port 5001 as hello following commands:</span></span>

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. <span data-ttu-id="d19aa-153">Nel nodo client hello, modificare toohello directory in cui iperf strumento verrà estratti e quindi eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d19aa-153">On hello client node, change toohello directory where iperf tool is extracted and then run hello following command:</span></span>

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    <span data-ttu-id="d19aa-154">client hello è la generazione di traffico in porta 5001 toohello server per 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="d19aa-154">hello client is inducing traffic on port 5001 toohello server for 30 seconds.</span></span> <span data-ttu-id="d19aa-155">Hello flag '-P ' indicante che si sono usando 32 nodi server toohello di connessioni simultanee.</span><span class="sxs-lookup"><span data-stu-id="d19aa-155">hello flag '-P ' that indicates we are using 32 simultaneous connections toohello server node.</span></span>

    <span data-ttu-id="d19aa-156">Hello seguente schermata Mostra output di hello di questo esempio:</span><span class="sxs-lookup"><span data-stu-id="d19aa-156">hello following screen shows hello output from this example:</span></span>

    ![Output](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. <span data-ttu-id="d19aa-158">(Facoltativo) toopreserve hello test risultati, eseguiti questo comando:</span><span class="sxs-lookup"><span data-stu-id="d19aa-158">(OPTIONAL) toopreserve hello testing results, run this command:</span></span>

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. <span data-ttu-id="d19aa-159">Dopo aver completato i passaggi precedenti hello, eseguire hello stessi passaggi con i ruoli di hello invertiti, in modo che hello nodo server sarà client hello e viceversa.</span><span class="sxs-lookup"><span data-stu-id="d19aa-159">After completing hello previous steps, execute hello same steps with hello roles reversed, so that hello server node will now be hello client and vice-versa.</span></span>

## <a name="address-slow-file-copy-issues"></a><span data-ttu-id="d19aa-160">Risolvere i problemi di esecuzione lenta della copia dei file</span><span class="sxs-lookup"><span data-stu-id="d19aa-160">Address slow file copy issues</span></span>
<span data-ttu-id="d19aa-161">È possibile che la copia dei file venga eseguita lentamente quando si usa Esplora risorse o il trascinamento della selezione tramite una sessione RDP.</span><span class="sxs-lookup"><span data-stu-id="d19aa-161">You may experience slow file coping when using Windows Explorer or dragging and dropping through an RDP session.</span></span> <span data-ttu-id="d19aa-162">Questo problema è in genere a causa di tooone o entrambi hello seguenti fattori:</span><span class="sxs-lookup"><span data-stu-id="d19aa-162">This problem is normally due tooone or both of hello following factors:</span></span>

- <span data-ttu-id="d19aa-163">Le applicazioni di copia dei file, ad esempio Esplora risorse e RDP, non usano più thread durante la copia dei file.</span><span class="sxs-lookup"><span data-stu-id="d19aa-163">File copy applications, such as Windows Explorer and RDP, do not use multiple threads when copying files.</span></span> <span data-ttu-id="d19aa-164">Per ottenere prestazioni migliori, utilizzare un'applicazione di copia di file a thread multipli, ad esempio [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) file toocopy con 16 o 32 thread.</span><span class="sxs-lookup"><span data-stu-id="d19aa-164">For better performance, use a multi-threaded file copy application such as [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy files by using 16 or 32 threads.</span></span> <span data-ttu-id="d19aa-165">numero di thread hello toochange per la copia dei file in Richcopy, fare clic su **azione** > **opzioni Copia** > **copia del File**.</span><span class="sxs-lookup"><span data-stu-id="d19aa-165">toochange hello thread number for file copy in Richcopy, click **Action** > **Copy options** > **File copy**.</span></span><br><br><span data-ttu-id="d19aa-166">
![Problemi di esecuzione lenta della copia dei file](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span><span class="sxs-lookup"><span data-stu-id="d19aa-166">
![Slow file copy issues](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span></span><br>
- <span data-ttu-id="d19aa-167">Velocità di lettura/scrittura disco macchina virtuale insufficiente.</span><span class="sxs-lookup"><span data-stu-id="d19aa-167">Insufficient VM disk read/write speed.</span></span> <span data-ttu-id="d19aa-168">Per altre informazioni, vedere [Risoluzione dei problemi di Archiviazione di Azure](../storage/common/storage-e2e-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="d19aa-168">For more information, see [Azure Storage Troubleshooting](../storage/common/storage-e2e-troubleshooting.md).</span></span>

## <a name="on-premises-device-external-facing-interface"></a><span data-ttu-id="d19aa-169">Interfaccia con connessione rivolta all'esterno del dispositivo locale</span><span class="sxs-lookup"><span data-stu-id="d19aa-169">On-premises device external facing interface</span></span>
<span data-ttu-id="d19aa-170">Se hello in locale il dispositivo VPN indirizzo IP con connessione Internet è incluso in hello [rete locale](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definizione in Azure, potrebbero verificarsi toobring impossibilità hello disconnette VPN, sporadici errori o problemi di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="d19aa-170">If hello on-premises VPN device Internet-facing IP address is included in hello [local network](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definition in Azure, you may experience inability toobring up hello VPN, sporadic disconnects, or performance issues.</span></span>

## <a name="checking-latency"></a><span data-ttu-id="d19aa-171">Verifica della latenza</span><span class="sxs-lookup"><span data-stu-id="d19aa-171">Checking latency</span></span>
<span data-ttu-id="d19aa-172">Utilizzare tracert tootrace tooMicrosoft bordo Azure dispositivo toodetermine se sono presenti eventuali ritardi superiore a 100 ms tra hop.</span><span class="sxs-lookup"><span data-stu-id="d19aa-172">Use tracert tootrace tooMicrosoft Azure Edge device toodetermine if there are any delays exceeding 100 ms between hops.</span></span>

<span data-ttu-id="d19aa-173">Esecuzione dalla rete locale hello, *tracert* toohello VIP di hello Azure Gateway o la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d19aa-173">From hello on-premises network, run *tracert* toohello VIP of hello Azure Gateway or VM.</span></span> <span data-ttu-id="d19aa-174">Dopo aver visualizzato solo * restituito, si conosce è stato raggiunto hello Azure edge.</span><span class="sxs-lookup"><span data-stu-id="d19aa-174">Once you see only * returned, you know you have reached hello Azure edge.</span></span> <span data-ttu-id="d19aa-175">Quando vengono visualizzati i nomi DNS che includono "MSN" restituito, si conosce che è stato raggiunto il backbone Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="d19aa-175">When you see DNS names that include "MSN" returned, you know you have reached hello Microsoft backbone.</span></span><br><br><span data-ttu-id="d19aa-176">
![Controllo della latenza](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span><span class="sxs-lookup"><span data-stu-id="d19aa-176">
![Checking Latency](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d19aa-177">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d19aa-177">Next steps</span></span>
<span data-ttu-id="d19aa-178">Per ulteriori informazioni o assistenza, vedere hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="d19aa-178">For more information or help, check out hello following links:</span></span>

- [<span data-ttu-id="d19aa-179">Ottimizzare la velocità effettiva di rete per le macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="d19aa-179">Optimize network throughput for Azure virtual machines</span></span>](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [<span data-ttu-id="d19aa-180">Supporto tecnico Microsoft</span><span class="sxs-lookup"><span data-stu-id="d19aa-180">Microsoft Support</span></span>](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
