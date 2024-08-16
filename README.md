# carbon_emission
## Question 1: Which products contribute the most to carbon emissions?
| product_name                                                                                                                       | carbon_footprint_pcf | 
| ---------------------------------------------------------------------------------------------------------------------------------: | -------------------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | 3718044              | 
| Wind Turbine G132 5 Megawats                                                                                                       | 3276187              | 
| Wind Turbine G114 2 Megawats                                                                                                       | 1532608              | 
| Wind Turbine G90 2 Megawats                                                                                                        | 1251625              | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | 191687               | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | 167000               | 
| TCDE                                                                                                                               | 99075                | 
| TCDE                                                                                                                               | 99075                | 
| Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | 91000                | 
| Electric Motor                                                                                                                     | 87589                | 
```
SELECT 
    product_name, 
    carbon_footprint_pcf
FROM 
    product_emissions
ORDER BY 
    carbon_footprint_pcf DESC
LIMIT 10

## Question 2: What are the industry groups of these products?
| product_name                                                                                                                       | carbon_footprint_pcf | industry_group                     | 
| ---------------------------------------------------------------------------------------------------------------------------------: | -------------------: | ---------------------------------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | 3718044              | Electrical Equipment and Machinery | 
| Wind Turbine G132 5 Megawats                                                                                                       | 3276187              | Electrical Equipment and Machinery | 
| Wind Turbine G114 2 Megawats                                                                                                       | 1532608              | Electrical Equipment and Machinery | 
| Wind Turbine G90 2 Megawats                                                                                                        | 1251625              | Electrical Equipment and Machinery | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | 191687               | Automobiles & Components           | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | 167000               | Materials                          | 
| TCDE                                                                                                                               | 99075                | Materials                          | 
| TCDE                                                                                                                               | 99075                | Materials                          | 
| Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | 91000                | Automobiles & Components           | 
| Electric Motor                                                                                                                     | 87589                | Capital Goods                      | 
'''
SELECT 
    pe.product_name, 
    pe.carbon_footprint_pcf, 
    ig.industry_group
FROM 
    product_emissions pe
JOIN 
    industry_groups ig ON pe.industry_group_id = ig.id
ORDER BY 
    pe.carbon_footprint_pcf DESC
LIMIT 10
```
## Question 3: What are the industries with the highest contribution to carbon emissions?
| industry_group                                   | total_carbon_emissions | 
| -----------------------------------------------: | ---------------------: | 
| Electrical Equipment and Machinery               | 9801558                | 
| Automobiles & Components                         | 2582264                | 
| Materials                                        | 577595                 | 
| Technology Hardware & Equipment                  | 363776                 | 
| Capital Goods                                    | 258712                 | 
| "Food, Beverage & Tobacco"                       | 111131                 | 
| "Pharmaceuticals, Biotechnology & Life Sciences" | 72486                  | 
| Chemicals                                        | 62369                  | 
| Software & Services                              | 46544                  | 
| Media                                            | 23017                  |
'''
SELECT 
    ig.industry_group, 
    SUM(pe.carbon_footprint_pcf) AS total_carbon_emissions
FROM 
    product_emissions pe
JOIN 
    industry_groups ig ON pe.industry_group_id = ig.id
GROUP BY 
    ig.industry_group
ORDER BY 
    total_carbon_emissions DESC
LIMIT 10

## Question 4: What are the companies with the highest contribution to carbon emissions?
| company_name                            | total_carbon_emissions | 
| --------------------------------------: | ---------------------: | 
| "Gamesa Corporación Tecnológica, S.A."  | 9778464                | 
| Daimler AG                              | 1594300                | 
| Volkswagen AG                           | 655960                 | 
| "Mitsubishi Gas Chemical Company, Inc." | 212016                 | 
| "Hino Motors, Ltd."                     | 191687                 | 
| Arcelor Mittal                          | 167007                 | 
| Weg S/A                                 | 160655                 | 
| General Motors Company                  | 137007                 | 
| "Lexmark International, Inc."           | 132012                 | 
| "Daikin Industries, Ltd."               | 105600                 |
'''
SELECT 
    c.company_name, 
    SUM(pe.carbon_footprint_pcf) AS total_carbon_emissions
FROM 
    product_emissions pe
JOIN 
    companies c ON pe.company_id = c.id
GROUP BY 
    c.company_name
ORDER BY 
    total_carbon_emissions DESC
LIMIT 10

## Question 5: What are the countries with the highest contribution to carbon emissions?
| country_name | total_carbon_emissions | 
| -----------: | ---------------------: | 
| Spain        | 9786130                | 
| Germany      | 2251225                | 
| Japan        | 653237                 | 
| USA          | 518381                 | 
| South Korea  | 186965                 | 
| Brazil       | 169337                 | 
| Luxembourg   | 167007                 | 
| Netherlands  | 70417                  | 
| Taiwan       | 62875                  | 
| India        | 24574                  |
'''
SELECT 
    co.country_name, 
    SUM(pe.carbon_footprint_pcf) AS total_carbon_emissions
FROM 
    product_emissions pe
JOIN 
    countries co ON pe.country_id = co.id
GROUP BY 
    co.country_name
ORDER BY 
    total_carbon_emissions DESC
LIMIT 10

## Question 6: What is the trend of carbon footprints (PCFs) over the years?
| year | total_carbon_emissions | 
| ---: | ---------------------: | 
| 2013 | 503857                 | 
| 2014 | 624226                 | 
| 2015 | 10840415               | 
| 2016 | 1640182                | 
| 2017 | 340271                 |
'''
SELECT 
    year, 
    SUM(carbon_footprint_pcf) AS total_carbon_emissions
FROM 
    product_emissions
GROUP BY 
    year
ORDER BY 
    year ASC;

## Question 7: Which industry groups has demonstrated the most notable decrease in carbon footprints (PCFs) over time?
| industry_group                                                         | emissions_2013 | emissions_2014 | emissions_2015 | emissions_2016 | emissions_2017 | decrease_in_emissions | 
| ---------------------------------------------------------------------: | -------------: | -------------: | -------------: | -------------: | -------------: | --------------------: | 
| Automobiles & Components                                               | 130189         | 230015         | 817227         | 1404833        | 0              | 130189                | 
| Technology Hardware & Equipment                                        | 61100          | 167361         | 106157         | 1566           | 27592          | 33508                 | 
| "Pharmaceuticals, Biotechnology & Life Sciences"                       | 32271          | 40215          | 0              | 0              | 0              | 32271                 | 
| Media                                                                  | 9645           | 9645           | 1919           | 1808           | 0              | 9645                  | 
| Consumer Durables & Apparel                                            | 2867           | 3280           | 0              | 1162           | 0              | 2867                  | 
| "Food, Beverage & Tobacco"                                             | 4995           | 2685           | 0              | 100289         | 3162           | 1833                  | 
| Energy                                                                 | 750            | 0              | 0              | 10024          | 0              | 750                   | 
| Commercial & Professional Services                                     | 1157           | 477            | 0              | 2890           | 741            | 416                   | 
| Utilities                                                              | 122            | 0              | 0              | 122            | 0              | 122                   | 
| Telecommunication Services                                             | 52             | 183            | 183            | 0              | 0              | 52                    | 
| "Textiles, Apparel, Footwear and Luxury Goods"                         | 0              | 0              | 387            | 0              | 0              | 0                     | 
| Semiconductors & Semiconductor Equipment                               | 0              | 50             | 0              | 4              | 0              | 0                     | 
| "Forest and Paper Products - Forestry, Timber, Pulp and Paper, Rubber" | 0              | 0              | 8909           | 0              | 0              | 0                     | 
| Food & Staples Retailing                                               | 0              | 773            | 706            | 2              | 0              | 0                     | 
| Electrical Equipment and Machinery                                     | 0              | 0              | 9801558        | 0              | 0              | 0                     | 
| Trading Companies & Distributors and Commercial Services & Supplies    | 0              | 0              | 239            | 0              | 0              | 0                     | 
| Semiconductors & Semiconductors Equipment                              | 0              | 0              | 3              | 0              | 0              | 0                     | 
| "Mining - Iron, Aluminum, Other Metals"                                | 0              | 0              | 8181           | 0              | 0              | 0                     | 
| Gas Utilities                                                          | 0              | 0              | 122            | 0              | 0              | 0                     | 
| "Consumer Durables, Household and Personal Products"                   | 0              | 0              | 931            | 0              | 0              | 0                     | 
| Tires                                                                  | 0              | 0              | 2022           | 0              | 0              | 0                     | 
| Retailing                                                              | 0              | 19             | 11             | 0              | 0              | 0                     | 
| Household & Personal Products                                          | 0              | 0              | 0              | 0              | 0              | 0                     | 
| Food & Beverage Processing                                             | 0              | 0              | 141            | 0              | 0              | 0                     | 
| Containers & Packaging                                                 | 0              | 0              | 2988           | 0              | 0              | 0                     | 
| Tobacco                                                                | 0              | 0              | 1              | 0              | 0              | 0                     | 
| Chemicals                                                              | 0              | 0              | 62369          | 0              | 0              | 0                     | 
| Software & Services                                                    | 6              | 146            | 22856          | 22846          | 690            | -684                  | 
| Materials                                                              | 200513         | 75678          | 0              | 88267          | 213137         | -12624                | 
| Capital Goods                                                          | 60190          | 93699          | 3505           | 6369           | 94949          | -34759                |
'''
WITH EmissionsByYear AS (
    SELECT 
        ig.industry_group, 
        SUM(CASE WHEN pe.year = 2013 THEN pe.carbon_footprint_pcf ELSE 0 END) AS emissions_2013,
        SUM(CASE WHEN pe.year = 2014 THEN pe.carbon_footprint_pcf ELSE 0 END) AS emissions_2014,
        SUM(CASE WHEN pe.year = 2015 THEN pe.carbon_footprint_pcf ELSE 0 END) AS emissions_2015,
        SUM(CASE WHEN pe.year = 2016 THEN pe.carbon_footprint_pcf ELSE 0 END) AS emissions_2016,
        SUM(CASE WHEN pe.year = 2017 THEN pe.carbon_footprint_pcf ELSE 0 END) AS emissions_2017
    FROM 
        product_emissions pe
    JOIN 
        industry_groups ig ON pe.industry_group_id = ig.id
    GROUP BY 
        ig.industry_group
)
SELECT 
    industry_group, 
    emissions_2013, 
    emissions_2014, 
    emissions_2015, 
    emissions_2016, 
    emissions_2017,
    (emissions_2013 - emissions_2017) AS decrease_in_emissions
FROM 
    EmissionsByYear
ORDER BY 
    decrease_in_emissions DESC;
