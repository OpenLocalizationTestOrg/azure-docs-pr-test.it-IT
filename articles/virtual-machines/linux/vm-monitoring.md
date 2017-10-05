---
title: Abilitare o disabilitare il monitoraggio delle VM di Azure
description: Descrive come abilitare o disabilitare il monitoraggio delle VM di Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 9b2fe579113d6ca6bfd27d82eb9d4657657d44ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a><span data-ttu-id="09da8-103">Abilitare o disabilitare il monitoraggio delle VM di Azure</span><span class="sxs-lookup"><span data-stu-id="09da8-103">Enable or Disable Azure VM Monitoring</span></span>

<span data-ttu-id="09da8-104">Questa sezione descrive come abilitare o disabilitare il monitoraggio nelle macchine virtuali in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="09da8-104">This section describes how to enable or disable monitoring on Virtual machines running on Azure.</span></span> <span data-ttu-id="09da8-105">È possibile abilitare o disabilitare il monitoraggio usando il portale o l'interfaccia della riga di comando di Azure per Mac, Linux e Windows (l'interfaccia della riga di comando di Azure).</span><span class="sxs-lookup"><span data-stu-id="09da8-105">You can enable or disable monitoring using the portal or Azure Command-line Interface for Mac, Linux, and Windows (the Azure CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09da8-106">Questo documento descrive la versione 2.3 dell'estensione Diagnostica per Linux, che è stata deprecata.</span><span class="sxs-lookup"><span data-stu-id="09da8-106">This document describes version 2.3 of the Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="09da8-107">La versione 2.3 sarà supportata fino al 30 giugno 2018.</span><span class="sxs-lookup"><span data-stu-id="09da8-107">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="09da8-108">È invece possibile abilitare la versione 3.0 dell'estensione Diagnostica per Linux.</span><span class="sxs-lookup"><span data-stu-id="09da8-108">Version 3.0 of the Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="09da8-109">Per altre informazioni, vedere [la documentazione](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="09da8-109">For more information, see [the documentation](./diagnostic-extension.md).</span></span>

## <a name="enable--disable-monitoring-through-the-azure-portal"></a><span data-ttu-id="09da8-110">Abilitare/Disabilitare il monitoraggio dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="09da8-110">Enable / Disable Monitoring through the Azure portal</span></span>

<span data-ttu-id="09da8-111">È possibile abilitare il monitoraggio della VM di Azure, che fornisce dati sull'istanza ogni minuto</span><span class="sxs-lookup"><span data-stu-id="09da8-111">You can enable  monitoring of your Azure VM, which provides data about your instance in 1-minute periods.</span></span> <span data-ttu-id="09da8-112">(sono incluse le modifiche dell'archivio).</span><span class="sxs-lookup"><span data-stu-id="09da8-112">(storage changes apply).</span></span> <span data-ttu-id="09da8-113">Dati di diagnostica dettagliati sono quindi disponibili per la VM nei grafici del portale o tramite l'API.</span><span class="sxs-lookup"><span data-stu-id="09da8-113">Detailed diagnostics data is then available for the VM in the portal graphs or through the API.</span></span> <span data-ttu-id="09da8-114">Per impostazione predefinita, il portale di Azure consente di abilitare il monitoraggio basato su host di un set limitato di metriche.</span><span class="sxs-lookup"><span data-stu-id="09da8-114">By default, Azure portal enables host-based monitoring of a limited set of metrics.</span></span> <span data-ttu-id="09da8-115">È possibile abilitare il monitoraggio delle metriche dalla macchina virtuale mentre questa si trova nello stato in corso di esecuzione o arrestato.</span><span class="sxs-lookup"><span data-stu-id="09da8-115">You can enable monitoring of metrics from within a VM while the VM is running or in stopped state.</span></span>

* <span data-ttu-id="09da8-116">Aprire il portale di Azure all'indirizzo [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="09da8-116">Open the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
* <span data-ttu-id="09da8-117">Nel riquadro di spostamento a sinistra fare clic su Macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="09da8-117">In the left navigation, click Virtual machines.</span></span>
* <span data-ttu-id="09da8-118">Nell'elenco Macchine virtuali selezionare un'istanza in esecuzione o arrestata.</span><span class="sxs-lookup"><span data-stu-id="09da8-118">In the list Virtual machines, select a running or stopped instance.</span></span> <span data-ttu-id="09da8-119">Verrà visualizzato il pannello "Macchina virtuale".</span><span class="sxs-lookup"><span data-stu-id="09da8-119">The "Virtual machine" blade opens.</span></span>
* <span data-ttu-id="09da8-120">Fare clic su Tutte le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="09da8-120">Click All settings.</span></span>
* <span data-ttu-id="09da8-121">Fare clic su Diagnostica.</span><span class="sxs-lookup"><span data-stu-id="09da8-121">Click Diagnostics.</span></span>
* <span data-ttu-id="09da8-122">Impostare lo stato su Sì o No.</span><span class="sxs-lookup"><span data-stu-id="09da8-122">Change status to On or Off.</span></span> <span data-ttu-id="09da8-123">In questo pannello è anche possibile selezionare il livello di dettagli di monitoraggio che si vuole abilitare per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="09da8-123">You can also pick in this blade the level of monitoring details you would like to enable for your virtual machine.</span></span>

![Abilitare/Disabilitare il monitoraggio dal portale di Azure.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a><span data-ttu-id="09da8-125">Abilitare/Disabilitare il monitoraggio con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="09da8-125">Enable / Disable Monitoring with Azure CLI</span></span>

<span data-ttu-id="09da8-126">Per abilitare il monitoraggio per una VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="09da8-126">To enable monitoring for an Azure VM.</span></span>

* <span data-ttu-id="09da8-127">Creare un file denominato, ad esempio, PrivateConfig.json:</span><span class="sxs-lookup"><span data-stu-id="09da8-127">Create a file (named such as PrivateConfig.json):</span></span>

```json
{
        "storageAccountName":"the storage account to receive data",
        "storageAccountKey":"the key of the account"
}
```

* <span data-ttu-id="09da8-128">Abilitare l'estensione tramite l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="09da8-128">Enable the extension via Azure CLI.</span></span>

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

<span data-ttu-id="09da8-129">Per altre informazioni vedere [Uso dell'estensione Diagnostica per Linux per monitorare le prestazioni e i dati di diagnostica di una macchina virtuale Linux](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="09da8-129">For more information, see [Using Linux Diagnostic Extension to Monitor Linux VM’s performance and diagnostic data](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
