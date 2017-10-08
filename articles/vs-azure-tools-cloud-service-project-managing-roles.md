---
title: i ruoli aaaManaging in Azure cloud services con Visual Studio | Documenti Microsoft
description: Informazioni su come tooadd e rimuovere i ruoli in Azure cloud services con Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 131edc534d1110ba3d25cd00a3a24b643576875c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a><span data-ttu-id="e2e00-103">Gestione dei ruoli nei servizi cloud di Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e2e00-103">Managing roles in Azure cloud services with Visual Studio</span></span>
<span data-ttu-id="e2e00-104">Dopo aver creato il servizio cloud di Azure, è possibile aggiungere nuovi ruoli tooit o rimuovere quelli esistenti.</span><span class="sxs-lookup"><span data-stu-id="e2e00-104">After you have created your Azure cloud service, you can add new roles tooit or remove existing roles from it.</span></span> <span data-ttu-id="e2e00-105">È inoltre possibile importare un progetto esistente e convertirlo tooa ruolo.</span><span class="sxs-lookup"><span data-stu-id="e2e00-105">You can also import an existing project and convert it tooa role.</span></span> <span data-ttu-id="e2e00-106">Ad esempio, è possibile importare un'applicazione Web ASP.NET e specificarla come ruolo Web.</span><span class="sxs-lookup"><span data-stu-id="e2e00-106">For example, you can import an ASP.NET web application and designate it as a web role.</span></span>

## <a name="adding-a-role-tooan-azure-cloud-service"></a><span data-ttu-id="e2e00-107">Aggiunta di un servizio cloud di Azure di tooan ruolo</span><span class="sxs-lookup"><span data-stu-id="e2e00-107">Adding a role tooan Azure cloud service</span></span>
<span data-ttu-id="e2e00-108">Hello alla procedura seguente illustra l'aggiunta di un web o lavoro ruolo tooan Azure progetto servizio cloud in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e2e00-108">hello following steps guide you through adding a web or worker role tooan Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="e2e00-109">Creare o aprire un progetto del servizio cloud di Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e2e00-109">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="e2e00-110">In **Esplora**, espandere il nodo di progetto hello</span><span class="sxs-lookup"><span data-stu-id="e2e00-110">In **Solution Explorer**, expand hello project node</span></span>

1. <span data-ttu-id="e2e00-111">Pulsante destro del mouse hello **ruoli** menu di scelta rapida nodo toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="e2e00-111">Right-click hello **Roles** node toodisplay hello context menu.</span></span> <span data-ttu-id="e2e00-112">Selezionare il menu di scelta rapida hello **Aggiungi**, quindi selezionare un ruolo web esistente o un ruolo di lavoro dalla soluzione corrente hello o creare un progetto di ruolo web o di lavoro.</span><span class="sxs-lookup"><span data-stu-id="e2e00-112">From hello context menu, select **Add**, then select an existing web role or worker role from hello current solution, or create a web or worker role project.</span></span> <span data-ttu-id="e2e00-113">È inoltre possibile selezionare un progetto appropriato, ad esempio un progetto di applicazione Web ASP.NET, e associarlo a un progetto di ruolo.</span><span class="sxs-lookup"><span data-stu-id="e2e00-113">You can also select an appropriate project, such as an ASP.NET web application project, and associate it with a role project.</span></span>

    ![Opzioni di menu tooadd un progetto di servizio di ruolo tooan cloud di Azure](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a><span data-ttu-id="e2e00-115">Rimuovere un ruolo da un servizio cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="e2e00-115">Removing a role from an Azure cloud service</span></span>
<span data-ttu-id="e2e00-116">Hello seguente procedura consente di rimuovere un ruolo web o di lavoro da un progetto di servizio cloud di Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e2e00-116">hello following steps guide you through removing a web or worker role from an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="e2e00-117">Creare o aprire un progetto del servizio cloud di Azure in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e2e00-117">Create or open an Azure cloud service project in Visual Studio.</span></span>

1. <span data-ttu-id="e2e00-118">In **Esplora**, espandere il nodo di progetto hello</span><span class="sxs-lookup"><span data-stu-id="e2e00-118">In **Solution Explorer**, expand hello project node</span></span>

1. <span data-ttu-id="e2e00-119">Espandere hello **ruoli** nodo.</span><span class="sxs-lookup"><span data-stu-id="e2e00-119">Expand hello **Roles** node.</span></span>

1. <span data-ttu-id="e2e00-120">Nodo di hello rapida desiderato tooremove e, selezionare il menu di scelta rapida hello **rimuovere**.</span><span class="sxs-lookup"><span data-stu-id="e2e00-120">Right-click hello node you want tooremove, and, from hello context menu, select **Remove**.</span></span> 

    ![Opzioni di menu tooadd tooan un ruolo del servizio cloud di Azure](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-tooan-azure-cloud-service-project"></a><span data-ttu-id="e2e00-122">Nuova aggiunta di un progetto di servizio di ruolo tooan cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="e2e00-122">Readding a role tooan Azure cloud service project</span></span>
<span data-ttu-id="e2e00-123">Rimuovere un ruolo dal progetto di servizio cloud, ma in seguito si decide tooadd nuovo ruolo di hello toohello progetto, solo dichiarazione del ruolo hello e gli attributi di base, ad esempio informazioni di diagnostica e di endpoint, vengono aggiunti.</span><span class="sxs-lookup"><span data-stu-id="e2e00-123">If you remove a role from your cloud service project but later decide tooadd hello role back toohello project, only hello role declaration and basic attributes, such as endpoints and diagnostics information, are added.</span></span> <span data-ttu-id="e2e00-124">Nessun risorse o riferimenti aggiuntivi vengono aggiunti toohello `ServiceDefinition.csdef` file o toohello `ServiceConfiguration.cscfg` file.</span><span class="sxs-lookup"><span data-stu-id="e2e00-124">No additional resources or references are added toohello `ServiceDefinition.csdef` file or toohello `ServiceConfiguration.cscfg` file.</span></span> <span data-ttu-id="e2e00-125">Se si desiderano tooadd queste informazioni, è necessario toomanually aggiungerlo nuovamente a questi file.</span><span class="sxs-lookup"><span data-stu-id="e2e00-125">If you want tooadd this information, you need toomanually add it back into these files.</span></span>

<span data-ttu-id="e2e00-126">Ad esempio, è possibile rimuovere un ruolo del servizio web e successivamente si decide di eseguire il backup di questo ruolo tooadd nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="e2e00-126">For example, you might remove a web service role and later you decide tooadd this role back into your solution.</span></span> <span data-ttu-id="e2e00-127">Se si esegue questa operazione, si verificherà un errore.</span><span class="sxs-lookup"><span data-stu-id="e2e00-127">If you do this, an error occurs.</span></span> <span data-ttu-id="e2e00-128">tooprevent questo errore, si dispone di hello tooadd `<LocalResources>` elemento mostrato nel seguente hello XML nuovamente in hello `ServiceDefinition.csdef` file.</span><span class="sxs-lookup"><span data-stu-id="e2e00-128">tooprevent this error, you have tooadd hello `<LocalResources>` element shown in hello following XML back into hello `ServiceDefinition.csdef` file.</span></span> <span data-ttu-id="e2e00-129">Utilizza il nome del ruolo di servizio web hello aggiunto al progetto hello come parte dell'attributo nome hello per hello hello  **<LocalStorage>**  elemento.</span><span class="sxs-lookup"><span data-stu-id="e2e00-129">Use hello name of hello web service role that you added back into hello project as part of hello name attribute for hello **<LocalStorage>** element.</span></span> <span data-ttu-id="e2e00-130">In questo esempio, è il nome di hello del ruolo del servizio web hello **WCFServiceWebRole1**.</span><span class="sxs-lookup"><span data-stu-id="e2e00-130">In this example, hello name of hello web service role is **WCFServiceWebRole1**.</span></span>

    <WebRole name="WCFServiceWebRole1">
        <Sites>
          <Site name="Web">
            <Bindings>
              <Binding name="Endpoint1" endpointName="Endpoint1" />
            </Bindings>
          </Site>
        </Sites>
        <Endpoints>
          <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
          <Import moduleName="Diagnostics" />
        </Imports>
       <LocalResources>
          <LocalStorage name="WCFServiceWebRole1.svclog" sizeInMB="1000" cleanOnRoleRecycle="false" />
       </LocalResources>
    </WebRole>

## <a name="next-steps"></a><span data-ttu-id="e2e00-131">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e2e00-131">Next steps</span></span>
- [<span data-ttu-id="e2e00-132">Configurare i ruoli di hello per un servizio cloud di Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e2e00-132">Configure hello Roles for an Azure cloud service with Visual Studio</span></span>](vs-azure-tools-configure-roles-for-cloud-service.md)
