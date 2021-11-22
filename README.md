# Gesundheitsdaten und Pandemiebewältigung 

Dieses Repository enthält R Markdown-Files und Daten im .rds- und .cvs-Format, die für die Datenaufbereitung und -analyse der Gebarungsprüfung [Gesundheitsdaten und Pandemiebewältigung](https://www.rechnungshof.gv.at/rh/home/home/home_3/Berichte_des_Rechnungshofes_im_Ueberblick.html) verwendet wurden. Mit diesen Daten können Abbildungen 4, 7 und 8 bzw. Abbildungen E, F und G im Anhang des Berichts erstellt werden.  

## Anmerkung: 

- Alle Analyseschritte wurden mit der Statistiksoftware R durchgeführt und in R Markdown-Files dokumentiert; Informationen zur Analyseumgebung finden Sie am Ende jedes R Markdown-Files. 
- Für das R-Projekt wurde mit dem [renv](https://rstudio.github.io/renv/index.html)-Package ein Lockfile mit allen notwendigen Packages erstellt, das sich ebenfalls im Repository befindet.
- Der Rechnungshof verwendet für Berichtsgrafiken ein eigenes [ggplot](https://ggplot2.tidyverse.org/index.html)-Theme. Da dies nicht veröffentlicht werden kann, werden alle Grafiken mit den Standardeinstellungen von R dargestellt.

## Daten:
Die Rohdaten stammen aus diesem Github-Repository: https://github.com/statistikat/coronaDAT. Das Repository umfasst zahlreiche COVID-19 bezogene Datensätze (u.a. die täglich gemeldete Zahl der Neuinfektionen, Tests oder Sterbefälle), die mehrmals täglich von den Websites des Gesundheitsministeriums (https://info.gesundheitsministerium.at/) und der Österreichische Agentur für Gesundheit und Ernährungssicherheit GmbH (AGES; https://covid19-dashboard.ages.at/) heruntergeladen werden. 

Downloadzeitpunkt: Dieses Github-Repository wurde am 03.04.2021 in den Ordner "../data/archive" heruntergeladen (ca. 400 MB). 

## R Skripte - Datenaufbereitung
Für die Aufbereitung der Rohdaten werden zwei R Skripte benötigt:

1. unzip.Rmd: Dieses File entzippt die Rohdaten aus dem [Github-Repository](https://github.com/statistikat/coronaDAT) im Ordner "../data/archive" und speichert die Daten in den Ordner "../data/strukturiert". Hierfür müssen zunächst die Daten von Github heruntergeladen werden. 

2. preprocessing.Rmd: Da die Rohdaten weitere von der AGES bzw. dem Gesundheitsministerium veröffentlichten Daten umfassen, werden in diesem Skript die täglich gemeldeten Neuinfektionszahlen extrahiert. In den Daten gibt es darüber hinaus unterschiedliche Datenquellen (AGES, Gesundheitsministerium). Der final bearbeitete Datensatz umfasst die täglichen Infektionszahlen sowie Information aus welcher Datenquelle diese stammen. Das finale Datenfile wird in "../data/epi_long_quelle.rds" gespeichert und beinhaltet:

	- die Zahl der täglich gemeldeten Neuinfektionen (erkrankte)
	- den Namen des Files, aus dem diese Information stammt (file_name)
	- das Veröffentlichungsdatum (datum)
	- den Veröffentlichungszeitpunkt (publikationszeitpunkt)
	- die Datenquelle (quelle)
	- den Publikationstag (publikationstag) 
	
Anmerkung: Aufgrund der Datenmenge und Anzahl an notwendigen Schritten zur Vorbereitung der Daten nehmen diese beiden R Skripts viel Zeit in Anspruch. Der Rechnungshof stellt daher das überarbeitete, für die weiteren Analysen notwendige File auch unter "..data/epi_long_quelle.rds" zur Verfügung (ca. 100 MB). Alle weiteren Analysen können daher auch mit diesem File reproduziert werden. 
	
## R Skripte - Datenanalyse und Visualisierung

1. analyse_datenquellen.Rmd: Dieses Skript analysiert Unterschiede zwischen den durch die AGES bzw. das Gesundheitsministerium gemeldeten Neuinfektionszahlen. In diesem File werden die Abbildungen E, F, G des Anhangs erstellt. 

2. analyse_infektionsverlauf.Rmd: Dieses Skript stellt anhand der AGES-Daten die zeitlichen Verläufe der Neuinfektionen, der Todesfälle und der täglichen Tests dar. Es werden die Abbildungen 4, 7, und 8 des Hauptteils des Berichts erstellt. Für die Analysen werden Daten vom 03.04.21 (14:02 Uhr) aus dem [Github-Repository](https://github.com/statistikat/coronaDAT) verwendet. Diese sind ebenfalls in unserem Repository enthalten (sofern das [Github-Repository](https://github.com/statistikat/coronaDAT) geclont wurde, können auch die identen Daten verwendet werden). Für die Berechnung der Inzidenzzahlen ist darüber hin das File "bevoelkerung_bundeslaender.rds" im Repository enthalten.
