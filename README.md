# retailpro-data-analytics8
En el panel de campos, se pueden visualizar otras medidas, adicionales a las solicitadas, estas serán usadas en mi entrega final.
% Crecimiento Semestral = VAR VentasActual   = [Total Ventas]
VAR VentasAnterior = [Ventas Semestre Anterior]
RETURN
    DIVIDE(
        VentasActual - VentasAnterior,
        VentasAnterior,
        0
    )
    Ventas Semestre Anterior = 
CALCULATE(
    [Total Ventas],
    DATEADD(Dim_Fechas[Date], -6, MONTH)
)
Ventas STD = VAR MaxFecha = MAX(Dim_Fechas[Date])
VAR SemestreActual = MAX(Dim_Fechas[Semestre Número])
VAR AnioActual = MAX(Dim_Fechas[Año])
RETURN
CALCULATE(
    [Total Ventas],
    FILTER(
        ALL(Dim_Fechas),
        Dim_Fechas[Año] = AnioActual &&
        Dim_Fechas[Semestre Número] = SemestreActual &&
        Dim_Fechas[Date] <= MaxFecha
    )
)
