---
title: aaaCreate elementi personalizzati per la macchina virtuale Labs DevTest | Documenti Microsoft
description: Informazioni su come tooauthor i propri elementi per utilizzano con DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 32dcdc61-ec23-4a01-b731-78c029ea5316
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 2bd603bc1241ca6b669a3a276a677729514f0df2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a>Creare elementi personalizzati per le macchine virtuali di lab di sviluppo e test
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a>Panoramica
**Elementi** vengono utilizzati toodeploy e configurare l'applicazione dopo il provisioning di una macchina virtuale. Un elemento è costituito da un file di definizione dell’elemento e altri file di script archiviati in una cartella in un archivio git. I file di definizione degli elementi costituiti da JSON e le espressioni che è possibile utilizzare toospecify si desidera tooinstall in una macchina virtuale. Ad esempio, è possibile definire il nome di hello artefatto, toorun comando e i parametri che vengono resi disponibili quando si esegue il comando hello. È possibile fare riferimento a file di script tooother nel file di definizione di artefatto hello in base al nome.

## <a name="artifact-definition-file-format"></a>Formato del file di definizione dell’elemento
Hello riportato di seguito nelle sezioni hello che costituiscono hello struttura di base di un file di definizione:

    {
      "$schema": "https://raw.githubusercontent.com/Azure/azure-devtestlab/master/schemas/2016-11-28/dtlArtifacts.json",
      "title": "",
      "description": "",
      "iconUri": "",
      "targetOsType": "",
      "parameters": {
        "<parameterName>": {
          "type": "",
          "displayName": "",
          "description": ""
        }
      },
      "runCommand": {
        "commandToExecute": ""
      }
    }

| Nome dell'elemento | Obbligatorio? | Descrizione |
| --- | --- | --- |
| $schema |No |Percorso del file di schema JSON hello che aiuta a test di validità hello hello del file di definizione. |
| title |Sì |Nome dell'elemento hello visualizzato in lab hello. |
| description |Sì |Descrizione dell'elemento hello visualizzato in lab hello. |
| iconUri |No |URI dell'icona hello visualizzata nell'ambiente lab hello. |
| targetOsType |Sì |Sistema operativo della macchina virtuale in cui è installato artefatto hello. Opzioni supportate: Windows e Linux. |
| parameters |No |Valori forniti quando viene eseguito il comando di installazione dell’elemento in un computer. Ciò consente di personalizzare l'elemento. |
| runCommand |Sì |Il comando di installazione dell’elemento che viene eseguito in una macchina virtuale. |

### <a name="artifact-parameters"></a>Parametri dell'elemento
Nella sezione parametri di hello hello del file di definizione, specificare i valori che un utente può immettere durante l'installazione di un elemento. È possibile fare riferimento a valori toothese nel comando di installazione di hello artefatto.

Definire i parametri con hello seguente struttura:

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| Nome dell'elemento | Obbligatorio? | Descrizione |
| --- | --- | --- |
| type |Sì |Tipo di valore del parametro. Vedere hello seguente elenco di tipi consentito hello: |
| displayName |Sì |Nome del parametro hello che viene visualizzato tooa utente nell'ambiente lab hello. | |
| description |Sì |Descrizione del parametro hello che viene visualizzato nell'ambiente lab hello. |

Hello tipi consentiti sono:

* string: tutte le stringhe JSON valide
* int: tutti i valori integer JSON validi
* bool: tutti i valori booleani JSON validi
* array: tutte le matrici JSON valide

## <a name="artifact-expressions-and-functions"></a>Espressioni e funzioni dell’elemento
È possibile utilizzare l'espressione e artefatto hello tooconstruct di funzioni di comando di installazione.
Le espressioni sono racchiusi tra parentesi quadre ([e]) e vengono valutate quando l'elemento hello è installato. Le espressioni possono trovarsi in qualsiasi punto in un valore stringa JSON e restituiscono sempre un altro valore JSON. Se è necessario che una stringa letterale che inizia con una parentesi quadra toouse [, è necessario utilizzare due parentesi quadre [[.
In genere, si usano espressioni con funzioni tooconstruct un valore. Proprio come in JavaScript, le chiamate di funzione sono formattate come functionName(arg1,arg2,arg3).

Hello elenco seguente mostra le funzioni comuni:

* Parameters(ParameterName) - restituisce un valore di parametro fornito durante l'esecuzione del comando artefatto hello.
* concat(arg1,arg2,arg3, …..) -     Combina più valori di stringa. Questa funzione può accettare qualsiasi numero di argomenti.

Hello seguente esempio viene illustrato come toouse tooconstruct un valore di espressione e funzioni:

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a>Creare un elemento personalizzato
Creare l'elemento personalizzato eseguendo questi passaggi:

1. Installare un editor di JSON, è necessario un toowork editor JSON con i file di definizione degli elementi. Si consiglia di utilizzare [Visual Studio Code](https://code.visualstudio.com/), che è disponibile per Windows, Linux e OS X.
2. Get artifactfile.json un esempio - estrazione degli elementi di hello creati dal team di Azure DevTest Labs al nostro [repository GitHub](https://github.com/Azure/azure-devtestlab), in cui è stata creata una libreria completa di elementi che consentono di creano i propri elementi. Scaricare un file di definizione di artefatto e apportare le modifiche tooit toocreate i propri elementi.
3. Avvalersi di IntelliSense - usare IntelliSense toosee elementi validi che possono essere utilizzati tooconstruct un file di definizione dell'elemento. È inoltre possibile visualizzare diverse opzioni hello per i valori di un elemento. Ad esempio, IntelliSense Mostra, si hello disponibili due opzioni di Windows o Linux durante la modifica di hello **targetOsType** elemento.
4. Elemento hello Store in un [repository git](devtest-lab-add-artifact-repo.md).
   
   1. Creare una directory distinta per ogni elemento in cui il nome di directory hello è hello stesso come il nome dell'artefatto hello.
   2. Archiviare i file di definizione di artefatto hello (artifactfile.json) nella directory di hello che è stato creato.
   3. Comando di installazione script hello archivio che fanno riferimento all'elemento hello.
      
      Di seguito è riportato un esempio di come potrebbe apparire una cartella di elementi:
      
      ![Esempio di archivio git dell’elemento](./media/devtest-lab-artifact-author/git-repo.png)
5. Aggiungere lab toohello repository di artefatti hello - vedere l'articolo toohello [aggiungere un repository Git per gli elementi e i modelli](devtest-lab-add-artifact-repo.md).

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a>Articoli correlati
* [Modalità errori artefatto toodiagnose in DevTest Labs](devtest-lab-troubleshoot-artifact-failure.md)
* [Aggiungere un dominio di Active Directory utilizzando un modello di gestione delle risorse in Azure DevTest Labs di tooexisting VM](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[aggiungere laboratorio tooa repository Git artefatto](devtest-lab-add-artifact-repo.md).

