---
title: flusso di Azure Network Security Group aaaVisualizing registra con Power BI | Documenti Microsoft
description: Questa pagina vengono descritti come flusso NSG toovisualize registra con Power BI.
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
ms.openlocfilehash: d9adcf256df8fed68c39be1a026ca64cc6b5c6d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="visualizing-network-security-group-flow-logs-with-power-bi"></a><span data-ttu-id="5e84c-103">Visualizzare i log dei flussi dei gruppi di sicurezza di rete con Power BI</span><span class="sxs-lookup"><span data-stu-id="5e84c-103">Visualizing Network Security Group flow logs with Power BI</span></span>

<span data-ttu-id="5e84c-104">I registri del flusso di gruppo di sicurezza di rete consentono di tooview informazioni sul traffico IP in ingresso e uscita sui gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="5e84c-104">Network Security Group flow logs allow you tooview information about ingress and egress IP traffic on Network Security Groups.</span></span> <span data-ttu-id="5e84c-105">Questi log flusso mostrano in uscita e i flussi in ingresso per ogni regola, hello flusso hello NIC applica, 5 tuple informazioni flusso hello (origine/destinazione IP, porta di origine/destinazione, Protocol), e se il traffico hello consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="5e84c-105">These flow logs show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="5e84c-106">Può essere difficile toogain approfondite del flusso di registrazione dei dati tramite la ricerca di file di log hello manualmente.</span><span class="sxs-lookup"><span data-stu-id="5e84c-106">It can be difficult toogain insights into flow logging data by manually searching hello log files.</span></span> <span data-ttu-id="5e84c-107">In questo articolo è fornire una soluzione toovisualize più recente del flusso di log e apprendere il traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="5e84c-107">In this article, we provide a solution toovisualize your most recent flow logs and learn about traffic on your network.</span></span>

## <a name="scenario"></a><span data-ttu-id="5e84c-108">Scenario</span><span class="sxs-lookup"><span data-stu-id="5e84c-108">Scenario</span></span>

<span data-ttu-id="5e84c-109">Connessione è hello seguente scenario, è stato configurato come sink hello per i dati di flusso di registrazione NSG account di archiviazione di Power BI desktop toohello.</span><span class="sxs-lookup"><span data-stu-id="5e84c-109">In hello following scenario, we connect Power BI desktop toohello storage account we have configured as hello sink for our NSG Flow Logging data.</span></span> <span data-ttu-id="5e84c-110">Dopo la connessione di account di archiviazione tooour, Power BI Scarica e analizza hello registri tooprovide una rappresentazione visiva del traffico hello che viene registrato tramite gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="5e84c-110">After we connect tooour storage account, Power BI downloads and parses hello logs tooprovide a visual representation of hello traffic that is logged by Network Security groups.</span></span>

<span data-ttu-id="5e84c-111">Utilizzo di oggetti visivi hello forniti nel modello di hello che è possibile esaminare:</span><span class="sxs-lookup"><span data-stu-id="5e84c-111">Using hello visuals supplied in hello template you can examine:</span></span>

* <span data-ttu-id="5e84c-112">Talker principali</span><span class="sxs-lookup"><span data-stu-id="5e84c-112">Top Talkers</span></span>
* <span data-ttu-id="5e84c-113">Dati di flusso della serie temporale in base alla direzione e alla regola decisa</span><span class="sxs-lookup"><span data-stu-id="5e84c-113">Time Series Flow Data by direction and rule decision</span></span>
* <span data-ttu-id="5e84c-114">Flussi in base all'indirizzo MAC dell'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="5e84c-114">Flows by Network Interface MAC address</span></span>
* <span data-ttu-id="5e84c-115">Flussi in base al gruppo di sicurezza di rete e alla regola</span><span class="sxs-lookup"><span data-stu-id="5e84c-115">Flows by NSG and Rule</span></span>
* <span data-ttu-id="5e84c-116">Flussi in base alla porta di destinazione</span><span class="sxs-lookup"><span data-stu-id="5e84c-116">Flows by Destination Port</span></span>

<span data-ttu-id="5e84c-117">modello di Hello fornito non è modificabile in modo è possibile modificarlo tooadd nuovi dati, gli oggetti visivi, o modificare query toosuit le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="5e84c-117">hello template provided is editable so you can modify it tooadd new data, visuals, or edit queries toosuit your needs.</span></span>

## <a name="setup"></a><span data-ttu-id="5e84c-118">Configurazione</span><span class="sxs-lookup"><span data-stu-id="5e84c-118">Setup</span></span>

<span data-ttu-id="5e84c-119">Prima di iniziare, è necessario abilitare la registrazione dei flussi dei gruppi di sicurezza di rete in uno o più gruppi di sicurezza di rete nell'account usato.</span><span class="sxs-lookup"><span data-stu-id="5e84c-119">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="5e84c-120">Flusso di log per istruzioni sull'abilitazione di sicurezza di rete, consultare l'articolo seguente toohello: [registrazione tooflow introduzione per gruppi di sicurezza di rete](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5e84c-120">For instructions on enabling Network Security flow logs, refer toohello following article: [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="5e84c-121">È inoltre necessario il client di Power BI Desktop hello installato nel computer in uso e sufficiente spazio libero nel computer toodownload e carico hello log dati che è presente nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5e84c-121">You must also have hello Power BI Desktop client installed on your machine, and enough free space on your machine toodownload and load hello log data that exists in your storage account.</span></span>

![Diagramma di Visio][1]

### <a name="steps"></a><span data-ttu-id="5e84c-123">Passi</span><span class="sxs-lookup"><span data-stu-id="5e84c-123">Steps</span></span>

1. <span data-ttu-id="5e84c-124">Scaricare e aprire hello segue il modello di Power BI in Power BI Desktop applicazione hello [flusso PowerBI Watcher di rete registri modello](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span><span class="sxs-lookup"><span data-stu-id="5e84c-124">Download and open hello following Power BI template in hello Power BI Desktop Application [Network Watcher PowerBI flow logs template](https://aka.ms/networkwatcherpowerbiflowlogstemplate)</span></span>
1. <span data-ttu-id="5e84c-125">Immettere i parametri di Query hello richiesto</span><span class="sxs-lookup"><span data-stu-id="5e84c-125">Enter hello required Query parameters</span></span>
    1. <span data-ttu-id="5e84c-126">**StorageAccountName** – toohello specifica il nome dell'account di archiviazione hello contenente il flusso NSG hello log che si desideri tooload e visualizzare.</span><span class="sxs-lookup"><span data-stu-id="5e84c-126">**StorageAccountName** – Specifies toohello name of hello storage account containing hello NSG flow logs that you would like tooload and visualize.</span></span>
    1. <span data-ttu-id="5e84c-127">**NumberOfLogFiles** : Specifica il numero di hello del file di log che desideri toodownload e visualizzare in Power BI.</span><span class="sxs-lookup"><span data-stu-id="5e84c-127">**NumberOfLogFiles** – Specifies hello number of log files that you would like toodownload and visualize in Power BI.</span></span> <span data-ttu-id="5e84c-128">Ad esempio, se si specifica 50, hello 50 file di log più recenti.</span><span class="sxs-lookup"><span data-stu-id="5e84c-128">For example, if 50 is specified, hello 50 latest log files.</span></span> <span data-ttu-id="5e84c-129">Abbiamo 2 NSGs FF abilitata e configurata toosend NSG flusso registri toothis account, quindi hello nelle ultime 25 ore dei log possono essere visualizzate.</span><span class="sxs-lookup"><span data-stu-id="5e84c-129">Ff we have 2 NSGs enabled and configured toosend NSG flow logs toothis account, then hello past 25 hours of logs can be viewed.</span></span>

    ![schermata principale di Power BI][2]

1. <span data-ttu-id="5e84c-131">Immettere la chiave di accesso dell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="5e84c-131">Enter hello Access Key for your storage account.</span></span> <span data-ttu-id="5e84c-132">È possibile trovare le chiavi di accesso valido passando tooyour account di archiviazione in Azure nel portale e selezionando hello **chiavi di accesso** dal menu Impostazioni hello.</span><span class="sxs-lookup"><span data-stu-id="5e84c-132">You can find valid access keys by navigating tooyour storage account in hello Azure portal and selecting **Access Keys** from hello Settings menu.</span></span> <span data-ttu-id="5e84c-133">Fare clic su **Connetti** e quindi applicare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="5e84c-133">Click **Connect** then apply changes.</span></span>

    ![chiavi di accesso][3]

    ![chiave di accesso 2][4]

4.  <span data-ttu-id="5e84c-136">I log sono scaricare e analizzato e ora è possibile utilizzare gli oggetti visivi creati in precedenza hello.</span><span class="sxs-lookup"><span data-stu-id="5e84c-136">Your logs are download and parsed and you can now utilize hello pre-created visuals.</span></span>

## <a name="understanding-hello-visuals"></a><span data-ttu-id="5e84c-137">Comprendere gli oggetti visivi hello</span><span class="sxs-lookup"><span data-stu-id="5e84c-137">Understanding hello visuals</span></span>

<span data-ttu-id="5e84c-138">Condizione in hello modello sono un set di oggetti visivi che consentono di senso di hello dati gruppo flusso di Log.</span><span class="sxs-lookup"><span data-stu-id="5e84c-138">Provided in hello template are a set of visuals that help make sense of hello NSG Flow Log data.</span></span> <span data-ttu-id="5e84c-139">Hello immagini seguenti mostrano un esempio dell'aspetto quando popolata con dati quale dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="5e84c-139">hello following images show a sample of what hello dashboard looks like when populated with data.</span></span> <span data-ttu-id="5e84c-140">Di seguito vengono esaminati in dettaglio i singoli oggetti visivi</span><span class="sxs-lookup"><span data-stu-id="5e84c-140">Below we examine each visual in greater detail</span></span> 

![Power BI][5]
 
<span data-ttu-id="5e84c-142">Talkers Top Hello Mostra visual hello gli indirizzi IP che hanno avviato hello la maggior parte delle connessioni su hello periodo specificato.</span><span class="sxs-lookup"><span data-stu-id="5e84c-142">hello Top Talkers visual shows hello IPs that have initiated hello most connections over hello period specified.</span></span> <span data-ttu-id="5e84c-143">dimensioni di Hello delle caselle hello corrispondono toohello numero di connessioni.</span><span class="sxs-lookup"><span data-stu-id="5e84c-143">hello size of hello boxes corresponds toohello relative number of connections.</span></span> 

![Top Talkers][6]

<span data-ttu-id="5e84c-145">Hello grafici di serie temporali seguente mostrano il numero di hello di flussi periodo hello.</span><span class="sxs-lookup"><span data-stu-id="5e84c-145">hello following time series graphs show hello number of flows over hello period.</span></span> <span data-ttu-id="5e84c-146">grafico superiore Hello è segmentata per la direzione di flusso hello e hello inferiore è segmentata per decisione hello (Consenti o Nega).</span><span class="sxs-lookup"><span data-stu-id="5e84c-146">hello upper graph is segmented by hello flow direction, and hello lower is segmented by hello decision made (allow or deny).</span></span> <span data-ttu-id="5e84c-147">Con questo oggetto visivo è possibile esaminare le tendenze relative al traffico nel tempo e identificare eventuali cali o picchi anomali nel traffico o nella sua segmentazione.</span><span class="sxs-lookup"><span data-stu-id="5e84c-147">With this visual, you can examine your traffic trends over time, and spot any abnormal spikes or decline in traffic or traffic segmentation.</span></span>

![flussi nel periodo][7]

<span data-ttu-id="5e84c-149">Hello seguenti grafici mostrano flussi hello per ogni interfaccia di rete, con segmentate per la direzione di flusso hello superiore e inferiore hello segmentate per decisione presa.</span><span class="sxs-lookup"><span data-stu-id="5e84c-149">hello following graphs show hello flows per Network interface, with hello upper segmented by flow direction and hello lower segmented by decision made.</span></span> <span data-ttu-id="5e84c-150">Con queste informazioni, è possibile ottenere informazioni approfondite che delle macchine virtuali comunicate hello tooothers relativo la maggior parte delle e se il traffico tooa macchina virtuale specifica viene consentito o negato.</span><span class="sxs-lookup"><span data-stu-id="5e84c-150">With this information, you can gain insights into which of your VMs communicated hello most relative tooothers, and if traffic tooa specific VM is being allowed or denied.</span></span>

![flussi per scheda di rete][8]

<span data-ttu-id="5e84c-152">Hello seguente grafico rotellina ad anello mostri una suddivisione di flussi dalla porta di destinazione.</span><span class="sxs-lookup"><span data-stu-id="5e84c-152">hello following donut wheel chart shows a breakdown of Flows by Destination Port.</span></span> <span data-ttu-id="5e84c-153">Con queste informazioni, è possibile visualizzare le porte di destinazione hello usato più comunemente utilizzate all'interno di hello specificato periodo.</span><span class="sxs-lookup"><span data-stu-id="5e84c-153">With this information, you can view hello most commonly used destination ports used within hello specified period.</span></span>

![grafico ad anello][9]

<span data-ttu-id="5e84c-155">Hello seguente grafico a barre mostra hello flusso dal gruppo e regola.</span><span class="sxs-lookup"><span data-stu-id="5e84c-155">hello following bar chart shows hello Flow by NSG and Rule.</span></span> <span data-ttu-id="5e84c-156">Con queste informazioni, è possibile vedere hello NSGs responsabile hello la maggior parte del traffico e suddivisione hello del traffico in un gruppo dalla regola.</span><span class="sxs-lookup"><span data-stu-id="5e84c-156">With this information, you can see hello NSGs responsible for hello most traffic, and hello breakdown of traffic on an NSG by rule.</span></span>

![grafico a barre][10]
 
<span data-ttu-id="5e84c-158">Hello seguenti grafici informativo visualizzato informazioni sulla NSGs hello presenti nei registri hello, hello numero di flussi acquisite nel periodo di hello e data hello del log primo di hello acquisiti.</span><span class="sxs-lookup"><span data-stu-id="5e84c-158">hello following informational charts display information about hello NSGs present in hello logs, hello number of Flows captured over hello period, and hello date of hello earliest log captured.</span></span> <span data-ttu-id="5e84c-159">Queste informazioni consentono un'idea dei quali NSGs vengono registrate e hello intervallo di date di flussi.</span><span class="sxs-lookup"><span data-stu-id="5e84c-159">This information gives you an idea of what NSGs are being logged and hello date range of flows.</span></span>

![grafico informativo 1][11]

![grafico informativo 2][12]

<span data-ttu-id="5e84c-162">Questo modello include hello tooallow i filtri dei dati in seguito si tooview solo hello i dati è interessati.</span><span class="sxs-lookup"><span data-stu-id="5e84c-162">This template includes hello following slicers tooallow you tooview only hello data you are most interested in.</span></span> <span data-ttu-id="5e84c-163">È possibile applicare filtri ai gruppi di risorse, ai gruppi di sicurezza di rete e alle regole.</span><span class="sxs-lookup"><span data-stu-id="5e84c-163">You can filter on your resource groups, NSGs, and rules.</span></span> <span data-ttu-id="5e84c-164">È anche possibile filtrare informazioni 5 tuple, delle decisioni e ora di hello log hello è stato scritto.</span><span class="sxs-lookup"><span data-stu-id="5e84c-164">You can also filter on 5-tuple information, decision, and hello time hello log was written.</span></span>

![filtri dei dati][13]

## <a name="conclusion"></a><span data-ttu-id="5e84c-166">Conclusioni</span><span class="sxs-lookup"><span data-stu-id="5e84c-166">Conclusion</span></span>

<span data-ttu-id="5e84c-167">Abbiamo anche mostrato in questo scenario che utilizzando i registri di gruppo di sicurezza di rete flusso forniti da Watcher di rete e di Power BI, è sono in grado di toovisualize e comprendere il traffico di hello.</span><span class="sxs-lookup"><span data-stu-id="5e84c-167">We showed in this scenario that by using Network Security Group Flow logs provided by Network Watcher and Power BI, we are able toovisualize and understand hello traffic.</span></span> <span data-ttu-id="5e84c-168">Power BI usando il modello di hello fornito, il download dei log hello direttamente dall'archivio e li elabora in locale.</span><span class="sxs-lookup"><span data-stu-id="5e84c-168">Using hello provided template, Power BI downloads hello logs directly from storage and processes them locally.</span></span> <span data-ttu-id="5e84c-169">Modello di tempo impiegato tooload hello varia a seconda numero hello di file richiesti e le dimensioni totali dei file scaricati.</span><span class="sxs-lookup"><span data-stu-id="5e84c-169">Time taken tooload hello template varies depending on hello number of files requested and total size of files downloaded.</span></span>

<span data-ttu-id="5e84c-170">È gratuito toocustomize questo modello per le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="5e84c-170">Feel free toocustomize this template for your needs.</span></span> <span data-ttu-id="5e84c-171">Power BI e i log dei flussi dei gruppi di sicurezza di rete possono essere usati in molti modi diversi.</span><span class="sxs-lookup"><span data-stu-id="5e84c-171">There are many numerous ways that you can use Power BI with Network Security Group Flow Logs.</span></span> 

## <a name="notes"></a><span data-ttu-id="5e84c-172">Note</span><span class="sxs-lookup"><span data-stu-id="5e84c-172">Notes</span></span>

* <span data-ttu-id="5e84c-173">Per impostazione predefinita, i log vengono archiviati in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span><span class="sxs-lookup"><span data-stu-id="5e84c-173">Logs by default are stored in `https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/`</span></span>

    * <span data-ttu-id="5e84c-174">Se esistono altri dati in un'altra directory sono hello toopull query e dati hello processo devono essere modificati.</span><span class="sxs-lookup"><span data-stu-id="5e84c-174">If other data exists in another directory they hello queries toopull and process hello data must be modified.</span></span>

* <span data-ttu-id="5e84c-175">modello Hello fornito non è consigliabile usare con più di 1 GB di log.</span><span class="sxs-lookup"><span data-stu-id="5e84c-175">hello provided template is not recommended for use with more than 1 GB of logs.</span></span>

* <span data-ttu-id="5e84c-176">In presenza di una grande quantità di log, è consigliabile prendere in considerazione una soluzione con un altro archivio dati, come Data Lake o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5e84c-176">If you have a large amount of logs, we recommend that you investigate a solution using another data store like Data Lake or SQL server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e84c-177">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5e84c-177">Next Steps</span></span>

<span data-ttu-id="5e84c-178">Informazioni su come toovisualize il flusso di gruppo Registra con hello Elastick Stack visitando [visualizzare tooand di modelli di traffico di rete dalle macchine virtuali utilizzando strumenti open source](network-watcher-using-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="5e84c-178">Learn how toovisualize your NSG flow logs with hello Elastick Stack by visiting [Visualize network traffic patterns tooand from your VMs using open source tools](network-watcher-using-open-source-tools.md)</span></span>

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
