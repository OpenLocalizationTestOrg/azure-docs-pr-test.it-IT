---
title: Distribuire QuickBooks in Azure RemoteApp | Microsoft Docs
description: Informazioni su come condividere QuickBooks con Azure RemoteApp.
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
ms.openlocfilehash: bbfac45220f6ef36c9951daae0ced1974e8ddabb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a><span data-ttu-id="9cbf9-103">Come distribuire QuickBooks in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="9cbf9-103">How do you deploy QuickBooks in Azure RemoteApp?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9cbf9-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="9cbf9-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="9cbf9-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="9cbf9-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="9cbf9-106">Usare le informazioni seguenti per la condivisione di QuickBooks come app in Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="9cbf9-106">Use the following information to share QuickBooks as an app in Azure RemoteApp.</span></span>

<span data-ttu-id="9cbf9-107">È possibile condividere QuickBooks 2015 Enterprise con Azure RemoteApp in una raccolta ibrida o cloud.</span><span class="sxs-lookup"><span data-stu-id="9cbf9-107">You can share QuickBooks 2015 Enterprise with Azure RemoteApp in either a hybrid or cloud collection.</span></span> <span data-ttu-id="9cbf9-108">Il file della società deve trovarsi in una macchina virtuale che esegue il server di database QuickBooks separato dai server di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="9cbf9-108">The company file must reside on a VM that is running QuickBooks database server that is separate from the Azure RemoteApp servers.</span></span> <span data-ttu-id="9cbf9-109">Non memorizzare mai il file della società nell'immagine di Azure RemoteApp. In caso contrario, potrebbe verificarsi la perdita dei dati.</span><span class="sxs-lookup"><span data-stu-id="9cbf9-109">Never store the company file on your Azure RemoteApp image - data loss is expected if you do this.</span></span> <span data-ttu-id="9cbf9-110">Solo QuickBooks Enterprise supporta l'hosting del file QuickBooks in una condivisione esterna con il server di database QuickBooks accessibile tramite rete standard di Windows.</span><span class="sxs-lookup"><span data-stu-id="9cbf9-110">Only QuickBooks Enterprise supports hosting the QuickBooks file on an external share with QuickBooks database server accessible via standard Windows networking.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="9cbf9-111">Il server di database QuickBooks che ospita il file della società deve risiedere in una macchina virtuale separata nell'ambito della stessa rete virtuale come raccolta di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="9cbf9-111">The QuickBooks database server that is hosting the company file must reside on a separate VM within the same VNET as the Azure RemoteApp collection.</span></span>  
> 
> 

## <a name="steps-to-deploy-quickbooks"></a><span data-ttu-id="9cbf9-112">Passaggi per distribuire QuickBooks</span><span class="sxs-lookup"><span data-stu-id="9cbf9-112">Steps to deploy QuickBooks</span></span>
1. <span data-ttu-id="9cbf9-113">Creare una macchina virtuale di Azure e installare QuickBooks e il server di database QuickBooks, quindi inserire il file della società in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9cbf9-113">Create an Azure VM and install QuickBooks, QuickBooks database server, and place the company file on a Azure VM.</span></span>  <span data-ttu-id="9cbf9-114">Assicurarsi di configurare correttamente le regole del firewall.</span><span class="sxs-lookup"><span data-stu-id="9cbf9-114">Make sure to properly configure firewall rules.</span></span>
2. <span data-ttu-id="9cbf9-115">Installare QuickBooks in un'[immagine personalizzata](remoteapp-imageoptions.md) e creare una [raccolta di Azure RemoteApp](remoteapp-collections.md), cloud o ibrida, esattamente nella stessa rete virtuale in cui risiede la macchina virtuale che ospita il server di database QuickBooks con i file della società.</span><span class="sxs-lookup"><span data-stu-id="9cbf9-115">Install QuickBooks on a [custom image](remoteapp-imageoptions.md) and create an [Azure RemoteApp collection](remoteapp-collections.md), either cloud or hybrid, within the exact same VNET where the VM hosting the QuickBooks database server with company files resides.</span></span> 
3. <span data-ttu-id="9cbf9-116">[pubblica](remoteapp-publish.md) l'app QuickBooks agli utenti.</span><span class="sxs-lookup"><span data-stu-id="9cbf9-116">[Publish](remoteapp-publish.md) QuickBooks app to users</span></span>
4. <span data-ttu-id="9cbf9-117">Avviare il client QuickBooks ospitato in Azure RemoteApp, passare tramite reti Windows standard alla macchina virtuale che ospita il server di database QuickBooks e aprire il file della società.</span><span class="sxs-lookup"><span data-stu-id="9cbf9-117">Launch the Azure RemoteApp-hosted QuickBooks client, navigate using standard Windows networking to the VM hosting the QuickBooks database server and open the company file.</span></span> 

## <a name="documentation-references"></a><span data-ttu-id="9cbf9-118">Riferimenti di documentazione</span><span class="sxs-lookup"><span data-stu-id="9cbf9-118">Documentation references</span></span>
* <span data-ttu-id="9cbf9-119">[Configurazioni supportate](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span><span class="sxs-lookup"><span data-stu-id="9cbf9-119">QuickBooks [supported configurations](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)</span></span>
* <span data-ttu-id="9cbf9-120">[Opzioni di distribuzione](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span><span class="sxs-lookup"><span data-stu-id="9cbf9-120">QuickBooks [deployment options](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)</span></span>

<span data-ttu-id="9cbf9-121">È inoltre possibile consultare la presentazione Ignite relativa all'[amministrazione e alla gestione di Microsoft Azure RemoteApp](https://channel9.msdn.com/Events/Ignite/2015/BRK3868). Andare al minuto 1:02:45 per la parte su QuickBooks.</span><span class="sxs-lookup"><span data-stu-id="9cbf9-121">You can also check out my Ignite presentation, [Fundamentals of Microsoft Azure RemoteApp Management and Administration](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) - fast-forward to 1:02:45 to get to the QuickBooks part.</span></span>

## <a name="deployment-architecture"></a><span data-ttu-id="9cbf9-122">Architettura di distribuzione</span><span class="sxs-lookup"><span data-stu-id="9cbf9-122">Deployment architecture</span></span>
![QuickBooks + distribuzione di Azure RemoteApp](./media/remoteapp-quickbooks/ra-quickbooks.png)

