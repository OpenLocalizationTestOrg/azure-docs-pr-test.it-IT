---
title: aaaAzure funzioni di definizione dell'interfaccia utente di creare applicazioni gestite | Documenti Microsoft
description: Viene descritto toouse funzioni hello durante la costruzione di definizioni dell'interfaccia utente per le applicazioni gestite di Azure
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
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: a34c6202372168cda769c471b1c9fdd539dd0f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-elements"></a>Elementi di CreateUiDefinition
Questo articolo descrive lo schema di hello e proprietà per tutti gli elementi supportati di un CreateUiDefinition. Usare questi elementi quando si [crea un'applicazione Azure gestita](managed-application-publishing.md). schema di Hello per la maggior parte degli elementi è come segue:

```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Keep calm and visit hello [Azure Portal](portal.azure.com).",
  "constraints": {},
  "options": {},
  "visible": true
}
```
| Proprietà | Obbligatorio | Description |
| -------- | -------- | ----------- |
| name | Sì | Un identificatore interno tooreference un'istanza specifica di un elemento. Hello utilizzo più comune di nome dell'elemento hello è `outputs`, in cui i valori di output di hello di hello specificata elementi sono mappate toohello parametri del modello di hello. È possibile anche utilizzare il valore di output di hello toobind di toohello un elemento `defaultValue` di un altro elemento. |
| type | Sì | Hello toorender di controllo dell'interfaccia utente per l'elemento hello. Per un elenco di tipi supportati, vedere [Elementi](#elements). |
| label | Sì | Hello visualizzare il testo dell'elemento hello. Alcuni tipi di elemento contengono più etichette, pertanto il valore di hello potrebbe essere un oggetto che contiene più stringhe. |
| defaultValue | No | valore predefinito di Hello dell'elemento hello. Alcuni tipi di elemento supportano i valori predefiniti complessa, pertanto il valore di hello potrebbe essere un oggetto. |
| toolTip | No | toodisplay di testo Hello nella descrizione hello dell'elemento hello. Simile troppo`label`, alcuni elementi supportano più stringhe di comando dello strumento. I collegamenti inline possono essere incorporati tramite la sintassi di markdown.
| constraints | No | Una o più proprietà di comportamento di convalida di hello toocustomize utilizzati dell'elemento hello. proprietà Hello è supportato per i vincoli variano in base a tipo di elemento. Alcuni tipi di elemento non supporta la personalizzazione del comportamento di convalida hello e pertanto non dispone di alcuna proprietà di vincoli. |
| options | No | Proprietà aggiuntive che consentono di personalizzare il comportamento di hello dell'elemento hello. Simile troppo`constraints`, proprietà hello supportato variano dal tipo di elemento. |
| visible | No | Indica se l'elemento hello viene visualizzato. Se `true`, elemento hello e gli elementi figlio applicabili vengono visualizzati. valore predefinito di Hello è `true`. Utilizzare [funzioni logiche](managed-application-createuidefinition-functions.md#logical-functions) toodynamically controllare questo valore della proprietà.

## <a name="elements"></a>Elementi

Hello documentazione per ogni elemento contiene un esempio dell'interfaccia utente, schema, la sezione Osservazioni sul comportamento di hello dell'elemento hello (in genere per quanto riguarda la convalida e la personalizzazione supportata) e output di esempio.

- [Microsoft.Common.DropDown](managed-application-microsoft-common-dropdown.md)
- [Microsoft.Common.FileUpload](managed-application-microsoft-common-fileupload.md)
- [Microsoft.Common.OptionsGroup](managed-application-microsoft-common-optionsgroup.md)
- [Microsoft.Common.PasswordBox](managed-application-microsoft-common-passwordbox.md)
- [Microsoft.Common.Section](managed-application-microsoft-common-section.md)
- [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md)
- [Microsoft.Compute.CredentialsCombo](managed-application-microsoft-compute-credentialscombo.md)
- [Microsoft.Compute.SizeSelector](managed-application-microsoft-compute-sizeselector.md)
- [Microsoft.Compute.UserNameTextBox](managed-application-microsoft-compute-usernametextbox.md)
- [Microsoft.Network.PublicIpAddressCombo](managed-application-microsoft-network-publicipaddresscombo.md)
- [Microsoft.Network.VirtualNetworkCombo](managed-application-microsoft-network-virtualnetworkcombo.md)
- [Microsoft.Storage.MultiStorageAccountCombo](managed-application-microsoft-storage-multistorageaccountcombo.md)
- [Microsoft.Storage.StorageAccountSelector](managed-application-microsoft-storage-storageaccountselector.md)

## <a name="next-steps"></a>Passaggi successivi
* Per le applicazioni toomanaged un'introduzione, vedere [Panoramica applicazione gestita di Azure](managed-application-overview.md).
* Le definizioni di interfaccia utente toocreating un'introduzione, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).
