---
title: "velocità effettiva della rete di macchina virtuale di Azure aaaTesting | Documenti Microsoft"
description: "Informazioni su come macchina virtuale di Azure tootest rete velocità effettiva."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/21/2017
ms.author: steveesp
ms.openlocfilehash: 2da85c27bc8d16a443b215891f4cd0460f41926f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a><span data-ttu-id="0cd9e-103">Test della larghezza di banda/velocità effettiva (NTTTCP)</span><span class="sxs-lookup"><span data-stu-id="0cd9e-103">Bandwidth/Throughput testing (NTTTCP)</span></span>

<span data-ttu-id="0cd9e-104">Durante il test delle prestazioni di velocità effettiva di rete in Azure, è uno strumento che ha come destinazione rete hello per il test e riduce al minimo hello uso di altre risorse che può influire sulle prestazioni di toouse migliore.</span><span class="sxs-lookup"><span data-stu-id="0cd9e-104">When testing network throughput performance in Azure, it's best toouse a tool that targets hello network for testing and minimizes hello use of other resources that could impact performance.</span></span> <span data-ttu-id="0cd9e-105">È consigliabile usare NTTTCP.</span><span class="sxs-lookup"><span data-stu-id="0cd9e-105">NTTTCP is recommended.</span></span>

<span data-ttu-id="0cd9e-106">Copiare lo strumento di hello tootwo macchine virtuali di Azure di hello stessa dimensione.</span><span class="sxs-lookup"><span data-stu-id="0cd9e-106">Copy hello tool tootwo Azure VMs of hello same size.</span></span> <span data-ttu-id="0cd9e-107">Una macchina virtuale funziona come mittente e altri come ricevitore hello.</span><span class="sxs-lookup"><span data-stu-id="0cd9e-107">One VM functions as SENDER and hello other as RECEIVER.</span></span>

#### <a name="deploying-vms-for-testing"></a><span data-ttu-id="0cd9e-108">Distribuzione di macchine virtuali per i test</span><span class="sxs-lookup"><span data-stu-id="0cd9e-108">Deploying VMs for testing</span></span>
<span data-ttu-id="0cd9e-109">Ai fini di hello di questo test, hello due macchine virtuali devono trovarsi in hello nello stesso servizio Cloud o hello stesso Set di disponibilità in modo che è possibile usare l'IP interno e l'esclusione bilanciamenti del carico hello test hello.</span><span class="sxs-lookup"><span data-stu-id="0cd9e-109">For hello purposes of this test, hello two VMs should be in either hello same Cloud Service or hello same Availability Set so that we can use their internal IPs and exclude hello Load Balancers from hello test.</span></span> <span data-ttu-id="0cd9e-110">È possibile tootest con hello VIP, ma questo tipo di test si trova fuori ambito hello di questo documento.</span><span class="sxs-lookup"><span data-stu-id="0cd9e-110">It is possible tootest with hello VIP but this kind of testing is outside hello scope of this document.</span></span>
 
<span data-ttu-id="0cd9e-111">Prendere nota dell'indirizzo IP del ricevitore hello.</span><span class="sxs-lookup"><span data-stu-id="0cd9e-111">Make a note of hello RECEIVER's IP address.</span></span> <span data-ttu-id="0cd9e-112">In questo esempio verrà definito "a.b.c.r."</span><span class="sxs-lookup"><span data-stu-id="0cd9e-112">Let's call that IP "a.b.c.r"</span></span>

<span data-ttu-id="0cd9e-113">Prendere nota del numero di hello di core nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="0cd9e-113">Make a note of hello number of cores on hello VM.</span></span> <span data-ttu-id="0cd9e-114">In questo esempio sarà "\#num\_cores"</span><span class="sxs-lookup"><span data-stu-id="0cd9e-114">Let's call this "\#num\_cores"</span></span>
 
<span data-ttu-id="0cd9e-115">Eseguire hello NTTTCP di test per 300 secondi (o 5 minuti) sul mittente hello macchina virtuale e il destinatario macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0cd9e-115">Run hello NTTTCP test for 300 seconds (or 5 minutes) on hello sender VM and receiver VM.</span></span>

<span data-ttu-id="0cd9e-116">Suggerimento: Quando si imposta questo test per hello prima volta, è possibile provare un più breve periodo tooget risultati dei test più rapidamente.</span><span class="sxs-lookup"><span data-stu-id="0cd9e-116">Tip: When setting up this test for hello first time, you might try a shorter test period tooget feedback sooner.</span></span> <span data-ttu-id="0cd9e-117">Una volta hello strumento funziona come previsto, è possibile estendere secondi too300 periodo di prova hello per ottenere risultati più accurati hello.</span><span class="sxs-lookup"><span data-stu-id="0cd9e-117">Once hello tool is working as expected, extend hello test period too300 seconds for hello most accurate results.</span></span>

> [!NOTE]
> <span data-ttu-id="0cd9e-118">mittente Hello **e** ricevitore deve specificare **hello stesso** test parametro di durata (-t).</span><span class="sxs-lookup"><span data-stu-id="0cd9e-118">hello sender **and** receiver must specify **hello same** test duration parameter (-t).</span></span>

<span data-ttu-id="0cd9e-119">tootest un singolo flusso TCP per 10 secondi:</span><span class="sxs-lookup"><span data-stu-id="0cd9e-119">tootest a single TCP stream for 10 seconds:</span></span>

<span data-ttu-id="0cd9e-120">Parametri ricevitore: ntttcp -r -t 10 -P 1</span><span class="sxs-lookup"><span data-stu-id="0cd9e-120">Receiver parameters: ntttcp -r -t 10 -P 1</span></span>

<span data-ttu-id="0cd9e-121">Parametri mittente: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span><span class="sxs-lookup"><span data-stu-id="0cd9e-121">Sender parameters: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span></span>

> [!NOTE]
> <span data-ttu-id="0cd9e-122">Hello precedente esempio deve essere solo tooconfirm utilizzata la configurazione.</span><span class="sxs-lookup"><span data-stu-id="0cd9e-122">hello preceding sample should only be used tooconfirm your configuration.</span></span> <span data-ttu-id="0cd9e-123">Alcuni esempi di test effettivi vengono trattati più avanti in questo documento.</span><span class="sxs-lookup"><span data-stu-id="0cd9e-123">Valid examples of testing are covered later in this document.</span></span>

## <a name="testing-vms-running-windows"></a><span data-ttu-id="0cd9e-124">Test di macchine virtuali che eseguono WINDOWS:</span><span class="sxs-lookup"><span data-stu-id="0cd9e-124">Testing VMs running WINDOWS:</span></span>

#### <a name="get-ntttcp-onto-hello-vms"></a><span data-ttu-id="0cd9e-125">Ottenere NTTTCP su hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="0cd9e-125">Get NTTTCP onto hello VMs.</span></span>

<span data-ttu-id="0cd9e-126">Scaricare la versione più recente di hello: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span><span class="sxs-lookup"><span data-stu-id="0cd9e-126">Download hello latest version: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span></span>

<span data-ttu-id="0cd9e-127">O cercarla se spostata: <https://www.bing.com/search?q=ntttcp+download>\<. Generalmente sarà il primo risultato ottenuto</span><span class="sxs-lookup"><span data-stu-id="0cd9e-127">Or search for it if moved: <https://www.bing.com/search?q=ntttcp+download>\< -- should be first hit</span></span>

<span data-ttu-id="0cd9e-128">È consigliabile inserire NTTTCP in una cartella separata, ad esempio, ad esempio c:\\strumenti</span><span class="sxs-lookup"><span data-stu-id="0cd9e-128">Consider putting NTTTCP in separate folder, like c:\\tools</span></span>

#### <a name="allow-ntttcp-through-hello-windows-firewall"></a><span data-ttu-id="0cd9e-129">Consente di NTTTCP attraverso il firewall di Windows hello</span><span class="sxs-lookup"><span data-stu-id="0cd9e-129">Allow NTTTCP through hello Windows firewall</span></span>
<span data-ttu-id="0cd9e-130">Sul ricevitore hello, creare una regola di assenso in hello Windows Firewall tooallow il tooarrive traffico NTTTCP.</span><span class="sxs-lookup"><span data-stu-id="0cd9e-130">On hello RECEIVER, create an Allow rule on hello Windows Firewall tooallow the NTTTCP traffic tooarrive.</span></span> <span data-ttu-id="0cd9e-131">È più semplice tooallow hello intero NTTTCP programma in base al nome anziché tooallow specifiche porte TCP in ingresso.</span><span class="sxs-lookup"><span data-stu-id="0cd9e-131">It's easiest tooallow hello entire NTTTCP program by name rather than tooallow specific TCP ports inbound.</span></span>

<span data-ttu-id="0cd9e-132">Consenti ntttcp tramite hello Windows Firewall simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="0cd9e-132">Allow ntttcp through hello Windows Firewall like this:</span></span>

<span data-ttu-id="0cd9e-133">netsh advfirewall firewall add rule program=\<PERCORSO\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="0cd9e-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

<span data-ttu-id="0cd9e-134">Ad esempio, se è stato copiato ntttcp.exe toohello "c:\\strumenti" cartella, potrebbe essere il comando hello:</span><span class="sxs-lookup"><span data-stu-id="0cd9e-134">For example, if you copied ntttcp.exe toohello "c:\\tools" folder, this would be hello command:</span></span> 

<span data-ttu-id="0cd9e-135">netsh advfirewall firewall add rule program=c:\\strumenti\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="0cd9e-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

#### <a name="running-ntttcp-tests"></a><span data-ttu-id="0cd9e-136">Esecuzione di test NTTTCP</span><span class="sxs-lookup"><span data-stu-id="0cd9e-136">Running NTTTCP tests</span></span>

<span data-ttu-id="0cd9e-137">Avviare NTTTCP su hello ricevitore (**eseguire da CMD**, ma non da PowerShell):</span><span class="sxs-lookup"><span data-stu-id="0cd9e-137">Start NTTTCP on hello RECEIVER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="0cd9e-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span><span class="sxs-lookup"><span data-stu-id="0cd9e-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span></span>

<span data-ttu-id="0cd9e-139">Se hello macchina virtuale dispone di quattro core e un indirizzo IP di 10.0.0.4, avrà un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="0cd9e-139">If hello VM has four cores and an IP address of 10.0.0.4, it would look like this:</span></span>

<span data-ttu-id="0cd9e-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="0cd9e-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span></span>


<span data-ttu-id="0cd9e-141">Avviare NTTTCP su hello mittente (**eseguire da CMD**, ma non da PowerShell):</span><span class="sxs-lookup"><span data-stu-id="0cd9e-141">Start NTTTCP on hello SENDER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="0cd9e-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="0cd9e-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span></span> 

<span data-ttu-id="0cd9e-143">Attendere i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="0cd9e-143">Wait for hello results.</span></span>


## <a name="testing-vms-running-linux"></a><span data-ttu-id="0cd9e-144">Test di macchine virtuali che eseguono LINUX:</span><span class="sxs-lookup"><span data-stu-id="0cd9e-144">Testing VMs running LINUX:</span></span>

<span data-ttu-id="0cd9e-145">Usare nttcp-for-linux,</span><span class="sxs-lookup"><span data-stu-id="0cd9e-145">Use nttcp-for-linux.</span></span> <span data-ttu-id="0cd9e-146">disponibile all'indirizzo <https://github.com/Microsoft/ntttcp-for-linux></span><span class="sxs-lookup"><span data-stu-id="0cd9e-146">It is available from <https://github.com/Microsoft/ntttcp-for-linux></span></span>

<span data-ttu-id="0cd9e-147">In hello le macchine virtuali Linux (mittente e ricevitore), eseguire questi comandi per preparare ntttcp per linux su macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="0cd9e-147">On hello Linux VMs (both SENDER and RECEIVER), run these commands to prepare ntttcp-for-linux on your VMs:</span></span>

<span data-ttu-id="0cd9e-148">CentOS - Installare Git:</span><span class="sxs-lookup"><span data-stu-id="0cd9e-148">CentOS - Install Git:</span></span>
``` bash
  yum install gcc -y  
  yum install git -y
```
<span data-ttu-id="0cd9e-149">Ubuntu - Installare Git:</span><span class="sxs-lookup"><span data-stu-id="0cd9e-149">Ubuntu - Install Git:</span></span>
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
<span data-ttu-id="0cd9e-150">Verificare e installare in entrambie le macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="0cd9e-150">Make and Install on both:</span></span>
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

<span data-ttu-id="0cd9e-151">Come esempio di Windows hello, si presuppone il che indirizzo IP del ricevitore di hello Linux è 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="0cd9e-151">As in hello Windows example, we assume hello Linux RECEIVER's IP is 10.0.0.4</span></span>

<span data-ttu-id="0cd9e-152">Avviare NTTTCP per Linux hello ricevitore:</span><span class="sxs-lookup"><span data-stu-id="0cd9e-152">Start NTTTCP-for-Linux on hello RECEIVER:</span></span>

``` bash
ntttcp -r -t 300
```

<span data-ttu-id="0cd9e-153">E in hello mittente, eseguire:</span><span class="sxs-lookup"><span data-stu-id="0cd9e-153">And on hello SENDER, run:</span></span>

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
<span data-ttu-id="0cd9e-154">Test lunghezza predefinite too60 secondi se nessun parametro di tipo ora viene assegnato</span><span class="sxs-lookup"><span data-stu-id="0cd9e-154">Test length defaults too60 seconds if no time parameter is given</span></span>

## <a name="testing-between-vms-running-windows-and-linux"></a><span data-ttu-id="0cd9e-155">Test tra macchine virtuali che eseguono Windows e LINUX:</span><span class="sxs-lookup"><span data-stu-id="0cd9e-155">Testing between VMs running Windows and LINUX:</span></span>

<span data-ttu-id="0cd9e-156">Sugli scenari di questo è necessario abilitare la modalità nosync hello che consentono di eseguire il test di hello.</span><span class="sxs-lookup"><span data-stu-id="0cd9e-156">On this scenarios we should enable hello no-sync mode so hello test can run.</span></span> <span data-ttu-id="0cd9e-157">Questa operazione viene eseguita tramite hello **-N flag** per Linux e **flag -ns** per Windows.</span><span class="sxs-lookup"><span data-stu-id="0cd9e-157">This is done by using hello **-N flag** for Linux, and **-ns flag** for Windows.</span></span>

#### <a name="from-linux-toowindows"></a><span data-ttu-id="0cd9e-158">Da tooWindows Linux:</span><span class="sxs-lookup"><span data-stu-id="0cd9e-158">From Linux tooWindows:</span></span>

<span data-ttu-id="0cd9e-159">Ricevitore <Windows>:</span><span class="sxs-lookup"><span data-stu-id="0cd9e-159">Receiver <Windows>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

<span data-ttu-id="0cd9e-160">Mittente <Linux>:</span><span class="sxs-lookup"><span data-stu-id="0cd9e-160">Sender <Linux> :</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-toolinux"></a><span data-ttu-id="0cd9e-161">Da Windows tooLinux:</span><span class="sxs-lookup"><span data-stu-id="0cd9e-161">From Windows tooLinux:</span></span>

<span data-ttu-id="0cd9e-162">Ricevitore <Linux>:</span><span class="sxs-lookup"><span data-stu-id="0cd9e-162">Receiver <Linux>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

<span data-ttu-id="0cd9e-163">Mittente <Windows>:</span><span class="sxs-lookup"><span data-stu-id="0cd9e-163">Sender <Windows>:</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a><span data-ttu-id="0cd9e-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0cd9e-164">Next steps</span></span>
* <span data-ttu-id="0cd9e-165">A seconda dei risultati, potrebbe esserci spazio troppo[ottimizzare macchine di velocità effettiva di rete](virtual-network-optimize-network-bandwidth.md) per lo scenario.</span><span class="sxs-lookup"><span data-stu-id="0cd9e-165">Depending on results, there may be room too[Optimize network throughput machines](virtual-network-optimize-network-bandwidth.md) for your scenario.</span></span>
* <span data-ttu-id="0cd9e-166">Ulteriori informazioni sono disponibili nell'articolo [Domande frequenti sulla rete virtuale di Azure](virtual-networks-faq.md)</span><span class="sxs-lookup"><span data-stu-id="0cd9e-166">Learn more wtih [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
