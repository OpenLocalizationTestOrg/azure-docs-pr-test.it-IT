---
title: Indicazione delle impostazioni DNS in un file di configurazione di rete virtuale | Documentazione Microsoft
description: Come modificare le impostazioni del server DNS in una rete virtuale usando un file di configurazione di rete virtuale nel modello di distribuzione classica
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a8905927-92ac-42b5-8c33-8e42c000692c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: ec33268915a1888509834ce6a5b2bc782a12ce4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a><span data-ttu-id="be8c3-103">Indicazione delle impostazioni DNS in un file di configurazione di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="be8c3-103">Specifying DNS settings in a virtual network configuration file</span></span>
<span data-ttu-id="be8c3-104">Un file di configurazione di rete dispone di due elementi che è possibile usare per specificare le impostazioni Domain Name System (DNS): **DnsServers** e **DnsServerRef**.</span><span class="sxs-lookup"><span data-stu-id="be8c3-104">A network configuration file has two elements that you can use to specify Domain Name System (DNS) settings: **DnsServers** and **DnsServerRef**.</span></span> <span data-ttu-id="be8c3-105">È possibile aggiungere un elenco dei server DNS specificando gli indirizzi IP e nomi di riferimento all’elemento **DnsServers** .</span><span class="sxs-lookup"><span data-stu-id="be8c3-105">You can add a list of DNS servers by specifying their IP addresses and reference names to the **DnsServers** element.</span></span> <span data-ttu-id="be8c3-106">È quindi possibile utilizzare un elemento **DnsServerRef** per specificare le voci del server DNS che vengono utilizzate per siti di rete diversi all'interno della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="be8c3-106">You can then use a **DnsServerRef** element to specify which DNS server entries from the DnsServers element are used for different network sites within your virtual network.</span></span>

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="be8c3-107">In questo articolo viene illustrato il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="be8c3-107">This article covers the classic deployment model.</span></span>

<span data-ttu-id="be8c3-108">Il file di configurazione di rete può contenere i seguenti elementi.</span><span class="sxs-lookup"><span data-stu-id="be8c3-108">The network configuration file may contain the following elements.</span></span> <span data-ttu-id="be8c3-109">Il titolo di ogni elemento è collegato a una pagina che fornisce informazioni aggiuntive sulle impostazioni del valore dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="be8c3-109">The title of each element is linked to a page that provides additional information about the element value settings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="be8c3-110">Per altre informazioni sull'utilizzo del file di configurazione di rete, vedere [Configurare una rete virtuale usando un file di configurazione di rete](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="be8c3-110">For information about how to configure the network configuration file, see [Configure a Virtual Network Using a Network Configuration File](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="be8c3-111">Per informazioni sulle impostazioni specifiche contenute in un file di configurazione di rete, vedere [Schema di configurazione di rete virtuale Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="be8c3-111">For information about each element contained in the network configuration file, see [Azure Virtual Network Configuration Schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
> 
> 

[<span data-ttu-id="be8c3-112">Elemento DNS</span><span class="sxs-lookup"><span data-stu-id="be8c3-112">Dns Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> <span data-ttu-id="be8c3-113">L'attributo **nome** dell'elemento **DnsServer** viene usato solo come riferimento per l'elemento **DnsServerRef**.</span><span class="sxs-lookup"><span data-stu-id="be8c3-113">The **name** attribute in the **DnsServer** element is used only as a reference for the **DnsServerRef** element.</span></span> <span data-ttu-id="be8c3-114">Non rappresenta il nome host per il server DNS.</span><span class="sxs-lookup"><span data-stu-id="be8c3-114">It does not represent the host name for the DNS server.</span></span> <span data-ttu-id="be8c3-115">Ogni valore dell’attributo **DnsServer** deve essere univoco nell'intera sottoscrizione Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="be8c3-115">Each **DnsServer** attribute value must be unique across the entire Microsoft Azure subscription</span></span>
> 
> 

[<span data-ttu-id="be8c3-116">Elemento siti di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="be8c3-116">Virtual Network Sites Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> <span data-ttu-id="be8c3-117">Per specificare questa impostazione per l'elemento siti di rete virtuale, esso deve essere definito in precedenza nell'elemento DNS.</span><span class="sxs-lookup"><span data-stu-id="be8c3-117">In order to specify this setting for the Virtual Network Sites element, it must be previously defined in the DNS element.</span></span> <span data-ttu-id="be8c3-118">Il *nome*del DnsServerRef dell'elemento siti di rete virtuale deve fare riferimento a un valore nome specificato nell'elemento DNS per *nome* DnsServer.</span><span class="sxs-lookup"><span data-stu-id="be8c3-118">The DnsServerRef *name* in the Virtual Network Sites element must refer to a name value specified in the DNS element for DnsServer *name*.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="be8c3-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="be8c3-119">Next steps</span></span>
* <span data-ttu-id="be8c3-120">Informazioni sullo [Schema di configurazione delle reti virtuali di Azure](http://go.microsoft.com/fwlink/?LinkId=248093).</span><span class="sxs-lookup"><span data-stu-id="be8c3-120">Understand the [Azure Virtual Network Configuration Schema](http://go.microsoft.com/fwlink/?LinkId=248093).</span></span>
* <span data-ttu-id="be8c3-121">Informazioni sullo [Schema di configurazione dei servizi di Azure](https://msdn.microsoft.com/library/windowsazure/ee758710).</span><span class="sxs-lookup"><span data-stu-id="be8c3-121">Understand the [Azure Service Configuration Schema](https://msdn.microsoft.com/library/windowsazure/ee758710).</span></span>
* <span data-ttu-id="be8c3-122">[Configurare una rete virtuale usando un file di configurazione di rete](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="be8c3-122">[Configure a virtual network using Network configuration files](virtual-networks-using-network-configuration-file.md).</span></span>

