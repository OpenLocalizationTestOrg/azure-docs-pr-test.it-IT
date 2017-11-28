---
title: Configurare un progetto di servizio cloud di Azure con Visual Studio | Documentazione Microsoft
description: Informazioni su come configurare un progetto di servizio cloud di Azure in Visuali Studio, in base ai requisiti specifici per il progetto.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: 799715093bd1a8c8e77e6cdb7168670dc263dfa5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="83866-103">Configurare un progetto di servizio cloud di Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="83866-103">Configure an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="83866-104">È possibile configurare un progetto di servizio cloud di Azure, in base ai requisiti specifici per il progetto.</span><span class="sxs-lookup"><span data-stu-id="83866-104">You can configure an Azure cloud service project, depending on your requirements for that project.</span></span> <span data-ttu-id="83866-105">È possibile impostare proprietà per il progetto per le categorie seguenti:</span><span class="sxs-lookup"><span data-stu-id="83866-105">You can set properties for the project for the following categories:</span></span>

- <span data-ttu-id="83866-106">**Pubblicare un servizio cloud in Azure** - È possibile impostare una proprietà per verificare che un servizio cloud esistente distribuito in Azure non venga eliminato inavvertitamente.</span><span class="sxs-lookup"><span data-stu-id="83866-106">**Publish a cloud service to Azure** - You can set a property to make sure that an existing cloud service deployed to Azure is not accidentally deleted.</span></span>
- <span data-ttu-id="83866-107">**Eseguire un servizio cloud o eseguirne il debug nel computer locale** - È possibile selezionare una configurazione del servizio da usare e indicare se si vuole avviare l'emulatore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="83866-107">**Run or debug a cloud service on the local computer** - You can select a service configuration to use and indicate whether you want to start the Azure storage emulator.</span></span>
- <span data-ttu-id="83866-108">**Convalidare un pacchetto del servizio cloud quando viene creato** - È possibile decidere di trattare tutti gli avvisi come errori in modo da assicurarsi che il pacchetto del servizio cloud venga distribuito senza problemi.</span><span class="sxs-lookup"><span data-stu-id="83866-108">**Validate a cloud service package when it is created** - You can decide to treat any warnings as errors so that you can ensure that the cloud service package deploys without any issues.</span></span> 

## <a name="steps-to-configure-an-azure-cloud-service-project"></a><span data-ttu-id="83866-109">Procedura per configurare un progetto di servizio cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="83866-109">Steps to configure an Azure cloud service project</span></span>
1. <span data-ttu-id="83866-110">Aprire o creare un progetto di servizio cloud in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="83866-110">Open or create a cloud service project in Visual Studio</span></span>

1. <span data-ttu-id="83866-111">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto e scegliere **Proprietà** dal menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="83866-111">In **Solution Explorer**, right-click the project, and, from the context menu, select **Properties**.</span></span>
   
1. <span data-ttu-id="83866-112">Nella pagina delle proprietà del progetto, selezionare la scheda **Sviluppo**.</span><span class="sxs-lookup"><span data-stu-id="83866-112">In the project's properties page, select the **Development** tab.</span></span>

    ![Menu Proprietà del progetto](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. <span data-ttu-id="83866-114">Impostare **Chiedi conferma prima di eliminare una distribuzione esistente** su **True**.</span><span class="sxs-lookup"><span data-stu-id="83866-114">Set **Prompt before deleting an existing deployment** to **True**.</span></span> <span data-ttu-id="83866-115">Questa impostazione aiuta a evitare l'eliminazione involontaria di una distribuzione esistente in Azure.</span><span class="sxs-lookup"><span data-stu-id="83866-115">This setting helps to ensure you don't accidentally delete an existing deployment in Azure</span></span>

1. <span data-ttu-id="83866-116">Per indicare la **Configurazione del servizio** da usare durante l'esecuzione o il debug del servizio cloud in locale, nell'elenco Configurazione servizio scegliere la configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="83866-116">Select the desired **Service configuration** to indicate which service configuration you want to use when you run or debug your cloud service locally.</span></span> <span data-ttu-id="83866-117">Per altre informazioni su come modificare una configurazione del servizio per un ruolo, vedere [Procedura: Configurare i ruoli di un servizio cloud di Azure con Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="83866-117">For more information on how to modify a service configuration for a role, see [How to configure the roles for an Azure cloud service with Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

1. <span data-ttu-id="83866-118">Per avviare l'emulatore di archiviazione di Azure durante l'esecuzione o il debug del servizio cloud in locale, in **Avvia l'emulatore di archiviazione di Microsoft Azure** scegliere **True**.</span><span class="sxs-lookup"><span data-stu-id="83866-118">Set **Start Azure storage emulator** to **True** to start the Azure storage emulator when you run or debug your cloud service locally.</span></span>

1. <span data-ttu-id="83866-119">Per assicurarsi che non sia possibile pubblicare se sono presenti errori di convalida del pacchetto, in **Considera gli avvisi come errori** scegliere **True**.</span><span class="sxs-lookup"><span data-stu-id="83866-119">Set **Treat warnings as errors** to **True** to make sure you cannot publish if there are package validation errors.</span></span>

1. <span data-ttu-id="83866-120">Per assicurarsi che il ruolo Web usi la stessa porta a ogni avvio in locale in IIS Express, in **Usa le porte del progetto Web** scegliere **True**.</span><span class="sxs-lookup"><span data-stu-id="83866-120">Set **Use web project ports** to **True** to make sure that your web role uses the same port each time it starts locally in IIS Express.</span></span>

1. <span data-ttu-id="83866-121">Dalla barra degli strumenti di Visual Studio selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="83866-121">From the Visual Studio toolbar, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83866-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="83866-122">Next steps</span></span>
- [<span data-ttu-id="83866-123">Configurare un progetto di servizio cloud di Azure tramite più configurazioni del servizio</span><span class="sxs-lookup"><span data-stu-id="83866-123">Configure an Azure project using multiple service configurations</span></span>](vs-azure-tools-multiple-services-project-configurations.md)

