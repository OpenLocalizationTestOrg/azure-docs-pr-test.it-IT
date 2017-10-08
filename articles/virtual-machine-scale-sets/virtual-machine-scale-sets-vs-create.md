---
title: "Set di scalabilità macchina virtuale utilizzando Visual Studio aaaDeploy | Documenti Microsoft"
description: "Distribuire set di scalabilità di macchine virtuali tramite Visual Studio e un modello di Resource Manager"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed0786b8-34b2-49a8-85b5-2a628128ead6
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c89a9f2478ccc3d22989aea604a4273bcc46df82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-visual-studio"></a>Come toocreate Set di scalabilità di macchine virtuali con Visual Studio
Questo articolo illustra come toodeploy una scalabilità di macchine virtuali di Azure impostare l'utilizzo di una distribuzione a gruppo di risorse di Visual Studio.

[Set di scalabilità di macchine virtuali Azure](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) è un toodeploy risorse di calcolo di Azure e gestire una raccolta di macchine virtuali simili con scalabilità automatica e il bilanciamento del carico. È possibile eseguire il provisioning e distribuire set di scalabilità di macchine virtuali tramite i [modelli di Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates). I modelli di Azure Resource Manager possono essere distribuiti tramite l'interfaccia della riga di comando di Azure, PowerShell, REST e direttamente da Visual Studio. Visual Studio offre un set di modelli di esempio che possono essere distribuiti come parte di un progetto di distribuzione del gruppo di risorse di Azure.

Distribuzioni del gruppo di risorse di Azure sono un modo toogroup e pubblicano un set di risorse di Azure correlate in una sola operazione di distribuzione. Sono disponibili altre informazioni in [Creazione e distribuzione di gruppi di risorse di Azure tramite Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

## <a name="pre-requisites"></a>Prerequisiti
tooget avviata la distribuzione di set di scalabilità di macchine virtuali in Visual Studio, è necessario seguente hello:

* Visual Studio 2013 o versioni successive
* Azure SDK 2.7, 2.8 o 2.9

>[!NOTE]
>Queste istruzioni presuppongono l'uso di Visual Studio con [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).

## <a name="creating-a-project"></a>Creazione di un progetto
1. Creare un nuovo progetto in Visual Studio scegliendo **File | Nuovo | Progetto**.
   
    ![File Nuovo][file_new]

2. In **Visual c# | Cloud**, scegliere **Azure Resource Manager** toocreate un progetto per la distribuzione di un modello di gestione risorse di Azure.
   
    ![Crea progetto][create_project]

3. Hello l'elenco dei modelli, selezionare hello Linux o modello di impostare scala macchina virtuale Windows.
   
   ![Seleziona modello][select_Template]

4. Una volta creato il progetto vedere PowerShell script di distribuzione, un modello di gestione risorse di Azure e un file di parametro per hello Set di scalabilità della macchina virtuale.
   
    ![Esplora soluzioni][solution_explorer]

## <a name="customize-your-project"></a>Personalizzare il progetto
Ora è possibile modificare toocustomize modello hello per le esigenze dell'applicazione, ad esempio l'aggiunta di proprietà di estensione di macchina virtuale o la modifica di caricare le regole di bilanciamento del carico. Per impostazione predefinita modelli di impostare hello macchina virtuale scala sono configurati toodeploy hello AzureDiagnostics estensione rende facile tooadd regole di scalabilità automatica. L'estensione inoltre distribuisce un servizio di bilanciamento del carico con un indirizzo IP pubblico, configurato con regole NAT in entrata. 

bilanciamento del carico Hello consente di connettersi a istanze di macchina virtuale toohello con SSH (Linux) o RDP (Windows). intervallo di porte front-end di Hello inizia in corrispondenza di 50000. Per linux, questo significa che se si SSH tooport 50000, si è indirizzato tooport 22 di hello prima macchina virtuale nel Set di scalabilità hello. Connessione tooport 50001 è indirizzato tooport 22 di hello seconda macchina virtuale e così via.

 Tooedit un modo efficace i modelli con Visual Studio è toouse hello struttura JSON tooorganize hello parametri, variabili e le risorse. Una conoscenza di hello schema Visual Studio può indicare errori nel modello prima di distribuirlo.

![Esplora JSON][json_explorer]

## <a name="deploy-hello-project"></a>Distribuire il progetto hello
1. Distribuire hello Azure Resource Manager risorsa modello di toocreate hello Set di scalabilità della macchina virtuale. Fare clic sul nodo del progetto hello e scegliere **Distribuisci | Nuova distribuzione**.
   
    ![Modello di distribuzione][5deploy_Template]
    
2. Nella finestra di dialogo "Distribuisci tooResource gruppo" hello, selezionare la sottoscrizione.
   
    ![Modello di distribuzione][6deploy_Template]

3. Da qui è possibile creare il modello per toodeploy un gruppo di risorse di Azure.
   
    ![Nuovo gruppo di risorse][new_resource]

4. Successivamente, fare clic su **modifica parametri** tooenter i parametri passati tooyour modello. Prevedere hello del sistema operativo, che è necessario toocreate hello distribuzione hello username e password. Se non si dispone di PowerShell Tools per Visual Studio installata, è consigliabile toocheck **salvare le password** tooavoid un nascosti della riga di comando di PowerShell richiedere o utilizzare [keyvault supporto](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).
   
    ![Modifica parametri][edit_parameters]

5. Fare quindi clic su **Distribuisci**. Hello **Output** finestra viene visualizzato l'avanzamento della distribuzione hello. Si noti che l'azione hello esegue hello **deploy-azureresourcegroup.ps1** script.
   
   ![Finestra Output][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a>Esplorare il set di scalabilità di macchine virtuali
Una volta completata la distribuzione di hello, è possibile visualizzare hello nuova macchina virtuale Set di scalabilità in Visual Studio hello **Cloud Explorer** (aggiornamento hello elenco). Cloud Explorer consente di gestire le risorse di Azure in Visual Studio durante lo sviluppo di applicazioni. È inoltre possibile visualizzare il Set di scalabilità della macchina virtuale in hello [portale di Azure](https://portal.azure.com) e [Esplora inventario risorse di Azure](https://resources.azure.com/).

![Cloud Explorer][cloud_explorer]

 portale Hello fornisce migliore hello toovisually gestire l'infrastruttura di Azure con un web browser, mentre Esplora inventario risorse di Azure fornisce un modo semplice di tooexplore e debug delle risorse di Azure, offrendo una finestra in hello "visualizzazione di istanza" e anche con PowerShell comandi per le risorse di hello che si sta esaminando.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver distribuito il set di scalabilità di macchine virtuali tramite Visual Studio, è possibile personalizzare ulteriormente toosuit il progetto dei requisiti dell'applicazione. Ad esempio, configurare scalabilità automatica tramite l'aggiunta di un **Insights** della risorsa, l'aggiunta di infrastruttura tooyour modello (ad esempio macchine virtuali autonome) o distribuzione di applicazioni mediante l'estensione script personalizzata hello. Modelli di esempio sono disponibili in hello [modelli di avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates) repository GitHub (ricerca di "vmss").

[file_new]: ./media/virtual-machine-scale-sets-vs-create/1-FileNew.png
[create_project]: ./media/virtual-machine-scale-sets-vs-create/2-CreateProject.png
[select_Template]: ./media/virtual-machine-scale-sets-vs-create/3b-SelectTemplateLin.png
[solution_explorer]: ./media/virtual-machine-scale-sets-vs-create/4-SolutionExplorer.png
[json_explorer]: ./media/virtual-machine-scale-sets-vs-create/10-JsonExplorer.png
[5deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/5-DeployTemplate.png
[6deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/6-DeployTemplate.png
[new_resource]: ./media/virtual-machine-scale-sets-vs-create/7-NewResourceGroup.png
[edit_parameters]: ./media/virtual-machine-scale-sets-vs-create/8-EditParameter.png
[output_window]: ./media/virtual-machine-scale-sets-vs-create/9-Output.png
[cloud_explorer]: ./media/virtual-machine-scale-sets-vs-create/12-CloudExplorer.png
