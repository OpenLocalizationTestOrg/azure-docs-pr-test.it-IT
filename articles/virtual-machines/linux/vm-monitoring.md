---
title: aaaEnable o la disabilitazione di macchina virtuale di Azure Monitoring
description: Viene descritto come tooEnable o disabilitare il monitoraggio di macchina virtuale Azure
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
ms.openlocfilehash: 39c2211e4e5f3ad364513b52c5acc70c00b432fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a><span data-ttu-id="dbded-103">Abilitare o disabilitare il monitoraggio delle VM di Azure</span><span class="sxs-lookup"><span data-stu-id="dbded-103">Enable or Disable Azure VM Monitoring</span></span>

<span data-ttu-id="dbded-104">In questa sezione viene descritto come tooenable o disabilitare il monitoraggio su virtuale dei computer in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="dbded-104">This section describes how tooenable or disable monitoring on Virtual machines running on Azure.</span></span> <span data-ttu-id="dbded-105">È possibile abilitare o disabilitare il monitoraggio tramite il portale di hello o interfaccia della riga di comando di Azure per Mac, Linux e Windows (Buongiorno CLI di Azure).</span><span class="sxs-lookup"><span data-stu-id="dbded-105">You can enable or disable monitoring using hello portal or Azure Command-line Interface for Mac, Linux, and Windows (hello Azure CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dbded-106">Questo documento descrive versione 2.3 di hello estensione diagnostica per Linux, che è stato deprecato.</span><span class="sxs-lookup"><span data-stu-id="dbded-106">This document describes version 2.3 of hello Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="dbded-107">La versione 2.3 sarà supportata fino al 30 giugno 2018.</span><span class="sxs-lookup"><span data-stu-id="dbded-107">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="dbded-108">Versione 3.0 di hello che estensione diagnostica per Linux può invece essere abilitato.</span><span class="sxs-lookup"><span data-stu-id="dbded-108">Version 3.0 of hello Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="dbded-109">Per ulteriori informazioni, vedere [hello documentazione](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="dbded-109">For more information, see [hello documentation](./diagnostic-extension.md).</span></span>

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a><span data-ttu-id="dbded-110">Abilitare o disabilitare il monitoraggio tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="dbded-110">Enable / Disable Monitoring through hello Azure portal</span></span>

<span data-ttu-id="dbded-111">È possibile abilitare il monitoraggio della VM di Azure, che fornisce dati sull'istanza ogni minuto</span><span class="sxs-lookup"><span data-stu-id="dbded-111">You can enable  monitoring of your Azure VM, which provides data about your instance in 1-minute periods.</span></span> <span data-ttu-id="dbded-112">(sono incluse le modifiche dell'archivio).</span><span class="sxs-lookup"><span data-stu-id="dbded-112">(storage changes apply).</span></span> <span data-ttu-id="dbded-113">Dati di diagnostica dettagliate sono quindi disponibili per hello VM nei grafici portale hello o tramite API hello.</span><span class="sxs-lookup"><span data-stu-id="dbded-113">Detailed diagnostics data is then available for hello VM in hello portal graphs or through hello API.</span></span> <span data-ttu-id="dbded-114">Per impostazione predefinita, il portale di Azure consente di abilitare il monitoraggio basato su host di un set limitato di metriche.</span><span class="sxs-lookup"><span data-stu-id="dbded-114">By default, Azure portal enables host-based monitoring of a limited set of metrics.</span></span> <span data-ttu-id="dbded-115">È possibile abilitare il monitoraggio delle metriche all'interno di una macchina virtuale durante hello che macchina virtuale è in esecuzione o in stato di arresto.</span><span class="sxs-lookup"><span data-stu-id="dbded-115">You can enable monitoring of metrics from within a VM while hello VM is running or in stopped state.</span></span>

* <span data-ttu-id="dbded-116">Aprire hello Azure portale in [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dbded-116">Open hello Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
* <span data-ttu-id="dbded-117">Nel riquadro di spostamento sinistro di hello, fare clic su macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="dbded-117">In hello left navigation, click Virtual machines.</span></span>
* <span data-ttu-id="dbded-118">Nelle macchine virtuali di hello elenco, selezionare un'istanza in esecuzione o arrestata.</span><span class="sxs-lookup"><span data-stu-id="dbded-118">In hello list Virtual machines, select a running or stopped instance.</span></span> <span data-ttu-id="dbded-119">Apre il pannello di "Macchina virtuale" Hello.</span><span class="sxs-lookup"><span data-stu-id="dbded-119">hello "Virtual machine" blade opens.</span></span>
* <span data-ttu-id="dbded-120">Fare clic su Tutte le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="dbded-120">Click All settings.</span></span>
* <span data-ttu-id="dbded-121">Fare clic su Diagnostica.</span><span class="sxs-lookup"><span data-stu-id="dbded-121">Click Diagnostics.</span></span>
* <span data-ttu-id="dbded-122">Modificare lo stato tooOn o impostata su Off.</span><span class="sxs-lookup"><span data-stu-id="dbded-122">Change status tooOn or Off.</span></span> <span data-ttu-id="dbded-123">È anche possibile selezionare in questo livello di hello Pannello di controllo dettaglio tooenable desiderato per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="dbded-123">You can also pick in this blade hello level of monitoring details you would like tooenable for your virtual machine.</span></span>

![Abilitare o disabilitare il monitoraggio tramite hello portale di Azure.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a><span data-ttu-id="dbded-125">Abilitare/Disabilitare il monitoraggio con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="dbded-125">Enable / Disable Monitoring with Azure CLI</span></span>

<span data-ttu-id="dbded-126">tooenable monitoraggio per una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dbded-126">tooenable monitoring for an Azure VM.</span></span>

* <span data-ttu-id="dbded-127">Creare un file denominato, ad esempio, PrivateConfig.json:</span><span class="sxs-lookup"><span data-stu-id="dbded-127">Create a file (named such as PrivateConfig.json):</span></span>

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* <span data-ttu-id="dbded-128">Abilitare estensione hello tramite CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="dbded-128">Enable hello extension via Azure CLI.</span></span>

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

<span data-ttu-id="dbded-129">Per ulteriori informazioni, vedere [estensione diagnostica per Linux tramite tooMonitor Linux VM dati sulle prestazioni e diagnostica](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dbded-129">For more information, see [Using Linux Diagnostic Extension tooMonitor Linux VM’s performance and diagnostic data](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
