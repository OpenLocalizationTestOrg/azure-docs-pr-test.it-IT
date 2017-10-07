---
title: aaaSizing informazioni per una rete virtuale in Azure RemoteApp | Documenti Microsoft
description: Informazioni sui requisiti di indirizzo IP di hello per Azure RemoteApp in esecuzione con una rete virtuale
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b6e1c4ba-0236-42b2-bced-69353bf211be
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: f98b831af32c41740b258d122b3e18765be08d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a><span data-ttu-id="e5cef-103">Informazioni sul ridimensionamento di una rete virtuale in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="e5cef-103">Sizing information for a VNET in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e5cef-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="e5cef-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e5cef-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="e5cef-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e5cef-106">Quando si usa Azure RemoteApp con una rete virtuale (VNET), RemoteApp Usa gli indirizzi IP in subnet hello.</span><span class="sxs-lookup"><span data-stu-id="e5cef-106">When you use Azure RemoteApp with a virtual network (VNET), RemoteApp uses IP addresses within hello subnet.</span></span> <span data-ttu-id="e5cef-107">In base alla scala di hello del servizio di RemoteApp, è necessario che la subnet disponga di indirizzi IP sufficienti per le macchine virtuali RemoteApp tooensure.</span><span class="sxs-lookup"><span data-stu-id="e5cef-107">Based on hello scale of your RemoteApp service, you need tooensure that your subnet has enough IP addresses available for RemoteApp virtual machines.</span></span> <span data-ttu-id="e5cef-108">Queste indicazioni di ridimensionamento non sono complete se si osserva in che modo RemoteApp esegue dinamicamente lo spin-up e lo spin-down delle macchine virtuali all'interno di una raccolta, tuttavia consentono di stimare l'intervallo di subnet.</span><span class="sxs-lookup"><span data-stu-id="e5cef-108">While this sizing guidance isn’t perfect given how RemoteApp dynamically spins up and spins down virtual machines within a collection, it will help you estimate your subnet range.</span></span> <span data-ttu-id="e5cef-109">Ciò è particolarmente importante perché, dopo un servizio di RemoteApp è posizionato in una rete virtuale, non è possibile aumentare la dimensione della subnet hello senza rimuovere RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="e5cef-109">This is especially important as, once a RemoteApp service is placed in a VNET, you cannot increase hello subnet size without removing RemoteApp.</span></span>

<span data-ttu-id="e5cef-110">Per ogni raccolta RemoteApp che si desidera toorun alla capacità massima, è necessario 100 gli indirizzi IP disponibili.</span><span class="sxs-lookup"><span data-stu-id="e5cef-110">For each RemoteApp collection that you want toorun at maximum capacity, you should have 100 IP addresses available.</span></span> <span data-ttu-id="e5cef-111">Ad esempio, se si dispone di una raccolta RemoteApp nel piano Standard hello e si desidera toohave hello massimo 500 utenti, è necessario 100 indirizzi IP per la raccolta.</span><span class="sxs-lookup"><span data-stu-id="e5cef-111">For example, if you have one RemoteApp collection in hello Standard plan and you want toohave hello maximum 500 users, you should have 100 IP addresses for that collection.</span></span> <span data-ttu-id="e5cef-112">Analogamente, è necessario 100 indirizzi IP per una raccolta RemoteApp nel piano base hello dotato di 800 utenti.</span><span class="sxs-lookup"><span data-stu-id="e5cef-112">Similarly, you need 100 IP addresses for a RemoteApp collection in hello Basic plan that has 800 users.</span></span> <span data-ttu-id="e5cef-113">Se si prevede di toohave un numero di utenti (minore di hello massima), è possibile ridurre gli indirizzi IP hello necessari per ogni raccolta.</span><span class="sxs-lookup"><span data-stu-id="e5cef-113">If you plan toohave fewer users (less than hello maximum), you can reduce hello IP addresses needed per collection.</span></span> <span data-ttu-id="e5cef-114">requisiti relativi alla dimensione minima subnet Hello sono 30 indirizzi IP (/ 27).</span><span class="sxs-lookup"><span data-stu-id="e5cef-114">hello minimum subnet size requirement is 30 IP addresses (/27).</span></span>

<span data-ttu-id="e5cef-115">Estrarre hello dopo che la rete virtuale sia configurata con informazioni toomake e funziona correttamente:</span><span class="sxs-lookup"><span data-stu-id="e5cef-115">Check out hello following information toomake sure your VNET is configured and working propertly:</span></span>

* [<span data-ttu-id="e5cef-116">Eseguire la migrazione da un tooan di rete virtuale personale rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="e5cef-116">Migrate from a personal VNET tooan Azure VNET</span></span>](remoteapp-migratevnet.md)
* [<span data-ttu-id="e5cef-117">Convalidare hello toouse di rete virtuale di Azure con Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="e5cef-117">Validate hello Azure VNET toouse with Azure RemoteApp</span></span>](remoteapp-vnet.md)

