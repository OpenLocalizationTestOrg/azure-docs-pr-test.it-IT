---
title: aaaDisplaying contenuto Javadoc in Eclipse per hello pacchetto di librerie di Azure per Java
description: Come toodisplay hello contenuto Javadoc per hello le librerie di Azure in Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 8070023a24dc07eca8df906db5b8b662ceed6ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-hello-azure-libraries-package-for-java"></a><span data-ttu-id="633b7-103">Visualizzazione di contenuto Javadoc in Eclipse per hello pacchetto di librerie di Azure per Java</span><span class="sxs-lookup"><span data-stu-id="633b7-103">Displaying Javadoc Content in Eclipse for hello Azure Libraries Package for Java</span></span>
<span data-ttu-id="633b7-104">Hello contenuto Javadoc per Azure Libraries for Java hello può essere visualizzato all'interno dell'ambiente Eclipse associando toohello contenuto Javadoc di hello Azure Libraries for Java.</span><span class="sxs-lookup"><span data-stu-id="633b7-104">hello Javadoc content for hello Azure Libraries for Java can be viewed within your Eclipse environment by associating hello Javadoc content toohello Azure Libraries for Java.</span></span> <span data-ttu-id="633b7-105">Hello passaggi seguenti viene illustrato come toouse questa funzionalità in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="633b7-105">hello following steps show you how toouse this functionality within Eclipse.</span></span>

<span data-ttu-id="633b7-106">Questa procedura presuppone che Hello Azure Library per il percorso di compilazione Java tooyour è già stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="633b7-106">This procedure assumes you have already added hello Azure Library for Java tooyour build path.</span></span>

## <a name="toodisplay-javadoc-content-in-eclipse-for-hello-azure-libraries-for-java"></a><span data-ttu-id="633b7-107">toodisplay contenuto Javadoc in Eclipse per hello Azure Libraries for Java</span><span class="sxs-lookup"><span data-stu-id="633b7-107">toodisplay Javadoc content in Eclipse for hello Azure Libraries for Java</span></span>
* <span data-ttu-id="633b7-108">In Project Explorer di Eclipse, in hello **Referenced Libraries** sezione del progetto, hello Apri menu di scelta rapida della libreria di Azure per Java JAR hello.</span><span class="sxs-lookup"><span data-stu-id="633b7-108">Within Eclipse's Project Explorer, in hello **Referenced Libraries** section of your project, open hello context menu for hello Azure Library for Java JAR.</span></span> <span data-ttu-id="633b7-109">Ad esempio, **0.1.0.jar-microsoft-Azure-api** (numero di versione di hello potrebbe essere diverse, a seconda della versione installata).</span><span class="sxs-lookup"><span data-stu-id="633b7-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (hello version number may be different, dependent upon which version you have installed).</span></span>

* <span data-ttu-id="633b7-110">Fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="633b7-110">Click **Properties**.</span></span>

* <span data-ttu-id="633b7-111">All'interno di hello **proprietà** finestra di dialogo, nel riquadro di sinistra hello, fare clic su **Javadoc Location**.</span><span class="sxs-lookup"><span data-stu-id="633b7-111">Within hello **Properties** dialog, in hello left-hand pane, click **Javadoc Location**.</span></span> <span data-ttu-id="633b7-112">Hello **Javadoc Location** viene visualizzata una finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="633b7-112">hello **Javadoc Location** dialog is displayed.</span></span>

* <span data-ttu-id="633b7-113">È possibile specificare un **URL Javadoc** o un **Javadoc nell'archivio**.</span><span class="sxs-lookup"><span data-stu-id="633b7-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span></span>

   * <span data-ttu-id="633b7-114">Se si sceglie toospecify un **Javadoc URL**, utilizzare ad esempio hello URL **http://dl.windowsazure.com/javadoc** o **http://dl.windowsazure.com/storage/javadoc**.</span><span class="sxs-lookup"><span data-stu-id="633b7-114">If you choose toospecify a **Javadoc URL**, use hello URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span></span>

   * <span data-ttu-id="633b7-115">Se si sceglie toouse **Javadoc in archive**, è possibile specificare un file esterno o un file di area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="633b7-115">If you choose toouse **Javadoc in archive**, you can specify an external file, or a workspace file.</span></span>

   <span data-ttu-id="633b7-116">Effettuare la selezione e sfogliare/convalidare in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="633b7-116">Make your choice and browse/validate as needed.</span></span> <span data-ttu-id="633b7-117">Hello esempio associa hello Azure Libraries for Java hello corrispondente file JAR di Javadoc è stato scaricato localmente tooa cartella denominata **c:\MyAzureJARs**.</span><span class="sxs-lookup"><span data-stu-id="633b7-117">hello following example associates hello Azure Libraries for Java with hello corresponding Javadoc JAR that has been downloaded locally tooa folder named **c:\MyAzureJARs**.</span></span>

   ![][ic553487]

* <span data-ttu-id="633b7-118">*Passaggio facoltativo*: fare clic su **Convalida**.</span><span class="sxs-lookup"><span data-stu-id="633b7-118">*Optional Step*: Click **Validate**.</span></span> <span data-ttu-id="633b7-119">Potenziali problemi con i file JAR di Javadoc hello potrebbero essere visualizzati.</span><span class="sxs-lookup"><span data-stu-id="633b7-119">Potential issues with hello Javadoc JAR could be displayed here.</span></span>

* <span data-ttu-id="633b7-120">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="633b7-120">Click **OK**.</span></span>

<span data-ttu-id="633b7-121">Una volta associato libreria hello, hello contenuto Javadoc deve essere visualizzato nell'IDE di Eclipse.</span><span class="sxs-lookup"><span data-stu-id="633b7-121">Once associated with hello library, hello Javadoc content should display within your Eclipse IDE.</span></span> <span data-ttu-id="633b7-122">Ad esempio, se `blob` è definito come tipo `CloudBlockBlob` all'interno del codice, hello seguito è riportato un esempio del contenuto Javadoc che viene visualizzata quando si digita `blob.acquireLease` nel codice:</span><span class="sxs-lookup"><span data-stu-id="633b7-122">For example, if `blob` is defined of type `CloudBlockBlob` within your code, hello following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span></span>

![][ic553488]

## <a name="see-also"></a><span data-ttu-id="633b7-123">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="633b7-123">See Also</span></span>
<span data-ttu-id="633b7-124">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="633b7-124">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="633b7-125">[Creare un'applicazione Hello World per Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="633b7-125">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="633b7-126">[L'installazione di hello Azure Toolkit per Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="633b7-126">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="633b7-127">Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="633b7-127">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
