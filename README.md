Jet Airline Safety: Aviation Accident Data Analysis
Overview
This project analyzes NTSB (National Transportation Safety Board) civil aviation accident data to support a business decision: our company is expanding into the aviation industry and needs a data-driven answer to which aircraft carry the lowest operational risk, so leadership can avoid purchasing into an aircraft category or manufacturer with a disproportionately high accident or fatality history.
Business Problem
The client's brief boils down to one question: if we're buying aircraft for commercial/private enterprise use, which ones are historically the safest bet?
To answer that with real evidence, this analysis works through four sub-questions:
Which aircraft manufacturers/models have historically shown the lowest injury and destruction rates?
Does aircraft size (large passenger vs. small aircraft) meaningfully change the risk profile?
Do operational/environmental factors (weather, phase of flight, purpose of flight) change risk enough to inform operating policy?
How has the accident rate trended over time? Is aviation getting safer, and is older accident data still representative of today's risk?
Data
Source: NTSB Aviation Accident Database (AviationData.csv) U.S. civil aviation accidents and selected incidents, 1962–present.
Scope applied:
Restricted to accidents from 1983 onward; aircraft design/regulation before this era isn't representative of aircraft the client would realistically purchase today.
Restricted to Aircraft.Category: Airplane, excluding amateur-built aircraft the client is evaluating; certified, commercially relevant aircraft, not homebuilt planes, helicopters, or gliders.
Manufacturers retained only if they have at least 50 recorded accidents, so risk rates are statistically meaningful rather than based on a handful of incidents.
Methodology
1. Data Cleaning (Pandas)
Standardized inconsistent column names across NTSB export vintages (e.g., Aircraft. damage vs. Aircraft_Damage)
Consolidated manufacturer name variants (e.g., MCDONNELL DOUGLAS → BOEING, AIRBUS INDUSTRIE → AIRBUS) so the same real-world manufacturer isn't split across labels
Built derived features:
Total.Passengers and Severe.Injury.Rate (normalized so aircraft of different capacities are comparable)
Is.Destroyed (binary flag from aircraft damage status)
Aircraft.Size (Large Passenger vs. Small Aircraft, based on engine count and occupancy)
Plane.Type (unique Make + Model identifier)
Dropped columns with >50% missing data
2. Descriptive Analysis
Used groupby, agg, and pivot_table to answer the business questions directly:
Accident volume by year
Risk profile (accident count, average severe injury rate, fatalities, destroyed rate) by manufacturer
Severe injury rate by aircraft size
Accident severity by weather condition
Accident count by phase of flight
Combined aircraft size × weather condition risk (pivot table)
3. Visualizations
Six charts (trend line, bar charts, box plot, heatmap) built with matplotlib/seaborn, each tied directly to one of the analyses above.
Key Findings
Manufacturer risk varies meaningfully. Some manufacturers show a consistently lower average severe-injury rate across hundreds of recorded accidents; these should be prioritized on any aircraft purchase shortlist (see the manufacturer ranking in the notebook for specifics).
Large passenger aircraft show a lower per-occupant severe injury rate than small aircraft, supporting certified multi-engine commercial-scale aircraft as the safer category for the client's expansion, all else equal.
Weather conditions matter. Accidents in instrument (low-visibility) conditions tend to have higher average fatality and destroyed-aircraft rates than in visual conditions, supporting conservative weather-minimum operating policies.
Takeoff and landing account for the largest share of accidents, indicating where pilot training and procedural safety investment should be concentrated.
