---
title: un servizio cloud di Azure in Windows PowerShell aaaScale | Documenti Microsoft
description: (versione classica) Informazioni su come toouse PowerShell tooscale un ruolo web o un ruolo di lavoro in o out in Azure.
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
ms.openlocfilehash: cfac6660e84f8ae24e4e9bdd5bf2016fb9cd7045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-a-cloud-service-in-powershell"></a><span data-ttu-id="9da85-103">Come tooscale un cloud service in PowerShell</span><span class="sxs-lookup"><span data-stu-id="9da85-103">How tooscale a cloud service in PowerShell</span></span>

<span data-ttu-id="9da85-104">È possibile utilizzare Windows PowerShell tooscale un ruolo web o un ruolo di lavoro in o out aggiungendo o rimuovendo istanze.</span><span class="sxs-lookup"><span data-stu-id="9da85-104">You can use Windows PowerShell tooscale a web role or worker role in or out by adding or removing instances.</span></span>  

## <a name="log-in-tooazure"></a><span data-ttu-id="9da85-105">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="9da85-105">Log in tooAzure</span></span>

<span data-ttu-id="9da85-106">Prima di poter eseguire qualsiasi operazione sulla sottoscrizione tramite PowerShell, è necessario eseguire l'accesso:</span><span class="sxs-lookup"><span data-stu-id="9da85-106">Before you can perform any operations on your subscription through PowerShell, you must log in:</span></span>

```powershell
Add-AzureAccount
```

<span data-ttu-id="9da85-107">Se si dispone di più sottoscrizioni associate all'account, potrebbe essere abbonamento hello toochange a seconda di dove si trova il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="9da85-107">If you have multiple subscriptions associated with your account, you may need toochange hello current subscription depending on where your cloud service resides.</span></span> <span data-ttu-id="9da85-108">toocheck hello sottoscrizione corrente, eseguire:</span><span class="sxs-lookup"><span data-stu-id="9da85-108">toocheck hello current subscription, run:</span></span>

```powershell
Get-AzureSubscription -Current
```

<span data-ttu-id="9da85-109">Se è necessario toochange sottoscrizione corrente di hello, eseguire:</span><span class="sxs-lookup"><span data-stu-id="9da85-109">If you need toochange hello current subscription, run:</span></span>

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-hello-current-instance-count-for-your-role"></a><span data-ttu-id="9da85-110">Verifica numero di istanze per il ruolo corrente hello</span><span class="sxs-lookup"><span data-stu-id="9da85-110">Check hello current instance count for your role</span></span>

<span data-ttu-id="9da85-111">stato corrente di hello toocheck del ruolo, eseguire:</span><span class="sxs-lookup"><span data-stu-id="9da85-111">toocheck hello current state of your role, run:</span></span>

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

<span data-ttu-id="9da85-112">È necessario ottenere informazioni sul ruolo hello, incluso il relativo numero di versione e l'istanza del sistema operativo corrente.</span><span class="sxs-lookup"><span data-stu-id="9da85-112">You should get back information about hello role, including its current OS version and instance count.</span></span> <span data-ttu-id="9da85-113">In questo caso, il ruolo di hello dispone di una singola istanza.</span><span class="sxs-lookup"><span data-stu-id="9da85-113">In this case, hello role has a single instance.</span></span>

![Informazioni sul ruolo hello](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-hello-role-by-adding-more-instances"></a><span data-ttu-id="9da85-115">Scalabilità orizzontale aggiungendo altre istanze del ruolo hello</span><span class="sxs-lookup"><span data-stu-id="9da85-115">Scale out hello role by adding more instances</span></span>

<span data-ttu-id="9da85-116">tooscale orizzontale il ruolo, passaggio hello numero desiderato di istanze come hello **conteggio** parametro toohello **Set-AzureRole** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9da85-116">tooscale out your role, pass hello desired number of instances as hello **Count** parameter toohello **Set-AzureRole** cmdlet:</span></span>

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

<span data-ttu-id="9da85-117">blocchi di cmdlet Hello temporaneamente durante le nuove istanze hello vengono configurati e avviati.</span><span class="sxs-lookup"><span data-stu-id="9da85-117">hello cmdlet blocks momentarily while hello new instances are provisioned and started.</span></span> <span data-ttu-id="9da85-118">Durante questo periodo, se si apre una nuova finestra di PowerShell e chiamare **Get-AzureRole** come illustrato in precedenza, è possibile vedere conteggio delle istanze hello nuova destinazione.</span><span class="sxs-lookup"><span data-stu-id="9da85-118">During this time, if you open a new PowerShell window and call **Get-AzureRole** as shown earlier, you will see hello new target instance count.</span></span> <span data-ttu-id="9da85-119">E, se si analizza lo stato di ruolo hello nel portale di hello, dovrebbe essere nuova istanza di hello avvio:</span><span class="sxs-lookup"><span data-stu-id="9da85-119">And if you inspect hello role status in hello portal, you should see hello new instance starting up:</span></span>

![Avvio dell'istanza VM in corso nel portale](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

<span data-ttu-id="9da85-121">Una volta avviate le nuove istanze hello, hello cmdlet restituirà correttamente:</span><span class="sxs-lookup"><span data-stu-id="9da85-121">Once hello new instances have started, hello cmdlet will return successfully:</span></span>

![Aumento delle istanze del ruolo riuscito](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-hello-role-by-removing-instances"></a><span data-ttu-id="9da85-123">Scala nel ruolo hello tramite la rimozione di istanze</span><span class="sxs-lookup"><span data-stu-id="9da85-123">Scale in hello role by removing instances</span></span>

<span data-ttu-id="9da85-124">È possibile scalare in un ruolo tramite la rimozione di istanze in hello allo stesso modo.</span><span class="sxs-lookup"><span data-stu-id="9da85-124">You can scale in a role by removing instances in hello same way.</span></span> <span data-ttu-id="9da85-125">Set hello **conteggio** parametro **Set-AzureRole** toohello numero di istanze desiderato toohave dopo scala hello nell'operazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="9da85-125">Set hello **Count** parameter on **Set-AzureRole** toohello number of instances you want toohave after hello scale in operation is complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9da85-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9da85-126">Next steps</span></span>

<span data-ttu-id="9da85-127">Non è possibile tooconfigure scalabilità automatica per i servizi cloud da PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9da85-127">It is not possible tooconfigure auto-scale for cloud services from PowerShell.</span></span> <span data-ttu-id="9da85-128">toodo che, vedere [le modalità di scalabilità di un servizio cloud tooauto](cloud-services-how-to-scale-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9da85-128">toodo that, see [How tooauto scale a cloud service](cloud-services-how-to-scale-portal.md).</span></span>
