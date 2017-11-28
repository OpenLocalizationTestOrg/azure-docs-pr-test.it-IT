---
title: aaaDeploy QuickBooks in Azure RemoteApp | Documenti Microsoft
description: Informazioni su come tooshare QuickBooks con Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c5d00753-77c0-4f0d-a5df-9451b46a31d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c21b1ac311449be2281f9ce157828260e856f55d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a><span data-ttu-id="61dfc-103">Come distribuire QuickBooks in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="61dfc-103">How do you deploy QuickBooks in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="61dfc-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="61dfc-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="61dfc-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="61dfc-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="61dfc-106">Utilizzare hello seguente informazioni tooshare QuickBooks come un'app in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="61dfc-106">Use hello following information tooshare QuickBooks as an app in Azure RemoteApp.</span></span>

<span data-ttu-id="61dfc-107">È possibile condividere QuickBooks 2015 Enterprise con Azure RemoteApp in una raccolta ibrida o cloud.</span><span class="sxs-lookup"><span data-stu-id="61dfc-107">You can share QuickBooks 2015 Enterprise with Azure RemoteApp in either a hybrid or cloud collection.</span></span> <span data-ttu-id="61dfc-108">file aziendale Hello deve risiedere in una macchina virtuale che esegue server di database QuickBooks è separato dai server di Azure RemoteApp hello.</span><span class="sxs-lookup"><span data-stu-id="61dfc-108">hello company file must reside on a VM that is running QuickBooks database server that is separate from hello Azure RemoteApp servers.</span></span> <span data-ttu-id="61dfc-109">Non memorizzare mai file aziendale hello sull'immagine Azure RemoteApp: perdita di dati è previsto se si esegue questa operazione.</span><span class="sxs-lookup"><span data-stu-id="61dfc-109">Never store hello company file on your Azure RemoteApp image - data loss is expected if you do this.</span></span> <span data-ttu-id="61dfc-110">Solo QuickBooks Enterprise supporta file di QuickBooks hello hosting in una condivisione esterna con server di database QuickBooks accessibile tramite rete standard di Windows.</span><span class="sxs-lookup"><span data-stu-id="61dfc-110">Only QuickBooks Enterprise supports hosting hello QuickBooks file on an external share with QuickBooks database server accessible via standard Windows networking.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="61dfc-111">Hello QuickBooks i server di database che ospita i file aziendale hello devono risiedere in una macchina virtuale separata all'interno di hello stessa rete virtuale come hello raccolta di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="61dfc-111">hello QuickBooks database server that is hosting hello company file must reside on a separate VM within hello same VNET as hello Azure RemoteApp collection.</span></span>  
> 
> 

## <a name="steps-toodeploy-quickbooks"></a><span data-ttu-id="61dfc-112">Passaggi toodeploy QuickBooks</span><span class="sxs-lookup"><span data-stu-id="61dfc-112">Steps toodeploy QuickBooks</span></span>
1. <span data-ttu-id="61dfc-113">Creare una macchina virtuale di Azure e installare QuickBooks, server di database QuickBooks e inserire file aziendale hello in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="61dfc-113">Create an Azure VM and install QuickBooks, QuickBooks database server, and place hello company file on a Azure VM.</span></span>  <span data-ttu-id="61dfc-114">Verificare che tooproperly configurare regole firewall.</span><span class="sxs-lookup"><span data-stu-id="61dfc-114">Make sure tooproperly configure firewall rules.</span></span>
2. <span data-ttu-id="61dfc-115">Installare QuickBooks in un [immagine personalizzata](remoteapp-imageoptions.md) e creare un [raccolta di Azure RemoteApp](remoteapp-collections.md), cloud o ibrida, all'interno di hello esatta stessa rete virtuale in cui hello macchina virtuale che ospita hello QuickBooks server di database con i file aziendali si trova.</span><span class="sxs-lookup"><span data-stu-id="61dfc-115">Install QuickBooks on a [custom image](remoteapp-imageoptions.md) and create an [Azure RemoteApp collection](remoteapp-collections.md), either cloud or hybrid, within hello exact same VNET where hello VM hosting hello QuickBooks database server with company files resides.</span></span> 
3. <span data-ttu-id="61dfc-116">[Pubblicare](remoteapp-publish.md) toousers app QuickBooks</span><span class="sxs-lookup"><span data-stu-id="61dfc-116">[Publish](remoteapp-publish.md) QuickBooks app toousers</span></span>
4. <span data-ttu-id="61dfc-117">Avviare il client di hello QuickBooks ospitati in Azure RemoteApp, passare tramite rete toohello VM hello QuickBooks database server di hosting standard di Windows e aprire file aziendale hello.</span><span class="sxs-lookup"><span data-stu-id="61dfc-117">Launch hello Azure RemoteApp-hosted QuickBooks client, navigate using standard Windows networking toohello VM hosting hello QuickBooks database server and open hello company file.</span></span> 

## <a name="documentation-references"></a><span data-ttu-id="61dfc-118">Riferimenti di documentazione</span><span class="sxs-lookup"><span data-stu-id="61dfc-118">Documentation references</span></span>
* <span data-ttu-id="61dfc-119">[Configurazioni supportate](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span><span class="sxs-lookup"><span data-stu-id="61dfc-119">QuickBooks [supported configurations](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span></span>
* <span data-ttu-id="61dfc-120">[Opzioni di distribuzione](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span><span class="sxs-lookup"><span data-stu-id="61dfc-120">QuickBooks [deployment options](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span></span>

<span data-ttu-id="61dfc-121">È inoltre possibile estrarre la presentazione, Ignite [nozioni di base di Microsoft Azure RemoteApp gestione e amministrazione](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) -too1:02:45 tooget toohello QuickBooks parte di uno sprint.</span><span class="sxs-lookup"><span data-stu-id="61dfc-121">You can also check out my Ignite presentation, [Fundamentals of Microsoft Azure RemoteApp Management and Administration](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) - fast-forward too1:02:45 tooget toohello QuickBooks part.</span></span>

## <a name="deployment-architecture"></a><span data-ttu-id="61dfc-122">Architettura di distribuzione</span><span class="sxs-lookup"><span data-stu-id="61dfc-122">Deployment architecture</span></span>
![QuickBooks + distribuzione di Azure RemoteApp](./media/remoteapp-quickbooks/ra-quickbooks.png)

