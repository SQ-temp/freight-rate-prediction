Name|Description 
|---|---|
load_id|The id of the shipment 
pickup|The place where the shipment located 
delivery|Where to deliver or transport 
pickup_lat| shipment latitude 
pickup_lon| shipment longitude
delivery_lat| Target place to delvier latitude
delivery_lon| Target place to delvier longitude
distance| The distance between the pickup city and the target 
equipment| The type of the van 
weight| shipment weight  
date| shipment date 
market_index| market signals 
quote_signal| after checking the data, it equals the rate per mile (posted_rate / distance) in months 1,2,3,6,9 and is noise in the other months (leakage), dropped 
posted_rate| the price of the shipment in dollar 


