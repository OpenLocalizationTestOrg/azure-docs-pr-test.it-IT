---
title: Impostazioni personalizzate per gli ambienti del servizio app
description: Impostazioni di configurazione personalizzate per gli ambienti del servizio app
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 1d1d85f3-6cc6-4d57-ae1a-5b37c642d812
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: stefsch
ms.openlocfilehash: 687475fae0c90713c15e8abbb92b71059eae81c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a><span data-ttu-id="a18c2-103">Impostazioni di configurazione personalizzate per gli ambienti del servizio app</span><span class="sxs-lookup"><span data-stu-id="a18c2-103">Custom configuration settings for App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="a18c2-104">Overview</span><span class="sxs-lookup"><span data-stu-id="a18c2-104">Overview</span></span>
<span data-ttu-id="a18c2-105">Gli ambienti del servizio app sono specifici di un singolo cliente. Per questo motivo alcune impostazioni di configurazione possono essere applicate esclusivamente ad ambienti del servizio app.</span><span class="sxs-lookup"><span data-stu-id="a18c2-105">Because App Service Environments are isolated to a single customer, there are certain configuration settings that can be applied exclusively to App Service Environments.</span></span> <span data-ttu-id="a18c2-106">Questo articolo descrive le diverse personalizzazioni disponibili per gli ambienti del servizio app.</span><span class="sxs-lookup"><span data-stu-id="a18c2-106">This article documents the various specific customizations that are available for App Service Environments.</span></span>

<span data-ttu-id="a18c2-107">Se non è disponibile un ambiente del servizio app, vedere [Come creare un ambiente del servizio app](app-service-web-how-to-create-an-app-service-environment.md).</span><span class="sxs-lookup"><span data-stu-id="a18c2-107">If you do not have an App Service Environment, see [How to Create an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span>

<span data-ttu-id="a18c2-108">È possibile archiviare le personalizzazioni dell'ambiente del servizio app tramite una matrice nel nuovo attributo **clusterSettings** .</span><span class="sxs-lookup"><span data-stu-id="a18c2-108">You can store App Service Environment customizations by using an array in the new **clusterSettings** attribute.</span></span> <span data-ttu-id="a18c2-109">Questo attributo si trova nel dizionario "Properties" dell'entità di Azure Resource Manager *hostingEnvironments* .</span><span class="sxs-lookup"><span data-stu-id="a18c2-109">This attribute is found in the "Properties" dictionary of the *hostingEnvironments* Azure Resource Manager entity.</span></span>

<span data-ttu-id="a18c2-110">Il frammento di modello di Resource Manager abbreviato seguente illustra l'attributo **clusterSettings** :</span><span class="sxs-lookup"><span data-stu-id="a18c2-110">The following abbreviated Resource Manager template snippet shows the **clusterSettings** attribute:</span></span>

    "resources": [
    {
       "apiVersion": "2015-08-01",
       "type": "Microsoft.Web/hostingEnvironments",
       "name": ...,
       "location": ...,
       "properties": {
          "clusterSettings": [
             {
                 "name": "nameOfCustomSetting",
                 "value": "valueOfCustomSetting"
             }
          ],
          "workerPools": [ ...],
          etc...
       }
    }

<span data-ttu-id="a18c2-111">L'attributo **clusterSettings** può essere incluso in un modello di Resource Manager per aggiornare l'ambiente del servizio app.</span><span class="sxs-lookup"><span data-stu-id="a18c2-111">The **clusterSettings** attribute can be included in a Resource Manager template to update the App Service Environment.</span></span>

## <a name="use-azure-resource-explorer-to-update-an-app-service-environment"></a><span data-ttu-id="a18c2-112">Usare Esplora risorse di Azure per aggiornare un ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="a18c2-112">Use Azure Resource Explorer to update an App Service Environment</span></span>
<span data-ttu-id="a18c2-113">In alternativa, è possibile aggiornare l'ambiente del servizio app tramite [Esplora risorse di Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a18c2-113">Alternatively, you can update the App Service Environment by using [Azure Resource Explorer](https://resources.azure.com).</span></span>  

1. <span data-ttu-id="a18c2-114">In Esplora risorse passare al nodo dell'ambiente del servizio app (**subscriptions** > **resourceGroups** > **providers** > **Microsoft.Web** > **hostingEnvironments**).</span><span class="sxs-lookup"><span data-stu-id="a18c2-114">In Resource Explorer, go to the node for the App Service Environment (**subscriptions** > **resourceGroups** > **providers** > **Microsoft.Web** > **hostingEnvironments**).</span></span> <span data-ttu-id="a18c2-115">quindi fare clic sull'ambiente del servizio app specifico che si vuole aggiornare.</span><span class="sxs-lookup"><span data-stu-id="a18c2-115">Then click the specific App Service Environment that you want to update.</span></span>
2. <span data-ttu-id="a18c2-116">Nel riquadro a destra fare clic su **Lettura/Scrittura** nella barra degli strumenti superiore per consentire la modifica interattiva in Esplora risorse.</span><span class="sxs-lookup"><span data-stu-id="a18c2-116">In the right pane, click **Read/Write** in the upper toolbar to allow interactive editing in Resource Explorer.</span></span>  
3. <span data-ttu-id="a18c2-117">Fare clic sul pulsante **Modifica** blu per rendere modificabile il modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a18c2-117">Click the blue **Edit** button to make the Resource Manager template editable.</span></span>
4. <span data-ttu-id="a18c2-118">Scorrere fino alla fine del riquadro destro.</span><span class="sxs-lookup"><span data-stu-id="a18c2-118">Scroll to the bottom of the right pane.</span></span> <span data-ttu-id="a18c2-119">L'attributo **clusterSettings** si trova nella parte inferiore. Qui è possibile immettere o aggiornare il valore corrispondente.</span><span class="sxs-lookup"><span data-stu-id="a18c2-119">The **clusterSettings** attribute is at the very bottom, where you can enter or update its value.</span></span>
5. <span data-ttu-id="a18c2-120">Digitare o copiare e incollare la matrice dei valori di configurazione voluti all'interno dell'attributo **clusterSettings** .</span><span class="sxs-lookup"><span data-stu-id="a18c2-120">Type (or copy and paste) the array of configuration values you want in the **clusterSettings** attribute.</span></span>  
6. <span data-ttu-id="a18c2-121">Fare clic sul pulsante verde **PUT** situato nella parte superiore del riquadro destro per eseguire il commit della modifica nell'ambiente del servizio app.</span><span class="sxs-lookup"><span data-stu-id="a18c2-121">Click the green **PUT** button that's located at the top of the right pane to commit the change to the App Service Environment.</span></span>

<span data-ttu-id="a18c2-122">Indipendentemente dalla modalità di invio della modifica, perché le modifiche siano effettive occorrono circa 30 minuti per ognuno dei front-end nell'ambiente del servizio.</span><span class="sxs-lookup"><span data-stu-id="a18c2-122">However you submit the change, it takes roughly 30 minutes multiplied by the number of front ends in the App Service Environment for the change to take effect.</span></span>
<span data-ttu-id="a18c2-123">Ad esempio, se un ambiente del servizio app dispone di quattro front-end, per l'aggiornamento della configurazione occorreranno circa due ore.</span><span class="sxs-lookup"><span data-stu-id="a18c2-123">For example, if an App Service Environment has four front ends, it will take roughly two hours for the configuration update to finish.</span></span> <span data-ttu-id="a18c2-124">Durante l'implementazione della modifica della configurazione non è possibile eseguire altre operazioni di ridimensionamento o di modifica della configurazione nell'ambiente del servizio app.</span><span class="sxs-lookup"><span data-stu-id="a18c2-124">While the configuration change is being rolled out, no other scaling operations or configuration change operations can take place in the App Service Environment.</span></span>

## <a name="disable-tls-10"></a><span data-ttu-id="a18c2-125">Disabilitare TLS 1.0</span><span class="sxs-lookup"><span data-stu-id="a18c2-125">Disable TLS 1.0</span></span>
<span data-ttu-id="a18c2-126">Una domanda ricorrente dei clienti, in particolare da parte di coloro che usano controlli di conformità PCI, riguarda come disabilitare esplicitamente lo standard TLS 1.0 per le proprie app.</span><span class="sxs-lookup"><span data-stu-id="a18c2-126">A recurring question from customers, especially customers who are dealing with PCI compliance audits, is how to explicitly disable TLS 1.0 for their apps.</span></span>

<span data-ttu-id="a18c2-127">È possibile disabilitare TLS 1.0 tramite la voce **clusterSettings** seguente:</span><span class="sxs-lookup"><span data-stu-id="a18c2-127">TLS 1.0 can be disabled through the following **clusterSettings** entry:</span></span>

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a><span data-ttu-id="a18c2-128">Modifica dell'ordine dei pacchetti di crittografia TLS</span><span class="sxs-lookup"><span data-stu-id="a18c2-128">Change TLS cipher suite order</span></span>
<span data-ttu-id="a18c2-129">Un'altra domanda dei clienti riguarda la possibilità di modificare l'elenco delle crittografie negoziate dal server. Questo risultato può essere ottenuto modificando **clusterSettings** come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="a18c2-129">Another question from customers is if they can modify the list of ciphers negotiated by their server and this can be achieved by modifying the **clusterSettings** as shown below.</span></span> <span data-ttu-id="a18c2-130">L'elenco dei pacchetti di crittografia può essere recuperato da [questo articolo MSDN](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span><span class="sxs-lookup"><span data-stu-id="a18c2-130">The list of cipher suites available can be retrieved from [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span></span>

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> <span data-ttu-id="a18c2-131">Se per il pacchetto di crittografia vengono impostati valori non corretti che non possono essere riconosciuti da SChannel, tutta la comunicazione TLS con il server potrebbe non funzionare.</span><span class="sxs-lookup"><span data-stu-id="a18c2-131">If incorrect values are set for the cipher suite that SChannel cannot understand, all TLS communication to your server might stop functioning.</span></span> <span data-ttu-id="a18c2-132">In tal caso, sarà necessario rimuovere la voce *FrontEndSSLCipherSuiteOrder* da **clusterSettings** e inviare il modello di Resource Manager aggiornato per ripristinare le impostazioni predefinite del pacchetto di crittografia.</span><span class="sxs-lookup"><span data-stu-id="a18c2-132">In such a case, you will need to remove the *FrontEndSSLCipherSuiteOrder* entry from **clusterSettings** and submit the updated Resource Manager template to revert back to the default cipher suite settings.</span></span>  <span data-ttu-id="a18c2-133">Usare questa funzionalità con cautela.</span><span class="sxs-lookup"><span data-stu-id="a18c2-133">Please use this functionality with caution.</span></span>
> 
> 

## <a name="get-started"></a><span data-ttu-id="a18c2-134">Introduzione</span><span class="sxs-lookup"><span data-stu-id="a18c2-134">Get started</span></span>
<span data-ttu-id="a18c2-135">Il sito dei modelli di avvio rapido di Azure Resource Manager include un modello con la definizione di base per la [creazione di un ambiente del servizio app](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span><span class="sxs-lookup"><span data-stu-id="a18c2-135">The Azure Quickstart Resource Manager template site includes a template with the base definition for [creating an App Service Environment](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span></span>

<!-- LINKS -->

<!-- IMAGES -->
