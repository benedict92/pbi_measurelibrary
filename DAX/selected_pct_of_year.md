--Bricht eine Gesamtmetrik lineare auf ein Jahr herunter, nach Prozent der vergangenen Laufzeit im ausgewählten Zeitraum.
--Funktioniert auch über mehrere Jahre hinweg. Bspw. Kosten auf Jahresbasis, werden Anteilig einem Zeitraum im Jahr zugeordnet.

--Ersetze D02_Datumstabelle durch die Bezeichnung deiner Datumstabelle
--Ersetze F04_Zielplanung_Budget[Budget_Jobteaser] durch die Spalte, die heruntergebrochen werden soll


VAR _grouped_table =
SUMMARIZE(
    D02_Datumstabelle, D02_Datumstabelle[Year],
    "selected_days_in_year", COUNT(D02_Datumstabelle[Date]),
    "total_days_per_year", CALCULATE(COUNT(D02_Datumstabelle[Date]),ALLEXCEPT(D02_Datumstabelle,D02_Datumstabelle[Year])),
    "total", SUM(F04_Zielplanung_Budget[Budget_JobTeaser]) 
)

VAR _add_relative =
ADDCOLUMNS(
    _grouped_table,
    "selected_date_range_total", ([selected_days_in_year] / [total_days_per_year])*[total]
)

RETURN
SUMX(_add_relative,[selected_date_range_total])