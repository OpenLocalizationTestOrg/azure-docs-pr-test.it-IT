---
title: aaaHow toogenerate e trasferire chiavi HSM protette per insieme credenziali chiavi Azure | Documenti Microsoft
description: Utilizzare questo toohelp articolo pianificare, generare e trasferire la propria toouse chiavi HSM protette insieme di credenziali chiave di Azure. Anche noto come BYOK o Bring Your Own Key.
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 51abafa1-812b-460f-a129-d714fdc391da
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: ambapat
ms.openlocfilehash: 3bb234bd1c4b81770542ccf7110e256385ca3309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a><span data-ttu-id="7d959-104">Come toogenerate e trasferire chiavi HSM protette per l'insieme di credenziali chiave di Azure</span><span class="sxs-lookup"><span data-stu-id="7d959-104">How toogenerate and transfer HSM-protected keys for Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="7d959-105">Introduzione</span><span class="sxs-lookup"><span data-stu-id="7d959-105">Introduction</span></span>
<span data-ttu-id="7d959-106">Per maggiore sicurezza, quando si usa l'insieme di credenziali chiave di Azure, è possibile importare o generare chiavi in moduli di protezione hardware (HSM) che non lasciano mai il limite HSM hello.</span><span class="sxs-lookup"><span data-stu-id="7d959-106">For added assurance, when you use Azure Key Vault, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="7d959-107">Questo scenario è spesso tooas cui *trasferire la propria chiave*, o BYOK.</span><span class="sxs-lookup"><span data-stu-id="7d959-107">This scenario is often referred tooas *bring your own key*, or BYOK.</span></span> <span data-ttu-id="7d959-108">Hello i moduli HSM sono FIPS 140-2 livello 2 convalidato.</span><span class="sxs-lookup"><span data-stu-id="7d959-108">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="7d959-109">Insieme di credenziali chiave di Azure Usa famiglia nShield di Thales di tooprotect moduli di protezione hardware le chiavi.</span><span class="sxs-lookup"><span data-stu-id="7d959-109">Azure Key Vault uses Thales nShield family of HSMs tooprotect your keys.</span></span>

<span data-ttu-id="7d959-110">Utilizzare informazioni hello toohelp in questo argomento si pianificano, generare e trasferire la propria toouse chiavi HSM protette insieme di credenziali chiave di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d959-110">Use hello information in this topic toohelp you plan for, generate, and then transfer your own HSM-protected keys toouse with Azure Key Vault.</span></span>

<span data-ttu-id="7d959-111">Questa funzionalità non è disponibile per la versione di Azure per la Cina.</span><span class="sxs-lookup"><span data-stu-id="7d959-111">This functionality is not available for Azure China.</span></span>

> [!NOTE]
> <span data-ttu-id="7d959-112">Per altre informazioni sull'insieme di credenziali di Azure, vedere [Cos'è l'insieme di credenziali delle chiavi di Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="7d959-112">For more information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>  
>
> <span data-ttu-id="7d959-113">Per un'esercitazione introduttiva che illustra la creazione di un insieme di credenziali delle chiavi per chiavi HSM protette, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7d959-113">For a getting started tutorial, which includes creating a key vault for HSM-protected keys, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>
>
>

<span data-ttu-id="7d959-114">Ulteriori informazioni sulla generazione e trasferimento di una chiave HSM protetta tramite Internet hello:</span><span class="sxs-lookup"><span data-stu-id="7d959-114">More information about generating and transferring an HSM-protected key over hello Internet:</span></span>

* <span data-ttu-id="7d959-115">Chiave di hello è generata in una workstation offline per ridurre la superficie di attacco hello.</span><span class="sxs-lookup"><span data-stu-id="7d959-115">You generate hello key from an offline workstation, which reduces hello attack surface.</span></span>
* <span data-ttu-id="7d959-116">chiave di Hello viene crittografata con una chiave chiave (scambio), che rimane crittografata finché viene trasferito toohello moduli di protezione hardware dell'insieme di credenziali chiave di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d959-116">hello key is encrypted with a Key Exchange Key (KEK), which stays encrypted until it is transferred toohello Azure Key Vault HSMs.</span></span> <span data-ttu-id="7d959-117">Solo hello versione crittografata della chiave lascia workstation originale hello.</span><span class="sxs-lookup"><span data-stu-id="7d959-117">Only hello encrypted version of your key leaves hello original workstation.</span></span>
* <span data-ttu-id="7d959-118">Hello set di strumenti imposta proprietà sulla chiave del tenant che associa la chiave toohello ambiente di sicurezza insieme credenziali chiavi Azure.</span><span class="sxs-lookup"><span data-stu-id="7d959-118">hello toolset sets properties on your tenant key that binds your key toohello Azure Key Vault security world.</span></span> <span data-ttu-id="7d959-119">Pertanto dopo moduli di protezione hardware dell'insieme di credenziali chiave hello Azure ricevuto e decrittografato la chiave, solo questi componenti a poterla usare.</span><span class="sxs-lookup"><span data-stu-id="7d959-119">So after hello Azure Key Vault HSMs receive and decrypt your key, only these HSMs can use it.</span></span> <span data-ttu-id="7d959-120">La chiave non può essere esportata.</span><span class="sxs-lookup"><span data-stu-id="7d959-120">Your key cannot be exported.</span></span> <span data-ttu-id="7d959-121">Questa associazione viene applicata dai moduli di protezione hardware Thales hello.</span><span class="sxs-lookup"><span data-stu-id="7d959-121">This binding is enforced by hello Thales HSMs.</span></span>
* <span data-ttu-id="7d959-122">Hello chiave chiave (scambio) che viene utilizzato tooencrypt la chiave viene generata nei moduli di protezione hardware dell'insieme di credenziali chiave hello Azure e non è esportabile.</span><span class="sxs-lookup"><span data-stu-id="7d959-122">hello Key Exchange Key (KEK) that is used tooencrypt your key is generated inside hello Azure Key Vault HSMs and is not exportable.</span></span> <span data-ttu-id="7d959-123">i moduli HSM Hello imporre che non può essere una versione crittografata di hello KEK all'esterno di hello moduli di protezione hardware.</span><span class="sxs-lookup"><span data-stu-id="7d959-123">hello HSMs enforce that there can be no clear version of hello KEK outside hello HSMs.</span></span> <span data-ttu-id="7d959-124">Set di strumenti hello include inoltre un'attestazione di Thales che hello KEK non è esportabile e che è stata generata in un modulo di protezione hardware originale prodotto da Thales.</span><span class="sxs-lookup"><span data-stu-id="7d959-124">In addition, hello toolset includes attestation from Thales that hello KEK is not exportable and was generated inside a genuine HSM that was manufactured by Thales.</span></span>
* <span data-ttu-id="7d959-125">set di strumenti Hello include un'attestazione di Thales che hello insieme credenziali chiavi Azure anche l'ambiente di sicurezza è stato generato in un modulo di protezione hardware originale prodotto da Thales.</span><span class="sxs-lookup"><span data-stu-id="7d959-125">hello toolset includes attestation from Thales that hello Azure Key Vault security world was also generated on a genuine HSM manufactured by Thales.</span></span> <span data-ttu-id="7d959-126">Questa attestazione dimostri tooyou che Microsoft Usa hardware originale.</span><span class="sxs-lookup"><span data-stu-id="7d959-126">This attestation proves tooyou that Microsoft is using genuine hardware.</span></span>
* <span data-ttu-id="7d959-127">Microsoft usa certificati KEK separati e ambienti di sicurezza separati in ogni area geografica.</span><span class="sxs-lookup"><span data-stu-id="7d959-127">Microsoft uses separate KEKs and separate Security Worlds in each geographical region.</span></span> <span data-ttu-id="7d959-128">Questa separazione assicura la chiave può essere utilizzata solo nei data center nell'area di hello in cui è stata generata.</span><span class="sxs-lookup"><span data-stu-id="7d959-128">This separation ensures that your key can be used only in data centers in hello region in which you encrypted it.</span></span> <span data-ttu-id="7d959-129">Una chiave di un cliente europeo, ad esempio, non può essere usata in data center che si trovano in America del Nord o in Asia.</span><span class="sxs-lookup"><span data-stu-id="7d959-129">For example, a key from a European customer cannot be used in data centers in North American or Asia.</span></span>

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a><span data-ttu-id="7d959-130">Altre informazioni sui moduli di protezione hardware di Thales e sui servizi di Microsoft</span><span class="sxs-lookup"><span data-stu-id="7d959-130">More information about Thales HSMs and Microsoft services</span></span>
<span data-ttu-id="7d959-131">Thales e-Security è un leader a livello di crittografia dei dati e servizi finanziari toohello soluzioni sicurezza informatica, tecnologico, produzione, enti pubblici e settori di tecnologia.</span><span class="sxs-lookup"><span data-stu-id="7d959-131">Thales e-Security is a leading global provider of data encryption and cyber security solutions toohello financial services, high technology, manufacturing, government, and technology sectors.</span></span> <span data-ttu-id="7d959-132">Con un 40 anni di protezione aziendali e informazioni per enti pubblici, le soluzioni Thales vengono usate da quattro hello cinque principali energetico e aerospaziale società.</span><span class="sxs-lookup"><span data-stu-id="7d959-132">With a 40-year track record of protecting corporate and government information, Thales solutions are used by four of hello five largest energy and aerospace companies.</span></span> <span data-ttu-id="7d959-133">in 22 paesi NATO, e consentono di proteggere più dell'80 percento delle transazioni di pagamento in tutto il mondo.</span><span class="sxs-lookup"><span data-stu-id="7d959-133">Their solutions are also used by 22 NATO countries, and secure more than 80 per cent of worldwide payment transactions.</span></span>

<span data-ttu-id="7d959-134">Microsoft ha collaborato con lo stato di Thales tooenhance hello livello tecnologico dei moduli di protezione hardware.</span><span class="sxs-lookup"><span data-stu-id="7d959-134">Microsoft has collaborated with Thales tooenhance hello state of art for HSMs.</span></span> <span data-ttu-id="7d959-135">Questi miglioramenti consentono tooget hello tra i vantaggi dei servizi ospitati senza perdere il controllo sulle proprie chiavi.</span><span class="sxs-lookup"><span data-stu-id="7d959-135">These enhancements enable you tooget hello typical benefits of hosted services without relinquishing control over your keys.</span></span> <span data-ttu-id="7d959-136">In particolare, questi miglioramenti consentono a Microsoft gestire hello moduli di protezione hardware in modo che non è necessario.</span><span class="sxs-lookup"><span data-stu-id="7d959-136">Specifically, these enhancements let Microsoft manage hello HSMs so that you do not have to.</span></span> <span data-ttu-id="7d959-137">Come cloud di Azure, servizio insieme di credenziali chiave garantisce la scalabilità verticale a breve preavviso toomeet picchi di utilizzo dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="7d959-137">As a cloud service, Azure Key Vault scales up at short notice toomeet your organization’s usage spikes.</span></span> <span data-ttu-id="7d959-138">AT hello stesso tempo, la chiave è protetta all'interno di Microsoft: si mantiene il controllo sul ciclo di vita chiave hello perché genera chiave hello e trasferirlo hardware del tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="7d959-138">At hello same time, your key is protected inside Microsoft’s HSMs: You retain control over hello key lifecycle because you generate hello key and transfer it tooMicrosoft’s HSMs.</span></span>

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a><span data-ttu-id="7d959-139">Implementazione di BYOK (Bring Your Own Key) per l'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="7d959-139">Implementing bring your own key (BYOK) for Azure Key Vault</span></span>
<span data-ttu-id="7d959-140">Hello utilizzare seguenti informazioni e procedure, se si intende generare la propria chiave HSM protetta e quindi trasferire tale insieme di credenziali chiave tooAzure: hello portare il proprio scenario key (BYOK).</span><span class="sxs-lookup"><span data-stu-id="7d959-140">Use hello following information and procedures if you will generate your own HSM-protected key and then transfer it tooAzure Key Vault—hello bring your own key (BYOK) scenario.</span></span>

## <a name="prerequisites-for-byok"></a><span data-ttu-id="7d959-141">Prerequisiti per la modalità BYOK</span><span class="sxs-lookup"><span data-stu-id="7d959-141">Prerequisites for BYOK</span></span>
<span data-ttu-id="7d959-142">Vedere hello seguente tabella per un elenco di prerequisiti per trasferire la propria chiave (BYOK) per insieme credenziali chiavi Azure.</span><span class="sxs-lookup"><span data-stu-id="7d959-142">See hello following table for a list of prerequisites for bring your own key (BYOK) for Azure Key Vault.</span></span>

| <span data-ttu-id="7d959-143">Requisito</span><span class="sxs-lookup"><span data-stu-id="7d959-143">Requirement</span></span> | <span data-ttu-id="7d959-144">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="7d959-144">More information</span></span> |
| --- | --- |
| <span data-ttu-id="7d959-145">TooAzure una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="7d959-145">A subscription tooAzure</span></span> |<span data-ttu-id="7d959-146">toocreate un insieme di credenziali chiave di Azure, necessaria una sottoscrizione di Azure: [iscriversi per una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="7d959-146">toocreate an Azure Key Vault, you need an Azure subscription: [Sign up for free trial](https://azure.microsoft.com/pricing/free-trial/)</span></span> |
| <span data-ttu-id="7d959-147">Hello insieme di credenziali chiave di Azure Premium del servizio livello toosupport chiavi HSM protette</span><span class="sxs-lookup"><span data-stu-id="7d959-147">hello Azure Key Vault Premium service tier toosupport HSM-protected keys</span></span> |<span data-ttu-id="7d959-148">Per ulteriori informazioni sui livelli di servizio hello e funzionalità per l'insieme di credenziali chiave di Azure, vedere hello [dei prezzi di Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/) sito Web.</span><span class="sxs-lookup"><span data-stu-id="7d959-148">For more information about hello service tiers and capabilities for Azure Key Vault, see hello [Azure Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/) website.</span></span> |
| <span data-ttu-id="7d959-149">Moduli di protezione hardware Thales, smart card e software di supporto</span><span class="sxs-lookup"><span data-stu-id="7d959-149">Thales HSM, smartcards, and support software</span></span> |<span data-ttu-id="7d959-150">È necessario disporre di accesso tooa modulo di protezione Hardware Thales e base conoscenze operative di protezione hardware Thales.</span><span class="sxs-lookup"><span data-stu-id="7d959-150">You must have access tooa Thales Hardware Security Module and basic operational knowledge of Thales HSMs.</span></span> <span data-ttu-id="7d959-151">Vedere [modulo di protezione Hardware Thales](https://www.thales-esecurity.com/msrms/buy) per elenco hello dei modelli compatibili o toopurchase un modulo HSM se non è uno.</span><span class="sxs-lookup"><span data-stu-id="7d959-151">See [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) for hello list of compatible models, or toopurchase an HSM if you do not have one.</span></span> |
| <span data-ttu-id="7d959-152">Hello hardware e software seguenti:</span><span class="sxs-lookup"><span data-stu-id="7d959-152">hello following hardware and software:</span></span><ol><li><span data-ttu-id="7d959-153">Una workstation x64 offline con Windows 7 come versione minima del sistema operativo Windows e software Thales nShield con versione minima 11.50.</span><span class="sxs-lookup"><span data-stu-id="7d959-153">An offline x64 workstation with a minimum Windows operation system of Windows 7 and Thales nShield software that is at least version 11.50.</span></span><br/><br/><span data-ttu-id="7d959-154">Se questa workstation esegue Windows 7, è necessario [installare Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span><span class="sxs-lookup"><span data-stu-id="7d959-154">If this workstation runs Windows 7, you must [install Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span></span></li><li><span data-ttu-id="7d959-155">Una workstation in cui è connesso toohello Internet e ha un sistema operativo di Windows 7 e [Azure PowerShell](/powershell/azure/overview) **minima versione 1.1.0** installato.</span><span class="sxs-lookup"><span data-stu-id="7d959-155">A workstation that is connected toohello Internet and has a minimum Windows operating system of Windows 7 and [Azure PowerShell](/powershell/azure/overview) **minimum version 1.1.0** installed.</span></span></li><li><span data-ttu-id="7d959-156">Unità USB o un altro dispositivo di archiviazione portatile con almeno 16 MB di spazio disponibile.</span><span class="sxs-lookup"><span data-stu-id="7d959-156">A USB drive or other portable storage device that has at least 16 MB free space.</span></span></li></ol> |<span data-ttu-id="7d959-157">Per motivi di sicurezza, è consigliabile che prima workstation hello non è connesso tooa rete.</span><span class="sxs-lookup"><span data-stu-id="7d959-157">For security reasons, we recommend that hello first workstation is not connected tooa network.</span></span> <span data-ttu-id="7d959-158">Questa indicazione tuttavia non viene applicata a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="7d959-158">However, this recommendation is not programmatically enforced.</span></span><br/><br/><span data-ttu-id="7d959-159">Si noti che nelle istruzioni hello che seguono, questa workstation workstation disconnessa hello tooas cui viene fatto riferimento.</span><span class="sxs-lookup"><span data-stu-id="7d959-159">Note that in hello instructions that follow, this workstation is referred tooas hello disconnected workstation.</span></span></p></blockquote><br/><span data-ttu-id="7d959-160">Inoltre, se la chiave del tenant è per una rete di produzione, è consigliabile utilizzare una seconda workstation separata toodownload hello set di strumenti e il caricamento hello chiave del tenant.</span><span class="sxs-lookup"><span data-stu-id="7d959-160">In addition, if your tenant key is for a production network, we recommend that you use a second, separate workstation toodownload hello toolset and upload hello tenant key.</span></span> <span data-ttu-id="7d959-161">Ma a scopo di test, è possibile utilizzare hello stessa workstation come primo hello.</span><span class="sxs-lookup"><span data-stu-id="7d959-161">But for testing purposes, you can use hello same workstation as hello first one.</span></span><br/><br/><span data-ttu-id="7d959-162">Si noti che nelle istruzioni hello che seguono, alla seconda workstation workstation connessa a Internet di cui viene fatto riferimento tooas hello.</span><span class="sxs-lookup"><span data-stu-id="7d959-162">Note that in hello instructions that follow, this second workstation is referred tooas hello Internet-connected workstation.</span></span></p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-tooazure-key-vault-hsm"></a><span data-ttu-id="7d959-163">Generare e trasferire la chiave tooAzure modulo di protezione hardware dell'insieme di credenziali chiave</span><span class="sxs-lookup"><span data-stu-id="7d959-163">Generate and transfer your key tooAzure Key Vault HSM</span></span>
<span data-ttu-id="7d959-164">Verranno utilizzati i seguenti cinque passaggi toogenerate hello e trasferire la chiave tooan hardware dell'insieme di credenziali chiave di Azure:</span><span class="sxs-lookup"><span data-stu-id="7d959-164">You will use hello following five steps toogenerate and transfer your key tooan Azure Key Vault HSM:</span></span>

* [<span data-ttu-id="7d959-165">Passaggio 1: Preparare la workstation connessa a Internet</span><span class="sxs-lookup"><span data-stu-id="7d959-165">Step 1: Prepare your Internet-connected workstation</span></span>](#step-1-prepare-your-internet-connected-workstation)
* [<span data-ttu-id="7d959-166">Passaggio 2: Preparare la workstation disconnessa</span><span class="sxs-lookup"><span data-stu-id="7d959-166">Step 2: Prepare your disconnected workstation</span></span>](#step-2-prepare-your-disconnected-workstation)
* [<span data-ttu-id="7d959-167">Passaggio 3: Generare la chiave</span><span class="sxs-lookup"><span data-stu-id="7d959-167">Step 3: Generate your key</span></span>](#step-3-generate-your-key)
* [<span data-ttu-id="7d959-168">Passaggio 4: Preparare la chiave per il trasferimento</span><span class="sxs-lookup"><span data-stu-id="7d959-168">Step 4: Prepare your key for transfer</span></span>](#step-4-prepare-your-key-for-transfer)
* [<span data-ttu-id="7d959-169">Passaggio 5: Trasferire la chiave tooAzure insieme di credenziali chiave</span><span class="sxs-lookup"><span data-stu-id="7d959-169">Step 5: Transfer your key tooAzure Key Vault</span></span>](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a><span data-ttu-id="7d959-170">Passaggio 1: Preparare la workstation connessa a Internet</span><span class="sxs-lookup"><span data-stu-id="7d959-170">Step 1: Prepare your Internet-connected workstation</span></span>
<span data-ttu-id="7d959-171">Per il primo passaggio, hello seguire le procedure seguenti nella workstation che è connesso toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="7d959-171">For this first step, do hello following procedures on your workstation that is connected toohello Internet.</span></span>

### <a name="step-11-install-azure-powershell"></a><span data-ttu-id="7d959-172">Passaggio 1.1: Installare Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d959-172">Step 1.1: Install Azure PowerShell</span></span>
<span data-ttu-id="7d959-173">Dalla workstation connessa a Internet hello, scaricare e installare modulo Azure PowerShell hello che include i cmdlet di hello toomanage insieme credenziali chiavi Azure.</span><span class="sxs-lookup"><span data-stu-id="7d959-173">From hello Internet-connected workstation, download and install hello Azure PowerShell module that includes hello cmdlets toomanage Azure Key Vault.</span></span> <span data-ttu-id="7d959-174">È necessaria la versione minima 0.8.13.</span><span class="sxs-lookup"><span data-stu-id="7d959-174">This requires a minimum version of 0.8.13.</span></span>

<span data-ttu-id="7d959-175">Per istruzioni sull'installazione, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7d959-175">For installation instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="step-12-get-your-azure-subscription-id"></a><span data-ttu-id="7d959-176">Passaggio 1.2: Ottenere l'ID sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="7d959-176">Step 1.2: Get your Azure subscription ID</span></span>
<span data-ttu-id="7d959-177">Avviare una sessione di Azure PowerShell e accedere tooyour account Azure con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="7d959-177">Start an Azure PowerShell session and sign in tooyour Azure account by using hello following command:</span></span>

        Add-AzureAccount
<span data-ttu-id="7d959-178">Nella finestra popup del browser hello, immettere il nome utente dell'account Azure e la password.</span><span class="sxs-lookup"><span data-stu-id="7d959-178">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="7d959-179">Utilizzare quindi hello [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) comando:</span><span class="sxs-lookup"><span data-stu-id="7d959-179">Then, use hello [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) command:</span></span>

        Get-AzureSubscription
<span data-ttu-id="7d959-180">Dall'output di hello, individuare l'ID di hello per sottoscrizione hello che si utilizzeranno per insieme credenziali chiavi Azure.</span><span class="sxs-lookup"><span data-stu-id="7d959-180">From hello output, locate hello ID for hello subscription you will use for Azure Key Vault.</span></span> <span data-ttu-id="7d959-181">Questo ID sottoscrizione verrà usato in seguito.</span><span class="sxs-lookup"><span data-stu-id="7d959-181">You will need this subscription ID later.</span></span>

<span data-ttu-id="7d959-182">Non chiudere la finestra di Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="7d959-182">Do not close hello Azure PowerShell window.</span></span>

### <a name="step-13-download-hello-byok-toolset-for-azure-key-vault"></a><span data-ttu-id="7d959-183">Passaggio 1.3: Scaricare il set di strumenti BYOK hello per insieme credenziali chiavi Azure</span><span class="sxs-lookup"><span data-stu-id="7d959-183">Step 1.3: Download hello BYOK toolset for Azure Key Vault</span></span>
<span data-ttu-id="7d959-184">Passare toohello Microsoft Download Center e [scaricare set di strumenti BYOK insieme di credenziali chiave di Azure hello](http://www.microsoft.com/download/details.aspx?id=45345) per area geografica o istanza di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d959-184">Go toohello Microsoft Download Center and [download hello Azure Key Vault BYOK toolset](http://www.microsoft.com/download/details.aspx?id=45345) for your geographic region or instance of Azure.</span></span> <span data-ttu-id="7d959-185">Utilizzare la seguente hello hash del pacchetto toodownload nome pacchetto di informazioni tooidentify hello e il corrispondente SHA-256:</span><span class="sxs-lookup"><span data-stu-id="7d959-185">Use hello following information tooidentify hello package name toodownload and its corresponding SHA-256 package hash:</span></span>

- - -
<span data-ttu-id="7d959-186">**Stati Uniti:**</span><span class="sxs-lookup"><span data-stu-id="7d959-186">**United States:**</span></span>

<span data-ttu-id="7d959-187">KeyVault-BYOK-Tools-UnitedStates.zip</span><span class="sxs-lookup"><span data-stu-id="7d959-187">KeyVault-BYOK-Tools-UnitedStates.zip</span></span>

<span data-ttu-id="7d959-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span><span class="sxs-lookup"><span data-stu-id="7d959-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span></span>

- - -
<span data-ttu-id="7d959-189">**Europa:**</span><span class="sxs-lookup"><span data-stu-id="7d959-189">**Europe:**</span></span>

<span data-ttu-id="7d959-190">KeyVault-BYOK-Tools-Europe.zip</span><span class="sxs-lookup"><span data-stu-id="7d959-190">KeyVault-BYOK-Tools-Europe.zip</span></span>

<span data-ttu-id="7d959-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span><span class="sxs-lookup"><span data-stu-id="7d959-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span></span>

- - -
<span data-ttu-id="7d959-192">**Asia:**</span><span class="sxs-lookup"><span data-stu-id="7d959-192">**Asia:**</span></span>

<span data-ttu-id="7d959-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span><span class="sxs-lookup"><span data-stu-id="7d959-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span></span>

<span data-ttu-id="7d959-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span><span class="sxs-lookup"><span data-stu-id="7d959-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span></span>

- - -
<span data-ttu-id="7d959-195">**America Latina:**</span><span class="sxs-lookup"><span data-stu-id="7d959-195">**Latin America:**</span></span>

<span data-ttu-id="7d959-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span><span class="sxs-lookup"><span data-stu-id="7d959-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span></span>

<span data-ttu-id="7d959-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span><span class="sxs-lookup"><span data-stu-id="7d959-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span></span>

- - -
<span data-ttu-id="7d959-198">**Giappone:**</span><span class="sxs-lookup"><span data-stu-id="7d959-198">**Japan:**</span></span>

<span data-ttu-id="7d959-199">KeyVault-BYOK-Tools-Japan.zip</span><span class="sxs-lookup"><span data-stu-id="7d959-199">KeyVault-BYOK-Tools-Japan.zip</span></span>

<span data-ttu-id="7d959-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span><span class="sxs-lookup"><span data-stu-id="7d959-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span></span>

- - -
<span data-ttu-id="7d959-201">**Corea:**</span><span class="sxs-lookup"><span data-stu-id="7d959-201">**Korea:**</span></span>

<span data-ttu-id="7d959-202">KeyVault-BYOK-strumenti-Korea.zip</span><span class="sxs-lookup"><span data-stu-id="7d959-202">KeyVault-BYOK-Tools-Korea.zip</span></span>

<span data-ttu-id="7d959-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span><span class="sxs-lookup"><span data-stu-id="7d959-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span></span>

- - -
<span data-ttu-id="7d959-204">**Australia:**</span><span class="sxs-lookup"><span data-stu-id="7d959-204">**Australia:**</span></span>

<span data-ttu-id="7d959-205">KeyVault-BYOK-Tools-Australia.zip</span><span class="sxs-lookup"><span data-stu-id="7d959-205">KeyVault-BYOK-Tools-Australia.zip</span></span>

<span data-ttu-id="7d959-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span><span class="sxs-lookup"><span data-stu-id="7d959-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span></span>

- - -
[<span data-ttu-id="7d959-207">**Azure per enti pubblici:**</span><span class="sxs-lookup"><span data-stu-id="7d959-207">**Azure Government:**</span></span>](https://azure.microsoft.com/features/gov/)

<span data-ttu-id="7d959-208">KeyVault-BYOK-Tools-USGovCloud.zip</span><span class="sxs-lookup"><span data-stu-id="7d959-208">KeyVault-BYOK-Tools-USGovCloud.zip</span></span>

<span data-ttu-id="7d959-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span><span class="sxs-lookup"><span data-stu-id="7d959-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span></span>

- - -
<span data-ttu-id="7d959-210">**Dipartimento della difesa del governo degli Stati Uniti:**</span><span class="sxs-lookup"><span data-stu-id="7d959-210">**US Government DOD:**</span></span>

<span data-ttu-id="7d959-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span><span class="sxs-lookup"><span data-stu-id="7d959-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span></span>

<span data-ttu-id="7d959-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span><span class="sxs-lookup"><span data-stu-id="7d959-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span></span>

- - -
<span data-ttu-id="7d959-213">**Canada:**</span><span class="sxs-lookup"><span data-stu-id="7d959-213">**Canada:**</span></span>

<span data-ttu-id="7d959-214">KeyVault-BYOK-Tools-Canada.zip</span><span class="sxs-lookup"><span data-stu-id="7d959-214">KeyVault-BYOK-Tools-Canada.zip</span></span>

<span data-ttu-id="7d959-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span><span class="sxs-lookup"><span data-stu-id="7d959-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span></span>

- - -
<span data-ttu-id="7d959-216">**Germania:**</span><span class="sxs-lookup"><span data-stu-id="7d959-216">**Germany:**</span></span>

<span data-ttu-id="7d959-217">KeyVault-BYOK-Tools-Germany.zip</span><span class="sxs-lookup"><span data-stu-id="7d959-217">KeyVault-BYOK-Tools-Germany.zip</span></span>

<span data-ttu-id="7d959-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span><span class="sxs-lookup"><span data-stu-id="7d959-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span></span>

- - -
<span data-ttu-id="7d959-219">**India:**</span><span class="sxs-lookup"><span data-stu-id="7d959-219">**India:**</span></span>

<span data-ttu-id="7d959-220">KeyVault-BYOK-Tools-India.zip</span><span class="sxs-lookup"><span data-stu-id="7d959-220">KeyVault-BYOK-Tools-India.zip</span></span>

<span data-ttu-id="7d959-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span><span class="sxs-lookup"><span data-stu-id="7d959-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span></span>

- - -
<span data-ttu-id="7d959-222">**Regno Unito:**</span><span class="sxs-lookup"><span data-stu-id="7d959-222">**United Kingdom:**</span></span>

<span data-ttu-id="7d959-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span><span class="sxs-lookup"><span data-stu-id="7d959-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span></span>

<span data-ttu-id="7d959-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span><span class="sxs-lookup"><span data-stu-id="7d959-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span></span>

- - -

<span data-ttu-id="7d959-225">integrità hello toovalidate dello scaricato set di strumenti BYOK, dalla sessione di PowerShell di Azure, utilizzare hello [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7d959-225">toovalidate hello integrity of your downloaded BYOK toolset, from your Azure PowerShell session, use hello [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span></span>

    Get-FileHash KeyVault-BYOK-Tools-*.zip

<span data-ttu-id="7d959-226">set di strumenti di Hello include seguente hello:</span><span class="sxs-lookup"><span data-stu-id="7d959-226">hello toolset includes hello following:</span></span>

* <span data-ttu-id="7d959-227">Un pacchetto di chiavi per lo scambio di chiavi (KEK) con un nome che inizia con **BYOK-KEK-pkg-.**</span><span class="sxs-lookup"><span data-stu-id="7d959-227">A Key Exchange Key (KEK) package that has a name beginning with **BYOK-KEK-pkg-.**</span></span>
* <span data-ttu-id="7d959-228">Un pacchetto relativo all'ambiente di sicurezza con un nome che inizia con **BYOK-SecurityWorld-pkg-.**</span><span class="sxs-lookup"><span data-stu-id="7d959-228">A Security World package that has a name beginning with **BYOK-SecurityWorld-pkg-.**</span></span>
* <span data-ttu-id="7d959-229">Uno script python denominato **verifykeypackage.py.**</span><span class="sxs-lookup"><span data-stu-id="7d959-229">A python script named **verifykeypackage.py.**</span></span>
* <span data-ttu-id="7d959-230">File eseguibile dalla riga di comando denominato **KeyTransferRemote.exe** e DLL associate.</span><span class="sxs-lookup"><span data-stu-id="7d959-230">A command-line executable file named **KeyTransferRemote.exe** and associated DLLs.</span></span>
* <span data-ttu-id="7d959-231">Componente Visual C++ Redistributable Package denominato **vcredist_x64.exe.**</span><span class="sxs-lookup"><span data-stu-id="7d959-231">A Visual C++ Redistributable Package, named **vcredist_x64.exe.**</span></span>

<span data-ttu-id="7d959-232">Copia un'unità USB tooa hello pacchetto o altro dispositivo di archiviazione portatile.</span><span class="sxs-lookup"><span data-stu-id="7d959-232">Copy hello package tooa USB drive or other portable storage.</span></span>

## <a name="step-2-prepare-your-disconnected-workstation"></a><span data-ttu-id="7d959-233">Passaggio 2: Preparare la workstation disconnessa</span><span class="sxs-lookup"><span data-stu-id="7d959-233">Step 2: Prepare your disconnected workstation</span></span>
<span data-ttu-id="7d959-234">Per questo secondo passaggio, hello seguire le procedure seguenti in workstation hello che non sia connessa tooa rete (hello Internet o rete interna).</span><span class="sxs-lookup"><span data-stu-id="7d959-234">For this second step, do hello following procedures on hello workstation that is not connected tooa network (either hello Internet or your internal network).</span></span>

### <a name="step-21-prepare-hello-disconnected-workstation-with-thales-hsm"></a><span data-ttu-id="7d959-235">Passaggio 2.1: Preparare workstation disconnessa hello con modulo di protezione hardware Thales</span><span class="sxs-lookup"><span data-stu-id="7d959-235">Step 2.1: Prepare hello disconnected workstation with Thales HSM</span></span>
<span data-ttu-id="7d959-236">Installare il software di supporto nCipher (Thales) hello in un computer Windows e quindi collegare un computer toothat di protezione hardware Thales.</span><span class="sxs-lookup"><span data-stu-id="7d959-236">Install hello nCipher (Thales) support software on a Windows computer, and then attach a Thales HSM toothat computer.</span></span>

<span data-ttu-id="7d959-237">Verificare che hello strumenti Thales si trovino nei percorsi (**%nfast_home%\bin**).</span><span class="sxs-lookup"><span data-stu-id="7d959-237">Ensure that hello Thales tools are in your path (**%nfast_home%\bin**).</span></span> <span data-ttu-id="7d959-238">Ad esempio, digitare il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="7d959-238">For example, type hello following:</span></span>

        set PATH=%PATH%;"%nfast_home%\bin"

<span data-ttu-id="7d959-239">Per ulteriori informazioni, vedere Guida dell'utente hello inclusa con hello di protezione hardware Thales.</span><span class="sxs-lookup"><span data-stu-id="7d959-239">For more information, see hello user guide included with hello Thales HSM.</span></span>

### <a name="step-22-install-hello-byok-toolset-on-hello-disconnected-workstation"></a><span data-ttu-id="7d959-240">Passaggio 2.2: Installazione hello set di strumenti BYOK nella workstation disconnessa hello</span><span class="sxs-lookup"><span data-stu-id="7d959-240">Step 2.2: Install hello BYOK toolset on hello disconnected workstation</span></span>
<span data-ttu-id="7d959-241">Copiare pacchetto di set di strumenti BYOK hello dall'unità USB hello o un altro dispositivo di archiviazione portatile e quindi hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="7d959-241">Copy hello BYOK toolset package from hello USB drive or other portable storage, and then do hello following:</span></span>

1. <span data-ttu-id="7d959-242">Estrarre i file di hello dal pacchetto scaricato hello in una cartella qualsiasi.</span><span class="sxs-lookup"><span data-stu-id="7d959-242">Extract hello files from hello downloaded package into any folder.</span></span>
2. <span data-ttu-id="7d959-243">In tale cartella eseguire vcredist_x64.exe.</span><span class="sxs-lookup"><span data-stu-id="7d959-243">From that folder, run vcredist_x64.exe.</span></span>
3. <span data-ttu-id="7d959-244">Seguire le istruzioni di hello toohello installare i componenti di runtime di hello Visual C++ per Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="7d959-244">Follow hello instructions toohello install hello Visual C++ runtime components for Visual Studio 2013.</span></span>

## <a name="step-3-generate-your-key"></a><span data-ttu-id="7d959-245">Passaggio 3: Generare la chiave</span><span class="sxs-lookup"><span data-stu-id="7d959-245">Step 3: Generate your key</span></span>
<span data-ttu-id="7d959-246">Per questo terzo passaggio, hello seguire le procedure seguenti nella workstation disconnessa hello.</span><span class="sxs-lookup"><span data-stu-id="7d959-246">For this third step, do hello following procedures on hello disconnected workstation.</span></span> <span data-ttu-id="7d959-247">toocomplete questo passaggio il modulo di protezione hardware deve essere in modalità di inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="7d959-247">toocomplete this step your HSM must be in initialization mode.</span></span> 


### <a name="step-31-change-hello-hsm-mode-tooi"></a><span data-ttu-id="7d959-248">Passaggio 3.1: Modificare hello HSM modalità too'I'</span><span class="sxs-lookup"><span data-stu-id="7d959-248">Step 3.1: Change hello HSM mode too'I'</span></span>
<span data-ttu-id="7d959-249">Se si utilizza nShield di Thales bordo, in modalità hello toochange: 1.</span><span class="sxs-lookup"><span data-stu-id="7d959-249">If you are using Thales nShield Edge, toochange hello mode: 1.</span></span> <span data-ttu-id="7d959-250">Modalità hello modalità pulsante toohighlight hello obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="7d959-250">Use hello Mode button toohighlight hello required mode.</span></span> <span data-ttu-id="7d959-251">2.</span><span class="sxs-lookup"><span data-stu-id="7d959-251">2.</span></span> <span data-ttu-id="7d959-252">Entro pochi secondi, tenere premuto il pulsante Cancella hello per pochi secondi.</span><span class="sxs-lookup"><span data-stu-id="7d959-252">Within a few seconds, press and hold hello Clear button for a couple of seconds.</span></span> <span data-ttu-id="7d959-253">Se viene modificata la modalità hello, hello nuova modalità si arresta LED lampeggiante e rimane acceso.</span><span class="sxs-lookup"><span data-stu-id="7d959-253">If hello mode changes, hello new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="7d959-254">Hello il LED di stato potrebbe flash irregolare per pochi secondi e quindi fa lampeggiare regolarmente quando il dispositivo hello è pronto.</span><span class="sxs-lookup"><span data-stu-id="7d959-254">hello Status LED might flash irregularly for a few seconds and then flashes regularly when hello device is ready.</span></span> <span data-ttu-id="7d959-255">In caso contrario, hello dispositivo rimane in modalità corrente hello con la modalità appropriata hello LED acceso.</span><span class="sxs-lookup"><span data-stu-id="7d959-255">Otherwise, hello device remains in hello current mode, with hello appropriate mode LED lit.</span></span>

### <a name="step-32-create-a-security-world"></a><span data-ttu-id="7d959-256">Passaggio 3.2: Creare un ambiente di sicurezza</span><span class="sxs-lookup"><span data-stu-id="7d959-256">Step 3.2: Create a security world</span></span>
<span data-ttu-id="7d959-257">Avviare un prompt dei comandi ed eseguire hello programma new-world di Thales.</span><span class="sxs-lookup"><span data-stu-id="7d959-257">Start a command prompt and run hello Thales new-world program.</span></span>

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

<span data-ttu-id="7d959-258">Tale programma crea un **ambiente di sicurezza** file NFAST_KMDATA%\local\world, che corrisponde a cartella C:\ProgramData\nCipher\Key Management data\local. toohello %.</span><span class="sxs-lookup"><span data-stu-id="7d959-258">This program creates a **Security World** file at %NFAST_KMDATA%\local\world, which corresponds toohello C:\ProgramData\nCipher\Key Management Data\local folder.</span></span> <span data-ttu-id="7d959-259">È possibile utilizzare valori diversi per il quorum hello ma in questo esempio, si è ancora schede vuote tooenter richiesta tre e un codice PIN per ciascuna di esse.</span><span class="sxs-lookup"><span data-stu-id="7d959-259">You can use different values for hello quorum but in our example, you’re prompted tooenter three blank cards and pins for each one.</span></span> <span data-ttu-id="7d959-260">Quindi, qualsiasi coppia di schede forniti ambiente di sicurezza toohello accesso completo.</span><span class="sxs-lookup"><span data-stu-id="7d959-260">Then, any two cards give full access toohello security world.</span></span> <span data-ttu-id="7d959-261">Tali schede diventano hello **Set di schede amministrative** per il nuovo ambiente di sicurezza hello.</span><span class="sxs-lookup"><span data-stu-id="7d959-261">These cards become hello **Administrator Card Set** for hello new security world.</span></span>

<span data-ttu-id="7d959-262">Quindi hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="7d959-262">Then do hello following:</span></span>

* <span data-ttu-id="7d959-263">Eseguire il backup di file di hello world.</span><span class="sxs-lookup"><span data-stu-id="7d959-263">Back up hello world file.</span></span> <span data-ttu-id="7d959-264">Proteggere i file di hello world hello amministratore schede e i codici PIN e assicurarsi che nessuna singola persona possa accedere toomore rispetto a una scheda.</span><span class="sxs-lookup"><span data-stu-id="7d959-264">Secure and protect hello world file, hello Administrator Cards, and their pins, and make sure that no single person has access toomore than one card.</span></span>

### <a name="step-33-change-hello-hsm-mode-tooo"></a><span data-ttu-id="7d959-265">Passaggio 3.3: Modificare hello HSM modalità too'O'</span><span class="sxs-lookup"><span data-stu-id="7d959-265">Step 3.3: Change hello HSM mode too'O'</span></span>
<span data-ttu-id="7d959-266">Se si utilizza nShield di Thales bordo, in modalità hello toochange: 1.</span><span class="sxs-lookup"><span data-stu-id="7d959-266">If you are using Thales nShield Edge, toochange hello mode: 1.</span></span> <span data-ttu-id="7d959-267">Modalità hello modalità pulsante toohighlight hello obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="7d959-267">Use hello Mode button toohighlight hello required mode.</span></span> <span data-ttu-id="7d959-268">2.</span><span class="sxs-lookup"><span data-stu-id="7d959-268">2.</span></span> <span data-ttu-id="7d959-269">Entro pochi secondi, tenere premuto il pulsante Cancella hello per pochi secondi.</span><span class="sxs-lookup"><span data-stu-id="7d959-269">Within a few seconds, press and hold hello Clear button for a couple of seconds.</span></span> <span data-ttu-id="7d959-270">Se viene modificata la modalità hello, hello nuova modalità si arresta LED lampeggiante e rimane acceso.</span><span class="sxs-lookup"><span data-stu-id="7d959-270">If hello mode changes, hello new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="7d959-271">Hello il LED di stato potrebbe flash irregolare per pochi secondi e quindi fa lampeggiare regolarmente quando il dispositivo hello è pronto.</span><span class="sxs-lookup"><span data-stu-id="7d959-271">hello Status LED might flash irregularly for a few seconds and then flashes regularly when hello device is ready.</span></span> <span data-ttu-id="7d959-272">In caso contrario, hello dispositivo rimane in modalità corrente hello con la modalità appropriata hello LED acceso.</span><span class="sxs-lookup"><span data-stu-id="7d959-272">Otherwise, hello device remains in hello current mode, with hello appropriate mode LED lit.</span></span>


### <a name="step-34-validate-hello-downloaded-package"></a><span data-ttu-id="7d959-273">Passaggio 3.4: Convalidare il pacchetto scaricato hello</span><span class="sxs-lookup"><span data-stu-id="7d959-273">Step 3.4: Validate hello downloaded package</span></span>
<span data-ttu-id="7d959-274">Questo passaggio è facoltativo ma consigliato, in modo che sia possibile convalidare seguente hello:</span><span class="sxs-lookup"><span data-stu-id="7d959-274">This step is optional but recommended so that you can validate hello following:</span></span>

* <span data-ttu-id="7d959-275">Chiave di scambio di chiave che è incluso nel set di strumenti hello Hello è stato generato da un modulo di protezione hardware Thales originale.</span><span class="sxs-lookup"><span data-stu-id="7d959-275">hello Key Exchange Key that is included in hello toolset has been generated from a genuine Thales HSM.</span></span>
* <span data-ttu-id="7d959-276">hash Hello di hello World di sicurezza che è incluso nel set di strumenti hello è stato generato da un modulo di protezione hardware Thales originale.</span><span class="sxs-lookup"><span data-stu-id="7d959-276">hello hash of hello Security World that is included in hello toolset has been generated in a genuine Thales HSM.</span></span>
* <span data-ttu-id="7d959-277">Chiave di scambio chiave Hello è non esportabile.</span><span class="sxs-lookup"><span data-stu-id="7d959-277">hello Key Exchange Key is non-exportable.</span></span>

> [!NOTE]
> <span data-ttu-id="7d959-278">hello toovalidate scaricato pacchetto, hello HSM deve essere connessa, acceso e deve avere un ambiente di sicurezza (ad esempio hello quello che appena creato).</span><span class="sxs-lookup"><span data-stu-id="7d959-278">toovalidate hello downloaded package, hello HSM must be connected, powered on, and must have a security world on it (such as hello one you’ve just created).</span></span>
>
>

<span data-ttu-id="7d959-279">pacchetto di hello scaricato toovalidate:</span><span class="sxs-lookup"><span data-stu-id="7d959-279">toovalidate hello downloaded package:</span></span>

1. <span data-ttu-id="7d959-280">Eseguire script verifykeypackage.py hello digitando uno dei seguenti hello, a seconda dell'area geografica o l'istanza di Azure:</span><span class="sxs-lookup"><span data-stu-id="7d959-280">Run hello verifykeypackage.py script by typing one of hello following, depending on your geographic region or instance of Azure:</span></span>

   * <span data-ttu-id="7d959-281">America del Nord</span><span class="sxs-lookup"><span data-stu-id="7d959-281">For North America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * <span data-ttu-id="7d959-282">Europa</span><span class="sxs-lookup"><span data-stu-id="7d959-282">For Europe:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * <span data-ttu-id="7d959-283">Asia</span><span class="sxs-lookup"><span data-stu-id="7d959-283">For Asia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * <span data-ttu-id="7d959-284">America Latina</span><span class="sxs-lookup"><span data-stu-id="7d959-284">For Latin America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * <span data-ttu-id="7d959-285">Giappone</span><span class="sxs-lookup"><span data-stu-id="7d959-285">For Japan:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * <span data-ttu-id="7d959-286">Per la Corea:</span><span class="sxs-lookup"><span data-stu-id="7d959-286">For Korea:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * <span data-ttu-id="7d959-287">Per l'Australia:</span><span class="sxs-lookup"><span data-stu-id="7d959-287">For Australia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * <span data-ttu-id="7d959-288">Per [Azure per enti pubblici](https://azure.microsoft.com/features/gov/), che utilizza l'istanza di hello US government di Azure:</span><span class="sxs-lookup"><span data-stu-id="7d959-288">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * <span data-ttu-id="7d959-289">Per il Dipartimento della difesa del governo degli Stati Uniti:</span><span class="sxs-lookup"><span data-stu-id="7d959-289">For US Government DOD:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * <span data-ttu-id="7d959-290">Per il Canada:</span><span class="sxs-lookup"><span data-stu-id="7d959-290">For Canada:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * <span data-ttu-id="7d959-291">Per la Germania:</span><span class="sxs-lookup"><span data-stu-id="7d959-291">For Germany:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * <span data-ttu-id="7d959-292">Per l'India:</span><span class="sxs-lookup"><span data-stu-id="7d959-292">For India:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > <span data-ttu-id="7d959-293">Hello software Thales include python nel %NFAST_HOME%\python\bin</span><span class="sxs-lookup"><span data-stu-id="7d959-293">hello Thales software includes python at %NFAST_HOME%\python\bin</span></span>
     >
     >
2. <span data-ttu-id="7d959-294">Confermare la visualizzazione seguente hello, che indica il completamento della convalida: **risultato: operazione riuscita**</span><span class="sxs-lookup"><span data-stu-id="7d959-294">Confirm that you see hello following, which indicates successful validation: **Result: SUCCESS**</span></span>

<span data-ttu-id="7d959-295">Questo script consente di convalidare la catena di firmatari hello backup toohello chiave radice di Thales.</span><span class="sxs-lookup"><span data-stu-id="7d959-295">This script validates hello signer chain up toohello Thales root key.</span></span> <span data-ttu-id="7d959-296">Hello hash di questa chiave radice è incorporata nello script hello e il relativo valore deve essere **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span><span class="sxs-lookup"><span data-stu-id="7d959-296">hello hash of this root key is embedded in hello script and its value should be **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span></span> <span data-ttu-id="7d959-297">Si può anche confermare questo valore separatamente visitando hello [sito Web di Thales](http://www.thalesesec.com/).</span><span class="sxs-lookup"><span data-stu-id="7d959-297">You can also confirm this value separately by visiting hello [Thales website](http://www.thalesesec.com/).</span></span>

<span data-ttu-id="7d959-298">Si è ora pronto toocreate una nuova chiave.</span><span class="sxs-lookup"><span data-stu-id="7d959-298">You’re now ready toocreate a new key.</span></span>

### <a name="step-35-create-a-new-key"></a><span data-ttu-id="7d959-299">Passaggio 3.5: Creare una nuova chiave</span><span class="sxs-lookup"><span data-stu-id="7d959-299">Step 3.5: Create a new key</span></span>
<span data-ttu-id="7d959-300">Generare una chiave tramite hello Thales **generatekey** programma.</span><span class="sxs-lookup"><span data-stu-id="7d959-300">Generate a key by using hello Thales **generatekey** program.</span></span>

<span data-ttu-id="7d959-301">Eseguire hello seguente tasto di comando toogenerate hello:</span><span class="sxs-lookup"><span data-stu-id="7d959-301">Run hello following command toogenerate hello key:</span></span>

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

<span data-ttu-id="7d959-302">Quando si esegue il comando, usare le istruzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7d959-302">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="7d959-303">parametro Hello *proteggere* deve essere impostato il valore di toohello **modulo**, come illustrato.</span><span class="sxs-lookup"><span data-stu-id="7d959-303">hello parameter *protect* must be set toohello value **module**, as shown.</span></span> <span data-ttu-id="7d959-304">Verrà creata una chiave protetta tramite modulo.</span><span class="sxs-lookup"><span data-stu-id="7d959-304">This creates a module-protected key.</span></span> <span data-ttu-id="7d959-305">set di strumenti BYOK Hello non supporta le chiavi protette da OCS.</span><span class="sxs-lookup"><span data-stu-id="7d959-305">hello BYOK toolset does not support OCS-protected keys.</span></span>
* <span data-ttu-id="7d959-306">Sostituire il valore di hello di *contosokey* per hello **ident** e **plainname** con qualsiasi valore di stringa.</span><span class="sxs-lookup"><span data-stu-id="7d959-306">Replace hello value of *contosokey* for hello **ident** and **plainname** with any string value.</span></span> <span data-ttu-id="7d959-307">sovraccarico amministrativo toominimize e ridurre il rischio di hello di errori, è consigliabile utilizzare hello stesso valore per entrambi.</span><span class="sxs-lookup"><span data-stu-id="7d959-307">toominimize administrative overheads and reduce hello risk of errors, we recommend that you use hello same value for both.</span></span> <span data-ttu-id="7d959-308">Hello **ident** valore deve contenere solo numeri, trattini e lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="7d959-308">hello **ident** value must contain only numbers, dashes, and lower case letters.</span></span>
* <span data-ttu-id="7d959-309">elemento pubexp Hello viene lasciato vuoto (impostazione predefinita) in questo esempio, ma è possibile specificare valori specifici.</span><span class="sxs-lookup"><span data-stu-id="7d959-309">hello pubexp is left blank (default) in this example, but you can specify specific values.</span></span> <span data-ttu-id="7d959-310">Per ulteriori informazioni, vedere la documentazione di Thales hello.</span><span class="sxs-lookup"><span data-stu-id="7d959-310">For more information, see hello Thales documentation.</span></span>

<span data-ttu-id="7d959-311">Questo comando crea un file di chiave in formato token nella cartella %NFAST_KMDATA%\local con un nome che inizia con **key_simple _**, seguito da hello **ident** che è stato specificato nel comando hello.</span><span class="sxs-lookup"><span data-stu-id="7d959-311">This command creates a Tokenized Key file in your %NFAST_KMDATA%\local folder with a name starting with **key_simple_**, followed by hello **ident** that was specified in hello command.</span></span> <span data-ttu-id="7d959-312">Ad esempio: **key_simple_contosokey**.</span><span class="sxs-lookup"><span data-stu-id="7d959-312">For example: **key_simple_contosokey**.</span></span> <span data-ttu-id="7d959-313">Questo file contiene una chiave crittografata.</span><span class="sxs-lookup"><span data-stu-id="7d959-313">This file contains an encrypted key.</span></span>

<span data-ttu-id="7d959-314">Eseguire il backup del file di chiave in formato token in un percorso sicuro.</span><span class="sxs-lookup"><span data-stu-id="7d959-314">Back up this Tokenized Key File in a safe location.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d959-315">Quando in seguito si trasferisce la chiave tooAzure insieme di credenziali chiave, Microsoft non è possibile esportare questa chiave tooyou indietro, pertanto è estremamente importante eseguire il backup della chiave e la sicurezza dell'ambiente in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="7d959-315">When you later transfer your key tooAzure Key Vault, Microsoft cannot export this key back tooyou so it becomes extremely important that you back up your key and security world safely.</span></span> <span data-ttu-id="7d959-316">Per ottenere informazioni aggiuntive e procedure consigliate per eseguire il backup della chiave, contattare Thales.</span><span class="sxs-lookup"><span data-stu-id="7d959-316">Contact Thales for guidance and best practices for backing up your key.</span></span>
>
>

<span data-ttu-id="7d959-317">Si sono ora pronti tootransfer la chiave tooAzure insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="7d959-317">You are now ready tootransfer your key tooAzure Key Vault.</span></span>

## <a name="step-4-prepare-your-key-for-transfer"></a><span data-ttu-id="7d959-318">Passaggio 4: Preparare la chiave per il trasferimento</span><span class="sxs-lookup"><span data-stu-id="7d959-318">Step 4: Prepare your key for transfer</span></span>
<span data-ttu-id="7d959-319">Per questo passaggio quarto hello seguire le procedure seguenti nella workstation disconnessa hello.</span><span class="sxs-lookup"><span data-stu-id="7d959-319">For this fourth step, do hello following procedures on hello disconnected workstation.</span></span>

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a><span data-ttu-id="7d959-320">Passaggio 4.1: Creare una copia della chiave con autorizzazioni ridotte</span><span class="sxs-lookup"><span data-stu-id="7d959-320">Step 4.1: Create a copy of your key with reduced permissions</span></span>

<span data-ttu-id="7d959-321">Aprire un nuovo prompt dei comandi e modificare hello toohello percorso della directory corrente in cui è stato decompresso file zip di hello BYOK.</span><span class="sxs-lookup"><span data-stu-id="7d959-321">Open a new command prompt and change hello current directory toohello location where you unzipped hello BYOK zip file.</span></span> <span data-ttu-id="7d959-322">le autorizzazioni di hello tooreduce per la chiave, da un prompt dei comandi, eseguono uno dei seguenti hello, a seconda dell'area geografica o l'istanza di Azure:</span><span class="sxs-lookup"><span data-stu-id="7d959-322">tooreduce hello permissions on your key, from a command prompt, run one of hello following, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="7d959-323">America del Nord</span><span class="sxs-lookup"><span data-stu-id="7d959-323">For North America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* <span data-ttu-id="7d959-324">Europa</span><span class="sxs-lookup"><span data-stu-id="7d959-324">For Europe:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* <span data-ttu-id="7d959-325">Asia</span><span class="sxs-lookup"><span data-stu-id="7d959-325">For Asia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* <span data-ttu-id="7d959-326">America Latina</span><span class="sxs-lookup"><span data-stu-id="7d959-326">For Latin America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* <span data-ttu-id="7d959-327">Giappone</span><span class="sxs-lookup"><span data-stu-id="7d959-327">For Japan:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* <span data-ttu-id="7d959-328">Per la Corea:</span><span class="sxs-lookup"><span data-stu-id="7d959-328">For Korea:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* <span data-ttu-id="7d959-329">Per l'Australia:</span><span class="sxs-lookup"><span data-stu-id="7d959-329">For Australia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* <span data-ttu-id="7d959-330">Per [Azure per enti pubblici](https://azure.microsoft.com/features/gov/), che utilizza l'istanza di hello US government di Azure:</span><span class="sxs-lookup"><span data-stu-id="7d959-330">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* <span data-ttu-id="7d959-331">Per il Dipartimento della difesa del governo degli Stati Uniti:</span><span class="sxs-lookup"><span data-stu-id="7d959-331">For US Government DOD:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* <span data-ttu-id="7d959-332">Per il Canada:</span><span class="sxs-lookup"><span data-stu-id="7d959-332">For Canada:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* <span data-ttu-id="7d959-333">Per la Germania:</span><span class="sxs-lookup"><span data-stu-id="7d959-333">For Germany:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* <span data-ttu-id="7d959-334">Per l'India:</span><span class="sxs-lookup"><span data-stu-id="7d959-334">For India:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

<span data-ttu-id="7d959-335">Quando si esegue questo comando, sostituire *contosokey* con hello stesso valore specificato in **3.5 passaggio: creare una nuova chiave** da hello [generare la chiave](#step-3-generate-your-key) passaggio.</span><span class="sxs-lookup"><span data-stu-id="7d959-335">When you run this command, replace *contosokey* with hello same value you specified in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>

<span data-ttu-id="7d959-336">Verrà chiesto tooplug le schede amministrazione ambiente di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="7d959-336">You are asked tooplug in your security world admin cards.</span></span>

<span data-ttu-id="7d959-337">Al termine, il comando hello vedrai **risultato: successo** e copia hello della chiave con autorizzazioni ridotte si trovano in hello file denominato key_xferacid _<contosokey>.</span><span class="sxs-lookup"><span data-stu-id="7d959-337">When hello command completes, you see **Result: SUCCESS** and hello copy of your key with reduced permissions are in hello file named key_xferacId_<contosokey>.</span></span>

<span data-ttu-id="7d959-338">È possibile controlla hello gli ACL mediante i seguenti comandi utilizzando hello utilità Thales:</span><span class="sxs-lookup"><span data-stu-id="7d959-338">You may inspects hello ACLS using following commands using hello Thales utilities:</span></span>

* <span data-ttu-id="7d959-339">aclprint.py:</span><span class="sxs-lookup"><span data-stu-id="7d959-339">aclprint.py:</span></span>

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* <span data-ttu-id="7d959-340">kmfile-dump.exe:</span><span class="sxs-lookup"><span data-stu-id="7d959-340">kmfile-dump.exe:</span></span>

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  <span data-ttu-id="7d959-341">Quando si eseguono questi comandi, sostituire contosokey con hello stesso valore specificato in **3.5 passaggio: creare una nuova chiave** da hello [generare la chiave](#step-3-generate-your-key) passaggio.</span><span class="sxs-lookup"><span data-stu-id="7d959-341">When you run these commands, replace contosokey with hello same value you specified in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a><span data-ttu-id="7d959-342">Passaggio 4.2: Crittografare la chiave tramite la chiave per lo scambio di chiavi di Microsoft</span><span class="sxs-lookup"><span data-stu-id="7d959-342">Step 4.2: Encrypt your key by using Microsoft’s Key Exchange Key</span></span>
<span data-ttu-id="7d959-343">Eseguire uno dei seguenti comandi, a seconda dell'area geografica o l'istanza di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="7d959-343">Run one of hello following commands, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="7d959-344">America del Nord</span><span class="sxs-lookup"><span data-stu-id="7d959-344">For North America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="7d959-345">Europa</span><span class="sxs-lookup"><span data-stu-id="7d959-345">For Europe:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="7d959-346">Asia</span><span class="sxs-lookup"><span data-stu-id="7d959-346">For Asia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="7d959-347">America Latina</span><span class="sxs-lookup"><span data-stu-id="7d959-347">For Latin America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="7d959-348">Giappone</span><span class="sxs-lookup"><span data-stu-id="7d959-348">For Japan:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="7d959-349">Per la Corea:</span><span class="sxs-lookup"><span data-stu-id="7d959-349">For Korea:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="7d959-350">Per l'Australia:</span><span class="sxs-lookup"><span data-stu-id="7d959-350">For Australia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="7d959-351">Per [Azure per enti pubblici](https://azure.microsoft.com/features/gov/), che utilizza l'istanza di hello US government di Azure:</span><span class="sxs-lookup"><span data-stu-id="7d959-351">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="7d959-352">Per il Dipartimento della difesa del governo degli Stati Uniti:</span><span class="sxs-lookup"><span data-stu-id="7d959-352">For US Government DOD:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="7d959-353">Per il Canada:</span><span class="sxs-lookup"><span data-stu-id="7d959-353">For Canada:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="7d959-354">Per la Germania:</span><span class="sxs-lookup"><span data-stu-id="7d959-354">For Germany:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="7d959-355">Per l'India:</span><span class="sxs-lookup"><span data-stu-id="7d959-355">For India:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

<span data-ttu-id="7d959-356">Quando si esegue il comando, usare le istruzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7d959-356">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="7d959-357">Sostituire *contosokey* con identificatore hello usato chiave hello toogenerate **3.5 passaggio: creare una nuova chiave** da hello [generare la chiave](#step-3-generate-your-key) passaggio.</span><span class="sxs-lookup"><span data-stu-id="7d959-357">Replace *contosokey* with hello identifier that you used toogenerate hello key in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>
* <span data-ttu-id="7d959-358">Sostituire *SubscriptionID* con ID hello hello sottoscrizione di Azure che contiene l'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="7d959-358">Replace *SubscriptionID* with hello ID of hello Azure subscription that contains your key vault.</span></span> <span data-ttu-id="7d959-359">Questo valore è stato recuperato in precedenza, in **passaggio 1.2: ottenere l'ID sottoscrizione di Azure** da hello [preparare la workstation connessa a Internet](#step-1-prepare-your-internet-connected-workstation) passaggio.</span><span class="sxs-lookup"><span data-stu-id="7d959-359">You retrieved this value previously, in **Step 1.2: Get your Azure subscription ID** from hello [Prepare your Internet-connected workstation](#step-1-prepare-your-internet-connected-workstation) step.</span></span>
* <span data-ttu-id="7d959-360">Sostituire *ContosoFirstHSMKey* con un'etichetta che viene usata per il nome del file di output.</span><span class="sxs-lookup"><span data-stu-id="7d959-360">Replace *ContosoFirstHSMKey* with a label that is used for your output file name.</span></span>

<span data-ttu-id="7d959-361">Quando viene completato correttamente, viene visualizzato **risultato: operazione riuscita** ed è presente un nuovo file nella cartella corrente hello con hello dopo il nome: KeyTransferPackage -*ContosoFirstHSMkey*byok</span><span class="sxs-lookup"><span data-stu-id="7d959-361">When this completes successfully, it displays **Result: SUCCESS** and there is a new file in hello current folder that has hello following name: KeyTransferPackage-*ContosoFirstHSMkey*.byok</span></span>

### <a name="step-43-copy-your-key-transfer-package-toohello-internet-connected-workstation"></a><span data-ttu-id="7d959-362">Passaggio 4.3: Copiare la workstation connessa a Internet di trasferimento della chiave pacchetto toohello</span><span class="sxs-lookup"><span data-stu-id="7d959-362">Step 4.3: Copy your key transfer package toohello Internet-connected workstation</span></span>
<span data-ttu-id="7d959-363">Utilizzare un'unità USB o un altro file di output di archiviazione portatile toocopy hello da hello precedente (KeyTransferPackage-ContosoFirstHSMkey.byok) passaggio tooyour workstation connessa a Internet.</span><span class="sxs-lookup"><span data-stu-id="7d959-363">Use a USB drive or other portable storage toocopy hello output file from hello previous step (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour Internet-connected workstation.</span></span>

## <a name="step-5-transfer-your-key-tooazure-key-vault"></a><span data-ttu-id="7d959-364">Passaggio 5: Trasferire la chiave tooAzure insieme di credenziali chiave</span><span class="sxs-lookup"><span data-stu-id="7d959-364">Step 5: Transfer your key tooAzure Key Vault</span></span>
<span data-ttu-id="7d959-365">Per il passaggio finale, utilizzare hello nella workstation connessa a Internet, hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet tooupload hello chiave pacchetto di trasferimento è stato copiato da hello disconnesso workstation toohello hardware dell'insieme di credenziali chiave di Azure:</span><span class="sxs-lookup"><span data-stu-id="7d959-365">For this final step, on hello Internet-connected workstation, use hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet tooupload hello key transfer package that you copied from hello disconnected workstation toohello Azure Key Vault HSM:</span></span>

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

<span data-ttu-id="7d959-366">Se il caricamento di hello ha esito positivo, viene visualizzato proprietà hello visualizzato della chiave di hello appena aggiunto.</span><span class="sxs-lookup"><span data-stu-id="7d959-366">If hello upload is successful, you see displayed hello properties of hello key that you just added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d959-367">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7d959-367">Next steps</span></span>
<span data-ttu-id="7d959-368">È ora possibile usare questa chiave HSM protetta nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="7d959-368">You can now use this HSM-protected key in your key vault.</span></span> <span data-ttu-id="7d959-369">Per ulteriori informazioni, vedere hello **se si desidera che un modulo di protezione hardware (HSM) toouse** sezione hello [introduzione insieme credenziali chiavi Azure](key-vault-get-started.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="7d959-369">For more information, see hello **If you want toouse a hardware security module (HSM)** section in hello [Getting started with Azure Key Vault](key-vault-get-started.md) tutorial.</span></span>
