---
title: applicazione di esempio aaaAzure per l'utilizzo con le reti perimetrali | Documenti Microsoft
description: Distribuire l'applicazione web semplice dopo la creazione di scenari di flusso di traffico tootest una rete Perimetrale
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 60340ab7-b82b-40e0-bd87-83e41fe4519c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: e0d9cf14590f75b50c64b677efce2c5425b83ec6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sample-application-for-use-with-dmzs"></a><span data-ttu-id="4d4e2-103">Applicazione di esempio per l'uso con reti perimetrali</span><span class="sxs-lookup"><span data-stu-id="4d4e2-103">Sample application for use with DMZs</span></span>
<span data-ttu-id="4d4e2-104">[Restituire la pagina sicurezza limite Best Practices toohello][HOME]</span><span class="sxs-lookup"><span data-stu-id="4d4e2-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="4d4e2-105">Questi script di PowerShell possono essere eseguiti localmente in hello IIS01 e AppVM01 tooinstall di server e configurare un'applicazione web semplice che visualizza una pagina html da server IIS01 front-end hello con contenuto dal server di AppVM01 hello back-end.</span><span class="sxs-lookup"><span data-stu-id="4d4e2-105">These PowerShell scripts can be run locally on hello IIS01 and AppVM01 servers tooinstall and set up a simple web application that displays an html page from hello front-end IIS01 server with content from hello back-end AppVM01 server.</span></span>

<span data-ttu-id="4d4e2-106">Questa applicazione fornisce un ambiente di test semplice per molti degli esempi di rete Perimetrale hello e come le modifiche apportate hello endpoint, NSGs, UDR e regole del Firewall possono influenzare i flussi di traffico.</span><span class="sxs-lookup"><span data-stu-id="4d4e2-106">This application provides a simple testing environment for many of hello DMZ Examples and how changes on hello Endpoints, NSGs, UDR, and Firewall rules can affect traffic flows.</span></span>

## <a name="firewall-rule-tooallow-icmp"></a><span data-ttu-id="4d4e2-107">Tooallow regola firewall ICMP</span><span class="sxs-lookup"><span data-stu-id="4d4e2-107">Firewall rule tooallow ICMP</span></span>
<span data-ttu-id="4d4e2-108">Questa istruzione PowerShell semplice può essere eseguita in tutto il traffico ICMP (Ping) tooallow macchina virtuale di Windows.</span><span class="sxs-lookup"><span data-stu-id="4d4e2-108">This simple PowerShell statement can be run on any Windows VM tooallow ICMP (Ping) traffic.</span></span> <span data-ttu-id="4d4e2-109">Questo aggiornamento firewall consente più semplice di test e risoluzione dei problemi, consentendo di hello ping protocollo toopass attraverso il firewall windows hello (per la maggior parte delle distribuzioni di Linux che ICMP è attivata per impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="4d4e2-109">This firewall update allows for easier testing and troubleshooting by allowing hello ping protocol toopass through hello windows firewall (for most Linux distros ICMP is on by default).</span></span>

```PowerShell
# Turn On ICMPv4
New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" `
    -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow
```

<span data-ttu-id="4d4e2-110">Se si utilizza hello script seguente, l'aggiunta della regola firewall è hello prima istruzione.</span><span class="sxs-lookup"><span data-stu-id="4d4e2-110">If you use hello following scripts, this firewall rule addition is hello first statement.</span></span>

## <a name="iis01---web-application-installation-script"></a><span data-ttu-id="4d4e2-111">IIS01 - Script di installazione dell'applicazione Web</span><span class="sxs-lookup"><span data-stu-id="4d4e2-111">IIS01 - Web application installation script</span></span>
<span data-ttu-id="4d4e2-112">Questo script consentirà di:</span><span class="sxs-lookup"><span data-stu-id="4d4e2-112">This script will:</span></span>

1. <span data-ttu-id="4d4e2-113">Aprire IMCPv4 (Ping) sul firewall di windows hello server locale per il test più semplice</span><span class="sxs-lookup"><span data-stu-id="4d4e2-113">Open IMCPv4 (Ping) on hello local server windows firewall for easier testing</span></span>
2. <span data-ttu-id="4d4e2-114">Installare IIS e hello .net v 4.5 Framework</span><span class="sxs-lookup"><span data-stu-id="4d4e2-114">Install IIS and hello .Net Framework v4.5</span></span>
3. <span data-ttu-id="4d4e2-115">Creare una pagina Web ASP.NET e un file Web.config.</span><span class="sxs-lookup"><span data-stu-id="4d4e2-115">Create an ASP.NET web page and a Web.config file</span></span>
4. <span data-ttu-id="4d4e2-116">Modificare hello predefinito applicazione pool toomake accesso ai file semplice</span><span class="sxs-lookup"><span data-stu-id="4d4e2-116">Change hello Default application pool toomake file access easier</span></span>
5. <span data-ttu-id="4d4e2-117">Impostare account di amministratore tooyour utente anonimo hello e una password</span><span class="sxs-lookup"><span data-stu-id="4d4e2-117">Set hello Anonymous user tooyour admin account and password</span></span>

<span data-ttu-id="4d4e2-118">Lo script di PowerShell deve essere eseguito localmente mentre viene usata una sessione RDP per accedere a IIS01.</span><span class="sxs-lookup"><span data-stu-id="4d4e2-118">This PowerShell script should be run locally while RDP’d into IIS01.</span></span>

```PowerShell
# IIS Server Post Build Config Script
# Get Admin Account and Password
    Write-Host "Please enter hello admin account information used toocreate this VM:" -ForegroundColor Cyan
    $theAdmin = Read-Host -Prompt "hello Admin Account Name (no domain or machine name)"
    $thePassword = Read-Host -Prompt "hello Admin Password"

# Turn On ICMPv4
    Write-Host "Creating ICMP Rule in Windows Firewall" -ForegroundColor Cyan
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Install IIS
    Write-Host "Installing IIS and .Net 4.5, this can take some time, like 15+ minutes..." -ForegroundColor Cyan
    add-windowsfeature Web-Server, Web-WebServer, Web-Common-Http, Web-Default-Doc, Web-Dir-Browsing, Web-Http-Errors, Web-Static-Content, Web-Health, Web-Http-Logging, Web-Performance, Web-Stat-Compression, Web-Security, Web-Filtering, Web-App-Dev, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Net-Ext, Web-Net-Ext45, Web-Asp-Net45, Web-Mgmt-Tools, Web-Mgmt-Console

# Create Web App Pages
    Write-Host "Creating Web page and Web.Config file" -ForegroundColor Cyan
    $MainPage = '<%@ Page Language="vb" AutoEventWireup="false" %>
    <%@ Import Namespace="System.IO" %>
    <script language="vb" runat="server">
        Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Load
            Dim FILENAME As String = "\\10.0.2.5\WebShare\Rand.txt"
            Dim objStreamReader As StreamReader
            objStreamReader = File.OpenText(FILENAME)
            Dim contents As String = objStreamReader.ReadToEnd()
            lblOutput.Text = contents
            objStreamReader.Close()
            lblTime.Text = Now()
        End Sub
    </script>

    <!DOCTYPE html>
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
        <title>DMZ Example App</title>
    </head>
    <body style="font-family: Optima,Segoe,Segoe UI,Candara,Calibri,Arial,sans-serif;">
      <form id="frmMain" runat="server">
        <div>
          <h1>Looks like you made it!</h1>
          This is a page from hello inside (a web server on a private network),<br />
          and it is making its way toohello outside! (If you are viewing this from hello internet)<br />
          <br />
          hello following sections show:
          <ul style="margin-top: 0px;">
            <li> Local Server Time - Shows if this page is or isnt cached anywhere</li>
            <li> File Output - Shows that hello web server is reaching AppVM01 on hello backend subnet and successfully returning content</li>
            <li> Image from hello Internet - Doesnt really show anything, but it made me happy toosee this when hello app worked</li>
          </ul>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Local Web Server Time</b>: <asp:Label runat="server" ID="lblTime" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>File Output from AppVM01</b>: <asp:Label runat="server" ID="lblOutput" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Image File Linked from hello Internet</b>:<br />
            <br />
            <img src="http://sd.keepcalm-o-matic.co.uk/i/keep-calm-you-made-it-7.png" alt="You made it!" width="150" length="175"/></div>
        </div>
      </form>
    </body>
    </html>'

    $WebConfig ='<?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.web>
        <compilation debug="true" strict="false" explicit="true" targetFramework="4.5" />
        <httpRuntime targetFramework="4.5" />
        <identity impersonate="true" />
        <customErrors mode="Off"/>
      </system.web>
      <system.webServer>
        <defaultDocument>
          <files>
            <add value="Home.aspx" />
          </files>
        </defaultDocument>
      </system.webServer>
    </configuration>'

    $MainPage | Out-File -FilePath "C:\inetpub\wwwroot\Home.aspx" -Encoding ascii
    $WebConfig | Out-File -FilePath "C:\inetpub\wwwroot\Web.config" -Encoding ascii

# Set App Pool tooClasic Pipeline tooremote file access will work easier
    Write-Host "Updaing IIS Settings" -ForegroundColor Cyan
    c:\windows\system32\inetsrv\appcmd.exe set app "Default Web Site/" /applicationPool:".NET v4.5 Classic"
    c:\windows\system32\inetsrv\appcmd.exe set config "Default Web Site/" /section:system.webServer/security/authentication/anonymousAuthentication /userName:$theAdmin /password:$thePassword /commit:apphost

# Make sure hello IIS settings take
    Write-Host "Restarting hello W3SVC" -ForegroundColor Cyan
    Restart-Service -Name W3SVC

    Write-Host
    Write-Host "Web App Creation Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="appvm01---file-server-installation-script"></a><span data-ttu-id="4d4e2-119">AppVM01 - Script di installazione del file server</span><span class="sxs-lookup"><span data-stu-id="4d4e2-119">AppVM01 - File server installation script</span></span>
<span data-ttu-id="4d4e2-120">Questo script consente di impostare hello back-end per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="4d4e2-120">This script sets up hello back-end for this simple application.</span></span> <span data-ttu-id="4d4e2-121">Questo script consentirà di:</span><span class="sxs-lookup"><span data-stu-id="4d4e2-121">This script will:</span></span>

1. <span data-ttu-id="4d4e2-122">Aprire IMCPv4 (Ping) nel firewall hello per semplificare il test</span><span class="sxs-lookup"><span data-stu-id="4d4e2-122">Open IMCPv4 (Ping) on hello firewall for easier testing</span></span>
2. <span data-ttu-id="4d4e2-123">Creare una directory per il sito web hello</span><span class="sxs-lookup"><span data-stu-id="4d4e2-123">Create a directory for hello web site</span></span>
3. <span data-ttu-id="4d4e2-124">Creare un toobe di file di testo in modalità remota accedere dalla pagina web hello</span><span class="sxs-lookup"><span data-stu-id="4d4e2-124">Create a text file toobe remotely access by hello web page</span></span>
4. <span data-ttu-id="4d4e2-125">Impostare le autorizzazioni per hello file e directory tooAnonymous tooallow accesso</span><span class="sxs-lookup"><span data-stu-id="4d4e2-125">Set permissions on hello directory and file tooAnonymous tooallow access</span></span>
5. <span data-ttu-id="4d4e2-126">Disattivare sicurezza avanzata di Internet Explorer tooallow più semplice da questo server</span><span class="sxs-lookup"><span data-stu-id="4d4e2-126">Turn off IE Enhanced Security tooallow easier browsing from this server</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="4d4e2-127">**Procedura consigliata**: mai disattivare sicurezza avanzata di Internet Explorer in un server di produzione e è in genere web hello toosurf consigliati da un server di produzione.</span><span class="sxs-lookup"><span data-stu-id="4d4e2-127">**Best Practice**: Never turn off IE Enhanced Security on a production server, plus it's generally a bad idea toosurf hello web from a production server.</span></span> <span data-ttu-id="4d4e2-128">Anche l'apertura di condivisioni file per l'accesso anonimo è un'attività da evitare, ma in questo caso viene eseguita per semplificare le operazioni.</span><span class="sxs-lookup"><span data-stu-id="4d4e2-128">Also, opening up file shares for anonymous access is a bad idea, but done here for simplicity.</span></span>
> 
> 

<span data-ttu-id="4d4e2-129">Lo script di PowerShell deve essere eseguito localmente mentre viene usata una sessione RDP per accedere ad AppVM01.</span><span class="sxs-lookup"><span data-stu-id="4d4e2-129">This PowerShell script should be run locally while RDP’d into AppVM01.</span></span> <span data-ttu-id="4d4e2-130">PowerShell è obbligatorio toobe Esegui come amministratore tooensure completamento dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="4d4e2-130">PowerShell is required toobe run as Administrator tooensure successful execution.</span></span>

```PowerShell
# AppVM01 Server Post Build Config Script
# PowerShell must be run as Administrator for Net Share commands toowork

# Turn On ICMPv4
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Create Directory
    New-Item "C:\WebShare" -ItemType Directory

# Write out Rand.txt
    $FileContent = "Hello, I'm hello contents of a remote file on AppVM01."
    $FileContent | Out-File -FilePath "C:\WebShare\Rand.txt" -Encoding ascii

# Set Permissions on share
    $Acl = Get-Acl "C:\WebShare"
    $AccessRule = New-Object system.security.accesscontrol.filesystemaccessrule("Everyone","ReadAndExecute, Synchronize","ContainerInherit, ObjectInherit","InheritOnly","Allow")
    $Acl.SetAccessRule($AccessRule)
    Set-Acl "C:\WebShare" $Acl

# Create network share
    Net Share WebShare=C:\WebShare "/grant:Everyone,READ"

# Turn Off IE Enhanced Security Configuration for Admins
    Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A7-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0

    Write-Host
    Write-Host "File Server Set up Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="dns01---dns-server-installation-script"></a><span data-ttu-id="4d4e2-131">DNS01 - Script di installazione del server DNS</span><span class="sxs-lookup"><span data-stu-id="4d4e2-131">DNS01 - DNS server installation script</span></span>
<span data-ttu-id="4d4e2-132">Non sussiste alcun script incluso in questo tooset di applicazione di esempio del server DNS hello.</span><span class="sxs-lookup"><span data-stu-id="4d4e2-132">There is no script included in this sample application tooset up hello DNS server.</span></span> <span data-ttu-id="4d4e2-133">Se il test di regole del firewall hello, gruppo o UDR deve tooinclude il traffico DNS, server hello DNS01 deve toobe impostato manualmente.</span><span class="sxs-lookup"><span data-stu-id="4d4e2-133">If testing of hello firewall rules, NSG, or UDR needs tooinclude DNS traffic, hello DNS01 server needs toobe set up manually.</span></span> <span data-ttu-id="4d4e2-134">file xml di configurazione di rete Hello e modello di gestione risorse per entrambi gli esempi includono DNS01 come server DNS primario hello e server DNS pubblico hello ospitato da livello 3 come server DNS backup hello.</span><span class="sxs-lookup"><span data-stu-id="4d4e2-134">hello Network Configuration xml file and Resource Manager Template for both examples includes DNS01 as hello primary DNS server and hello public DNS server hosted by Level 3 as hello backup DNS server.</span></span> <span data-ttu-id="4d4e2-135">server DNS di livello 3 Hello sarebbe hello effettivo server DNS usato per il traffico non locale e con DNS01 non del programma di installazione, nessuna rete locale si verificherebbe DNS.</span><span class="sxs-lookup"><span data-stu-id="4d4e2-135">hello Level 3 DNS server would be hello actual DNS server used for non-local traffic, and with DNS01 not setup, no local network DNS would occur.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d4e2-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4d4e2-136">Next steps</span></span>
* <span data-ttu-id="4d4e2-137">Eseguire script IIS01 hello in un server IIS</span><span class="sxs-lookup"><span data-stu-id="4d4e2-137">Run hello IIS01 script on an IIS server</span></span>
* <span data-ttu-id="4d4e2-138">Eseguire script del file server in AppVM01</span><span class="sxs-lookup"><span data-stu-id="4d4e2-138">Run File Server script on AppVM01</span></span>
* <span data-ttu-id="4d4e2-139">Sfoglia toohello IP pubblico in IIS01 toovalidate la compilazione</span><span class="sxs-lookup"><span data-stu-id="4d4e2-139">Browse toohello Public IP on IIS01 toovalidate your build</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
