---
title: Caricare un certificato dell'API Gestione di Azure | Documentazione Microsoft
description: Informazioni su come caricare il certificato di gestione API per il portale di Azure classico.
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
ms.openlocfilehash: 9dc438e927acd9aef38f06807fabf3dda9b021c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a><span data-ttu-id="d2738-103">Caricare un certificato di gestione dell'API di gestione di Azure</span><span class="sxs-lookup"><span data-stu-id="d2738-103">Upload an Azure Management API Management Certificate</span></span>
<span data-ttu-id="d2738-104">I certificati di gestione consentono di eseguire l'autenticazione con il modello di distribuzione classico fornito da Azure.</span><span class="sxs-lookup"><span data-stu-id="d2738-104">Management certificates allow you to authenticate with the classic deployment model provided by Azure.</span></span> <span data-ttu-id="d2738-105">Molti programmi e strumenti (ad esempio Visual Studio o Azure SDK) usano questi certificati per automatizzare la configurazione e la distribuzione di vari servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="d2738-105">Many programs and tools (such as Visual Studio or the Azure SDK) use these certificates to automate configuration and deployment of various Azure services.</span></span> 

> [!WARNING]
> <span data-ttu-id="d2738-106">Fare attenzione.</span><span class="sxs-lookup"><span data-stu-id="d2738-106">Be careful!</span></span> <span data-ttu-id="d2738-107">Questi tipi di certificati consentono a chiunque esegua l'autenticazione di gestire la sottoscrizione a cui sono associati.</span><span class="sxs-lookup"><span data-stu-id="d2738-107">These types of certificates allow anyone who authenticates with them to manage the subscription they are associated with.</span></span>
>
>

<span data-ttu-id="d2738-108">Se servono altre informazioni sui certificati di Azure, compresa la creazione di un certificato autofirmato, vedere [Panoramica sui certificati per i servizi cloud di Azure](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span><span class="sxs-lookup"><span data-stu-id="d2738-108">If you'd like more information about Azure certificates (including creating a self-signed certificate), see [Certificates overview for Azure Cloud Services](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).</span></span>

<span data-ttu-id="d2738-109">È anche possibile usare [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) per autenticare il codice client per scopi di automazione.</span><span class="sxs-lookup"><span data-stu-id="d2738-109">You can also use [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) to authenticate client-code for automation purposes.</span></span>

## <a name="upload-a-management-certificate"></a><span data-ttu-id="d2738-110">Creare un certificato di gestione</span><span class="sxs-lookup"><span data-stu-id="d2738-110">Upload a management certificate</span></span>
<span data-ttu-id="d2738-111">Dopo aver creato un certificato di gestione (file con estensione cer solo con la chiave pubblica), è possibile caricarlo nel portale.</span><span class="sxs-lookup"><span data-stu-id="d2738-111">Once you have a management certificate created, (.cer file with only the public key) you can upload it into the portal.</span></span> <span data-ttu-id="d2738-112">Quando il certificato è disponibile nel portale, chiunque disponga di un certificato corrispondente (chiave privata) può connettersi tramite l'API di gestione e accedere alle risorse per la sottoscrizione associata.</span><span class="sxs-lookup"><span data-stu-id="d2738-112">When the certificate is available in the portal, anyone with a matching certificate (private key) can connect through the Management API and access the resources for the associated subscription.</span></span>

1. <span data-ttu-id="d2738-113">Accedere al [Portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d2738-113">Log in to the [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="d2738-114">Fare clic su **Altri servizi** in fondo all'elenco dei servizi di Azure e quindi selezionare **Sottoscrizioni** nel gruppo di servizi _Generale_.</span><span class="sxs-lookup"><span data-stu-id="d2738-114">Click **More services** at the bottom Azure service list, then select **Subscriptions** in the _General_ service group.</span></span>

    ![Menu Sottoscrizioni](./media/azure-api-management-certs/subscriptions_menu.png)

3. <span data-ttu-id="d2738-116">Assicurarsi di selezionare la sottoscrizione corretta a cui si vuole associare il certificato.</span><span class="sxs-lookup"><span data-stu-id="d2738-116">Make sure to select the correct subscription that you want to associate with the certificate.</span></span>     
4. <span data-ttu-id="d2738-117">Dopo aver selezionato la sottoscrizione corretta, selezionare **Certificati di gestione** nel gruppo _Impostazioni_.</span><span class="sxs-lookup"><span data-stu-id="d2738-117">After you have selected the correct subscription, press **Management certificates** in the _Settings_ group.</span></span>

    ![Impostazioni](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. <span data-ttu-id="d2738-119">Fare clic sul pulsante **Upload** (Carica).</span><span class="sxs-lookup"><span data-stu-id="d2738-119">Press the **Upload** button.</span></span>

    ![Caricamento nella pagina Certificati](./media/azure-api-management-certs/certificates_page.png)
6. <span data-ttu-id="d2738-121">Compilare le informazioni della finestra di dialogo e fare clic su **Carica**.</span><span class="sxs-lookup"><span data-stu-id="d2738-121">Fill out the dialog information and press **Upload**.</span></span>

    ![Impostazioni](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a><span data-ttu-id="d2738-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d2738-123">Next steps</span></span>
<span data-ttu-id="d2738-124">Ora che è disponibile un certificato di gestione associato a una sottoscrizione, è possibile (dopo avere installato il certificato corrispondente in locale) connettersi a livello di codice all'[API REST del modello di distribuzione classico](https://msdn.microsoft.com/library/azure/mt420159.aspx) e automatizzare le varie risorse di Azure che possono essere associate a tale sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d2738-124">Now that you have a management certificate associated with a subscription, you can (after you have installed the matching certificate locally) programmatically connect to the [classic deployment model REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) and automate the various Azure resources that are also associated with that subscription.</span></span>
