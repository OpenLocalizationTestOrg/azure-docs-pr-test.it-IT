---
title: Backup denominato le credenziali di autenticazione aaaSetting | Documenti Microsoft
description: "Informazioni su come servizio cloud tootooprovide credenziali che Visual Studio è possibile utilizzare tooauthenticate richieste tooAzure toopublish tooAzure un'applicazione da Visual Studio o toomonitor esistente... "
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
ms.openlocfilehash: 3cc147a2f7a3e766293ca282f56078cf24281346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-named-authentication-credentials"></a><span data-ttu-id="c933c-103">Configurazione delle credenziali per l'autenticazione denominate</span><span class="sxs-lookup"><span data-stu-id="c933c-103">Setting Up Named Authentication Credentials</span></span>
<span data-ttu-id="c933c-104">toopublish tooAzure un'applicazione da Visual Studio o toomonitor un servizio cloud esistente, è necessario fornire credenziali che Visual Studio è possibile utilizzare tooauthenticate richiede tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c933c-104">toopublish an application tooAzure from Visual Studio or toomonitor an existing cloud service, you must provide credentials that Visual Studio can use tooauthenticate requests tooAzure.</span></span> <span data-ttu-id="c933c-105">Esistono diverse posizioni in cui è possibile accedere in tooprovide queste credenziali di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c933c-105">There are several places in Visual Studio where you can sign in tooprovide these credentials.</span></span> <span data-ttu-id="c933c-106">Da Esplora Server hello, ad esempio, è possibile aprire il menu di scelta rapida hello per hello **Azure** nodo e scegliere **connettersi tooMicrosoft sottoscrizione Azure...** . Quando si accede, informazioni sulla sottoscrizione hello associati all'account di Azure è disponibile in Visual Studio e non vi sono altre che è toodo.</span><span class="sxs-lookup"><span data-stu-id="c933c-106">For example, from hello Server Explorer, you can open hello shortcut menu for hello **Azure** node and choose **Connect tooMicrosoft Azure Subscription...**. When you sign in, hello subscription information associated with your Azure account is available in Visual Studio, and there is nothing more you have toodo.</span></span>

<span data-ttu-id="c933c-107">Gli strumenti di Azure supporta inoltre un modo meno recente di fornire le credenziali, l'utilizzo di file di sottoscrizione hello (file publishsettings).</span><span class="sxs-lookup"><span data-stu-id="c933c-107">Azure Tools also supports an older way of providing credentials, using hello subscription file (.publishsettings file).</span></span> <span data-ttu-id="c933c-108">Questo argomento illustra tale metodo, ancora supportato in Azure SDK 2.2.</span><span class="sxs-lookup"><span data-stu-id="c933c-108">This topic describes this method, which is still supported in Azure SDK 2.2.</span></span>

<span data-ttu-id="c933c-109">Hello seguenti elementi è necessario per l'autenticazione tooAzure:</span><span class="sxs-lookup"><span data-stu-id="c933c-109">hello following items are required for authentication tooAzure:</span></span>

* <span data-ttu-id="c933c-110">ID sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="c933c-110">Your subscription ID</span></span>
* <span data-ttu-id="c933c-111">Un certificato X.509 v3 valido</span><span class="sxs-lookup"><span data-stu-id="c933c-111">A valid X.509 v3 certificate</span></span>

> [!NOTE]
> <span data-ttu-id="c933c-112">lunghezza di Hello della chiave del certificato x. 509 v3 hello deve essere di almeno 2048 bit.</span><span class="sxs-lookup"><span data-stu-id="c933c-112">hello length of hello X.509 v3 certificate's key must be at least 2048 bits.</span></span> <span data-ttu-id="c933c-113">Azure rifiuterà qualsiasi certificato che non soddisfa questo requisito o che sia non valido.</span><span class="sxs-lookup"><span data-stu-id="c933c-113">Azure will reject any certificate that doesn’t meet this requirement or that isn’t valid.</span></span>
>
>

<span data-ttu-id="c933c-114">Visual Studio Usa l'ID sottoscrizione e i dati del certificato hello come credenziali.</span><span class="sxs-lookup"><span data-stu-id="c933c-114">Visual Studio uses your subscription ID together with hello certificate data as credentials.</span></span> <span data-ttu-id="c933c-115">le credenziali appropriate Hello vengono fatto riferimento nel file di sottoscrizione hello (file publishsettings), che contiene una chiave pubblica per il certificato di hello.</span><span class="sxs-lookup"><span data-stu-id="c933c-115">hello appropriate credentials are referenced in hello subscription file (.publishsettings file), which contains a public key for hello certificate.</span></span> <span data-ttu-id="c933c-116">file di sottoscrizione Hello può contenere le credenziali per più di una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="c933c-116">hello subscription file can contain credentials for more than one subscription.</span></span>

<span data-ttu-id="c933c-117">È possibile modificare le informazioni sulla sottoscrizione hello da hello **nuova/modifica sottoscrizione** la finestra di dialogo, come descritto più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="c933c-117">You can edit hello subscription information from hello **New/Edit Subscription** dialog box, as explained later in this topic.</span></span>

<span data-ttu-id="c933c-118">Se si desidera toocreate un certificato manualmente, è possibile fare riferimento a istruzioni toohello [creare e caricare un certificato di gestione per Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) e caricare manualmente hello certificato toohello [portale di Azure classico ](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="c933c-118">If you want toocreate a certificate yourself, you can refer toohello instructions in [Create and Upload a Management Certificate for Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) and then manually upload hello certificate toohello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>

> [!NOTE]
> <span data-ttu-id="c933c-119">Queste credenziali che Visual Studio richiede toomanage che non sono i servizi cloud hello stesse credenziali che sono necessari tooauthenticate una richiesta nei servizi di archiviazione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c933c-119">These credentials that Visual Studio requires toomanage your cloud services aren’t hello same credentials that are required tooauthenticate a request against hello Azure storage services.</span></span>
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a><span data-ttu-id="c933c-120">Importare, configurare o modificare le credenziali di autenticazione in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c933c-120">Import, set up, or edit authentication credentials in Visual Studio</span></span>
<span data-ttu-id="c933c-121">Importare, impostare o modificare le credenziali di autenticazione in hello **nuova sottoscrizione** nella finestra di dialogo viene visualizzata se si esegue hello azione seguente:</span><span class="sxs-lookup"><span data-stu-id="c933c-121">You can import, set up, or modify your authentication credentials in hello **New Subscription** dialog box, which appears if you perform hello following action:</span></span>

* <span data-ttu-id="c933c-122">In **Esplora Server**, aprire il menu di scelta rapida hello per hello **Azure** nodo, scegliere **Gestisci e filtra sottoscrizioni...** , scegliere hello **certificati** scheda ed eseguire uno dei seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="c933c-122">In **Server Explorer**, open hello shortcut menu for hello **Azure** node, choose **Manage and Filter Subscriptions...**, choose hello **Certificates** tab, and do one of hello following:</span></span>

    * <span data-ttu-id="c933c-123">Scegliere **importare** tooopen hello Importa sottoscrizioni di Microsoft Azure finestra di dialogo in cui è possibile scaricare il file sottoscrizioni hello per hello attualmente caricato sottoscrizione, Sfoglia tooits percorso di download e quindi importarlo per l'utilizzo in autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c933c-123">Choose **Import** tooopen hello Import Microsoft Azure Subscriptions dialog where you can download hello  subscriptions file for hello currently loaded subscription, browse tooits download location, and then import it for use in authentication.</span></span>
    * <span data-ttu-id="c933c-124">Scegliere **New** tooopen hello nuova sottoscrizione finestra di dialogo in cui è possibile impostare una nuova sottoscrizione per l'utilizzo dell'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c933c-124">Choose **New** tooopen hello New Subscription dialog where you can set up a new subscription for use in authentication.</span></span>
    * <span data-ttu-id="c933c-125">Scegliere **modifica** (dopo aver scelto la sottoscrizione) tooopen hello Modifica sottoscrizione finestra di dialogo in cui è possibile modificare una sottoscrizione esistente per l'utilizzo dell'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="c933c-125">Choose **Edit** (after choosing your active subscription) tooopen hello Edit Subscription dialog where you can edit an existing subscription for use in authentication.</span></span> 

<span data-ttu-id="c933c-126">Hello nella procedura si presuppone che hello **nuova sottoscrizione** la finestra di dialogo è aperta.</span><span class="sxs-lookup"><span data-stu-id="c933c-126">hello following procedure assumes that hello **New Subscription** dialog box is open.</span></span>

### <a name="tooset-up-authentication-credentials-in-visual-studio"></a><span data-ttu-id="c933c-127">tooset delle credenziali di autenticazione in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c933c-127">tooset up authentication credentials in Visual Studio</span></span>
1. <span data-ttu-id="c933c-128">In hello **selezionare un certificato esistente** per elenco autenticazione, scegliere un certificato.</span><span class="sxs-lookup"><span data-stu-id="c933c-128">In hello **Select an existing certificate** for authentication list, choose a certificate.</span></span>
2. <span data-ttu-id="c933c-129">Scegliere hello **Copia percorso completo di hello** collegamento.</span><span class="sxs-lookup"><span data-stu-id="c933c-129">Choose hello **Copy hello full path** link.</span></span> <span data-ttu-id="c933c-130">percorso di Hello per il certificato di hello (file con estensione cer) è toohello copiato negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="c933c-130">hello path for hello certificate (.cer file) is copied toohello Clipboard.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c933c-131">toopublish l'applicazione Azure da Visual Studio, è necessario caricare questo certificato toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="c933c-131">toopublish your Azure application from Visual Studio, you must upload this certificate toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   >
   >
3. <span data-ttu-id="c933c-132">certificato hello tooupload toohello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="c933c-132">tooupload hello certificate toohello Azure portal:</span></span>

   1. <span data-ttu-id="c933c-133">Aprire hello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="c933c-133">Open hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   2. <span data-ttu-id="c933c-134">Se richiesto, accedere al portale toohello e quindi passare troppo**impostazioni**, **i certificati di gestione**.</span><span class="sxs-lookup"><span data-stu-id="c933c-134">If prompted, sign in toohello portal and then navigate too**Settings**, **Management Certificates**.</span></span>
   3. <span data-ttu-id="c933c-135">Nel riquadro di hello gestione certificati, scegliere **caricare**.</span><span class="sxs-lookup"><span data-stu-id="c933c-135">In hello Management certificates pane, choose **Upload**.</span></span>
   4. <span data-ttu-id="c933c-136">Selezionare la sottoscrizione di Azure, incollare percorso completo di hello del file con estensione cer hello appena creato e scegliere **caricare**.</span><span class="sxs-lookup"><span data-stu-id="c933c-136">Select your Azure subscription, paste hello full path of hello .cer file that you just created, and choose **Upload**.</span></span>
