---
title: Introduzione al server Web ASP.NET per Azure AD v2 - Configurazione | Microsoft Docs
description: Implementazione di accessi Microsoft in una soluzione ASP.NET con un'applicazione tradizionale basata su Web browser tramite lo standard OpenID Connect
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 0c627802ccfba230dcde2dafffee26cb1c895791
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="60f56-103">Creare un'applicazione (Rapida)</span><span class="sxs-lookup"><span data-stu-id="60f56-103">Create an application (Express)</span></span>
<span data-ttu-id="60f56-104">È ora necessario registrare l'applicazione nel *portale di registrazione delle applicazioni Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="60f56-104">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="60f56-105">Registrare l'applicazione tramite il [portale di registrazione delle applicazioni Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span><span class="sxs-lookup"><span data-stu-id="60f56-105">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span></span>
2.  <span data-ttu-id="60f56-106">Immettere un nome per l'applicazione e l'indirizzo di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="60f56-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="60f56-107">Assicurarsi che l'opzione per l'installazione guidata sia selezionata</span><span class="sxs-lookup"><span data-stu-id="60f56-107">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="60f56-108">Seguire le istruzioni per aggiungere un URL di reindirizzamento all'applicazione</span><span class="sxs-lookup"><span data-stu-id="60f56-108">Follow the instructions to add a Redirect URL to your application</span></span>

## <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="60f56-109">Aggiungere le informazioni di registrazione dell'applicazione alla soluzione (Avanzata)</span><span class="sxs-lookup"><span data-stu-id="60f56-109">Add your application registration information to your solution (Advanced)</span></span>
<span data-ttu-id="60f56-110">È ora necessario registrare l'applicazione nel *portale di registrazione delle applicazioni Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="60f56-110">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="60f56-111">Passare al [portale di registrazione delle applicazioni Microsoft](https://apps.dev.microsoft.com/portal/register-app) per registrare un'applicazione</span><span class="sxs-lookup"><span data-stu-id="60f56-111">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) to register an application</span></span>
2. <span data-ttu-id="60f56-112">Immettere un nome per l'applicazione e l'indirizzo di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="60f56-112">Enter a name for your application and your email</span></span> 
3.  <span data-ttu-id="60f56-113">Assicurarsi che l'opzione per l'installazione guidata sia deselezionata</span><span class="sxs-lookup"><span data-stu-id="60f56-113">Make sure the option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="60f56-114">Fare clic su `Add Platform`, quindi selezionare `Web`</span><span class="sxs-lookup"><span data-stu-id="60f56-114">Click `Add Platform`, then select `Web`</span></span>
5.  <span data-ttu-id="60f56-115">Tornare a Visual Studio e in Esplora soluzioni selezionare il progetto, quindi esaminare la finestra Proprietà (se la finestra Proprietà non è visualizzata, premere F4)</span><span class="sxs-lookup"><span data-stu-id="60f56-115">Go back to Visual Studio and, in Solution Explorer, select the project and look at the Properties window (if you don’t see a Properties window, press F4)</span></span>
6.  <span data-ttu-id="60f56-116">Impostare il valore di SSL abilitato su `True`</span><span class="sxs-lookup"><span data-stu-id="60f56-116">Change SSL Enabled to `True`</span></span>
7.  <span data-ttu-id="60f56-117">Copiare l'URL SSL e aggiungere tale URL all'elenco di URL di reindirizzamento nell'elenco corrispondente del portale di registrazione:</span><span class="sxs-lookup"><span data-stu-id="60f56-117">Copy the SSL URL and add this URL to the list of Redirect URLs in the Registration Portal’s list of Redirect URLs:</span></span><br/><br/>![Proprietà del progetto](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  <span data-ttu-id="60f56-119">Aggiungere il codice seguente in `web.config`, disponibile nella sezione `configuration\appSettings` della cartella radice:</span><span class="sxs-lookup"><span data-stu-id="60f56-119">Add the following in `web.config` located in the root folder under the section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
<span data-ttu-id="60f56-120">Sostituire `ClientId` con l'ID applicazione appena registrato</span><span class="sxs-lookup"><span data-stu-id="60f56-120">Replace `ClientId` with the Application Id you just registered</span></span>
</li>
<li>
<span data-ttu-id="60f56-121">Sostituire `redirectUri` con l'URL SSL del progetto</span><span class="sxs-lookup"><span data-stu-id="60f56-121">Replace `redirectUri` with the SSL URL of your project</span></span>
</li>
</ol>
<!-- End Docs -->
