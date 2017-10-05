---
title: Aumentare o ridurre il numero di istanze per un servizio cloud Azure in Windows PowerShell | Documentazione Microsoft
description: (classico) Informazioni su come usare PowerShell per aumentare o ridurre il numero di istanze per un ruolo Web o un ruolo di lavoro in Azure.
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: ee37dd8c-6714-4c61-adb8-03d6bbf76c9a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: mmccrory
ms.openlocfilehash: a7ae8ff202d403dff19b8c9a6a09492235db27ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-scale-a-cloud-service-in-powershell"></a><span data-ttu-id="15380-103">Come aumentare o ridurre il numero di istanze per un servizio cloud in PowerShell</span><span class="sxs-lookup"><span data-stu-id="15380-103">How to scale a cloud service in PowerShell</span></span>

<span data-ttu-id="15380-104">È possibile usare Windows PowerShell per aumentare o ridurre il numero di istanze per un ruolo Web o un ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="15380-104">You can use Windows PowerShell to scale a web role or worker role in or out by adding or removing instances.</span></span>  

## <a name="log-in-to-azure"></a><span data-ttu-id="15380-105">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="15380-105">Log in to Azure</span></span>

<span data-ttu-id="15380-106">Prima di poter eseguire qualsiasi operazione sulla sottoscrizione tramite PowerShell, è necessario eseguire l'accesso:</span><span class="sxs-lookup"><span data-stu-id="15380-106">Before you can perform any operations on your subscription through PowerShell, you must log in:</span></span>

```powershell
Add-AzureAccount
```

<span data-ttu-id="15380-107">Se sono disponibili più sottoscrizioni associate all'account, potrebbe essere necessario modificare la sottoscrizione corrente a seconda di dove si trova il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="15380-107">If you have multiple subscriptions associated with your account, you may need to change the current subscription depending on where your cloud service resides.</span></span> <span data-ttu-id="15380-108">Per controllare la sottoscrizione corrente, eseguire:</span><span class="sxs-lookup"><span data-stu-id="15380-108">To check the current subscription, run:</span></span>

```powershell
Get-AzureSubscription -Current
```

<span data-ttu-id="15380-109">Se è necessario modificare la sottoscrizione corrente, eseguire:</span><span class="sxs-lookup"><span data-stu-id="15380-109">If you need to change the current subscription, run:</span></span>

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-the-current-instance-count-for-your-role"></a><span data-ttu-id="15380-110">Controllare il numero corrente di istanze per il ruolo</span><span class="sxs-lookup"><span data-stu-id="15380-110">Check the current instance count for your role</span></span>

<span data-ttu-id="15380-111">Per controllare lo stato corrente del ruolo, eseguire:</span><span class="sxs-lookup"><span data-stu-id="15380-111">To check the current state of your role, run:</span></span>

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

<span data-ttu-id="15380-112">Si dovrebbero così ottenere informazioni sul ruolo, inclusa la versione corrente del sistema operativo e il numero corrente di istanze.</span><span class="sxs-lookup"><span data-stu-id="15380-112">You should get back information about the role, including its current OS version and instance count.</span></span> <span data-ttu-id="15380-113">In questo caso, il ruolo ha una singola istanza.</span><span class="sxs-lookup"><span data-stu-id="15380-113">In this case, the role has a single instance.</span></span>

![Informazioni sul ruolo](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-the-role-by-adding-more-instances"></a><span data-ttu-id="15380-115">Aumentare il numero di istanze per il ruolo aggiungendo istanze</span><span class="sxs-lookup"><span data-stu-id="15380-115">Scale out the role by adding more instances</span></span>

<span data-ttu-id="15380-116">Per aumentare il numero di istanze del ruolo, passare il numero desiderato con il parametro **Count** del cmdlet **Set-AzureRole**:</span><span class="sxs-lookup"><span data-stu-id="15380-116">To scale out your role, pass the desired number of instances as the **Count** parameter to the **Set-AzureRole** cmdlet:</span></span>

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

<span data-ttu-id="15380-117">Il cmdlet si blocca temporaneamente durante il provisioning e l'avvio delle nuove istanze.</span><span class="sxs-lookup"><span data-stu-id="15380-117">The cmdlet blocks momentarily while the new instances are provisioned and started.</span></span> <span data-ttu-id="15380-118">Se durante questo periodo si apre una nuova finestra di PowerShell e si chiama **Get-AzureRole** come indicato in precedenza, verrà visualizzato il nuovo numero di istanze di destinazione.</span><span class="sxs-lookup"><span data-stu-id="15380-118">During this time, if you open a new PowerShell window and call **Get-AzureRole** as shown earlier, you will see the new target instance count.</span></span> <span data-ttu-id="15380-119">Se si controlla lo stato del ruolo nel portale, si vedrà che per la nuova istanza è indicato che l'avvio è in corso:</span><span class="sxs-lookup"><span data-stu-id="15380-119">And if you inspect the role status in the portal, you should see the new instance starting up:</span></span>

![Avvio dell'istanza VM in corso nel portale](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

<span data-ttu-id="15380-121">Una volta avviate le nuove istanze, il cmdlet restituirà il controllo indicando la riuscita dell'operazione:</span><span class="sxs-lookup"><span data-stu-id="15380-121">Once the new instances have started, the cmdlet will return successfully:</span></span>

![Aumento delle istanze del ruolo riuscito](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-the-role-by-removing-instances"></a><span data-ttu-id="15380-123">Ridurre il numero di istanze per il ruolo rimuovendo istanze</span><span class="sxs-lookup"><span data-stu-id="15380-123">Scale in the role by removing instances</span></span>

<span data-ttu-id="15380-124">In modo analogo, è possibile ridurre il numero di istanze per un ruolo rimuovendo istanze.</span><span class="sxs-lookup"><span data-stu-id="15380-124">You can scale in a role by removing instances in the same way.</span></span> <span data-ttu-id="15380-125">Impostare il parametro **Count** di **Set-AzureRole** sul numero di istanze da ottenere al termine dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="15380-125">Set the **Count** parameter on **Set-AzureRole** to the number of instances you want to have after the scale in operation is complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15380-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="15380-126">Next steps</span></span>

<span data-ttu-id="15380-127">Non è possibile configurare la scalabilità automatica per i servizi cloud da PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15380-127">It is not possible to configure auto-scale for cloud services from PowerShell.</span></span> <span data-ttu-id="15380-128">Per eseguire questa operazione, vedere [Come configurare la scalabilità automatica di un servizio cloud](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="15380-128">To do that, see [How to auto scale a cloud service](cloud-services-how-to-scale-portal.md).</span></span>
