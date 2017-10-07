---
title: la creazione di definizione dell'interfaccia utente per le applicazioni gestite Azure aaaUnderstand | Documenti Microsoft
description: Viene descritto come definizioni dell'interfaccia utente toocreate per le applicazioni gestite di Azure
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/11/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: d53ddf438c24d5a6cb8dd53ca0b4694ab0462515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-createuidefinition"></a>Introduzione a CreateUiDefinition
Questo documento introduce i concetti di base hello di un CreateUiDefinition, utilizzato dall'interfaccia utente di hello toogenerate portale Azure hello per la creazione di un'applicazione gestita.

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

CreateUiDefinition contiene sempre tre proprietà: 

* handler
* version
* parameters

Per le applicazioni gestite, deve essere sempre gestore `Microsoft.Compute.MultiVm`, e la versione più recente supportato hello è `0.1.2-preview`.

schema Hello di proprietà parametri hello dipende dalla combinazione di hello del gestore specificato hello e versione. Per le applicazioni gestite, proprietà hello supportato sono `basics`, `steps`, e `outputs`. Nozioni di base e passaggi proprietà Hello contengono hello _elementi_ , ad esempio caselle di testo ed elenchi a discesa - toobe visualizzati in hello portale di Azure. output di Hello è toomap utilizzati valori di output di hello di hello elementi specificati toohello parametri di modello di distribuzione Azure Resource Manager hello.

L'inclusione di `$schema` è consigliata ma facoltativa. Se specificato, hello valore per `version` deve corrispondere una versione di hello hello `$schema` URI.

## <a name="basics"></a>Nozioni di base
Hello nozioni di base è sempre hello primo passaggio della procedura guidata hello generata hello portale di Azure analizza un CreateUiDefinition. Inoltre specificare gli elementi di hello toodisplaying `basics`, portale hello inserisce elementi per la sottoscrizione di hello toochoose gli utenti, gruppo di risorse e posizione per la distribuzione di hello. In genere, gli elementi che eseguono query per i parametri a livello di distribuzione, ad esempio hello nome delle credenziali di un cluster o un amministratore, devono andare in questo passaggio.

Se il comportamento di un elemento dipende dalla sottoscrizione, gruppo di risorse o percorso dell'utente hello, tale elemento può essere utilizzato in Nozioni di base. Ad esempio, **Microsoft.Compute.SizeSelector** varia a seconda sottoscrizione e il percorso toodetermine hello elenco dell'utente hello di dimensioni disponibili. È quindi possibile usare **Microsoft.Compute.SizeSelector** solo nelle proprietà steps. In genere, solo gli elementi in hello **Microsoft.Common** dello spazio dei nomi può essere usato in Nozioni di base. Anche se alcuni elementi in altri spazi dei nomi (ad esempio **Microsoft.Compute.Credentials**) che non dipendono dal contesto dell'utente hello, sono ancora consentiti.

## <a name="steps"></a>Passi
proprietà passaggi Hello può contenere zero o più toodisplay passaggi aggiuntivi dopo nozioni di base, ognuno dei quali contiene uno o più elementi. È possibile aggiungere passaggi per ogni ruolo o a livello di applicazione hello da distribuire. Ad esempio, è possibile aggiungere un passaggio per gli input per i nodi master hello e un passaggio per i nodi di lavoro hello in un cluster.

## <a name="outputs"></a>outputs
portale di Azure Hello utilizza hello `outputs` gli elementi di proprietà toomap da `basics` e `steps` toohello parametri di modello di distribuzione Azure Resource Manager hello. Hello chiavi del dizionario sono nomi di hello hello dei parametri di modello e i valori hello sono proprietà degli oggetti di output di hello dagli elementi hello a cui fa riferimento.

## <a name="functions"></a>Funzioni
Simile troppo[funzioni di modello](resource-group-template-functions.md) in Gestione risorse di Azure (entrambi nella sintassi e la funzionalità), CreateUiDefinition fornisce funzioni per l'utilizzo degli elementi input e output, nonché le funzionalità, ad esempio istruzioni condizionali.

## <a name="next-steps"></a>Passaggi successivi
CreateUiDefinition ha uno schema semplice, profondità di reale Hello di esso viene fornito da tutti gli elementi di hello è supportato e funzioni, quali hello documenti seguenti descrivono in modo dettagliato wondrous:

- [Elementi](managed-application-createuidefinition-elements.md)
- [Funzioni](managed-application-createuidefinition-functions.md)

Per uno schema JSON corrente per CreateUiDefinition, vedere qui: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json. 

Nelle versioni successive è disponibile in hello nello stesso percorso. Sostituire hello `0.1.2-preview` parte dell'URL di hello e hello `version` valore con l'identificatore di versione di hello intendi toouse. gli identificatori di versione di Hello attualmente supportato sono `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, e `0.1.2-preview`.
