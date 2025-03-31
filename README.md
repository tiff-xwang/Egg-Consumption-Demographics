# Egg Consumption Demographics
🪺🥚🍳🍮

## Goal
I started this project in February 2025 when the bird flu shot up egg prices everywhere.
Hoping to find out more about how the egg shortage would impact consumers, I dived into <a href="https://wwwn.cdc.gov/nchs/nhanes/default.aspx">CDC's National Health and Nutrition Examination Survey</a> that sheds light on what Americans eat.

## Findings
After filtering for food containing eggs (omelettes, hard-boiled, egg salad...), I found that most people consumed fewer eggs from 2013 to 2023, except the rich, whose family income was about five times or more than the <a href="https://aspe.hhs.gov/topics/poverty-economic-mobility/poverty-guidelines/prior-hhs-poverty-guidelines-federal-register-references/2023-poverty-guidelines-computations">poverty threshold</a>. That means for a one-person family in 2023, their income was $14,580 x 5 = $72,900.
 
## Data & Workflow
All the datasets I used are in [docs](docs). 

First, to filter down to egg dishes, I cross-referenced food codes I copied by hand from [USDA's website](https://fdc.nal.usda.gov/food-search?type=Survey%20(FNDDS)) with their ready-made [Excel](docs/WWEIA1112_foodcat_FNDDS.xlsx), and came out with a [comprehensive list](docs/appended_egg_codes.xlsx) that should include all the egg-related food codes.

Then, for each two-year survey, I followed this workflow:
1. Get participant number ('SEQN') and food codes ('DR1IFDCD') from the [dietary survey](https://wwwn.cdc.gov/nchs/nhanes/default.aspx) (downloaded local files look like '[DR1IFF_J.xpt](docs/2017-18/DR1IFF_J.xpt)')
<br>⇩</br>
2. Filter for eggs in food codes and rename columns={"DR1IFDCD": "food_code"}
⇩
3. Get income-to-poverty ratio ('INDFMPIR') from [demographics data](https://wwwn.cdc.gov/nchs/nhanes/search/datapage.aspx?Component=Demographics) (downloaded local files look like '[DEMO_J.xpt](docs/2017-18/DEMO_J.xpt)')
⇩
4. Rename columns={"INDFMPIR": "income_poverty"}
⇩
5. Join dietary and demographics data, which produces a new dataset called 'egg_consumption_demo.xlsx', with columns 'SEQN', 'food_code', and 'income_poverty'
⇩
5. Plot / exploratory data analysis