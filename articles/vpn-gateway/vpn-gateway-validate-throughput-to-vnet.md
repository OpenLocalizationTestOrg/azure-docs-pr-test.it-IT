---
title: "Convalidare la velocità effettiva della VPN verso una rete virtuale di Microsoft Azure | Microsoft Docs"
description: "Lo scopo di questo documento è quello di consentire a un utente di convalidare la velocità effettiva della rete dalle relative risorse locali a una macchina virtuale di Azure."
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
ms.openlocfilehash: 2e0347854b5d30c955a50a01d6f7ba08e24f94b6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-validate-vpn-throughput-to-a-virtual-network"></a><span data-ttu-id="9da11-103">Come convalidare la velocità effettiva della VPN verso una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="9da11-103">How to validate VPN throughput to a virtual network</span></span>

<span data-ttu-id="9da11-104">Una connessione del gateway VPN consente di stabilire una connettività cross-premise sicura tra la rete virtuale in Azure e l'infrastruttura IT locale.</span><span class="sxs-lookup"><span data-stu-id="9da11-104">A VPN gateway connection enables you to establish secure, cross-premises connectivity between your Virtual Network within Azure and your on-premises IT infrastructure.</span></span>

<span data-ttu-id="9da11-105">Questo articolo descrive come convalidare la velocità effettiva della rete dalle risorse locali a una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9da11-105">This article shows how to validate network throughput from the on-premises resources to an Azure virtual machine.</span></span> <span data-ttu-id="9da11-106">Fornisce inoltre informazioni aggiuntive sulla risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="9da11-106">It also provides troubleshooting guidance.</span></span>

>[!NOTE]
><span data-ttu-id="9da11-107">Questo articolo ha lo scopo di semplificare la diagnosi e la risoluzione dei problemi comuni.</span><span class="sxs-lookup"><span data-stu-id="9da11-107">This article is intended to help diagnose and fix common issues.</span></span> <span data-ttu-id="9da11-108">Se non si riesce a risolvere il problema tramite le informazioni seguenti, [contattare il supporto tecnico](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="9da11-108">If you're unable to solve the issue by using the following information, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="9da11-109">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9da11-109">Overview</span></span>

<span data-ttu-id="9da11-110">La connessione del gateway VPN coinvolge i componenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="9da11-110">The VPN gateway connection involves the following components:</span></span>

- <span data-ttu-id="9da11-111">Dispositivo VPN locale (visualizzare un elenco di [dispositivi VPN convalidati](vpn-gateway-about-vpn-devices.md#devicetable)).</span><span class="sxs-lookup"><span data-stu-id="9da11-111">On-premises VPN device (view a list of [validated VPN devices)](vpn-gateway-about-vpn-devices.md#devicetable).</span></span>
- <span data-ttu-id="9da11-112">Internet pubblico</span><span class="sxs-lookup"><span data-stu-id="9da11-112">Public Internet</span></span>
- <span data-ttu-id="9da11-113">Gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="9da11-113">Azure VPN gateway</span></span>
- <span data-ttu-id="9da11-114">Macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="9da11-114">Azure virtual machine</span></span>

<span data-ttu-id="9da11-115">Il diagramma seguente mostra la connettività logica di una rete locale a una rete virtuale di Azure tramite VPN.</span><span class="sxs-lookup"><span data-stu-id="9da11-115">The following diagram shows the logical connectivity of an on-premises network to an Azure virtual network through VPN.</span></span>

![Connettività logica della rete del cliente alla rete MSFT tramite VPN](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-the-maximum-expected-ingressegress"></a><span data-ttu-id="9da11-117">Calcolare il traffico in ingresso/in uscita massimo previsto</span><span class="sxs-lookup"><span data-stu-id="9da11-117">Calculate the maximum expected ingress/egress</span></span>

1.  <span data-ttu-id="9da11-118">Determinare i requisiti di velocità effettiva di base dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9da11-118">Determine your application's baseline throughput requirements.</span></span>
2.  <span data-ttu-id="9da11-119">Determinare i limiti di velocità effettiva del gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="9da11-119">Determine your Azure VPN gateway throughput limits.</span></span> <span data-ttu-id="9da11-120">Per altre informazioni, vedere la sezione "Velocità effettiva aggregata stimata per tipo di VPN e SKU" in [Pianificazione e progettazione per il gateway VPN](vpn-gateway-plan-design.md).</span><span class="sxs-lookup"><span data-stu-id="9da11-120">For help, see the "Aggregate throughput by SKU and VPN type" section of [Planning and design for VPN Gateway](vpn-gateway-plan-design.md).</span></span>
3.  <span data-ttu-id="9da11-121">Determinare le [informazioni aggiuntive relative alla velocità effettiva della macchina virtuale di Azure](../virtual-machines/virtual-machines-windows-sizes.md) in base alle dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9da11-121">Determine the [Azure VM throughput guidance](../virtual-machines/virtual-machines-windows-sizes.md) for your VM size.</span></span>
4.  <span data-ttu-id="9da11-122">Determinare la larghezza di banda del provider di servizi Internet (ISP).</span><span class="sxs-lookup"><span data-stu-id="9da11-122">Determine your Internet Service Provider (ISP) bandwidth.</span></span>
5.  <span data-ttu-id="9da11-123">Eseguire il calcolo di velocità effettiva prevista - larghezza di banda minima di (macchina virtuale, gateway, ISP) * 0,8.</span><span class="sxs-lookup"><span data-stu-id="9da11-123">Calculate your expected throughput - Least bandwidth of (VM, Gateway, ISP) * 0.8.</span></span>

<span data-ttu-id="9da11-124">Se la velocità effettiva calcolata non soddisfa i requisiti di velocità effettiva di base dell'applicazione, è necessario aumentare la larghezza di banda della risorsa identificata come collo di bottiglia.</span><span class="sxs-lookup"><span data-stu-id="9da11-124">If your calculated throughput does not meet your application's baseline throughput requirements, you need to increase the bandwidth of the resource that you identified as the bottleneck.</span></span> <span data-ttu-id="9da11-125">Per ridimensionare un gateway VPN di Azure, vedere [Changing a gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku) (Modifica SKU del gateway).</span><span class="sxs-lookup"><span data-stu-id="9da11-125">To resize an Azure VPN Gateway, see [Changing a gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="9da11-126">Per ridimensionare una macchina virtuale, vedere [Ridimensionare una VM ](../virtual-machines/virtual-machines-windows-resize-vm.md).</span><span class="sxs-lookup"><span data-stu-id="9da11-126">To resize a virtual machine, see [Resize a VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span></span> <span data-ttu-id="9da11-127">Se non si dispone della larghezza di banda Internet prevista, è consigliabile anche contattare il provider di servizi Internet.</span><span class="sxs-lookup"><span data-stu-id="9da11-127">If you are not experiencing expected Internet bandwidth, you may also want to contact your ISP.</span></span>

## <a name="validate-network-throughput-by-using-performance-tools"></a><span data-ttu-id="9da11-128">Convalidare la velocità effettiva della rete mediante gli strumenti di prestazioni</span><span class="sxs-lookup"><span data-stu-id="9da11-128">Validate network throughput by using performance tools</span></span>

<span data-ttu-id="9da11-129">È consigliabile eseguire questa convalida al di fuori delle ore di punta, poiché la saturazione della velocità effettiva del tunnel VPN durante il test non fornisce risultati accurati.</span><span class="sxs-lookup"><span data-stu-id="9da11-129">This validation should be performed during non-peak hours, as VPN tunnel throughput saturation during testing does not give accurate results.</span></span>

<span data-ttu-id="9da11-130">Lo strumento usato per questo test è iPerf, che è supportato sia su Windows sia su Linux e dispone di modalità client e server.</span><span class="sxs-lookup"><span data-stu-id="9da11-130">The tool we use for this test is iPerf, which works on both Windows and Linux and has both client and server modes.</span></span> <span data-ttu-id="9da11-131">Per le macchine virtuali di Windows è limitato a 3 Gbps.</span><span class="sxs-lookup"><span data-stu-id="9da11-131">It is limited to 3 Gbps for Windows VMs.</span></span>

<span data-ttu-id="9da11-132">Questo strumento non esegue operazioni di lettura/scrittura su disco,</span><span class="sxs-lookup"><span data-stu-id="9da11-132">This tool does not perform any read/write operations to disk.</span></span> <span data-ttu-id="9da11-133">ma produce solo traffico TCP generato automaticamente da un'entità finale all'altra.</span><span class="sxs-lookup"><span data-stu-id="9da11-133">It solely produces self-generated TCP traffic from one end to the other.</span></span> <span data-ttu-id="9da11-134">Genera statistiche in base alla sperimentazione che misura la larghezza di banda disponibile tra i nodi client e server.</span><span class="sxs-lookup"><span data-stu-id="9da11-134">It generated statistics based on experimentation that measures the bandwidth available between client and server nodes.</span></span> <span data-ttu-id="9da11-135">Durante l'esecuzione del test tra due nodi, uno agisce come server e l'altro come client.</span><span class="sxs-lookup"><span data-stu-id="9da11-135">When testing between two nodes, one acts as the server and the other as a client.</span></span> <span data-ttu-id="9da11-136">Al termine di questo test, è consigliabile invertire i ruoli per testare la velocità effettiva di caricamento e download su entrambi i nodi.</span><span class="sxs-lookup"><span data-stu-id="9da11-136">Once this test is completed, we recommend that you reverse the roles to test both upload and download throughput on both nodes.</span></span>

### <a name="download-iperf"></a><span data-ttu-id="9da11-137">Scaricare iPerf</span><span class="sxs-lookup"><span data-stu-id="9da11-137">Download iPerf</span></span>
<span data-ttu-id="9da11-138">Eseguire il download di [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span><span class="sxs-lookup"><span data-stu-id="9da11-138">Download [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span></span> <span data-ttu-id="9da11-139">Per dettagli, vedere la [documentazione di iPerf](https://iperf.fr/iperf-doc.php).</span><span class="sxs-lookup"><span data-stu-id="9da11-139">For details, see [iPerf documentation](https://iperf.fr/iperf-doc.php).</span></span>

 >[!NOTE]
 ><span data-ttu-id="9da11-140">Gli strumenti di terze parti citati in questo articolo sono prodotti da società indipendenti di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9da11-140">The third-party products that this article discusses are manufactured by companies that are independent of Microsoft.</span></span> <span data-ttu-id="9da11-141">Microsoft non fornisce alcuna garanzia, implicita o esplicita, sulle prestazioni o sull'affidabilità di questi prodotti.</span><span class="sxs-lookup"><span data-stu-id="9da11-141">Microsoft makes no warranty, implied or otherwise, about the performance or reliability of these products.</span></span>
 >
 >

### <a name="run-iperf-iperf3exe"></a><span data-ttu-id="9da11-142">Eseguire iPerf (iperf3.exe)</span><span class="sxs-lookup"><span data-stu-id="9da11-142">Run iPerf (iperf3.exe)</span></span>
1. <span data-ttu-id="9da11-143">Abilitare una regola NSG/ACL che consenta il traffico (per il test dell'indirizzo IP pubblico nella macchina virtuale di Azure).</span><span class="sxs-lookup"><span data-stu-id="9da11-143">Enable an NSG/ACL rule allowing the traffic (for public IP address testing on Azure VM).</span></span>

2. <span data-ttu-id="9da11-144">In entrambi i nodi abilitare un'eccezione firewall per la porta 5001.</span><span class="sxs-lookup"><span data-stu-id="9da11-144">On both nodes, enable a firewall exception for port 5001.</span></span>

    <span data-ttu-id="9da11-145">**Windows:** eseguire questo comando come amministratore.</span><span class="sxs-lookup"><span data-stu-id="9da11-145">**Windows:** Run the following command as an administrator:</span></span>

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    <span data-ttu-id="9da11-146">Per rimuovere la regola al termine del test, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="9da11-146">To remove the rule when testing is complete, run this command:</span></span>

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    <span data-ttu-id="9da11-147">**Linux di Azure**: le immagini Linux di Azure dispongono di firewall permissivi.</span><span class="sxs-lookup"><span data-stu-id="9da11-147">**Azure Linux:**  Azure Linux images have permissive firewalls.</span></span> <span data-ttu-id="9da11-148">Se un'applicazione è in ascolto su una porta, è consentito il passaggio del traffico.</span><span class="sxs-lookup"><span data-stu-id="9da11-148">If there is an application listening on a port, the traffic is allowed through.</span></span> <span data-ttu-id="9da11-149">Per le immagini personalizzate protette potrebbero essere necessarie porte aperte in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="9da11-149">Custom images that are secured may need ports opened explicitly.</span></span> <span data-ttu-id="9da11-150">Firewall a livello di sistema operativo Linux comuni includono `iptables`, `ufw` o `firewalld`.</span><span class="sxs-lookup"><span data-stu-id="9da11-150">Common Linux OS-layer firewalls include `iptables`, `ufw`, or `firewalld`.</span></span>

3. <span data-ttu-id="9da11-151">Sul nodo del server passare alla directory in cui è stato estratto iperf3.exe.</span><span class="sxs-lookup"><span data-stu-id="9da11-151">On the server node, change to the directory where iperf3.exe is extracted.</span></span> <span data-ttu-id="9da11-152">Eseguire quindi iPerf in modalità server e impostarlo per l'ascolto sulla porta 5001, come nei comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9da11-152">Then run iPerf in server mode and set it to listen on port 5001 as the following commands:</span></span>

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. <span data-ttu-id="9da11-153">Nel nodo client passare alla directory in cui è stato estratto lo strumento iperf e quindi eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="9da11-153">On the client node, change to the directory where iperf tool is extracted and then run the following command:</span></span>

    ```CMD
    iperf3.exe -c <IP of the iperf Server> -t 30 -p 5001 -P 32
    ```

    <span data-ttu-id="9da11-154">Il client indirizza il traffico sulla porta 5001 verso il server per 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="9da11-154">The client is inducing traffic on port 5001 to the server for 30 seconds.</span></span> <span data-ttu-id="9da11-155">Il flag '-P ' indica che vengono usate 32 connessioni simultanee per il nodo del server.</span><span class="sxs-lookup"><span data-stu-id="9da11-155">The flag '-P ' that indicates we are using 32 simultaneous connections to the server node.</span></span>

    <span data-ttu-id="9da11-156">La schermata seguente mostra l'output di questo esempio:</span><span class="sxs-lookup"><span data-stu-id="9da11-156">The following screen shows the output from this example:</span></span>

    ![Output](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. <span data-ttu-id="9da11-158">(FACOLTATIVO) Per mantenere i risultati del test, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="9da11-158">(OPTIONAL) To preserve the testing results, run this command:</span></span>

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. <span data-ttu-id="9da11-159">Dopo aver completato i passaggi precedenti, eseguire la stessa procedura con i ruoli invertiti, in modo che il nodo del server sarà il client e viceversa.</span><span class="sxs-lookup"><span data-stu-id="9da11-159">After completing the previous steps, execute the same steps with the roles reversed, so that the server node will now be the client and vice-versa.</span></span>

## <a name="address-slow-file-copy-issues"></a><span data-ttu-id="9da11-160">Risolvere i problemi di esecuzione lenta della copia dei file</span><span class="sxs-lookup"><span data-stu-id="9da11-160">Address slow file copy issues</span></span>
<span data-ttu-id="9da11-161">È possibile che la copia dei file venga eseguita lentamente quando si usa Esplora risorse o il trascinamento della selezione tramite una sessione RDP.</span><span class="sxs-lookup"><span data-stu-id="9da11-161">You may experience slow file coping when using Windows Explorer or dragging and dropping through an RDP session.</span></span> <span data-ttu-id="9da11-162">Questo problema è in genere dovuto a uno o a entrambi i fattori seguenti:</span><span class="sxs-lookup"><span data-stu-id="9da11-162">This problem is normally due to one or both of the following factors:</span></span>

- <span data-ttu-id="9da11-163">Le applicazioni di copia dei file, ad esempio Esplora risorse e RDP, non usano più thread durante la copia dei file.</span><span class="sxs-lookup"><span data-stu-id="9da11-163">File copy applications, such as Windows Explorer and RDP, do not use multiple threads when copying files.</span></span> <span data-ttu-id="9da11-164">Per prestazioni ottimali, usare un'applicazione per la copia dei file multithread, ad esempio [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx), per copiare i file a 16 o 32 thread.</span><span class="sxs-lookup"><span data-stu-id="9da11-164">For better performance, use a multi-threaded file copy application such as [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) to copy files by using 16 or 32 threads.</span></span> <span data-ttu-id="9da11-165">Per modificare il numero di thread per la copia dei file in Richcopy, fare clic su **Azione** > **Opzioni copia** > **Copia dei file**.</span><span class="sxs-lookup"><span data-stu-id="9da11-165">To change the thread number for file copy in Richcopy, click **Action** > **Copy options** > **File copy**.</span></span><br><br><span data-ttu-id="9da11-166">
![Problemi di esecuzione lenta della copia dei file](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span><span class="sxs-lookup"><span data-stu-id="9da11-166">
![Slow file copy issues](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span></span><br>
- <span data-ttu-id="9da11-167">Velocità di lettura/scrittura disco macchina virtuale insufficiente.</span><span class="sxs-lookup"><span data-stu-id="9da11-167">Insufficient VM disk read/write speed.</span></span> <span data-ttu-id="9da11-168">Per altre informazioni, vedere [Risoluzione dei problemi di Archiviazione di Azure](../storage/common/storage-e2e-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="9da11-168">For more information, see [Azure Storage Troubleshooting](../storage/common/storage-e2e-troubleshooting.md).</span></span>

## <a name="on-premises-device-external-facing-interface"></a><span data-ttu-id="9da11-169">Interfaccia con connessione rivolta all'esterno del dispositivo locale</span><span class="sxs-lookup"><span data-stu-id="9da11-169">On-premises device external facing interface</span></span>
<span data-ttu-id="9da11-170">Se l'indirizzo IP per Internet del dispositivo VPN locale è incluso nella definizione della [rete locale](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) in Azure, potrebbe non essere possibile vedere la VPN, potrebbero verificarsi sporadiche disconnessioni o problemi di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="9da11-170">If the on-premises VPN device Internet-facing IP address is included in the [local network](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definition in Azure, you may experience inability to bring up the VPN, sporadic disconnects, or performance issues.</span></span>

## <a name="checking-latency"></a><span data-ttu-id="9da11-171">Verifica della latenza</span><span class="sxs-lookup"><span data-stu-id="9da11-171">Checking latency</span></span>
<span data-ttu-id="9da11-172">Usare tracert per tenere traccia del dispositivo perimetrale di Microsoft Azure per determinare se sono presenti eventuali ritardi con oltre 100 ms tra hop.</span><span class="sxs-lookup"><span data-stu-id="9da11-172">Use tracert to trace to Microsoft Azure Edge device to determine if there are any delays exceeding 100 ms between hops.</span></span>

<span data-ttu-id="9da11-173">Dalla rete locale eseguire *tracert* all'indirizzo VIP del gateway o della macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9da11-173">From the on-premises network, run *tracert* to the VIP of the Azure Gateway or VM.</span></span> <span data-ttu-id="9da11-174">Quando viene restituito solo un asterisco (*), vuol dire che è stato raggiunto il dispositivo periferico di Azure.</span><span class="sxs-lookup"><span data-stu-id="9da11-174">Once you see only * returned, you know you have reached the Azure edge.</span></span> <span data-ttu-id="9da11-175">Quando vengono restituiti nomi DNS che includono "MSN", vuol dire che è stata raggiunta la backbone di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9da11-175">When you see DNS names that include "MSN" returned, you know you have reached the Microsoft backbone.</span></span><br><br><span data-ttu-id="9da11-176">
![Controllo della latenza](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span><span class="sxs-lookup"><span data-stu-id="9da11-176">
![Checking Latency](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="9da11-177">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9da11-177">Next steps</span></span>
<span data-ttu-id="9da11-178">Per maggiori informazioni o assistenza, consultare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="9da11-178">For more information or help, check out the following links:</span></span>

- [<span data-ttu-id="9da11-179">Ottimizzare la velocità effettiva di rete per le macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="9da11-179">Optimize network throughput for Azure virtual machines</span></span>](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [<span data-ttu-id="9da11-180">Supporto tecnico Microsoft</span><span class="sxs-lookup"><span data-stu-id="9da11-180">Microsoft Support</span></span>](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
