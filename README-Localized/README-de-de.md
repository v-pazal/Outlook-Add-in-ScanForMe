# <a name="outlook-add-in:-a-mail-add-in-for-a-read-scenario-that-checks-whether-the-user-is-mentioned-on-the-to-line,-cc-line-or-body-of-an-email."></a>Outlook-Add-In: Ein E-Mail-Add-In für ein Leseszenario, in dem geprüft wird, ob der Benutzer im Feld „An“, „Cc“ oder im Nachrichtentext enthalten ist.

**Inhaltsverzeichnis**

* [Zusammenfassung](#summary)
* [Voraussetzungen](#prerequisites)
* [Hauptkomponenten des Beispiels](#components)
* [Codebeschreibung](#codedescription)
* [Erstellen und Debuggen](#build)
* [Problembehandlung](#troubleshooting)
* [Fragen und Kommentare](#questions)
* [Mitwirkung](#contribute)
* [Zusätzliche Ressourcen](#additional-resources)

<a name="summary"></a>
##<a name="summary"></a>Zusammenfassung

In diesem Beispiel erfahren Sie, wie Sie mithilfe der [JavaScript-API für Office](https://msdn.microsoft.com/library/b27e70c3-d87d-4d27-85e0-103996273298(v=office.15)) ein Outlook-Add-In erstellen, das im E-Mail-Nachrichtentext nach Links sucht. Im folgenden finden einen Überblick über das Szenario.

 ![](../https://github.com/OfficeDev/Outlook-Add-in-ScanForMe/blob/master/readme-images/screenshot1.PNG)

<a name="prerequisites"></a>
##<a name="prerequisites"></a>Voraussetzungen
Für dieses Beispiel ist Folgendes erforderlich:  

  - Visual Studio 2013 mit Update 5 oder Visual Studio 2015  
  - Ein Computer mit Exchange 2013 mit mindestens einem E-Mail-Konto oder ein Office 365-Konto. Wenn Sie kein Konto besitzen, [nehmen Sie am Office 365 Entwicklerprogramm teil, und erhalten Sie ein kostenloses 1-Jahres-Abonnement für Office 365](https://aka.ms/devprogramsignup).
  - Internet Explorer 9 oder höher muss installiert, aber nicht der Standardbrowser sein. Zur Unterstützung von Office-Add-Ins verwendet der Office-Client, der als Host agiert, Browserkomponenten, die Bestandteil von Internet Explorer 9 oder höher sind.
  - Eine der folgenden Anwendungen als Standardbrowser: Internet Explorer 9, Safari 5.0.6, Firefox 5, Chrome 13, oder eine höhere Version eines dieser Browser.
  - Vertrautheit mit der JavaScript-Programmierung und Webdiensten.

<a name="components"></a>
##<a name="key-components"></a>Hauptkomponenten

Diese Projektmappe wurde in [Visual Studio](https://msdn.microsoft.com/library/office/fp179827.aspx#Tools_CreatingWithVS) erstellt. Sie besteht aus zwei Projekten: ScanForMe und ScanForMeWeb. Im Folgenden werden die Schlüsseldateien in diesen Projekten aufgeführt. 
#### <a name="scanforme-project"></a>ScanForMe-Projekt

* 
  [
  ```ScanForMe.xml```
  ](https://github.com/OfficeDev/Outlook-Add-in-ScanForMe/blob/master/ScanForMe/ScanForMeManifest/ScanForMe.xml) Die [Manifestdatei](https://msdn.microsoft.com/library/office/jj220082.aspx#StartBuildingApps_AnatomyofApp) für das Word-Add-In.

#### <a name="scanformeweb-project"></a>ScanForMeWeb-Projekt

* [```Home.html```](https://github.com/OfficeDev/Outlook-Add-in-ScanForMe/blob/master/ScanForMeWeb/AppRead/Home/Home.html) Die HTML-Benutzeroberfläche für das Word-Add-In.
* [```Home.js```](https://github.com/OfficeDev/Outlook-Add-in-ScanForMe/blob/master/ScanForMeWeb/AppRead/Home/Home.js) Der von Home.html verwendete JavaScript-Code für die Zusammenarbeit mit Word mithilfe der JavaScript-API für Office. 


<a name="codedescription"></a>
##<a name="description-of-the-code"></a>Codebeschreibung

Die grundlegende Logik dieses Beispiels befindet sich in der Datei [```Home.js```](https://github.com/OfficeDev/Outlook-Add-in-ScanForMe/blob/master/ScanForMeWeb/AppRead/Home/Home.js) im ScanForMeWeb-Projekt. 

Nachdem das Add-In initialisiert wurde, werden die `item.to`- und `item.cc`-Eigenschaften auf die E-Mail-Adresse des Benutzers geprüft. Die E-Mail-Adresse des Benutzers wird aus der [```Office.context.mailbox.userProfile```](https://msdn.microsoft.com/library/office/fp160976.aspx)-Eigenschaft abgerufen. Wenn der Benutzer in den Feldern „An“ oder „Cc“ dieser E-Mail gefunden wurde, wird dieses Tatsache in der Benutzeroberfläche des Add-Ins registriert. 

Die [```getAsync()```](https://msdn.microsoft.com/library/office/mt269089.aspx)-Methode des Body-Objekts wird dann zum Abrufen von E-Mail-Text im Textformat verwendet. Wenn dieser asynchrone Vorgang abgeschlossen ist, wird unsere Inlinerückruffunktion aufgerufen. Diese Funktion verwendet einen regulären Ausdruck, mit dem der E-Mail-Text auf den Vornamen des Benutzers geprüft wird. Wenn dieser gefunden wird, wird in der Benutzeroberfläche des Add-Ins gemeldet, dass der Benutzer im E-Mail-Text erwähnt wird. 

>Hinweis: Ein Beispiel zur Verwendung von getAsync zum Abrufen von E-Mail-Text im HTML-Format finden Sie im [Outlook-Add-in-LinkRevealer](https://github.com/OfficeDev/Outlook-Add-in-LinkRevealer)-Beispiel. 


<a name="build"></a>
##<a name="build-and-debug"></a>Erstellen und Debuggen
1. Öffnen Sie die Datei [```ScanForMe.sln```](ScanForMe.sln) in Visual Studio.
2. Drücken Sie F5, um das Beispiel-Add-In zu erstellen und zu debuggen. 
3. Wenn Outlook gestartet wird, wählen Sie eine E-Mail-Nachricht aus dem Posteingang.
4. Starten Sie das Add-In, indem Sie es in der Add-In-App-Leiste auswählen.

 - Screenshot erforderlich


5. [Beschreiben Sie das weitere Vorgehen]


<a name="troubleshooting"></a>
## <a name="troubleshooting"></a>Problembehandlung

- Wenn das Add-In nicht im Aufgabenbereich angezeigt wird, wählen Sie **Einfügen > Meine Add-Ins > Nach meinem Namen suchen**.

<a name="questions"></a>
## <a name="questions-and-comments"></a>Fragen und Kommentare

- Wenn Sie beim Ausführen dieses Beispiels Probleme haben, [melden Sie sie bitte](https://github.com/OfficeDev/Outlook-Add-in-ScanForMe/issues).
- Allgemeine Fragen zur Office-Add-In-Entwicklung sollten in [Stack Overflow](http://stackoverflow.com/questions/tagged/office-addins) gestellt werden. Stellen Sie sicher, dass Ihre Fragen oder Kommentare mit [office-addins] markiert sind.


<a name="contribute"></a>
## <a name="contributing"></a>Mitwirkung ##
Wir bitten Sie um Mitwirkung an unseren Beispielen. Richtlinien zur Vorgehensweise finden Sie in unseren [Mitwirkungsrichtlinien](./Contributing.md)

In diesem Projekt wurden die [Microsoft Open Source-Verhaltensregeln](https://opensource.microsoft.com/codeofconduct/) übernommen. Weitere Informationen finden Sie unter [Häufig gestellte Fragen zu Verhaltensregeln](https://opensource.microsoft.com/codeofconduct/faq/), oder richten Sie Ihre Fragen oder Kommentare an [opencode@microsoft.com](mailto:opencode@microsoft.com).


<a name="additional-resources"></a>
## <a name="additional-resources"></a>Zusätzliche Ressourcen ##

- [Weitere Add-In-Beispiele](https://github.com/OfficeDev?utf8=%E2%9C%93&query=-Add-in)
- 
  [Office-Add-Ins](http://msdn.microsoft.com/library/office/jj220060.aspx)
- 
  [Aufbau eines Add-Ins](https://msdn.microsoft.com/library/office/jj220082.aspx#StartBuildingApps_AnatomyofApp)
- 
  [Erstellen eines Office-Add-Ins mithilfe von Visual Studio](https://msdn.microsoft.com/library/office/fp179827.aspx#Tools_CreatingWithVS)


## <a name="copyright"></a>Copyright
Copyright (c) 2015 Microsoft. Alle Rechte vorbehalten.