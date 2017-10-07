---
title: aaaOverview come toocreate e distribuire un toohello offerta Marketplace | Documenti Microsoft
description: Comprendere hello passaggi necessari toobecome uno sviluppatore di Microsoft approvato e creare e distribuire un'immagine di macchina virtuale, un modello, servizio dati o servizio sviluppatore in hello Azure Marketplace
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5343bd26-c6e4-4589-85b7-4a2c00bba8ab
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio
ms.openlocfilehash: ac5480b98b8b1021a595db951ed9c974f74415dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-and-manage-an-offer-in-hello-azure-marketplace"></a>Pubblicare e gestire un'offerta in hello Azure Marketplace
In questo articolo viene fornito agli sviluppatori di toohelp creare, distribuire e gestire le relative soluzioni elencati in hello Azure Marketplace per altri clienti Azure e toopurchase partner e l'utilizzo.

## <a name="marketplace-publishing"></a>Pubblicazione sul Marketplace
Come un server di pubblicazione Azure, è possibile distribuire e vendere soluzioni innovative o gli sviluppatori tooother del servizio, fornitori di software indipendenti, e professionisti IT di hello Marketplace. Tramite hello Marketplace, è possibile contattare i clienti che desiderano tooquickly sviluppano applicazioni basate su cloud e le soluzioni mobili. Se la soluzione venga destinata agli utenti di business, sarà possibile hello tooconsider [AppSource](http://appsource.microsoft.com) marketplace.


## <a name="supported-types-of-solutions"></a>Tipi di soluzioni supportati
Hello prima cosa si desidera toodo come un server di pubblicazione è toodefine il tipo di soluzione offre la società. Hello Marketplace supporta i seguenti tipi di offerte di hello:

|Tipo di soluzione|Macchine virtuali|Modello di soluzione|
|---|---|---|
|**Definizione**|Immagini preconfigurate con un sistema operativo completamente installato e una o più applicazioni. Un'immagine di macchina virtuale fornisce hello informazioni necessarie toocreate e distribuire le macchine virtuali in hello servizio macchine virtuali di Azure.|Una struttura di dati che può fare riferimento a uno o più servizi di Azure distinti, compresi i servizi pubblicati da altri venditori. Azure ai sottoscrittori di usarlo toodeploy una o più offerte in modo coordinato singolo.|
|**Esempio**|In qualità di editore di Azure, l'utente ha creato e convalidato una macchina virtuale con un servizio di database innovativo. Altri sottoscrittori Azure desidera tooprocure e distribuire la macchina virtuale negli ambienti di servizio cloud.|Come un server di pubblicazione Azure, è stato fornito un set di servizi da in Azure che rendono i servizi cloud toodeploy rapido con bilanciamento del carico, sicurezza avanzata e la disponibilità elevata. Altri sottoscrittori Azure risparmiare tempo reperimento di modello di soluzione hello in grado di soddisfare l'obiettivo. Non devono toomanually individuare, approvvigionamento di sistemi, distribuire e configurare hello identici o simili servizi di Azure.|

> [!NOTE]
> Alcuni passaggi sono condivisi tra tipi diversi di hello di soluzioni e gli altri sono distinti toohello rispettivo tipo di soluzione. In questo articolo fornisce una breve panoramica dei passaggi di hello toocomplete è necessario per qualsiasi tipo di soluzione.

## <a name="publish-a-solution"></a>Pubblicare una soluzione
![Candidare, registrare, pubblicare](media/marketplace-publishing-getting-started/img01.png)

### <a name="nominate-your-solution-for-pre-approval"></a>Proporre la soluzione per l'approvazione
una macchina virtuale toopublish [soluzione](https://createopportunity.azurewebsites.net) toohello Marketplace, hello completo Microsoft Azure Certified **soluzione candidatura modulo**.

>[!NOTE]
> Se si lavora con un Partner Account Manager o un gestore di Partner DX, chiedere loro toonominate la soluzione per il programma di hello Azure Certified. È anche possibile scegliere toohello [Microsoft Azure Certified](http://createopportunity.azurewebsites.net) pagina Web e compilare hello form dell'applicazione. Immettere la posta elettronica hello del Partner Account Manager o gestione di Partner DX in hello **Microsoft Sponsor contattare** casella.

Se si soddisfano i criteri di idoneità hello in hello [criteri la partecipazione di Azure Marketplace](http://go.microsoft.com/fwlink/?LinkID=526833) e l'applicazione è stata approvata, è iniziare a lavorare con si tooonboard il toohello Esplora Marketplace.

### <a name="register-your-account-as-a-microsoft-seller"></a>Registrare l'account come venditore Microsoft
Registrare l'account Microsoft come [account di Microsoft Developer](marketplace-publishing-accounts-creation-registration.md).

### <a name="publish-your-solution"></a>Pubblicare la soluzione
toopublish toohello una soluzione Marketplace, seguire questi passaggi:
1. I requisiti hello tecniche.

    a. Soddisfare hello [prerequisiti tecniche](marketplace-publishing-pre-requisites.md).

    b. Soddisfare hello [prerequisiti tecnici VM](marketplace-publishing-vm-image-creation-prerequisites.md).

    c. Soddisfare hello [prerequisiti tecniche del modello di soluzione](marketplace-publishing-solution-template-creation-prerequisites.md).

2. Creare l'offerta.

    a. Creare un'offerta di [macchina virtuale](marketplace-publishing-vm-image-creation.md).

    b. Creare un'offerta del [modello di soluzione](marketplace-publishing-solution-template-creation.md).

3. Creare il [contenuto marketing](marketplace-publishing-push-to-staging.md) dell'offerta.

4. Testare l'offerta nella fase di gestione temporanea.

    a. Testare l'offerta VM [nella fase di gestione temporanea](marketplace-publishing-vm-image-test-in-staging.md).

    b. Testare l'offerta del modello di soluzione nella [fase di gestione temporanea](marketplace-publishing-solution-template-test-in-staging.md).

5. Distribuire l'offerta toohello [Marketplace](marketplace-publishing-push-to-production.md).


### <a name="create-and-manage-a-virtual-machine-image"></a>Creare e gestire un'immagine di macchina virtuale
Creare e gestire un'immagine di macchina virtuale con le risorse seguenti:
* Creare un'immagine di macchina virtuale [in locale](marketplace-publishing-vm-image-creation-on-premise.md).
* Creare una macchina virtuale in esecuzione [Windows nel portale di Azure hello](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Creare una macchina virtuale in esecuzione [Linux nel portale di Azure hello](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Risolvere problemi comuni incontrati durante la [creazione del disco rigido virtuale](marketplace-publishing-vm-image-creation-troubleshooting.md).

## <a name="manage-your-solution"></a>Gestire la soluzione
Gestire la soluzione con la Guida da hello seguenti risorse:
* [Manuale di post-produzione hello di lettura per la macchina virtuale](marketplace-publishing-vm-image-post-publishing.md)
* [L'aggiornamento dei dettagli di tecniche hello di un'offerta o di uno SKU](marketplace-publishing-vm-image-post-publishing.md#update-the-nontechnical-details-of-an-offer-or-a-sku)
* [Aggiornare i dettagli tecnici di hello di un'offerta o di uno SKU](marketplace-publishing-vm-image-post-publishing.md#update-the-technical-details-of-a-sku)
* [Aggiungere un nuovo SKU in un'offerta elencata](marketplace-publishing-vm-image-post-publishing.md#add-a-new-sku-under-a-listed-offer)
* [Modificare hello numero di dischi dati per una SKU elencati](marketplace-publishing-vm-image-post-publishing.md#change-the-data-disk-count-for-a-listed-sku)
* [Eliminare un'offerta elencata da hello Marketplace](marketplace-publishing-vm-image-post-publishing.md)
* [Eliminare un elenco di SKU dal hello Marketplace](marketplace-publishing-vm-image-post-publishing.md#delete-a-listed-sku-from-the-marketplace)
* [Elimina versione corrente di hello di uno SKU elencato da hello Marketplace](marketplace-publishing-vm-image-post-publishing.md#delete-the-current-version-of-a-listed-sku-from-the-marketplace)
* [Ripristinare l'elenco di valori dei prezzi tooproduction hello](marketplace-publishing-vm-image-post-publishing.md#revert-the-listing-price-to-production-values)
* [Ripristinare hello tooproduction valori del modello di fatturazione](marketplace-publishing-vm-image-post-publishing.md#revert-the-billing-model-to-production-values)
* [Ripristinare hello impostazione di visibilità di un valore di produzione toohello SKU elencato](marketplace-publishing-vm-image-post-publishing.md#revert-the-visibility-setting-of-a-listed-sku-to-the-production-value)
* [Visualizzare e modificare il Cloud Solution Provider "Incentivi rivenditore" in Azure Marketplace](marketplace-publishing-csp-incentive.md)
* [Informazioni sui report relativi ai proventi](marketplace-publishing-report-payout.md)
* [Ottenere supporto come editore](marketplace-publishing-get-publisher-support.md)

## <a name="additional-resources"></a>Risorse aggiuntive
[Configurare Azure PowerShell](marketplace-publishing-powershell-setup.md)
