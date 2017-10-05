---
title: Accesso ai cloud privati di Azure con Visual Studio | Microsoft Docs
description: Informazioni su come accedere alle risorse del cloud privato con Visual Studio.
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
ms.openlocfilehash: b2578c837732ab05d538e9b896ed3a3035075a70
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a><span data-ttu-id="a3e9f-103">Accesso ai cloud privati di Azure con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a3e9f-103">Accessing private Azure clouds with Visual Studio</span></span>
<span data-ttu-id="a3e9f-104">Per impostazione predefinita, Visual Studio supporta gli endpoint REST del cloud pubblico di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3e9f-104">By default, Visual Studio supports public Azure cloud REST endpoints.</span></span> <span data-ttu-id="a3e9f-105">Questo argomento illustra come usare il certificato del cloud privato per accedere e usare il cloud privato da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3e9f-105">In this topic, you learn how to use your private cloud's certificate to access - and interact with - the private cloud from Visual Studio.</span></span>

## <a name="to-access-a-private-azure-cloud-in-visual-studio"></a><span data-ttu-id="a3e9f-106">Per accedere a un cloud privato di Azure in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a3e9f-106">To access a private Azure cloud in Visual Studio</span></span>
1. <span data-ttu-id="a3e9f-107">Nel [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885) per il cloud privato scaricare il file di impostazioni di pubblicazione o contattare l'amministratore per ottenerne uno.</span><span class="sxs-lookup"><span data-stu-id="a3e9f-107">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) for the private cloud, download your publish-settings file, or contact your administrator for a publish-settings file.</span></span> <span data-ttu-id="a3e9f-108">Nella versione pubblica di Azure, il collegamento da cui scaricare questo file è [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span><span class="sxs-lookup"><span data-stu-id="a3e9f-108">On the public version of Azure, the link to download this is [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span></span> <span data-ttu-id="a3e9f-109">L'estensione del file scaricato deve essere `.publishsettings`.</span><span class="sxs-lookup"><span data-stu-id="a3e9f-109">(The downloaded file should have an extension of `.publishsettings`)</span></span>

1. <span data-ttu-id="a3e9f-110">Aprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a3e9f-110">Open Visual Studio</span></span>

1. <span data-ttu-id="a3e9f-111">In **Esplora server** fare clic con il pulsante destro del mouse sul nodo **Azure** e quindi selezionare **Gestisci e filtra sottoscrizioni** nel menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="a3e9f-111">In **Server Explorer**, right-click the **Azure** node and, from the context menu, select **Manage and Filter Subscriptions**.</span></span>
   
    ![Comando Gestisci sottoscrizioni](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. <span data-ttu-id="a3e9f-113">Nella finestra di dialogo **Gestisci sottoscrizioni Microsoft Azure** selezionare la scheda **Certificati** e quindi selezionare **Importa**.</span><span class="sxs-lookup"><span data-stu-id="a3e9f-113">In the **Manage Microsoft Azure Subscriptions** dialog, select the **Certificates** tab, and then select **Import**.</span></span>
   
    ![Importazione di certificati di Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. <span data-ttu-id="a3e9f-115">Nella finestra di dialogo **Importa sottoscrizioni Microsoft Azure** selezionare **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="a3e9f-115">In the **Import Microsoft Azure Subscriptions** dialog, select **Browse**.</span></span>

    ![Pulsante Sfoglia nella finestra di dialogo Importa sottoscrizioni Microsoft Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. <span data-ttu-id="a3e9f-117">Nella finestra di dialogo **Apri** passare alla directory in cui è stato salvato il file di impostazioni di pubblicazione, selezionare il file e quindi selezionare **Apri**.</span><span class="sxs-lookup"><span data-stu-id="a3e9f-117">In the **Open** dialog, browse to the directory where you saved the publish-settings file, select the file, and then select **Open**.</span></span>

    ![Selezionare il file di impostazioni di pubblicazione](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. <span data-ttu-id="a3e9f-119">Dopo essere tornati nella finestra di dialogo **Importa sottoscrizioni Microsoft Azure** selezionare **Importa**.</span><span class="sxs-lookup"><span data-stu-id="a3e9f-119">When returned to the **Import Microsoft Azure Subscriptions** dialog, select **Import**.</span></span>

    ![Importare il file di impostazioni di pubblicazione](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    <span data-ttu-id="a3e9f-121">I certificati vengono importati dal file di impostazioni di pubblicazione in Visual Studio, consentendo così di interagire con le risorse del cloud privato.</span><span class="sxs-lookup"><span data-stu-id="a3e9f-121">The certificates are imported from the publish-settings file into Visual Studio, and you can now interact with your private cloud resources.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="a3e9f-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a3e9f-122">Next steps</span></span>
- [<span data-ttu-id="a3e9f-123">Pubblicazione in un servizio cloud di Azure da Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a3e9f-123">Publishing to an Azure Cloud Service from Visual Studio</span></span>](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- <span data-ttu-id="a3e9f-124">[Procedura: Scaricare e importare le impostazioni di pubblicazione e le informazioni sulla sottoscrizione](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span><span class="sxs-lookup"><span data-stu-id="a3e9f-124">[How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span></span>
