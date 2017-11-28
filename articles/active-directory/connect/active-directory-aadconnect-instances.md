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
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a><span data-ttu-id="25955-103">Azure AD Connect: Considerazioni speciali per le istanze</span><span class="sxs-lookup"><span data-stu-id="25955-103">Azure AD Connect: Special considerations for instances</span></span>
<span data-ttu-id="25955-104">Azure AD Connect è più utilizzata con l'istanza di hello world wide di Azure AD e Office 365.</span><span class="sxs-lookup"><span data-stu-id="25955-104">Azure AD Connect is most commonly used with hello world-wide instance of Azure AD and Office 365.</span></span> <span data-ttu-id="25955-105">Ma esistono anche altre istanze e hanno requisiti diversi per gli URL e altre considerazioni speciali.</span><span class="sxs-lookup"><span data-stu-id="25955-105">But there are also other instances and these have different requirements for URLs and other special considerations.</span></span>

## <a name="microsoft-cloud-germany"></a><span data-ttu-id="25955-106">Microsoft Cloud Germany</span><span class="sxs-lookup"><span data-stu-id="25955-106">Microsoft Cloud Germany</span></span>
<span data-ttu-id="25955-107">Hello [Microsoft Cloud Germania](http://www.microsoft.de/cloud-deutschland) è un cloud sovrani gestito da un dominio trusted in tedesco di dati.</span><span class="sxs-lookup"><span data-stu-id="25955-107">hello [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) is a sovereign cloud operated by a German data trustee.</span></span>

| <span data-ttu-id="25955-108">Tooopen URL server proxy</span><span class="sxs-lookup"><span data-stu-id="25955-108">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="25955-109">\*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="25955-109">\*.microsoftonline.de</span></span> |
| <span data-ttu-id="25955-110">\*.windows.net</span><span class="sxs-lookup"><span data-stu-id="25955-110">\*.windows.net</span></span> |
| <span data-ttu-id="25955-111">+Elenchi di revoche dei certificati</span><span class="sxs-lookup"><span data-stu-id="25955-111">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="25955-112">Quando si accede nel tenant di Azure AD tooyour, è necessario utilizzare un account nel dominio onmicrosoft.de hello.</span><span class="sxs-lookup"><span data-stu-id="25955-112">When you sign in tooyour Azure AD tenant, you must use an account in hello onmicrosoft.de domain.</span></span>

<span data-ttu-id="25955-113">Funzionalità attualmente non è presente in Germania Cloud Microsoft hello:</span><span class="sxs-lookup"><span data-stu-id="25955-113">Features currently not present in hello Microsoft Cloud Germany:</span></span>

* <span data-ttu-id="25955-114">**Azure AD Connect Health** non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="25955-114">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="25955-115">**Aggiornamenti automatici** non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="25955-115">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="25955-116">**Writeback delle password** è disponibile in anteprima con Azure AD Connect versione 1.1.570.0 e successive.</span><span class="sxs-lookup"><span data-stu-id="25955-116">**Password writeback** is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="25955-117">Altri servizi di Azure AD Premium non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="25955-117">Other Azure AD Premium services are not available.</span></span>

## <a name="microsoft-azure-government-cloud"></a><span data-ttu-id="25955-118">Cloud di Microsoft Azure per enti pubblici</span><span class="sxs-lookup"><span data-stu-id="25955-118">Microsoft Azure Government cloud</span></span>
<span data-ttu-id="25955-119">Hello [cloud di Microsoft Azure per enti pubblici](https://azure.microsoft.com/features/gov/) è un cloud per governo degli Stati Uniti.</span><span class="sxs-lookup"><span data-stu-id="25955-119">hello [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is a cloud for US government.</span></span>

<span data-ttu-id="25955-120">È stato supportato da versioni precedenti di DirSync.</span><span class="sxs-lookup"><span data-stu-id="25955-120">This cloud has been supported by earlier releases of DirSync.</span></span> <span data-ttu-id="25955-121">Da compilazione 1.1.180 di Azure AD Connect, hello prossima generazione di cloud hello è supportato.</span><span class="sxs-lookup"><span data-stu-id="25955-121">From build 1.1.180 of Azure AD Connect, hello next generation of hello cloud is supported.</span></span> <span data-ttu-id="25955-122">Questa generazione utilizza gli endpoint di base solo Stati Uniti e di un elenco di URL tooopen nel server proxy.</span><span class="sxs-lookup"><span data-stu-id="25955-122">This generation is using US-only based endpoints and have a different list of URLs tooopen in your proxy server.</span></span>

| <span data-ttu-id="25955-123">Tooopen URL server proxy</span><span class="sxs-lookup"><span data-stu-id="25955-123">URLs tooopen in proxy server</span></span> |
| --- |
| <span data-ttu-id="25955-124">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="25955-124">\*.microsoftonline.com</span></span> |
| <span data-ttu-id="25955-125">\*. microsoftonline.us</span><span class="sxs-lookup"><span data-stu-id="25955-125">\*.microsoftonline.us</span></span> |
| <span data-ttu-id="25955-126">\*.gov.us.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="25955-126">\*.gov.us.microsoftonline.com</span></span> |
| <span data-ttu-id="25955-127">+Elenchi di revoche dei certificati</span><span class="sxs-lookup"><span data-stu-id="25955-127">+Certificate Revocation Lists</span></span> |

<span data-ttu-id="25955-128">Azure AD Connect non è in grado di tooautomatically rilevare che si trova nel cloud per enti pubblici hello tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25955-128">Azure AD Connect is not able tooautomatically detect that your Azure AD tenant is located in hello Government cloud.</span></span> <span data-ttu-id="25955-129">È invece necessario hello tootake seguente azioni quando si installa Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="25955-129">Instead you need tootake hello following actions when you install Azure AD Connect.</span></span>

1. <span data-ttu-id="25955-130">Avviare l'installazione di Azure AD Connect hello.</span><span class="sxs-lookup"><span data-stu-id="25955-130">Start hello Azure AD Connect installation.</span></span>
2. <span data-ttu-id="25955-131">Quando viene visualizzata prima pagina hello in cui è richiesta la hello tooaccept contratto di licenza, non continuare, ma lasciare la procedura guidata installazione hello in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="25955-131">When you see hello first page where you are supposed tooaccept hello EULA, do not continue but leave hello installation wizard running.</span></span>
3. <span data-ttu-id="25955-132">Avviare regedit e modificare la chiave del Registro di sistema hello `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello valore `2`.</span><span class="sxs-lookup"><span data-stu-id="25955-132">Start regedit and change hello registry key `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello value `2`.</span></span>
4. <span data-ttu-id="25955-133">Tornare indietro toohello Azure AD Connect installazione guidata, accettare l'EULA hello e continuare.</span><span class="sxs-lookup"><span data-stu-id="25955-133">Go back toohello Azure AD Connect installation wizard, accept hello EULA, and continue.</span></span> <span data-ttu-id="25955-134">Durante l'installazione, assicurarsi che hello toouse **configurazione personalizzata** percorso di installazione (e non l'installazione rapida).</span><span class="sxs-lookup"><span data-stu-id="25955-134">During installation, make sure toouse hello **custom configuration** installation path (and not Express installation).</span></span> <span data-ttu-id="25955-135">Quindi continuare l'installazione di hello come di consueto.</span><span class="sxs-lookup"><span data-stu-id="25955-135">Then continue hello installation as usual.</span></span>

<span data-ttu-id="25955-136">Funzionalità attualmente non è presente nel cloud di Microsoft Azure per enti pubblici hello:</span><span class="sxs-lookup"><span data-stu-id="25955-136">Features currently not present in hello Microsoft Azure Government cloud:</span></span>

* <span data-ttu-id="25955-137">**Azure AD Connect Health** non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="25955-137">**Azure AD Connect Health** is not available.</span></span>
* <span data-ttu-id="25955-138">**Aggiornamenti automatici** non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="25955-138">**Automatic updates** is not available.</span></span>
* <span data-ttu-id="25955-139">**Writeback delle password** è disponibile in anteprima con Azure AD Connect versione 1.1.570.0 e successive.</span><span class="sxs-lookup"><span data-stu-id="25955-139">**Password writeback**  is available for preview with Azure AD Connect version 1.1.570.0 and after.</span></span>
* <span data-ttu-id="25955-140">Altri servizi di Azure AD Premium non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="25955-140">Other Azure AD Premium services are not available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25955-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25955-141">Next steps</span></span>
<span data-ttu-id="25955-142">Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="25955-142">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
