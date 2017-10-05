---
title: Configurazione delle credenziali per l'autenticazione denominate | Documentazione Microsoft
description: "Informazioni su come fornire le credenziali che Visual Studio può usare per l'autenticazione delle richieste inviate a Azure per pubblicare un'applicazione in Azure da Visual Studio o monitorare un servizio cloud esistente. "
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/22/2017
ms.author: kraigb
ms.openlocfilehash: c486676a70e195ec85ad40540ea4b7caaa86bc48
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="setting-up-named-authentication-credentials"></a><span data-ttu-id="59448-103">Configurazione delle credenziali per l'autenticazione denominate</span><span class="sxs-lookup"><span data-stu-id="59448-103">Setting Up Named Authentication Credentials</span></span>
<span data-ttu-id="59448-104">Per pubblicare un'applicazione in Azure da Visual Studio o monitorare un servizio cloud esistente, è necessario fornire le credenziali che Visual Studio può usare per l'autenticazione delle richieste inviate a Azure.</span><span class="sxs-lookup"><span data-stu-id="59448-104">To publish an application to Azure from Visual Studio or to monitor an existing cloud service, you must provide credentials that Visual Studio can use to authenticate requests to Azure.</span></span> <span data-ttu-id="59448-105">In Visual Studio è possibile fornire queste credenziali accedendo a più posizioni.</span><span class="sxs-lookup"><span data-stu-id="59448-105">There are several places in Visual Studio where you can sign in to provide these credentials.</span></span> <span data-ttu-id="59448-106">Ad esempio, da Esplora server è possibile aprire il menu di scelta rapida per il nodo **Azure** e scegliere **Connessione alla sottoscrizione di Microsoft Azure**. Dopo l'accesso, le informazioni sulla sottoscrizione associate all'account Azure sono disponibili in Visual Studio. Non è necessario eseguire altre operazioni.</span><span class="sxs-lookup"><span data-stu-id="59448-106">For example, from the Server Explorer, you can open the shortcut menu for the **Azure** node and choose **Connect to Microsoft Azure Subscription...**. When you sign in, the subscription information associated with your Azure account is available in Visual Studio, and there is nothing more you have to do.</span></span>

<span data-ttu-id="59448-107">Gli strumenti di Azure supportano anche un modo meno recente di fornire le credenziali, attraverso il file di sottoscrizione, con estensione publishsettings.</span><span class="sxs-lookup"><span data-stu-id="59448-107">Azure Tools also supports an older way of providing credentials, using the subscription file (.publishsettings file).</span></span> <span data-ttu-id="59448-108">Questo argomento illustra tale metodo, ancora supportato in Azure SDK 2.2.</span><span class="sxs-lookup"><span data-stu-id="59448-108">This topic describes this method, which is still supported in Azure SDK 2.2.</span></span>

<span data-ttu-id="59448-109">Per l'autenticazione in Azure sono richiesti gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="59448-109">The following items are required for authentication to Azure:</span></span>

* <span data-ttu-id="59448-110">ID sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="59448-110">Your subscription ID</span></span>
* <span data-ttu-id="59448-111">Un certificato X.509 v3 valido</span><span class="sxs-lookup"><span data-stu-id="59448-111">A valid X.509 v3 certificate</span></span>

> [!NOTE]
> <span data-ttu-id="59448-112">La lunghezza della chiave del certificato X.509 v3 deve essere di almeno 2048 bit.</span><span class="sxs-lookup"><span data-stu-id="59448-112">The length of the X.509 v3 certificate's key must be at least 2048 bits.</span></span> <span data-ttu-id="59448-113">Azure rifiuterà qualsiasi certificato che non soddisfa questo requisito o che sia non valido.</span><span class="sxs-lookup"><span data-stu-id="59448-113">Azure will reject any certificate that doesn’t meet this requirement or that isn’t valid.</span></span>
>
>

<span data-ttu-id="59448-114">Visual Studio usa l'ID sottoscrizione e i dati del certificato come credenziali.</span><span class="sxs-lookup"><span data-stu-id="59448-114">Visual Studio uses your subscription ID together with the certificate data as credentials.</span></span> <span data-ttu-id="59448-115">Nel file di sottoscrizione, con estensione publishsettings, che contiene una chiave pubblica per il certificato, viene fatto riferimento alle credenziali appropriate.</span><span class="sxs-lookup"><span data-stu-id="59448-115">The appropriate credentials are referenced in the subscription file (.publishsettings file), which contains a public key for the certificate.</span></span> <span data-ttu-id="59448-116">Il file di sottoscrizione può contenere le credenziali per più di una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="59448-116">The subscription file can contain credentials for more than one subscription.</span></span>

<span data-ttu-id="59448-117">Per modificare le informazioni sulla sottoscrizione è possibile usare le finestre di dialogo **Nuova sottoscrizione e Modifica sottoscrizione** , come illustrato più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="59448-117">You can edit the subscription information from the **New/Edit Subscription** dialog box, as explained later in this topic.</span></span>

<span data-ttu-id="59448-118">Se si vuole creare un certificato, vedere le istruzioni contenute in [Creare e caricare un certificato di gestione per Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) e quindi caricare manualmente il certificato nel [portale di Azure classico](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="59448-118">If you want to create a certificate yourself, you can refer to the instructions in [Create and Upload a Management Certificate for Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) and then manually upload the certificate to the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>

> [!NOTE]
> <span data-ttu-id="59448-119">Le credenziali richieste da Visual Studio per gestire i servizi cloud non sono le stesse necessarie per autenticare una richiesta per i servizi di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="59448-119">These credentials that Visual Studio requires to manage your cloud services aren’t the same credentials that are required to authenticate a request against the Azure storage services.</span></span>
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a><span data-ttu-id="59448-120">Importare, configurare o modificare le credenziali di autenticazione in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="59448-120">Import, set up, or edit authentication credentials in Visual Studio</span></span>
<span data-ttu-id="59448-121">È possibile importare, impostare o modificare le credenziali di autenticazione nella finestra di dialogo **Nuova sottoscrizione**, visualizzata dopo l'azione seguente:</span><span class="sxs-lookup"><span data-stu-id="59448-121">You can import, set up, or modify your authentication credentials in the **New Subscription** dialog box, which appears if you perform the following action:</span></span>

* <span data-ttu-id="59448-122">In **Esplora server** aprire il menu di scelta rapida per il nodo **Azure**, scegliere **Gestisci e filtra sottoscrizioni**, scegliere la scheda **Certificati**, quindi procedere in uno dei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="59448-122">In **Server Explorer**, open the shortcut menu for the **Azure** node, choose **Manage and Filter Subscriptions...**, choose the **Certificates** tab, and do one of the following:</span></span>

    * <span data-ttu-id="59448-123">Scegliere **Importa** per aprire la finestra di dialogo Importa sottoscrizioni Microsoft Azure, in cui è possibile scaricare il file delle sottoscrizioni per la sottoscrizione attualmente caricata, sfogliare il relativo percorso di download, quindi importarlo per l'uso in autenticazione.</span><span class="sxs-lookup"><span data-stu-id="59448-123">Choose **Import** to open the Import Microsoft Azure Subscriptions dialog where you can download the  subscriptions file for the currently loaded subscription, browse to its download location, and then import it for use in authentication.</span></span>
    * <span data-ttu-id="59448-124">Scegliere **Nuovo** per aprire la finestra di dialogo Nuova sottoscrizione, in cui è possibile impostare una nuova sottoscrizione per l'uso in autenticazione.</span><span class="sxs-lookup"><span data-stu-id="59448-124">Choose **New** to open the New Subscription dialog where you can set up a new subscription for use in authentication.</span></span>
    * <span data-ttu-id="59448-125">Scegliere **Modifica** (dopo aver scelto la sottoscrizione attiva) per aprire la finestra di dialogo Modifica sottoscrizione, in cui è possibile modificare una sottoscrizione esistente per l'uso in autenticazione.</span><span class="sxs-lookup"><span data-stu-id="59448-125">Choose **Edit** (after choosing your active subscription) to open the Edit Subscription dialog where you can edit an existing subscription for use in authentication.</span></span> 

<span data-ttu-id="59448-126">La procedura riportata di seguito presuppone che la finestra di dialogo **Nuova sottoscrizione** sia visualizzata.</span><span class="sxs-lookup"><span data-stu-id="59448-126">The following procedure assumes that the **New Subscription** dialog box is open.</span></span>

### <a name="to-set-up-authentication-credentials-in-visual-studio"></a><span data-ttu-id="59448-127">Per configurare le credenziali di autenticazione in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="59448-127">To set up authentication credentials in Visual Studio</span></span>
1. <span data-ttu-id="59448-128">Scegliere un certificato dall'elenco **Selezionare un certificato esistente per l'autenticazione** .</span><span class="sxs-lookup"><span data-stu-id="59448-128">In the **Select an existing certificate** for authentication list, choose a certificate.</span></span>
2. <span data-ttu-id="59448-129">Scegliere il collegamento **Copia il percorso completo**.</span><span class="sxs-lookup"><span data-stu-id="59448-129">Choose the **Copy the full path** link.</span></span> <span data-ttu-id="59448-130">Il percorso del certificato, ovvero il file con estensione cer, viene copiato negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="59448-130">The path for the certificate (.cer file) is copied to the Clipboard.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="59448-131">Per pubblicare l'applicazione Azure da Visual Studio, è necessario caricare questo certificato nel [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="59448-131">To publish your Azure application from Visual Studio, you must upload this certificate to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   >
   >
3. <span data-ttu-id="59448-132">Per caricare il certificato nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="59448-132">To upload the certificate to the Azure portal:</span></span>

   1. <span data-ttu-id="59448-133">Aprire il [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="59448-133">Open the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   2. <span data-ttu-id="59448-134">Se richiesto, accedere al portale e quindi passare a **Impostazioni**, **Certificati di gestione**.</span><span class="sxs-lookup"><span data-stu-id="59448-134">If prompted, sign in to the portal and then navigate to **Settings**, **Management Certificates**.</span></span>
   3. <span data-ttu-id="59448-135">Nel riquadro Certificati di gestione, scegliere **Carica**.</span><span class="sxs-lookup"><span data-stu-id="59448-135">In the Management certificates pane, choose **Upload**.</span></span>
   4. <span data-ttu-id="59448-136">Selezionare la sottoscrizione di Azure, incollare il percorso completo del file con estensione .cer appena creato e scegliere **Carica**.</span><span class="sxs-lookup"><span data-stu-id="59448-136">Select your Azure subscription, paste the full path of the .cer file that you just created, and choose **Upload**.</span></span>
