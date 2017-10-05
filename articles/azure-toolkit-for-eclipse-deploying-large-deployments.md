---
title: Distribuire distribuzioni di grandi dimensioni
description: Informazioni su come distribuire le distribuzioni di grandi dimensioni usando il Toolkit di Azure per Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: e12e379e2b6727653e2377b1760c3745596a1e9c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploying-large-deployments"></a><span data-ttu-id="3b95c-103">Distribuire distribuzioni di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="3b95c-103">Deploying Large Deployments</span></span>
<span data-ttu-id="3b95c-104">Se la distribuzione è troppo grande per essere contenuta nella cartella approot predefinita, è possibile usare una risorsa di archiviazione locale come la cartella radice di distribuzione per il JDK e il server dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3b95c-104">If your deployment is too large to be contained in the default approot folder, you can use a local storage resource as the deployment root folder for your JDK and application server.</span></span>

## <a name="to-use-a-local-storage-resource-as-the-deployment-root-folder-for-large-deployments"></a><span data-ttu-id="3b95c-105">Per utilizzare una risorsa di archiviazione locale come la cartella radice di distribuzione per distribuzioni di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="3b95c-105">To use a local storage resource as the deployment root folder for large deployments</span></span>
1. <span data-ttu-id="3b95c-106">Creare una nuova una risorsa di archiviazione locale</span><span class="sxs-lookup"><span data-stu-id="3b95c-106">Create a new local storage resource.</span></span> <span data-ttu-id="3b95c-107">Il nome della risorsa non è rilevante.</span><span class="sxs-lookup"><span data-stu-id="3b95c-107">The name of the resource does not matter.</span></span> <span data-ttu-id="3b95c-108">Le risorse di archiviazione sono definite a livello di ruolo.</span><span class="sxs-lookup"><span data-stu-id="3b95c-108">Storage resources are defined at the role level.</span></span> <span data-ttu-id="3b95c-109">Il modo più rapido per accedere alla finestra di dialogo di configurazione dell'archiviazione locale, da cui è possibile creare una nuova risorsa di archiviazione locale, è quello di usare la procedura seguente: fare clic con il pulsante destro del mouse sul ruolo nella visualizzazione **Project Explorer** (Esplora progetti), espandendo il nodo del progetto di Azure se non viene visualizzato il ruolo, quindi fare clic su **Azure** e su **Archiviazione locale**.</span><span class="sxs-lookup"><span data-stu-id="3b95c-109">The quickest way to access the local storage configuration dialog, from which you could create a new local storage resource, is by using the following steps: Right-click the role in the **Project Explorer** view (expand your Azure project node if you don't see the role), click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="3b95c-110">Nella finestra di dialogo **Archiviazione locale** fare clic su **Aggiungi** per creare una nuova risorsa di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="3b95c-110">Within the **Local Storage** dialog, click **Add** to create a new local storage resource.</span></span>

2. <span data-ttu-id="3b95c-111">Impostare le dimensioni desiderate ad almeno 2048 MB (qualunque valore inferiore potrebbe causare gli stessi problemi di dimensioni del file che si riscontrerebbero nella cartella approot).</span><span class="sxs-lookup"><span data-stu-id="3b95c-111">Set the desired size to at least 2048 MB (anything less may cause the same file size problems as you would encounter in the approot).</span></span>

3. <span data-ttu-id="3b95c-112">Assicurarsi di selezionare **Pulire i contenuti quando l'istanza del ruolo viene riciclata** ; ciò impedirà alla logica di avvio della distribuzione di imbattersi in conflitti con i file esistenti nella risorsa quando l'istanza del ruolo viene riciclata.</span><span class="sxs-lookup"><span data-stu-id="3b95c-112">Ensure that **Clean the contents when the role instance is recycled** is checked; this will help prevent the deployment's startup logic from running into conflicts with pre-existing files in the resource when the role instance is recycled.</span></span>

4. <span data-ttu-id="3b95c-113">Assicurarsi che il valore di **Environment variable storing the resource's directory path after deployment** (Variabile di ambiente per l'archiviazione del percorso della directory della risorsa dopo la distribuzione) sia impostato sulla stringa **DEPLOYROOT**.</span><span class="sxs-lookup"><span data-stu-id="3b95c-113">Ensure that the **Environment variable storing the resource's directory path after deployment** value is set to the string **DEPLOYROOT**.</span></span> <span data-ttu-id="3b95c-114">La finestra di dialogo della risorsa di archiviazione locale sarà simile a quella seguente.</span><span class="sxs-lookup"><span data-stu-id="3b95c-114">Your local storage resource dialog will look similar to the following.</span></span>

   ![][ic667943]

<span data-ttu-id="3b95c-115">In alternativa, se si usa **DEPLOYROOT** come *nome* della risorsa locale e non si modifica il nome della variabile di ambiente generata automaticamente (che verrà impostato su **DEPLOYROOT_PATH** in questo caso), questo nome andrà bene anche per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="3b95c-115">Alternatively, if you use **DEPLOYROOT** as the *name* of your local resource and you do not change the automatically-generated environment variable name (which will be set to **DEPLOYROOT_PATH** in that case), that would work for your application as well.</span></span>

<span data-ttu-id="3b95c-116">Altre informazioni sulla creazione di una risorsa di archiviazione locale sono reperibili in [Proprietà dell'archiviazione locale][Local storage properties].</span><span class="sxs-lookup"><span data-stu-id="3b95c-116">Additional information about creating a local storage resource can be found at [Local storage properties][Local storage properties].</span></span>

## <a name="see-also"></a><span data-ttu-id="3b95c-117">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="3b95c-117">See Also</span></span>
<span data-ttu-id="3b95c-118">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3b95c-118">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="3b95c-119">[Creare un'applicazione Hello World per Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3b95c-119">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="3b95c-120">[Installazione di Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="3b95c-120">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="3b95c-121">Per altre informazioni su come usare Azure con Java, vedere il [Centro per sviluppatori Java di Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="3b95c-121">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
