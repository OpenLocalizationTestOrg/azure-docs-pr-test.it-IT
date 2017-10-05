---
title: Modificare i prefissi degli indirizzi IP per il gateway di rete locale e l'indirizzo IP del Gateway VPN | Azure| Portale | Microsoft Docs
description: Questo articolo illustra in modo dettagliato come modificare i prefissi degli indirizzi IP per il gateway di rete locale usando il portale di Azure.
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
ms.openlocfilehash: bdd6f90fe97408bd45a72adf58bfdc190207de46
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="modify-local-network-gateway-settings-using-the-azure-portal"></a><span data-ttu-id="0e429-103">Modificare le impostazioni del gateway di rete locale usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0e429-103">Modify local network gateway settings using the Azure portal</span></span>

<span data-ttu-id="0e429-104">In alcuni casi le impostazioni per il valore AddressPrefix o GatewayIPAddress del gateway di rete locale subiscono modifiche.</span><span class="sxs-lookup"><span data-stu-id="0e429-104">Sometimes the settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="0e429-105">Questo articolo illustra come modificare le impostazioni del gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="0e429-105">This article shows you how to modify your local network gateway settings.</span></span> <span data-ttu-id="0e429-106">È anche possibile modificare queste impostazioni con un altro metodo selezionando un'opzione diversa nell'elenco seguente:</span><span class="sxs-lookup"><span data-stu-id="0e429-106">You can also modify these settings using a different method by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0e429-107">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0e429-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="0e429-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e429-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="0e429-109">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="0e429-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <span data-ttu-id="0e429-110"><a name="ipaddprefix"></a>Modificare i prefissi degli indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="0e429-110"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

<span data-ttu-id="0e429-111">Quando si modificano i prefissi degli indirizzi IP, la procedura seguita varia a seconda che il gateway di rete locale abbia una connessione oppure no.</span><span class="sxs-lookup"><span data-stu-id="0e429-111">When you modify IP address prefixes, the steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <span data-ttu-id="0e429-112"><a name="gwip"></a>Modificare l'indirizzo IP del gateway</span><span class="sxs-lookup"><span data-stu-id="0e429-112"><a name="gwip"></a>Modify the gateway IP address</span></span>

<span data-ttu-id="0e429-113">Se l'indirizzo IP pubblico del dispositivo VPN a cui ci si vuole connettere è stato modificato, è necessario modificare il gateway di rete locale per riflettere tale modifica.</span><span class="sxs-lookup"><span data-stu-id="0e429-113">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="0e429-114">Quando si modifica l'indirizzo IP pubblico, la procedura seguita varia a seconda che il gateway di rete locale abbia una connessione oppure no.</span><span class="sxs-lookup"><span data-stu-id="0e429-114">When you change the public IP address, the steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a><span data-ttu-id="0e429-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0e429-115">Next steps</span></span>

<span data-ttu-id="0e429-116">È possibile verificare la connessione al gateway.</span><span class="sxs-lookup"><span data-stu-id="0e429-116">You can verify your gateway connection.</span></span> <span data-ttu-id="0e429-117">Vedere [Verificare una connessione al gateway](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="0e429-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>