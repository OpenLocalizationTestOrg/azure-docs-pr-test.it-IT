---
title: aaaCreate o modificare labs automaticamente l'utilizzo di modelli di gestione risorse di Azure con PowerShell | Documenti Microsoft
description: Informazioni su come toouse modelli di gestione risorse di Azure con PowerShell toocreate o modificare labs automaticamente in un ambiente di DevTest lab
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: dad9944c-0b20-48be-ba80-8f4aa0950903
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: 29c8bc67caaec17b1f8926dde4e5d9d314b06600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-modify-labs-automatically-using-azure-resource-manager-templates-and-powershell"></a>Creare o modificare automaticamente i lab usando i modelli di Azure Resource Manager con PowerShell

DevTest Labs offre molti modelli di Azure Resource Manager e script di PowerShell utili per creare rapidamente e automaticamente nuovi lab o modificare quelli esistenti e quindi distribuire tali risorse.

In questo articolo consente di completare il processo di hello dell'utilizzo di questi modelli e gli script di creazione di hello tooautomate, modifica e la distribuzione del lab. In questo articolo viene anche di in cui è possibile trovare ulteriori informazioni sulla modalità toouse PowerShell tooperform alcuni comuni di attività in DevTest Labs.

## <a name="step-1-gather-your-templates-and-scripts"></a>Passaggio 1: raccogliere modelli e script
È possibile trovare [modelli di Azure Resource Manager](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) e [script di PowerShell](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) preconfigurati nel nostro [repository Github](https://github.com/Azure/azure-devtestlab) pubblico. Usarli così come sono o personalizzarli in base alle proprie esigenze e archiviarli nel proprio [repository Git privato](devtest-lab-add-artifact-repo.md). 

## <a name="step-2-modify-your-azure-resource-manager-template"></a>Passaggio 2: modificare il modello di Azure Resource Manager
È possibile seguire i passaggi di hello in [creare il primo modello di gestione risorse di Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template) se è mai stato creato un modello prima.

Inoltre, [procedure consigliate per la creazione di modelli di Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) offre molti toohelp linee guida e suggerimenti si creano modelli di gestione risorse di Azure che sono toouse semplice e affidabile. In genere, si utilizzerà una variante di uno degli approcci hello o gli esempi forniti e modificare il modello per le proprie esigenze.

## <a name="step-3-deploy-resources-with-powershell"></a>Passaggio 3: distribuire le risorse con PowerShell
Dopo aver personalizzato di modelli e gli script, seguire i passaggi di hello necessari troppo[distribuire le risorse e modelli di gestione risorse di Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy). articolo Hello vengono fornite informazioni generali sull'uso di Azure PowerShell con Gestione risorse di Azure modelli toodeploy tooAzure le risorse.


## <a name="common-tasks-you-can-perform-in-devtest-labs-using-powershell"></a>Attività comuni che è possibile eseguire nei lab di DevTest Labs tramite PowerShell
Esistono molte altre attività comuni che è possibile automatizzare con PowerShell. Hello della documentazione di hello nelle sezioni seguenti hello passaggi necessari tooperform queste attività.

* [Creare un'immagine personalizzata da un file VHD usando PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
* [Caricare l'account di archiviazione del toolab file disco rigido virtuale con PowerShell](devtest-lab-upload-vhd-using-powershell.md)
* [Aggiungere un ambiente lab tooa utente esterno tramite PowerShell](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell)
* [Creare un ruolo personalizzato lab tramite PowerShell](devtest-lab-grant-user-permissions-to-specific-lab-policies.md#creating-a-lab-custom-role-using-powershell)

### <a name="next-steps"></a>Passaggi successivi
* Informazioni su come toocreate un [repository Git privato](devtest-lab-add-artifact-repo.md) in cui verranno archiviati i modelli personalizzati o gli script.
* Esplorare hello [modelli di gestione risorse di Azure dalla raccolta di modelli di avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates).
