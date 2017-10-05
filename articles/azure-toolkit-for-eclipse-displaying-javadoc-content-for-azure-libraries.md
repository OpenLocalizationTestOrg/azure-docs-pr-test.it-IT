---
title: Visualizzare il contenuto Javadoc in Eclipse per il pacchetto di librerie di Azure per Java
description: Come visualizzare il contenuto Javadoc per le librerie di Azure in Eclipse.
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
ms.openlocfilehash: b44deb773b2159cba1d5d957455409f10fc49334
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-the-azure-libraries-package-for-java"></a><span data-ttu-id="a83a8-103">Visualizzare il contenuto Javadoc in Eclipse per il pacchetto di librerie di Azure per Java</span><span class="sxs-lookup"><span data-stu-id="a83a8-103">Displaying Javadoc Content in Eclipse for the Azure Libraries Package for Java</span></span>
<span data-ttu-id="a83a8-104">Il contenuto Javadoc per le librerie di Azure per Java può essere visualizzato nell'ambiente Eclipse associando il contenuto Javadoc per le librerie di Azure per Java.</span><span class="sxs-lookup"><span data-stu-id="a83a8-104">The Javadoc content for the Azure Libraries for Java can be viewed within your Eclipse environment by associating the Javadoc content to the Azure Libraries for Java.</span></span> <span data-ttu-id="a83a8-105">La procedura seguente mostra come usare questa funzionalità in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a83a8-105">The following steps show you how to use this functionality within Eclipse.</span></span>

<span data-ttu-id="a83a8-106">Questa procedura presuppone che la libreria di Azure per Java sia già stata aggiunta al percorso di compilazione.</span><span class="sxs-lookup"><span data-stu-id="a83a8-106">This procedure assumes you have already added the Azure Library for Java to your build path.</span></span>

## <a name="to-display-javadoc-content-in-eclipse-for-the-azure-libraries-for-java"></a><span data-ttu-id="a83a8-107">Visualizzare il contenuto Javadoc in Eclipse per le librerie di Azure per Java</span><span class="sxs-lookup"><span data-stu-id="a83a8-107">To display Javadoc content in Eclipse for the Azure Libraries for Java</span></span>
* <span data-ttu-id="a83a8-108">In Project Explorer di Eclipse, nella sezione del progetto **Librerie a cui si fa riferimento** , aprire il menu di scelta rapida per la libreria di Azure per Java JAR.</span><span class="sxs-lookup"><span data-stu-id="a83a8-108">Within Eclipse's Project Explorer, in the **Referenced Libraries** section of your project, open the context menu for the Azure Library for Java JAR.</span></span> <span data-ttu-id="a83a8-109">Ad esempio, **microsoft-windowsazure-api-0.1.0.jar** (il numero della versione può essere diverso, a seconda della versione installata).</span><span class="sxs-lookup"><span data-stu-id="a83a8-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (the version number may be different, dependent upon which version you have installed).</span></span>

* <span data-ttu-id="a83a8-110">Fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="a83a8-110">Click **Properties**.</span></span>

* <span data-ttu-id="a83a8-111">Nella finestra di dialogo **Properties** (Proprietà) nel riquadro sinistro, fare clic su **Javadoc Location** (Posizione Javadoc).</span><span class="sxs-lookup"><span data-stu-id="a83a8-111">Within the **Properties** dialog, in the left-hand pane, click **Javadoc Location**.</span></span> <span data-ttu-id="a83a8-112">Viene visualizzata la finestra di dialogo **Posizione Javadoc** .</span><span class="sxs-lookup"><span data-stu-id="a83a8-112">The **Javadoc Location** dialog is displayed.</span></span>

* <span data-ttu-id="a83a8-113">È possibile specificare un **URL Javadoc** o un **Javadoc nell'archivio**.</span><span class="sxs-lookup"><span data-stu-id="a83a8-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span></span>

   * <span data-ttu-id="a83a8-114">Se si sceglie di specificare un **URL Javadoc**, usare URL simili a **http://dl.windowsazure.com/javadoc** o **http://dl.windowsazure.com/storage/javadoc**.</span><span class="sxs-lookup"><span data-stu-id="a83a8-114">If you choose to specify a **Javadoc URL**, use the URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span></span>

   * <span data-ttu-id="a83a8-115">Se si sceglie di utilizzare **Javadoc nell'archivio**, è possibile specificare un file esterno o un file dell’area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="a83a8-115">If you choose to use **Javadoc in archive**, you can specify an external file, or a workspace file.</span></span>

   <span data-ttu-id="a83a8-116">Effettuare la selezione e sfogliare/convalidare in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="a83a8-116">Make your choice and browse/validate as needed.</span></span> <span data-ttu-id="a83a8-117">L'esempio seguente associa le librerie di Azure per Java con il corrispondente file JAR di Javadoc scaricato localmente in una cartella denominata **c:\MyAzureJARs**.</span><span class="sxs-lookup"><span data-stu-id="a83a8-117">The following example associates the Azure Libraries for Java with the corresponding Javadoc JAR that has been downloaded locally to a folder named **c:\MyAzureJARs**.</span></span>

   ![][ic553487]

* <span data-ttu-id="a83a8-118">*Passaggio facoltativo*: fare clic su **Convalida**.</span><span class="sxs-lookup"><span data-stu-id="a83a8-118">*Optional Step*: Click **Validate**.</span></span> <span data-ttu-id="a83a8-119">Potrebbero essere visualizzati dei potenziali problemi con il file JAR di Javadoc.</span><span class="sxs-lookup"><span data-stu-id="a83a8-119">Potential issues with the Javadoc JAR could be displayed here.</span></span>

* <span data-ttu-id="a83a8-120">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a83a8-120">Click **OK**.</span></span>

<span data-ttu-id="a83a8-121">Una volta associato alla libreria, il contenuto Javadoc deve essere visualizzato nell'IDE di Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a83a8-121">Once associated with the library, the Javadoc content should display within your Eclipse IDE.</span></span> <span data-ttu-id="a83a8-122">Ad esempio, se `blob` è definito come tipo `CloudBlockBlob` nel codice, quello che segue è un esempio del contenuto Javadoc che viene visualizzato quando si digita `blob.acquireLease` nel codice:</span><span class="sxs-lookup"><span data-stu-id="a83a8-122">For example, if `blob` is defined of type `CloudBlockBlob` within your code, the following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span></span>

![][ic553488]

## <a name="see-also"></a><span data-ttu-id="a83a8-123">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="a83a8-123">See Also</span></span>
<span data-ttu-id="a83a8-124">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a83a8-124">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="a83a8-125">[Creare un'applicazione Hello World per Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a83a8-125">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="a83a8-126">[Installazione di Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a83a8-126">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="a83a8-127">Per altre informazioni su come usare Azure con Java, vedere il [Centro per sviluppatori Java di Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="a83a8-127">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
