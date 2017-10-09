---
title: un progetto di servizio cloud di Azure con Visual Studio aaaConfigure | Documenti Microsoft
description: Informazioni di progetto di servizio in Visual Studio, a seconda dei requisiti per il progetto cloud tooconfigure di Azure.
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
ms.openlocfilehash: 40eb5eedd6ea23bf03c8707431799be28beae701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="32cd4-103">Configurare un progetto di servizio cloud di Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="32cd4-103">Configure an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="32cd4-104">È possibile configurare un progetto di servizio cloud di Azure, in base ai requisiti specifici per il progetto.</span><span class="sxs-lookup"><span data-stu-id="32cd4-104">You can configure an Azure cloud service project, depending on your requirements for that project.</span></span> <span data-ttu-id="32cd4-105">È possibile impostare proprietà per il progetto di hello per hello seguenti categorie:</span><span class="sxs-lookup"><span data-stu-id="32cd4-105">You can set properties for hello project for hello following categories:</span></span>

- <span data-ttu-id="32cd4-106">**Pubblicare un tooAzure servizio cloud** -è possibile impostare una proprietà toomake assicurarsi che un servizio distribuito tooAzure di esistente cloud non è stato eliminato accidentalmente.</span><span class="sxs-lookup"><span data-stu-id="32cd4-106">**Publish a cloud service tooAzure** - You can set a property toomake sure that an existing cloud service deployed tooAzure is not accidentally deleted.</span></span>
- <span data-ttu-id="32cd4-107">**Eseguire o eseguire il debug di un servizio cloud nel computer locale hello** -è possibile selezionare un toouse di configurazione del servizio e indicare se si desidera toostart hello emulatore di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="32cd4-107">**Run or debug a cloud service on hello local computer** - You can select a service configuration toouse and indicate whether you want toostart hello Azure storage emulator.</span></span>
- <span data-ttu-id="32cd4-108">**Convalidare un pacchetto del servizio cloud al momento della creazione** -è possibile decidere tootreat gli avvisi come errori, in modo che è possibile verificare il pacchetto del servizio cloud hello distribuisce senza problemi.</span><span class="sxs-lookup"><span data-stu-id="32cd4-108">**Validate a cloud service package when it is created** - You can decide tootreat any warnings as errors so that you can ensure that hello cloud service package deploys without any issues.</span></span> 

## <a name="steps-tooconfigure-an-azure-cloud-service-project"></a><span data-ttu-id="32cd4-109">Passaggi tooconfigure un progetto di servizio cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="32cd4-109">Steps tooconfigure an Azure cloud service project</span></span>
1. <span data-ttu-id="32cd4-110">Aprire o creare un progetto di servizio cloud in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="32cd4-110">Open or create a cloud service project in Visual Studio</span></span>

1. <span data-ttu-id="32cd4-111">In **Esplora**, fare clic sul progetto hello e selezionare il menu di scelta rapida hello **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="32cd4-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>
   
1. <span data-ttu-id="32cd4-112">Nella pagina delle proprietà del progetto hello, selezionare hello **sviluppo** scheda.</span><span class="sxs-lookup"><span data-stu-id="32cd4-112">In hello project's properties page, select hello **Development** tab.</span></span>

    ![Menu Proprietà del progetto](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. <span data-ttu-id="32cd4-114">Impostare **Chiedi conferma prima di eliminare una distribuzione esistente** troppo**True**.</span><span class="sxs-lookup"><span data-stu-id="32cd4-114">Set **Prompt before deleting an existing deployment** too**True**.</span></span> <span data-ttu-id="32cd4-115">Questa impostazione consente di tooensure non è stato eliminato accidentalmente una distribuzione esistente in Azure</span><span class="sxs-lookup"><span data-stu-id="32cd4-115">This setting helps tooensure you don't accidentally delete an existing deployment in Azure</span></span>

1. <span data-ttu-id="32cd4-116">Seleziona hello desiderato **configurazione del servizio** tooindicate la configurazione di servizio desiderato toouse quando si esegue o eseguire il debug del servizio cloud localmente.</span><span class="sxs-lookup"><span data-stu-id="32cd4-116">Select hello desired **Service configuration** tooindicate which service configuration you want toouse when you run or debug your cloud service locally.</span></span> <span data-ttu-id="32cd4-117">Per ulteriori informazioni su come toomodify una configurazione del servizio per un ruolo, vedere [come tooconfigure hello ruoli per un Azure cloud del servizio con Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="32cd4-117">For more information on how toomodify a service configuration for a role, see [How tooconfigure hello roles for an Azure cloud service with Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

1. <span data-ttu-id="32cd4-118">Impostare **emulatore di archiviazione Azure avvia** troppo**True** toostart hello emulatore di archiviazione Azure quando si esegue o eseguire il debug del servizio cloud localmente.</span><span class="sxs-lookup"><span data-stu-id="32cd4-118">Set **Start Azure storage emulator** too**True** toostart hello Azure storage emulator when you run or debug your cloud service locally.</span></span>

1. <span data-ttu-id="32cd4-119">Impostare **considerarli come errori** troppo**True** toomake che non è possibile pubblicare se sono presenti errori di convalida del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="32cd4-119">Set **Treat warnings as errors** too**True** toomake sure you cannot publish if there are package validation errors.</span></span>

1. <span data-ttu-id="32cd4-120">Impostare **utilizzare porte del progetto web** troppo**True** toomake assicurarsi che il ruolo web Usa hello stessa porta ogni volta che viene avviato in locale in IIS Express.</span><span class="sxs-lookup"><span data-stu-id="32cd4-120">Set **Use web project ports** too**True** toomake sure that your web role uses hello same port each time it starts locally in IIS Express.</span></span>

1. <span data-ttu-id="32cd4-121">Barra degli strumenti di Visual Studio hello, selezionare **salvare**.</span><span class="sxs-lookup"><span data-stu-id="32cd4-121">From hello Visual Studio toolbar, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32cd4-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="32cd4-122">Next steps</span></span>
- [<span data-ttu-id="32cd4-123">Configurare un progetto di servizio cloud di Azure tramite più configurazioni del servizio</span><span class="sxs-lookup"><span data-stu-id="32cd4-123">Configure an Azure project using multiple service configurations</span></span>](vs-azure-tools-multiple-services-project-configurations.md)

