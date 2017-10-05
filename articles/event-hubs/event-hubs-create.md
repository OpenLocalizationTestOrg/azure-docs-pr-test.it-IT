---
title: Creare un hub eventi di Azure | Documentazione Microsoft
description: Creare uno spazio dei nomi di Hub eventi di Azure e un hub eventi usando il Portale di Azure
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
ms.openlocfilehash: 816bf1426704d3391550e80c0700f1b011683a94
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-the-azure-portal"></a><span data-ttu-id="49b0c-103">Creare uno spazio dei nomi di Hub eventi e un hub eventi usando il Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="49b0c-103">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="49b0c-104">Creare uno spazio dei nomi di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="49b0c-104">Create an Event Hubs namespace</span></span>
1. <span data-ttu-id="49b0c-105">Accedere al [portale di Azure][Azure portal] e fare clic su **Nuovo** nella parte superiore sinistra della schermata.</span><span class="sxs-lookup"><span data-stu-id="49b0c-105">Log on to the [Azure portal][Azure portal], and click **New** at the top left of the screen.</span></span>
1. <span data-ttu-id="49b0c-106">Fare clic su **Internet delle cose** e quindi su **Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="49b0c-106">Click **Internet of Things**, and then click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. <span data-ttu-id="49b0c-107">Nel pannello **Crea spazio dei nomi** immettere un nome per lo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="49b0c-107">In the **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="49b0c-108">Verrà effettuato immediatamente un controllo sulla disponibilità del nome.</span><span class="sxs-lookup"><span data-stu-id="49b0c-108">The system immediately checks to see if the name is available.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. <span data-ttu-id="49b0c-109">Dopo aver verificato che il nome dello spazio dei nomi sia disponibile, scegliere il piano tariffario (Basic o Standard).</span><span class="sxs-lookup"><span data-stu-id="49b0c-109">After making sure the namespace name is available, choose the pricing tier (Basic or Standard).</span></span> <span data-ttu-id="49b0c-110">Scegliere anche una sottoscrizione, un gruppo di risorse e una località di Azure in cui creare la risorsa.</span><span class="sxs-lookup"><span data-stu-id="49b0c-110">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span></span> 
1. <span data-ttu-id="49b0c-111">Fare clic su **Crea** per creare lo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="49b0c-111">Click **Create** to create the namespace.</span></span> <span data-ttu-id="49b0c-112">Per il provisioning completo delle risorse da parte del sistema, potrebbero essere necessari alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="49b0c-112">You may have to wait a few minutes for the system to fully provision the resources.</span></span>
2. <span data-ttu-id="49b0c-113">Nell'elenco di spazi dei nomi del portale fare clic sullo spazio dei nomi appena creato.</span><span class="sxs-lookup"><span data-stu-id="49b0c-113">In the portal list of namespaces, click the newly created namespace.</span></span>
2. <span data-ttu-id="49b0c-114">Fare clic su **Criteri di accesso condivisi** e quindi su **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="49b0c-114">Click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. <span data-ttu-id="49b0c-115">Fare clic sul pulsante di copia per copiare la stringa di connessione **RootManageSharedAccessKey** negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="49b0c-115">Click the copy button to copy the **RootManageSharedAccessKey** connection string to the clipboard.</span></span> <span data-ttu-id="49b0c-116">Salvare la stringa di connessione in una posizione temporanea, ad esempio il Blocco note, per usarla in seguito.</span><span class="sxs-lookup"><span data-stu-id="49b0c-116">Save this connection string in a temporary location, such as Notepad, to use later.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a><span data-ttu-id="49b0c-117">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="49b0c-117">Create an event hub</span></span>

1. <span data-ttu-id="49b0c-118">Nell'elenco di spazi dei nomi di Hub eventi fare clic sullo spazio dei nomi appena creato.</span><span class="sxs-lookup"><span data-stu-id="49b0c-118">In the Event Hubs namespace list, click the newly created namespace.</span></span>      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. <span data-ttu-id="49b0c-119">Nel pannello dello spazio dei nomi fare clic su **Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="49b0c-119">In the namespace blade, click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. <span data-ttu-id="49b0c-120">Nella parte superiore del pannello fare clic su **Aggiungi hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="49b0c-120">At the top of the blade, click **Add Event Hub**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. <span data-ttu-id="49b0c-121">Digitare un nome per l'hub eventi e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="49b0c-121">Type a name for your event hub, then click **Create**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub5.png)

<span data-ttu-id="49b0c-122">L'hub eventi è stato creato e sono disponibili le stringhe di connessione necessarie per inviare e ricevere eventi.</span><span class="sxs-lookup"><span data-stu-id="49b0c-122">Your event hub is now created, and you have the connection strings you need to send and receive events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49b0c-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="49b0c-123">Next steps</span></span>
<span data-ttu-id="49b0c-124">Per altre informazioni sugli Hub eventi, visitare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="49b0c-124">To learn more about Event Hubs, visit these links:</span></span>

* [<span data-ttu-id="49b0c-125">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="49b0c-125">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="49b0c-126">Panoramica dell'API di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="49b0c-126">Event Hubs API overview</span></span>](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/