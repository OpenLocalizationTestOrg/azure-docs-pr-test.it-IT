---
title: ispezione aaaPacket con Watcher di rete di Azure | Documenti Microsoft
description: In questo articolo viene descritto come toouse analisi approfondita dei pacchetti di rete Watcher tooperform raccolti da una macchina virtuale
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
ms.openlocfilehash: 4aeddcd482edc4df3d63e87b5c4b0788c540850b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a><span data-ttu-id="d5f3d-103">Ispezione dei pacchetti con Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="d5f3d-103">Packet inspection with Azure Network Watcher</span></span>

<span data-ttu-id="d5f3d-104">Utilizza la funzionalità di acquisizione pacchetti hello del controllo di rete, è possibile avviare e gestire le sessioni di acquisizioni su macchine virtuali di Azure dal portale di hello, PowerShell CLI e a livello di programmazione tramite hello SDK e API REST.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-104">Using hello packet capture feature of Network Watcher, you can initiate and manage captures sessions on your Azure VMs from hello portal, PowerShell, CLI, and programmatically through hello SDK and REST API.</span></span> <span data-ttu-id="d5f3d-105">Acquisizione di pacchetti consente tooaddress scenari che richiedono dati a livello di pacchetto, fornendo informazioni hello in un formato facilmente utilizzabile.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-105">Packet capture allows you tooaddress scenarios that require packet level data by providing hello information in a readily usable format.</span></span> <span data-ttu-id="d5f3d-106">Sfruttando i dati di hello tooinspect strumenti liberamente disponibili, è possibile esaminare le comunicazioni inviate tooand dalle macchine virtuali e ottenere informazioni approfondite del traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-106">Leveraging freely available tools tooinspect hello data, you can examine communications sent tooand from your VMs and gain insights into your network traffic.</span></span> <span data-ttu-id="d5f3d-107">Alcuni esempi di uso dei dati di acquisizione di pacchetti includono: esame dei problemi della rete o delle applicazioni, rilevamento dell'uso improprio della rete e dei tentativi di intrusione o gestione della conformità alle normative.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-107">Some example uses of packet capture data include: investigating network or application issues, detecting network misuse and intrusion attempts, or maintaining regulatory compliance.</span></span> <span data-ttu-id="d5f3d-108">In questo articolo viene illustrata come tooopen un file di acquisizione di pacchetti forniti dal controllo di rete utilizzando uno strumento open source comuni.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-108">In this article, we show how tooopen a packet capture file provided by Network Watcher using a popular open source tool.</span></span> <span data-ttu-id="d5f3d-109">Inoltre, Microsoft fornisce esempi che mostrano come toocalculate una latenza della connessione, identificare il traffico anomalo ed esaminare le statistiche di rete.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-109">We will also provide examples showing how toocalculate a connection latency, identify abnormal traffic, and examine networking statistics.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d5f3d-110">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="d5f3d-110">Before you begin</span></span>

<span data-ttu-id="d5f3d-111">Questo articolo descrive alcuni scenari preconfigurati in un'acquisizione di pacchetti eseguita prima.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-111">This article goes through some pre-configured scenarios on a packet capture that was run previously.</span></span> <span data-ttu-id="d5f3d-112">Gli scenari esaminano un'acquisizione di pacchetti per illustrare le funzionalità accessibili.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-112">These scenarios illustrate capabilities that can be accessed by reviewing a packet capture.</span></span> <span data-ttu-id="d5f3d-113">Questo scenario Usa [WireShark](https://www.wireshark.org/) tooinspect acquisizione di pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-113">This scenario uses [WireShark](https://www.wireshark.org/) tooinspect hello packet capture.</span></span>

<span data-ttu-id="d5f3d-114">Questo scenario presume che sia già stata eseguita un'acquisizione di pacchetti in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-114">This scenario assumes you already ran a packet capture on a virtual machine.</span></span> <span data-ttu-id="d5f3d-115">modalità di acquisizione pacchetto eseguita toocreate visitare toolearn [acquisizioni di pacchetti di gestione con il portale di hello](network-watcher-packet-capture-manage-portal.md) o con REST visitando [acquisizioni di pacchetti di gestione con l'API REST](network-watcher-packet-capture-manage-rest.md).</span><span class="sxs-lookup"><span data-stu-id="d5f3d-115">toolearn how toocreate a packet capture visit [Manage packet captures with hello portal](network-watcher-packet-capture-manage-portal.md) or with REST by visiting [Managing Packet Captures with REST API](network-watcher-packet-capture-manage-rest.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="d5f3d-116">Scenario</span><span class="sxs-lookup"><span data-stu-id="d5f3d-116">Scenario</span></span>

<span data-ttu-id="d5f3d-117">In questo scenario:</span><span class="sxs-lookup"><span data-stu-id="d5f3d-117">In this scenario, you:</span></span>

* <span data-ttu-id="d5f3d-118">Si esamina un'acquisizione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="d5f3d-118">Review a packet capture</span></span>

## <a name="calculate-network-latency"></a><span data-ttu-id="d5f3d-119">Calcolare la latenza di rete</span><span class="sxs-lookup"><span data-stu-id="d5f3d-119">Calculate network latency</span></span>

<span data-ttu-id="d5f3d-120">In questo scenario viene illustrata la modalità tooview hello iniziale Round Trip Time (RTT) di una conversazione di protocollo TCP (Transmission Control) che si verificano tra due endpoint.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-120">In this scenario, we show how tooview hello initial Round Trip Time (RTT) of a Transmission Control Protocol (TCP) conversation occurring between two endpoints.</span></span>

<span data-ttu-id="d5f3d-121">Quando viene stabilita una connessione TCP, hello primi tre pacchetti inviati nella connessione hello seguono un handshake a tre vie hello tooas modello conosciuta.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-121">When a TCP connection is established, hello first three packets sent in hello connection follow a pattern commonly referred tooas hello three-way handshake.</span></span> <span data-ttu-id="d5f3d-122">Esaminando i pacchetti hello primi due inviati questo handshake, una richiesta iniziale dal client hello e una risposta dal server hello, è possibile calcolare la latenza di hello quando è stata stabilita la connessione.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-122">By examining hello first two packets sent in this handshake, an initial request from hello client and a response from hello server, we can calculate hello latency when this connection was established.</span></span> <span data-ttu-id="d5f3d-123">Tale latenza è tooas cui hello Round Trip Time (RTT).</span><span class="sxs-lookup"><span data-stu-id="d5f3d-123">This latency is referred tooas hello Round Trip Time (RTT).</span></span> <span data-ttu-id="d5f3d-124">Per ulteriori informazioni sul protocollo TCP hello e handshake a tre vie hello consultare toohello seguente risorsa.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-124">For more information on hello TCP protocol and hello three-way handshake refer toohello following resource.</span></span> <span data-ttu-id="d5f3d-125">https://support.microsoft.com/it-it/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span><span class="sxs-lookup"><span data-stu-id="d5f3d-125">https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span></span>

### <a name="step-1"></a><span data-ttu-id="d5f3d-126">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="d5f3d-126">Step 1</span></span>

<span data-ttu-id="d5f3d-127">Avviare WireShark</span><span class="sxs-lookup"><span data-stu-id="d5f3d-127">Launch WireShark</span></span>

### <a name="step-2"></a><span data-ttu-id="d5f3d-128">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="d5f3d-128">Step 2</span></span>

<span data-ttu-id="d5f3d-129">Hello carico **CAP** file di acquisizione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-129">Load hello **.cap** file from your packet capture.</span></span> <span data-ttu-id="d5f3d-130">Questo file è reperibile nel blob hello è stato salvato nella macchina virtuale di hello localmente nel, a seconda di come è stato configurato.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-130">This file can be found in hello blob it was saved in our locally on hello virtual machine, depending on how you configured it.</span></span>

### <a name="step-3"></a><span data-ttu-id="d5f3d-131">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="d5f3d-131">Step 3</span></span>

<span data-ttu-id="d5f3d-132">tooview hello iniziale Round Trip Time (RTT) nelle conversazioni TCP, verrà letto solo in pacchetti primi due hello coinvolti nell'handshake TCP hello.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-132">tooview hello initial Round Trip Time (RTT) in TCP conversations, we will only be looking at hello first two packets involved in hello TCP handshake.</span></span> <span data-ttu-id="d5f3d-133">Si utilizzerà innanzitutto due i pacchetti hello in handshake a tre vie hello, che sono hello [SYN], [SYN, ACK] pacchetti.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-133">We will be using hello first two packets in hello three-way handshake, which are hello [SYN], [SYN, ACK] packets.</span></span> <span data-ttu-id="d5f3d-134">Hanno un nome per i flag impostati nell'intestazione TCP hello.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-134">They are named for flags set in hello TCP header.</span></span> <span data-ttu-id="d5f3d-135">non Hello ultimo pacchetto handshake hello, pacchetti hello [ACK], verrà utilizzato in questo scenario.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-135">hello last packet in hello handshake, hello [ACK] packet, will not be used in this scenario.</span></span> <span data-ttu-id="d5f3d-136">Hello [SYN] pacchetto viene inviato dal client hello.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-136">hello [SYN] packet is sent by hello client.</span></span> <span data-ttu-id="d5f3d-137">Dopo che viene ricevuto server hello invia pacchetti hello [ACK] come una conferma di ricezione hello SYN dal client hello.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-137">Once it is received hello server sends hello [ACK] packet as an acknowledgement of receiving hello SYN from hello client.</span></span> <span data-ttu-id="d5f3d-138">Utilizzo delle tabelle dei fatti hello che risposta hello del server richiede un overhead minimo, è calcolare hello RTT sottraendo tempo hello pacchetti hello [SYN, ACK] è stato ricevuto da client hello dal pacchetto di tempo [SYN] hello inviato dal client hello.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-138">Leveraging hello fact that hello server’s response requires very little overhead, we calculate hello RTT by subtracting hello time hello [SYN, ACK] packet was received by hello client by hello time [SYN] packet was sent by hello client.</span></span>

<span data-ttu-id="d5f3d-139">Usando WireShark questo valore viene calcolato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-139">Using WireShark this value is calculated for us.</span></span>

<span data-ttu-id="d5f3d-140">toomore visualizzare facilmente i primi due pacchetti hello in handshake a tre vie TCP hello, verrà utilizzato il filtro delle funzionalità fornite da WireShark hello.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-140">toomore easily view hello first two packets in hello TCP three-way handshake, we will utilize hello filtering capability provided by WireShark.</span></span>

<span data-ttu-id="d5f3d-141">filtro hello tooapply WireShark, espandere hello "Transmission Control Protocol" segmento di un pacchetto [SYN] nell'acquisizione ed esaminare i flag di hello impostati nell'intestazione TCP hello.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-141">tooapply hello filter in WireShark, expand hello “Transmission Control Protocol” Segment of a [SYN] packet in your capture and examine hello flags set in hello TCP header.</span></span>

<span data-ttu-id="d5f3d-142">Poiché in esame toofilter in tutti i [SYN] e [SYN, ACK] pacchetti, con flag cofirm che hello Syn bit impostato too1, quindi fare clic destro sul bit Syn hello -> Applica come filtro -> selezionati.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-142">Since we are looking toofilter on all [SYN] and [SYN, ACK] packets, under flags cofirm that hello Syn bit is set too1, then right click on hello Syn bit -> Apply as Filter -> Selected.</span></span>

![Figura 7][7]

### <a name="step-4"></a><span data-ttu-id="d5f3d-144">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="d5f3d-144">Step 4</span></span>

<span data-ttu-id="d5f3d-145">Ora che sono stati filtrati finestra tooonly vedere i pacchetti hello con hello [SYN] bit impostato, è possibile selezionare le conversazioni si è interessati a tooview hello RTT iniziale.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-145">Now that you have filtered hello window tooonly see packets with hello [SYN] bit set, you can easily select conversations you are interested in tooview hello initial RTT.</span></span> <span data-ttu-id="d5f3d-146">Hello di tooview un modo semplice RTT in WireShark fare clic su elenco a discesa hello contrassegnato analysis "SEQ/ACK".</span><span class="sxs-lookup"><span data-stu-id="d5f3d-146">A simple way tooview hello RTT in WireShark simply click hello dropdown marked “SEQ/ACK” analysis.</span></span> <span data-ttu-id="d5f3d-147">Verrà quindi visualizzato hello che RTT visualizzato.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-147">You will then see hello RTT displayed.</span></span> <span data-ttu-id="d5f3d-148">In questo caso, hello RTT era 0.0022114 secondi o 2.211 ms.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-148">In this case, hello RTT was 0.0022114 seconds, or 2.211 ms.</span></span>

![Figura 8][8]

## <a name="unwanted-protocols"></a><span data-ttu-id="d5f3d-150">Protocolli indesiderati</span><span class="sxs-lookup"><span data-stu-id="d5f3d-150">Unwanted protocols</span></span>

<span data-ttu-id="d5f3d-151">In un'istanza di una macchina virtuale distribuita in Azure potrebbero essere in esecuzione più applicazioni.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-151">You can have many applications running on a virtual machine instance you have deployed in Azure.</span></span> <span data-ttu-id="d5f3d-152">Molte di queste applicazioni di comunicare in rete hello, probabilmente senza alcuna autorizzazione esplicita.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-152">Many of these applications communicate over hello network, perhaps without your explicit permission.</span></span> <span data-ttu-id="d5f3d-153">L'uso della comunicazione di rete toostore acquisizione pacchetto, è possibile esaminare come applicazione comunichino sulla rete hello e cercare eventuali problemi.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-153">Using packet capture toostore network communication, we can investigate how application are talking on hello network and look for any issues.</span></span>

<span data-ttu-id="d5f3d-154">In questo esempio viene esaminata un'acquisizione di pacchetti già eseguita per trovare protocolli indesiderati che potrebbero indicare una comunicazione non autorizzata da un'applicazione in esecuzione nel computer.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-154">In this example, we review a previous ran packet capture for unwanted protocols that may indicate unauthorized communication from an application running on your machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="d5f3d-155">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="d5f3d-155">Step 1</span></span>

<span data-ttu-id="d5f3d-156">Utilizzo di hello stessa acquisizione in hello precedente scenario, scegliere **statistiche** > **protocollo gerarchia**</span><span class="sxs-lookup"><span data-stu-id="d5f3d-156">Using hello same capture in hello previous scenario click **Statistics** > **Protocol Hierarchy**</span></span>

![Menu Protocol Hierarchy (Gerarchia protocolli)][2]

<span data-ttu-id="d5f3d-158">verrà visualizzata la finestra gerarchia di protocollo Hello.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-158">hello protocol hierarchy window appears.</span></span> <span data-ttu-id="d5f3d-159">Questa visualizzazione fornisce un elenco di tutti i protocolli di hello che erano in uso durante la sessione di acquisizione hello e numero di hello di pacchetti trasmessi e ricevuti tramite protocolli hello.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-159">This view provides a list of all hello protocols that were in use during hello capture session and hello number of packets transmitted and received using hello protocols.</span></span> <span data-ttu-id="d5f3d-160">Si tratta di una visualizzazione utile per trovare il traffico di rete indesiderato nelle macchine virtuali o in rete.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-160">This view can be useful for finding unwanted network traffic on your virtual machines or network.</span></span>

![Gerarchia dei protocolli aperta][3]

<span data-ttu-id="d5f3d-162">Come si può notare in hello dopo l'acquisizione dello schermo, si è verificato il traffico tramite il protocollo BitTorrent hello, che viene utilizzato per la condivisione di file toopeer peer.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-162">As you can see in hello following screen capture, there was traffic using hello BitTorrent protocol, which is used for peer toopeer file sharing.</span></span> <span data-ttu-id="d5f3d-163">Un amministratore non si prevede toosee BitTorrent traffico specifico le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-163">As an administrator you do not expect toosee BitTorrent traffic on this particular virtual machines.</span></span> <span data-ttu-id="d5f3d-164">Ora è consapevoli del traffico, è possibile rimuovere hello peer toopeer software installato in questa macchina virtuale o hello blocco del traffico tramite un Firewall o i gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-164">Now you aware of this traffic, you can remove hello peer toopeer software that installed on this virtual machine, or block hello traffic using Network Security Groups or a Firewall.</span></span> <span data-ttu-id="d5f3d-165">Inoltre, è possibile scegliere toorun acquisizioni di pacchetti in una pianificazione, pertanto è possibile esaminare regolarmente hello protocollo utilizzo nelle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-165">Additionally, you may elect toorun packet captures on a schedule, so you can review hello protocol use on your virtual machines regularly.</span></span> <span data-ttu-id="d5f3d-166">Per un esempio sulle modalità di attività di rete tooautomate in azure visita [monitoraggio delle risorse di rete con automazione di azure](network-watcher-monitor-with-azure-automation.md)</span><span class="sxs-lookup"><span data-stu-id="d5f3d-166">For an example on how tooautomate network tasks in azure visit [Monitor network resources with azure automation](network-watcher-monitor-with-azure-automation.md)</span></span>

## <a name="finding-top-destinations-and-ports"></a><span data-ttu-id="d5f3d-167">Ricerca di porte e destinazioni principali</span><span class="sxs-lookup"><span data-stu-id="d5f3d-167">Finding top destinations and ports</span></span>

<span data-ttu-id="d5f3d-168">Informazioni sui tipi di hello del traffico, hello endpoint e porte hello comunicate tramite è un importante durante il monitoraggio e risoluzione dei problemi delle applicazioni e risorse di rete.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-168">Understanding hello types of traffic, hello endpoints, and hello ports communicated over is an important when monitoring or troubleshooting applications and resources on your network.</span></span> <span data-ttu-id="d5f3d-169">Utilizzo di un file di acquisizione dei pacchetti precedente, è possibile apprendere rapidamente hello prime destinazioni la macchina virtuale sta comunicando e hello porte in uso.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-169">Utilizing a packet capture file from above, we can quickly learn hello top destinations our VM is communicating with and hello ports being utilized.</span></span>

### <a name="step-1"></a><span data-ttu-id="d5f3d-170">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="d5f3d-170">Step 1</span></span>

<span data-ttu-id="d5f3d-171">Utilizzando hello stessa acquisizione in hello precedente scenario, scegliere **statistiche** > **statistiche IPv4** > **destinazioni e le porte**</span><span class="sxs-lookup"><span data-stu-id="d5f3d-171">Using hello same capture in hello previous scenario click **Statistics** > **IPv4 Statistics** > **Destinations and Ports**</span></span>

![Finestra di acquisizione di pacchetti][4]

### <a name="step-2"></a><span data-ttu-id="d5f3d-173">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="d5f3d-173">Step 2</span></span>

<span data-ttu-id="d5f3d-174">Come esaminare i risultati di hello distingue una riga, si sono verificati più connessioni sulla porta 111.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-174">As we look through hello results a line stands out, there were multiple connections on port 111.</span></span> <span data-ttu-id="d5f3d-175">porta Hello più utilizzato è 3389, ovvero desktop remoto e hello rimanenti sono porte dinamiche RPC.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-175">hello most used port was 3389, which is remote desktop, and hello remaining are RPC dynamic ports.</span></span>

<span data-ttu-id="d5f3d-176">Questo traffico può significare nothing, ma è una porta che veniva utilizzata per un numero di connessioni e amministratore toohello sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-176">While this traffic may mean nothing, it is a port that was used for many connections and is unknown toohello administrator.</span></span>

![Figura 5][5]

### <a name="step-3"></a><span data-ttu-id="d5f3d-178">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="d5f3d-178">Step 3</span></span>

<span data-ttu-id="d5f3d-179">Ora che è stato rilevato un timeout della porta sul posto che è possibile filtrare l'acquisizione in base a una porta di hello.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-179">Now that we have determined an out of place port we can filter our capture based on hello port.</span></span>

<span data-ttu-id="d5f3d-180">filtro Hello in questo scenario sarà:</span><span class="sxs-lookup"><span data-stu-id="d5f3d-180">hello filter in this scenario would be:</span></span>

```
tcp.port == 111
```

<span data-ttu-id="d5f3d-181">Testo del filtro hello sopra è immettere nella casella di testo hello filtro e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-181">We enter hello filter text from above in hello filter textbox and hit enter.</span></span>

![Figura 6][6]

<span data-ttu-id="d5f3d-183">Dai risultati di hello, possiamo vedere tutto il traffico hello proviene da una macchina virtuale locale hello stessa subnet.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-183">From hello results, we can see all hello traffic is coming from a local virtual machine on hello same subnet.</span></span> <span data-ttu-id="d5f3d-184">Se ancora non comprendere perché è in corso il traffico, è possibile controllare ulteriormente toodetermine pacchetti hello motivo per cui esegue queste chiamate sulla porta 111.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-184">If we still don’t understand why this traffic is occurring, we can further inspect hello packets toodetermine why it is making these calls on port 111.</span></span> <span data-ttu-id="d5f3d-185">Con queste informazioni è possibile effettuare l'azione appropriata hello.</span><span class="sxs-lookup"><span data-stu-id="d5f3d-185">With this information we can take hello appropriate action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5f3d-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d5f3d-186">Next steps</span></span>

<span data-ttu-id="d5f3d-187">Informazioni circa hello altre funzionalità di diagnostica di rete Watcher visitando [Panoramica di monitoraggio della rete di Azure](network-watcher-monitoring-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d5f3d-187">Learn about hello other diagnostic features of Network Watcher by visiting [Azure network monitoring overview](network-watcher-monitoring-overview.md)</span></span>

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













