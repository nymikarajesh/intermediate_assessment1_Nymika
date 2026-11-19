# intermediate_assessment1_Nymika
vehicle_type=VLOOKUP([@[Vehicle_ID]],Vehicle_Master!A:B,2,0)
Fuel_cost=[@[Fuel_Consumed_L]]*95
KM_per_ltr=[@[Distance_km]]/[@[Fuel_Consumed_L]]
if [Delivery_Status] = "On-Time" then 1 else 0
Fuel Efficiency = DIVIDE ( SUM ( Trip_Data1[Distance_km] ), SUM ( Trip_Data1[Fuel_Consumed_L] ) )
Total Trips = COUNTROWS ( Trip_Data1 )

On-Time Trips =
CALCULATE ( [Total Trips], Trip_Data1[Delivery_Status] = "On-Time" )

On-Time Delivery % = DIVIDE ( [On-Time Trips], [Total Trips] )
Fuel Cost = SUM ( Trip_Data1[Fuel_cost] )

Maintenance Cost =
SUMX (
    VALUES ( Trip_Data1[Vehicle_ID] ),
    LOOKUPVALUE (
        Vehicle_Master[Maintenance_Cost],
        Vehicle_Master[Vehicle_ID], Trip_Data1[Vehicle_ID]
    )
)

Cost per km =
DIVIDE ( [Fuel Cost] + [Maintenance Cost], SUM ( Trip_Data1[Distance_km] ) )
Total Trips = COUNTROWS ( Trip_Data1 )
On-Time Trips = CALCULATE ( [Total Trips], Trip_Data1[Delivery_Status] = "On-Time" )
On-Time Delivery % = DIVIDE ( [On-Time Trips], [Total Trips] )
Fuel Cost = SUM ( Trip_Data1[Fuel_cost] )
Maintenance Cost =
SUMX (
    VALUES ( Trip_Data1[Vehicle_ID] ),
    LOOKUPVALUE (
        Vehicle_Master2[Maintenance_Cost],
        Vehicle_Master2[Vehicle_ID], Trip_Data1[Vehicle_ID]
    )
)
Cost per km = DIVIDE ( [Fuel Cost] + [Maintenance Cost], SUM ( Trip_Data1[Distance_km] ) )
