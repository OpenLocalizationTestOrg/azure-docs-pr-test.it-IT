---
title: aaaHow tooopen hello le porte del firewall necessarie per un'applicazione Proxy dell'applicazione | Documenti Microsoft
description: Scoprire quali tooopen porte per toowork Proxy dell'applicazione hello Azure AD correttamente
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
ms.openlocfilehash: cdc7badb7c15591689a3bfd6bb26da182b00fb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-hello-firewall-ports-required-for-an-application-proxy-application"></a><span data-ttu-id="01111-103">Come tooopen hello porte del firewall necessarie per un'applicazione Proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="01111-103">How tooopen hello firewall ports required for an Application Proxy application</span></span>

<span data-ttu-id="01111-104">toosee un elenco completo delle porte necessarie hello e la funzione hello di ciascuna porta, vedere sezione Prerequisiti hello hello [documentazione del Proxy di applicazione](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span><span class="sxs-lookup"><span data-stu-id="01111-104">toosee a full list of hello required ports and hello function of each port, see hello prerequisites section of hello [Application Proxy documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span></span> <span data-ttu-id="01111-105">Si noti che il Proxy di applicazione usa solo le porte in uscita.</span><span class="sxs-lookup"><span data-stu-id="01111-105">note that Application Proxy only uses outbound ports.</span></span>

<span data-ttu-id="01111-106">È inoltre possibile verificare se è aperta tutti hello necessarie porte da aprire hello [strumento di Test porte connettore](https://aadap-portcheck.connectorporttest.msappproxy.net/) dalla rete locale.</span><span class="sxs-lookup"><span data-stu-id="01111-106">You can also check whether you have all hello required ports open by opening hello [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) from your on-prem network.</span></span> <span data-ttu-id="01111-107">La presenza di più segni di spunta verdi indica una maggiore resilienza.</span><span class="sxs-lookup"><span data-stu-id="01111-107">More green checkmarks means greater resiliency.</span></span> 

## <a name="app-proxy-regions"></a><span data-ttu-id="01111-108">Aree del proxy dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="01111-108">App Proxy regions</span></span>

<span data-ttu-id="01111-109">Stiamo lavorando in un modo toolet si conosce quali di queste aree deve toobe verde per l'utente.</span><span class="sxs-lookup"><span data-stu-id="01111-109">We are working on a way toolet you know which of these regions needs toobe green for you.</span></span> <span data-ttu-id="01111-110">Per il momento, assicurarsi che tutte siano verdi.</span><span class="sxs-lookup"><span data-stu-id="01111-110">For now, make sure they all are.</span></span> <span data-ttu-id="01111-111">Anche l'area Stati Uniti centrali è necessaria indipendentemente dall'area in cui ci si trova.</span><span class="sxs-lookup"><span data-stu-id="01111-111">Central US is also required regardless of which region you are in.</span></span>

<span data-ttu-id="01111-112">toomake che hello strumento offre hello risultati corretti, assicurarsi di:</span><span class="sxs-lookup"><span data-stu-id="01111-112">toomake sure hello tool gives you hello right results, be sure to:</span></span>

-   <span data-ttu-id="01111-113">Aprire lo strumento hello in un browser dal server hello in cui è stato installato connettore hello.</span><span class="sxs-lookup"><span data-stu-id="01111-113">Open hello tool on a browser from hello server where you have installed hello Connector.</span></span>

-   <span data-ttu-id="01111-114">Verificare che qualsiasi tooyour applicabile proxy o firewall connettore vengono anche applicate toothis pagina.</span><span class="sxs-lookup"><span data-stu-id="01111-114">Ensure that any proxies or firewalls applicable tooyour Connector are also applied toothis page.</span></span> <span data-ttu-id="01111-115">Questa operazione può essere eseguita in Internet Explorer passando troppo**impostazioni**  - &gt; **Opzioni Internet**  - &gt; **connessioni**  - &gt; **Impostazioni Lan**.</span><span class="sxs-lookup"><span data-stu-id="01111-115">This can be done in Internet Explorer by going too**Settings** -&gt; **Internet Options** -&gt; **Connections** -&gt; **Lan Settings**.</span></span> <span data-ttu-id="01111-116">In questa pagina viene visualizzato il campo di hello "Usa un Proxy Server per il LAN".</span><span class="sxs-lookup"><span data-stu-id="01111-116">On this page, you see hello field “Use a Proxy Server for your LAN”.</span></span> <span data-ttu-id="01111-117">Selezionare questa casella e inserire l'indirizzo del proxy hello nel campo "Address" hello.</span><span class="sxs-lookup"><span data-stu-id="01111-117">Select this box, and put hello proxy address into hello “Address” field.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01111-118">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="01111-118">Next steps</span></span>
[<span data-ttu-id="01111-119">Comprendere i connettori del proxy applicazione Azure AD</span><span class="sxs-lookup"><span data-stu-id="01111-119">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
