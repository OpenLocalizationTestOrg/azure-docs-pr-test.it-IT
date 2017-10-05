---
title: 'Azure AD Connect: Istanze del servizio di sincronizzazione | Documentazione Microsoft'
description: Questa pagina contiene considerazioni speciali per le istanze di Azure AD.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e8321c3d16253226a5931cacbce6fa5d50b697bd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a><span data-ttu-id="64ec2-103">Azure AD Connect: Considerazioni speciali per le istanze</span><span class="sxs-lookup"><span data-stu-id="64ec2-103">Azure AD Connect: Special considerations for instances</span></span>
<span data-ttu-id="64ec2-104">Azure AD Connect si usa soprattutto con l'istanza di Azure AD e Office 365 disponibili in tutto il mondo.</span><span class="sxs-lookup"><span data-stu-id="64ec2-104">Azure AD Connect is most commonly used with the world-wide instance of Azure AD and Office 365.</span></span> <span data-ttu-id="64ec2-105">Ma esistono anche altre istanze e hanno requisiti diversi per gli URL e altre considerazioni speciali.</span><span class="sxs-lookup"><span data-stu-id="64ec2-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span></span>

## <a name="microsoft-cloud-germany"></a><span data-ttu-id="64ec2-106">Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="64ec2-106">Microsoft Cloud Germany</span></span>
<span data-ttu-id="64ec2-107">[Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) è un sovereign cloud gestito da un trustee dei dati tedesco.</span><span class="sxs-lookup"><span data-stu-id="64ec2-107">The [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span></span>

| <span data-ttu-id="64ec2-108">URL da aprire nel server proxy</span><span class="sxs-lookup"><span data-stu-id="64ec2-108">URLs to open in proxy server</span></span> |
| --- |
| <span data-ttu-id="64ec2-109">\*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="64ec2-109">\*.microsoftonline.de</span></span> |
| <span data-ttu-id="64ec2-110">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="64ec2-110">\*.windows.net</span></span> |
| <span data-ttu-id="64ec2-111">+Elenchi di revoche dei certificati</span><span class="sxs-lookup"><span data-stu-id="64ec2-111">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="64ec2-112">Quando si accede al tenant di Azure AD, è necessario usare un account nel dominio onmicrosoft.de.</span><span class="sxs-lookup"><span data-stu-id="64ec2-112">When you sign in to your Azure AD tenant, you must use an account in the onmicrosoft.de domain.</span></span>

<span data-ttu-id="64ec2-113">Funzionalità attualmente non presenti in Microsoft Cloud Germany:</span><span class="sxs-lookup"><span data-stu-id="64ec2-113">Features currently not present in the Microsoft Cloud Germany:</span></span>

* <span data-ttu-id="64ec2-114">**Azure AD Connect Health** non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="64ec2-114">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="64ec2-115">**Aggiornamenti automatici** non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="64ec2-115">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="64ec2-116">**Writeback delle password** è disponibile in anteprima con Azure AD Connect versione 1.1.570.0 e successive.</span><span class="sxs-lookup"><span data-stu-id="64ec2-116">**Password writeback** is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="64ec2-117">Altri servizi di Azure AD Premium non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="64ec2-117">Other Azure AD Premium services are not available.</span></span>

## <a name="microsoft-azure-government-cloud"></a><span data-ttu-id="64ec2-118">Cloud di Microsoft Azure per enti pubblici</span><span class="sxs-lookup"><span data-stu-id="64ec2-118">Microsoft Azure Government cloud</span></span>
<span data-ttu-id="64ec2-119">Il [cloud di Microsoft Azure per enti pubblici](https://azure.microsoft.com/features/gov/) è un cloud riservato al governo degli Stati Uniti.</span><span class="sxs-lookup"><span data-stu-id="64ec2-119">The [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span></span>

<span data-ttu-id="64ec2-120">È stato supportato da versioni precedenti di DirSync.</span><span class="sxs-lookup"><span data-stu-id="64ec2-120">This cloud has been supported by earlier releases of DirSync.</span></span> <span data-ttu-id="64ec2-121">A partire dalla build 1.1.180 di Azure AD Connect è supportata la generazione successiva del cloud.</span><span class="sxs-lookup"><span data-stu-id="64ec2-121">From build 1.1.180 of Azure AD Connect, the next generation of the cloud is supported.</span></span> <span data-ttu-id="64ec2-122">Questa generazione usa endpoint situati esclusivamente negli Stati Uniti e un elenco diverso di URL da aprire nel server proxy.</span><span class="sxs-lookup"><span data-stu-id="64ec2-122">This generation is using US-only based endpoints and have a different list of URLs to open in your proxy server.</span></span>

| <span data-ttu-id="64ec2-123">URL da aprire nel server proxy</span><span class="sxs-lookup"><span data-stu-id="64ec2-123">URLs to open in proxy server</span></span> |
| --- |
| <span data-ttu-id="64ec2-124">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="64ec2-124">\*.microsoftonline.com</span></span> |
| <span data-ttu-id="64ec2-125">\*. microsoftonline.us</span><span class="sxs-lookup"><span data-stu-id="64ec2-125">\*.microsoftonline.us</span></span> |
| <span data-ttu-id="64ec2-126">\*.gov.us.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="64ec2-126">\*.gov.us.microsoftonline.com</span></span> |
| <span data-ttu-id="64ec2-127">+Elenchi di revoche dei certificati</span><span class="sxs-lookup"><span data-stu-id="64ec2-127">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="64ec2-128">Azure AD Connect non è in grado di rilevare automaticamente che il tenant di Azure AD si trova nel cloud per enti pubblici.</span><span class="sxs-lookup"><span data-stu-id="64ec2-128">Azure AD Connect is not able to automatically detect that your Azure AD tenant is located in the Government cloud.</span></span> <span data-ttu-id="64ec2-129">È necessario intraprendere le azioni seguenti quando si installa Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="64ec2-129">Instead you need to take the following actions when you install Azure AD Connect.</span></span>

1. <span data-ttu-id="64ec2-130">Avviare l'installazione di Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="64ec2-130">Start the Azure AD Connect installation.</span></span>
2. <span data-ttu-id="64ec2-131">Quando viene visualizzata la prima pagina in cui si accetta il contratto di licenza, non continuare ma lasciare che venga eseguita l'installazione guidata.</span><span class="sxs-lookup"><span data-stu-id="64ec2-131">When you see the first page where you are supposed to accept the EULA, do not continue but leave the installation wizard running.</span></span>
3. <span data-ttu-id="64ec2-132">Avviare regedit e modificare la chiave del Registro di sistema `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` impostandola sul valore `2`.</span><span class="sxs-lookup"><span data-stu-id="64ec2-132">Start regedit and change the registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` to the value `2`.</span></span>
4. <span data-ttu-id="64ec2-133">Tornare all'installazione guidata di Azure AD Connect, accettare il contratto di licenza e continuare.</span><span class="sxs-lookup"><span data-stu-id="64ec2-133">Go back to the Azure AD Connect installation wizard, accept the EULA, and continue.</span></span> <span data-ttu-id="64ec2-134">Durante l'installazione, assicurarsi di usare il percorso di installazione della **configurazione personalizzata** e non l'installazione rapida.</span><span class="sxs-lookup"><span data-stu-id="64ec2-134">During installation, make sure to use the **custom configuration** installation path (and not Express installation).</span></span> <span data-ttu-id="64ec2-135">Continuare l'installazione come di consueto.</span><span class="sxs-lookup"><span data-stu-id="64ec2-135">Then continue the installation as usual.</span></span>

<span data-ttu-id="64ec2-136">Funzionalità attualmente non presenti nel cloud di Microsoft Azure per enti pubblici:</span><span class="sxs-lookup"><span data-stu-id="64ec2-136">Features currently not present in the Microsoft Azure Government cloud:</span></span>

* <span data-ttu-id="64ec2-137">**Azure AD Connect Health** non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="64ec2-137">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="64ec2-138">**Aggiornamenti automatici** non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="64ec2-138">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="64ec2-139">**Writeback delle password** è disponibile in anteprima con Azure AD Connect versione 1.1.570.0 e successive.</span><span class="sxs-lookup"><span data-stu-id="64ec2-139">**Password writeback**  is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="64ec2-140">Altri servizi di Azure AD Premium non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="64ec2-140">Other Azure AD Premium services are not available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64ec2-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="64ec2-141">Next steps</span></span>
<span data-ttu-id="64ec2-142">Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="64ec2-142">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
