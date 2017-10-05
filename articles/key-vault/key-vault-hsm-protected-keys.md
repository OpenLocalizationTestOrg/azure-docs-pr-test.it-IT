---
title: Come generare e trasferire chiavi protette dal modulo di protezione hardware per l'insieme di credenziali delle chiavi di Azure | Microsoft Docs
description: Questo argomento permette di pianificare, generare e quindi trasferire le proprie chiavi HSM protette da usare con l'insieme di credenziali delle chiavi di Azure. Anche noto come BYOK o Bring Your Own Key.
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
ms.openlocfilehash: 5dbee1221f64045c64fecb344de1e03b2183dfb1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-generate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a><span data-ttu-id="d2a02-104">Come generare e trasferire chiavi HSM protette per l'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="d2a02-104">How to generate and transfer HSM-protected keys for Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="d2a02-105">Introduzione</span><span class="sxs-lookup"><span data-stu-id="d2a02-105">Introduction</span></span>
<span data-ttu-id="d2a02-106">Per una maggiore sicurezza, quando si usa l'insieme di credenziali delle chiavi di Azure è possibile importare o generare le chiavi in moduli di protezione hardware (HSM) che rimangono sempre entro il limite HSM.</span><span class="sxs-lookup"><span data-stu-id="d2a02-106">For added assurance, when you use Azure Key Vault, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="d2a02-107">Questo scenario viene spesso definito con il termine modalità *Bring Your Own Key*o BYOK.</span><span class="sxs-lookup"><span data-stu-id="d2a02-107">This scenario is often referred to as *bring your own key*, or BYOK.</span></span> <span data-ttu-id="d2a02-108">I moduli di protezione hardware sono certificati per FIPS 140-2 livello 2.</span><span class="sxs-lookup"><span data-stu-id="d2a02-108">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="d2a02-109">L'insieme di credenziali delle chiavi di Azure usa la famiglia di HSM nShield di Thales per proteggere le chiavi.</span><span class="sxs-lookup"><span data-stu-id="d2a02-109">Azure Key Vault uses Thales nShield family of HSMs to protect your keys.</span></span>

<span data-ttu-id="d2a02-110">Questo argomento include informazioni utili per pianificare, generare e quindi trasferire le proprie chiavi protette da HSM da usare con l'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="d2a02-110">Use the information in this topic to help you plan for, generate, and then transfer your own HSM-protected keys to use with Azure Key Vault.</span></span>

<span data-ttu-id="d2a02-111">Questa funzionalità non è disponibile per la versione di Azure per la Cina.</span><span class="sxs-lookup"><span data-stu-id="d2a02-111">This functionality is not available for Azure China.</span></span>

> [!NOTE]
> <span data-ttu-id="d2a02-112">Per altre informazioni sull'insieme di credenziali di Azure, vedere [Cos'è l'insieme di credenziali delle chiavi di Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="d2a02-112">For more information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>  
>
> <span data-ttu-id="d2a02-113">Per un'esercitazione introduttiva che illustra la creazione di un insieme di credenziali delle chiavi per chiavi HSM protette, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d2a02-113">For a getting started tutorial, which includes creating a key vault for HSM-protected keys, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>
>
>

<span data-ttu-id="d2a02-114">Altre informazioni su generazione e trasferimento di una chiave HSM protetta tramite Internet:</span><span class="sxs-lookup"><span data-stu-id="d2a02-114">More information about generating and transferring an HSM-protected key over the Internet:</span></span>

* <span data-ttu-id="d2a02-115">La chiave viene generata in una workstation offline per ridurre la superficie di attacco.</span><span class="sxs-lookup"><span data-stu-id="d2a02-115">You generate the key from an offline workstation, which reduces the attack surface.</span></span>
* <span data-ttu-id="d2a02-116">La crittografia della chiave viene eseguita tramite una chiave per lo scambio delle chiavi che rimane crittografata fino al momento del trasferimento ai moduli di protezione hardware dell'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="d2a02-116">The key is encrypted with a Key Exchange Key (KEK), which stays encrypted until it is transferred to the Azure Key Vault HSMs.</span></span> <span data-ttu-id="d2a02-117">Solo la versione crittografata della chiave viene inviata dalla workstation originale.</span><span class="sxs-lookup"><span data-stu-id="d2a02-117">Only the encrypted version of your key leaves the original workstation.</span></span>
* <span data-ttu-id="d2a02-118">Il set di strumenti imposta proprietà sulla chiave che consentono di associarla all'ambiente di sicurezza dell'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="d2a02-118">The toolset sets properties on your tenant key that binds your key to the Azure Key Vault security world.</span></span> <span data-ttu-id="d2a02-119">Di conseguenza, dopo che i moduli di protezione hardware dell'insieme di credenziali delle chiavi di Azure avranno ricevuto e decrittografato la chiave, saranno gli unici componenti a poterla usare.</span><span class="sxs-lookup"><span data-stu-id="d2a02-119">So after the Azure Key Vault HSMs receive and decrypt your key, only these HSMs can use it.</span></span> <span data-ttu-id="d2a02-120">La chiave non può essere esportata.</span><span class="sxs-lookup"><span data-stu-id="d2a02-120">Your key cannot be exported.</span></span> <span data-ttu-id="d2a02-121">Questo binding viene applicato dai moduli di protezione hardware Thales.</span><span class="sxs-lookup"><span data-stu-id="d2a02-121">This binding is enforced by the Thales HSMs.</span></span>
* <span data-ttu-id="d2a02-122">La chiave per lo scambio delle chiavi usata per crittografare la chiave viene generata nei moduli di protezione hardware dell'insieme di credenziali delle chiavi di Azure e non è esportabile.</span><span class="sxs-lookup"><span data-stu-id="d2a02-122">The Key Exchange Key (KEK) that is used to encrypt your key is generated inside the Azure Key Vault HSMs and is not exportable.</span></span> <span data-ttu-id="d2a02-123">I moduli di protezione hardware applicano la regola in base alla quale non può esistere una versione non crittografata della chiave per lo scambio delle chiavi all'esterno dei moduli stessi.</span><span class="sxs-lookup"><span data-stu-id="d2a02-123">The HSMs enforce that there can be no clear version of the KEK outside the HSMs.</span></span> <span data-ttu-id="d2a02-124">Il set di strumenti include inoltre un'attestazione di Thales che dichiara che la chiave per lo scambio delle chiavi non è esportabile e che è stata generata in un modulo di protezione hardware originale prodotto da Thales.</span><span class="sxs-lookup"><span data-stu-id="d2a02-124">In addition, the toolset includes attestation from Thales that the KEK is not exportable and was generated inside a genuine HSM that was manufactured by Thales.</span></span>
* <span data-ttu-id="d2a02-125">Il set di strumenti include un'attestazione di Thales che dichiara che anche l'ambiente di sicurezza dell'insieme di credenziali delle chiavi di Azure è stato generato in un modulo di protezione hardware originale prodotto da Thales.</span><span class="sxs-lookup"><span data-stu-id="d2a02-125">The toolset includes attestation from Thales that the Azure Key Vault security world was also generated on a genuine HSM manufactured by Thales.</span></span> <span data-ttu-id="d2a02-126">Questo attestato conferma che Microsoft usa hardware originale.</span><span class="sxs-lookup"><span data-stu-id="d2a02-126">This attestation proves to you that Microsoft is using genuine hardware.</span></span>
* <span data-ttu-id="d2a02-127">Microsoft usa certificati KEK separati e ambienti di sicurezza separati in ogni area geografica.</span><span class="sxs-lookup"><span data-stu-id="d2a02-127">Microsoft uses separate KEKs and separate Security Worlds in each geographical region.</span></span> <span data-ttu-id="d2a02-128">Questa separazione assicura che la chiave possa essere usata solo nei data center appartenenti all'area in cui è stata crittografata.</span><span class="sxs-lookup"><span data-stu-id="d2a02-128">This separation ensures that your key can be used only in data centers in the region in which you encrypted it.</span></span> <span data-ttu-id="d2a02-129">Una chiave di un cliente europeo, ad esempio, non può essere usata in data center che si trovano in America del Nord o in Asia.</span><span class="sxs-lookup"><span data-stu-id="d2a02-129">For example, a key from a European customer cannot be used in data centers in North American or Asia.</span></span>

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a><span data-ttu-id="d2a02-130">Altre informazioni sui moduli di protezione hardware di Thales e sui servizi di Microsoft</span><span class="sxs-lookup"><span data-stu-id="d2a02-130">More information about Thales HSMs and Microsoft services</span></span>
<span data-ttu-id="d2a02-131">Thales e-Security è un fornitore leader a livello mondiale di soluzioni di crittografia dei dati e di sicurezza informatica per i settori finanziario, tecnologico, manifatturiero e pubblico.</span><span class="sxs-lookup"><span data-stu-id="d2a02-131">Thales e-Security is a leading global provider of data encryption and cyber security solutions to the financial services, high technology, manufacturing, government, and technology sectors.</span></span> <span data-ttu-id="d2a02-132">Basate su un'esperienza di 40 anni nella protezione di informazioni aziendali e degli enti pubblici, le soluzioni Thales vengono usate da quattro delle cinque maggiori società dei settori energetico e aerospaziale,</span><span class="sxs-lookup"><span data-stu-id="d2a02-132">With a 40-year track record of protecting corporate and government information, Thales solutions are used by four of the five largest energy and aerospace companies.</span></span> <span data-ttu-id="d2a02-133">in 22 paesi NATO, e consentono di proteggere più dell'80 percento delle transazioni di pagamento in tutto il mondo.</span><span class="sxs-lookup"><span data-stu-id="d2a02-133">Their solutions are also used by 22 NATO countries, and secure more than 80 per cent of worldwide payment transactions.</span></span>

<span data-ttu-id="d2a02-134">Microsoft ha collaborato con Thales per migliorare il livello tecnologico dei moduli di protezione hardware</span><span class="sxs-lookup"><span data-stu-id="d2a02-134">Microsoft has collaborated with Thales to enhance the state of art for HSMs.</span></span> <span data-ttu-id="d2a02-135">per consentire all'utente di sfruttare i vantaggi tipici dei servizi ospitati senza perdere il controllo sulle proprie chiavi.</span><span class="sxs-lookup"><span data-stu-id="d2a02-135">These enhancements enable you to get the typical benefits of hosted services without relinquishing control over your keys.</span></span> <span data-ttu-id="d2a02-136">In particolare, tali miglioramenti consentono a Microsoft di gestire i moduli di protezione hardware in modo che questa operazione non debba essere eseguita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="d2a02-136">Specifically, these enhancements let Microsoft manage the HSMs so that you do not have to.</span></span> <span data-ttu-id="d2a02-137">In quanto servizio cloud, l'insieme di credenziali delle chiavi di Azure è in grado di supportare la scalabilità verticale con breve preavviso per soddisfare i picchi d'uso dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="d2a02-137">As a cloud service, Azure Key Vault scales up at short notice to meet your organization’s usage spikes.</span></span> <span data-ttu-id="d2a02-138">Contemporaneamente, la chiave è protetta all'interno dei moduli di protezione hardware di Microsoft e l'utente mantiene il controllo sul ciclo di vita della chiave, perché genera la chiave e la trasferisce ai moduli di protezione hardware di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d2a02-138">At the same time, your key is protected inside Microsoft’s HSMs: You retain control over the key lifecycle because you generate the key and transfer it to Microsoft’s HSMs.</span></span>

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a><span data-ttu-id="d2a02-139">Implementazione di BYOK (Bring Your Own Key) per l'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="d2a02-139">Implementing bring your own key (BYOK) for Azure Key Vault</span></span>
<span data-ttu-id="d2a02-140">Usare le informazioni e le procedure seguenti se si genera una chiave HSM protetta e quindi la si trasferisce all'insieme di credenziali delle chiavi di Azure, ovvero lo scenario BYOK (Bring Your Own Key).</span><span class="sxs-lookup"><span data-stu-id="d2a02-140">Use the following information and procedures if you will generate your own HSM-protected key and then transfer it to Azure Key Vault—the bring your own key (BYOK) scenario.</span></span>

## <a name="prerequisites-for-byok"></a><span data-ttu-id="d2a02-141">Prerequisiti per la modalità BYOK</span><span class="sxs-lookup"><span data-stu-id="d2a02-141">Prerequisites for BYOK</span></span>
<span data-ttu-id="d2a02-142">Nella tabella seguente sono elencati i prerequisiti relativi alla modalità BYOK per l'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="d2a02-142">See the following table for a list of prerequisites for bring your own key (BYOK) for Azure Key Vault.</span></span>

| <span data-ttu-id="d2a02-143">Requisito</span><span class="sxs-lookup"><span data-stu-id="d2a02-143">Requirement</span></span> | <span data-ttu-id="d2a02-144">Altre informazioni</span><span class="sxs-lookup"><span data-stu-id="d2a02-144">More information</span></span> |
| --- | --- |
| <span data-ttu-id="d2a02-145">Sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="d2a02-145">A subscription to Azure</span></span> |<span data-ttu-id="d2a02-146">Per creare un insieme di credenziali delle chiavi di Azure, è necessaria una sottoscrizione di Azure: [Iscriversi per una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="d2a02-146">To create an Azure Key Vault, you need an Azure subscription: [Sign up for free trial](https://azure.microsoft.com/pricing/free-trial/)</span></span> |
| <span data-ttu-id="d2a02-147">È inoltre necessario il livello di servizio Premium dell'insieme di credenziali delle chiavi di Azure per supportare chiavi HSM protette.</span><span class="sxs-lookup"><span data-stu-id="d2a02-147">The Azure Key Vault Premium service tier to support HSM-protected keys</span></span> |<span data-ttu-id="d2a02-148">Per altre informazioni su livelli di servizio e funzionalità per l'insieme di credenziali delle chiavi di Azure, vedere il sito Web relativo ai [prezzi dell'insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/pricing/details/key-vault/) .</span><span class="sxs-lookup"><span data-stu-id="d2a02-148">For more information about the service tiers and capabilities for Azure Key Vault, see the [Azure Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/) website.</span></span> |
| <span data-ttu-id="d2a02-149">Moduli di protezione hardware Thales, smart card e software di supporto</span><span class="sxs-lookup"><span data-stu-id="d2a02-149">Thales HSM, smartcards, and support software</span></span> |<span data-ttu-id="d2a02-150">È necessario avere l'accesso ai moduli di protezione hardware Thales e averne una conoscenza a livello operativo.</span><span class="sxs-lookup"><span data-stu-id="d2a02-150">You must have access to a Thales Hardware Security Module and basic operational knowledge of Thales HSMs.</span></span> <span data-ttu-id="d2a02-151">Per l'elenco dei modelli compatibili o per acquistare un modulo di protezione hardware qualora non se ne sia già in possesso, vedere la pagina relativa ai [moduli di protezione hardware Thales](https://www.thales-esecurity.com/msrms/buy) .</span><span class="sxs-lookup"><span data-stu-id="d2a02-151">See [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) for the list of compatible models, or to purchase an HSM if you do not have one.</span></span> |
| <span data-ttu-id="d2a02-152">Componenti hardware e software seguenti:</span><span class="sxs-lookup"><span data-stu-id="d2a02-152">The following hardware and software:</span></span><ol><li><span data-ttu-id="d2a02-153">Una workstation x64 offline con Windows 7 come versione minima del sistema operativo Windows e software Thales nShield con versione minima 11.50.</span><span class="sxs-lookup"><span data-stu-id="d2a02-153">An offline x64 workstation with a minimum Windows operation system of Windows 7 and Thales nShield software that is at least version 11.50.</span></span><br/><br/><span data-ttu-id="d2a02-154">Se questa workstation esegue Windows 7, è necessario [installare Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span><span class="sxs-lookup"><span data-stu-id="d2a02-154">If this workstation runs Windows 7, you must [install Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span></span></li><li><span data-ttu-id="d2a02-155">Una workstation connessa a Internet con sistema operativo Windows 7 o versione successiva e con [Azure PowerShell](/powershell/azure/overview) **1.1.0** o versione successiva installato.</span><span class="sxs-lookup"><span data-stu-id="d2a02-155">A workstation that is connected to the Internet and has a minimum Windows operating system of Windows 7 and [Azure PowerShell](/powershell/azure/overview) **minimum version 1.1.0** installed.</span></span></li><li><span data-ttu-id="d2a02-156">Unità USB o un altro dispositivo di archiviazione portatile con almeno 16 MB di spazio disponibile.</span><span class="sxs-lookup"><span data-stu-id="d2a02-156">A USB drive or other portable storage device that has at least 16 MB free space.</span></span></li></ol> |<span data-ttu-id="d2a02-157">Per motivi di sicurezza, si consiglia che la prima workstation non sia connessa a una rete.</span><span class="sxs-lookup"><span data-stu-id="d2a02-157">For security reasons, we recommend that the first workstation is not connected to a network.</span></span> <span data-ttu-id="d2a02-158">Questa indicazione tuttavia non viene applicata a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="d2a02-158">However, this recommendation is not programmatically enforced.</span></span><br/><br/><span data-ttu-id="d2a02-159">Si noti che nelle istruzioni seguenti questa workstation viene indicata come workstation disconnessa.</span><span class="sxs-lookup"><span data-stu-id="d2a02-159">Note that in the instructions that follow, this workstation is referred to as the disconnected workstation.</span></span></p></blockquote><br/><span data-ttu-id="d2a02-160">Se inoltre la propria chiave del tenant è destinata a essere usata in una rete di produzione, si consiglia di usare una seconda workstation separata per scaricare il set di strumenti e caricare la chiave del tenant.</span><span class="sxs-lookup"><span data-stu-id="d2a02-160">In addition, if your tenant key is for a production network, we recommend that you use a second, separate workstation to download the toolset and upload the tenant key.</span></span> <span data-ttu-id="d2a02-161">A scopo di test è comunque possibile usare la prima workstation.</span><span class="sxs-lookup"><span data-stu-id="d2a02-161">But for testing purposes, you can use the same workstation as the first one.</span></span><br/><br/><span data-ttu-id="d2a02-162">Si noti che nelle istruzioni seguenti la seconda workstation viene indicata come workstation connessa a Internet.</span><span class="sxs-lookup"><span data-stu-id="d2a02-162">Note that in the instructions that follow, this second workstation is referred to as the Internet-connected workstation.</span></span></p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-to-azure-key-vault-hsm"></a><span data-ttu-id="d2a02-163">Generare e trasferire la chiave al modulo di protezione hardware dell'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="d2a02-163">Generate and transfer your key to Azure Key Vault HSM</span></span>
<span data-ttu-id="d2a02-164">Per generare e trasferire la chiave al modulo di protezione hardware dell'insieme di credenziali delle chiavi di Azure, eseguire i cinque passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d2a02-164">You will use the following five steps to generate and transfer your key to an Azure Key Vault HSM:</span></span>

* [<span data-ttu-id="d2a02-165">Passaggio 1: Preparare la workstation connessa a Internet</span><span class="sxs-lookup"><span data-stu-id="d2a02-165">Step 1: Prepare your Internet-connected workstation</span></span>](#step-1-prepare-your-internet-connected-workstation)
* [<span data-ttu-id="d2a02-166">Passaggio 2: Preparare la workstation disconnessa</span><span class="sxs-lookup"><span data-stu-id="d2a02-166">Step 2: Prepare your disconnected workstation</span></span>](#step-2-prepare-your-disconnected-workstation)
* [<span data-ttu-id="d2a02-167">Passaggio 3: Generare la chiave</span><span class="sxs-lookup"><span data-stu-id="d2a02-167">Step 3: Generate your key</span></span>](#step-3-generate-your-key)
* [<span data-ttu-id="d2a02-168">Passaggio 4: Preparare la chiave per il trasferimento</span><span class="sxs-lookup"><span data-stu-id="d2a02-168">Step 4: Prepare your key for transfer</span></span>](#step-4-prepare-your-key-for-transfer)
* [<span data-ttu-id="d2a02-169">Passaggio 5: Trasferire la chiave all'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="d2a02-169">Step 5: Transfer your key to Azure Key Vault</span></span>](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a><span data-ttu-id="d2a02-170">Passaggio 1: Preparare la workstation connessa a Internet</span><span class="sxs-lookup"><span data-stu-id="d2a02-170">Step 1: Prepare your Internet-connected workstation</span></span>
<span data-ttu-id="d2a02-171">Per questo primo passaggio è necessario eseguire le procedure seguenti nella workstation connessa a Internet.</span><span class="sxs-lookup"><span data-stu-id="d2a02-171">For this first step, do the following procedures on your workstation that is connected to the Internet.</span></span>

### <a name="step-11-install-azure-powershell"></a><span data-ttu-id="d2a02-172">Passaggio 1.1: Installare Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2a02-172">Step 1.1: Install Azure PowerShell</span></span>
<span data-ttu-id="d2a02-173">Dalla workstation connessa a Internet scaricare e installare il modulo di Azure PowerShell che include i cmdlet per la gestione dell'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="d2a02-173">From the Internet-connected workstation, download and install the Azure PowerShell module that includes the cmdlets to manage Azure Key Vault.</span></span> <span data-ttu-id="d2a02-174">È necessaria la versione minima 0.8.13.</span><span class="sxs-lookup"><span data-stu-id="d2a02-174">This requires a minimum version of 0.8.13.</span></span>

<span data-ttu-id="d2a02-175">Per le istruzioni di installazione, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d2a02-175">For installation instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="step-12-get-your-azure-subscription-id"></a><span data-ttu-id="d2a02-176">Passaggio 1.2: Ottenere l'ID sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="d2a02-176">Step 1.2: Get your Azure subscription ID</span></span>
<span data-ttu-id="d2a02-177">Avviare una sessione di Azure PowerShell e accedere al proprio account Azure con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d2a02-177">Start an Azure PowerShell session and sign in to your Azure account by using the following command:</span></span>

        Add-AzureAccount
<span data-ttu-id="d2a02-178">Nella finestra del browser a comparsa, immettere il nome utente e la password dell'account Azure.</span><span class="sxs-lookup"><span data-stu-id="d2a02-178">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="d2a02-179">Usare quindi il comando [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) :</span><span class="sxs-lookup"><span data-stu-id="d2a02-179">Then, use the [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) command:</span></span>

        Get-AzureSubscription
<span data-ttu-id="d2a02-180">Nell'output individuare l'ID della sottoscrizione che si userà per l'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="d2a02-180">From the output, locate the ID for the subscription you will use for Azure Key Vault.</span></span> <span data-ttu-id="d2a02-181">Questo ID sottoscrizione verrà usato in seguito.</span><span class="sxs-lookup"><span data-stu-id="d2a02-181">You will need this subscription ID later.</span></span>

<span data-ttu-id="d2a02-182">Non chiudere la finestra di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d2a02-182">Do not close the Azure PowerShell window.</span></span>

### <a name="step-13-download-the-byok-toolset-for-azure-key-vault"></a><span data-ttu-id="d2a02-183">Passaggio 1.3: Scaricare il set di strumenti BYOK per l'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="d2a02-183">Step 1.3: Download the BYOK toolset for Azure Key Vault</span></span>
<span data-ttu-id="d2a02-184">Accedere all'Area download Microsoft e [scaricare il set di strumenti BYOK per l'insieme di credenziali delle chiavi di Azure](http://www.microsoft.com/download/details.aspx?id=45345) per la propria area geografica o istanza di Azure.</span><span class="sxs-lookup"><span data-stu-id="d2a02-184">Go to the Microsoft Download Center and [download the Azure Key Vault BYOK toolset](http://www.microsoft.com/download/details.aspx?id=45345) for your geographic region or instance of Azure.</span></span> <span data-ttu-id="d2a02-185">Usare le informazioni seguenti per identificare il nome del pacchetto da scaricare e il relativo hash del pacchetto SHA-256:</span><span class="sxs-lookup"><span data-stu-id="d2a02-185">Use the following information to identify the package name to download and its corresponding SHA-256 package hash:</span></span>

- - -
<span data-ttu-id="d2a02-186">**Stati Uniti:**</span><span class="sxs-lookup"><span data-stu-id="d2a02-186">**United States:**</span></span>

<span data-ttu-id="d2a02-187">KeyVault-BYOK-Tools-UnitedStates.zip</span><span class="sxs-lookup"><span data-stu-id="d2a02-187">KeyVault-BYOK-Tools-UnitedStates.zip</span></span>

<span data-ttu-id="d2a02-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span><span class="sxs-lookup"><span data-stu-id="d2a02-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span></span>

- - -
<span data-ttu-id="d2a02-189">**Europa:**</span><span class="sxs-lookup"><span data-stu-id="d2a02-189">**Europe:**</span></span>

<span data-ttu-id="d2a02-190">KeyVault-BYOK-Tools-Europe.zip</span><span class="sxs-lookup"><span data-stu-id="d2a02-190">KeyVault-BYOK-Tools-Europe.zip</span></span>

<span data-ttu-id="d2a02-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span><span class="sxs-lookup"><span data-stu-id="d2a02-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span></span>

- - -
<span data-ttu-id="d2a02-192">**Asia:**</span><span class="sxs-lookup"><span data-stu-id="d2a02-192">**Asia:**</span></span>

<span data-ttu-id="d2a02-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span><span class="sxs-lookup"><span data-stu-id="d2a02-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span></span>

<span data-ttu-id="d2a02-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span><span class="sxs-lookup"><span data-stu-id="d2a02-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span></span>

- - -
<span data-ttu-id="d2a02-195">**America Latina:**</span><span class="sxs-lookup"><span data-stu-id="d2a02-195">**Latin America:**</span></span>

<span data-ttu-id="d2a02-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span><span class="sxs-lookup"><span data-stu-id="d2a02-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span></span>

<span data-ttu-id="d2a02-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span><span class="sxs-lookup"><span data-stu-id="d2a02-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span></span>

- - -
<span data-ttu-id="d2a02-198">**Giappone:**</span><span class="sxs-lookup"><span data-stu-id="d2a02-198">**Japan:**</span></span>

<span data-ttu-id="d2a02-199">KeyVault-BYOK-Tools-Japan.zip</span><span class="sxs-lookup"><span data-stu-id="d2a02-199">KeyVault-BYOK-Tools-Japan.zip</span></span>

<span data-ttu-id="d2a02-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span><span class="sxs-lookup"><span data-stu-id="d2a02-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span></span>

- - -
<span data-ttu-id="d2a02-201">**Corea:**</span><span class="sxs-lookup"><span data-stu-id="d2a02-201">**Korea:**</span></span>

<span data-ttu-id="d2a02-202">KeyVault-BYOK-strumenti-Korea.zip</span><span class="sxs-lookup"><span data-stu-id="d2a02-202">KeyVault-BYOK-Tools-Korea.zip</span></span>

<span data-ttu-id="d2a02-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span><span class="sxs-lookup"><span data-stu-id="d2a02-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span></span>

- - -
<span data-ttu-id="d2a02-204">**Australia:**</span><span class="sxs-lookup"><span data-stu-id="d2a02-204">**Australia:**</span></span>

<span data-ttu-id="d2a02-205">KeyVault-BYOK-Tools-Australia.zip</span><span class="sxs-lookup"><span data-stu-id="d2a02-205">KeyVault-BYOK-Tools-Australia.zip</span></span>

<span data-ttu-id="d2a02-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span><span class="sxs-lookup"><span data-stu-id="d2a02-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span></span>

- - -
[<span data-ttu-id="d2a02-207">**Azure per enti pubblici:**</span><span class="sxs-lookup"><span data-stu-id="d2a02-207">**Azure Government:**</span></span>](https://azure.microsoft.com/features/gov/)

<span data-ttu-id="d2a02-208">KeyVault-BYOK-Tools-USGovCloud.zip</span><span class="sxs-lookup"><span data-stu-id="d2a02-208">KeyVault-BYOK-Tools-USGovCloud.zip</span></span>

<span data-ttu-id="d2a02-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span><span class="sxs-lookup"><span data-stu-id="d2a02-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span></span>

- - -
<span data-ttu-id="d2a02-210">**Dipartimento della difesa del governo degli Stati Uniti:**</span><span class="sxs-lookup"><span data-stu-id="d2a02-210">**US Government DOD:**</span></span>

<span data-ttu-id="d2a02-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span><span class="sxs-lookup"><span data-stu-id="d2a02-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span></span>

<span data-ttu-id="d2a02-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span><span class="sxs-lookup"><span data-stu-id="d2a02-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span></span>

- - -
<span data-ttu-id="d2a02-213">**Canada:**</span><span class="sxs-lookup"><span data-stu-id="d2a02-213">**Canada:**</span></span>

<span data-ttu-id="d2a02-214">KeyVault-BYOK-Tools-Canada.zip</span><span class="sxs-lookup"><span data-stu-id="d2a02-214">KeyVault-BYOK-Tools-Canada.zip</span></span>

<span data-ttu-id="d2a02-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span><span class="sxs-lookup"><span data-stu-id="d2a02-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span></span>

- - -
<span data-ttu-id="d2a02-216">**Germania:**</span><span class="sxs-lookup"><span data-stu-id="d2a02-216">**Germany:**</span></span>

<span data-ttu-id="d2a02-217">KeyVault-BYOK-Tools-Germany.zip</span><span class="sxs-lookup"><span data-stu-id="d2a02-217">KeyVault-BYOK-Tools-Germany.zip</span></span>

<span data-ttu-id="d2a02-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span><span class="sxs-lookup"><span data-stu-id="d2a02-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span></span>

- - -
<span data-ttu-id="d2a02-219">**India:**</span><span class="sxs-lookup"><span data-stu-id="d2a02-219">**India:**</span></span>

<span data-ttu-id="d2a02-220">KeyVault-BYOK-Tools-India.zip</span><span class="sxs-lookup"><span data-stu-id="d2a02-220">KeyVault-BYOK-Tools-India.zip</span></span>

<span data-ttu-id="d2a02-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span><span class="sxs-lookup"><span data-stu-id="d2a02-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span></span>

- - -
<span data-ttu-id="d2a02-222">**Regno Unito:**</span><span class="sxs-lookup"><span data-stu-id="d2a02-222">**United Kingdom:**</span></span>

<span data-ttu-id="d2a02-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span><span class="sxs-lookup"><span data-stu-id="d2a02-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span></span>

<span data-ttu-id="d2a02-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span><span class="sxs-lookup"><span data-stu-id="d2a02-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span></span>

- - -

<span data-ttu-id="d2a02-225">Per convalidare l'integrità del set di strumenti BYOK scaricato, nella sessione di Azure PowerShell usare il cmdlet [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d2a02-225">To validate the integrity of your downloaded BYOK toolset, from your Azure PowerShell session, use the [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span></span>

    Get-FileHash KeyVault-BYOK-Tools-*.zip

<span data-ttu-id="d2a02-226">Il set di strumenti include gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d2a02-226">The toolset includes the following:</span></span>

* <span data-ttu-id="d2a02-227">Un pacchetto di chiavi per lo scambio di chiavi (KEK) con un nome che inizia con **BYOK-KEK-pkg-.**</span><span class="sxs-lookup"><span data-stu-id="d2a02-227">A Key Exchange Key (KEK) package that has a name beginning with **BYOK-KEK-pkg-.**</span></span>
* <span data-ttu-id="d2a02-228">Un pacchetto relativo all'ambiente di sicurezza con un nome che inizia con **BYOK-SecurityWorld-pkg-.**</span><span class="sxs-lookup"><span data-stu-id="d2a02-228">A Security World package that has a name beginning with **BYOK-SecurityWorld-pkg-.**</span></span>
* <span data-ttu-id="d2a02-229">Uno script python denominato **verifykeypackage.py.**</span><span class="sxs-lookup"><span data-stu-id="d2a02-229">A python script named **verifykeypackage.py.**</span></span>
* <span data-ttu-id="d2a02-230">File eseguibile dalla riga di comando denominato **KeyTransferRemote.exe** e DLL associate.</span><span class="sxs-lookup"><span data-stu-id="d2a02-230">A command-line executable file named **KeyTransferRemote.exe** and associated DLLs.</span></span>
* <span data-ttu-id="d2a02-231">Componente Visual C++ Redistributable Package denominato **vcredist_x64.exe.**</span><span class="sxs-lookup"><span data-stu-id="d2a02-231">A Visual C++ Redistributable Package, named **vcredist_x64.exe.**</span></span>

<span data-ttu-id="d2a02-232">Copiare il pacchetto in un'unità USB o in un altro dispositivo di archiviazione portatile.</span><span class="sxs-lookup"><span data-stu-id="d2a02-232">Copy the package to a USB drive or other portable storage.</span></span>

## <a name="step-2-prepare-your-disconnected-workstation"></a><span data-ttu-id="d2a02-233">Passaggio 2: Preparare la workstation disconnessa</span><span class="sxs-lookup"><span data-stu-id="d2a02-233">Step 2: Prepare your disconnected workstation</span></span>
<span data-ttu-id="d2a02-234">Per questo secondo passaggio eseguire le procedure seguenti nella workstation non connessa alla rete (Internet o la rete interna).</span><span class="sxs-lookup"><span data-stu-id="d2a02-234">For this second step, do the following procedures on the workstation that is not connected to a network (either the Internet or your internal network).</span></span>

### <a name="step-21-prepare-the-disconnected-workstation-with-thales-hsm"></a><span data-ttu-id="d2a02-235">Passaggio 2.1: Preparare la workstation disconnessa con il modulo di protezione hardware Thales</span><span class="sxs-lookup"><span data-stu-id="d2a02-235">Step 2.1: Prepare the disconnected workstation with Thales HSM</span></span>
<span data-ttu-id="d2a02-236">Installare il software di supporto nCipher (Thales) in un computer Windows, quindi collegare un modulo di protezione hardware Thales a tale computer.</span><span class="sxs-lookup"><span data-stu-id="d2a02-236">Install the nCipher (Thales) support software on a Windows computer, and then attach a Thales HSM to that computer.</span></span>

<span data-ttu-id="d2a02-237">Verificare che gli strumenti Thales si trovino nel percorso (**%nfast_home%\bin**).</span><span class="sxs-lookup"><span data-stu-id="d2a02-237">Ensure that the Thales tools are in your path (**%nfast_home%\bin**).</span></span> <span data-ttu-id="d2a02-238">Digitare ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d2a02-238">For example, type the following:</span></span>

        set PATH=%PATH%;"%nfast_home%\bin"

<span data-ttu-id="d2a02-239">Per altre informazioni, vedere il manuale dell'utente fornito con il modulo di protezione hardware Thales.</span><span class="sxs-lookup"><span data-stu-id="d2a02-239">For more information, see the user guide included with the Thales HSM.</span></span>

### <a name="step-22-install-the-byok-toolset-on-the-disconnected-workstation"></a><span data-ttu-id="d2a02-240">Passaggio 2.2: Installare il set di strumenti BYOK nella workstation disconnessa</span><span class="sxs-lookup"><span data-stu-id="d2a02-240">Step 2.2: Install the BYOK toolset on the disconnected workstation</span></span>
<span data-ttu-id="d2a02-241">Copiare il pacchetto del set di strumenti BYOK dall'unità USB o da un altro dispositivo di archiviazione portatile, quindi eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d2a02-241">Copy the BYOK toolset package from the USB drive or other portable storage, and then do the following:</span></span>

1. <span data-ttu-id="d2a02-242">Estrarre i file dal pacchetto scaricato in una cartella qualsiasi.</span><span class="sxs-lookup"><span data-stu-id="d2a02-242">Extract the files from the downloaded package into any folder.</span></span>
2. <span data-ttu-id="d2a02-243">In tale cartella eseguire vcredist_x64.exe.</span><span class="sxs-lookup"><span data-stu-id="d2a02-243">From that folder, run vcredist_x64.exe.</span></span>
3. <span data-ttu-id="d2a02-244">Seguire le istruzioni per installare i componenti di runtime di Visual C++ per Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="d2a02-244">Follow the instructions to the install the Visual C++ runtime components for Visual Studio 2013.</span></span>

## <a name="step-3-generate-your-key"></a><span data-ttu-id="d2a02-245">Passaggio 3: Generare la chiave</span><span class="sxs-lookup"><span data-stu-id="d2a02-245">Step 3: Generate your key</span></span>
<span data-ttu-id="d2a02-246">Per questo terzo passaggio eseguire le procedure seguenti nella workstation disconnessa.</span><span class="sxs-lookup"><span data-stu-id="d2a02-246">For this third step, do the following procedures on the disconnected workstation.</span></span> <span data-ttu-id="d2a02-247">Per poter completare questo passaggio, il modulo di protezione hardware deve essere in modalità di inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="d2a02-247">To complete this step your HSM must be in initialization mode.</span></span> 


### <a name="step-31-change-the-hsm-mode-to-i"></a><span data-ttu-id="d2a02-248">Passaggio 3.1: Modificare la modalità del modulo di protezione hardware in 'I'</span><span class="sxs-lookup"><span data-stu-id="d2a02-248">Step 3.1: Change the HSM mode to 'I'</span></span>
<span data-ttu-id="d2a02-249">Se si usa Thales nShield Edge, per modificare la modalità: 1.</span><span class="sxs-lookup"><span data-stu-id="d2a02-249">If you are using Thales nShield Edge, to change the mode: 1.</span></span> <span data-ttu-id="d2a02-250">Usare il pulsante Modalità per evidenziare la modalità richiesta.</span><span class="sxs-lookup"><span data-stu-id="d2a02-250">Use the Mode button to highlight the required mode.</span></span> <span data-ttu-id="d2a02-251">2.</span><span class="sxs-lookup"><span data-stu-id="d2a02-251">2.</span></span> <span data-ttu-id="d2a02-252">Entro pochi secondi, premere e tenere premuto per pochi secondi il pulsante Cancella.</span><span class="sxs-lookup"><span data-stu-id="d2a02-252">Within a few seconds, press and hold the Clear button for a couple of seconds.</span></span> <span data-ttu-id="d2a02-253">Se la modalità viene modificata, il LED della nuova modalità smette di lampeggiare e rimane acceso.</span><span class="sxs-lookup"><span data-stu-id="d2a02-253">If the mode changes, the new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="d2a02-254">È possibile che il LED di stato lampeggi in modo irregolare per pochi secondi e quindi lampeggi in modo regolare quando il dispositivo è pronto.</span><span class="sxs-lookup"><span data-stu-id="d2a02-254">The Status LED might flash irregularly for a few seconds and then flashes regularly when the device is ready.</span></span> <span data-ttu-id="d2a02-255">In caso contrario, il dispositivo rimane nella modalità corrente, con il LED della modalità appropriata acceso.</span><span class="sxs-lookup"><span data-stu-id="d2a02-255">Otherwise, the device remains in the current mode, with the appropriate mode LED lit.</span></span>

### <a name="step-32-create-a-security-world"></a><span data-ttu-id="d2a02-256">Passaggio 3.2: Creare un ambiente di sicurezza</span><span class="sxs-lookup"><span data-stu-id="d2a02-256">Step 3.2: Create a security world</span></span>
<span data-ttu-id="d2a02-257">Avviare un prompt dei comandi ed eseguire il programma new-world di Thales.</span><span class="sxs-lookup"><span data-stu-id="d2a02-257">Start a command prompt and run the Thales new-world program.</span></span>

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

<span data-ttu-id="d2a02-258">Questo programma crea un file di **ambiente di sicurezza** nel percorso %NFAST_KMDATA%\local\world, che corrisponde alla cartella C:\ProgramData\nCipher\Key Management Data\local.</span><span class="sxs-lookup"><span data-stu-id="d2a02-258">This program creates a **Security World** file at %NFAST_KMDATA%\local\world, which corresponds to the C:\ProgramData\nCipher\Key Management Data\local folder.</span></span> <span data-ttu-id="d2a02-259">È possibile creare valori diversi per il quorum, ma nell'esempio viene chiesto di immettere tre schede vuote e un codice PIN per ogni scheda.</span><span class="sxs-lookup"><span data-stu-id="d2a02-259">You can use different values for the quorum but in our example, you’re prompted to enter three blank cards and pins for each one.</span></span> <span data-ttu-id="d2a02-260">Qualsiasi coppia di schede consente di accedere in modo completo all'ambiente di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d2a02-260">Then, any two cards give full access to the security world.</span></span> <span data-ttu-id="d2a02-261">Queste schede diventano il **set di schede amministrative** per il nuovo ambiente di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d2a02-261">These cards become the **Administrator Card Set** for the new security world.</span></span>

<span data-ttu-id="d2a02-262">Eseguire quindi le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d2a02-262">Then do the following:</span></span>

* <span data-ttu-id="d2a02-263">Eseguire il backup del file relativo all'ambiente.</span><span class="sxs-lookup"><span data-stu-id="d2a02-263">Back up the world file.</span></span> <span data-ttu-id="d2a02-264">Proteggere il file relativo all'ambiente, le schede amministrative e i codici PIN relativi e verificare che nessuna singola persona possa accedere a più di una scheda.</span><span class="sxs-lookup"><span data-stu-id="d2a02-264">Secure and protect the world file, the Administrator Cards, and their pins, and make sure that no single person has access to more than one card.</span></span>

### <a name="step-33-change-the-hsm-mode-to-o"></a><span data-ttu-id="d2a02-265">Passaggio 3.3: Modificare la modalità del modulo di protezione hardware in 'O'</span><span class="sxs-lookup"><span data-stu-id="d2a02-265">Step 3.3: Change the HSM mode to 'O'</span></span>
<span data-ttu-id="d2a02-266">Se si usa Thales nShield Edge, per modificare la modalità: 1.</span><span class="sxs-lookup"><span data-stu-id="d2a02-266">If you are using Thales nShield Edge, to change the mode: 1.</span></span> <span data-ttu-id="d2a02-267">Usare il pulsante Modalità per evidenziare la modalità richiesta.</span><span class="sxs-lookup"><span data-stu-id="d2a02-267">Use the Mode button to highlight the required mode.</span></span> <span data-ttu-id="d2a02-268">2.</span><span class="sxs-lookup"><span data-stu-id="d2a02-268">2.</span></span> <span data-ttu-id="d2a02-269">Entro pochi secondi, premere e tenere premuto per pochi secondi il pulsante Cancella.</span><span class="sxs-lookup"><span data-stu-id="d2a02-269">Within a few seconds, press and hold the Clear button for a couple of seconds.</span></span> <span data-ttu-id="d2a02-270">Se la modalità viene modificata, il LED della nuova modalità smette di lampeggiare e rimane acceso.</span><span class="sxs-lookup"><span data-stu-id="d2a02-270">If the mode changes, the new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="d2a02-271">È possibile che il LED di stato lampeggi in modo irregolare per pochi secondi e quindi lampeggi in modo regolare quando il dispositivo è pronto.</span><span class="sxs-lookup"><span data-stu-id="d2a02-271">The Status LED might flash irregularly for a few seconds and then flashes regularly when the device is ready.</span></span> <span data-ttu-id="d2a02-272">In caso contrario, il dispositivo rimane nella modalità corrente, con il LED della modalità appropriata acceso.</span><span class="sxs-lookup"><span data-stu-id="d2a02-272">Otherwise, the device remains in the current mode, with the appropriate mode LED lit.</span></span>


### <a name="step-34-validate-the-downloaded-package"></a><span data-ttu-id="d2a02-273">Passaggio 3.4: Convalidare il pacchetto scaricato</span><span class="sxs-lookup"><span data-stu-id="d2a02-273">Step 3.4: Validate the downloaded package</span></span>
<span data-ttu-id="d2a02-274">Questo passaggio è facoltativo, ma è consigliato in modo che sia possibile convalidare gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d2a02-274">This step is optional but recommended so that you can validate the following:</span></span>

* <span data-ttu-id="d2a02-275">Chiave per lo scambio delle chiavi inclusa nel set di strumenti generato da un modulo di protezione hardware Thales originale.</span><span class="sxs-lookup"><span data-stu-id="d2a02-275">The Key Exchange Key that is included in the toolset has been generated from a genuine Thales HSM.</span></span>
* <span data-ttu-id="d2a02-276">Hash dell'ambiente di sicurezza incluso nel set di strumenti generato da un modulo di protezione hardware Thales originale.</span><span class="sxs-lookup"><span data-stu-id="d2a02-276">The hash of the Security World that is included in the toolset has been generated in a genuine Thales HSM.</span></span>
* <span data-ttu-id="d2a02-277">Impossibilità di esportare la chiave per lo scambio delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="d2a02-277">The Key Exchange Key is non-exportable.</span></span>

> [!NOTE]
> <span data-ttu-id="d2a02-278">Per convalidare il pacchetto scaricato, il modulo di protezione hardware deve essere connesso e acceso e deve essere associato a un ambiente di sicurezza (ad esempio quello appena creato).</span><span class="sxs-lookup"><span data-stu-id="d2a02-278">To validate the downloaded package, the HSM must be connected, powered on, and must have a security world on it (such as the one you’ve just created).</span></span>
>
>

<span data-ttu-id="d2a02-279">Per convalidare il pacchetto scaricato:</span><span class="sxs-lookup"><span data-stu-id="d2a02-279">To validate the downloaded package:</span></span>

1. <span data-ttu-id="d2a02-280">Eseguire lo script verifykeypackage.py associando uno dei comandi seguenti, a seconda dell'area geografica o istanza di Azure:</span><span class="sxs-lookup"><span data-stu-id="d2a02-280">Run the verifykeypackage.py script by typing one of the following, depending on your geographic region or instance of Azure:</span></span>

   * <span data-ttu-id="d2a02-281">America del Nord</span><span class="sxs-lookup"><span data-stu-id="d2a02-281">For North America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * <span data-ttu-id="d2a02-282">Europa</span><span class="sxs-lookup"><span data-stu-id="d2a02-282">For Europe:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * <span data-ttu-id="d2a02-283">Asia</span><span class="sxs-lookup"><span data-stu-id="d2a02-283">For Asia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * <span data-ttu-id="d2a02-284">America Latina</span><span class="sxs-lookup"><span data-stu-id="d2a02-284">For Latin America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * <span data-ttu-id="d2a02-285">Giappone</span><span class="sxs-lookup"><span data-stu-id="d2a02-285">For Japan:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * <span data-ttu-id="d2a02-286">Per la Corea:</span><span class="sxs-lookup"><span data-stu-id="d2a02-286">For Korea:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * <span data-ttu-id="d2a02-287">Per l'Australia:</span><span class="sxs-lookup"><span data-stu-id="d2a02-287">For Australia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * <span data-ttu-id="d2a02-288">Per [Azure per enti pubblici](https://azure.microsoft.com/features/gov/), che usa l'istanza di Azure per il Governo degli Stati Uniti:</span><span class="sxs-lookup"><span data-stu-id="d2a02-288">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * <span data-ttu-id="d2a02-289">Per il Dipartimento della difesa del governo degli Stati Uniti:</span><span class="sxs-lookup"><span data-stu-id="d2a02-289">For US Government DOD:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * <span data-ttu-id="d2a02-290">Per il Canada:</span><span class="sxs-lookup"><span data-stu-id="d2a02-290">For Canada:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * <span data-ttu-id="d2a02-291">Per la Germania:</span><span class="sxs-lookup"><span data-stu-id="d2a02-291">For Germany:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * <span data-ttu-id="d2a02-292">Per l'India:</span><span class="sxs-lookup"><span data-stu-id="d2a02-292">For India:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > <span data-ttu-id="d2a02-293">Il software Thales include python nel percorso %NFAST_HOME%\python\bin.</span><span class="sxs-lookup"><span data-stu-id="d2a02-293">The Thales software includes python at %NFAST_HOME%\python\bin</span></span>
     >
     >
2. <span data-ttu-id="d2a02-294">Assicurarsi di visualizzare il risultato positivo seguente, che indica il completamento della convalida: **Result: SUCCESS**</span><span class="sxs-lookup"><span data-stu-id="d2a02-294">Confirm that you see the following, which indicates successful validation: **Result: SUCCESS**</span></span>

<span data-ttu-id="d2a02-295">Questo script consente di convalidare la catena di firmatari fino alla chiave radice di Thales.</span><span class="sxs-lookup"><span data-stu-id="d2a02-295">This script validates the signer chain up to the Thales root key.</span></span> <span data-ttu-id="d2a02-296">La funzione hash di questa chiave radice è incorporata nello script e il relativo valore deve essere **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span><span class="sxs-lookup"><span data-stu-id="d2a02-296">The hash of this root key is embedded in the script and its value should be **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span></span> <span data-ttu-id="d2a02-297">Si può anche confermare questo valore separatamente sul [sito Web di Thales](http://www.thalesesec.com/).</span><span class="sxs-lookup"><span data-stu-id="d2a02-297">You can also confirm this value separately by visiting the [Thales website](http://www.thalesesec.com/).</span></span>

<span data-ttu-id="d2a02-298">È ora possibile creare una nuova chiave.</span><span class="sxs-lookup"><span data-stu-id="d2a02-298">You’re now ready to create a new key.</span></span>

### <a name="step-35-create-a-new-key"></a><span data-ttu-id="d2a02-299">Passaggio 3.5: Creare una nuova chiave</span><span class="sxs-lookup"><span data-stu-id="d2a02-299">Step 3.5: Create a new key</span></span>
<span data-ttu-id="d2a02-300">Generare una chiave tramite il programma **generatekey** di Thales.</span><span class="sxs-lookup"><span data-stu-id="d2a02-300">Generate a key by using the Thales **generatekey** program.</span></span>

<span data-ttu-id="d2a02-301">Eseguire il comando seguente per generare la chiave:</span><span class="sxs-lookup"><span data-stu-id="d2a02-301">Run the following command to generate the key:</span></span>

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

<span data-ttu-id="d2a02-302">Quando si esegue il comando, usare le istruzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d2a02-302">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="d2a02-303">Il parametro *protect* deve essere impostato sul valore **module**, come illustrato.</span><span class="sxs-lookup"><span data-stu-id="d2a02-303">The parameter *protect* must be set to the value **module**, as shown.</span></span> <span data-ttu-id="d2a02-304">Verrà creata una chiave protetta tramite modulo.</span><span class="sxs-lookup"><span data-stu-id="d2a02-304">This creates a module-protected key.</span></span> <span data-ttu-id="d2a02-305">Il set di strumenti BYOK non supporta le chiavi protette con OCS.</span><span class="sxs-lookup"><span data-stu-id="d2a02-305">The BYOK toolset does not support OCS-protected keys.</span></span>
* <span data-ttu-id="d2a02-306">Sostituire il valore di *contosokey* per gli elementi **ident** e **plainname** con qualsiasi valore di stringa.</span><span class="sxs-lookup"><span data-stu-id="d2a02-306">Replace the value of *contosokey* for the **ident** and **plainname** with any string value.</span></span> <span data-ttu-id="d2a02-307">Per ridurre il sovraccarico amministrativo e il rischio di errori, è consigliabile usare lo stesso valore per entrambi gli elementi.</span><span class="sxs-lookup"><span data-stu-id="d2a02-307">To minimize administrative overheads and reduce the risk of errors, we recommend that you use the same value for both.</span></span> <span data-ttu-id="d2a02-308">Il valore **ident** deve contenere solo numeri, trattini e lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="d2a02-308">The **ident** value must contain only numbers, dashes, and lower case letters.</span></span>
* <span data-ttu-id="d2a02-309">L'elemento pubexp viene lasciato vuoto in questo esempio (impostazione predefinita), ma è possibile indicare valori specifici.</span><span class="sxs-lookup"><span data-stu-id="d2a02-309">The pubexp is left blank (default) in this example, but you can specify specific values.</span></span> <span data-ttu-id="d2a02-310">Per altre informazioni, vedere la documentazione di Thales.</span><span class="sxs-lookup"><span data-stu-id="d2a02-310">For more information, see the Thales documentation.</span></span>

<span data-ttu-id="d2a02-311">Questo comando crea un file di chiave in formato token nella cartella %NFAST_KMDATA%\local con un nome che inizia con **key_simple_** seguito dall'elemento **ident** specificato nel comando.</span><span class="sxs-lookup"><span data-stu-id="d2a02-311">This command creates a Tokenized Key file in your %NFAST_KMDATA%\local folder with a name starting with **key_simple_**, followed by the **ident** that was specified in the command.</span></span> <span data-ttu-id="d2a02-312">Ad esempio: **key_simple_contosokey**.</span><span class="sxs-lookup"><span data-stu-id="d2a02-312">For example: **key_simple_contosokey**.</span></span> <span data-ttu-id="d2a02-313">Questo file contiene una chiave crittografata.</span><span class="sxs-lookup"><span data-stu-id="d2a02-313">This file contains an encrypted key.</span></span>

<span data-ttu-id="d2a02-314">Eseguire il backup del file di chiave in formato token in un percorso sicuro.</span><span class="sxs-lookup"><span data-stu-id="d2a02-314">Back up this Tokenized Key File in a safe location.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d2a02-315">Quando in seguito si trasferisce la chiave all'insieme di credenziali delle chiavi di Azure, Microsoft non può esportarla nuovamente nei dispositivi dell'utente, quindi è estremamente importante eseguire il backup della chiave e dell'ambiente di sicurezza in modo sicuro.</span><span class="sxs-lookup"><span data-stu-id="d2a02-315">When you later transfer your key to Azure Key Vault, Microsoft cannot export this key back to you so it becomes extremely important that you back up your key and security world safely.</span></span> <span data-ttu-id="d2a02-316">Per ottenere informazioni aggiuntive e procedure consigliate per eseguire il backup della chiave, contattare Thales.</span><span class="sxs-lookup"><span data-stu-id="d2a02-316">Contact Thales for guidance and best practices for backing up your key.</span></span>
>
>

<span data-ttu-id="d2a02-317">È ora possibile trasferire la chiave all'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="d2a02-317">You are now ready to transfer your key to Azure Key Vault.</span></span>

## <a name="step-4-prepare-your-key-for-transfer"></a><span data-ttu-id="d2a02-318">Passaggio 4: Preparare la chiave per il trasferimento</span><span class="sxs-lookup"><span data-stu-id="d2a02-318">Step 4: Prepare your key for transfer</span></span>
<span data-ttu-id="d2a02-319">Per questo quarto passaggio eseguire le procedure seguenti nella workstation disconnessa.</span><span class="sxs-lookup"><span data-stu-id="d2a02-319">For this fourth step, do the following procedures on the disconnected workstation.</span></span>

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a><span data-ttu-id="d2a02-320">Passaggio 4.1: Creare una copia della chiave con autorizzazioni ridotte</span><span class="sxs-lookup"><span data-stu-id="d2a02-320">Step 4.1: Create a copy of your key with reduced permissions</span></span>

<span data-ttu-id="d2a02-321">Aprire un nuovo prompt dei comandi e passare alla directory in cui è stato decompresso il file ZIP BYOK.</span><span class="sxs-lookup"><span data-stu-id="d2a02-321">Open a new command prompt and change the current directory to the location where you unzipped the BYOK zip file.</span></span> <span data-ttu-id="d2a02-322">Per ridurre le autorizzazioni sulla chiave, in un prompt dei comandi eseguire uno dei comandi seguenti in base all'area geografica o all'istanza di Azure:</span><span class="sxs-lookup"><span data-stu-id="d2a02-322">To reduce the permissions on your key, from a command prompt, run one of the following, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="d2a02-323">America del Nord</span><span class="sxs-lookup"><span data-stu-id="d2a02-323">For North America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* <span data-ttu-id="d2a02-324">Europa</span><span class="sxs-lookup"><span data-stu-id="d2a02-324">For Europe:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* <span data-ttu-id="d2a02-325">Asia</span><span class="sxs-lookup"><span data-stu-id="d2a02-325">For Asia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* <span data-ttu-id="d2a02-326">America Latina</span><span class="sxs-lookup"><span data-stu-id="d2a02-326">For Latin America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* <span data-ttu-id="d2a02-327">Giappone</span><span class="sxs-lookup"><span data-stu-id="d2a02-327">For Japan:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* <span data-ttu-id="d2a02-328">Per la Corea:</span><span class="sxs-lookup"><span data-stu-id="d2a02-328">For Korea:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* <span data-ttu-id="d2a02-329">Per l'Australia:</span><span class="sxs-lookup"><span data-stu-id="d2a02-329">For Australia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* <span data-ttu-id="d2a02-330">Per [Azure per enti pubblici](https://azure.microsoft.com/features/gov/), che usa l'istanza di Azure per il Governo degli Stati Uniti:</span><span class="sxs-lookup"><span data-stu-id="d2a02-330">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* <span data-ttu-id="d2a02-331">Per il Dipartimento della difesa del governo degli Stati Uniti:</span><span class="sxs-lookup"><span data-stu-id="d2a02-331">For US Government DOD:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* <span data-ttu-id="d2a02-332">Per il Canada:</span><span class="sxs-lookup"><span data-stu-id="d2a02-332">For Canada:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* <span data-ttu-id="d2a02-333">Per la Germania:</span><span class="sxs-lookup"><span data-stu-id="d2a02-333">For Germany:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* <span data-ttu-id="d2a02-334">Per l'India:</span><span class="sxs-lookup"><span data-stu-id="d2a02-334">For India:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

<span data-ttu-id="d2a02-335">Quando si esegue il comando, sostituire *contosokey* con lo stesso valore specificato in **Passaggio 3.5: Creare una nuova chiave** nel passaggio [Generare la chiave](#step-3-generate-your-key).</span><span class="sxs-lookup"><span data-stu-id="d2a02-335">When you run this command, replace *contosokey* with the same value you specified in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>

<span data-ttu-id="d2a02-336">Viene chiesto di inserire le schede amministrative relative all'ambiente di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d2a02-336">You are asked to plug in your security world admin cards.</span></span>

<span data-ttu-id="d2a02-337">Al completamento del comando, viene visualizzato il messaggio **Result: SUCCESS** e la copia della chiave con autorizzazioni ridotte si trova nel file denominato key_xferacId_<contosokey>.</span><span class="sxs-lookup"><span data-stu-id="d2a02-337">When the command completes, you see **Result: SUCCESS** and the copy of your key with reduced permissions are in the file named key_xferacId_<contosokey>.</span></span>

<span data-ttu-id="d2a02-338">È possibile ispezionare gli elenchi di controllo di accesso usando i comandi seguenti e le utilità Thales:</span><span class="sxs-lookup"><span data-stu-id="d2a02-338">You may inspects the ACLS using following commands using the Thales utilities:</span></span>

* <span data-ttu-id="d2a02-339">aclprint.py:</span><span class="sxs-lookup"><span data-stu-id="d2a02-339">aclprint.py:</span></span>

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* <span data-ttu-id="d2a02-340">kmfile-dump.exe:</span><span class="sxs-lookup"><span data-stu-id="d2a02-340">kmfile-dump.exe:</span></span>

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  <span data-ttu-id="d2a02-341">Quando si eseguono questi comandi, sostituire contosokey con lo stesso valore specificato in **Passaggio 3.5: Creare una nuova chiave** nel passaggio [Generare la chiave](#step-3-generate-your-key).</span><span class="sxs-lookup"><span data-stu-id="d2a02-341">When you run these commands, replace contosokey with the same value you specified in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a><span data-ttu-id="d2a02-342">Passaggio 4.2: Crittografare la chiave tramite la chiave per lo scambio di chiavi di Microsoft</span><span class="sxs-lookup"><span data-stu-id="d2a02-342">Step 4.2: Encrypt your key by using Microsoft’s Key Exchange Key</span></span>
<span data-ttu-id="d2a02-343">Eseguire uno di questi comandi, in base all'area geografica o all'istanza di Azure:</span><span class="sxs-lookup"><span data-stu-id="d2a02-343">Run one of the following commands, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="d2a02-344">America del Nord</span><span class="sxs-lookup"><span data-stu-id="d2a02-344">For North America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d2a02-345">Europa</span><span class="sxs-lookup"><span data-stu-id="d2a02-345">For Europe:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d2a02-346">Asia</span><span class="sxs-lookup"><span data-stu-id="d2a02-346">For Asia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d2a02-347">America Latina</span><span class="sxs-lookup"><span data-stu-id="d2a02-347">For Latin America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d2a02-348">Giappone</span><span class="sxs-lookup"><span data-stu-id="d2a02-348">For Japan:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d2a02-349">Per la Corea:</span><span class="sxs-lookup"><span data-stu-id="d2a02-349">For Korea:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d2a02-350">Per l'Australia:</span><span class="sxs-lookup"><span data-stu-id="d2a02-350">For Australia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d2a02-351">Per [Azure per enti pubblici](https://azure.microsoft.com/features/gov/), che usa l'istanza di Azure per il Governo degli Stati Uniti:</span><span class="sxs-lookup"><span data-stu-id="d2a02-351">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d2a02-352">Per il Dipartimento della difesa del governo degli Stati Uniti:</span><span class="sxs-lookup"><span data-stu-id="d2a02-352">For US Government DOD:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d2a02-353">Per il Canada:</span><span class="sxs-lookup"><span data-stu-id="d2a02-353">For Canada:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d2a02-354">Per la Germania:</span><span class="sxs-lookup"><span data-stu-id="d2a02-354">For Germany:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="d2a02-355">Per l'India:</span><span class="sxs-lookup"><span data-stu-id="d2a02-355">For India:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

<span data-ttu-id="d2a02-356">Quando si esegue il comando, usare le istruzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d2a02-356">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="d2a02-357">Sostituire *contosokey* con l'identificatore usato per generare la chiave in **Passaggio 3.5: Creare una nuova chiave** nel passaggio [Generare la chiave](#step-3-generate-your-key).</span><span class="sxs-lookup"><span data-stu-id="d2a02-357">Replace *contosokey* with the identifier that you used to generate the key in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>
* <span data-ttu-id="d2a02-358">Sostituire *SubscriptionID* con l'ID della sottoscrizione di Azure che contiene l'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="d2a02-358">Replace *SubscriptionID* with the ID of the Azure subscription that contains your key vault.</span></span> <span data-ttu-id="d2a02-359">Questo valore è stato recuperato in precedenza, in **Passaggio 1.2: Ottenere l'ID sottoscrizione di Azure** nel passaggio [Preparare la workstation connessa a Internet](#step-1-prepare-your-internet-connected-workstation).</span><span class="sxs-lookup"><span data-stu-id="d2a02-359">You retrieved this value previously, in **Step 1.2: Get your Azure subscription ID** from the [Prepare your Internet-connected workstation](#step-1-prepare-your-internet-connected-workstation) step.</span></span>
* <span data-ttu-id="d2a02-360">Sostituire *ContosoFirstHSMKey* con un'etichetta che viene usata per il nome del file di output.</span><span class="sxs-lookup"><span data-stu-id="d2a02-360">Replace *ContosoFirstHSMKey* with a label that is used for your output file name.</span></span>

<span data-ttu-id="d2a02-361">Se l'operazione ha esito positivo, viene visualizzato il messaggio **Result: SUCCESS** e nella cartella corrente è presente un nuovo file con il nome: KeyTransferPackage-*ContosoFirstHSMkey*.byok</span><span class="sxs-lookup"><span data-stu-id="d2a02-361">When this completes successfully, it displays **Result: SUCCESS** and there is a new file in the current folder that has the following name: KeyTransferPackage-*ContosoFirstHSMkey*.byok</span></span>

### <a name="step-43-copy-your-key-transfer-package-to-the-internet-connected-workstation"></a><span data-ttu-id="d2a02-362">Passaggio 4.3: Copiare il pacchetto di trasferimento della chiave nella workstation connessa a Internet</span><span class="sxs-lookup"><span data-stu-id="d2a02-362">Step 4.3: Copy your key transfer package to the Internet-connected workstation</span></span>
<span data-ttu-id="d2a02-363">Usare un'unità USB o un altro dispositivo di archiviazione portatile per copiare il file di output creato nel passaggio precedente (KeyTransferPackage-ContosoFirstHSMkey.byok) nella workstation connessa a Internet.</span><span class="sxs-lookup"><span data-stu-id="d2a02-363">Use a USB drive or other portable storage to copy the output file from the previous step (KeyTransferPackage-ContosoFirstHSMkey.byok) to your Internet-connected workstation.</span></span>

## <a name="step-5-transfer-your-key-to-azure-key-vault"></a><span data-ttu-id="d2a02-364">Passaggio 5: Trasferire la chiave all'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="d2a02-364">Step 5: Transfer your key to Azure Key Vault</span></span>
<span data-ttu-id="d2a02-365">Per questo passaggio finale, nella workstation connessa a Internet usare il cmdlet [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey), per caricare il pacchetto di trasferimento della chiave copiato dalla workstation disconnessa al modulo di protezione hardware dell'insieme di credenziali delle chiavi di Azure:</span><span class="sxs-lookup"><span data-stu-id="d2a02-365">For this final step, on the Internet-connected workstation, use the [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet to upload the key transfer package that you copied from the disconnected workstation to the Azure Key Vault HSM:</span></span>

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

<span data-ttu-id="d2a02-366">Se il pacchetto viene caricato correttamente, verranno visualizzate le proprietà della chiave aggiunta.</span><span class="sxs-lookup"><span data-stu-id="d2a02-366">If the upload is successful, you see displayed the properties of the key that you just added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2a02-367">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d2a02-367">Next steps</span></span>
<span data-ttu-id="d2a02-368">È ora possibile usare questa chiave HSM protetta nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="d2a02-368">You can now use this HSM-protected key in your key vault.</span></span> <span data-ttu-id="d2a02-369">Per altre informazioni, vedere la sezione **Per usare un modulo di protezione hardware (HSM)** nell'esercitazione [Introduzione all'insieme di credenziali delle chiavi di Azure](key-vault-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="d2a02-369">For more information, see the **If you want to use a hardware security module (HSM)** section in the [Getting started with Azure Key Vault](key-vault-get-started.md) tutorial.</span></span>
