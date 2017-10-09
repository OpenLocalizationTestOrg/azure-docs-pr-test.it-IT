---
title: un progetto di servizio cloud di Azure con Visual Studio aaaCreating | Documenti Microsoft
description: Informazioni su ora toocreate un progetto di servizio cloud di Azure con Visual Studio
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3c357016aa423688199a7ab3a670115e33a98fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="4d8e4-103">Creazione di un progetto di servizio cloud di Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4d8e4-103">Creating an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="4d8e4-104">Hello Azure Tools per Visual Studio fornisce un modello di progetto che consente di creare un servizio cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d8e4-104">hello Azure Tools for Visual Studio provides a project template that lets you create an Azure cloud service.</span></span> <span data-ttu-id="4d8e4-105">Dopo aver creato il progetto di hello, Visual Studio consente tooconfigure, eseguire il debug e distribuire tooAzure servizio cloud di hello.</span><span class="sxs-lookup"><span data-stu-id="4d8e4-105">Once hello project has been created, Visual Studio enables you tooconfigure, debug, and deploy hello cloud service tooAzure.</span></span>

## <a name="steps-toocreate-an-azure-cloud-service-project-in-visual-studio"></a><span data-ttu-id="4d8e4-106">Passaggi toocreate un progetto di servizio cloud di Azure in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4d8e4-106">Steps toocreate an Azure cloud service project in Visual Studio</span></span>
<span data-ttu-id="4d8e4-107">In questa sezione viene illustrata la creazione di un progetto di servizio cloud di Azure in Visual Studio con uno o più ruoli Web.</span><span class="sxs-lookup"><span data-stu-id="4d8e4-107">This section walks you through creating an Azure cloud service project in Visual Studio with one or more web roles.</span></span>  

1. <span data-ttu-id="4d8e4-108">Avviare Visual Studio come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4d8e4-108">Start Visual Studio as an administrator.</span></span>

1. <span data-ttu-id="4d8e4-109">Scegliere dal menu principale hello **File** > **New** > **progetto**.</span><span class="sxs-lookup"><span data-stu-id="4d8e4-109">On hello main menu, select **File** > **New** > **Project**.</span></span>

1. <span data-ttu-id="4d8e4-110">Selezionare **Cloud** da hello Visual c# o Visual Basic i nodi di modello di progetto e selezionare **servizio Cloud di Azure** elenco hello di modelli.</span><span class="sxs-lookup"><span data-stu-id="4d8e4-110">Select **Cloud** from hello Visual C# or Visual Basic project template nodes, and select **Azure Cloud Service** from hello list of templates.</span></span>

    ![Nuovo servizio cloud di Azure](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. <span data-ttu-id="4d8e4-112">Specificare la versione di hello .NET Framework si desidera toouse toodevelop il progetto.</span><span class="sxs-lookup"><span data-stu-id="4d8e4-112">Specify which version of hello .NET Framework you want toouse toodevelop your project.</span></span>

1. <span data-ttu-id="4d8e4-113">Immettere un nome e percorso per il progetto e un nome per la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="4d8e4-113">Enter a name and location for your project and a name for hello solution.</span></span> 

1. <span data-ttu-id="4d8e4-114">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="4d8e4-114">Select **OK**.</span></span>

1. <span data-ttu-id="4d8e4-115">In hello **nuovo servizio Cloud di Microsoft Azure** finestra di dialogo, i ruoli selezionare hello che si desidera tooadd e scegliere tooadd pulsante freccia destra di hello li tooyour soluzione.</span><span class="sxs-lookup"><span data-stu-id="4d8e4-115">In hello **New Microsoft Azure Cloud Service** dialog, select hello roles that you want tooadd, and choose hello right arrow button tooadd them tooyour solution.</span></span>

    ![Selezionare i ruoli del nuovo servizio cloud di Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. <span data-ttu-id="4d8e4-117">un ruolo che si è aggiunto, al passaggio del mouse sul ruolo hello in hello toorename **nuovo servizio Cloud di Microsoft Azure** finestra di dialogo, selezionare il menu di scelta rapida hello **rinominare**.</span><span class="sxs-lookup"><span data-stu-id="4d8e4-117">toorename a role that you've added, hover on hello role in hello **New Microsoft Azure Cloud Service** dialog, and, from hello context menu, select **Rename**.</span></span> <span data-ttu-id="4d8e4-118">È inoltre possibile rinominare un ruolo all'interno della soluzione (in hello **Esplora**) dopo che è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="4d8e4-118">You can also rename a role within your solution (in hello **Solution Explorer**) after it has been added.</span></span>

    ![Rinominare un ruolo dei servizi cloud di Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

<span data-ttu-id="4d8e4-120">progetto di Visual Studio Azure Hello dispone di associazioni toohello ruolo progetti nella soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="4d8e4-120">hello Visual Studio Azure project has associations toohello role projects in hello solution.</span></span> <span data-ttu-id="4d8e4-121">progetto Hello include anche hello *file di definizione del servizio* e *file di configurazione del servizio*:</span><span class="sxs-lookup"><span data-stu-id="4d8e4-121">hello project also includes hello *service definition file* and *service configuration file*:</span></span>

- <span data-ttu-id="4d8e4-122">**File di definizione del servizio** -definisce le impostazioni di runtime hello per l'applicazione, inclusi i ruoli sono necessari, endpoint e dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4d8e4-122">**Service definition file** - Defines hello runtime settings for your application, including what roles are required, endpoints, and virtual machine size.</span></span> 
- <span data-ttu-id="4d8e4-123">**File di configurazione del servizio** -consente di configurare il numero di istanze di un ruolo viene eseguito e hello valori delle impostazioni di hello è definite per un ruolo.</span><span class="sxs-lookup"><span data-stu-id="4d8e4-123">**Service configuration file** - Configures how many instances of a role are run and hello values of hello settings defined for a role.</span></span> 

<span data-ttu-id="4d8e4-124">Per ulteriori informazioni su questi file, vedere [configurare i ruoli di hello per un servizio cloud di Azure con Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="4d8e4-124">For more information about these files, see [Configure hello Roles for an Azure cloud service with Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d8e4-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4d8e4-125">Next steps</span></span>
- [<span data-ttu-id="4d8e4-126">Gestione dei ruoli nei progetti di servizi cloud di Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4d8e4-126">Managing roles in Azure cloud service projects with Visual Studio</span></span>](./vs-azure-tools-cloud-service-project-managing-roles.md)
