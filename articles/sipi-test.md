---
title: File di test Sipi | Documenti Microsoft
description: File di test per verificare le dipendenze ReadyForTest
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
ms.openlocfilehash: 871d58818dcbaee5f7a5f07c19e2297ec6459a6f
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/28/2017
---
# <a name="sipi-test-file"></a><span data-ttu-id="eba74-103">File di test Sipi</span><span class="sxs-lookup"><span data-stu-id="eba74-103">Sipi test file</span></span>

<span data-ttu-id="eba74-104">Questa esercitazione introduttiva consente di registrare un'applicazione in un tenant di Microsoft Azure Active Directory (Azure AD) B2C in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="eba74-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="eba74-105">Al termine, l'applicazione viene registrata per l'uso nel tenant di Azure B2C.</span><span class="sxs-lookup"><span data-stu-id="eba74-105">When you're finished, your application is registered for use in the Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eba74-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="eba74-106">Prerequisites</span></span>

<span data-ttu-id="eba74-107">Per compilare un'applicazione che accetta l'iscrizione e l'accesso dell'utente, è necessario innanzi tutto registrarla con tenant di Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="eba74-107">To build an application that accepts consumer sign-up and sign-in, you first need to register the application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="eba74-108">Per ottenere il tenant, seguire la procedura illustrata in [Azure Active Directory B2C: creare un tenant di Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="eba74-108">Get your own tenant by using the steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="eba74-109">Le applicazioni create dal pannello Azure AD B2C nel portale di Azure devono essere gestite dalla stessa posizione.</span><span class="sxs-lookup"><span data-stu-id="eba74-109">Applications created from the Azure AD B2C blade in the Azure portal must be managed from the same location.</span></span> <span data-ttu-id="eba74-110">Le applicazioni B2C, se vengono modificate usando PowerShell o un altro portale, non sono più supportate e non funzionano con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="eba74-110">If you edit the B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="eba74-111">Per altri dettagli, vedere la sezione [App con errori](#faulted-apps).</span><span class="sxs-lookup"><span data-stu-id="eba74-111">See details in the [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-to-b2c-settings"></a><span data-ttu-id="eba74-112">Passare alle impostazioni di B2C</span><span class="sxs-lookup"><span data-stu-id="eba74-112">Navigate to B2C settings</span></span>

<span data-ttu-id="eba74-113">Accedere al [portale di Azure](https://portal.azure.com/) come amministratore globale del tenant di B2C.</span><span class="sxs-lookup"><span data-stu-id="eba74-113">Log in to the [Azure portal](https://portal.azure.com/) as the Global Administrator of the B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

<span data-ttu-id="eba74-114">Scegliere i passaggi successivi in base al tipo di applicazione da registrare:</span><span class="sxs-lookup"><span data-stu-id="eba74-114">Choose next steps based on the application type you are registering:</span></span>
