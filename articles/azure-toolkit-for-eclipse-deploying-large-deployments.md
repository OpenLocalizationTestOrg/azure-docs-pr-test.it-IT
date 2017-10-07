---
title: aaaDeploying distribuzioni di grandi dimensioni
description: Informazioni su come le distribuzioni di grandi dimensioni toodeploy utilizzando hello Azure Toolkit per Eclipse.
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
ms.openlocfilehash: 6b1d2a7a5e49c78154fc856a221e64ca8dcfbe9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-large-deployments"></a><span data-ttu-id="559bc-103">Distribuire distribuzioni di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="559bc-103">Deploying Large Deployments</span></span>
<span data-ttu-id="559bc-104">Se la distribuzione è troppo grande toobe contenuta nella cartella approot predefinita di hello, è possibile utilizzare una risorsa di archiviazione locale come cartella radice di distribuzione hello per il JDK e server applicazioni.</span><span class="sxs-lookup"><span data-stu-id="559bc-104">If your deployment is too large toobe contained in hello default approot folder, you can use a local storage resource as hello deployment root folder for your JDK and application server.</span></span>

## <a name="toouse-a-local-storage-resource-as-hello-deployment-root-folder-for-large-deployments"></a><span data-ttu-id="559bc-105">toouse una risorsa di archiviazione locale come cartella radice di distribuzione hello per le distribuzioni di grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="559bc-105">toouse a local storage resource as hello deployment root folder for large deployments</span></span>
1. <span data-ttu-id="559bc-106">Creare una nuova una risorsa di archiviazione locale</span><span class="sxs-lookup"><span data-stu-id="559bc-106">Create a new local storage resource.</span></span> <span data-ttu-id="559bc-107">nome Hello della risorsa di hello non è rilevante.</span><span class="sxs-lookup"><span data-stu-id="559bc-107">hello name of hello resource does not matter.</span></span> <span data-ttu-id="559bc-108">Risorse di archiviazione sono definite a livello di ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="559bc-108">Storage resources are defined at hello role level.</span></span> <span data-ttu-id="559bc-109">Hello più rapido modo tooaccess hello archiviazione locale finestra di dialogo configurazione, da cui è possibile creare una nuova risorsa di archiviazione locale, è tramite hello alla procedura seguente: ruolo di hello pulsante destro del mouse in hello **Esplora progetti** vista (espandere il Azure nodo del progetto se non viene visualizzato il ruolo di hello), fare clic su **Azure**, quindi fare clic su **archiviazione locale**.</span><span class="sxs-lookup"><span data-stu-id="559bc-109">hello quickest way tooaccess hello local storage configuration dialog, from which you could create a new local storage resource, is by using hello following steps: Right-click hello role in hello **Project Explorer** view (expand your Azure project node if you don't see hello role), click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="559bc-110">All'interno di hello **archiviazione locale** finestra di dialogo, fare clic su **Aggiungi** toocreate una nuova risorsa di archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="559bc-110">Within hello **Local Storage** dialog, click **Add** toocreate a new local storage resource.</span></span>

2. <span data-ttu-id="559bc-111">Hello set desiderato di dimensioni tooat almeno 2048 MB (un valore minore potrebbe causare hello stessi problemi di dimensioni di file si riscontrerebbero in hello approot).</span><span class="sxs-lookup"><span data-stu-id="559bc-111">Set hello desired size tooat least 2048 MB (anything less may cause hello same file size problems as you would encounter in hello approot).</span></span>

3. <span data-ttu-id="559bc-112">Verificare che **pulire contenuto hello quando l'istanza del ruolo hello viene riciclato** è selezionato; Ciò consentirà di impedire l'esecuzione in è in conflitto con i file preesistenti nella risorsa hello logica di avvio della distribuzione di hello quando hello ruolo istanza viene riciclata.</span><span class="sxs-lookup"><span data-stu-id="559bc-112">Ensure that **Clean hello contents when hello role instance is recycled** is checked; this will help prevent hello deployment's startup logic from running into conflicts with pre-existing files in hello resource when hello role instance is recycled.</span></span>

4. <span data-ttu-id="559bc-113">Verificare che hello **l'archiviazione variabile di ambiente hello percorso della directory della risorsa dopo la distribuzione** valore viene impostato stringa toohello **DEPLOYROOT**.</span><span class="sxs-lookup"><span data-stu-id="559bc-113">Ensure that hello **Environment variable storing hello resource's directory path after deployment** value is set toohello string **DEPLOYROOT**.</span></span> <span data-ttu-id="559bc-114">La finestra di dialogo di risorse di archiviazione locale avrà un aspetto simile toohello seguente.</span><span class="sxs-lookup"><span data-stu-id="559bc-114">Your local storage resource dialog will look similar toohello following.</span></span>

   ![][ic667943]

<span data-ttu-id="559bc-115">In alternativa, se si utilizza **DEPLOYROOT** come hello *nome* di risorsa locale e non modificare il nome variabile di ambiente generato automaticamente hello (che verrà impostato troppo **DEPLOYROOT_PATH** in questo caso), che viene utilizzata per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="559bc-115">Alternatively, if you use **DEPLOYROOT** as hello *name* of your local resource and you do not change hello automatically-generated environment variable name (which will be set too**DEPLOYROOT_PATH** in that case), that would work for your application as well.</span></span>

<span data-ttu-id="559bc-116">Altre informazioni sulla creazione di una risorsa di archiviazione locale sono reperibili in [Proprietà dell'archiviazione locale][Local storage properties].</span><span class="sxs-lookup"><span data-stu-id="559bc-116">Additional information about creating a local storage resource can be found at [Local storage properties][Local storage properties].</span></span>

## <a name="see-also"></a><span data-ttu-id="559bc-117">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="559bc-117">See Also</span></span>
<span data-ttu-id="559bc-118">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="559bc-118">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="559bc-119">[Creare un'applicazione Hello World per Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="559bc-119">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="559bc-120">[L'installazione di hello Azure Toolkit per Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="559bc-120">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="559bc-121">Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="559bc-121">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
