---
title: impostazioni di aaaCustom per gli ambienti del servizio App
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
ms.openlocfilehash: 3d140688c88b389e71bfdd465c418339cccab3a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a><span data-ttu-id="13624-103">Impostazioni di configurazione personalizzate per gli ambienti del servizio app</span><span class="sxs-lookup"><span data-stu-id="13624-103">Custom configuration settings for App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="13624-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="13624-104">Overview</span></span>
<span data-ttu-id="13624-105">Poiché gli ambienti del servizio App sono isolati tooa singolo cliente, esistono alcune impostazioni di configurazione che possono essere applicate esclusivamente tooApp gli ambienti del servizio.</span><span class="sxs-lookup"><span data-stu-id="13624-105">Because App Service Environments are isolated tooa single customer, there are certain configuration settings that can be applied exclusively tooApp Service Environments.</span></span> <span data-ttu-id="13624-106">In questo articolo illustrata hello diverse personalizzazioni specifiche disponibili per gli ambienti del servizio App.</span><span class="sxs-lookup"><span data-stu-id="13624-106">This article documents hello various specific customizations that are available for App Service Environments.</span></span>

<span data-ttu-id="13624-107">Se non si dispone di un ambiente del servizio App, vedere [come un ambiente del servizio App tooCreate](app-service-web-how-to-create-an-app-service-environment.md).</span><span class="sxs-lookup"><span data-stu-id="13624-107">If you do not have an App Service Environment, see [How tooCreate an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span>

<span data-ttu-id="13624-108">È possibile archiviare le personalizzazioni dell'ambiente del servizio App tramite una matrice in hello nuova **clusterSettings** attributo.</span><span class="sxs-lookup"><span data-stu-id="13624-108">You can store App Service Environment customizations by using an array in hello new **clusterSettings** attribute.</span></span> <span data-ttu-id="13624-109">Questo attributo viene trovato nel dizionario "Proprietà" hello hello *hostingEnvironments* entità di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="13624-109">This attribute is found in hello "Properties" dictionary of hello *hostingEnvironments* Azure Resource Manager entity.</span></span>

<span data-ttu-id="13624-110">Hello abbreviato Gestione risorse modello frammento seguente viene illustrato hello **clusterSettings** attributo:</span><span class="sxs-lookup"><span data-stu-id="13624-110">hello following abbreviated Resource Manager template snippet shows hello **clusterSettings** attribute:</span></span>

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

<span data-ttu-id="13624-111">Hello **clusterSettings** attributo può essere incluso in un hello tooupdate modello di gestione risorse ambiente del servizio App.</span><span class="sxs-lookup"><span data-stu-id="13624-111">hello **clusterSettings** attribute can be included in a Resource Manager template tooupdate hello App Service Environment.</span></span>

## <a name="use-azure-resource-explorer-tooupdate-an-app-service-environment"></a><span data-ttu-id="13624-112">Utilizzare Esplora risorse Azure tooupdate un ambiente del servizio App</span><span class="sxs-lookup"><span data-stu-id="13624-112">Use Azure Resource Explorer tooupdate an App Service Environment</span></span>
<span data-ttu-id="13624-113">In alternativa, è possibile aggiornare l'ambiente del servizio App hello utilizzando [Esplora inventario risorse di Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="13624-113">Alternatively, you can update hello App Service Environment by using [Azure Resource Explorer](https://resources.azure.com).</span></span>  

1. <span data-ttu-id="13624-114">In Esplora risorse passare toohello nodo per l'ambiente del servizio App hello (**sottoscrizioni** > **resourceGroups** > **provider**  >  **Microsoft** > **hostingEnvironments**).</span><span class="sxs-lookup"><span data-stu-id="13624-114">In Resource Explorer, go toohello node for hello App Service Environment (**subscriptions** > **resourceGroups** > **providers** > **Microsoft.Web** > **hostingEnvironments**).</span></span> <span data-ttu-id="13624-115">Quindi fare clic su hello specifico ambiente del servizio App che si desidera tooupdate.</span><span class="sxs-lookup"><span data-stu-id="13624-115">Then click hello specific App Service Environment that you want tooupdate.</span></span>
2. <span data-ttu-id="13624-116">Nel riquadro di destra hello, fare clic su **lettura/scrittura** in tooallow barra degli strumenti superiore hello interattivo modifica in Esplora inventario risorse.</span><span class="sxs-lookup"><span data-stu-id="13624-116">In hello right pane, click **Read/Write** in hello upper toolbar tooallow interactive editing in Resource Explorer.</span></span>  
3. <span data-ttu-id="13624-117">Fare clic su hello blu **modifica** toomake hello Gestione risorse modello modificabile.</span><span class="sxs-lookup"><span data-stu-id="13624-117">Click hello blue **Edit** button toomake hello Resource Manager template editable.</span></span>
4. <span data-ttu-id="13624-118">Scorrimento toohello parte inferiore del riquadro di destra hello.</span><span class="sxs-lookup"><span data-stu-id="13624-118">Scroll toohello bottom of hello right pane.</span></span> <span data-ttu-id="13624-119">Hello **clusterSettings** in hello parte inferiore, in cui è possibile immettere o aggiornare il relativo valore è l'attributo.</span><span class="sxs-lookup"><span data-stu-id="13624-119">hello **clusterSettings** attribute is at hello very bottom, where you can enter or update its value.</span></span>
5. <span data-ttu-id="13624-120">Matrice di hello tipo (o copia e Incolla) di valori di configurazione desiderati in hello **clusterSettings** attributo.</span><span class="sxs-lookup"><span data-stu-id="13624-120">Type (or copy and paste) hello array of configuration values you want in hello **clusterSettings** attribute.</span></span>  
6. <span data-ttu-id="13624-121">Fare clic su hello verde **inserire** pulsante che è disponibile nella parte superiore di hello di hello riquadro destro toocommit hello modifica toohello ambiente del servizio App.</span><span class="sxs-lookup"><span data-stu-id="13624-121">Click hello green **PUT** button that's located at hello top of hello right pane toocommit hello change toohello App Service Environment.</span></span>

<span data-ttu-id="13624-122">Tuttavia, si invia modifica hello, impiegato moltiplicati per il numero di hello di front-end in hello ambiente del servizio App per effetto di hello modifica tootake circa 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="13624-122">However you submit hello change, it takes roughly 30 minutes multiplied by hello number of front ends in hello App Service Environment for hello change tootake effect.</span></span>
<span data-ttu-id="13624-123">Ad esempio, se un ambiente del servizio App dispone di quattro front-end, richiederà circa due ore per hello configurazione aggiornamento toofinish.</span><span class="sxs-lookup"><span data-stu-id="13624-123">For example, if an App Service Environment has four front ends, it will take roughly two hours for hello configuration update toofinish.</span></span> <span data-ttu-id="13624-124">Durante la modifica di configurazione hello è in fase di implementazione, non esistono altre operazioni di scala o operazioni di modifica della configurazione possono avvenire in hello ambiente del servizio App.</span><span class="sxs-lookup"><span data-stu-id="13624-124">While hello configuration change is being rolled out, no other scaling operations or configuration change operations can take place in hello App Service Environment.</span></span>

## <a name="disable-tls-10"></a><span data-ttu-id="13624-125">Disabilitare TLS 1.0</span><span class="sxs-lookup"><span data-stu-id="13624-125">Disable TLS 1.0</span></span>
<span data-ttu-id="13624-126">Una domanda ricorrente dai clienti, in particolare i clienti che utilizzano la conformità PCI controlli, è come tooexplicitly disabilitare TLS 1.0 per le app.</span><span class="sxs-lookup"><span data-stu-id="13624-126">A recurring question from customers, especially customers who are dealing with PCI compliance audits, is how tooexplicitly disable TLS 1.0 for their apps.</span></span>

<span data-ttu-id="13624-127">TLS 1.0 può essere disabilitato tramite il seguente hello **clusterSettings** voce:</span><span class="sxs-lookup"><span data-stu-id="13624-127">TLS 1.0 can be disabled through hello following **clusterSettings** entry:</span></span>

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a><span data-ttu-id="13624-128">Modifica dell'ordine dei pacchetti di crittografia TLS</span><span class="sxs-lookup"><span data-stu-id="13624-128">Change TLS cipher suite order</span></span>
<span data-ttu-id="13624-129">Un'altra domanda dai clienti è se è possibile modificare l'elenco di hello crittografie negoziato da server e questo può essere ottenuto modificando hello **clusterSettings** come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="13624-129">Another question from customers is if they can modify hello list of ciphers negotiated by their server and this can be achieved by modifying hello **clusterSettings** as shown below.</span></span> <span data-ttu-id="13624-130">elenco di Hello dei pacchetti di crittografia disponibili può essere recuperato da [questo articolo MSDN](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span><span class="sxs-lookup"><span data-stu-id="13624-130">hello list of cipher suites available can be retrieved from [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span></span>

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> <span data-ttu-id="13624-131">Se i valori non corretti vengono impostati per pacchetto di crittografia hello che non è possibile comprendere SChannel, tutti i server di tooyour comunicazione TLS potrebbe smettere di funzionare.</span><span class="sxs-lookup"><span data-stu-id="13624-131">If incorrect values are set for hello cipher suite that SChannel cannot understand, all TLS communication tooyour server might stop functioning.</span></span> <span data-ttu-id="13624-132">In tal caso, sarà necessario hello tooremove *FrontEndSSLCipherSuiteOrder* voce **clusterSettings** e inviare hello aggiornato di crittografia predefinito di gestione risorse modello toorevert toohello indietro impostazioni di gruppo.</span><span class="sxs-lookup"><span data-stu-id="13624-132">In such a case, you will need tooremove hello *FrontEndSSLCipherSuiteOrder* entry from **clusterSettings** and submit hello updated Resource Manager template toorevert back toohello default cipher suite settings.</span></span>  <span data-ttu-id="13624-133">Usare questa funzionalità con cautela.</span><span class="sxs-lookup"><span data-stu-id="13624-133">Please use this functionality with caution.</span></span>
> 
> 

## <a name="get-started"></a><span data-ttu-id="13624-134">Attività iniziali</span><span class="sxs-lookup"><span data-stu-id="13624-134">Get started</span></span>
<span data-ttu-id="13624-135">sito di modello di avvio rapido di Azure Resource Manager Hello include un modello con la definizione di base hello per [la creazione di un ambiente del servizio App](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span><span class="sxs-lookup"><span data-stu-id="13624-135">hello Azure Quickstart Resource Manager template site includes a template with hello base definition for [creating an App Service Environment](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span></span>

<!-- LINKS -->

<!-- IMAGES -->
