---
title: Elemento FileUpload dell'interfaccia utente di Applicazione gestita di Azure | Microsoft Docs
description: Illustra l'elemento Microsoft.Common.FileUpload dell'interfaccia utente per le applicazioni gestite di Azure
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
ms.openlocfilehash: 217e9e63eb7cd198f70cee42b418867df9f1f993
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a><span data-ttu-id="3da96-103">Elemento Microsoft.Common.FileUpload dell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="3da96-103">Microsoft.Common.FileUpload UI element</span></span>
<span data-ttu-id="3da96-104">Controllo che consente a un utente di specificare uno o più file da caricare.</span><span class="sxs-lookup"><span data-stu-id="3da96-104">A control that allows a user to specify one or more files to upload.</span></span> <span data-ttu-id="3da96-105">Usare questo elemento quando si [crea un'applicazione Azure gestita](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="3da96-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="3da96-106">Esempio di interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="3da96-106">UI sample</span></span>
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a><span data-ttu-id="3da96-108">Schema</span><span class="sxs-lookup"><span data-stu-id="3da96-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="3da96-109">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="3da96-109">Remarks</span></span>
- <span data-ttu-id="3da96-110">`constraints.accept` specifica i tipi di file visualizzati nella finestra di dialogo del browser relativa ai file.</span><span class="sxs-lookup"><span data-stu-id="3da96-110">`constraints.accept` specifies the types of files that are shown in the browser's file dialog.</span></span> <span data-ttu-id="3da96-111">Per informazioni sui valori consentiti, vedere la [specifica HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept).</span><span class="sxs-lookup"><span data-stu-id="3da96-111">See the [HTML5 specification](http://www.w3.org/TR/html5/forms.html#attr-input-accept) for allowed values.</span></span> <span data-ttu-id="3da96-112">Il valore predefinito è **null**.</span><span class="sxs-lookup"><span data-stu-id="3da96-112">The default value is **null**.</span></span>
- <span data-ttu-id="3da96-113">Se la proprietà `options.multiple` è impostata su **true**, l'utente è autorizzato a selezionare più di un file nella finestra di dialogo del browser relativa ai file.</span><span class="sxs-lookup"><span data-stu-id="3da96-113">If `options.multiple` is set to **true**, the user is allowed to select more than one file in the browser's file dialog.</span></span> <span data-ttu-id="3da96-114">Il valore predefinito è **false**.</span><span class="sxs-lookup"><span data-stu-id="3da96-114">The default value is **false**.</span></span>
- <span data-ttu-id="3da96-115">Questo elemento supporta il caricamento dei file in due modalità in base al valore di `options.uploadMode`.</span><span class="sxs-lookup"><span data-stu-id="3da96-115">This element supports uploading files in two modes based on the value of `options.uploadMode`.</span></span> <span data-ttu-id="3da96-116">Se il valore **file** è specificato, l'output include i contenuti del file sotto forma di BLOB.</span><span class="sxs-lookup"><span data-stu-id="3da96-116">If **file** is specified, the output contains the contents of the file as a blob.</span></span> <span data-ttu-id="3da96-117">Se il valore **url** è specificato, il file viene caricato in una posizione temporanea e l'output contiene l'URL del BLOB.</span><span class="sxs-lookup"><span data-stu-id="3da96-117">If **url** is specified, then the file is uploaded to a temporary location, and the output contains the URL of the blob.</span></span> <span data-ttu-id="3da96-118">I BLOB temporanei verranno eliminati dopo 24 ore.</span><span class="sxs-lookup"><span data-stu-id="3da96-118">Temporary blobs will be purged after 24 hours.</span></span> <span data-ttu-id="3da96-119">Il valore predefinito è **file**.</span><span class="sxs-lookup"><span data-stu-id="3da96-119">The default value is **file**.</span></span>
- <span data-ttu-id="3da96-120">Il valore di `options.openMode` determina la modalità di lettura del file.</span><span class="sxs-lookup"><span data-stu-id="3da96-120">The value of `options.openMode` determines how the file is read.</span></span> <span data-ttu-id="3da96-121">Se si prevede che il file sia in testo normale, specificare **text**. In caso contrario, specificare **binary**.</span><span class="sxs-lookup"><span data-stu-id="3da96-121">If the file is expected to be plain text, specify **text**; else, specify **binary**.</span></span> <span data-ttu-id="3da96-122">Il valore predefinito è **text**.</span><span class="sxs-lookup"><span data-stu-id="3da96-122">The default value is **text**.</span></span>
- <span data-ttu-id="3da96-123">Se la proprietà `options.uploadMode` è impostata su **file** e `options.openMode` su **binary**, l'output avrà una codifica Base64.</span><span class="sxs-lookup"><span data-stu-id="3da96-123">If `options.uploadMode` is set to **file** and `options.openMode` is set to **binary**, the output is base64-encoded.</span></span>
- <span data-ttu-id="3da96-124">`options.encoding` specifica la codifica da usare per la lettura del file.</span><span class="sxs-lookup"><span data-stu-id="3da96-124">`options.encoding` specifies the encoding to use when reading the file.</span></span> <span data-ttu-id="3da96-125">Il valore predefinito è **UTF-8** e viene usato solo quando la proprietà `options.openMode` è impostata su **text**.</span><span class="sxs-lookup"><span data-stu-id="3da96-125">The default value is **UTF-8**, and is used only when `options.openMode` is set to **text**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="3da96-126">Output di esempio</span><span class="sxs-lookup"><span data-stu-id="3da96-126">Sample output</span></span>
<span data-ttu-id="3da96-127">Se options.multiple è false e options.uploadMode è file, l'output include i contenuti del file sotto forma di stringa JSON:</span><span class="sxs-lookup"><span data-stu-id="3da96-127">If options.multiple is false and options.uploadMode is file, then the output contains the contents of the file as a JSON string:</span></span>

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

<span data-ttu-id="3da96-128">Se options.multiple è true e options.uploadMode è file, l'output include i contenuti del file sotto forma di matrice JSON:</span><span class="sxs-lookup"><span data-stu-id="3da96-128">If options.multiple is true and\`options.uploadMode is file, then the output contains the contents of the files as a JSON array:</span></span>

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

<span data-ttu-id="3da96-129">Se options.multiple è false e options.uploadMode è url, l'output include un URL sotto forma di stringa JSON:</span><span class="sxs-lookup"><span data-stu-id="3da96-129">If options.multiple is false and options.uploadMode is url, then the output contains a URL as a JSON string:</span></span>

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

<span data-ttu-id="3da96-130">Se options.multiple è true e options.uploadMode è url, l'output include un elenco di URL sotto forma di matrice JSON:</span><span class="sxs-lookup"><span data-stu-id="3da96-130">If options.multiple is true and options.uploadMode is url, then the output contains a list of URLs as a JSON array:</span></span>
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

<span data-ttu-id="3da96-131">Durante il test di CreateUiDefinition, alcuni browser, ad esempio Google Chrome, troncano gli URL generati dall'elemento Microsoft.Common.FileUpload nella console del browser.</span><span class="sxs-lookup"><span data-stu-id="3da96-131">When testing a CreateUiDefinition, some browsers (like Google Chrome) truncate URLs generated by the Microsoft.Common.FileUpload element in the browser console.</span></span> <span data-ttu-id="3da96-132">Potrebbe essere necessario fare clic con il pulsante destro del mouse sui singoli collegamenti per copiare gli URL completi.</span><span class="sxs-lookup"><span data-stu-id="3da96-132">You may need to right-click individual links to copy the full URLs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3da96-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3da96-133">Next steps</span></span>
* <span data-ttu-id="3da96-134">Per un'introduzione alle applicazioni gestite, vedere [Panoramica di Applicazione gestita di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3da96-134">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="3da96-135">Per un'introduzione alla creazione delle definizioni dell'interfaccia utente, vedere [Introduzione a CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3da96-135">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="3da96-136">Per una descrizione delle proprietà comuni negli elementi dell'interfaccia utente, vedere [Elementi di CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="3da96-136">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
