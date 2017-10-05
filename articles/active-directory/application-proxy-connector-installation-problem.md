---
title: Problemi di installazione del connettore dell'agente proxy dell'applicazione | Microsoft Docs
description: Come risolvere i problemi che potrebbero verificarsi durante l'installazione del connettore dell'agente proxy dell'applicazione
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
ms.openlocfilehash: 91b3f6f3c8339647f568a509e9efd8e1fffb13dd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="problem-installing-the-application-proxy-agent-connector"></a><span data-ttu-id="fd5e1-103">Problemi di installazione del connettore dell'agente proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="fd5e1-103">Problem installing the Application Proxy Agent Connector</span></span>

<span data-ttu-id="fd5e1-104">Il connettore proxy dell'applicazione AAD di Microsoft è un componente di dominio interno che usa le connessioni in uscita per stabilire la connettività dall'endpoint disponibile del cloud al dominio interno.</span><span class="sxs-lookup"><span data-stu-id="fd5e1-104">Microsoft AAD Application Proxy Connector is an internal domain component that uses outbound connections to establish the connectivity from the cloud available endpoint to the internal domain.</span></span>

## <a name="general-problem-areas-with-connector-installation"></a><span data-ttu-id="fd5e1-105">Aree problematiche generali con l'installazione del connettore</span><span class="sxs-lookup"><span data-stu-id="fd5e1-105">General Problem Areas with Connector installation</span></span>

<span data-ttu-id="fd5e1-106">Quando l'installazione di un connettore non riesce, la causa principale riguarda in genere una delle seguenti aree:</span><span class="sxs-lookup"><span data-stu-id="fd5e1-106">When the installation of a connector fails, the root cause is usually one of the following areas:</span></span>

1.  <span data-ttu-id="fd5e1-107">**Connettività**: per completare un'installazione, è necessario che il nuovo connettore registri e definisca le future proprietà di attendibilità.</span><span class="sxs-lookup"><span data-stu-id="fd5e1-107">**Connectivity** – to complete a successful installation, the new connector needs to register and establish future trust properties.</span></span> <span data-ttu-id="fd5e1-108">Questa operazione viene eseguita tramite la connessione al servizio cloud proxy dell’applicazione AAD.</span><span class="sxs-lookup"><span data-stu-id="fd5e1-108">This is done by connecting to the AAD Application Proxy cloud service.</span></span>

2.  <span data-ttu-id="fd5e1-109">**Definizione dell'attendibilità**: il nuovo connettore crea un certificato autofirmato ed effettua la registrazione al servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="fd5e1-109">**Trust Establishment** – the new connector creates a self-signed cert and registers to the cloud service.</span></span>

3.  <span data-ttu-id="fd5e1-110">**Autenticazione dell'amministratore**: durante l'installazione, l'utente deve fornire le credenziali di amministratore per completare l'installazione del connettore.</span><span class="sxs-lookup"><span data-stu-id="fd5e1-110">**Authentication of the admin** – during installation, the user must provide admin credentials to complete the Connector installation.</span></span>

## <a name="verify-connectivity-to-the-cloud-application-proxy-service-and-microsoft-login-page"></a><span data-ttu-id="fd5e1-111">Verificare la connettività al servizio proxy dell'applicazione cloud e alla pagina di accesso Microsoft</span><span class="sxs-lookup"><span data-stu-id="fd5e1-111">Verify connectivity to the Cloud Application Proxy service and Microsoft Login page</span></span>

<span data-ttu-id="fd5e1-112">**Obiettivo:** verificare che il computer di connessione possa connettersi all'endpoint di registrazione proxy dell'applicazione AAD, nonché alla pagina di accesso Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fd5e1-112">**Objective:** Verify that the connector machine can connect to the AAD Application Proxy registration endpoint as well as Microsoft login page.</span></span>

1.  <span data-ttu-id="fd5e1-113">Aprire un browser e passare alla pagina Web seguente: <https://aadap-portcheck.connectorporttest.msappproxy.net>, quindi verificare che la connettività al data center degli Stati Uniti orientali e Stati Uniti centrali con le porte 9090 e 9091 sia funzionante.</span><span class="sxs-lookup"><span data-stu-id="fd5e1-113">Open a browser and go to the following web page: <https://aadap-portcheck.connectorporttest.msappproxy.net> , and verify that the connectivity to Central US and East US datacenters with ports 9090 and 9091 is working.</span></span>

2.  <span data-ttu-id="fd5e1-114">Se la connessione a una di queste porte non funziona (non è presente un segno di spunta verde), verificare che \*.msappproxy.net con le porte 9090 e 9091 sia definito correttamente per il firewall o proxy di back-end.</span><span class="sxs-lookup"><span data-stu-id="fd5e1-114">If any of those ports is not successful (doesn’t have a green checkmark), verify that the Firewall or backend proxy has \*.msappproxy.net with ports 9090 and 9091 defined correctly.</span></span>

3.  <span data-ttu-id="fd5e1-115">Aprire un browser (scheda separata) e passare alla pagina Web seguente: <https://login.microsoftonline.com>, quindi assicurarsi che sia possibile accedere a tale pagina.</span><span class="sxs-lookup"><span data-stu-id="fd5e1-115">Open a browser (separate tab) and go to the following web page: <https://login.microsoftonline.com>, make sure that you can login to that page.</span></span>

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a><span data-ttu-id="fd5e1-116">Verificare che il computer e i componenti di back-end supportino il certificato di attendibilità proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="fd5e1-116">Verify Machine and backend components support for Application Proxy trust cert</span></span>

<span data-ttu-id="fd5e1-117">**Obiettivo:** verificare che il computer di connessione, il proxy e il firewall di back-end possano supportare il certificato creato dal connettore per l'attendibilità futura.</span><span class="sxs-lookup"><span data-stu-id="fd5e1-117">**Objective:** Verify that the connector machine, backend proxy and firewall can support the certificate created by the connector for future trust.</span></span>

>[!NOTE]
><span data-ttu-id="fd5e1-118">Il connettore tenta di creare un certificato SHA512 supportato da TLS1.2.</span><span class="sxs-lookup"><span data-stu-id="fd5e1-118">The connector tries to create a SHA512 cert that is supported by TLS1.2.</span></span> <span data-ttu-id="fd5e1-119">Se il computer o il proxy e il firewall di back-end non supportano TLS1.2, l'installazione non viene completata.</span><span class="sxs-lookup"><span data-stu-id="fd5e1-119">If the machine or the backend firewall and proxy does not support TLS1.2, the installation fail.</span></span>
>
>

<span data-ttu-id="fd5e1-120">**Per risolvere il problema:**</span><span class="sxs-lookup"><span data-stu-id="fd5e1-120">**To resolve the issue:**</span></span>

1.  <span data-ttu-id="fd5e1-121">Verificare che il computer supporti TLS1.2: tutte le versioni di Windows successive alla 2012 R2 dovrebbero supportare TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="fd5e1-121">Verify the machine supports TLS1.2 – All Windows versions after 2012 R2 should support TLS 1.2.</span></span> <span data-ttu-id="fd5e1-122">Se la versione del computer di connessione di cui si dispone è 2012 R2 o precedente, assicurarsi che le seguenti Knowledge Base siano installate: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span><span class="sxs-lookup"><span data-stu-id="fd5e1-122">If your connector machine is from a version of 2012 R2 or prior, make sure that the following KBs are installed on the machine: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span></span>

2.  <span data-ttu-id="fd5e1-123">Contattare l'amministratore di rete e chiedere di verificare che il proxy e il firewall di back-end non blocchino SHA512 per il traffico in uscita.</span><span class="sxs-lookup"><span data-stu-id="fd5e1-123">Contact your network admin and ask to verify that the backend proxy and firewall do not block SHA512 for outgoing traffic.</span></span>

## <a name="verify-admin-is-used-to-install-the-connector"></a><span data-ttu-id="fd5e1-124">Verificare che il connettore venga installato da un utente con il ruolo di amministratore</span><span class="sxs-lookup"><span data-stu-id="fd5e1-124">Verify admin is used to install the connector</span></span>

<span data-ttu-id="fd5e1-125">**Obiettivo:** verificare che l'utente che tenta di installare il connettore sia un amministratore con le credenziali corrette.</span><span class="sxs-lookup"><span data-stu-id="fd5e1-125">**Objective:** Verify that the user who tries to install the connector is an administrator with correct credentials.</span></span> <span data-ttu-id="fd5e1-126">Al momento per completare l'installazione è necessario che l'utente sia un amministratore globale.</span><span class="sxs-lookup"><span data-stu-id="fd5e1-126">Currently, the user must be a global administrator for the installation to succeed.</span></span>

<span data-ttu-id="fd5e1-127">**Per verificare che le credenziali siano corrette:**</span><span class="sxs-lookup"><span data-stu-id="fd5e1-127">**To verify the credentials are correct:**</span></span>

<span data-ttu-id="fd5e1-128">Connettersi a <https://login.microsoftonline.com> e usare le stesse credenziali.</span><span class="sxs-lookup"><span data-stu-id="fd5e1-128">Connect to <https://login.microsoftonline.com> and use the same credentials.</span></span> <span data-ttu-id="fd5e1-129">Assicurarsi che l'accesso venga completato.</span><span class="sxs-lookup"><span data-stu-id="fd5e1-129">Make sure the login is successful.</span></span> <span data-ttu-id="fd5e1-130">È possibile controllare il ruolo dell'utente in **Azure Active Directory**  - &gt; **Utenti e gruppi**  - &gt; **Tutti gli utenti**.</span><span class="sxs-lookup"><span data-stu-id="fd5e1-130">You can check the user role by going to **Azure Active Directory** -&gt; **Users and Groups** -&gt; **All Users**.</span></span> 

<span data-ttu-id="fd5e1-131">Selezionare l'account utente, quindi "Ruolo directory" dal menu che viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="fd5e1-131">Select your user account, then “Directory Role” in the resulting menu.</span></span> <span data-ttu-id="fd5e1-132">Verificare che il ruolo selezionato sia "Amministratore globale".</span><span class="sxs-lookup"><span data-stu-id="fd5e1-132">Verify that the selected role is “Global administrator”.</span></span> <span data-ttu-id="fd5e1-133">Se non si è in grado di accedere a nessuna delle pagine con questa procedura, non si è un amministratore globale.</span><span class="sxs-lookup"><span data-stu-id="fd5e1-133">If you are unable to access any of the pages along these steps, you are not a global administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd5e1-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fd5e1-134">Next steps</span></span>
[<span data-ttu-id="fd5e1-135">Comprendere i connettori del proxy applicazione Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd5e1-135">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
