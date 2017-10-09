
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. Accedi toohello [portale di Azure](https://portal.azure.com/) in http://portal.azure.com/.
2. Nel banner sinistro hello, fare clic su **Esplora tutto**. Hello **Sfoglia** pannello viene visualizzato.
3. Scorrere e fare clic su **Server SQL**. Hello **istanze di SQL Server** pannello viene visualizzato.
   
    ![Trovare il server di Database SQL di Azure nel portale di hello][b21-FindServerInPortal]
4. Per praticità, fare clic su hello ridurre al minimo il controllo in precedenza hello **Sfoglia** blade.
5. Nella casella di testo filtro hello, iniziare a digitare il nome di hello del server. Viene visualizzata la riga.
6. Fare clic sulla riga hello del server. Viene visualizzato un pannello per il server.
7. Nel pannello del server, fare clic su **impostazioni**. Hello **impostazioni** pannello viene visualizzato.
8. Fare clic su **Firewall**. Hello **le impostazioni del Firewall** pannello viene visualizzato.
   
    ![Fare clic su Impostazioni > Firewall][b31-SettingsFirewallNavig]
9. Fare clic su **aggiungere Client IP**. Digitare un nome per la nuova regola nella prima casella di testo hello.
10. Tipo di hello basso e alto valori di intervallo hello desiderato di indirizzi IP tooenable.
    
    * Può essere utile toohave hello basso valore fine con **,0** e alta con hello **.255**.
    
    ![Aggiungere un tooallow intervallo di indirizzi IP][b41-AddRange]
11. Fare clic su **Salva**.

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
