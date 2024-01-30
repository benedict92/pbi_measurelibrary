Conversions Gesamt SPLY = 
CALCULATE(
    [Conversions Gesamt], 
    SAMEPERIODLASTYEAR(DATESBETWEEN(D02_Datumstabelle[Date], MIN(D02_Datumstabelle[Date]), TODAY())))

--Returns the measure for the sameperiodlastyear until today.
--Applys for cases where you use an external filter e.g. Date >= 2023-10-01 and you want to be sure only values up until today are considered.
--Example:
--Today = 2024-01-30; Max of your Datetable: 2024-12-31; you set the filter Date >= 2023-10-01
--You want to compare 2023-10-01..2024-01-30 vs. sameperiodlastyear
--Without the conditions below SAMEPERIODLASTYEAR returns 2022-10-01..2023-12-31 !!! That's wrong!