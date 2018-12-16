ImgSize, WDX Content Plugin for Total Commander, 2005-2013 by J. Bleichroth

(Deutsche �bersetzung: siehe weiter unten in dieser Datei.)

Plugin columns:    Width(x), Height(y), Pixel(x * y), Diagonal(diagonal length), 
                   Orientation (Square, Portrait, Landscape), Size (small, medium, large), 
                   Aspect ratio, Bpp, Dpi

Supported formats: JPG GIF BMP PNG TIFF PSD PCX EPS/PS

Plugin purpose:    Sorting images by size

---------------------------------------------------

Changelog:
2013-05-14  v2.03  Recompiled with newest Compiler version
2012-03-24  v2.02  Unicode/longfilename support, 64bit (wdx64), Versions infos added, Dpi column added, 
                   Sorting properties (columns: Orientation, Size) improved, Plugin delay mode changed (configurable)
2005-07-03  v1.12  Bpp column added
2005-07-02  v1.11  Aspect ratio column internal format changed for TC 6.52 and higher
2005-04-17  v1.10  Aspect ratio column added
2005-02-19  v1.09  ImgSize.lng changed
2005-02-18  v1.08  auto language select, ini file changed to imgsize.ini (in plugin dir), english column names changed
2005-02-08  v1.07  PSD PCX EPS/PS support added, improved readme.txt
2005-02-03  v1.06  TIFF images support added
2005-01-31  v1.05  Some translations changed on user request
2005-01-30  v1.04  IniFile (usually (TC depending): contplug.ini) configurable texts and size definitions
2005-01-28  v1.03  Orientation (Square, Portrait, Landscape) column added, Size (small, medium, large) column added
2005-01-28  v1.02  additional file checks added, French language added
2005-01-27 Initial release

---------------------------------------------------

Addiional informations about the ini file (imgsize.ini):

The IniFile (imgsize.ini) is (optional) changable for the following details:

- For language support of 'Square', 'Portrait', 'Landscape', 'small', 'medium', 'large'
  please change the LanguageNo=N (N = 1..3), if the automatic language support does no 
  work as requested and set "TextLanguageAutoSelect=No".

- Enable/Disable EPS/PS File support: EpsFiles=N PsFiles=N (N = 0/1 or Yes/No)

- Size column definitions:
  small:  image smaller than: (x and y) or (x and y) or (x and y) ... ((0,0)= element not used)
  large:  image larger than:  (x and y) or (x and y) or (x and y) ... ((0,0)= element not used)
  medium: all other images
  
---------------------------------------------------

Installation: 
- Standard: Open the plugin zip file (with a pluginst.inf file for automatic inst.) within TC
- Manual:   Use TC Menu -> Configuration -> Options -> Plugins -> 
            Content Plugins configure -> Add ...

---------------------------------------------------

Usage: 
- Use TC Menu -> Configuration -> Options -> Custom columns -> New/Edit ...
or
- Right-click on the (left or right) TC window columns - > Configure custom columns -> New/Edit ..

---------------------------------------------------

Support questions, bug reports, suggestions please here:
Total Commander Forum -> Plugins and addons: devel.+support (English)
Link: http://www.ghisler.ch/board/viewforum.php?f=6

---------------------------------------------------

License and liability:
ImgSize, WDX Content Plugin for Total Commander, Copyright 2005-2013 J. Bleichroth
Any liability for damage of any sort is hereby denied.
All rights reserved. 
This Total Commander Plugin is free usable, copyrighted software by J. Bleichroth
Distribution reserved. No distribution without permission by J. Bleichroth.

===============================================================================

Deutsche �bersetzung:

ImgSize, WDX Content Plugin f�r Total Commander, 2005-2013 von J. Bleichroth

Plugin Kolumnen:      Breite (x), H�he (y), Pixel (x * y), Diagonal (diagonale L�nge),
                      Orientierung (Square, Portrait, Landschaft), Gr��e (klein, mittel, gro�),
                      Seitenverh�ltnis, BPP, Dpi

Unterst�tzte Formate: JPG GIF PNG BMP TIFF PSD PCX EPS / PS

Plugin Zweck:         Images sortieren nach Gr��e

---------------------------------------------------

Changelog:
2013-05-14  v2.03 Neu kompiliert mit neuesten Compiler-Version
2012-03-24  v2.02 Unicode/Lange Dateinamen-Unterst�tzung, 64bit (wdx64), Versions Infos hinzugef�gt, Dpi Kolumne hinzugef�gt, 
                  Verbesserte Sortiereigenschaften (Kolumnen: Orientirung, Gr�sse), Plugin delay mode ge�ndert (konfigurierbar)
2005.07.03  v1,12 Kolumne Bpp hinzugef�gt
2005.07.02  v1,11 Internes Format der Kolumne Seitenverh�ltnis f�r TC 6,52 ge�ndert und h�her
2005.04.17  v1,10 Kolumne Seitenverh�ltnis hinzugef�gt
2005.02.19  v1,09 ImgSize.lng ge�ndert
2005.02.18  v1,08 Autom. Sprachwahl, INI-Datei zu imgsize.ini (im Plugin-dir) ver�ndert, englische Kolumnennamen ver�ndert 
2005.02.08  v1,07 PSD PCX EPS/PS-Unterst�tzung hinzugef�gt, readme.txt verbessert
2005.02.03  v1,06 TIFF-Bilder Unterst�tzung hinzugef�gt
2005.01.31  v1,05 Einige �bersetzungen auf Userwunsch ge�ndert
2005.01.30  v1,04 IniFile (in der Regel (TC abh�ngig): contplug.ini) konfigurierbare Texte und Gr��e Definitionen
2005.01.28  v1,03 Kolumne Orientierung (Quadratisch, Portrait, Landschaft) hinzugef�gt, Kolumne Gr��e (klein, mittel, gro�) hinzugef�gt
2005.01.28  v1,02 zus�tzliche Dateichecks hinzugef�gt, franz�sische Sprache hinzugef�gt
2005.01.27  Erste Ver�ffentlichung

---------------------------------------------------

Zus�tzliche Informationen zur INI-Datei (imgsize.ini):

Die INI-Datei (imgsize.ini) ist f�r die folgenden Details (optional) �nderbar:

- Zum �ndern der Sprache von 'Square', 'Portrait', 'Landschaft', 'klein', 'mittel', 'gro�'
  �ndern Sie bitte LanguageNo=N (N = 1..5), wenn die automatische Spracherkennung nicht wie
  gew�nscht arbeitet und stellen Sie TextLanguageAutoSelect=No ein.

- Aktivieren/Deaktivieren der EPS/PS-Datei-Unterst�tzung: EpsFiles=N PsFiles=N (N = 0/1 oder Yes/No)

- Definitionen Kolumne Gr��e:
  klein:  Bild kleiner als: (x und y) oder (x und y) oder (x und y) ... ((0,0) = Element nicht verwendet)
  gro�:   Bild gr��er  als: (x und y) oder (x und y) oder (x und y) ... ((0,0) = Element nicht verwendet)
  mittel: alle anderen Bilder

---------------------------------------------------

Installation:
- Standard: �ffnen Sie das Plugin-Zip-Archiv (Mit einer pluginst.inf-Datei f�r die automatische Installation) 
            innerhalb vom TC mit Enter und folgen sie dann den Anweisungen des Tc
- Manuell:  TC Men� -> Konfiguration -> Optionen -> Plugins -> Inhalts-Plugins konfigurieren -> Hinzuf�gen ...

---------------------------------------------------

Benutzung:
- TC Men� -> Konfiguration -> Optionen -> Benutzerdefinierte Spalten -> Neu/Bearbeiten ...
oder
- Oberhalb vom (linken oder rechten) TC Fenster Kolumnen mit der rechten Maustaste klicken -> 
  Konfigurieren benutzerdefinierter Spalten -> Neu/Bearbeiten ..

---------------------------------------------------

Support-Anfragen, Fehlermeldungen, Anregungen bitte hier einstellen:
Total Commander Forum -> Plugins und Addons:. Devel + Support (englisch)
Link: http://www.ghisler.ch/board/viewforum.php?f=6

---------------------------------------------------

Lizenz und Haftung:
ImgSize, WDX Content Plugin f�r Total Commander, Copyright 2005-2013 J. Bleichroth
Jegliche Haftung f�r Sch�den jeglicher Art wird hiermit ausgeschlossen.
Alle Rechte vorbehalten.
Dieses Total Commander-Plugin ist kostenlos nutzbare, urheberrechtlich gesch�tzte Software von J. Bleichroth.
Verteilung vorbehalten. Keine Verteilung ohne Genehmigung von J. Bleichroth.

---------------------------------------------------
