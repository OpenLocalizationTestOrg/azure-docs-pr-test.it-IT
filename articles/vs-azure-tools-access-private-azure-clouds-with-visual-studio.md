---
title: aaaAccessing cloud privati di Azure con Visual Studio | Documenti Microsoft
description: Informazioni su come privato tooaccess risorse cloud con Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/19/2017
ms.author: kraigb
ms.openlocfilehash: 5cfd6439afdcf98c6f7d7f29ab6c4256ed02533a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a><span data-ttu-id="73221-103">Accesso ai cloud privati di Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="73221-103">Accessing private Azure clouds with Visual Studio</span></span>
<span data-ttu-id="73221-104">Per impostazione predefinita, Visual Studio supporta gli endpoint REST del cloud pubblico di Azure.</span><span class="sxs-lookup"><span data-stu-id="73221-104">By default, Visual Studio supports public Azure cloud REST endpoints.</span></span> <span data-ttu-id="73221-105">In questo argomento, è illustrato toouse cloud il privata del certificato tooaccess - e interagire con: hello cloud privato da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="73221-105">In this topic, you learn how toouse your private cloud's certificate tooaccess - and interact with - hello private cloud from Visual Studio.</span></span>

## <a name="tooaccess-a-private-azure-cloud-in-visual-studio"></a><span data-ttu-id="73221-106">tooaccess un Azure privato cloud in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="73221-106">tooaccess a private Azure cloud in Visual Studio</span></span>
1. <span data-ttu-id="73221-107">In hello [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885) per cloud privato hello, scaricare il file di impostazioni di pubblicazione o contattare l'amministratore per un file di impostazioni di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="73221-107">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) for hello private cloud, download your publish-settings file, or contact your administrator for a publish-settings file.</span></span> <span data-ttu-id="73221-108">Nella versione pubblica di hello di Azure, hello toodownload collegamento si tratta di [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span><span class="sxs-lookup"><span data-stu-id="73221-108">On hello public version of Azure, hello link toodownload this is [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span></span> <span data-ttu-id="73221-109">(file scaricato hello deve avere l'estensione `.publishsettings`)</span><span class="sxs-lookup"><span data-stu-id="73221-109">(hello downloaded file should have an extension of `.publishsettings`)</span></span>

1. <span data-ttu-id="73221-110">Aprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="73221-110">Open Visual Studio</span></span>

1. <span data-ttu-id="73221-111">In **Esplora Server**, hello rapida **Azure** nodo e selezionare il menu di scelta rapida hello **Gestisci e filtra sottoscrizioni**.</span><span class="sxs-lookup"><span data-stu-id="73221-111">In **Server Explorer**, right-click hello **Azure** node and, from hello context menu, select **Manage and Filter Subscriptions**.</span></span>
   
    ![Comando Gestisci sottoscrizioni](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. <span data-ttu-id="73221-113">In hello **Gestione sottoscrizioni Microsoft Azure** finestra di dialogo, seleziona hello **certificati** scheda e quindi selezionare **importazione**.</span><span class="sxs-lookup"><span data-stu-id="73221-113">In hello **Manage Microsoft Azure Subscriptions** dialog, select hello **Certificates** tab, and then select **Import**.</span></span>
   
    ![Importazione di certificati di Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. <span data-ttu-id="73221-115">In hello **Importa sottoscrizioni di Microsoft Azure** finestra di dialogo Seleziona **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="73221-115">In hello **Import Microsoft Azure Subscriptions** dialog, select **Browse**.</span></span>

    ![Pulsante nella finestra di dialogo Importa sottoscrizioni di Microsoft Azure hello Sfoglia](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. <span data-ttu-id="73221-117">In hello **aprire** finestra di dialogo Sfoglia toohello directory in cui è salvato hello impostazioni di pubblicazione file, selezionare hello file e quindi seleziona **aprire**.</span><span class="sxs-lookup"><span data-stu-id="73221-117">In hello **Open** dialog, browse toohello directory where you saved hello publish-settings file, select hello file, and then select **Open**.</span></span>

    ![Selezionare il file di impostazioni di pubblicazione hello](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. <span data-ttu-id="73221-119">Quando restituito toohello **Importa sottoscrizioni di Microsoft Azure** finestra di dialogo Seleziona **importazione**.</span><span class="sxs-lookup"><span data-stu-id="73221-119">When returned toohello **Import Microsoft Azure Subscriptions** dialog, select **Import**.</span></span>

    ![Importare il file di impostazioni di pubblicazione hello](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    <span data-ttu-id="73221-121">Hello certificati sono importati dal file di impostazioni di pubblicazione hello in Visual Studio e ora è possibile interagire con le risorse di cloud privato.</span><span class="sxs-lookup"><span data-stu-id="73221-121">hello certificates are imported from hello publish-settings file into Visual Studio, and you can now interact with your private cloud resources.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="73221-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="73221-122">Next steps</span></span>
- [<span data-ttu-id="73221-123">Tooan pubblicazione servizio Cloud di Azure da Visual Studio</span><span class="sxs-lookup"><span data-stu-id="73221-123">Publishing tooan Azure Cloud Service from Visual Studio</span></span>](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- <span data-ttu-id="73221-124">[Procedura: Scaricare e importare le impostazioni di pubblicazione e le informazioni sulla sottoscrizione](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span><span class="sxs-lookup"><span data-stu-id="73221-124">[How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span></span>
