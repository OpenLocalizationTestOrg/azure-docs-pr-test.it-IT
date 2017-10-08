---
title: errori di artefatto aaaDiagnose nella macchina virtuale di Azure DevTest Labs | Documenti Microsoft
description: Informazioni su come gli errori di artefatto tootroubleshoot DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 115e0086-3293-4adf-8738-9f639f31f918
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: tarcher
ms.openlocfilehash: 40b3cea72cf071cc5d9a6d002d309d923c3d3084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-artifact-failures-in-hello-lab"></a>Diagnosticare gli errori di artefatto in lab hello 
Dopo aver creato un elemento, è possibile controllare toosee se ha avuto esito positivo o non è riuscita. Registri di artefatto in DevTest Labs forniscono informazioni che è possibile utilizzare toodiagnose un errore di elemento. Esistono due modi diversi, è possibile visualizzare le informazioni sul log per una macchina virtuale Windows hello artefatto.

> [!NOTE]
> tooensure che gli errori correttamente vengono identificati e descritto, è importante elemento hello è strutturato in modo corretto. Per informazioni su come toocorrectly costruire un elemento, vedere [creare gli elementi personalizzati](devtest-lab-artifact-author.md). E toosee un esempio di un elemento strutturato correttamente, consultare questa [tipi di parametri di Test](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts/windows-test-paramtypes) artefatto.

## <a name="troubleshoot-artifact-failures-using-hello-azure-portal"></a>Risoluzione dei problemi di elemento utilizzando hello portale di Azure
errori di toodiagnose portale Azure hello toouse durante la creazione dell'elemento, seguire questi passaggi:

1. Dall'elenco di hello delle risorse, selezionare l'ambiente lab.

2. Scegliere una macchina virtuale di Windows che include l'elemento hello desiderato tooinvestigate hello.

3. Nel riquadro sinistro di hello in **generale**, scegliere **elementi**. Viene visualizzato un elenco di elementi associati a tale macchina virtuale, che indicano il nome di hello dell'artefatto hello e il relativo stato.

   ![Esempio di archivio git dell’elemento](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifacts-failure.png)

4. Scegliere un elemento che mostra lo stato **Failed**. elemento Hello viene aperto e verrà visualizzato un messaggio di estensione che include i dettagli sull'errore hello dell'artefatto hello.

   ![Esempio di archivio git dell’elemento](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error.png)


## <a name="troubleshoot-artifact-failures-from-within-hello-vm"></a>Risolvere gli errori di artefatto di hello VM
i registri di artefatto hello tooview dalla macchina virtuale hello, seguire questi passaggi:

1. Accedi toohello macchina virtuale che contiene l'elemento hello desiderato toodiagnose.

2. Passare tooC:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.9\Status dove "1.9 è numero di versione di hello estensione lato client.

   ![Esempio di archivio git dell’elemento](./media/devtest-lab-troubleshoot-artifact-failure/devtest-lab-artifact-error-vm-status.png)

3. Aprire hello **stato** file tooview le informazioni che consente di diagnosticare gli errori di elemento per la macchina virtuale.




[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Post di blog correlati
* [Aggiungere un dominio di Active Directory utilizzando un modello di gestione delle risorse in Azure DevTest Labs di tooexisting VM](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[aggiungere un ambiente lab tooa di repository Git](devtest-lab-add-artifact-repo.md).

