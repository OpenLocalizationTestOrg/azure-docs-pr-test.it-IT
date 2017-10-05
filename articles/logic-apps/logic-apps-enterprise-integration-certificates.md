---
title: <span data-ttu-id="c1aa7-101">Uso dei certificati con Enterprise Integration Pack | Documentazione Microsoft</span><span class="sxs-lookup"><span data-stu-id="c1aa7-101">Using certificates with Enterprise Integration Pack | Microsoft Docs</span></span>
description: <span data-ttu-id="c1aa7-102">Informazioni su come usare i certificati con Enterprise Integration Pack| App per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="c1aa7-102">Learn how to use certificates with the Enterprise Integration Pack | Azure Logic Apps</span></span>
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 0570aab14283b38f9efcc50636f0c0c1c8e3ed13
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a><span data-ttu-id="c1aa7-103">Informazioni sui certificati ed Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="c1aa7-103">Learn about certificates and Enterprise Integration Pack</span></span>
## <a name="overview"></a><span data-ttu-id="c1aa7-104">Overview</span><span class="sxs-lookup"><span data-stu-id="c1aa7-104">Overview</span></span>
<span data-ttu-id="c1aa7-105">Enterprise Integration impiega i certificati per proteggere le comunicazioni B2B.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-105">Enterprise integration uses certificates to secure B2B communications.</span></span> <span data-ttu-id="c1aa7-106">È possibile usare due tipi di certificati nelle app di Enterprise Integration:</span><span class="sxs-lookup"><span data-stu-id="c1aa7-106">You can use two types of certificates in your enterprise integration apps:</span></span>

* <span data-ttu-id="c1aa7-107">Certificati pubblici, che devono essere acquistati da un'autorità di certificazione (CA).</span><span class="sxs-lookup"><span data-stu-id="c1aa7-107">Public certificates, which must be purchased from a certification authority (CA).</span></span>
* <span data-ttu-id="c1aa7-108">Certificati privati, che si possono rilasciare personalmente.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-108">Private certificates, which you can issue yourself.</span></span> <span data-ttu-id="c1aa7-109">Sono talvolta definiti certificati autofirmati.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-109">These certificates are sometimes referred to as self-signed certificates.</span></span>

## <a name="what-are-certificates"></a><span data-ttu-id="c1aa7-110">Che cosa sono i certificati?</span><span class="sxs-lookup"><span data-stu-id="c1aa7-110">What are certificates?</span></span>
<span data-ttu-id="c1aa7-111">I certificati sono documenti digitali che verificano l'identità dei partecipanti nelle comunicazioni elettroniche e proteggono le comunicazioni elettroniche stesse.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-111">Certificates are digital documents that verify the identity of the participants in electronic communications and that also secure electronic communications.</span></span>

## <a name="why-use-certificates"></a><span data-ttu-id="c1aa7-112">Perché usare i certificati?</span><span class="sxs-lookup"><span data-stu-id="c1aa7-112">Why use certificates?</span></span>
<span data-ttu-id="c1aa7-113">In alcuni casi è necessario garantire la riservatezza delle comunicazioni B2B.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-113">Sometimes B2B communications must be kept confidential.</span></span> <span data-ttu-id="c1aa7-114">Enterprise Integration usa i certificati per proteggere queste comunicazioni in due modi:</span><span class="sxs-lookup"><span data-stu-id="c1aa7-114">Enterprise integration uses certificates to secure these communications in two ways:</span></span>

* <span data-ttu-id="c1aa7-115">Crittografando il contenuto dei messaggi</span><span class="sxs-lookup"><span data-stu-id="c1aa7-115">By encrypting the contents of messages</span></span>
* <span data-ttu-id="c1aa7-116">Apponendo una firma digitale ai messaggi</span><span class="sxs-lookup"><span data-stu-id="c1aa7-116">By digitally signing messages</span></span>  

## <a name="upload-a-public-certificate"></a><span data-ttu-id="c1aa7-117">Caricare un certificato pubblico</span><span class="sxs-lookup"><span data-stu-id="c1aa7-117">Upload a public certificate</span></span>

<span data-ttu-id="c1aa7-118">Per usare un *certificato pubblico* nelle app per la logica con funzionalità B2B, è necessario prima caricare il certificato nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-118">To use a *public certificate* in your logic apps with B2B capabilities, you first need to upload the certificate into your integration account.</span></span>  

<span data-ttu-id="c1aa7-119">Dopo che è stato caricato, un certificato diventa disponibile per proteggere i messaggi B2B quando se ne definiscono le proprietà nei [contratti](logic-apps-enterprise-integration-agreements.md) creati.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-119">After you upload a certificate, it's available to help you secure your B2B messages when you define their properties in the [agreements](logic-apps-enterprise-integration-agreements.md) that you create.</span></span>  

<span data-ttu-id="c1aa7-120">Ecco i passaggi dettagliati per caricare i certificati pubblici nell'account di integrazione dopo l'accesso al portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="c1aa7-120">Here are the detailed steps for uploading your public certificates into your integration account after you sign in to the Azure portal:</span></span>

1. <span data-ttu-id="c1aa7-121">Selezionare **Altri servizi** e immettere **integrazione** nella casella di ricerca Filtro.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-121">Select **More services** and enter **integration** in the filter search box.</span></span> <span data-ttu-id="c1aa7-122">Selezionare **Account di integrazione** nell'elenco dei risultati.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-122">Select **Integration Accounts** from the results list</span></span>     
<span data-ttu-id="c1aa7-123">![Selezionare Esplora](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span><span class="sxs-lookup"><span data-stu-id="c1aa7-123">![Select Browse](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span></span>  
2. <span data-ttu-id="c1aa7-124">Selezionare l'account di integrazione a cui aggiungere il certificato.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-124">Select the integration account to which you want to add the certificate.</span></span>  
![Selezionare l'account di integrazione a cui aggiungere il certificato](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. <span data-ttu-id="c1aa7-126">Selezionare il riquadro **Certificati** .</span><span class="sxs-lookup"><span data-stu-id="c1aa7-126">Select the **Certificates** tile.</span></span>  
<span data-ttu-id="c1aa7-127">![Selezionare il riquadro Certificati](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="c1aa7-127">![Select the Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>
4. <span data-ttu-id="c1aa7-128">Selezionare il pulsante **Aggiungi** nel pannello **Certificati** che si apre.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-128">In the **Certificates** blade that opens, select the **Add** button.</span></span>   
<span data-ttu-id="c1aa7-129">![Selezionare il pulsante Aggiungi](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="c1aa7-129">![Select the Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
5. <span data-ttu-id="c1aa7-130">Immettere un **nome** per il certificato e quindi selezionare il tipo di certificato **pubblico** nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-130">Enter a **Name** for your certificate, and then select the certificate type as **public** from the dropdown.</span></span>  
6. <span data-ttu-id="c1aa7-131">Selezionare l'icona della cartella sul lato destro della casella di testo **Certificato**.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-131">Select the folder icon on the right side of the **Certificate** text box.</span></span> <span data-ttu-id="c1aa7-132">Quando viene visualizzato il selettore file, individuare e selezionare il file del certificato da caricare nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-132">When the file picker opens, find and select the certificate file that you want to upload to your integration account.</span></span>
7. <span data-ttu-id="c1aa7-133">Selezionare il certificato e poi **OK** nel selettore file.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-133">Select the certificate, and then select **OK** in the file picker.</span></span> <span data-ttu-id="c1aa7-134">Questa operazione convalida e carica il certificato nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-134">This validates and uploads the certificate to your integration account.</span></span>
8. <span data-ttu-id="c1aa7-135">Infine, di nuovo nel pannello **Aggiungi certificato**, selezionare il pulsante **OK**.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-135">Finally, back on the **Add certificate** blade, select the **OK** button.</span></span>  
<span data-ttu-id="c1aa7-136">![Selezionare il pulsante OK](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span><span class="sxs-lookup"><span data-stu-id="c1aa7-136">![Select the OK button](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span></span>  
9. <span data-ttu-id="c1aa7-137">Selezionare il riquadro **Certificati** .</span><span class="sxs-lookup"><span data-stu-id="c1aa7-137">Select the **Certificates** tile.</span></span> <span data-ttu-id="c1aa7-138">Viene visualizzato il certificato appena aggiunto.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-138">You should see the newly added certificate.</span></span>  
<span data-ttu-id="c1aa7-139">![Vedere il nuovo certificato](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span><span class="sxs-lookup"><span data-stu-id="c1aa7-139">![See the new certificate](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span></span>  

## <a name="upload-a-private-certificate"></a><span data-ttu-id="c1aa7-140">Caricare un certificato privato</span><span class="sxs-lookup"><span data-stu-id="c1aa7-140">Upload a private certificate</span></span>

<span data-ttu-id="c1aa7-141">Per usare un *certificato privato* nelle app per la logica con funzionalità B2B, è possibile caricare un certificato privato nell'account di integrazione attenendosi alla procedura seguente</span><span class="sxs-lookup"><span data-stu-id="c1aa7-141">To use a *private certificate* in your logic apps with B2B capabilities, You can upload a private certificate to your integration account by taking the following steps</span></span>

1. <span data-ttu-id="c1aa7-142">[Caricare la chiave privata in Key Vault](../key-vault/key-vault-get-started.md "Informazioni su Key Vault") e specificare un **nome chiave**.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-142">[Upload your private key to Key Vault](../key-vault/key-vault-get-started.md "Learn about Key Vault") and provide a **Key Name**</span></span> 
   
   > [!TIP]
   > <span data-ttu-id="c1aa7-143">È necessario autorizzare App per la logica a eseguire operazioni su Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-143">You must authorize Logic Apps to perform operations on Key Vault.</span></span> <span data-ttu-id="c1aa7-144">È possibile concedere l'accesso all'entità servizio App per la logica usando questo comando di PowerShell: `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span><span class="sxs-lookup"><span data-stu-id="c1aa7-144">You can grant access to the Logic Apps service principal by using the following PowerShell command: `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span></span>  
   > 
   > 

<span data-ttu-id="c1aa7-145">Dopo avere eseguito il passaggio precedente, aggiungere un certificato privato all'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-145">After you've taken the previous step, add a private certificate to integration account.</span></span>

<span data-ttu-id="c1aa7-146">Ecco i passaggi dettagliati per caricare i certificati privati nell'account di integrazione dopo l'accesso al portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="c1aa7-146">Following are the detailed steps for uploading your private certificates into your integration account after you sign in to the Azure portal:</span></span>  
 
1. <span data-ttu-id="c1aa7-147">Selezionare l'account di integrazione a cui aggiungere il certificato e selezionare il riquadro **Certificati**.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-147">Select the integration account to which you want to add the certificate and select the **Certificates** tile.</span></span>  
<span data-ttu-id="c1aa7-148">![Selezionare il riquadro Certificati](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="c1aa7-148">![Select the Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>  
2. <span data-ttu-id="c1aa7-149">Selezionare il pulsante **Aggiungi** nel pannello **Certificati** che si apre.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-149">In the **Certificates** blade that opens, select the **Add** button.</span></span>   
<span data-ttu-id="c1aa7-150">![Selezionare il pulsante Aggiungi](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="c1aa7-150">![Select the Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
3. <span data-ttu-id="c1aa7-151">Immettere un **nome** per il certificato e selezionare il tipo di certificato **privato** nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-151">Enter a **Name** for your certificate, and select the certificate type as **private** from the dropdown.</span></span>   
4. <span data-ttu-id="c1aa7-152">Selezionare l'icona della cartella sul lato destro della casella di testo **Certificato**.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-152">select the folder icon on the right side of the **Certificate** text box.</span></span> <span data-ttu-id="c1aa7-153">Quando viene visualizzato il selettore file,trovare il certificato pubblico corrispondente da caricare nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-153">When the file picker opens, find the corresponding public certificate that you want to upload to your integration account.</span></span>   
   
   > [!Note]
   > <span data-ttu-id="c1aa7-154">Quando si aggiunge un certificato privato, è importante aggiungere il certificato pubblico corrispondente da visualizzare nelle impostazioni di ricezione e invio dell'[accordo AS2](logic-apps-enterprise-integration-as2.md) per la firma e la crittografia dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-154">While adding a private certificate it is important to add corresponding public certificate to show in [AS2 agreement](logic-apps-enterprise-integration-as2.md) receive and send settings for signing and encrypting the messages.</span></span>
   > 
   >   

5. <span data-ttu-id="c1aa7-155">Selezionare il **gruppo di risorse**, l'**insieme di credenziali delle chiavi** e il **nome chiave** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-155">Select the **Resource Group**, **Key Vault**, **Key Name** and select the **OK** button.</span></span>  
<span data-ttu-id="c1aa7-156">![Add certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="c1aa7-156">![Add certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span></span>  
6. <span data-ttu-id="c1aa7-157">Selezionare il riquadro **Certificati** .</span><span class="sxs-lookup"><span data-stu-id="c1aa7-157">Select the **Certificates** tile.</span></span> <span data-ttu-id="c1aa7-158">Viene visualizzato il certificato appena aggiunto.</span><span class="sxs-lookup"><span data-stu-id="c1aa7-158">You should see the newly added certificate.</span></span>
<span data-ttu-id="c1aa7-159">![Vedere il nuovo certificato](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="c1aa7-159">![See the new certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span></span>  



* [<span data-ttu-id="c1aa7-160">Creare un contratto B2B</span><span class="sxs-lookup"><span data-stu-id="c1aa7-160">Create a B2B agreement</span></span>](logic-apps-enterprise-integration-agreements.md)  
* [<span data-ttu-id="c1aa7-161">Altre informazioni sull'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="c1aa7-161">Learn more about Key Vault</span></span>](../key-vault/key-vault-get-started.md "Informazioni sull'insieme di credenziali delle chiavi")  

