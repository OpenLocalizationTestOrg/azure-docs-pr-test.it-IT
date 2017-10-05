---
title: Ispezione dei pacchetti con Azure Network Watcher | Microsoft Docs
description: Questo articolo descrive come usare Network Watcher per eseguire un'ispezione approfondita dei pacchetti raccolti da una VM
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b907d00-9c35-40f5-a61e-beb7b782276f
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 91c47bb8922a9be21dff72e7cf64b29b14a36e9e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a><span data-ttu-id="557be-103">Ispezione dei pacchetti con Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="557be-103">Packet inspection with Azure Network Watcher</span></span>

<span data-ttu-id="557be-104">Usando la funzionalità di acquisizione di pacchetti di Network Watcher, è possibile avviare e gestire sessioni di acquisizioni nelle VM di Azure dal portale, da PowerShell, dall'interfaccia della riga di comando e a livello di codice tramite l'SDK e l'API REST.</span><span class="sxs-lookup"><span data-stu-id="557be-104">Using the packet capture feature of Network Watcher, you can initiate and manage captures sessions on your Azure VMs from the portal, PowerShell, CLI, and programmatically through the SDK and REST API.</span></span> <span data-ttu-id="557be-105">L'acquisizione di pacchetti consente di gestire scenari in cui sono necessari dati a livello di pacchetto fornendo le informazioni in un formato subito utilizzabile.</span><span class="sxs-lookup"><span data-stu-id="557be-105">Packet capture allows you to address scenarios that require packet level data by providing the information in a readily usable format.</span></span> <span data-ttu-id="557be-106">Sfruttando gli strumenti disponibili gratuitamente per ispezionare i dati, è possibile esaminare le comunicazioni inviate alle e dalle VM e ottenere informazioni dettagliate sul traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="557be-106">Leveraging freely available tools to inspect the data, you can examine communications sent to and from your VMs and gain insights into your network traffic.</span></span> <span data-ttu-id="557be-107">Alcuni esempi di uso dei dati di acquisizione di pacchetti includono: esame dei problemi della rete o delle applicazioni, rilevamento dell'uso improprio della rete e dei tentativi di intrusione o gestione della conformità alle normative.</span><span class="sxs-lookup"><span data-stu-id="557be-107">Some example uses of packet capture data include: investigating network or application issues, detecting network misuse and intrusion attempts, or maintaining regulatory compliance.</span></span> <span data-ttu-id="557be-108">In questo articolo viene illustrato come aprire un file di acquisizione di pacchetti fornito da Network Watcher usando un diffuso strumento open source.</span><span class="sxs-lookup"><span data-stu-id="557be-108">In this article, we show how to open a packet capture file provided by Network Watcher using a popular open source tool.</span></span> <span data-ttu-id="557be-109">Verranno anche forniti esempi che illustrano come calcolare la latenza di una connessione, identificare il traffico anomalo ed esaminare le statistiche di rete.</span><span class="sxs-lookup"><span data-stu-id="557be-109">We will also provide examples showing how to calculate a connection latency, identify abnormal traffic, and examine networking statistics.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="557be-110">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="557be-110">Before you begin</span></span>

<span data-ttu-id="557be-111">Questo articolo descrive alcuni scenari preconfigurati in un'acquisizione di pacchetti eseguita prima.</span><span class="sxs-lookup"><span data-stu-id="557be-111">This article goes through some pre-configured scenarios on a packet capture that was run previously.</span></span> <span data-ttu-id="557be-112">Gli scenari esaminano un'acquisizione di pacchetti per illustrare le funzionalità accessibili.</span><span class="sxs-lookup"><span data-stu-id="557be-112">These scenarios illustrate capabilities that can be accessed by reviewing a packet capture.</span></span> <span data-ttu-id="557be-113">Questo scenario usa [WireShark](https://www.wireshark.org/) per ispezionare l'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="557be-113">This scenario uses [WireShark](https://www.wireshark.org/) to inspect the packet capture.</span></span>

<span data-ttu-id="557be-114">Questo scenario presume che sia già stata eseguita un'acquisizione di pacchetti in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="557be-114">This scenario assumes you already ran a packet capture on a virtual machine.</span></span> <span data-ttu-id="557be-115">Per informazioni su come creare un'acquisizione di pacchetti, vedere [Manage packet captures with the portal](network-watcher-packet-capture-manage-portal.md) (Gestire le acquisizioni di pacchetti con il portale) o [Managing Packet Captures with REST API](network-watcher-packet-capture-manage-rest.md) (Gestione di acquisizioni di pacchetti con l'API REST).</span><span class="sxs-lookup"><span data-stu-id="557be-115">To learn how to create a packet capture visit [Manage packet captures with the portal](network-watcher-packet-capture-manage-portal.md) or with REST by visiting [Managing Packet Captures with REST API](network-watcher-packet-capture-manage-rest.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="557be-116">Scenario</span><span class="sxs-lookup"><span data-stu-id="557be-116">Scenario</span></span>

<span data-ttu-id="557be-117">In questo scenario:</span><span class="sxs-lookup"><span data-stu-id="557be-117">In this scenario, you:</span></span>

* <span data-ttu-id="557be-118">Si esamina un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="557be-118">Review a packet capture</span></span>

## <a name="calculate-network-latency"></a><span data-ttu-id="557be-119">Calcolare la latenza di rete</span><span class="sxs-lookup"><span data-stu-id="557be-119">Calculate network latency</span></span>

<span data-ttu-id="557be-120">In questo scenario viene illustrato come visualizzare il tempo di round trip (RTT, Round Trip Time) di una conversazione TCP (Transmission Control Protocol) che avviene tra due endpoint.</span><span class="sxs-lookup"><span data-stu-id="557be-120">In this scenario, we show how to view the initial Round Trip Time (RTT) of a Transmission Control Protocol (TCP) conversation occurring between two endpoints.</span></span>

<span data-ttu-id="557be-121">Quando viene stabilita una connessione TCP, i primi tre pacchetti inviati nella connessione seguono un modello chiamato in genere handshake a tre livelli.</span><span class="sxs-lookup"><span data-stu-id="557be-121">When a TCP connection is established, the first three packets sent in the connection follow a pattern commonly referred to as the three-way handshake.</span></span> <span data-ttu-id="557be-122">Esaminando i primi due pacchetti inviati in questo handshake, una richiesta iniziale dal client e una risposta dal server, è possibile calcolare la latenza quando questa connessione viene stabilita.</span><span class="sxs-lookup"><span data-stu-id="557be-122">By examining the first two packets sent in this handshake, an initial request from the client and a response from the server, we can calculate the latency when this connection was established.</span></span> <span data-ttu-id="557be-123">Questa latenza è chiamata tempo di round trip.</span><span class="sxs-lookup"><span data-stu-id="557be-123">This latency is referred to as the Round Trip Time (RTT).</span></span> <span data-ttu-id="557be-124">Per altre informazioni sul protocollo TCP e l'handshake a tre livelli, vedere la risorsa seguente.</span><span class="sxs-lookup"><span data-stu-id="557be-124">For more information on the TCP protocol and the three-way handshake refer to the following resource.</span></span> <span data-ttu-id="557be-125">https://support.microsoft.com/it-it/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span><span class="sxs-lookup"><span data-stu-id="557be-125">https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span></span>

### <a name="step-1"></a><span data-ttu-id="557be-126">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="557be-126">Step 1</span></span>

<span data-ttu-id="557be-127">Avviare WireShark</span><span class="sxs-lookup"><span data-stu-id="557be-127">Launch WireShark</span></span>

### <a name="step-2"></a><span data-ttu-id="557be-128">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="557be-128">Step 2</span></span>

<span data-ttu-id="557be-129">Caricare il file con estensione **cap** dall'acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="557be-129">Load the **.cap** file from your packet capture.</span></span> <span data-ttu-id="557be-130">Questo file si trova nel BLOB se è stato salvato in locale nella macchina virtuale, a seconda della configurazione eseguita.</span><span class="sxs-lookup"><span data-stu-id="557be-130">This file can be found in the blob it was saved in our locally on the virtual machine, depending on how you configured it.</span></span>

### <a name="step-3"></a><span data-ttu-id="557be-131">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="557be-131">Step 3</span></span>

<span data-ttu-id="557be-132">Per visualizzare il tempo di round trip iniziale nelle conversazioni TCP, verranno esaminati solo i primi due pacchetti coinvolti nell'handshake TCP.</span><span class="sxs-lookup"><span data-stu-id="557be-132">To view the initial Round Trip Time (RTT) in TCP conversations, we will only be looking at the first two packets involved in the TCP handshake.</span></span> <span data-ttu-id="557be-133">Nell'handshake a tre livelli verranno usati i primi due pacchetti, ovvero [SYN] e [SYN, ACK].</span><span class="sxs-lookup"><span data-stu-id="557be-133">We will be using the first two packets in the three-way handshake, which are the [SYN], [SYN, ACK] packets.</span></span> <span data-ttu-id="557be-134">Il nome deriva dai flag impostati nell'intestazione TCP.</span><span class="sxs-lookup"><span data-stu-id="557be-134">They are named for flags set in the TCP header.</span></span> <span data-ttu-id="557be-135">L'ultimo pacchetto nell'handshake, il pacchetto [ACK], non verrà usato in questo scenario.</span><span class="sxs-lookup"><span data-stu-id="557be-135">The last packet in the handshake, the [ACK] packet, will not be used in this scenario.</span></span> <span data-ttu-id="557be-136">Il pacchetto [SYN] viene inviato dal client.</span><span class="sxs-lookup"><span data-stu-id="557be-136">The [SYN] packet is sent by the client.</span></span> <span data-ttu-id="557be-137">Dopo che è stato ricevuto, il server invia il pacchetto [ACK] come acknowledgement della ricezione di SYN dal client.</span><span class="sxs-lookup"><span data-stu-id="557be-137">Once it is received the server sends the [ACK] packet as an acknowledgement of receiving the SYN from the client.</span></span> <span data-ttu-id="557be-138">Sfruttando il fatto che la risposta del server richiede un overhead molto basso, il tempo RTT viene calcolato sottraendo dall'ora in cui il pacchetto [SYN, ACK] è stato ricevuto dal client l'ora in cui il pacchetto [SYN] è stato inviato dal client.</span><span class="sxs-lookup"><span data-stu-id="557be-138">Leveraging the fact that the server’s response requires very little overhead, we calculate the RTT by subtracting the time the [SYN, ACK] packet was received by the client by the time [SYN] packet was sent by the client.</span></span>

<span data-ttu-id="557be-139">Usando WireShark questo valore viene calcolato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="557be-139">Using WireShark this value is calculated for us.</span></span>

<span data-ttu-id="557be-140">Per visualizzare più facilmente i primi due pacchetti nell'handshake a tre livelli TCP, verrà utilizzata la funzionalità di filtro di WireShark.</span><span class="sxs-lookup"><span data-stu-id="557be-140">To more easily view the first two packets in the TCP three-way handshake, we will utilize the filtering capability provided by WireShark.</span></span>

<span data-ttu-id="557be-141">Per applicare il filtro in WireShark, espandere il segmento "Transmission Control Protocol" di un pacchetto [SYN] nell'acquisizione ed esaminare i flag impostati nell'intestazione TCP.</span><span class="sxs-lookup"><span data-stu-id="557be-141">To apply the filter in WireShark, expand the “Transmission Control Protocol” Segment of a [SYN] packet in your capture and examine the flags set in the TCP header.</span></span>

<span data-ttu-id="557be-142">Poiché si vogliono filtrare i pacchetti [SYN] e [SYN, ACK], nei flag seguenti verificare che il bit Syn sia impostato su 1, quindi fare clic con il pulsante destro del mouse sul bit Syn -> Apply as Filter (Applica come filtro) -> Selezionato.</span><span class="sxs-lookup"><span data-stu-id="557be-142">Since we are looking to filter on all [SYN] and [SYN, ACK] packets, under flags cofirm that the Syn bit is set to 1, then right click on the Syn bit -> Apply as Filter -> Selected.</span></span>

![Figura 7][7]

### <a name="step-4"></a><span data-ttu-id="557be-144">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="557be-144">Step 4</span></span>

<span data-ttu-id="557be-145">Dopo avere filtrato la finestra per visualizzare solo i pacchetti con il bit [SYN] impostato, è possibile selezionare facilmente le conversazioni a cui si è interessati per visualizzare il tempo RTT iniziale.</span><span class="sxs-lookup"><span data-stu-id="557be-145">Now that you have filtered the window to only see packets with the [SYN] bit set, you can easily select conversations you are interested in to view the initial RTT.</span></span> <span data-ttu-id="557be-146">Per visualizzare facilmente il tempo RTT in WireShark, è sufficiente fare clic sul menu a discesa dell'analisi "SEQ/ACK".</span><span class="sxs-lookup"><span data-stu-id="557be-146">A simple way to view the RTT in WireShark simply click the dropdown marked “SEQ/ACK” analysis.</span></span> <span data-ttu-id="557be-147">Verrà quindi visualizzato il tempo RTT.</span><span class="sxs-lookup"><span data-stu-id="557be-147">You will then see the RTT displayed.</span></span> <span data-ttu-id="557be-148">In questo caso, il tempo RTT era 0,0022114 secondi o 2,211 ms.</span><span class="sxs-lookup"><span data-stu-id="557be-148">In this case, the RTT was 0.0022114 seconds, or 2.211 ms.</span></span>

![Figura 8][8]

## <a name="unwanted-protocols"></a><span data-ttu-id="557be-150">Protocolli indesiderati</span><span class="sxs-lookup"><span data-stu-id="557be-150">Unwanted protocols</span></span>

<span data-ttu-id="557be-151">In un'istanza di una macchina virtuale distribuita in Azure potrebbero essere in esecuzione più applicazioni.</span><span class="sxs-lookup"><span data-stu-id="557be-151">You can have many applications running on a virtual machine instance you have deployed in Azure.</span></span> <span data-ttu-id="557be-152">Molte di queste applicazioni comunicano in rete, a volte senza esplicita autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="557be-152">Many of these applications communicate over the network, perhaps without your explicit permission.</span></span> <span data-ttu-id="557be-153">Usando l'acquisizione di pacchetti per archiviare la comunicazione di rete, è possibile esaminare come le applicazioni comunicano in rete e cercare eventuali problemi.</span><span class="sxs-lookup"><span data-stu-id="557be-153">Using packet capture to store network communication, we can investigate how application are talking on the network and look for any issues.</span></span>

<span data-ttu-id="557be-154">In questo esempio viene esaminata un'acquisizione di pacchetti già eseguita per trovare protocolli indesiderati che potrebbero indicare una comunicazione non autorizzata da un'applicazione in esecuzione nel computer.</span><span class="sxs-lookup"><span data-stu-id="557be-154">In this example, we review a previous ran packet capture for unwanted protocols that may indicate unauthorized communication from an application running on your machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="557be-155">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="557be-155">Step 1</span></span>

<span data-ttu-id="557be-156">Usando la stessa acquisizione dello scenario precedente, fare clic su **Statistics** (Statistiche) > **Protocol Hierarchy** (Gerarchia protocolli)</span><span class="sxs-lookup"><span data-stu-id="557be-156">Using the same capture in the previous scenario click **Statistics** > **Protocol Hierarchy**</span></span>

![Menu Protocol Hierarchy (Gerarchia protocolli)][2]

<span data-ttu-id="557be-158">Verrà visualizzata la finestra della gerarchia dei protocolli.</span><span class="sxs-lookup"><span data-stu-id="557be-158">The protocol hierarchy window appears.</span></span> <span data-ttu-id="557be-159">Questa visualizzazione fornisce un elenco di tutti i protocolli usati durante la sessione di acquisizione e il numero di pacchetti trasmessi e ricevuti usando i protocolli.</span><span class="sxs-lookup"><span data-stu-id="557be-159">This view provides a list of all the protocols that were in use during the capture session and the number of packets transmitted and received using the protocols.</span></span> <span data-ttu-id="557be-160">Si tratta di una visualizzazione utile per trovare il traffico di rete indesiderato nelle macchine virtuali o in rete.</span><span class="sxs-lookup"><span data-stu-id="557be-160">This view can be useful for finding unwanted network traffic on your virtual machines or network.</span></span>

![Gerarchia dei protocolli aperta][3]

<span data-ttu-id="557be-162">Come si può osservare nell'acquisizione della schermata seguente, parte del traffico usava il protocollo BitTorrent, che viene usato per la condivisione di file peer-to-peer.</span><span class="sxs-lookup"><span data-stu-id="557be-162">As you can see in the following screen capture, there was traffic using the BitTorrent protocol, which is used for peer to peer file sharing.</span></span> <span data-ttu-id="557be-163">Un amministratore non si aspetta di trovare traffico BitTorrent in queste particolari macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="557be-163">As an administrator you do not expect to see BitTorrent traffic on this particular virtual machines.</span></span> <span data-ttu-id="557be-164">Dopo avere trovato questo tipo di traffico, è possibile rimuovere il software peer-to-peer installato in questa macchina virtuale o bloccare il traffico usando i gruppi di sicurezza di rete o un firewall.</span><span class="sxs-lookup"><span data-stu-id="557be-164">Now you aware of this traffic, you can remove the peer to peer software that installed on this virtual machine, or block the traffic using Network Security Groups or a Firewall.</span></span> <span data-ttu-id="557be-165">È anche possibile scegliere di eseguire le acquisizioni di pacchetti in base a una pianificazione per poter esaminare periodicamente l'uso del protocollo nelle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="557be-165">Additionally, you may elect to run packet captures on a schedule, so you can review the protocol use on your virtual machines regularly.</span></span> <span data-ttu-id="557be-166">Per un esempio di come automatizzare le attività di rete in Azure, vedere [Monitor network resources with azure automation](network-watcher-monitor-with-azure-automation.md) (Monitorare le risorse di rete con Automazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="557be-166">For an example on how to automate network tasks in azure visit [Monitor network resources with azure automation](network-watcher-monitor-with-azure-automation.md)</span></span>

## <a name="finding-top-destinations-and-ports"></a><span data-ttu-id="557be-167">Ricerca di porte e destinazioni principali</span><span class="sxs-lookup"><span data-stu-id="557be-167">Finding top destinations and ports</span></span>

<span data-ttu-id="557be-168">Conoscere i tipi di traffico, gli endpoint e le porte attraverso cui avviene la comunicazione è importante quando si monitorano o si risolvono i problemi delle applicazioni e delle risorse nella rete.</span><span class="sxs-lookup"><span data-stu-id="557be-168">Understanding the types of traffic, the endpoints, and the ports communicated over is an important when monitoring or troubleshooting applications and resources on your network.</span></span> <span data-ttu-id="557be-169">Utilizzando un file di acquisizione di pacchetti già usato, è possibile conoscere rapidamente le destinazioni principali con cui comunica la VM e le porte utilizzate.</span><span class="sxs-lookup"><span data-stu-id="557be-169">Utilizing a packet capture file from above, we can quickly learn the top destinations our VM is communicating with and the ports being utilized.</span></span>

### <a name="step-1"></a><span data-ttu-id="557be-170">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="557be-170">Step 1</span></span>

<span data-ttu-id="557be-171">Usando la stessa acquisizione dello scenario precedente, fare clic su **Statistics** (Statistiche) > **IPv4 Statistics** (Statistiche IPv4) > **Destinations and Ports** (Destinazioni e porte)</span><span class="sxs-lookup"><span data-stu-id="557be-171">Using the same capture in the previous scenario click **Statistics** > **IPv4 Statistics** > **Destinations and Ports**</span></span>

![Finestra di acquisizione di pacchetti][4]

### <a name="step-2"></a><span data-ttu-id="557be-173">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="557be-173">Step 2</span></span>

<span data-ttu-id="557be-174">Tra i risultati si nota una riga in cui sono presenti più connessioni alla porta 111.</span><span class="sxs-lookup"><span data-stu-id="557be-174">As we look through the results a line stands out, there were multiple connections on port 111.</span></span> <span data-ttu-id="557be-175">La porta più usata è la 3389, che è un desktop remoto. Le altre sono porte dinamiche RPC.</span><span class="sxs-lookup"><span data-stu-id="557be-175">The most used port was 3389, which is remote desktop, and the remaining are RPC dynamic ports.</span></span>

<span data-ttu-id="557be-176">Anche se questo traffico può non essere significativo, la porta è però stata usata per diverse connessioni ed è sconosciuta all'amministratore.</span><span class="sxs-lookup"><span data-stu-id="557be-176">While this traffic may mean nothing, it is a port that was used for many connections and is unknown to the administrator.</span></span>

![Figura 5][5]

### <a name="step-3"></a><span data-ttu-id="557be-178">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="557be-178">Step 3</span></span>

<span data-ttu-id="557be-179">Dopo avere trovato una porta anomala, è possibile filtrare l'acquisizione in base alla porta.</span><span class="sxs-lookup"><span data-stu-id="557be-179">Now that we have determined an out of place port we can filter our capture based on the port.</span></span>

<span data-ttu-id="557be-180">Il filtro in questo scenario sarà:</span><span class="sxs-lookup"><span data-stu-id="557be-180">The filter in this scenario would be:</span></span>

```
tcp.port == 111
```

<span data-ttu-id="557be-181">Si immette il testo del filtro precedente nella casella di testo del filtro e si preme INVIO.</span><span class="sxs-lookup"><span data-stu-id="557be-181">We enter the filter text from above in the filter textbox and hit enter.</span></span>

![Figura 6][6]

<span data-ttu-id="557be-183">Dai risultati è possibile osservare che tutto il traffico proviene da una macchina virtuale locale nella stessa subnet.</span><span class="sxs-lookup"><span data-stu-id="557be-183">From the results, we can see all the traffic is coming from a local virtual machine on the same subnet.</span></span> <span data-ttu-id="557be-184">Se l'origine di questo traffico non è ancora evidente, è possibile ispezionare meglio i pacchetti per determinare perché vengono eseguite queste chiamate sulla porta 111.</span><span class="sxs-lookup"><span data-stu-id="557be-184">If we still don’t understand why this traffic is occurring, we can further inspect the packets to determine why it is making these calls on port 111.</span></span> <span data-ttu-id="557be-185">Con queste informazioni è possibile eseguire l'azione appropriata.</span><span class="sxs-lookup"><span data-stu-id="557be-185">With this information we can take the appropriate action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="557be-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="557be-186">Next steps</span></span>

<span data-ttu-id="557be-187">Per informazioni sulle altre funzionalità di diagnostica di Network Watcher, vedere [Azure network monitoring overview](network-watcher-monitoring-overview.md) (Panoramica del monitoraggio della rete di Azure)</span><span class="sxs-lookup"><span data-stu-id="557be-187">Learn about the other diagnostic features of Network Watcher by visiting [Azure network monitoring overview](network-watcher-monitoring-overview.md)</span></span>

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













