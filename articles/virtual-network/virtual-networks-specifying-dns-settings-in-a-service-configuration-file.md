---
title: Indicazione delle impostazioni DNS in un file cscfg | Documentazione Microsoft
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
ms.openlocfilehash: 0fba2ea06827aff29a7a092933edb8120d668b29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a><span data-ttu-id="ba345-103">Specifica le impostazioni DNS in un File di configurazione del servizio</span><span class="sxs-lookup"><span data-stu-id="ba345-103">Specifying DNS Settings in a Service Configuration File</span></span>
## <a name="dns-elements"></a><span data-ttu-id="ba345-104">Elemento DNS</span><span class="sxs-lookup"><span data-stu-id="ba345-104">DNS elements</span></span>
<span data-ttu-id="ba345-105">Un file di configurazione del servizio può contenere un elemento DnsServers con un elenco di indirizzi IPv4 per i server Domain Name System (DNS) che verrà utilizzato dal servizio.</span><span class="sxs-lookup"><span data-stu-id="ba345-105">A service configuration file may contain a DnsServers element with a list of IPv4 addresses for the Domain Name System (DNS) servers that the service will use.</span></span> <span data-ttu-id="ba345-106">Le impostazioni nel file di configurazione del servizio hanno la precedenza sulle impostazioni nel file di configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="ba345-106">Settings in the service configuration file take precedence over settings in the network configuration file.</span></span> <span data-ttu-id="ba345-107">Per altre informazioni, vedere [Schema di configurazione dei servizi di Azure (con estensione .cscfg)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba345-107">For more information, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span></span>

<span data-ttu-id="ba345-108">**Elemento NetworkConfiguration**</span><span class="sxs-lookup"><span data-stu-id="ba345-108">**NetworkConfiguration element**</span></span>

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> <span data-ttu-id="ba345-109">L'attributo **name** nell'elemento **DnsServer** viene usato solo come nome di riferimento.</span><span class="sxs-lookup"><span data-stu-id="ba345-109">The **name** attribute in the **DnsServer** element is used only as a reference name.</span></span> <span data-ttu-id="ba345-110">Non rappresenta il nome host per il server DNS.</span><span class="sxs-lookup"><span data-stu-id="ba345-110">It does not represent the host name for the DNS server.</span></span> <span data-ttu-id="ba345-111">Ogni valore dell’attributo **DnsServer** deve essere univoco nell'intera sottoscrizione Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="ba345-111">Each **DnsServer** attribute value must be unique across the entire Microsoft Azure subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="ba345-112">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ba345-112">See Also</span></span>
[<span data-ttu-id="ba345-113">Schema di configurazione dei servizi di Azure (file .cscfg)</span><span class="sxs-lookup"><span data-stu-id="ba345-113">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710)

[<span data-ttu-id="ba345-114">Attività di configurazione di Rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="ba345-114">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="ba345-115">Configurare una rete virtuale usando un file di configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="ba345-115">Configure a Virtual Network Using Network Configuration Files</span></span>](http://go.microsoft.com/fwlink/?LinkId=248094)

[<span data-ttu-id="ba345-116">Informazioni sulle impostazioni della rete virtuale nel portale di gestione</span><span class="sxs-lookup"><span data-stu-id="ba345-116">About Virtual Network settings in the Management Portal</span></span>](http://go.microsoft.com/fwlink/?LinkId=248092)

