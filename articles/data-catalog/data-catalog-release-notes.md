---
title: Note sulla versione di Azure Data Catalog | Documentazione Microsoft
description: Note sulla versione del Catalogo dati di Azure.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: d3db9bee0558cac5fb4f5b8fb4ab67a35ce0f141
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-data-catalog-release-notes"></a><span data-ttu-id="d1c15-103">Note sulla versione del Catalogo dati di Azure</span><span class="sxs-lookup"><span data-stu-id="d1c15-103">Azure Data Catalog release notes</span></span>
## <a name="notes-for-the-november-20-2015-release-of-azure-data-catalog"></a><span data-ttu-id="d1c15-104">Note per la versione del 20 novembre 2015 del Catalogo dati di Azure</span><span class="sxs-lookup"><span data-stu-id="d1c15-104">Notes for the November 20, 2015 release of Azure Data Catalog</span></span>
### <a name="opening-data-sources-in-power-bi-desktop"></a><span data-ttu-id="d1c15-105">Apertura di origini di dati in Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="d1c15-105">Opening Data Sources in Power BI Desktop</span></span>
<span data-ttu-id="d1c15-106">Quando si utilizza l'opzione "Apri in Power BI Desktop" dal portale **Catalogo dati di Azure** , gli utenti potrebbero rilevare uno dei due problemi dell'applicazione Power BI Desktop:</span><span class="sxs-lookup"><span data-stu-id="d1c15-106">When using the "Open in Power BI Desktop" option from the **Azure Data Catalog** portal, users may encounter one of two problems in the Power BI Desktop application:</span></span>

* <span data-ttu-id="d1c15-107">Viene visualizzata una finestra di dialogo con il titolo "Impossibile aprire il documento"</span><span class="sxs-lookup"><span data-stu-id="d1c15-107">A dialog box with the title "Unable to Open Document" is displayed</span></span>
* <span data-ttu-id="d1c15-108">L'applicazione Power BI Desktop si apre, ma il file sembra vuoto</span><span class="sxs-lookup"><span data-stu-id="d1c15-108">The Power BI Desktop application opens, but the file appears to be empty</span></span>

<span data-ttu-id="d1c15-109">Per ogni situazione, il problema può essere risolto scaricando e installando la versione più recente di Power BI Desktop da [PowerBI.com](https://powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="d1c15-109">For each situation, the problem can be resolved by downloading and installing the latest version of Power BI Desktop from [PowerBI.com](https://powerbi.com).</span></span>

## <a name="notes-for-the-november-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="d1c15-110">Note per la versione del 13 novembre 2015 del Catalogo dati di Azure</span><span class="sxs-lookup"><span data-stu-id="d1c15-110">Notes for the November 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-to-teradata"></a><span data-ttu-id="d1c15-111">Registrazione e connessione a Teradata</span><span class="sxs-lookup"><span data-stu-id="d1c15-111">Registering and connecting to Teradata</span></span>
<span data-ttu-id="d1c15-112">Per la connessione alle origini dati di Teradata, gli utenti devono installare i driver Teradata ODBC corretti che corrispondono al numero di bit (32 bit o 64 bit) del software in uso.</span><span class="sxs-lookup"><span data-stu-id="d1c15-112">When connecting to Teradata data sources users must have installed the correct Teradata ODBC driver that match the bitness (32-bit or 64-bit) of the software being used.</span></span>

<span data-ttu-id="d1c15-113">A questa data di rilascio di ADC, il più recente [driver Teradata ODBC per windows (versione 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) è compatibile con Office 2013, ma non con Office 2016.</span><span class="sxs-lookup"><span data-stu-id="d1c15-113">As of this ADC release date, the most recent [Teradata ODBC driver for windows ( version 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) is compatible with Office 2013, but not with Office 2016.</span></span>

## <a name="notes-for-the-july-13-2015-release-of-azure-data-catalog"></a><span data-ttu-id="d1c15-114">Note per la versione del 13 luglio 2015 del Catalogo dati di Azure</span><span class="sxs-lookup"><span data-stu-id="d1c15-114">Notes for the July 13, 2015 release of Azure Data Catalog</span></span>
### <a name="registering-and-connecting-to-oracle-database"></a><span data-ttu-id="d1c15-115">Registrazione e connessione al database Oracle</span><span class="sxs-lookup"><span data-stu-id="d1c15-115">Registering and connecting to Oracle Database</span></span>
<span data-ttu-id="d1c15-116">Per la connessione alle origini dati del Database Oracle, gli utenti devono installare i driver Oracle corretti che corrispondono al numero di bit (32 bit o 64 bit) del software in uso.</span><span class="sxs-lookup"><span data-stu-id="d1c15-116">When connecting to Oracle Database data sources users must have installed the correct Oracle drivers that match the bitness (32-bit or 64-bit) of the software being used.</span></span>

* <span data-ttu-id="d1c15-117">Per la registrazione delle origini dati di Oracle in un computer che esegue Windows a 32 bit, verranno usati i driver di Oracle a 32 bit</span><span class="sxs-lookup"><span data-stu-id="d1c15-117">When registering Oracle data sources on a computer running 32-bit Windows, the 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="d1c15-118">Per la registrazione delle origini dati di Oracle in un computer che esegue Windows a 64 bit, verranno usati i driver di Oracle a 64 bit</span><span class="sxs-lookup"><span data-stu-id="d1c15-118">When registering Oracle data sources on a computer running 64-bit Windows, the 64-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="d1c15-119">Per la connessione alle origini dati di Oracle tramite Excel in un computer che esegue la versione a 32 bit di Microsoft Office, incluso in Windows a 64 bit, verranno usati i driver di Oracle a 32 bit</span><span class="sxs-lookup"><span data-stu-id="d1c15-119">When connecting to Oracle data sources using Excel on a computer running the 32-bit version of Microsoft Office, including on 64-bit Windows, the 32-bit Oracle drivers will be used</span></span>
* <span data-ttu-id="d1c15-120">Per la connessione alle origini dati di Oracle tramite Excel in un computer che esegue la versione a 64 bit di Microsoft Office, verranno usati i driver di Oracle a 64 bit</span><span class="sxs-lookup"><span data-stu-id="d1c15-120">When connecting to Oracle data sources using Excel on a computer running the 64-bit version of Microsoft Office, the 64-bit Oracle drivers will be used</span></span>

### <a name="registering-and-connecting-to-sql-server-reporting-services"></a><span data-ttu-id="d1c15-121">Registrazione e la connessione a SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="d1c15-121">Registering and connecting to SQL Server Reporting Services</span></span>
<span data-ttu-id="d1c15-122">Attualmente il supporto per le origini dati di SQL Server Reporting Services (SSRS) è limitato al server in modalità nativa.</span><span class="sxs-lookup"><span data-stu-id="d1c15-122">Support for SQL Server Reporting Services (SSRS) data sources is currently limited to Native Mode servers only.</span></span> <span data-ttu-id="d1c15-123">Il supporto per SSRS in modalità SharePoint verrà aggiunto in una versione successiva.</span><span class="sxs-lookup"><span data-stu-id="d1c15-123">Support for SSRS in SharePoint mode will be added in a later release.</span></span>

### <a name="opening-data-assets-in-excel"></a><span data-ttu-id="d1c15-124">Apertura degli asset di dati in Excel</span><span class="sxs-lookup"><span data-stu-id="d1c15-124">Opening data assets in Excel</span></span>
<span data-ttu-id="d1c15-125">Quando si aprono asset di dati in Microsoft Excel dal portale di **Azure Data Catalog**, potrebbe essere visualizzata agli utenti una finestra di dialogo con un **avviso di sicurezza di Microsoft Excel**.</span><span class="sxs-lookup"><span data-stu-id="d1c15-125">When opening data assets in Microsoft Excel from the **Azure Data Catalog** portal, users may be prompted with a **Microsoft Excel Security Notice** dialog box.</span></span> <span data-ttu-id="d1c15-126">È un comportamento standard e previsto e gli utenti possono selezionare **Abilita** per continuare.</span><span class="sxs-lookup"><span data-stu-id="d1c15-126">This is standard, expected behavior, and users can select **Enable** to continue.</span></span>

<span data-ttu-id="d1c15-127">Per altre informazioni, vedere [Attivazione o disattivazione degli avvisi di protezione relativi ai collegamenti a siti Web sospetti e a file scaricati da tali siti](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span><span class="sxs-lookup"><span data-stu-id="d1c15-127">For more information, see [Enable or disable security alerts about links and files from suspicious websites](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).</span></span>

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a><span data-ttu-id="d1c15-128">Configurazione di proxy e criteri e registrazione dell'origine dati</span><span class="sxs-lookup"><span data-stu-id="d1c15-128">Proxy and policy configuration and data source registration</span></span>
<span data-ttu-id="d1c15-129">È possibile che si verifichi una situazione in cui gli utenti possono accedere al portale del Catalogo dati di Azure, ma, quando tentano di accedere allo strumento di registrazione dell'origine dati, viene restituito un messaggio di errore che impedisce l'accesso.</span><span class="sxs-lookup"><span data-stu-id="d1c15-129">Users may encounter a situation where they can log on to the Azure Data Catalog portal, but when they attempt to log on to the data source registration tool they encounter an error message that prevents them from logging on.</span></span>

<span data-ttu-id="d1c15-130">Le possibili cause di questo comportamento problematico sono due:</span><span class="sxs-lookup"><span data-stu-id="d1c15-130">There are two potential causes for this problem behavior:</span></span>

<span data-ttu-id="d1c15-131">**Causa 1: la configurazione di Active Directory Federation Services** Lo strumento di registrazione dell'origine dati usa l'autenticazione basata su form per convalidare gli accessi degli utenti in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d1c15-131">**Cause 1: Active Directory Federation Services configuration** The data source registration tool uses Forms Authentication to validate user logons against Active Directory.</span></span> <span data-ttu-id="d1c15-132">Per accedere, l'autenticazione basata su form deve essere abilitata nei criteri di autenticazione globali da un amministratore di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d1c15-132">For successful logon, Forms Authentication must be enabled in the Global Authentication Policy by an Active Directory administrator.</span></span>

<span data-ttu-id="d1c15-133">In alcune situazioni, questo errore si verifica solo quando l'utente è nella rete aziendale o si connette dall'esterno della rete aziendale.</span><span class="sxs-lookup"><span data-stu-id="d1c15-133">In some situations, this error behavior may occur only when the user is on the company network, or only when the user is connecting from outside the company network.</span></span> <span data-ttu-id="d1c15-134">I criteri di autenticazione globali consentono di abilitare i metodi di autenticazione separatamente per le connessioni Extranet e Intranet.</span><span class="sxs-lookup"><span data-stu-id="d1c15-134">The Global Authentication Policy allows authentication methods to be enabled separately for intranet and extranet connections.</span></span> <span data-ttu-id="d1c15-135">Se l'autenticazione basata su form non è abilitata per la rete da cui l'utente si connette, è possibile che si verifichino errori di accesso.</span><span class="sxs-lookup"><span data-stu-id="d1c15-135">Logon errors may occur if Forms Authentication is not enabled for the network from which the user is connecting.</span></span>

<span data-ttu-id="d1c15-136">Per altre informazioni, vedere [Configurare i criteri di autenticazione](https://technet.microsoft.com/library/dn486781.aspx).</span><span class="sxs-lookup"><span data-stu-id="d1c15-136">For more information, see [Configuring Authentication Policies](https://technet.microsoft.com/library/dn486781.aspx).</span></span>

<span data-ttu-id="d1c15-137">**Causa 2: la configurazione del proxy di rete** Se la rete aziendale usa un server proxy, lo strumento di registrazione potrebbe non essere in grado di connettersi ad Azure Active Directory tramite il proxy.</span><span class="sxs-lookup"><span data-stu-id="d1c15-137">**Cause 2: Network proxy configuration** If the corporate network uses a proxy server, the registration tool may not be able to connect to Azure Active Directory through the proxy.</span></span> <span data-ttu-id="d1c15-138">Gli utenti possono abilitare lo strumento di registrazione modificando il file di configurazione dello strumento e aggiungendo questa sezione al file:</span><span class="sxs-lookup"><span data-stu-id="d1c15-138">Users can ensure that the registration tool by editing the tool’s configuration file, adding this section to the file:</span></span>

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


<span data-ttu-id="d1c15-139">Per individuare il file RegistrationTool.exe.config, avviare lo strumento di registrazione e quindi aprire l'utilità Gestione attività Windows.</span><span class="sxs-lookup"><span data-stu-id="d1c15-139">To locate the RegistrationTool.exe.config file, launch the registration tool, and then open the Windows Task Manager utility.</span></span> <span data-ttu-id="d1c15-140">Nella scheda Dettagli di Gestione attività, fare clic con il pulsante destro del mouse su RegistrationTool.exe e scegliere Apri percorso file dal menu a comparsa.</span><span class="sxs-lookup"><span data-stu-id="d1c15-140">On the Details tab in Task manager, right-click on RegistrationTool.exe and choose Open file location from the pop-up menu.</span></span>
