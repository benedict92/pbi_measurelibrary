cf_total_compare_sply = 
VAR _ts = [Ticketsales_OLS]
VAR _ts_sply = [Ticketsales_OLS SPLY]
VAR _pct_delta = DIVIDE(_ts,_ts_sply,0)-1

VAR limit_red = -0.05 //all values below this one will become red
VAR limit_green = 0.05 //all values above this one will become green

RETURN
SWITCH(
    TRUE(),
    _pct_delta < limit_red, "#C00000", //red
    _pct_delta >= limit_red && _pct_delta <= limit_green, "#ffd966", //yellow
    _pct_delta > limit_green,"#6aa84f", //green
    BLANK()
)