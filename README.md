# ITgePA_RPA_Rothbaum

## 1. Extraction from Input Form: FULLY FUNCTIONAL
### Input: 
	Google Excel Sheet <FAU ITgeP Input>: [(Checked), Time, E-Mail, Manufacturer (Example: Kinavo Servo Motor (changzhou) Ltd), 
	Description (Example: Kinavo Motor SMH40-103028ENL), Part Number (Example: SMH40-103028ENL)]
### Output: 
	Input Tabelle.xlsx [(Checked), Time, E-Mail, Manufacturer (Example: Kinavo Servo Motor (changzhou) Ltd), 
	Description (Example: Kinavo Motor SMH40-103028ENL), Part Number (Example: SMH40-103028ENL)] -> ".\"
	Google Excel Sheet <FAU ITgeP Input>: [(Checked), Time, E-Mail, Manufacturer (Example: Kinavo Servo Motor (changzhou) Ltd), 
	Description (Example: Kinavo Motor SMH40-103028ENL), Part Number (Example: SMH40-103028ENL)]
### Beschreibung:
	Erzeugen einer Spalte <Checked> falls nicht im Google Sheet vorhanden. Daraufhin werden alle Anfragen herunter 
	geladen und alle neuen Beiträge mit <Completed> markiert. Nicht Threadsafe! Funktioniert nur, wenn die Datei
	zuvor von UI-Path erstellt wurde. Daher gewünschte Datei anlegen und mit Google-Forms auf diese erstellte Datei
	verweisen. Methode auskommentiert um notwendige Datei zu erstellen, bei erster Ausführung.

------------------------

## 2. Create_Output_Google_Doc: FULLY FUNCTIONAL
### Input:
	
### Output: 
	Drive Folder <ITgePA Rothbaum Ordner>
	Google Excel Sheet <Spread_Rothbaum_output>: [Checked, Part Number, Description, Manufacturer, Hight, Width, Length, Volume, Weight]
	Output Tabelle.xlsx [Completed, Part Number, Description, Manufacturer, Hight, Width, Length, Volume, Weight] -> ".\"
### Beschreibung:
	Erzeugt die Vorlagen falls nicht vorhanden. Daraufhin wird der aktuelle Stand lokal nach <.\Output Tabelle.xlsx> heruntergeladen.

------------------------

## 3. Übertragen von Input zu Output Temp: FULLY FUNCTIONAL
### Input: 
	Input Tabelle.xlsx [Checked, Time, E-Mail, Manufacturer (Example: Kinavo Servo Motor (changzhou) Ltd), 
	Description (Example: Kinavo Motor SMH40-103028ENL), Part Number (Example: SMH40-103028ENL)] -> ".\"
	Output Tabelle.xlsx [Completed, Part Number, Description, Manufacturer, Hight, Width, Length, Volume, Weight] -> ".\"
### Output:
	Input Tabelle.xlsx [Completed, Manufacturer, Description, Part Number] -> ".\"
	Output Tabelle Temp.xlsx [Completed, Part Number, Description, Manufacturer, Hight, Width, Length, Volume, Weight] -> ".\"
### Beschreibung:
	<Output Tabelle> wird kopiert nach <./Output Tabelle Temp.xlsx>. Alles Daten in <./Output Tabelle Temp.xlsx>
	werden gelöscht. Dieses wird zur weitere verarbeitung der Daten genutzt. Auslegung hierbei für <500 Einträge.
	Dies kann im Code erweitert werden (Ist momentan auf 500 begrenzt, damit das Programm nicht unnötigerweise
	unendlich weit läuft. Email & Time Einträge werden im Input zur Duplikat-Ermittlung gelöscht. 
	Daraufhin werden alle bestehenden Duplikate eliminiert. Da Duplikate bereits im GoogleDrive als <Completed> markiert, 
	werden diese auch bei zukünftigen Durchläufen eliminiert.
	Umbennung der Header zu: [Completed, Manufacturer, Description, Part Number]

------------------------

## 3.1 CopyPaste Helper3: FULLY FUNCTIONAL
### Input:
	Input Tabelle.xlsx [Checked, Manufacturer, Description, Part Number] -> ".\"
	Output Tabelle Temp.xlsx [Completed, Part Number, Description, Manufacturer, Hight, Width, Length, Volume, Weight] -> ".\"
### Output:
	Output Tabelle Temp.xlsx [Completed, Part Number, Description, Manufacturer, Hight, Width, Length, Volume, Weight] -> ".\"
	
### Beschreibung:
	Überträgt alle Einträge aus <Input Tabelle> nach <Output Tabelle Temp>.

------------------------

## 4. Extraktion von Traceparts & Unpack: FULLY FUNCTIONAL
### Input:
	Download Folder set to: ".\UIDownloads"
	Applikation: Firefox Browser
	Output Tabelle Temp.xlsx [Completed, Part Number, Description, Manufacturer, Hight, Width, Length, Volume, Weight] -> ".\"
### Output:
	Folder with Unpacked Files: ".\Unpacked"
	All Subfolders with .stp Files inside
### Beschreibung:
	Failed und Completed Elemente werden aus der Liste gelöscht um nur aktuelle Bauteile zu suchen.
	Liest alle Objekte aus und Überträgt die neuen in Traceparts. Bei Erfolg werden die Bestandteile mit <Downloaded> markiert, bei
	scheitern mit <Failed>. Erstellung des Ordners ".\Unpacked". Alle Dateien in ".\UIDownloads" werden nach ".\Unpacked" entpackt 
	und daraufhin gelöscht.

-----------------------

## 5. Bearbeitung in FreeCAD: FULLY FUNCTIONAL
### Input:
	Unpacked Folder with files: ".\Unpacked"
	Output Tabelle Temp.xlsx [Completed, Part Number, Description, Manufacturer, Hight, Width, Length, Volume, Weight] -> ".\"
### Output:
	Output Tabelle Temp.xlsx [Part Number, Description, Manufacturer, Hight, Width, Length, Volume, Weight, Completed] -> ".\"
### Beschreibung:
	Für jeden Eintrag, werden in FreeCAD die Maße ermittelt und in Output Tabelle Temp.xlsx übertragen. Probleme bei der Erkennung von
	FreeCAD bei neu geöffnetem Programm. Nach Abschluss der Analyse werden die Einträge mit <Completed> markiert. Werte werden in die
	entsprechenden Spalten eingetragen

-----------------------

## 6. Übertragung aus Temp nach Output: FULLY FUNCTIONAL
### Input:
	Output Tabelle Temp.xlsx [Part Number, Description, Manufacturer, Hight, Width, Length, Submit Mail, Completed] -> ".\"
	Output Tabelle.xlsx [Part Number, Description, Manufacturer, Hight, Width, Length, Submit Mail, Completed] -> ".\"
### Output:
	Output Tabelle.xlsx [Part Number, Description, Manufacturer, Hight, Width, Length, Submit Mail, Completed] -> ".\"
### Beschreibung:
	Apendet alle neuen Einträge an den bestehenden Datensatz in Output Tabelle.xlsx.

-----------------------

## 7. Upload to Google Docs: FULLY FUNCTIONAL
### Input:
	Output Tabelle.xlsx [Part Number, Description, Manufacturer, Hight, Width, Length, Submit Mail, Completed] -> ".\Output Tabelle.xlsx"
	Google_Drive_Ordner: ITgePA_Rothbaum_Ordner
### Output:
	Google Excel Sheet: Spread_Rothbaum_Output_File [Part Number, Description, Manufacturer, Hight, Width, Length, Submit Mail, Completed]
### Beschreibung:
	Upload der Lokalen Datei zu Google und entfernen der alten Version. Hinterlegt Datei im Ordner <ITgePA_Rothbaum_Ordner>.
  
-----------------------

## 8. CleanUp: FULLY FUNCTIONAL
### Input:
	Input Tabelle.xlsx [Checked, Time, E-Mail, Manufacturer, Description, Part Number] -> ".\"
	Output Tabelle.xlsx [Part Number, Description, Manufacturer, Hight, Width, Length, Submit Mail, Completed] -> ".\"
	Output Tabelle Temp.xlsx [Part Number, Description, Manufacturer, Hight, Width, Length, Submit Mail, Completed] -> ".\"
	Folder with Unpacked Files: ".\Unpacked"
### Output:
### Beschreibung:
	Löscht alle angelegten Tabellen. Löschen des Ordners <.\Unpacked>

