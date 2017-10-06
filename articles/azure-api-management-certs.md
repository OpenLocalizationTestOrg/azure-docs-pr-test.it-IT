---
title: aaaUpload un certificato API di gestione di Azure | Documenti Microsoft
description: Informazioni su come il convertitore tooupload API di gestione del certificato per hello portale classico di Azure.
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 1b813833-39c8-46be-8666-fd0960cfbf04
ms.service: na
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: adegeo
ms.openlocfilehash: 8294d7131cfb01dba664bd4fd04b6fc22c1e93ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a><span data-ttu-id="4f5e9-103">Caricare un certificato di gestione dell'API di gestione di Azure</span><span class="sxs-lookup"><span data-stu-id="4f5e9-103">Upload an Azure Management API Management Certificate</span></span>
<span data-ttu-id="4f5e9-104">I certificati di gestione consentono tooauthenticate con modello di distribuzione classica hello fornita da Azure.</span><span class="sxs-lookup"><span data-stu-id="4f5e9-104">Management certificates allow you tooauthenticate with hello classic deployment model provided by Azure.</span></span> <span data-ttu-id="4f5e9-105">Molti programmi e strumenti (ad esempio Visual Studio o hello Azure SDK) di utilizzare questi configurazione tooautomate dei certificati e la distribuzione dei vari servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="4f5e9-105">Many programs and tools (such as Visual Studio or hello Azure SDK) use these certificates tooautomate configuration and deployment of various Azure services.</span></span> 

> [!WARNING]
> <span data-ttu-id="4f5e9-106">Fare attenzione.</span><span class="sxs-lookup"><span data-stu-id="4f5e9-106">Be careful!</span></span> <span data-ttu-id="4f5e9-107">Questi tipi di certificati consentono di qualsiasi utente che esegue l'autenticazione con le sottoscrizioni di hello toomanage sono associate.</span><span class="sxs-lookup"><span data-stu-id="4f5e9-107">These types of certificates allow anyone who authenticates with them toomanage hello subscription they are associated with.</span></span>
>
>

<span data-ttu-id="4f5e9-108">Se servono altre informazioni sui certificati di Azure, compresa la creazione di un certificato autofirmato, vedere [Panoramica sui certificati per i servizi cloud di Azure](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span><span class="sxs-lookup"><span data-stu-id="4f5e9-108">If you'd like more information about Azure certificates (including creating a self-signed certificate), see [Certificates overview for Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span></span>

<span data-ttu-id="4f5e9-109">È inoltre possibile utilizzare [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate codice client per scopi di automazione.</span><span class="sxs-lookup"><span data-stu-id="4f5e9-109">You can also use [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate client-code for automation purposes.</span></span>

## <a name="upload-a-management-certificate"></a><span data-ttu-id="4f5e9-110">Creare un certificato di gestione</span><span class="sxs-lookup"><span data-stu-id="4f5e9-110">Upload a management certificate</span></span>
<span data-ttu-id="4f5e9-111">Una volta che si disponga di un certificato di gestione creato (file con estensione cer con solo una chiave pubblica hello) è possibile caricarlo nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="4f5e9-111">Once you have a management certificate created, (.cer file with only hello public key) you can upload it into hello portal.</span></span> <span data-ttu-id="4f5e9-112">Quando è disponibile nel portale di hello certificato di hello, chiunque disponga di un certificato corrispondente (chiave privata) può connettersi tramite hello API di gestione e accesso hello risorse per la sottoscrizione associata hello.</span><span class="sxs-lookup"><span data-stu-id="4f5e9-112">When hello certificate is available in hello portal, anyone with a matching certificate (private key) can connect through hello Management API and access hello resources for hello associated subscription.</span></span>

1. <span data-ttu-id="4f5e9-113">Accedi toohello [portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4f5e9-113">Log in toohello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="4f5e9-114">Fare clic su **più servizi** elenco di servizi di Azure hello inferiore, quindi selezionare **sottoscrizioni** in hello _generale_ gruppo del servizio.</span><span class="sxs-lookup"><span data-stu-id="4f5e9-114">Click **More services** at hello bottom Azure service list, then select **Subscriptions** in hello _General_ service group.</span></span>

    ![Menu Sottoscrizioni](./media/azure-api-management-certs/subscriptions_menu.png)

3. <span data-ttu-id="4f5e9-116">Assicurarsi che tooselect hello corretto sottoscrizione che si desidera tooassociate con certificato hello.</span><span class="sxs-lookup"><span data-stu-id="4f5e9-116">Make sure tooselect hello correct subscription that you want tooassociate with hello certificate.</span></span>     
4. <span data-ttu-id="4f5e9-117">Dopo aver selezionato la sottoscrizione corretta hello, premere **i certificati di gestione** in hello _impostazioni_ gruppo.</span><span class="sxs-lookup"><span data-stu-id="4f5e9-117">After you have selected hello correct subscription, press **Management certificates** in hello _Settings_ group.</span></span>

    ![Impostazioni](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. <span data-ttu-id="4f5e9-119">Hello premere **caricare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="4f5e9-119">Press hello **Upload** button.</span></span>

    ![Caricamento nella pagina Certificati](./media/azure-api-management-certs/certificates_page.png)
6. <span data-ttu-id="4f5e9-121">Compila informazioni di finestra di dialogo hello e premere **caricare**.</span><span class="sxs-lookup"><span data-stu-id="4f5e9-121">Fill out hello dialog information and press **Upload**.</span></span>

    ![Impostazioni](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a><span data-ttu-id="4f5e9-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4f5e9-123">Next steps</span></span>
<span data-ttu-id="4f5e9-124">Dopo aver creato un certificato di gestione associato a una sottoscrizione, è possibile (dopo aver installato hello corrispondente certificato in locale) a livello di programmazione connettersi toohello [API REST del modello di distribuzione classica](https://msdn.microsoft.com/library/azure/mt420159.aspx) e automatizzare Hello varie risorse di Azure che sono anche associate alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="4f5e9-124">Now that you have a management certificate associated with a subscription, you can (after you have installed hello matching certificate locally) programmatically connect toohello [classic deployment model REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) and automate hello various Azure resources that are also associated with that subscription.</span></span>
