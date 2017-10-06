---
title: File di test Sipi | Documenti Microsoft
description: Verifica dipendenze dei file toocheck ReadyForTest
services: active-directory-b2c
documentationcenter: 
author: Sipi
manager: Sipi
editor: Sipi
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f68
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: Sipi
ms.openlocfilehash: afd3dc94dfb30926b316256fb06a768a391004f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sipi-test-file"></a><span data-ttu-id="7e39f-103">File di test Sipi</span><span class="sxs-lookup"><span data-stu-id="7e39f-103">Sipi test file</span></span>

<span data-ttu-id="7e39f-104">Questa esercitazione introduttiva consente di registrare un'applicazione in un tenant di Microsoft Azure Active Directory (Azure AD) B2C in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="7e39f-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="7e39f-105">Al termine, l'applicazione è registrata per l'uso nel tenant di Azure B2C hello.</span><span class="sxs-lookup"><span data-stu-id="7e39f-105">When you're finished, your application is registered for use in hello Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e39f-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7e39f-106">Prerequisites</span></span>

<span data-ttu-id="7e39f-107">toobuild un'applicazione che accetta consumer per l'abbonamento e l'accesso, è necessario innanzitutto un'applicazione hello tooregister con un tenant di Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="7e39f-107">toobuild an application that accepts consumer sign-up and sign-in, you first need tooregister hello application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="7e39f-108">Ottenere il proprio tenant utilizzando i passaggi descritti nella procedura hello [creare un tenant di Azure Active Directory B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7e39f-108">Get your own tenant by using hello steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="7e39f-109">Le applicazioni create dal Pannello di Azure Active Directory B2C hello in hello portale di Azure devono essere gestite da hello nello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="7e39f-109">Applications created from hello Azure AD B2C blade in hello Azure portal must be managed from hello same location.</span></span> <span data-ttu-id="7e39f-110">Se si modificano applicazioni B2C hello tramite PowerShell o un altro portale, essi diventano non supportati e non funzionano con Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="7e39f-110">If you edit hello B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="7e39f-111">Visualizzare i dettagli di hello [errore app](#faulted-apps) sezione.</span><span class="sxs-lookup"><span data-stu-id="7e39f-111">See details in hello [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-toob2c-settings"></a><span data-ttu-id="7e39f-112">Passare a impostazioni tooB2C</span><span class="sxs-lookup"><span data-stu-id="7e39f-112">Navigate tooB2C settings</span></span>

<span data-ttu-id="7e39f-113">Accedi toohello [portale di Azure](https://portal.azure.com/) come amministratore globale del tenant hello B2C hello.</span><span class="sxs-lookup"><span data-stu-id="7e39f-113">Log in toohello [Azure portal](https://portal.azure.com/) as hello Global Administrator of hello B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

<span data-ttu-id="7e39f-114">Scegliere i passaggi successivi in base al tipo di applicazione hello che registrazione:</span><span class="sxs-lookup"><span data-stu-id="7e39f-114">Choose next steps based on hello application type you are registering:</span></span>
