---
title: modelli di traffico di rete aaaVisualize con Watcher di rete di Azure e strumenti open source | Documenti Microsoft
description: Questa pagina vengono descritti come pacchetto Watcher di rete toouse capture Capanalysis toovisualize traffico modelli tooand dalle macchine virtuali.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a><span data-ttu-id="4dc3c-103">Visualizzare tooand di modelli di traffico di rete dalle macchine virtuali utilizzando strumenti open source</span><span class="sxs-lookup"><span data-stu-id="4dc3c-103">Visualize network traffic patterns tooand from your VMs using open source tools</span></span>

<span data-ttu-id="4dc3c-104">Le acquisizioni di pacchetti contengono dati di rete che consentono di analisi forense rete tooperform e analisi approfondita dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-104">Packet captures contain network data that allow you tooperform network forensics and deep packet inspection.</span></span> <span data-ttu-id="4dc3c-105">Sono disponibili apre molti strumenti di origine è possibile utilizzare tooanalyze pacchetto acquisizioni toogain approfondimenti sulla rete.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-105">There are many opens source tools you can use tooanalyze packet captures toogain insights about your network.</span></span> <span data-ttu-id="4dc3c-106">Uno di questi strumenti è CapAnalysis, uno strumento di visualizzazione dell'acquisizione pacchetti open source.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-106">One such tool is CapAnalysis, an open source packet capture visualization tool.</span></span> <span data-ttu-id="4dc3c-107">Visualizzazione dei dati di acquisizione pacchetto è un modo utile tooquickly derivare informazioni dettagliate sui modelli e anomalie all'interno della rete.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-107">Visualizing packet capture data is a valuable way tooquickly derive insights on patterns and anomalies within your network.</span></span> <span data-ttu-id="4dc3c-108">e di condividere tali informazioni in un modo facilmente utilizzabile.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-108">Visualizations also provide a means of sharing such insights in an easily consumable manner.</span></span>

<span data-ttu-id="4dc3c-109">Watcher di rete di Azure fornisce che si hello toocapture possibilità acquisisce dati importanti, consentendo tooperform pacchetti sulla rete.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-109">Azure’s Network Watcher provides you hello ability toocapture this valuable data by allowing you tooperform packet captures on your network.</span></span> <span data-ttu-id="4dc3c-110">In questo articolo è fornire una procedura dettagliata di come toovisualize e ottenere informazioni dai pacchetti acquisisce con CapAnalysis Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-110">In this article, we provide a walkthrough of how toovisualize and gain insights from packet captures using CapAnalysis with Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="4dc3c-111">Scenario</span><span class="sxs-lookup"><span data-stu-id="4dc3c-111">Scenario</span></span>

<span data-ttu-id="4dc3c-112">Si dispone di un'applicazione web semplice distribuita in una macchina virtuale in Azure desidera toouse Apri origine strumenti toovisualize relativo tooquickly il traffico di rete identificare modelli di flusso e di eventuali anomalie possibili.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-112">You have a simple web application deployed on a VM in Azure want toouse open source tools toovisualize its network traffic tooquickly identify flow patterns and any possible anomalies.</span></span> <span data-ttu-id="4dc3c-113">Network Watcher permette di ottenere un'acquisizione pacchetti dell'ambiente di rete e di memorizzarla direttamente nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-113">With Network Watcher, you can obtain a packet capture of your network environment and directly store it on your storage account.</span></span> <span data-ttu-id="4dc3c-114">CapAnalysis quindi inserimento hello acquisizione pacchetto direttamente dal blob di archiviazione hello e visualizzare il relativo contenuto.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-114">CapAnalysis can then ingest hello packet capture directly from hello storage blob and visualize its contents.</span></span>

![scenario][1]

## <a name="steps"></a><span data-ttu-id="4dc3c-116">Passi</span><span class="sxs-lookup"><span data-stu-id="4dc3c-116">Steps</span></span>

### <a name="install-capanalysis"></a><span data-ttu-id="4dc3c-117">Installare CapAnalysis</span><span class="sxs-lookup"><span data-stu-id="4dc3c-117">Install CapAnalysis</span></span>

<span data-ttu-id="4dc3c-118">tooinstall CapAnalysis in una macchina virtuale, è possibile fare riferimento le istruzioni ufficiale toohello https://www.capanalysis.net/ca/how-to-install-capanalysis qui.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-118">tooinstall CapAnalysis on a virtual machine, you can refer toohello official instructions here https://www.capanalysis.net/ca/how-to-install-capanalysis.</span></span>
<span data-ttu-id="4dc3c-119">In ordine di accesso CapAnalysis in modalità remota, è la porta tooopen 9877 nella VM aggiungendo una nuova regola di sicurezza in ingresso.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-119">In order access CapAnalysis remotely, we need tooopen port 9877 on your VM by adding a new inbound security rule.</span></span> <span data-ttu-id="4dc3c-120">Per ulteriori informazioni sulla creazione di regole nei gruppi di sicurezza di rete, fare riferimento troppo[creare regole in un gruppo esistente](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span><span class="sxs-lookup"><span data-stu-id="4dc3c-120">For more about creating rules in Network Security Groups, refer too[Create rules in an existing NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg).</span></span> <span data-ttu-id="4dc3c-121">Una volta regola hello è stata aggiunta correttamente, dovrebbe essere in grado di tooaccess CapAnalysis da`http://<PublicIP>:9877`</span><span class="sxs-lookup"><span data-stu-id="4dc3c-121">Once hello rule has been successfully added, you should be able tooaccess CapAnalysis from `http://<PublicIP>:9877`</span></span>

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a><span data-ttu-id="4dc3c-122">Utilizzare il Watcher di rete di Azure toostart sessione di acquisizione di un pacchetto</span><span class="sxs-lookup"><span data-stu-id="4dc3c-122">Use Azure Network Watcher toostart a packet capture session</span></span>

<span data-ttu-id="4dc3c-123">Watcher di rete consente il traffico di tootrack toocapture pacchetti da e verso una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-123">Network Watcher allows you toocapture packets tootrack traffic in and out of a virtual machine.</span></span> <span data-ttu-id="4dc3c-124">È possibile fare riferimento a istruzioni toohello [acquisizioni di pacchetti di gestione con Watcher di rete](network-watcher-packet-capture-manage-portal.md) toostart una sessione di acquisizione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-124">You can refer toohello instructions at [Manage packet captures with Network Watcher](network-watcher-packet-capture-manage-portal.md) toostart a packet capture session.</span></span> <span data-ttu-id="4dc3c-125">Questa acquisizione pacchetto può essere archiviata in un toobe di archiviazione blob a cui accede CapAnalysis.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-125">This packet capture can be stored in a storage blob toobe accessed by CapAnalysis.</span></span>

### <a name="upload-a-packet-capture-toocapanalysis"></a><span data-ttu-id="4dc3c-126">Caricare un tooCapAnalysis acquisizione pacchetti</span><span class="sxs-lookup"><span data-stu-id="4dc3c-126">Upload a packet capture tooCapAnalysis</span></span>
<span data-ttu-id="4dc3c-127">È possibile caricare direttamente un'acquisizione pacchetto eseguita dal controllo di rete utilizzando hello "importazione dalla scheda"URL e fornendo un blob di archiviazione toohello collegamento in cui è memorizzato l'acquisizione di pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-127">You can directly upload a packet capture taken by network watcher using hello “Import from URL” tab and providing a link toohello storage blob where hello packet capture is stored.</span></span>

<span data-ttu-id="4dc3c-128">Se si fornisce un collegamento di tooCapAnalysis, assicurarsi che tooappend un URL di firma di accesso condiviso toohello token archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-128">When providing a link tooCapAnalysis, make sure tooappend a SAS token toohello storage blob URL.</span></span>  <span data-ttu-id="4dc3c-129">toodo, passare la firma di accesso tooShared dall'account di archiviazione hello, designare hello consentita le autorizzazioni, quindi premere hello generare SAS pulsante toocreate un token.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-129">toodo this, navigate tooShared access signature from hello storage account, designate hello allowed permissions, and press hello Generate SAS button toocreate a token.</span></span> <span data-ttu-id="4dc3c-130">È quindi possibile aggiungere questo URL del blob archiviazione SAS toohello token pacchetto acquisizione.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-130">You can then append this SAS token toohello packet capture storage blob URL.</span></span>

<span data-ttu-id="4dc3c-131">Hello URL risultante avrà un aspetto simile al seguente: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span><span class="sxs-lookup"><span data-stu-id="4dc3c-131">hello resulting URL will look something like this: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere</span></span>


### <a name="analyzing-packet-captures"></a><span data-ttu-id="4dc3c-132">Analizzare le acquisizioni pacchetti</span><span class="sxs-lookup"><span data-stu-id="4dc3c-132">Analyzing packet captures</span></span>

<span data-ttu-id="4dc3c-133">CapAnalysis offre varie opzioni toovisualize l'acquisizione pacchetto, ogni analisi fornita da una prospettiva diversa.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-133">CapAnalysis offers various options toovisualize your packet capture, each providing analysis from a different perspective.</span></span> <span data-ttu-id="4dc3c-134">Questi riepiloghi visivi permettono di comprendere le tendenze del traffico di rete e individuare rapidamente eventuali attività inconsuete.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-134">With these visual summaries, you can understand your network traffic trends and quickly spot any unusual activity.</span></span> <span data-ttu-id="4dc3c-135">Alcune di queste funzionalità vengono visualizzate in hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="4dc3c-135">A few of these features are shown in hello following list:</span></span>

1. <span data-ttu-id="4dc3c-136">Tabelle di flusso</span><span class="sxs-lookup"><span data-stu-id="4dc3c-136">Flow Tables</span></span>

    <span data-ttu-id="4dc3c-137">In questo modo tabella hello elenco di flussi di dati del pacchetto di hello, hello timestamp associato flussi hello e hello vari protocolli associati al flusso di hello, nonché di IP di origine e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-137">This table gives you hello list of flows in hello packet data, hello time stamp associated with hello flows and hello various protocols associated with hello flow, as well as source and destination IP.</span></span>

    ![Pagina dei flussi di CapAnalysis][5]

1. <span data-ttu-id="4dc3c-139">Panoramica dei protocolli</span><span class="sxs-lookup"><span data-stu-id="4dc3c-139">Protocol Overview</span></span>

    <span data-ttu-id="4dc3c-140">In questo riquadro consente tooquickly Vedere distribuzione hello del traffico di rete su hello diversi protocolli e aree geografiche.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-140">This pane allows you tooquickly see hello distribution of network traffic over hello various protocols and geographies.</span></span>

    ![Panoramica dei protocolli di CapAnalysis][6]

1. <span data-ttu-id="4dc3c-142">Statistiche</span><span class="sxs-lookup"><span data-stu-id="4dc3c-142">Statistics</span></span>

    <span data-ttu-id="4dc3c-143">In questo riquadro consente alle statistiche sul traffico di rete di tooview: byte inviati e ricevuti dall'origine e destinazione IP, i flussi per ogni origine hello e di destinazione gli indirizzi IP, protocollo utilizzato per flussi diversi e la durata di hello dei flussi.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-143">This pane allows you tooview network traffic statistics – bytes sent and received from source and destination IPs, flows for each of hello source and destination IPs, protocol used for various flows, and hello duration of flows.</span></span>

    ![Statistiche di CapAnalysis][7]

1. <span data-ttu-id="4dc3c-145">Mappa geografica</span><span class="sxs-lookup"><span data-stu-id="4dc3c-145">Geomap</span></span>

    <span data-ttu-id="4dc3c-146">Questo riquadro consente di visualizzare una mappa del traffico di rete, con colori scalabilità toohello volume di traffico da ogni paese.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-146">This pane provides you with a map view of your network traffic, with colors scaling toohello volume of traffic from each country.</span></span> <span data-ttu-id="4dc3c-147">È possibile selezionare i paesi evidenziati tooview flusso ulteriori statistiche, ad esempio percentuale hello dei dati inviati e ricevuti da indirizzi IP in tale paese.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-147">You can select highlighted countries tooview additional flow statistics such as hello proportion of data sent and received from IPs in that country.</span></span>

    ![Mappa geografica][8]

1. <span data-ttu-id="4dc3c-149">Filtri</span><span class="sxs-lookup"><span data-stu-id="4dc3c-149">Filters</span></span>

    <span data-ttu-id="4dc3c-150">CapAnalysis include un set di filtri per l'analisi rapida di pacchetti specifici.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-150">CapAnalysis provides a set of filters for quick analysis of specific packets.</span></span> <span data-ttu-id="4dc3c-151">Ad esempio, è possibile scegliere i dati di hello toofilter per informazioni dettagliate specifiche protocollo toogain a tale subset di traffico.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-151">For example, you can choose toofilter hello data by protocol toogain specific insights on that subset of traffic.</span></span>

    ![filters][11]

    <span data-ttu-id="4dc3c-153">Visitare [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn ulteriori informazioni sulla funzionalità tutti CapAnalysis.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-153">Visit [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn more about all CapAnalysis' capabilities.</span></span>

## <a name="conclusion"></a><span data-ttu-id="4dc3c-154">Conclusioni</span><span class="sxs-lookup"><span data-stu-id="4dc3c-154">Conclusion</span></span>

<span data-ttu-id="4dc3c-155">La funzionalità di acquisizione del Watcher di rete pacchetto consente toocapture hello tooperform necessario rete analisi forensi e comprendere meglio il traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-155">Network Watcher’s packet capture feature allows you toocapture hello data necessary tooperform network forensics and better understand your network traffic.</span></span> <span data-ttu-id="4dc3c-156">In questo scenario è stato illustrato come integrate facilmente le acquisizioni pacchetti di Network Watcher con strumenti di visualizzazione open source.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-156">In this scenario, we showed how packet captures from Network Watcher can easily be integrated with open source visualization tools.</span></span> <span data-ttu-id="4dc3c-157">Tramite strumenti open source, ad esempio acquisisce CapAnalysis toovisualize pacchetti, è possibile eseguire l'analisi approfondita dei pacchetti e identificare rapidamente le tendenze all'interno del traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="4dc3c-157">By using open source tools such as CapAnalysis toovisualize packets captures, you can perform deep packet inspection and quickly identify trends within your network traffic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4dc3c-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4dc3c-158">Next steps</span></span>

<span data-ttu-id="4dc3c-159">toolearn ulteriori informazioni sui registri del flusso di gruppo, visitare [registra flusso NSG](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="4dc3c-159">toolearn more about NSG flow logs, visit [NSG Flow logs](network-watcher-nsg-flow-logging-overview.md)</span></span>

<span data-ttu-id="4dc3c-160">Informazioni su come toovisualize il flusso di gruppo Registra con Power BI visitando [NSG visualizzare flussi di log con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="4dc3c-160">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png
