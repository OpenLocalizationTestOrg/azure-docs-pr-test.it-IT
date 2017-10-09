---
title: le impostazioni DNS in un file di configurazione del servizio aaaSpecifying | Documenti Microsoft
description: Specificare le impostazioni DNS personalizzate utilizzando il file di configurazione del servizio per la rete virtuale
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 467a4b99-8691-40b3-b640-e25e49675c71
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/24/2016
ms.author: jdial
ms.openlocfilehash: f192e33566dd8e669da04e6378a0c8e4b0b35ecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a><span data-ttu-id="c1730-103">Specifica le impostazioni DNS in un File di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="c1730-103">Specifying DNS Settings in a Service Configuration File</span></span>
## <a name="dns-elements"></a><span data-ttu-id="c1730-104">Elemento DNS</span><span class="sxs-lookup"><span data-stu-id="c1730-104">DNS elements</span></span>
<span data-ttu-id="c1730-105">Un file di configurazione del servizio può contenere un elemento DnsServers con un elenco di indirizzi IPv4 per i server di sistema DNS (Domain Name) hello che verrà utilizzato dal servizio hello.</span><span class="sxs-lookup"><span data-stu-id="c1730-105">A service configuration file may contain a DnsServers element with a list of IPv4 addresses for hello Domain Name System (DNS) servers that hello service will use.</span></span> <span data-ttu-id="c1730-106">Le impostazioni nel file di configurazione del servizio hello hanno la precedenza rispetto alle impostazioni nel file di configurazione di rete hello.</span><span class="sxs-lookup"><span data-stu-id="c1730-106">Settings in hello service configuration file take precedence over settings in hello network configuration file.</span></span> <span data-ttu-id="c1730-107">Per altre informazioni, vedere [Schema di configurazione dei servizi di Azure (con estensione .cscfg)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="c1730-107">For more information, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span></span>

<span data-ttu-id="c1730-108">**Elemento NetworkConfiguration**</span><span class="sxs-lookup"><span data-stu-id="c1730-108">**NetworkConfiguration element**</span></span>

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> <span data-ttu-id="c1730-109">Hello **nome** attributo hello **DnsServer** elemento viene usato solo come un nome di riferimento.</span><span class="sxs-lookup"><span data-stu-id="c1730-109">hello **name** attribute in hello **DnsServer** element is used only as a reference name.</span></span> <span data-ttu-id="c1730-110">Che rappresenta il nome host hello per il server DNS hello.</span><span class="sxs-lookup"><span data-stu-id="c1730-110">It does not represent hello host name for hello DNS server.</span></span> <span data-ttu-id="c1730-111">Ogni **DnsServer** intera sottoscrizione di Microsoft Azure hello valore dell'attributo deve essere univoco.</span><span class="sxs-lookup"><span data-stu-id="c1730-111">Each **DnsServer** attribute value must be unique across hello entire Microsoft Azure subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="c1730-112">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="c1730-112">See Also</span></span>
[<span data-ttu-id="c1730-113">Schema di configurazione dei servizi di Azure (file .cscfg)</span><span class="sxs-lookup"><span data-stu-id="c1730-113">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710)

[<span data-ttu-id="c1730-114">Attività di configurazione di Rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="c1730-114">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="c1730-115">Configurare una rete virtuale usando un file di configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="c1730-115">Configure a Virtual Network Using Network Configuration Files</span></span>](http://go.microsoft.com/fwlink/?LinkId=248094)

[<span data-ttu-id="c1730-116">Informazioni sulle impostazioni di rete virtuale nel portale di gestione di hello</span><span class="sxs-lookup"><span data-stu-id="c1730-116">About Virtual Network settings in hello Management Portal</span></span>](http://go.microsoft.com/fwlink/?LinkId=248092)

