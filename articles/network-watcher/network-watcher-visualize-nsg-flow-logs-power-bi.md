---
title: Visualizzare i log dei flussi dei gruppi di sicurezza di rete di Azure con Power BI | Microsoft Docs
description: Questo articolo illustra come visualizzare i log dei flussi dei gruppi di sicurezza di rete con Power BI.
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 1e4f95fa-f5f0-4e03-bc25-008fbfc4934c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d8c61ca2a3bd5affe02e8f9500655db6699a245f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a><span data-ttu-id="7dd38-103">Visualizzare i log dei flussi dei gruppi di sicurezza di rete con Power BI</span><span class="sxs-lookup"><span data-stu-id="7dd38-103">Visualizing Network Security Group flow logs with Power BI</span></span>

<span data-ttu-id="7dd38-104">I log dei flussi dei gruppi di sicurezza di rete permettono di visualizzare le informazioni sul traffico IP in ingresso e in uscita nei gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="7dd38-104">Network Security Group flow logs allow you to view information about ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="7dd38-105">Questi log mostrano i flussi in ingresso e in uscita in base a regole, la scheda di rete a cui si applica il flusso, informazioni a 5 tuple sul flusso, ad esempio l'indirizzo IP di origine/destinazione, la porta di origine/destinazione o il protocollo, e se il traffico è stato consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="7dd38-105">These flow logs show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="7dd38-106">Cercando manualmente nei file di log può essere difficile ottenere informazioni dettagliate sui dati di log dei flussi.</span><span class="sxs-lookup"><span data-stu-id="7dd38-106">It can be difficult to gain insights into flow logging data by manually searching the log files.</span></span> <span data-ttu-id="7dd38-107">Questo articolo offre una soluzione per visualizzare i log dei flussi più recenti e ottenere informazioni sul traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="7dd38-107">In this article, we provide a solution to visualize your most recent flow logs and learn about traffic on your network.</span></span>

## <a name="scenario"></a><span data-ttu-id="7dd38-108">Scenario</span><span class="sxs-lookup"><span data-stu-id="7dd38-108">Scenario</span></span>

<span data-ttu-id="7dd38-109">Nello scenario seguente Power BI Desktop viene connesso all'account di archiviazione configurato come sink per i dati di registrazione dei flussi dei gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="7dd38-109">In the following scenario, we connect Power BI desktop to the storage account we have configured as the sink for our NSG Flow Logging data.</span></span> <span data-ttu-id="7dd38-110">Dopo la connessione all'account di archiviazione, Power BI scarica e analizza i log per fornire una rappresentazione visiva del traffico registrato dai gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="7dd38-110">After we connect to our storage account, Power BI downloads and parses the logs to provide a visual representation of the traffic that is logged by Network Security groups.</span></span>

<span data-ttu-id="7dd38-111">Usando gli oggetti visivi inclusi nel modello è possibile esaminare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="7dd38-111">Using the visuals supplied in the template you can examine:</span></span>

* <span data-ttu-id="7dd38-112">Talker principali</span><span class="sxs-lookup"><span data-stu-id="7dd38-112">Top Talkers</span></span>
* <span data-ttu-id="7dd38-113">Dati di flusso della serie temporale in base alla direzione e alla regola decisa</span><span class="sxs-lookup"><span data-stu-id="7dd38-113">Time Series Flow Data by direction and rule decision</span></span>
* <span data-ttu-id="7dd38-114">Flussi in base all'indirizzo MAC dell'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="7dd38-114">Flows by Network Interface MAC address</span></span>
* <span data-ttu-id="7dd38-115">Flussi in base al gruppo di sicurezza di rete e alla regola</span><span class="sxs-lookup"><span data-stu-id="7dd38-115">Flows by NSG and Rule</span></span>
* <span data-ttu-id="7dd38-116">Flussi in base alla porta di destinazione</span><span class="sxs-lookup"><span data-stu-id="7dd38-116">Flows by Destination Port</span></span>

<span data-ttu-id="7dd38-117">Il modello incluso è modificabile. È quindi possibile aggiungervi nuovi dati e oggetti visivi o modificare le query in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="7dd38-117">The template provided is editable so you can modify it to add new data, visuals, or edit queries to suit your needs.</span></span>

## <a name="setup"></a><span data-ttu-id="7dd38-118">Configurazione</span><span class="sxs-lookup"><span data-stu-id="7dd38-118">Setup</span></span>

<span data-ttu-id="7dd38-119">Prima di iniziare, è necessario abilitare la registrazione dei flussi dei gruppi di sicurezza di rete in uno o più gruppi di sicurezza di rete nell'account usato.</span><span class="sxs-lookup"><span data-stu-id="7dd38-119">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="7dd38-120">Per istruzioni in proposito, vedere [Introduzione alla registrazione dei flussi per i gruppi di sicurezza di rete](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7dd38-120">For instructions on enabling Network Security flow logs, refer to the following article: [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="7dd38-121">È necessario che il client di Power BI Desktop sia installato nel computer e che lo spazio disponibile nel computer sia sufficiente per scaricare e caricare i dati di log presenti nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7dd38-121">You must also have the Power BI Desktop client installed on your machine, and enough free space on your machine to download and load the log data that exists in your storage account.</span></span>

![Diagramma di Visio][1]

### <a name="steps"></a><span data-ttu-id="7dd38-123">Passi</span><span class="sxs-lookup"><span data-stu-id="7dd38-123">Steps</span></span>

1. <span data-ttu-id="7dd38-124">Scaricare e aprire il [modello di log dei flussi Power BI di Network Watcher](https://aka.ms/networkwatcherpowerbiflowlogstemplate) nell'applicazione Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="7dd38-124">Download and open the following Power BI template in the Power BI Desktop Application [Network Watcher PowerBI flow logs template](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span></span>
1. <span data-ttu-id="7dd38-125">Immettere i parametri di query obbligatori.</span><span class="sxs-lookup"><span data-stu-id="7dd38-125">Enter the required Query parameters</span></span>
    1. <span data-ttu-id="7dd38-126">**StorageAccountName**: specifica il nome dell'account di archiviazione contenente i log dei flussi dei gruppi di sicurezza di rete da caricare e visualizzare.</span><span class="sxs-lookup"><span data-stu-id="7dd38-126">**StorageAccountName** – Specifies to the name of the storage account containing the NSG flow logs that you would like to load and visualize.</span></span>
    1. <span data-ttu-id="7dd38-127">**NumberOfLogFiles**: specifica il numero di file di log da scaricare e visualizzare in Power BI.</span><span class="sxs-lookup"><span data-stu-id="7dd38-127">**NumberOfLogFiles** – Specifies the number of log files that you would like to download and visualize in Power BI.</span></span> <span data-ttu-id="7dd38-128">Ad esempio, se si specifica 50, vengono scaricati e visualizzati i 50 file di log più recenti.</span><span class="sxs-lookup"><span data-stu-id="7dd38-128">For example, if 50 is specified, the 50 latest log files.</span></span> <span data-ttu-id="7dd38-129">Se vengono abilitati e configurati due gruppi di sicurezza di rete per l'invio di log dei flussi dei gruppi di sicurezza di rete a questo account, è possibile visualizzare i log corrispondenti alle ultime 25 ore.</span><span class="sxs-lookup"><span data-stu-id="7dd38-129">Ff we have 2 NSGs enabled and configured to send NSG flow logs to this account, then the past 25 hours of logs can be viewed.</span></span>

    ![schermata principale di Power BI][2]

1. <span data-ttu-id="7dd38-131">Immettere la chiave di accesso per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7dd38-131">Enter the Access Key for your storage account.</span></span> <span data-ttu-id="7dd38-132">Per trovare le chiavi di accesso valide, accedere all'account di archiviazione nel portale di Azure e selezionare **Chiavi di accesso** dal menu Impostazioni.</span><span class="sxs-lookup"><span data-stu-id="7dd38-132">You can find valid access keys by navigating to your storage account in the Azure portal and selecting **Access Keys** from the Settings menu.</span></span> <span data-ttu-id="7dd38-133">Fare clic su **Connetti** e quindi applicare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="7dd38-133">Click **Connect** then apply changes.</span></span>

    ![chiavi di accesso][3]

    ![chiave di accesso 2][4]

4.  <span data-ttu-id="7dd38-136">I log vengono scaricati e analizzati ed è quindi possibile usare gli oggetti visivi creati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="7dd38-136">Your logs are download and parsed and you can now utilize the pre-created visuals.</span></span>

## <a name="understanding-the-visuals"></a><span data-ttu-id="7dd38-137">Informazioni sugli oggetti visivi</span><span class="sxs-lookup"><span data-stu-id="7dd38-137">Understanding the visuals</span></span>

<span data-ttu-id="7dd38-138">Il modello include un set di oggetti visivi che aiutano a comprendere i dati dei registri dei flussi dei gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="7dd38-138">Provided in the template are a set of visuals that help make sense of the NSG Flow Log data.</span></span> <span data-ttu-id="7dd38-139">Le immagini seguenti mostrano un esempio dell'aspetto del dashboard popolato con i dati.</span><span class="sxs-lookup"><span data-stu-id="7dd38-139">The following images show a sample of what the dashboard looks like when populated with data.</span></span> <span data-ttu-id="7dd38-140">Di seguito vengono esaminati in dettaglio i singoli oggetti visivi</span><span class="sxs-lookup"><span data-stu-id="7dd38-140">Below we examine each visual in greater detail</span></span> 

![Power BI][5]
 
<span data-ttu-id="7dd38-142">L'oggetto visivo Top Talkers (Talker principali) mostra gli indirizzi IP che hanno avviato il maggior numero di connessioni nel periodo specificato.</span><span class="sxs-lookup"><span data-stu-id="7dd38-142">The Top Talkers visual shows the IPs that have initiated the most connections over the period specified.</span></span> <span data-ttu-id="7dd38-143">La dimensione delle caselle corrisponde al relativo numero di connessioni.</span><span class="sxs-lookup"><span data-stu-id="7dd38-143">The size of the boxes corresponds to the relative number of connections.</span></span> 

![Top Talkers][6]

<span data-ttu-id="7dd38-145">I grafici di serie temporali riportati di seguito mostrano il numero dei flussi nel periodo specificato.</span><span class="sxs-lookup"><span data-stu-id="7dd38-145">The following time series graphs show the number of flows over the period.</span></span> <span data-ttu-id="7dd38-146">Il grafico superiore è segmentato in base alla direzione del flusso, mentre quello inferiore è segmentato in base alla decisione presa, ovvero consenso o negazione.</span><span class="sxs-lookup"><span data-stu-id="7dd38-146">The upper graph is segmented by the flow direction, and the lower is segmented by the decision made (allow or deny).</span></span> <span data-ttu-id="7dd38-147">Con questo oggetto visivo è possibile esaminare le tendenze relative al traffico nel tempo e identificare eventuali cali o picchi anomali nel traffico o nella sua segmentazione.</span><span class="sxs-lookup"><span data-stu-id="7dd38-147">With this visual, you can examine your traffic trends over time, and spot any abnormal spikes or decline in traffic or traffic segmentation.</span></span>

![flussi nel periodo][7]

<span data-ttu-id="7dd38-149">I grafici seguenti mostrano i flussi per ogni interfaccia di rete. Il grafico superiore è segmentato in base alla direzione dei flussi, mentre quello inferiore è segmentato in base alla decisione presa.</span><span class="sxs-lookup"><span data-stu-id="7dd38-149">The following graphs show the flows per Network interface, with the upper segmented by flow direction and the lower segmented by decision made.</span></span> <span data-ttu-id="7dd38-150">Questi dati permettono di ottenere informazioni dettagliate sulla macchina virtuale che ha comunicato di più rispetto alle altre e sul traffico consentito o negato verso una determinata macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7dd38-150">With this information, you can gain insights into which of your VMs communicated the most relative to others, and if traffic to a specific VM is being allowed or denied.</span></span>

![flussi per scheda di rete][8]

<span data-ttu-id="7dd38-152">Il grafico ad anello riportato di seguito mostra una suddivisione dei flussi in base alla porta di destinazione.</span><span class="sxs-lookup"><span data-stu-id="7dd38-152">The following donut wheel chart shows a breakdown of Flows by Destination Port.</span></span> <span data-ttu-id="7dd38-153">Con queste informazioni è possibile visualizzare le porte di destinazione più usate nel periodo specificato.</span><span class="sxs-lookup"><span data-stu-id="7dd38-153">With this information, you can view the most commonly used destination ports used within the specified period.</span></span>

![grafico ad anello][9]

<span data-ttu-id="7dd38-155">Il grafico a barre riportato di seguito mostra i flussi in base ai gruppi di sicurezza di rete e alle regole.</span><span class="sxs-lookup"><span data-stu-id="7dd38-155">The following bar chart shows the Flow by NSG and Rule.</span></span> <span data-ttu-id="7dd38-156">Con queste informazioni è possibile visualizzare i gruppi di sicurezza di rete responsabili della maggior parte del traffico e la suddivisione del traffico in un gruppo di sicurezza di rete in base alle regole.</span><span class="sxs-lookup"><span data-stu-id="7dd38-156">With this information, you can see the NSGs responsible for the most traffic, and the breakdown of traffic on an NSG by rule.</span></span>

![grafico a barre][10]
 
<span data-ttu-id="7dd38-158">I grafici informativi riportati di seguito mostrano i gruppi di sicurezza di rete presenti nei log, il numero di flussi acquisiti nel periodo specificato e la data del log acquisito più di recente.</span><span class="sxs-lookup"><span data-stu-id="7dd38-158">The following informational charts display information about the NSGs present in the logs, the number of Flows captured over the period, and the date of the earliest log captured.</span></span> <span data-ttu-id="7dd38-159">Queste informazioni permettono di capire quali gruppi di sicurezza di rete vengono registrati e l'intervallo di date dei flussi.</span><span class="sxs-lookup"><span data-stu-id="7dd38-159">This information gives you an idea of what NSGs are being logged and the date range of flows.</span></span>

![grafico informativo 1][11]

![grafico informativo 2][12]

<span data-ttu-id="7dd38-162">Questo modello include i filtri dei dati indicati di seguito, che permettono di visualizzare solo i dati rilevanti.</span><span class="sxs-lookup"><span data-stu-id="7dd38-162">This template includes the following slicers to allow you to view only the data you are most interested in.</span></span> <span data-ttu-id="7dd38-163">È possibile applicare filtri ai gruppi di risorse, ai gruppi di sicurezza di rete e alle regole.</span><span class="sxs-lookup"><span data-stu-id="7dd38-163">You can filter on your resource groups, NSGs, and rules.</span></span> <span data-ttu-id="7dd38-164">È anche possibile applicare filtri alle informazioni a 5 tuple, alle decisioni e all'orario di scrittura del log.</span><span class="sxs-lookup"><span data-stu-id="7dd38-164">You can also filter on 5-tuple information, decision, and the time the log was written.</span></span>

![filtri dei dati][13]

## <a name="conclusion"></a><span data-ttu-id="7dd38-166">Conclusione</span><span class="sxs-lookup"><span data-stu-id="7dd38-166">Conclusion</span></span>

<span data-ttu-id="7dd38-167">Questo scenario ha permesso di dimostrare come l'uso dei registri dei flussi dei gruppi di sicurezza di rete inclusi in Network Watcher e Power BI permetta di visualizzare e comprendere il traffico.</span><span class="sxs-lookup"><span data-stu-id="7dd38-167">We showed in this scenario that by using Network Security Group Flow logs provided by Network Watcher and Power BI, we are able to visualize and understand the traffic.</span></span> <span data-ttu-id="7dd38-168">Usando il modello incluso, Power BI scarica i log direttamente dall'archivio e li elabora in locale.</span><span class="sxs-lookup"><span data-stu-id="7dd38-168">Using the provided template, Power BI downloads the logs directly from storage and processes them locally.</span></span> <span data-ttu-id="7dd38-169">Il tempo necessario a caricare il modello varia a seconda del numero di file richiesti e della dimensione totale dei file scaricati.</span><span class="sxs-lookup"><span data-stu-id="7dd38-169">Time taken to load the template varies depending on the number of files requested and total size of files downloaded.</span></span>

<span data-ttu-id="7dd38-170">È possibile personalizzare il modello in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="7dd38-170">Feel free to customize this template for your needs.</span></span> <span data-ttu-id="7dd38-171">Power BI e i log dei flussi dei gruppi di sicurezza di rete possono essere usati in molti modi diversi.</span><span class="sxs-lookup"><span data-stu-id="7dd38-171">There are many numerous ways that you can use Power BI with Network Security Group Flow Logs.</span></span> 

## <a name="notes"></a><span data-ttu-id="7dd38-172">Note</span><span class="sxs-lookup"><span data-stu-id="7dd38-172">Notes</span></span>

* <span data-ttu-id="7dd38-173">Per impostazione predefinita, i log vengono archiviati in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span><span class="sxs-lookup"><span data-stu-id="7dd38-173">Logs by default are stored in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span></span>

    * <span data-ttu-id="7dd38-174">Se esistono altri dati in un'altra directory, è necessario modificare le query per il pull e l'elaborazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="7dd38-174">If other data exists in another directory they the queries to pull and process the data must be modified.</span></span>

* <span data-ttu-id="7dd38-175">Non è consigliabile usare il modello incluso con più di 1 GB di log.</span><span class="sxs-lookup"><span data-stu-id="7dd38-175">The provided template is not recommended for use with more than 1 GB of logs.</span></span>

* <span data-ttu-id="7dd38-176">In presenza di una grande quantità di log, è consigliabile prendere in considerazione una soluzione con un altro archivio dati, come Data Lake o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7dd38-176">If you have a large amount of logs, we recommend that you investigate a solution using another data store like Data Lake or SQL server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7dd38-177">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7dd38-177">Next Steps</span></span>

<span data-ttu-id="7dd38-178">Per informazioni su come visualizzare i log dei flussi dei gruppi di sicurezza di rete con Elastick Stack, vedere [Visualize network traffic patterns to and from your VMs using open source tools](network-watcher-using-open-source-tools.md) (Visualizzare i modelli di traffico di rete da e verso le macchine virtuali con strumenti open source)</span><span class="sxs-lookup"><span data-stu-id="7dd38-178">Learn how to visualize your NSG flow logs with the Elastick Stack by visiting [Visualize network traffic patterns to and from your VMs using open source tools](network-watcher-using-open-source-tools.md)</span></span>

[1]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure7.png
[8]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure8.png
[9]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure9.png
[10]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure10.png
[11]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure11.png
[12]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure12.png
[13]: ./media/network-watcher-visualize-nsg-flow-logs-power-bi/figure13.png
