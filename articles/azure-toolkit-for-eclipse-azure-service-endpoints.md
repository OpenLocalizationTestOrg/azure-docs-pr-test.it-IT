---
title: aaaAzure gli endpoint del servizio
description: Descrive le impostazioni di Endpoint del servizio Azure hello in hello Azure Toolkit per Eclipse.
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
ms.openlocfilehash: 357aa56409a894719077f2c8f302575c8ebb6883
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-endpoints"></a><span data-ttu-id="30706-103">Endpoint del servizio di Azure</span><span class="sxs-lookup"><span data-stu-id="30706-103">Azure Service Endpoints</span></span>
<span data-ttu-id="30706-104">Gli endpoint del servizio Azure determinano che se l'applicazione è distribuita tooand gestita dalla piattaforma Azure globale hello, Azure gestito da 21Vianet in Cina o una privata piattaforma Azure.</span><span class="sxs-lookup"><span data-stu-id="30706-104">Azure service endpoints determine whether your application is deployed tooand managed by hello global Azure platform, Azure operated by 21Vianet in China, or a private Azure platform.</span></span> <span data-ttu-id="30706-105">Hello **gli endpoint del servizio** finestra di dialogo consente toospecify che si desidera toouse endpoint del servizio.</span><span class="sxs-lookup"><span data-stu-id="30706-105">hello **Service Endpoints** dialog allows you toospecify which service endpoints you want toouse.</span></span> <span data-ttu-id="30706-106">hello tooopen **gli endpoint del servizio** finestra di dialogo, in Eclipse, fare clic su **finestra**, fare clic su **preferenze**, espandere **Azure**, quindi fare clic su **Gli endpoint del servizio**.</span><span class="sxs-lookup"><span data-stu-id="30706-106">tooopen hello **Service Endpoints** dialog, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Service Endpoints**.</span></span> <span data-ttu-id="30706-107">Hello impostazione **Active Set** campo determina quale servizio di Azure verranno utilizzati l'endpoint per hello Azure progetti nell'area di lavoro corrente.</span><span class="sxs-lookup"><span data-stu-id="30706-107">Setting hello **Active Set** field determines which Azure service endpoints will be used for hello Azure projects in your current workspace.</span></span>

<span data-ttu-id="30706-108">Hello seguente illustra la hello **gli endpoint del servizio** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="30706-108">hello following shows hello **Service Endpoints** dialog.</span></span>

![][ic719493]

## <a name="tooset-hello-service-endpoints"></a><span data-ttu-id="30706-109">endpoint del servizio hello tooset</span><span class="sxs-lookup"><span data-stu-id="30706-109">tooset hello service endpoints</span></span>
<span data-ttu-id="30706-110">In hello **gli endpoint del servizio** finestra di dialogo, eseguire una di hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="30706-110">In hello **Service Endpoints** dialog, take one of hello following actions:</span></span>

* <span data-ttu-id="30706-111">Se si desidera toouse hello piattaforma Azure globale, da hello **Active Set** elenco a discesa, seleziona **windowsazure.com** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="30706-111">If you want toouse hello global Azure platform, from hello **Active Set** dropdown list, select **windowsazure.com** and click **OK**.</span></span>

* <span data-ttu-id="30706-112">Se si desidera toouse Azure gestito da 21Vianet in Cina, da hello **Active Set** elenco a discesa, seleziona **windowsazure.cn (China)** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="30706-112">If you want toouse Azure operated by 21Vianet in China, from hello **Active Set** dropdown list, select **windowsazure.cn (China)** and click **OK**.</span></span>

* <span data-ttu-id="30706-113">Se si desidera toouse una piattaforma Azure privata:</span><span class="sxs-lookup"><span data-stu-id="30706-113">If you want toouse a private Azure platform:</span></span>

  1. <span data-ttu-id="30706-114">Fare clic su **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="30706-114">Click **Edit**.</span></span>

  2. <span data-ttu-id="30706-115">Verrà visualizzata una finestra di dialogo che informa che hello **gli endpoint del servizio** finestra di dialogo verrà chiusa e verranno aperto hello preferenza set di file.</span><span class="sxs-lookup"><span data-stu-id="30706-115">A dialog box opens, informing you that hello **Service Endpoints** dialog will be closed, and hello preference sets file will be opened.</span></span> <span data-ttu-id="30706-116">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="30706-116">Click **OK**.</span></span>

  3. <span data-ttu-id="30706-117">Nel file preferencesets.xml hello, creare un nuovo `preferenceset` elemento.</span><span class="sxs-lookup"><span data-stu-id="30706-117">In hello preferencesets.xml file, create a new `preferenceset` element.</span></span> <span data-ttu-id="30706-118">Per questo nuovo elemento, creare `name`, `blob`, `management`, `portalURL` e `publishsettings` gli attributi e aggiungere i valori per tale piattaforma Azure privata tooyour corrispondono.</span><span class="sxs-lookup"><span data-stu-id="30706-118">For this new element, create `name`, `blob`, `management`, `portalURL` and `publishsettings` attributes, and add values for them that correspond tooyour private Azure platform.</span></span> <span data-ttu-id="30706-119">È possibile utilizzare i valori hello forniti hello esistenti `preferenceset` elementi come modelli.</span><span class="sxs-lookup"><span data-stu-id="30706-119">You can use hello values provided for hello existing `preferenceset` elements as templates.</span></span> <span data-ttu-id="30706-120">**Nota**: hello valore utilizzato per hello `blob` attributo deve contenere il testo hello "blob" nell'URL hello.</span><span class="sxs-lookup"><span data-stu-id="30706-120">**Note**: hello value used for hello `blob` attribute must contain hello text "blob" in hello URL.</span></span>

  4. <span data-ttu-id="30706-121">Salvare e chiudere preferencesets.xml.</span><span class="sxs-lookup"><span data-stu-id="30706-121">Save and close preferencesets.xml.</span></span>

  5. <span data-ttu-id="30706-122">Riaprire hello **gli endpoint del servizio** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="30706-122">Reopen hello **Service Endpoints** dialog.</span></span>

  6. <span data-ttu-id="30706-123">Da hello **Active Set** dall'elenco a discesa selezionare hello attivo imposta creata e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="30706-123">From hello **Active Set** dropdown list, select hello active set that you created and click **OK**.</span></span>

  7. <span data-ttu-id="30706-124">Dopo aver creato la piattaforma Azure privata `preferenceset` elemento, è possibile modificare hello tooit di valori assegnati facendo hello **modifica** pulsante hello **Endpoint dei servizi** finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="30706-124">Once you've created your private Azure platform `preferenceset` element, you can change hello values assigned tooit by clicking hello **Edit** button in hello **Services Endpoint** dialog.</span></span> <span data-ttu-id="30706-125">È inoltre possibile creare più elementi `preferenceset` della piattaforma Azure privata, se lo si desidera.</span><span class="sxs-lookup"><span data-stu-id="30706-125">You can also create multiple private Azure platform `preferenceset` elements, if you desire.</span></span>

## <a name="see-also"></a><span data-ttu-id="30706-126">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="30706-126">See Also</span></span>
<span data-ttu-id="30706-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="30706-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="30706-128">[L'installazione di hello Azure Toolkit per Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="30706-128">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="30706-129">[Creare un'applicazione Hello World per Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="30706-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="30706-130">Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="30706-130">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
