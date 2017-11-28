---
title: aaaHow toocreate uno spazio dei nomi Service Bus in hello portale di Azure | Documenti Microsoft
description: Creare uno spazio dei nomi del Bus di servizio utilizzando hello portale di Azure.
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fbb10e62-b133-4851-9d27-40bd844db3ba
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: d8907e7e4a804056f6d66d5a177d9ace967ed2ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-hello-azure-portal"></a><span data-ttu-id="7d770-103">Creare uno spazio dei nomi del Bus di servizio utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7d770-103">Create a Service Bus namespace using hello Azure portal</span></span>

<span data-ttu-id="7d770-104">Uno spazio dei nomi è un contenitore di ambito per tutti i componenti di messaggistica.</span><span class="sxs-lookup"><span data-stu-id="7d770-104">A namespace is a scoping container for all messaging components.</span></span> <span data-ttu-id="7d770-105">Più code e argomenti possono risiedere in un unico spazio dei nomi e gli spazi dei nomi vengono spesso usati come contenitori di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="7d770-105">Multiple queues and topics can reside within a single namespace, and namespaces often serve as application containers.</span></span> <span data-ttu-id="7d770-106">Esistono due modi diversi toocreate uno spazio dei nomi del Bus di servizio:</span><span class="sxs-lookup"><span data-stu-id="7d770-106">There are two different ways toocreate a Service Bus namespace:</span></span>

1. <span data-ttu-id="7d770-107">Portale di Azure (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="7d770-107">Azure portal (this article)</span></span>
2. <span data-ttu-id="7d770-108">[Modelli di Gestione risorse][create-namespace-using-arm]</span><span class="sxs-lookup"><span data-stu-id="7d770-108">[Resource Manager templates][create-namespace-using-arm]</span></span>

## <a name="create-a-namespace-in-hello-azure-portal"></a><span data-ttu-id="7d770-109">Creare uno spazio dei nomi in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="7d770-109">Create a namespace in hello Azure portal</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

<span data-ttu-id="7d770-110">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="7d770-110">Congratulations!</span></span> <span data-ttu-id="7d770-111">È stato creato uno spazio dei nomi per la messaggistica del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="7d770-111">You have now created a Service Bus Messaging namespace.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d770-112">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7d770-112">Next steps</span></span>

<span data-ttu-id="7d770-113">Estrarre il nostro [GitHub esempi][github-samples], che illustrano alcune delle più avanzate funzionalità di messaggistica del Bus di servizio Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7d770-113">Check out our [GitHub samples][github-samples], which show some of hello more advanced features of Azure Service Bus Messaging.</span></span>

[create-namespace-using-arm]: service-bus-resource-manager-overview.md
[github-samples]: https://github.com/Azure/azure-service-bus/tree/master/samples
