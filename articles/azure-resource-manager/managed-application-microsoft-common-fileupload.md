---
title: elemento gestita dell'interfaccia utente dell'applicazione FileUpload aaaAzure | Documenti Microsoft
description: Descrive l'elemento dell'interfaccia utente Microsoft.Common.FileUpload hello per le applicazioni gestite di Azure
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 7af5bec992e3f120afb1bdf56d8b4c19a8e5e834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a><span data-ttu-id="99bec-103">Elemento Microsoft.Common.FileUpload dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="99bec-103">Microsoft.Common.FileUpload UI element</span></span>
<span data-ttu-id="99bec-104">Un controllo che consente a un utente toospecify uno o più file tooupload.</span><span class="sxs-lookup"><span data-stu-id="99bec-104">A control that allows a user toospecify one or more files tooupload.</span></span> <span data-ttu-id="99bec-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="99bec-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="99bec-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="99bec-106">UI sample</span></span>
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a><span data-ttu-id="99bec-108">Schema</span><span class="sxs-lookup"><span data-stu-id="99bec-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.FileUpload",
  "label": "Some file upload",
  "toolTip": "",
  "constraints": {
    "required": true,
    "accept": ".doc,.docx,.xml,application/msword"
  },
  "options": {
    "multiple": false,
    "uploadMode": "file",
    "openMode": "text",
    "encoding": "UTF-8"
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="99bec-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="99bec-109">Remarks</span></span>
- <span data-ttu-id="99bec-110">`constraints.accept`Specifica i tipi di file vengono visualizzati nella finestra di dialogo del browser hello file hello.</span><span class="sxs-lookup"><span data-stu-id="99bec-110">`constraints.accept` specifies hello types of files that are shown in hello browser's file dialog.</span></span> <span data-ttu-id="99bec-111">Vedere hello [specifica HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept) per i valori consentiti.</span><span class="sxs-lookup"><span data-stu-id="99bec-111">See hello [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span></span> <span data-ttu-id="99bec-112">valore predefinito di Hello è **null**.</span><span class="sxs-lookup"><span data-stu-id="99bec-112">hello default value is **null**.</span></span>
- <span data-ttu-id="99bec-113">Se `options.multiple` è troppo**true**, hello autorizzato tooselect più di un file nella finestra di dialogo del browser hello file.</span><span class="sxs-lookup"><span data-stu-id="99bec-113">If `options.multiple` is set too**true**, hello user is allowed tooselect more than one file in hello browser's file dialog.</span></span> <span data-ttu-id="99bec-114">valore predefinito di Hello è **false**.</span><span class="sxs-lookup"><span data-stu-id="99bec-114">hello default value is **false**.</span></span>
- <span data-ttu-id="99bec-115">Questo elemento consente di caricare file in due modalità in base al valore di hello di `options.uploadMode`.</span><span class="sxs-lookup"><span data-stu-id="99bec-115">This element supports uploading files in two modes based on hello value of `options.uploadMode`.</span></span> <span data-ttu-id="99bec-116">Se **file** viene specificato, l'output di hello hello contenuto del file hello come blob.</span><span class="sxs-lookup"><span data-stu-id="99bec-116">If **file** is specified, hello output contains hello contents of hello file as a blob.</span></span> <span data-ttu-id="99bec-117">Se **url** viene specificato, il file hello è percorso temporaneo tooa caricato e output di hello contiene hello URL del blob hello.</span><span class="sxs-lookup"><span data-stu-id="99bec-117">If **url** is specified, then hello file is uploaded tooa temporary location, and hello output contains hello URL of hello blob.</span></span> <span data-ttu-id="99bec-118">I BLOB temporanei verranno eliminati dopo 24 ore.</span><span class="sxs-lookup"><span data-stu-id="99bec-118">Temporary blobs will be purged after 24 hours.</span></span> <span data-ttu-id="99bec-119">valore predefinito di Hello è **file**.</span><span class="sxs-lookup"><span data-stu-id="99bec-119">hello default value is **file**.</span></span>
- <span data-ttu-id="99bec-120">valore di Hello `options.openMode` determina la modalità di lettura file hello.</span><span class="sxs-lookup"><span data-stu-id="99bec-120">hello value of `options.openMode` determines how hello file is read.</span></span> <span data-ttu-id="99bec-121">Se il file hello è testo normale previsto toobe, specificare **testo**; in caso contrario, specificare **binario**.</span><span class="sxs-lookup"><span data-stu-id="99bec-121">If hello file is expected toobe plain text, specify **text**; else, specify **binary**.</span></span> <span data-ttu-id="99bec-122">valore predefinito di Hello è **testo**.</span><span class="sxs-lookup"><span data-stu-id="99bec-122">hello default value is **text**.</span></span>
- <span data-ttu-id="99bec-123">Se `options.uploadMode` è troppo**file** e `options.openMode` è troppo**binario**, output di hello è con codifica base64.</span><span class="sxs-lookup"><span data-stu-id="99bec-123">If `options.uploadMode` is set too**file** and `options.openMode` is set too**binary**, hello output is base64-encoded.</span></span>
- <span data-ttu-id="99bec-124">`options.encoding`Specifica toouse codifica hello durante la lettura del file hello.</span><span class="sxs-lookup"><span data-stu-id="99bec-124">`options.encoding` specifies hello encoding toouse when reading hello file.</span></span> <span data-ttu-id="99bec-125">valore predefinito di Hello è **UTF-8**e viene utilizzato solo quando `options.openMode` è troppo**testo**.</span><span class="sxs-lookup"><span data-stu-id="99bec-125">hello default value is **UTF-8**, and is used only when `options.openMode` is set too**text**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="99bec-126">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="99bec-126">Sample output</span></span>
<span data-ttu-id="99bec-127">Se è false options.multiple e options.uploadMode è file, l'output contiene contenuto hello del file hello come una stringa JSON:</span><span class="sxs-lookup"><span data-stu-id="99bec-127">If options.multiple is false and options.uploadMode is file, then the output contains hello contents of hello file as a JSON string:</span></span>

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

<span data-ttu-id="99bec-128">Se è true options.multiple and'options.uploadMode è file, quindi l'output contiene contenuto hello del file hello come matrice JSON:</span><span class="sxs-lookup"><span data-stu-id="99bec-128">If options.multiple is true and\`options.uploadMode is file, then the output contains hello contents of hello files as a JSON array:</span></span>

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

<span data-ttu-id="99bec-129">Se options.multiple è false e options.uploadMode è url, l'output include un URL sotto forma di stringa JSON:</span><span class="sxs-lookup"><span data-stu-id="99bec-129">If options.multiple is false and options.uploadMode is url, then the output contains a URL as a JSON string:</span></span>

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

<span data-ttu-id="99bec-130">Se options.multiple è true e options.uploadMode è url, l'output include un elenco di URL sotto forma di matrice JSON:</span><span class="sxs-lookup"><span data-stu-id="99bec-130">If options.multiple is true and options.uploadMode is url, then the output contains a list of URLs as a JSON array:</span></span>
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

<span data-ttu-id="99bec-131">Quando si testa un CreateUiDefinition, alcuni browser (ad esempio Google Chrome) troncare URL generati dall'elemento Microsoft.Common.FileUpload hello nella console del browser hello.</span><span class="sxs-lookup"><span data-stu-id="99bec-131">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by hello Microsoft.Common.FileUpload element in hello browser console.</span></span> <span data-ttu-id="99bec-132">Potrebbe essere URL completi di clic tooright singoli collegamenti toocopy hello.</span><span class="sxs-lookup"><span data-stu-id="99bec-132">You may need tooright-click individual links toocopy hello full URLs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="99bec-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="99bec-133">Next steps</span></span>
* <span data-ttu-id="99bec-134">Per le applicazioni toomanaged un'introduzione, vedere [Panoramica applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="99bec-134">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="99bec-135">Le definizioni di interfaccia utente toocreating un'introduzione, vedere [introduzione CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="99bec-135">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="99bec-136">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="99bec-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
