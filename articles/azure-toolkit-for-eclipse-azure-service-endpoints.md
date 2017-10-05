---
title: Endpoint del servizio di Azure
description: "Descrive le impostazioni dell’Endpoint del servizio di Azure nel Toolkit di Azure per Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9c6125ec-7278-461e-b69c-ed56e844f742
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6059c292c2687f1bf3d9be04c03aaaaf6adde945
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-service-endpoints"></a><span data-ttu-id="28f5a-103">Endpoint del servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="28f5a-103">Azure Service Endpoints</span></span>
<span data-ttu-id="28f5a-104">Gli endpoint del servizio di Azure determinano se l'applicazione è distribuita e gestita dalla piattaforma Azure globale, da Azure gestito da 21Vianet in Cina o da una piattaforma Azure privata.</span><span class="sxs-lookup"><span data-stu-id="28f5a-104">Azure service endpoints determine whether your application is deployed to and managed by the global Azure platform, Azure operated by 21Vianet in China, or a private Azure platform.</span></span> <span data-ttu-id="28f5a-105">La finestra di dialogo **Endpoint del servizio** consente di specificare quali endpoint del servizio si desidera usare.</span><span class="sxs-lookup"><span data-stu-id="28f5a-105">The **Service Endpoints** dialog allows you to specify which service endpoints you want to use.</span></span> <span data-ttu-id="28f5a-106">Per aprire la finestra di dialogo **Service Endpoints** (Endpoint del servizio), in Eclipse fare clic su **Window** (Finestra) e quindi su **Preferences** (Preferenze), espandere **Azure** e infine fare clic su **Service Endpoints** (Endpoint del servizio).</span><span class="sxs-lookup"><span data-stu-id="28f5a-106">To open the **Service Endpoints** dialog, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Service Endpoints**.</span></span> <span data-ttu-id="28f5a-107">L'impostazione del campo **Set attivo** determina quali endpoint del servizio di Azure verranno usati per i progetti di Azure nell'area di lavoro corrente.</span><span class="sxs-lookup"><span data-stu-id="28f5a-107">Setting the **Active Set** field determines which Azure service endpoints will be used for the Azure projects in your current workspace.</span></span>

<span data-ttu-id="28f5a-108">Di seguito viene mostrata la finestra di dialogo **Endpoint del servizio** .</span><span class="sxs-lookup"><span data-stu-id="28f5a-108">The following shows the **Service Endpoints** dialog.</span></span>

![][ic719493]

## <a name="to-set-the-service-endpoints"></a><span data-ttu-id="28f5a-109">Per impostare gli endpoint del servizio</span><span class="sxs-lookup"><span data-stu-id="28f5a-109">To set the service endpoints</span></span>
<span data-ttu-id="28f5a-110">Nella finestra di dialogo **Endpoint del servizio** , eseguire una delle seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="28f5a-110">In the **Service Endpoints** dialog, take one of the following actions:</span></span>

* <span data-ttu-id="28f5a-111">Se si vuole usare la piattaforma Azure globale, nell'elenco a discesa **Active Set** (Set attivo) selezionare **windowsazure.com** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="28f5a-111">If you want to use the global Azure platform, from the **Active Set** dropdown list, select **windowsazure.com** and click **OK**.</span></span>

* <span data-ttu-id="28f5a-112">Se si vuole usare Azure gestito da 21Vianet in Cina, nell'elenco a discesa **Active Set** (Set attivo) selezionare **windowsazure.cn (China)** (windowsazure.cn - Cina) e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="28f5a-112">If you want to use Azure operated by 21Vianet in China, from the **Active Set** dropdown list, select **windowsazure.cn (China)** and click **OK**.</span></span>

* <span data-ttu-id="28f5a-113">Se si desidera utilizzare una piattaforma Azure privata:</span><span class="sxs-lookup"><span data-stu-id="28f5a-113">If you want to use a private Azure platform:</span></span>

  1. <span data-ttu-id="28f5a-114">Fare clic su **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="28f5a-114">Click **Edit**.</span></span>

  2. <span data-ttu-id="28f5a-115">Verrà visualizzata una finestra di dialogo che informa che la finestra di dialogo **Endpoint del servizio** verrà chiusa e che verrà aperto il file dei set di preferenza.</span><span class="sxs-lookup"><span data-stu-id="28f5a-115">A dialog box opens, informing you that the **Service Endpoints** dialog will be closed, and the preference sets file will be opened.</span></span> <span data-ttu-id="28f5a-116">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="28f5a-116">Click **OK**.</span></span>

  3. <span data-ttu-id="28f5a-117">Nel file preferencesets.xml, creare un nuovo elemento `preferenceset` .</span><span class="sxs-lookup"><span data-stu-id="28f5a-117">In the preferencesets.xml file, create a new `preferenceset` element.</span></span> <span data-ttu-id="28f5a-118">Per questo nuovo elemento, creare gli attributi `name`, `blob`, `management`, `portalURL` e `publishsettings` e aggiungere ad essi valori che corrispondano alla piattaforma Azure privata.</span><span class="sxs-lookup"><span data-stu-id="28f5a-118">For this new element, create `name`, `blob`, `management`, `portalURL` and `publishsettings` attributes, and add values for them that correspond to your private Azure platform.</span></span> <span data-ttu-id="28f5a-119">È possibile utilizzare i valori forniti dagli elementi esistenti `preferenceset` come modelli.</span><span class="sxs-lookup"><span data-stu-id="28f5a-119">You can use the values provided for the existing `preferenceset` elements as templates.</span></span> <span data-ttu-id="28f5a-120">**Nota**: il valore usato per l'attributo `blob` deve contenere il testo "blob" nell'URL.</span><span class="sxs-lookup"><span data-stu-id="28f5a-120">**Note**: The value used for the `blob` attribute must contain the text "blob" in the URL.</span></span>

  4. <span data-ttu-id="28f5a-121">Salvare e chiudere preferencesets.xml.</span><span class="sxs-lookup"><span data-stu-id="28f5a-121">Save and close preferencesets.xml.</span></span>

  5. <span data-ttu-id="28f5a-122">Riaprire la finestra di dialogo **Endpoint del servizio** .</span><span class="sxs-lookup"><span data-stu-id="28f5a-122">Reopen the **Service Endpoints** dialog.</span></span>

  6. <span data-ttu-id="28f5a-123">Nell'elenco a discesa **Active Set** (Set attivo) selezionare il set attivo creato e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="28f5a-123">From the **Active Set** dropdown list, select the active set that you created and click **OK**.</span></span>

  7. <span data-ttu-id="28f5a-124">Dopo aver creato l'elemento `preferenceset` della piattaforma Azure privata, è possibile modificare i valori assegnati facendo clic sul pulsante **Edit** (Modifica) nella finestra di dialogo **Service Endpoints** (Endpoint del servizio).</span><span class="sxs-lookup"><span data-stu-id="28f5a-124">Once you've created your private Azure platform `preferenceset` element, you can change the values assigned to it by clicking the **Edit** button in the **Services Endpoint** dialog.</span></span> <span data-ttu-id="28f5a-125">È inoltre possibile creare più elementi `preferenceset` della piattaforma Azure privata, se lo si desidera.</span><span class="sxs-lookup"><span data-stu-id="28f5a-125">You can also create multiple private Azure platform `preferenceset` elements, if you desire.</span></span>

## <a name="see-also"></a><span data-ttu-id="28f5a-126">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="28f5a-126">See Also</span></span>
<span data-ttu-id="28f5a-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="28f5a-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="28f5a-128">[Installazione di Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="28f5a-128">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="28f5a-129">[Creare un'applicazione Hello World per Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="28f5a-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="28f5a-130">Per altre informazioni su come usare Azure con Java, vedere il [Centro per sviluppatori Java di Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="28f5a-130">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
