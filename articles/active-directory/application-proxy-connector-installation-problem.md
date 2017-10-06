---
title: l'installazione aaaProblem hello connettore agente Proxy dell'applicazione | Documenti Microsoft
description: "Come tootroubleshoot problemi potrà faccia durante l'installazione di hello connettore agente Proxy di applicazione"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 07ac366a429083af0c9b87aa9df9cf3876132b90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-proxy-agent-connector"></a><span data-ttu-id="f7d2d-103">Problema durante l'installazione hello connettore agente Proxy di applicazione</span><span class="sxs-lookup"><span data-stu-id="f7d2d-103">Problem installing hello Application Proxy Agent Connector</span></span>

<span data-ttu-id="f7d2d-104">Connettore Proxy dell'applicazione Microsoft AAD è un componente di dominio interno che utilizza la connettività di hello tooestablish le connessioni in uscita dal dominio interno toohello hello cloud endpoint disponibile.</span><span class="sxs-lookup"><span data-stu-id="f7d2d-104">Microsoft AAD Application Proxy Connector is an internal domain component that uses outbound connections tooestablish hello connectivity from hello cloud available endpoint toohello internal domain.</span></span>

## <a name="general-problem-areas-with-connector-installation"></a><span data-ttu-id="f7d2d-105">Aree problematiche generali con l'installazione del connettore</span><span class="sxs-lookup"><span data-stu-id="f7d2d-105">General Problem Areas with Connector installation</span></span>

<span data-ttu-id="f7d2d-106">Quando l'installazione di hello di un connettore non riesce, causa radice di hello è in genere una delle seguenti aree hello:</span><span class="sxs-lookup"><span data-stu-id="f7d2d-106">When hello installation of a connector fails, hello root cause is usually one of hello following areas:</span></span>

1.  <span data-ttu-id="f7d2d-107">**Connettività** – toocomplete una corretta installazione hello nuovo connettore esigenze tooregister e stabilire le proprietà di attendibilità future.</span><span class="sxs-lookup"><span data-stu-id="f7d2d-107">**Connectivity** – toocomplete a successful installation, hello new connector needs tooregister and establish future trust properties.</span></span> <span data-ttu-id="f7d2d-108">Questa operazione viene eseguita tramite la connessione toohello servizio cloud Proxy dell'applicazione AAD.</span><span class="sxs-lookup"><span data-stu-id="f7d2d-108">This is done by connecting toohello AAD Application Proxy cloud service.</span></span>

2.  <span data-ttu-id="f7d2d-109">**Creazione del trust** – nuovo connettore hello crea un certificato autofirmato e registra il servizio di cloud toohello.</span><span class="sxs-lookup"><span data-stu-id="f7d2d-109">**Trust Establishment** – hello new connector creates a self-signed cert and registers toohello cloud service.</span></span>

3.  <span data-ttu-id="f7d2d-110">**L'autenticazione di salve** : durante l'installazione, hello utente deve fornire le credenziali di amministratore l'installazione del connettore toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="f7d2d-110">**Authentication of hello admin** – during installation, hello user must provide admin credentials toocomplete hello Connector installation.</span></span>

## <a name="verify-connectivity-toohello-cloud-application-proxy-service-and-microsoft-login-page"></a><span data-ttu-id="f7d2d-111">Verifica del servizio Proxy di applicazione Cloud toohello di connettività e di pagine di Login Microsoft</span><span class="sxs-lookup"><span data-stu-id="f7d2d-111">Verify connectivity toohello Cloud Application Proxy service and Microsoft Login page</span></span>

<span data-ttu-id="f7d2d-112">**Obiettivo:** verificare tale macchina connettore hello possa connettersi a endpoint di registrazione AAD Application Proxy toohello come pagina di accesso di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f7d2d-112">**Objective:** Verify that hello connector machine can connect toohello AAD Application Proxy registration endpoint as well as Microsoft login page.</span></span>

1.  <span data-ttu-id="f7d2d-113">Aprire toohello un browser e andare seguente pagina web: <https://aadap-portcheck.connectorporttest.msappproxy.net> , verificare che tooCentral connettività hello Stati Uniti e funzioni di Data Center Stati Uniti orientali con porte 9090 e 9091.</span><span class="sxs-lookup"><span data-stu-id="f7d2d-113">Open a browser and go toohello following web page: <https://aadap-portcheck.connectorporttest.msappproxy.net> , and verify that hello connectivity tooCentral US and East US datacenters with ports 9090 and 9091 is working.</span></span>

2.  <span data-ttu-id="f7d2d-114">Se le porte non è riuscita (non dispone di un segno di spunta verde), verificare che hello Firewall o proxy back-end ha \*. msappproxy.net con porte 9090 e 9091 definito correttamente.</span><span class="sxs-lookup"><span data-stu-id="f7d2d-114">If any of those ports is not successful (doesn’t have a green checkmark), verify that hello Firewall or backend proxy has \*.msappproxy.net with ports 9090 and 9091 defined correctly.</span></span>

3.  <span data-ttu-id="f7d2d-115">Aprire un browser (scheda separata) e passare toohello seguente pagina web: <https://login.microsoftonline.com>, assicurarsi che si può eseguire l'accesso toothat pagina.</span><span class="sxs-lookup"><span data-stu-id="f7d2d-115">Open a browser (separate tab) and go toohello following web page: <https://login.microsoftonline.com>, make sure that you can login toothat page.</span></span>

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a><span data-ttu-id="f7d2d-116">Verificare che il computer e i componenti di back-end supportino il certificato di attendibilità proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="f7d2d-116">Verify Machine and backend components support for Application Proxy trust cert</span></span>

<span data-ttu-id="f7d2d-117">**Obiettivo:** verificare che macchina connettore hello, back-end proxy e firewall supporti certificato hello creato tramite il connettore di hello per trust future.</span><span class="sxs-lookup"><span data-stu-id="f7d2d-117">**Objective:** Verify that hello connector machine, backend proxy and firewall can support hello certificate created by hello connector for future trust.</span></span>

>[!NOTE]
><span data-ttu-id="f7d2d-118">connettore Hello tenta toocreate un certificato SHA512 supportato da TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="f7d2d-118">hello connector tries toocreate a SHA512 cert that is supported by TLS1.2.</span></span> <span data-ttu-id="f7d2d-119">Se la macchina hello o firewall back-end hello e proxy non supporta TLS 1.2, l'installazione di hello non riuscire.</span><span class="sxs-lookup"><span data-stu-id="f7d2d-119">If hello machine or hello backend firewall and proxy does not support TLS1.2, hello installation fail.</span></span>
>
>

<span data-ttu-id="f7d2d-120">**problema di hello tooresolve:**</span><span class="sxs-lookup"><span data-stu-id="f7d2d-120">**tooresolve hello issue:**</span></span>

1.  <span data-ttu-id="f7d2d-121">Verificare che la macchina hello supporta TLS 1.2: le versioni di tutte le finestre dopo 2012 R2 devono supportare TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="f7d2d-121">Verify hello machine supports TLS1.2 – All Windows versions after 2012 R2 should support TLS 1.2.</span></span> <span data-ttu-id="f7d2d-122">Se il computer del connettore da una versione del 2012 R2 o precedente, assicurarsi che tale hello Knowledge Base seguente vengono installati nel computer di hello: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span><span class="sxs-lookup"><span data-stu-id="f7d2d-122">If your connector machine is from a version of 2012 R2 or prior, make sure that hello following KBs are installed on hello machine: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span></span>

2.  <span data-ttu-id="f7d2d-123">Contattare l'amministratore di rete e richiedere tooverify che firewall e proxy di back-end hello non blocchino SHA512 per il traffico in uscita.</span><span class="sxs-lookup"><span data-stu-id="f7d2d-123">Contact your network admin and ask tooverify that hello backend proxy and firewall do not block SHA512 for outgoing traffic.</span></span>

## <a name="verify-admin-is-used-tooinstall-hello-connector"></a><span data-ttu-id="f7d2d-124">Verificare amministrazione viene utilizzato tooinstall hello connettore</span><span class="sxs-lookup"><span data-stu-id="f7d2d-124">Verify admin is used tooinstall hello connector</span></span>

<span data-ttu-id="f7d2d-125">**Obiettivo:** verificare che un utente di hello che tenta di connettore hello tooinstall sia un amministratore con le credenziali corrette.</span><span class="sxs-lookup"><span data-stu-id="f7d2d-125">**Objective:** Verify that hello user who tries tooinstall hello connector is an administrator with correct credentials.</span></span> <span data-ttu-id="f7d2d-126">Attualmente, utente hello deve essere un amministratore globale per hello installazione toosucceed.</span><span class="sxs-lookup"><span data-stu-id="f7d2d-126">Currently, hello user must be a global administrator for hello installation toosucceed.</span></span>

<span data-ttu-id="f7d2d-127">**le credenziali di hello tooverify sono corrette:**</span><span class="sxs-lookup"><span data-stu-id="f7d2d-127">**tooverify hello credentials are correct:**</span></span>

<span data-ttu-id="f7d2d-128">Connettersi troppo<https://login.microsoftonline.com> e utilizzare hello stesse credenziali.</span><span class="sxs-lookup"><span data-stu-id="f7d2d-128">Connect too<https://login.microsoftonline.com> and use hello same credentials.</span></span> <span data-ttu-id="f7d2d-129">Verificare che l'account di accesso hello ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="f7d2d-129">Make sure hello login is successful.</span></span> <span data-ttu-id="f7d2d-130">È possibile verificare il ruolo di utente hello passando troppo**Azure Active Directory**  - &gt; **utenti e gruppi**  - &gt; **tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="f7d2d-130">You can check hello user role by going too**Azure Active Directory** -&gt; **Users and Groups** -&gt; **All Users**.</span></span> 

<span data-ttu-id="f7d2d-131">Selezionare l'account utente, quindi "ruolo della Directory" nel menu di hello risultante.</span><span class="sxs-lookup"><span data-stu-id="f7d2d-131">Select your user account, then “Directory Role” in hello resulting menu.</span></span> <span data-ttu-id="f7d2d-132">Verificare che il ruolo selezionato hello "Amministratore globale".</span><span class="sxs-lookup"><span data-stu-id="f7d2d-132">Verify that hello selected role is “Global administrator”.</span></span> <span data-ttu-id="f7d2d-133">Se si è grado tooaccess qualsiasi hello pagine lungo questi passaggi, non è un amministratore globale.</span><span class="sxs-lookup"><span data-stu-id="f7d2d-133">If you are unable tooaccess any of hello pages along these steps, you are not a global administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7d2d-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f7d2d-134">Next steps</span></span>
[<span data-ttu-id="f7d2d-135">Comprendere i connettori del proxy applicazione Azure AD</span><span class="sxs-lookup"><span data-stu-id="f7d2d-135">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
