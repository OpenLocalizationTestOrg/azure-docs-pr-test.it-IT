---
title: un hub eventi Azure aaaCreate | Documenti Microsoft
description: Creare uno spazio dei nomi dell'hub eventi di Azure e un hub di eventi utilizzando hello portale di Azure
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: ff99e327-c8db-4354-9040-9c60c51a2191
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: sethm
ms.openlocfilehash: 9a8b7711e2ca7d112e24be19353d43c365ff6935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-hello-azure-portal"></a><span data-ttu-id="6bdc8-103">Creare uno spazio dei nomi dell'hub eventi e un hub di eventi utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6bdc8-103">Create an Event Hubs namespace and an event hub using hello Azure portal</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="6bdc8-104">Creare uno spazio dei nomi di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="6bdc8-104">Create an Event Hubs namespace</span></span>
1. <span data-ttu-id="6bdc8-105">Accesso toohello [portale di Azure][Azure portal], fare clic su **New** in hello in alto a sinistra della schermata di hello.</span><span class="sxs-lookup"><span data-stu-id="6bdc8-105">Log on toohello [Azure portal][Azure portal], and click **New** at hello top left of hello screen.</span></span>
1. <span data-ttu-id="6bdc8-106">Fare clic su **Internet delle cose** e quindi su **Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="6bdc8-106">Click **Internet of Things**, and then click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. <span data-ttu-id="6bdc8-107">In hello **Crea spazio dei nomi** pannello, immettere un nome di spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="6bdc8-107">In hello **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="6bdc8-108">sistema di Hello controlla immediatamente toosee se nome hello è disponibile.</span><span class="sxs-lookup"><span data-stu-id="6bdc8-108">hello system immediately checks toosee if hello name is available.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. <span data-ttu-id="6bdc8-109">Dopo il nome di spazio dei nomi che hello è disponibile, scegliere hello tariffario (Standard o Basic).</span><span class="sxs-lookup"><span data-stu-id="6bdc8-109">After making sure hello namespace name is available, choose hello pricing tier (Basic or Standard).</span></span> <span data-ttu-id="6bdc8-110">Inoltre, è possibile scegliere una sottoscrizione di Azure, un gruppo di risorse e una posizione nella quale risorsa hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="6bdc8-110">Also, choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> 
1. <span data-ttu-id="6bdc8-111">Fare clic su **crea** dello spazio dei nomi di toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="6bdc8-111">Click **Create** toocreate hello namespace.</span></span> <span data-ttu-id="6bdc8-112">È possibile toowait per le risorse hello di effettuare il provisioning di hello sistema toofully qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="6bdc8-112">You may have toowait a few minutes for hello system toofully provision hello resources.</span></span>
2. <span data-ttu-id="6bdc8-113">Hello portale selezionare nell'elenco degli spazi dei nomi hello appena creato spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="6bdc8-113">In hello portal list of namespaces, click hello newly created namespace.</span></span>
2. <span data-ttu-id="6bdc8-114">Fare clic su **Criteri di accesso condivisi** e quindi su **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="6bdc8-114">Click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. <span data-ttu-id="6bdc8-115">Fare clic su hello toocopy pulsante Copia di hello **RootManageSharedAccessKey** Appunti toohello stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="6bdc8-115">Click hello copy button toocopy hello **RootManageSharedAccessKey** connection string toohello clipboard.</span></span> <span data-ttu-id="6bdc8-116">Salvare la stringa di connessione in un percorso temporaneo, ad esempio Blocco note, toouse in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="6bdc8-116">Save this connection string in a temporary location, such as Notepad, toouse later.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a><span data-ttu-id="6bdc8-117">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="6bdc8-117">Create an event hub</span></span>

1. <span data-ttu-id="6bdc8-118">Nell'elenco dello spazio dei nomi di hub eventi hello, fare clic su spazio dei nomi hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="6bdc8-118">In hello Event Hubs namespace list, click hello newly created namespace.</span></span>      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. <span data-ttu-id="6bdc8-119">Nel Pannello di hello dello spazio dei nomi, fare clic su **hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="6bdc8-119">In hello namespace blade, click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. <span data-ttu-id="6bdc8-120">Nella parte superiore di hello del Pannello di hello, fare clic su **aggiungere Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="6bdc8-120">At hello top of hello blade, click **Add Event Hub**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. <span data-ttu-id="6bdc8-121">Digitare un nome per l'hub eventi e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="6bdc8-121">Type a name for your event hub, then click **Create**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub5.png)

<span data-ttu-id="6bdc8-122">È stato creato l'hub di eventi e disporre le stringhe di connessione hello è necessario toosend eventi e di ricezione.</span><span class="sxs-lookup"><span data-stu-id="6bdc8-122">Your event hub is now created, and you have hello connection strings you need toosend and receive events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bdc8-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6bdc8-123">Next steps</span></span>
<span data-ttu-id="6bdc8-124">toolearn più sugli hub di eventi, visitare i collegamenti:</span><span class="sxs-lookup"><span data-stu-id="6bdc8-124">toolearn more about Event Hubs, visit these links:</span></span>

* [<span data-ttu-id="6bdc8-125">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="6bdc8-125">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="6bdc8-126">Panoramica dell'API di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="6bdc8-126">Event Hubs API overview</span></span>](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/