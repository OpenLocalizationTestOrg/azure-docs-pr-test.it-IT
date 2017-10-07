---
title: aaaAzure gestite le applicazioni in hello Marketplace | Documenti Microsoft
description: Viene descritto Azure gestite le applicazioni che sono disponibili tramite hello Marketplace.
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b3cdf3f1fccdd47db699e4892ae8bce35118bfd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-in-hello-marketplace"></a>Le applicazioni in hello Marketplace gestito di Azure

 File msp, ISV e integratori di sistema (SIs) possono usare Azure gestito toooffer applicazioni ai clienti di Azure Marketplace tooall soluzioni. Tali soluzioni ridurre la manutenzione di hello e overhead di manutenzione per i clienti. I server di pubblicazione è possibile vendere infrastruttura e il software tramite hello Marketplace. È possibile collegare supporto operativo toomanaged applicazioni e servizi. Per altre informazioni, vedere [Panoramica delle applicazioni gestite di Azure](managed-application-overview.md).

In questo articolo viene illustrato un MSP, ISV o SI può pubblicare un toohello applicazione Marketplace e renderlo toocustomers ampiamente disponibili.

## <a name="prerequisites-for-publishing-a-managed-application"></a>Prerequisiti per la pubblicazione di un'applicazione gestita

Prerequisiti toolisting in hello Marketplace:

* Tecnici

    *  Per informazioni sulla struttura di base hello e la sintassi dei modelli di gestione risorse di Azure, vedere [modelli di Azure Resource Manager](resource-group-authoring-templates.md).
    *  soluzioni di tooview modello completo, vedere [modelli di avvio rapido di Azure](https://azure.microsoft.com/en-us/documentation/templates/) o hello [repository di modelli di avvio rapido](https://github.com/azure/azure-quickstart-templates).
    *  Per informazioni su come toocreate hello interfaccia per i clienti di distribuire l'applicazione tramite hello Marketplace, vedere [creare un file di definizione dell'interfaccia](managed-application-createuidefinition-overview.md).

* Non tecnici (requisiti aziendali)

    *   L'azienda o figlie devono trovarsi in un paese in cui vendite sono supportate da hello Marketplace.
    *   Il prodotto deve essere concesso in licenza in modo che sia compatibile con i modelli di fatturazione supportati da hello Marketplace.
    *   Si è responsabile di garantire il supporto tecnico disponibile toocustomers in modo commercialmente ragionevole. supporto Hello può essere disponibile, a pagamento, o tramite una community di supporto.
    *   Il partner ha la responsabilità di concedere in licenza il software e le dipendenze da software di terze parti.
    *   È necessario fornire contenuto che soddisfa i criteri per l'offerta di toobe elencato nel Marketplace hello in hello portale di Azure.
    *   È necessario accettare i termini toohello dell'accordo di server di pubblicazione e i criteri di partecipazione hello Azure Marketplace.
    *   È necessario accettare toocomply con contratto di Microsoft Azure Certified programma hello condizioni per l'utilizzo e informativa sulla Privacy di Microsoft.

## <a name="create-a-new-azure-application-offer"></a>Creare una nuova offerta di applicazione Azure

Una volta soddisfatti i prerequisiti di hello, si è pronti toocreate l'offerta di applicazione gestita. Di seguito è disponibile una breve panoramica di un'offerta e di uno SKU.

### <a name="offer"></a>Offerta

offerta Hello per un'applicazione gestita corrisponde classe tooa del prodotto offerta da un server di pubblicazione. Se si dispone di un nuovo tipo di soluzione dell'applicazione che si desidera toomake disponibile in hello Marketplace, è possibile configurarlo come una nuova offerta. Un'offerta è una raccolta di SKU. Ogni offerta viene visualizzata come proprio entità in hello Marketplace.

### <a name="sku"></a>SKU

Uno SKU è hello unità più piccola acquistabili di un'offerta. È possibile utilizzare uno SKU all'interno di hello toodifferentiate di classe (offerta) stesso prodotto tra:

* le diverse funzionalità supportate
* Se offerta hello sia gestita o meno.
* i modelli di fatturazione supportati

Uno SKU appare sotto hello padre offerta in Marketplace hello. Viene visualizzato come il proprio entità acquistabili in hello portale di Azure.

### <a name="set-up-an-offer"></a>Configurare un'offerta

1. Accedi toohello [portale per i Partner di Cloud](https://cloudpartner.azure.com/).

2. Nel riquadro di spostamento hello hello sinistra, selezionare **+ nuova offerta** > **applicazioni Azure**.

    ![Nuova offerta](./media/managed-application-author-marketplace/newOffer.png)

3. Compilare moduli hello che vengono visualizzati nel hello lasciato in hello **Editor** visualizzazione. I campi obbligatori sono contrassegnati con un asterisco rosso (*).

    ![Impostazioni dell'offerta](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    Quattro moduli principali sono utilizzati toocreate un'applicazione gestita:

    a. Impostazioni dell'offerta

    b. SKU

    c. Marketplace

    d. Supporto

Questi moduli sono descritti in dettaglio nelle sezioni che seguono hello.

## <a name="offer-settings-form"></a>Modulo delle impostazioni dell'offerta
Utilizzare le impostazioni di offerta hello toospecify questo form di base.

1. Compilare hello **offrono impostazioni** form. Hello diversi campi sono:

    a. **ID di offerta**: questo identificatore univoco identifica hello offerta all'interno di un profilo di pubblicazione. Questo ID è visibile negli URL dei prodotti, nei modelli di Resource Manager e nei report di fatturazione. Può essere composto solo da caratteri alfanumerici minuscoli o trattini (-). Hello ID non può terminare con un trattino. È limitato tooa massimo 50 caratteri. Questo campo è bloccato dopo la pubblicazione dell'offerta.

    b. **ID dell'editore**: usare questo profilo di pubblicazione riepilogo toochoose hello desiderato toopublish questa offerta in. Questo campo è bloccato dopo la pubblicazione dell'offerta.

    c. **Nome**: viene visualizzato questo nome per l'offerta in Marketplace hello e nel portale di hello. Può contenere massimo 50 caratteri. Includere un nome di marchio riconoscibile per il prodotto. Non includere il nome della società, a meno che non corrisponda al nome con cui viene commercializzato. Se si sta marketing questa offerta nel proprio sito Web, verificare che il nome hello sia esattamente come viene visualizzato nel sito Web.

2. Selezionare **salvare** toosave dello stato di avanzamento. 

## <a name="skus-form"></a>Modulo degli SKU
passaggio successivo Hello è tooadd SKU per l'offerta.

1. Selezionare **SKU** > **New SKU** (Nuovo SKU). 

    ![Selezionare il nuovo SKU](./media/managed-application-author-marketplace/newOffer_skus.png)

2. Immettere un **ID SKU**. Un ID SKU è un identificatore univoco per hello SKU all'interno di un'offerta. Questo ID è visibile negli URL dei prodotti, nei modelli di Resource Manager e nei report di fatturazione. Può essere composto solo da caratteri alfanumerici minuscoli o trattini (-). Hello ID non può terminare con un trattino, ed è limitato tooa massimo 50 caratteri. Questo campo è bloccato dopo la pubblicazione dell'offerta. All'interno di un'offerta possono essere presenti più SKU. È necessario uno SKU per ogni immagine Prevedi toopublish.

3. Compilare hello **dettagli di SKU** sezione hello seguente formato:

    ![Fornire il nuovo SKU](./media/managed-application-author-marketplace/newOffer_newsku.png)

    Compilare hello seguenti campi:
    
    a. **Title** (Titolo): immettere un titolo per lo SKU, Questa opzione è disponibile nella raccolta di hello per questo elemento.

    b. **Summary (Riepilogo)**: immettere un breve riepilogo per questo SKU, Questo testo viene visualizzato sotto il titolo di hello.

    c. **Descrizione**: immettere una descrizione dettagliata hello SKU.

    d. **Tipo SKU**: hello i valori consentiti sono **applicazione gestita** e **modelli di soluzioni**. In questo caso, selezionare **Managed Application** (Applicazione gestita).

4. Compilare hello **i dettagli del pacchetto** sezione hello seguente formato:

    ![Pacchetto](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    Compilare hello seguenti campi:

    a. **Versione corrente**: immettere una versione per il pacchetto di hello caricati. Deve essere nel formato hello `{number}.{number}.{number}{number}`.

    b. **Selezionare un file di pacchetto**: questo pacchetto contiene i seguenti file vengono compressi in un file ZIP hello:
    * **applianceMainTemplate.json**: file di modello di distribuzione hello utilizzati toodeploy hello soluzione/applicazione. Per informazioni su come file di modello di distribuzione toocreate, vedere [creare il primo modello di gestione risorse di Azure](resource-manager-create-first-template.md).
    * **appliancecreateUIDefinition.json**: questo file viene utilizzato tramite l'interfaccia hello toogenerate portale Azure hello utente che ha utilizzato tooprovision questa soluzione/applicazione. Per altre informazioni, vedere [Introduzione a CreateUiDefinition](managed-application-createuidefinition-overview.md).
    * **mainTemplate.json**: il file modello contiene solo risorse di Microsoft.Solution/appliances hello. file mainTemplate Hello include hello le proprietà seguenti:

        *  **tipo**: utilizzare **Marketplace** per le applicazioni gestite in hello Marketplace.
        *  **ManagedResourceGroupId**: il gruppo di risorse nella sottoscrizione del cliente hello è distribuite in tutte le risorse di hello definite in applianceMainTemplate.json.
        *  **PublisherPackageId**: la stringa che identifica in modo univoco il pacchetto di hello. Fornire il valore di hello in formato hello `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.

Ottenere hello **ID offerta** e **ID editore** dal portale di pubblicazione, come illustrato nella seguente immagine hello hello:

![Offer ID (ID offerta)](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
Ottenere hello **ID SKU**, come illustrato nella seguente immagine hello:

![ID SKU](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
Ottenere il pacchetto di hello **versione**, come illustrato nella seguente immagine hello:

![Versione del pacchetto](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  In base a hello precedenti esempi, hello valore **PublisherPackageId** è `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.

  mainTemplate.json di esempio:

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify hello name of hello storage account"
        }
      },
      "storageAccountType": {
        "type": "string"
      }
    },
    "variables": {
      "managedResourceGroup": "[concat(resourceGroup().id,uniquestring(resourceGroup().id))]"
    },
    "resources": [{
      "type": "Microsoft.Solutions/appliances",
      "apiVersion": "2016-09-01-preview",
      "name": "[concat(parameters('storageAccountNamePrefix'), '-', 'managed')]",
      "location": "[resourceGroup().location]",
      "kind": "marketplace",
      "properties": {
        "managedResourceGroupId": "[variables('managedResourceGroup')]",
        "PublisherPackageId":"azureappliancetest.ravmanagedapptest.ravpreviewmanagedsku.1.0.0",
        "parameters": {
          "storageAccountName": {
            "value": "[parameters('storageAccountNamePrefix')]"
          },
          "storageAccountType": {
            "value": "[parameters('storageAccountType')]"
          }
        }
      }
    }],
    "outputs": {

    }
  }
  ```

Il pacchetto deve contenere tutti i modelli annidati o gli script toosuccessfully necessario effettuare il provisioning di questa applicazione. Hello mainTemplate.json applianceMainTemplate.json e applianceCreateUIDefinition.json file devono essere presenti nella cartella radice hello.

* **Autorizzazioni**: questa proprietà definisce l'accesso e hello livello di accesso che ottiene risorse toohello nelle sottoscrizioni dei clienti. server di pubblicazione Hello utilizzarlo applicazione hello toomanage per conto cliente hello.
* **PrincipalId**: questa proprietà è l'identificatore di hello Azure Active Directory (Azure AD) di un'applicazione che ha concesso autorizzazioni determinate risorse di hello nella sottoscrizione del cliente hello, un gruppo di utenti o un utente. Definizione di ruolo Hello descritte le autorizzazioni di hello. 
* **Definizione di ruolo**: questa proprietà è un elenco di tutti i ruoli controllo di accesso basato sui ruoli (RBAC) di incorporati hello fornite da Azure AD. È possibile selezionare hello ruolo più appropriato alle risorse di hello toomanage toouse per conto cliente hello.

È possibile aggiungere più autorizzazioni. È consigliabile creare un gruppo di utenti di AD e specificare il relativo ID in **PrincipalId**. In questo modo, è possibile aggiungere più utenti toohello gruppo senza necessità di prova prova tooupdate SKU.

Per ulteriori informazioni sui ruoli, vedere [introduzione RBAC nel portale di Azure hello](../active-directory/role-based-access-control-what-is.md).

## <a name="marketplace-form"></a>Modulo Marketplace

chiede di Hello modulo Marketplace per i campi visualizzati nell'hello [Azure Marketplace](https://azuremarketplace.microsoft.com) e hello [portale di Azure](https://portal.azure.com/).

### <a name="preview-subscription-ids"></a>Preview Subscription IDs (ID sottoscrizione di anteprima)

Immettere un elenco di ID che può accedere l'offerta di hello dopo la pubblicazione di sottoscrizione di Azure. È possibile utilizzare questi offerta di sottoscrizioni elencate vuoti tootest hello visualizzato in anteprima prima di renderlo in tempo reale. È possibile compilare un elenco vuoto di too100 sottoscrizioni nel portale di partner hello.

### <a name="suggested-categories"></a>Suggested Categories (Categorie suggerite)

Selezionare le categorie di toofive dall'elenco di hello che l'offerta può essere più associato. Queste categorie sono utilizzati toomap le categorie di prodotti toohello offerta sono disponibili in hello [Azure Marketplace](https://azuremarketplace.microsoft.com) hello e [portale di Azure](https://portal.azure.com/).

#### <a name="azure-marketplace"></a>Azure Marketplace

riepilogo Hello dell'applicazione gestita Visualizza hello seguenti campi:

![Riepilogo del Marketplace](./media/managed-application-author-marketplace/publishvm10.png)

Hello **Panoramica** scheda applicazione gestita Visualizza hello seguenti campi:

![Panoramica del Marketplace](./media/managed-application-author-marketplace/publishvm11.png)

Hello **piani + prezzi** scheda applicazione gestita Visualizza hello seguenti campi:

![Piani del Marketplace](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a>Portale di Azure

riepilogo Hello dell'applicazione gestita Visualizza hello seguenti campi:

![Riepilogo del portale](./media/managed-application-author-marketplace/publishvm12.png)

Panoramica di Hello per l'applicazione gestita Visualizza hello seguenti campi:

![Panoramica del portale](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a>Linee guida per il logo

Seguire queste linee guida per qualsiasi logo che viene caricato nel portale di Partner di Cloud hello:

*   Hello progettazione di Azure dispone di una tavolozza dei colori semplice. Limita il numero di hello database primario e secondario colori sul logo.
*   colori del tema Hello del portale hello sono bianchi e neri. Non utilizzare i colori come colore di sfondo hello per il logo. Usare un colore che rende visibile nel portale di hello del logo. Si consiglia di usare colori primari semplici. *Se si utilizza uno sfondo trasparente, assicurarsi che i logo hello e testo non sono bianchi, nero o blu.*
*   Non usare uno sfondo sfumato sul logo hello.
*   Non inserire testo in logo hello, nemmeno società o nome dell'organizzazione. Hello aspetto del logo deve essere flat ed evitare le sfumature.
*   Assicurarsi che non siano stati estesi logo hello.

#### <a name="hero-logo"></a>Logo alto

logo hero Hello è facoltativo. server di pubblicazione Hello possibile scegliere di non tooupload un logo hero. Icona hero hello viene caricato, non può essere eliminata. In quel momento, partner hello deve seguire le linee guida Marketplace hello per le icone hero.

Seguire queste linee guida per l'icona del logo hero hello:

*   nome visualizzato di publisher Hello, hello piano titolo e offerta hello riepilogo lunghe vengono visualizzati in bianco. Pertanto, non utilizzare un colore chiaro per lo sfondo di hello dell'icona hero hello. Lo sfondo nero, bianco o trasparente non è ammesso per le icone del logo alto.
*   Dopo l'offerta di hello è elencato, server di pubblicazione hello il nome visualizzato, titolo piano hello, offerta hello riepilogo lunghe e hello **crea** pulsante sono incorporati a livello di codice all'interno di logo hero hello. Di conseguenza, non immettere il testo durante la progettazione logo hero hello. Lasciare spazio vuoto in hello destra perché include testo hello a livello di codice che lo spazio. spazio vuoto di Hello per testo hello deve essere 415 x 100 pixel in hello destra. Viene applicato un offset di 370 pixel da sinistra hello.

    ![Esempio di logo alto](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a>Modulo di supporto

Compilare hello **supporta** form con il supporto contatti dalla società. ad esempio le informazioni di contatto del supporto tecnico e dell'assistenza clienti.

## <a name="publish-an-offer"></a>Pubblicare un'offerta

Dopo aver specificato tutte le sezioni di hello, selezionare **pubblica** processo hello toostart che rende il toocustomers disponibili offerta.

## <a name="next-steps"></a>Passaggi successivi

* Per le applicazioni toomanaged un'introduzione, vedere [panoramica delle applicazioni gestite](managed-application-overview.md).
* Per informazioni sull'utilizzo di un'applicazione gestita da hello Marketplace, vedere [utilizzare Azure gestite le applicazioni in hello Marketplace](managed-application-consume-marketplace.md).
* Per informazioni sulla pubblicazione di un'applicazione gestita del catalogo di servizi, vedere [Creare e pubblicare un'applicazione gestita del catalogo di servizi](managed-application-publishing.md).
* Per informazioni sull'uso delle applicazioni gestite del catalogo di servizi, vedere [Utilizzare un'applicazione gestita di Azure](managed-application-consumption.md).
