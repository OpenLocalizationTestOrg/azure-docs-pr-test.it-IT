---
title: Informazioni sul ridimensionamento di una rete virtuale in Azure RemoteApp | Documentazione Microsoft
description: Informazioni sui requisiti relativi agli indirizzi IP per Azure RemoteApp in esecuzione con una rete virtuale
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
ms.openlocfilehash: 9375981db64ec4a1ae523e958423b5f5787cec33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a><span data-ttu-id="510ec-103">Informazioni sul ridimensionamento di una rete virtuale in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="510ec-103">Sizing information for a VNET in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="510ec-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="510ec-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="510ec-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="510ec-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="510ec-106">Quando si usa Azure RemoteApp con una rete virtuale (VNET), RemoteApp usa gli indirizzi IP all'interno della subnet.</span><span class="sxs-lookup"><span data-stu-id="510ec-106">When you use Azure RemoteApp with a virtual network (VNET), RemoteApp uses IP addresses within the subnet.</span></span> <span data-ttu-id="510ec-107">In base alla scala del servizio RemoteApp, è necessario assicurarsi che la subnet abbia indirizzi IP sufficienti per le macchine virtuali RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="510ec-107">Based on the scale of your RemoteApp service, you need to ensure that your subnet has enough IP addresses available for RemoteApp virtual machines.</span></span> <span data-ttu-id="510ec-108">Queste indicazioni di ridimensionamento non sono complete se si osserva in che modo RemoteApp esegue dinamicamente lo spin-up e lo spin-down delle macchine virtuali all'interno di una raccolta, tuttavia consentono di stimare l'intervallo di subnet.</span><span class="sxs-lookup"><span data-stu-id="510ec-108">While this sizing guidance isn’t perfect given how RemoteApp dynamically spins up and spins down virtual machines within a collection, it will help you estimate your subnet range.</span></span> <span data-ttu-id="510ec-109">Ciò è particolarmente importante perché, quando si include un servizio RemoteApp in una rete virtuale, non è possibile aumentare le dimensioni della subnet senza rimuovere RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="510ec-109">This is especially important as, once a RemoteApp service is placed in a VNET, you cannot increase the subnet size without removing RemoteApp.</span></span>

<span data-ttu-id="510ec-110">Per ogni raccolta RemoteApp da eseguire alla capacità massima devono essere disponibili 100 indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="510ec-110">For each RemoteApp collection that you want to run at maximum capacity, you should have 100 IP addresses available.</span></span> <span data-ttu-id="510ec-111">Ad esempio, se si ha una raccolta RemoteApp nel piano Standard e si vuole avere un numero massimo di 500 utenti, sono necessari 100 indirizzi IP per la raccolta.</span><span class="sxs-lookup"><span data-stu-id="510ec-111">For example, if you have one RemoteApp collection in the Standard plan and you want to have the maximum 500 users, you should have 100 IP addresses for that collection.</span></span> <span data-ttu-id="510ec-112">Analogamente, in un piano Basic con 800 utenti sono necessari 100 indirizzi IP per una raccolta RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="510ec-112">Similarly, you need 100 IP addresses for a RemoteApp collection in the Basic plan that has 800 users.</span></span> <span data-ttu-id="510ec-113">Se si prevede un numero minore di utenti (inferiore al numero massimo), è possibile ridurre gli indirizzi IP per ogni raccolta.</span><span class="sxs-lookup"><span data-stu-id="510ec-113">If you plan to have fewer users (less than the maximum), you can reduce the IP addresses needed per collection.</span></span> <span data-ttu-id="510ec-114">Il requisito minimo per le dimensioni della subnet è di 30 indirizzi IP (/27).</span><span class="sxs-lookup"><span data-stu-id="510ec-114">The minimum subnet size requirement is 30 IP addresses (/27).</span></span>

<span data-ttu-id="510ec-115">Consultare le informazioni seguenti per assicurarsi che la rete virtuale sia configurata e funzioni correttamente:</span><span class="sxs-lookup"><span data-stu-id="510ec-115">Check out the following information to make sure your VNET is configured and working propertly:</span></span>

* [<span data-ttu-id="510ec-116">Come eseguire la migrazione da una rete virtuale personale a una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="510ec-116">Migrate from a personal VNET to an Azure VNET</span></span>](remoteapp-migratevnet.md)
* [<span data-ttu-id="510ec-117">Convalidare la rete virtuale di Azure da usare con Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="510ec-117">Validate the Azure VNET to use with Azure RemoteApp</span></span>](remoteapp-vnet.md)

