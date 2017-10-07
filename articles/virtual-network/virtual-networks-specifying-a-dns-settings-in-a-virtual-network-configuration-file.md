---
title: aaaSpecifying impostazioni DNS in un file di configurazione di rete virtuale | Documenti Microsoft
description: Come file di impostazioni del server DNS toochange in una rete virtuale usando una configurazione di rete virtuale nel modello di distribuzione classica hello
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
ms.openlocfilehash: d53a658773e1c930b5a28a701db0be9edd26565e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a><span data-ttu-id="fedbe-103">Indicazione delle impostazioni DNS in un file di configurazione di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="fedbe-103">Specifying DNS settings in a virtual network configuration file</span></span>
<span data-ttu-id="fedbe-104">Un file di configurazione di rete dispone di due elementi che è possibile utilizzare le impostazioni di sistema DNS (Domain Name) toospecify: **DnsServers** e **DnsServerRef**.</span><span class="sxs-lookup"><span data-stu-id="fedbe-104">A network configuration file has two elements that you can use toospecify Domain Name System (DNS) settings: **DnsServers** and **DnsServerRef**.</span></span> <span data-ttu-id="fedbe-105">È possibile aggiungere un elenco dei server DNS specificando i relativi indirizzi IP e fare riferimento a nomi toohello **DnsServers** elemento.</span><span class="sxs-lookup"><span data-stu-id="fedbe-105">You can add a list of DNS servers by specifying their IP addresses and reference names toohello **DnsServers** element.</span></span> <span data-ttu-id="fedbe-106">È quindi possibile utilizzare un **DnsServerRef** toospecify elemento quali voci dei server DNS dall'elemento DnsServers hello vengono utilizzate per vari siti di rete all'interno della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="fedbe-106">You can then use a **DnsServerRef** element toospecify which DNS server entries from hello DnsServers element are used for different network sites within your virtual network.</span></span>

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="fedbe-107">Questo articolo descrive il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="fedbe-107">This article covers hello classic deployment model.</span></span>

<span data-ttu-id="fedbe-108">file di configurazione di rete Hello può contenere hello seguenti elementi.</span><span class="sxs-lookup"><span data-stu-id="fedbe-108">hello network configuration file may contain hello following elements.</span></span> <span data-ttu-id="fedbe-109">titolo Hello di ogni elemento è collegato tooa pagina che fornisce informazioni aggiuntive sull'elemento hello impostazioni dei valori.</span><span class="sxs-lookup"><span data-stu-id="fedbe-109">hello title of each element is linked tooa page that provides additional information about hello element value settings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fedbe-110">Per informazioni su come tooconfigure hello file di configurazione di rete, vedere [configurare una rete virtuale usando un File di configurazione di rete](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="fedbe-110">For information about how tooconfigure hello network configuration file, see [Configure a Virtual Network Using a Network Configuration File](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="fedbe-111">Per informazioni su ogni elemento contenuto nel file di configurazione di rete hello, vedere [Schema di configurazione di rete virtuale Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="fedbe-111">For information about each element contained in hello network configuration file, see [Azure Virtual Network Configuration Schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
> 
> 

[<span data-ttu-id="fedbe-112">Elemento DNS</span><span class="sxs-lookup"><span data-stu-id="fedbe-112">Dns Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> <span data-ttu-id="fedbe-113">Hello **nome** attributo hello **DnsServer** elemento viene usato solo come riferimento per hello **DnsServerRef** elemento.</span><span class="sxs-lookup"><span data-stu-id="fedbe-113">hello **name** attribute in hello **DnsServer** element is used only as a reference for hello **DnsServerRef** element.</span></span> <span data-ttu-id="fedbe-114">Che rappresenta il nome host hello per il server DNS hello.</span><span class="sxs-lookup"><span data-stu-id="fedbe-114">It does not represent hello host name for hello DNS server.</span></span> <span data-ttu-id="fedbe-115">Ogni **DnsServer** intera sottoscrizione di Microsoft Azure hello valore dell'attributo deve essere univoco</span><span class="sxs-lookup"><span data-stu-id="fedbe-115">Each **DnsServer** attribute value must be unique across hello entire Microsoft Azure subscription</span></span>
> 
> 

[<span data-ttu-id="fedbe-116">Elemento siti di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="fedbe-116">Virtual Network Sites Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> <span data-ttu-id="fedbe-117">In ordine toospecify questa impostazione per l'elemento relativo ai siti di rete virtuale hello, deve essere definito in precedenza nell'elemento DNS hello.</span><span class="sxs-lookup"><span data-stu-id="fedbe-117">In order toospecify this setting for hello Virtual Network Sites element, it must be previously defined in hello DNS element.</span></span> <span data-ttu-id="fedbe-118">Hello DnsServerRef *nome* in siti di rete virtuale hello l'elemento deve fare riferimento tooa nome valore specificato nell'elemento DNS hello per DnsServer *nome*.</span><span class="sxs-lookup"><span data-stu-id="fedbe-118">hello DnsServerRef *name* in hello Virtual Network Sites element must refer tooa name value specified in hello DNS element for DnsServer *name*.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="fedbe-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fedbe-119">Next steps</span></span>
* <span data-ttu-id="fedbe-120">Comprendere hello [Schema di configurazione di rete virtuale Azure](http://go.microsoft.com/fwlink/?LinkId=248093).</span><span class="sxs-lookup"><span data-stu-id="fedbe-120">Understand hello [Azure Virtual Network Configuration Schema](http://go.microsoft.com/fwlink/?LinkId=248093).</span></span>
* <span data-ttu-id="fedbe-121">Comprendere hello [dello Schema di configurazione del servizio di Azure](https://msdn.microsoft.com/library/windowsazure/ee758710).</span><span class="sxs-lookup"><span data-stu-id="fedbe-121">Understand hello [Azure Service Configuration Schema](https://msdn.microsoft.com/library/windowsazure/ee758710).</span></span>
* <span data-ttu-id="fedbe-122">[Configurare una rete virtuale usando un file di configurazione di rete](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="fedbe-122">[Configure a virtual network using Network configuration files](virtual-networks-using-network-configuration-file.md).</span></span>

