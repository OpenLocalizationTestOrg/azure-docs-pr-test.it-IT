---
title: Modificare i prefissi di indirizzo IP gateway hello rete locale e l'indirizzo IP del Gateway VPN di hello | Azure | Portale | Documenti Microsoft
description: In questo articolo illustra la modifica di prefissi di indirizzi IP per il gateway di rete locale tramite hello portale di Azure.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 001df7b748ccc234d87aab3501a4f0e4ddfe60f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-portal"></a><span data-ttu-id="1198b-103">Modificare le impostazioni di gateway di rete locale utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1198b-103">Modify local network gateway settings using hello Azure portal</span></span>

<span data-ttu-id="1198b-104">In alcuni casi modificare le impostazioni di hello per il gateway di rete locale AddressPrefix o GatewayIPAddress.</span><span class="sxs-lookup"><span data-stu-id="1198b-104">Sometimes hello settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="1198b-105">In questo articolo illustra come toomodify le impostazioni del gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="1198b-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="1198b-106">È inoltre possibile modificare queste impostazioni utilizzando un metodo diverso selezionando un'opzione diversa da hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="1198b-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1198b-107">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1198b-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="1198b-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1198b-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="1198b-109">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="1198b-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <span data-ttu-id="1198b-110"><a name="ipaddprefix"></a>Modificare i prefissi degli indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="1198b-110"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

<span data-ttu-id="1198b-111">Quando si modificano i prefissi di indirizzi IP, hello è attenersi alla procedura dipendono se il gateway di rete locale dispone di una connessione.</span><span class="sxs-lookup"><span data-stu-id="1198b-111">When you modify IP address prefixes, hello steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <span data-ttu-id="1198b-112"><a name="gwip"></a>Modificare l'indirizzo IP del gateway hello</span><span class="sxs-lookup"><span data-stu-id="1198b-112"><a name="gwip"></a>Modify hello gateway IP address</span></span>

<span data-ttu-id="1198b-113">Se il dispositivo VPN hello che si desidera tooconnect toohas modificato l'indirizzo IP pubblico, è necessario toomodify hello rete locale gateway tooreflect modificare.</span><span class="sxs-lookup"><span data-stu-id="1198b-113">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="1198b-114">Quando si modifica l'indirizzo IP pubblico hello, hello è attenersi alla procedura dipendono se il gateway di rete locale dispone di una connessione.</span><span class="sxs-lookup"><span data-stu-id="1198b-114">When you change hello public IP address, hello steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a><span data-ttu-id="1198b-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1198b-115">Next steps</span></span>

<span data-ttu-id="1198b-116">È possibile verificare la connessione al gateway.</span><span class="sxs-lookup"><span data-stu-id="1198b-116">You can verify your gateway connection.</span></span> <span data-ttu-id="1198b-117">Vedere [Verificare una connessione al gateway](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="1198b-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>