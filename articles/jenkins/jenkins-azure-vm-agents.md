---
title: aaaUse gli agenti di macchina virtuale di Azure per l'integrazione continua con Jenkins.
description: Agenti di macchine virtuali di Azure come slave di Jenkins
services: multiple
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 2388e6919d0280372166fbd325d80dafb00d7550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a>Usare gli agenti di macchine virtuali di Azure per l'integrazione continua con Jenkins

Questa Guida introduttiva viene illustrato come toouse hello toocreate plug-in Jenkins agenti VM di Azure un agente Linux (Ubuntu) su richiesta in Azure.

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa Guida rapida:

* Se si dispone già di un master Jenkins, è possibile iniziare con hello [modello di soluzione](install-jenkins-solution-template.md) 
* Fare riferimento troppo[creare un'entità servizio di Azure con Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) se non si dispone già di un'entità servizio di Azure.

## <a name="install-azure-vm-agents-plugin"></a>Installare il plug-in Agenti di macchine virtuali di Azure

Se si avvia da hello [modello di soluzione](install-jenkins-solution-template.md), plug-in agente VM di Azure hello è installato nel database master di Jenkins hello.

In caso contrario, installare hello **agenti VM di Azure** plug-in nel dashboard di Jenkins hello.

## <a name="configure-hello-plugin"></a>Configurare i plug-in hello

* Nel dashboard di Jenkins hello, fare clic su **Jenkins Gestisci -> Configurazione sistema ->**. Scorrere toohello parte inferiore della pagina hello e individuare la sezione hello con elenco a discesa hello **aggiungere nuovo cloud**. Scegliere dal menu hello **agenti VM di Microsoft Azure**
* Selezionare un account esistente dall'elenco a discesa di hello le credenziali di Azure.  tooadd un nuovo **dell'entità servizio di Microsoft Azure,** immettere hello seguenti valori: ID sottoscrizione, l'ID Client, segreto Client ed Endpoint Token OAuth 2.0.

![Credenziali di Azure](./media/jenkins-azure-vm-agents/service-principal.png)

* Fare clic su **verifica configurazione** toomake tale configurazione del profilo hello sia corretto.
* Salvare la configurazione di hello e continuare toohello successivo.

## <a name="template-configuration"></a>Configurazione del modello

### <a name="general-configuration"></a>Configurazione generale
Successivamente, configurare un modello per utilizzare toodefine un agente di macchine Virtuali di Azure. 

* Fare clic su **Aggiungi** tooadd un modello. 
* Specificare un nome per il nuovo modello. 
* Per etichetta hello, immettere "ubuntu". Questa etichetta viene usata durante la configurazione del processo hello.
* Selezionare la regione desiderata hello dalla casella combinata hello.
* Seleziona hello desiderato dimensioni della macchina virtuale.
* Specificare nome dell'account di archiviazione di Azure hello o lasciare il campo nome predefinito di hello toouse vuoto "jenkinsarmst".
* Specificare il periodo di conservazione di hello in minuti. Questa impostazione definisce il numero di hello di minuti che Jenkins può attendere prima di eliminare automaticamente un agente di inattività. Specificare 0 se non si desidera toobe agenti inattivo eliminata automaticamente.

![Configurazione generale](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a>Configurazione dell'immagine

Selezionare un agente, Linux (Ubuntu) toocreate **immagine di riferimento** e utilizzare hello seguente configurazione come un esempio. Fare riferimento troppo[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) per hello Azure più recenti supportate immagini.

* Image Publisher (Editore immagine): Canonical
* Image Offer (Offerta immagine): UbuntuServer
* Image Sku (Sku immagine): 14.04.5-LTS
* Image Version (Versione immagine): la più recente
* OS Type (Tipo di sistema operativo): Linux
* Launch Method (Metodo di avvio): SSH
* Specificare le credenziali di amministratore
* Per lo script di inizializzazione della macchina virtuale, immettere:
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![Configurazione dell'immagine](./media/jenkins-azure-vm-agents/image-config.png)

* Fare clic su **verificare modello** configurazione hello tooverify.
* Fare clic su **Salva**.

## <a name="create-a-job-in-jenkins"></a>Creare un processo in Jenkins

* Nel dashboard di Jenkins hello, fare clic su **nuovo elemento**. 
* Immettere un nome, selezionare **Freestyle project** (Progetto Freestyle) e fare clic su **OK**.
* In hello **generale** , selezionare "Limita l'accesso in cui è possono eseguire progetti" e digitare "ubuntu" nell'espressione di etichetta. È ora possibile vedere "ubuntu" nell'elenco a discesa hello.
* Fare clic su **Salva**.

![Configurazione del processo](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a>Compilare il nuovo progetto

* Tornare toohello Jenkins dashboard.
* Nuovo processo di scelta rapida hello creato, quindi fare clic su **compilare ora**. Verrà avviata la compilazione. 
* Una volta completata la compilazione hello, andare troppo**output di Console**. Vedrai che compilazione hello è stata eseguita in modalità remota in Azure.

![Output console](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a>Riferimento

* Video di Azure Friday: [Integrazione continua con Jenkins tramite gli agenti di macchine virtuali di Azure](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)
* Informazioni di supporto e opzioni di configurazione: [Wiki del plug-in Jenkins Agente di macchine virtuali di Azure](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin) 

