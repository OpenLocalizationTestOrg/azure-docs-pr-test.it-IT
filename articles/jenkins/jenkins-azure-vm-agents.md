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
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a><span data-ttu-id="33e22-103">Usare gli agenti di macchine virtuali di Azure per l'integrazione continua con Jenkins</span><span class="sxs-lookup"><span data-stu-id="33e22-103">Use Azure VM agents for continuous integration with Jenkins.</span></span>

<span data-ttu-id="33e22-104">Questa Guida introduttiva viene illustrato come toouse hello toocreate plug-in Jenkins agenti VM di Azure un agente Linux (Ubuntu) su richiesta in Azure.</span><span class="sxs-lookup"><span data-stu-id="33e22-104">This quickstart shows how toouse hello Jenkins Azure VM Agents plugin toocreate an on-demand Linux (Ubuntu) agent in Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33e22-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="33e22-105">Prerequisites</span></span>

<span data-ttu-id="33e22-106">toocomplete questa Guida rapida:</span><span class="sxs-lookup"><span data-stu-id="33e22-106">toocomplete this quickstart:</span></span>

* <span data-ttu-id="33e22-107">Se si dispone già di un master Jenkins, è possibile iniziare con hello [modello di soluzione](install-jenkins-solution-template.md)</span><span class="sxs-lookup"><span data-stu-id="33e22-107">If you do not already have a Jenkins master, you can start with hello [Solution Template](install-jenkins-solution-template.md)</span></span> 
* <span data-ttu-id="33e22-108">Fare riferimento troppo[creare un'entità servizio di Azure con Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) se non si dispone già di un'entità servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="33e22-108">Refer too[Create an Azure Service principal with Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) if you do not already have an Azure service principal.</span></span>

## <a name="install-azure-vm-agents-plugin"></a><span data-ttu-id="33e22-109">Installare il plug-in Agenti di macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="33e22-109">Install Azure VM Agents plugin</span></span>

<span data-ttu-id="33e22-110">Se si avvia da hello [modello di soluzione](install-jenkins-solution-template.md), plug-in agente VM di Azure hello è installato nel database master di Jenkins hello.</span><span class="sxs-lookup"><span data-stu-id="33e22-110">If you start from hello [Solution Template](install-jenkins-solution-template.md), hello Azure VM Agent plugin is installed in hello Jenkins master.</span></span>

<span data-ttu-id="33e22-111">In caso contrario, installare hello **agenti VM di Azure** plug-in nel dashboard di Jenkins hello.</span><span class="sxs-lookup"><span data-stu-id="33e22-111">Otherwise, install hello **Azure VM Agents** plugin from within hello Jenkins dashboard.</span></span>

## <a name="configure-hello-plugin"></a><span data-ttu-id="33e22-112">Configurare i plug-in hello</span><span class="sxs-lookup"><span data-stu-id="33e22-112">Configure hello plugin</span></span>

* <span data-ttu-id="33e22-113">Nel dashboard di Jenkins hello, fare clic su **Jenkins Gestisci -> Configurazione sistema ->**.</span><span class="sxs-lookup"><span data-stu-id="33e22-113">Within hello Jenkins dashboard, click **Manage Jenkins -> Configure System ->**.</span></span> <span data-ttu-id="33e22-114">Scorrere toohello parte inferiore della pagina hello e individuare la sezione hello con elenco a discesa hello **aggiungere nuovo cloud**.</span><span class="sxs-lookup"><span data-stu-id="33e22-114">Scroll toohello bottom of hello page and find hello section with hello dropdown **Add new cloud**.</span></span> <span data-ttu-id="33e22-115">Scegliere dal menu hello **agenti VM di Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="33e22-115">From hello menu, select **Microsoft Azure VM Agents**</span></span>
* <span data-ttu-id="33e22-116">Selezionare un account esistente dall'elenco a discesa di hello le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="33e22-116">Select an existing account from hello Azure Credentials dropdown.</span></span>  <span data-ttu-id="33e22-117">tooadd un nuovo **dell'entità servizio di Microsoft Azure,** immettere hello seguenti valori: ID sottoscrizione, l'ID Client, segreto Client ed Endpoint Token OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="33e22-117">tooadd a new **Microsoft Azure Service Principal,** enter hello following values: Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span>

![Credenziali di Azure](./media/jenkins-azure-vm-agents/service-principal.png)

* <span data-ttu-id="33e22-119">Fare clic su **verifica configurazione** toomake tale configurazione del profilo hello sia corretto.</span><span class="sxs-lookup"><span data-stu-id="33e22-119">Click **Verify configuration** toomake sure that hello profile configuration is correct.</span></span>
* <span data-ttu-id="33e22-120">Salvare la configurazione di hello e continuare toohello successivo.</span><span class="sxs-lookup"><span data-stu-id="33e22-120">Save hello configuration, and continue toohello next step.</span></span>

## <a name="template-configuration"></a><span data-ttu-id="33e22-121">Configurazione del modello</span><span class="sxs-lookup"><span data-stu-id="33e22-121">Template configuration</span></span>

### <a name="general-configuration"></a><span data-ttu-id="33e22-122">Configurazione generale</span><span class="sxs-lookup"><span data-stu-id="33e22-122">General configuration</span></span>
<span data-ttu-id="33e22-123">Successivamente, configurare un modello per utilizzare toodefine un agente di macchine Virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="33e22-123">Next, configure a template for use toodefine an Azure VM agent.</span></span> 

* <span data-ttu-id="33e22-124">Fare clic su **Aggiungi** tooadd un modello.</span><span class="sxs-lookup"><span data-stu-id="33e22-124">Click **Add** tooadd a template.</span></span> 
* <span data-ttu-id="33e22-125">Specificare un nome per il nuovo modello.</span><span class="sxs-lookup"><span data-stu-id="33e22-125">Provide a name for your new template.</span></span> 
* <span data-ttu-id="33e22-126">Per etichetta hello, immettere "ubuntu".</span><span class="sxs-lookup"><span data-stu-id="33e22-126">For hello label, enter  "ubuntu."</span></span> <span data-ttu-id="33e22-127">Questa etichetta viene usata durante la configurazione del processo hello.</span><span class="sxs-lookup"><span data-stu-id="33e22-127">This label is used during hello job configuration.</span></span>
* <span data-ttu-id="33e22-128">Selezionare la regione desiderata hello dalla casella combinata hello.</span><span class="sxs-lookup"><span data-stu-id="33e22-128">Select hello desired region from hello combo box.</span></span>
* <span data-ttu-id="33e22-129">Seleziona hello desiderato dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="33e22-129">Select hello desired VM size.</span></span>
* <span data-ttu-id="33e22-130">Specificare nome dell'account di archiviazione di Azure hello o lasciare il campo nome predefinito di hello toouse vuoto "jenkinsarmst".</span><span class="sxs-lookup"><span data-stu-id="33e22-130">Specify hello Azure Storage account name or leave it blank toouse hello default name "jenkinsarmst."</span></span>
* <span data-ttu-id="33e22-131">Specificare il periodo di conservazione di hello in minuti.</span><span class="sxs-lookup"><span data-stu-id="33e22-131">Specify hello retention time in minutes.</span></span> <span data-ttu-id="33e22-132">Questa impostazione definisce il numero di hello di minuti che Jenkins può attendere prima di eliminare automaticamente un agente di inattività.</span><span class="sxs-lookup"><span data-stu-id="33e22-132">This setting defines hello number of minutes Jenkins can wait before automatically deleting an idle agent.</span></span> <span data-ttu-id="33e22-133">Specificare 0 se non si desidera toobe agenti inattivo eliminata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="33e22-133">Specify 0 if you do not want idle agents toobe deleted automatically.</span></span>

![Configurazione generale](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a><span data-ttu-id="33e22-135">Configurazione dell'immagine</span><span class="sxs-lookup"><span data-stu-id="33e22-135">Image configuration</span></span>

<span data-ttu-id="33e22-136">Selezionare un agente, Linux (Ubuntu) toocreate **immagine di riferimento** e utilizzare hello seguente configurazione come un esempio.</span><span class="sxs-lookup"><span data-stu-id="33e22-136">toocreate a Linux (Ubuntu) agent, select **Image reference** and use hello following configuration as an example.</span></span> <span data-ttu-id="33e22-137">Fare riferimento troppo[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) per hello Azure più recenti supportate immagini.</span><span class="sxs-lookup"><span data-stu-id="33e22-137">Refer too[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) for hello latest Azure supported images.</span></span>

* <span data-ttu-id="33e22-138">Image Publisher (Editore immagine): Canonical</span><span class="sxs-lookup"><span data-stu-id="33e22-138">Image Publisher: Canonical</span></span>
* <span data-ttu-id="33e22-139">Image Offer (Offerta immagine): UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="33e22-139">Image Offer: UbuntuServer</span></span>
* <span data-ttu-id="33e22-140">Image Sku (Sku immagine): 14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="33e22-140">Image Sku: 14.04.5-LTS</span></span>
* <span data-ttu-id="33e22-141">Image Version (Versione immagine): la più recente</span><span class="sxs-lookup"><span data-stu-id="33e22-141">Image version: latest</span></span>
* <span data-ttu-id="33e22-142">OS Type (Tipo di sistema operativo): Linux</span><span class="sxs-lookup"><span data-stu-id="33e22-142">OS Type: Linux</span></span>
* <span data-ttu-id="33e22-143">Launch Method (Metodo di avvio): SSH</span><span class="sxs-lookup"><span data-stu-id="33e22-143">Launch method: SSH</span></span>
* <span data-ttu-id="33e22-144">Specificare le credenziali di amministratore</span><span class="sxs-lookup"><span data-stu-id="33e22-144">Provide an admin credentials</span></span>
* <span data-ttu-id="33e22-145">Per lo script di inizializzazione della macchina virtuale, immettere:</span><span class="sxs-lookup"><span data-stu-id="33e22-145">For VM initialization script, enter:</span></span>
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![Configurazione dell'immagine](./media/jenkins-azure-vm-agents/image-config.png)

* <span data-ttu-id="33e22-147">Fare clic su **verificare modello** configurazione hello tooverify.</span><span class="sxs-lookup"><span data-stu-id="33e22-147">Click **Verify Template** tooverify hello configuration.</span></span>
* <span data-ttu-id="33e22-148">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="33e22-148">Click **Save**.</span></span>

## <a name="create-a-job-in-jenkins"></a><span data-ttu-id="33e22-149">Creare un processo in Jenkins</span><span class="sxs-lookup"><span data-stu-id="33e22-149">Create a job in Jenkins</span></span>

* <span data-ttu-id="33e22-150">Nel dashboard di Jenkins hello, fare clic su **nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="33e22-150">Within hello Jenkins dashboard, click **New Item**.</span></span> 
* <span data-ttu-id="33e22-151">Immettere un nome, selezionare **Freestyle project** (Progetto Freestyle) e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="33e22-151">Enter a name and select **Freestyle project** and click **OK**.</span></span>
* <span data-ttu-id="33e22-152">In hello **generale** , selezionare "Limita l'accesso in cui è possono eseguire progetti" e digitare "ubuntu" nell'espressione di etichetta.</span><span class="sxs-lookup"><span data-stu-id="33e22-152">In hello **General** tab, select "Restrict where project can be run" and type "ubuntu" in Label Expression.</span></span> <span data-ttu-id="33e22-153">È ora possibile vedere "ubuntu" nell'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="33e22-153">You now see "ubuntu" in hello dropdown.</span></span>
* <span data-ttu-id="33e22-154">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="33e22-154">Click **Save**.</span></span>

![Configurazione del processo](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a><span data-ttu-id="33e22-156">Compilare il nuovo progetto</span><span class="sxs-lookup"><span data-stu-id="33e22-156">Build your new project</span></span>

* <span data-ttu-id="33e22-157">Tornare toohello Jenkins dashboard.</span><span class="sxs-lookup"><span data-stu-id="33e22-157">Go back toohello Jenkins dashboard.</span></span>
* <span data-ttu-id="33e22-158">Nuovo processo di scelta rapida hello creato, quindi fare clic su **compilare ora**.</span><span class="sxs-lookup"><span data-stu-id="33e22-158">Right-click hello new job you created, then click **Build now**.</span></span> <span data-ttu-id="33e22-159">Verrà avviata la compilazione.</span><span class="sxs-lookup"><span data-stu-id="33e22-159">A build is kicked off.</span></span> 
* <span data-ttu-id="33e22-160">Una volta completata la compilazione hello, andare troppo**output di Console**.</span><span class="sxs-lookup"><span data-stu-id="33e22-160">Once hello build is complete, go too**Console output**.</span></span> <span data-ttu-id="33e22-161">Vedrai che compilazione hello è stata eseguita in modalità remota in Azure.</span><span class="sxs-lookup"><span data-stu-id="33e22-161">You see that hello build was performed remotely on Azure.</span></span>

![Output console](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a><span data-ttu-id="33e22-163">Riferimento</span><span class="sxs-lookup"><span data-stu-id="33e22-163">Reference</span></span>

* <span data-ttu-id="33e22-164">Video di Azure Friday: [Integrazione continua con Jenkins tramite gli agenti di macchine virtuali di Azure](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span><span class="sxs-lookup"><span data-stu-id="33e22-164">Azure Friday video: [Continuous Integration with Jenkins using Azure VM agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span></span>
* <span data-ttu-id="33e22-165">Informazioni di supporto e opzioni di configurazione: [Wiki del plug-in Jenkins Agente di macchine virtuali di Azure](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span><span class="sxs-lookup"><span data-stu-id="33e22-165">Support information and configuration options:  [Azure VM Agent Jenkins Plugin Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span></span> 

