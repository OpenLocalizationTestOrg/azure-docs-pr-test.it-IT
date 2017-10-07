---
title: aaaUnderstand condiviso degli indirizzi IP in Azure DevTest Labs | Documenti Microsoft
description: Informazioni sul modo Azure DevTest Labs Usa condiviso IP indirizzi toominimize hello pubblica IP indirizzi necessari tooaccess macchine virtuali nel lab.
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a>Comprendere gli indirizzi IP condivisi in Azure DevTest Labs

Azure DevTest Labs consente lab condivisione delle macchine virtuali hello stesso pubblico numero dell'indirizzo IP toominimize hello di pubblico tooaccess necessarie di indirizzi IP nel lab di singole macchine virtuali.  In questo articolo viene descritto come funzionano gli indirizzi IP condivisi e le opzioni di configurazione correlate.

## <a name="shared-ip-setting"></a>Impostazione di un indirizzo IP condiviso

Quando viene creato, un lab si trova nella subnet di una rete virtuale.  Per impostazione predefinita, questa subnet viene creata con **Abilita condivisa IP pubblico** impostare troppo*Sì*.  Questa configurazione crea un indirizzo IP pubblico per l'intera subnet hello.  Per altre informazioni sulla configurazione di reti e subnet virtuali, vedere [Configurare una rete virtuale per Azure DevTest Labs](devtest-lab-configure-vnet.md).

![Nuova subnet del lab](media/devtest-lab-shared-ip/lab-subnet.png)

Per i lab esistenti, è possibile abilitare questa opzione selezionando **Criteri e configurazione > Reti virtuali**. Quindi, selezionare una rete virtuale dall'elenco hello e scegliere **abilitare IP pubblico condiviso** per una subnet selezionata. È anche possibile disabilitare questa opzione in qualsiasi lab se non si desidera tooshare un indirizzo IP pubblico in lab, macchine virtuali.

Tutte le macchine virtuali creato in questa toousing predefinito lab un indirizzo IP condiviso.  Quando si creano hello macchina virtuale, questa impostazione può essere analizzata in hello **impostazioni avanzate** pannello **configurazione degli indirizzi IP**.

![Nuova macchina virtuale](media/devtest-lab-shared-ip/new-vm.png)

- **Condiviso:** tutte le macchine virtuali create come **Condivise** vengono inserite in un gruppo di risorse (RG). Un singolo indirizzo IP viene assegnato a tale scopo RG e tutte le macchine virtuali in hello RG utilizzerà l'indirizzo IP.
- **Pubblico:** ciascuna macchina virtuale creata dispone del proprio indirizzo IP e viene creata nel proprio gruppo di risorse.
- **Privato:** ogni macchina virtuale creata usa un indirizzo IP privato. Non sarà in grado di tooconnect toothis macchina virtuale direttamente da hello internet con Desktop remoto.

Ogni volta che una macchina virtuale con IP condiviso abilitato viene aggiunto toohello subnet, DevTest Labs automaticamente aggiunge hello VM tooa il bilanciamento del carico e assegna un numero di porta TCP in indirizzo IP pubblico hello, inoltro toohello porta RDP in hello macchina virtuale.  

## <a name="using-hello-shared-ip"></a>Utilizza hello condivisa IP

- **Gli utenti di Linux:** toohello SSH VM utilizzando l'indirizzo IP hello o nome di dominio completo, seguito da due punti, seguita dalla porta hello. Ad esempio, nella seguente figura hello hello RDP indirizzi toohello tooconnect macchina virtuale è `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.

  ![Esempio di macchina virtuale](media/devtest-lab-shared-ip/vm-info.png)

- **Gli utenti di Windows:** hello seleziona **Connetti** pulsante hello toodownload portale Azure un file RDP configurati in precedenza e accedere hello macchina virtuale.

## <a name="next-steps"></a>Passaggi successivi

* [Definire i criteri di lab in Azure DevTest Labs](devtest-lab-set-lab-policy.md)
* [Configurare una rete virtuale per Azure DevTest Labs](devtest-lab-configure-vnet.md)





