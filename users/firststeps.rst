##############
Erste Schritte
##############

Für den Betrieb von SmartWFM wird das Frontend und ein Backend benötigt.

Backend
=======

Es ist möglich verschiedene Backends mit dem SWFM-Frontend zu benutzen. Zur Zeit gibt es leider nur ein Backend in PHP:

Vorraussetzungen
----------------

* Webserver mit PHP (apache, lighttpd, etc.)
* PHP 5.x (eventuell funktionieren spätere Versionen von PHP 4.x, welche aber ungetested sind)

Installation
------------

* Backend herunterladen 
* Inhalt dieses Archives in einen Ordner entpacken
* Inhalt der Ordners src in einen seperaten Ordner auf dem Webserver laden (z.B. **/var/www/backend-php**), welcher per Browser erreichbar ist
* http://your-web-server.example.com/backend-php/ öffnen und den Anweisungen folgen ODER die Datei config/local.php selbst erstellen (siehe Einstellungen)
* [optional] Beispielkonfiguration unter config/local.php.dist anschauen

Einstellungen
-------------

.. list-table::
	:widths: 15 10 30
	:header-rows: 1

	* - Name
	  - Typ
	  - Beschreibung
	* - **basepath**
	  - String
	  - Wurzelverzeichnis, aus dem man innerhalb des SmartWFM nicht herausnavigieren kann
	* - **mimetype_detection_mode**
	  - String
	  - Art der MIME-type-Erkennung, mögliche Werte sind:
		:internal:	Verwendung der PHP-Funktion mime_content_type
		:cmd_file:	file-Kommando wird auf die Datei angewendet
		:file:		Endung der Datei gilt als Kriterium für den MIME-type
	* - **commands_path**
	  - String
	  - Pfad zum commands-Verzeichnis des Backends
	* - **commands**
	  - Array
	  - Liste mit den Dateinamen (ohne die Endung .php) der Backendplugins, die geladen werden sollen
	* - **filesystem_mode**
	  - String
	  - Art des Dateisystems, mögliche Werte sind:
		:local:		Benutzung der Standard-Dateisystemoperationen von PHP
		:afs:		wie local, nur mit zusätzlicher Unterstützung für die Rechteverwaltung unter AFS

Diese Einstellungen werden in der Datei **config/local.php** auf folgende Weise gesetzt::

	SmartWFM_Registry::set('NAME_DER_OPTION', 'WERT');

Weitere Einstellungen sind im folgenden Abschnitt zu finden, da diese dann nur einem speziellem Command zugeordnet sind und somit nicht benötigt werden, wenn dieses nicht eingebunden ist.

Backend-Plugins (Commands)
--------------------------

.. list-table::
	:widths: 20 20 20 40
	:header-rows: 1
	
	* - Name
	  - Funktionen
	  - Frontend-Module, die diese Funktionen benötigen
	  - Einstellungen (in config/local.php)
	* - **afs_special_actions**
	  - 
	  	* Quota auslesen
	  	* AFS-Rechte lesen und setzen
	  	* AFS-Gruppen lesen, erstellen und entfernen
		* AFS-Gruppen-Mitgliedschaften lesen, hinzufügen und entfernen
	  - 
	  	* **afs_actions** (Plugin)
	  - 
	* - **afs_actions**
	  - 
	  	* Archive erstellen, lesen und entpacken
	  - 
	  	* **archives** (Plugin)
	  - 
	* - **base_actions**
	  - 
	  	* Verzeichnisse erstellen und löschen
	  	* Verzeichnisinhalt auflisten
	  	* Dateien verschieben, kopieren, löschen, umbenennen
	  - 
	  	* **base_actions** (Plugin)
	  	* **browser** (Widget)
	  	* **treemenu** (Widget)
	  - 
	* - **base_direct_commands**
	  -
	  	* Hoch- und Herunterladen von Dateien
	  	* Quellcode-Highlighting
	  - 
	  	* **base_actions** (Plugin)
	  	* **esource_viewer** (Plugin)
	  	* **image_viewer** (Plugin)
	  - 
	  	:use_x_sendfile (Boolean): 
	  		legt fest, ob x-sendfile für den Download von Dateien verwendet wird
	  		
	  		Hinweise (unter Apache 2.x):
	  		
		  	*mod_xsendfile* installieren und folgende Einstellungen vornehmen::
		  	
			  	XSendFile On
				XSendFileAllowAbove On
	
	* - **new_file**
	  -
	  - 
	  	* **new_file** (Plugin)
	  -
	* - **search_actions**
	  -
	  	* Suche nach Dateien
	  - 
	  	* **search** (Widget)
	  -
	* - **setting_actions**
	  -
	  	* speichern und laden der Frontend-Einstellungen
	  -
	  	* **setting** (Plugin)
	  -
	  	:setting_filename (String): 
	  		Dateiname für Datei, die die SWFM-Frontend-Einstellungen des Benutzers speichert

			Pfad für mehrere Benutzer dynamisch anpassen - Bsp.: "/home/".$_SERVER['PHP_AUTH_USER']."/.smartwfm.ini"
		  	
Frontend
========

* Frontend herunterladen
* Inhalt dieses Archives in einen Ordner auf dem Webserver entpacken (z.B. **/var/www/swfm**), welcher per Browser erreichbar ist


Beispielkonfiguration
---------------------

.. code-block:: guess

	<script type="text/javascript">
		SmartWFM.init({
			'command_url': '../php/index.php',
			'lang': lang,
			'plugins' : [
				'base_actions'
			],
			'widgets' : [
				'treemenu',
				'browser',
			],
			'menu.main.file': ['newtab'],
			'menu.main.edit': ['copy', 'move', 'paste', 'rename', 'delete'],
			'menu.main.view': ['iconview', 'listview'],
			'menu.main.tools': [],
			'menu.main.extras': [],
			'widget.treemenu.menu.context': ['treemenu-newtab'],
			'widget.browser.menu.context': ['copy', 'move', 'paste', 'rename', '|', 'delete'],
		});
	</script>