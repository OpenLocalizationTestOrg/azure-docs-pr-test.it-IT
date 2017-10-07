---
title: i certificati aaaUsing con Enterprise Integration Pack | Documenti Microsoft
description: Informazioni su come toouse certificati con hello Enterprise Integration Pack | App per la logica di Azure
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
ms.openlocfilehash: 7ba9f597a03a852a9ba05d2af08fe4bc2d98aef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a><span data-ttu-id="86a67-103">Informazioni sui certificati ed Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="86a67-103">Learn about certificates and Enterprise Integration Pack</span></span>
## <a name="overview"></a><span data-ttu-id="86a67-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="86a67-104">Overview</span></span>
<span data-ttu-id="86a67-105">Integrazione di Enterprise utilizza le comunicazioni di certificati toosecure B2B.</span><span class="sxs-lookup"><span data-stu-id="86a67-105">Enterprise integration uses certificates toosecure B2B communications.</span></span> <span data-ttu-id="86a67-106">È possibile usare due tipi di certificati nelle app di Enterprise Integration:</span><span class="sxs-lookup"><span data-stu-id="86a67-106">You can use two types of certificates in your enterprise integration apps:</span></span>

* <span data-ttu-id="86a67-107">Certificati pubblici, che devono essere acquistati da un'autorità di certificazione (CA).</span><span class="sxs-lookup"><span data-stu-id="86a67-107">Public certificates, which must be purchased from a certification authority (CA).</span></span>
* <span data-ttu-id="86a67-108">Certificati privati, che si possono rilasciare personalmente.</span><span class="sxs-lookup"><span data-stu-id="86a67-108">Private certificates, which you can issue yourself.</span></span> <span data-ttu-id="86a67-109">In alcuni casi, questi certificati sono autofirmati tooas cui viene fatto riferimento.</span><span class="sxs-lookup"><span data-stu-id="86a67-109">These certificates are sometimes referred tooas self-signed certificates.</span></span>

## <a name="what-are-certificates"></a><span data-ttu-id="86a67-110">Che cosa sono i certificati?</span><span class="sxs-lookup"><span data-stu-id="86a67-110">What are certificates?</span></span>
<span data-ttu-id="86a67-111">I certificati sono documenti digitali per verificare l'identità hello di partecipanti hello comunicazioni elettroniche e che inoltre proteggere le comunicazioni elettroniche.</span><span class="sxs-lookup"><span data-stu-id="86a67-111">Certificates are digital documents that verify hello identity of hello participants in electronic communications and that also secure electronic communications.</span></span>

## <a name="why-use-certificates"></a><span data-ttu-id="86a67-112">Perché usare i certificati?</span><span class="sxs-lookup"><span data-stu-id="86a67-112">Why use certificates?</span></span>
<span data-ttu-id="86a67-113">In alcuni casi è necessario garantire la riservatezza delle comunicazioni B2B.</span><span class="sxs-lookup"><span data-stu-id="86a67-113">Sometimes B2B communications must be kept confidential.</span></span> <span data-ttu-id="86a67-114">Integrazione di Enterprise utilizza i certificati toosecure queste comunicazioni in due modi:</span><span class="sxs-lookup"><span data-stu-id="86a67-114">Enterprise integration uses certificates toosecure these communications in two ways:</span></span>

* <span data-ttu-id="86a67-115">Grazie alla crittografia contenuto hello dei messaggi</span><span class="sxs-lookup"><span data-stu-id="86a67-115">By encrypting hello contents of messages</span></span>
* <span data-ttu-id="86a67-116">Apponendo una firma digitale ai messaggi</span><span class="sxs-lookup"><span data-stu-id="86a67-116">By digitally signing messages</span></span>  

## <a name="upload-a-public-certificate"></a><span data-ttu-id="86a67-117">Caricare un certificato pubblico</span><span class="sxs-lookup"><span data-stu-id="86a67-117">Upload a public certificate</span></span>

<span data-ttu-id="86a67-118">toouse un *certificato pubblico* nelle App logica con funzionalità B2B, è innanzitutto necessario certificato hello tooupload nell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="86a67-118">toouse a *public certificate* in your logic apps with B2B capabilities, you first need tooupload hello certificate into your integration account.</span></span>  

<span data-ttu-id="86a67-119">Dopo aver caricato un certificato, è disponibile toohelp è proteggere i messaggi B2B quando si definiscono le relative proprietà in hello [contratti](logic-apps-enterprise-integration-agreements.md) creati.</span><span class="sxs-lookup"><span data-stu-id="86a67-119">After you upload a certificate, it's available toohelp you secure your B2B messages when you define their properties in hello [agreements](logic-apps-enterprise-integration-agreements.md) that you create.</span></span>  

<span data-ttu-id="86a67-120">Ecco i passaggi dettagliati per caricare i certificati pubblici nell'account di integrazione dopo l'accesso al portale di Azure toohello hello:</span><span class="sxs-lookup"><span data-stu-id="86a67-120">Here are hello detailed steps for uploading your public certificates into your integration account after you sign in toohello Azure portal:</span></span>

1. <span data-ttu-id="86a67-121">Selezionare **più servizi** e immettere **integrazione** nella casella di ricerca di hello filtro.</span><span class="sxs-lookup"><span data-stu-id="86a67-121">Select **More services** and enter **integration** in hello filter search box.</span></span> <span data-ttu-id="86a67-122">Selezionare **account di integrazione** dall'elenco dei risultati hello</span><span class="sxs-lookup"><span data-stu-id="86a67-122">Select **Integration Accounts** from hello results list</span></span>     
<span data-ttu-id="86a67-123">![Selezionare Esplora](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span><span class="sxs-lookup"><span data-stu-id="86a67-123">![Select Browse](media/logic-apps-enterprise-integration-certificates/overview-1.png)</span></span>  
2. <span data-ttu-id="86a67-124">Selezionare hello integrazione account toowhich si desidera tooadd hello certificato.</span><span class="sxs-lookup"><span data-stu-id="86a67-124">Select hello integration account toowhich you want tooadd hello certificate.</span></span>  
![Selezionare hello integrazione account toowhich si desidera tooadd hello certificato](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. <span data-ttu-id="86a67-126">Seleziona hello **certificati** riquadro.</span><span class="sxs-lookup"><span data-stu-id="86a67-126">Select hello **Certificates** tile.</span></span>  
<span data-ttu-id="86a67-127">![Riquadro hello selezionare certificati](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="86a67-127">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>
4. <span data-ttu-id="86a67-128">In hello **certificati** pannello visualizzato, seleziona hello **Aggiungi** pulsante.</span><span class="sxs-lookup"><span data-stu-id="86a67-128">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="86a67-129">![Pulsante Aggiungi hello](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="86a67-129">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
5. <span data-ttu-id="86a67-130">Immettere un **nome** per il certificato e quindi selezionare hello tipo di certificato come **pubblica** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="86a67-130">Enter a **Name** for your certificate, and then select hello certificate type as **public** from hello dropdown.</span></span>  
6. <span data-ttu-id="86a67-131">Icona della cartella selezionare hello sul lato destro hello di hello **certificato** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="86a67-131">Select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="86a67-132">Quando si apre il selettore di file hello, individuare e selezionare il file di certificato hello cui account di integrazione tooyour tooupload.</span><span class="sxs-lookup"><span data-stu-id="86a67-132">When hello file picker opens, find and select hello certificate file that you want tooupload tooyour integration account.</span></span>
7. <span data-ttu-id="86a67-133">Selezionare il certificato di hello, quindi **OK** nel selettore file hello.</span><span class="sxs-lookup"><span data-stu-id="86a67-133">Select hello certificate, and then select **OK** in hello file picker.</span></span> <span data-ttu-id="86a67-134">Questa convalida e carica hello certificato tooyour integrazione account.</span><span class="sxs-lookup"><span data-stu-id="86a67-134">This validates and uploads hello certificate tooyour integration account.</span></span>
8. <span data-ttu-id="86a67-135">Infine, eseguire il backup su hello **Aggiungi certificato** blade, seleziona hello **OK** pulsante.</span><span class="sxs-lookup"><span data-stu-id="86a67-135">Finally, back on hello **Add certificate** blade, select hello **OK** button.</span></span>  
<span data-ttu-id="86a67-136">![Selezionare pulsante OK hello](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span><span class="sxs-lookup"><span data-stu-id="86a67-136">![Select hello OK button](media/logic-apps-enterprise-integration-certificates/certificate-3.png)</span></span>  
9. <span data-ttu-id="86a67-137">Seleziona hello **certificati** riquadro.</span><span class="sxs-lookup"><span data-stu-id="86a67-137">Select hello **Certificates** tile.</span></span> <span data-ttu-id="86a67-138">Dovrebbe essere hello appena aggiunto certificato.</span><span class="sxs-lookup"><span data-stu-id="86a67-138">You should see hello newly added certificate.</span></span>  
<span data-ttu-id="86a67-139">![Vedere il nuovo certificato di hello](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span><span class="sxs-lookup"><span data-stu-id="86a67-139">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/certificate-4.png)</span></span>  

## <a name="upload-a-private-certificate"></a><span data-ttu-id="86a67-140">Caricare un certificato privato</span><span class="sxs-lookup"><span data-stu-id="86a67-140">Upload a private certificate</span></span>

<span data-ttu-id="86a67-141">toouse un *certificato privato* nelle App logica con funzionalità B2B, è possibile caricare un account di integrazione tooyour certificato privato da hello richiede alla procedura seguente</span><span class="sxs-lookup"><span data-stu-id="86a67-141">toouse a *private certificate* in your logic apps with B2B capabilities, You can upload a private certificate tooyour integration account by taking hello following steps</span></span>

1. <span data-ttu-id="86a67-142">[Caricare il tooKey chiave privata insieme di credenziali](../key-vault/key-vault-get-started.md "informazioni sull'insieme di credenziali chiave") e fornire un **nome chiave**</span><span class="sxs-lookup"><span data-stu-id="86a67-142">[Upload your private key tooKey Vault](../key-vault/key-vault-get-started.md "Learn about Key Vault") and provide a **Key Name**</span></span> 
   
   > [!TIP]
   > <span data-ttu-id="86a67-143">È necessario autorizzare le operazioni di App per la logica tooperform in insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="86a67-143">You must authorize Logic Apps tooperform operations on Key Vault.</span></span> <span data-ttu-id="86a67-144">È possibile concedere l'entità di servizio App per la logica di accesso toohello utilizzando hello comando PowerShell seguente:`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span><span class="sxs-lookup"><span data-stu-id="86a67-144">You can grant access toohello Logic Apps service principal by using hello following PowerShell command: `Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`</span></span>  
   > 
   > 

<span data-ttu-id="86a67-145">Dopo aver acquisito passaggio precedente hello, aggiungere un account di toointegration certificato privato.</span><span class="sxs-lookup"><span data-stu-id="86a67-145">After you've taken hello previous step, add a private certificate toointegration account.</span></span>

<span data-ttu-id="86a67-146">Seguenti sono hello i passaggi dettagliati per il caricamento dei certificati privati all'account di integrazione dopo l'accesso toohello portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="86a67-146">Following are hello detailed steps for uploading your private certificates into your integration account after you sign in toohello Azure portal:</span></span>  
 
1. <span data-ttu-id="86a67-147">Selezionare hello integrazione account toowhich si desidera che il certificato di hello tooadd e si seleziona hello **certificati** riquadro.</span><span class="sxs-lookup"><span data-stu-id="86a67-147">Select hello integration account toowhich you want tooadd hello certificate and select hello **Certificates** tile.</span></span>  
<span data-ttu-id="86a67-148">![Riquadro hello selezionare certificati](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="86a67-148">![Select hello Certificates tile](media/logic-apps-enterprise-integration-certificates/certificate-1.png)</span></span>  
2. <span data-ttu-id="86a67-149">In hello **certificati** pannello visualizzato, seleziona hello **Aggiungi** pulsante.</span><span class="sxs-lookup"><span data-stu-id="86a67-149">In hello **Certificates** blade that opens, select hello **Add** button.</span></span>   
<span data-ttu-id="86a67-150">![Pulsante Aggiungi hello](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="86a67-150">![Select hello Add button](media/logic-apps-enterprise-integration-certificates/certificate-2.png)</span></span>
3. <span data-ttu-id="86a67-151">Immettere un **nome** per il certificato e il tipo di certificato selezionare hello come **privata** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="86a67-151">Enter a **Name** for your certificate, and select hello certificate type as **private** from hello dropdown.</span></span>   
4. <span data-ttu-id="86a67-152">Selezionare l'icona della cartella hello sul lato destro hello di hello **certificato** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="86a67-152">select hello folder icon on hello right side of hello **Certificate** text box.</span></span> <span data-ttu-id="86a67-153">Quando si apre il selettore di file hello, trovare hello corrispondente certificato pubblico che si desidera l'account di integrazione tooyour tooupload.</span><span class="sxs-lookup"><span data-stu-id="86a67-153">When hello file picker opens, find hello corresponding public certificate that you want tooupload tooyour integration account.</span></span>   
   
   > [!Note]
   > <span data-ttu-id="86a67-154">Durante l'aggiunta di un certificato privato è importante tooadd corrispondente pubblica certificato tooshow in [accordo AS2](logic-apps-enterprise-integration-as2.md) ricevere e inviare le impostazioni per la firma e crittografia dei messaggi hello.</span><span class="sxs-lookup"><span data-stu-id="86a67-154">While adding a private certificate it is important tooadd corresponding public certificate tooshow in [AS2 agreement](logic-apps-enterprise-integration-as2.md) receive and send settings for signing and encrypting hello messages.</span></span>
   > 
   >   

5. <span data-ttu-id="86a67-155">Seleziona hello **gruppo di risorse**, **insieme di credenziali chiave**, **nome chiave** e seleziona hello **OK** pulsante.</span><span class="sxs-lookup"><span data-stu-id="86a67-155">Select hello **Resource Group**, **Key Vault**, **Key Name** and select hello **OK** button.</span></span>  
<span data-ttu-id="86a67-156">![Add certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span><span class="sxs-lookup"><span data-stu-id="86a67-156">![Add certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)</span></span>  
6. <span data-ttu-id="86a67-157">Seleziona hello **certificati** riquadro.</span><span class="sxs-lookup"><span data-stu-id="86a67-157">Select hello **Certificates** tile.</span></span> <span data-ttu-id="86a67-158">Dovrebbe essere hello appena aggiunto certificato.</span><span class="sxs-lookup"><span data-stu-id="86a67-158">You should see hello newly added certificate.</span></span>
<span data-ttu-id="86a67-159">![Vedere il nuovo certificato di hello](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span><span class="sxs-lookup"><span data-stu-id="86a67-159">![See hello new certificate](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)</span></span>  



* [<span data-ttu-id="86a67-160">Creare un contratto B2B</span><span class="sxs-lookup"><span data-stu-id="86a67-160">Create a B2B agreement</span></span>](logic-apps-enterprise-integration-agreements.md)  
* [<span data-ttu-id="86a67-161">Altre informazioni sull'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="86a67-161">Learn more about Key Vault</span></span>](../key-vault/key-vault-get-started.md "Informazioni sull'insieme di credenziali delle chiavi")  

