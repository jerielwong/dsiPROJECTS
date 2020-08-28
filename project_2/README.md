# Ames, Iowa Housing Analysis and Modelling
***
## Problem Statement
Heavily driven by the market, housing prices are a reflection of consumer behaviour that highlights preferences of the overall population. In this analysis, we will be contructing various ridge, lasso, and elastic net regression models to predict housing prices in Ames, Iowa. This will not only allow us to forecast future prices, but will also give us points of inference from which we can better understand consumer behaviour.

We will be utilizing the Ames Housing Dataset that documents housing sales from 2006 to 2010. From the location of the home to the interior finish of the garage, this dataset is extremely comprehensive and contains well over 80 features. The provided data dictionary is reflected below, along with an aditional column describing the corresponding data type.

The main metric we will be using to assess the models is RMSE (root mean squared error) as it allows us to accurately assess how a model performs both on train and test data. Although we are optimizing for RMSE, we will also be looking at adjusted R2 to compare between models. We will be limiting our features to between 25 to 30, in order to balance interpretability and accuracy. 

This analysis will largely benefit real estate companies interested in Ames to make better business decisions, but will also benefit individuals looking for a home by allowing them to understand how their preferences may affect the price of a home. In this analysis, we will be looking to answer the following questions:
* What features are most relevant for a real estate developer to increase the price of a home?
* In what ways can a real estate developer re-allocate flooring space to increase the price of a home?
* What feature quality is the most relevant to the price of a home?
* What locations should prospective home-owners avoid if they are on a tight budget?
* What features should home-owners exclude to reduce cost?

We will determine this analysis successfuly if we can produce a model with 25-30 features that has a RMSE under 35000, and is able to provide meaningful answers to our business problems.
***
## Contents
* [Problem Statement](#Problem-Statement)
* [Data Dictionary](#Data-Dictionary)
* [Contents](#Contents)


* 1. [Data Cleaning](#1.-Data-Cleaning)
    *  1.1 [Library Imports](#1.1-Library-Imports)
    *  1.2 [Dataset Imports](#1.2-Dataset-Imports)
    *  1.3 [First Look (Head, Shape, Type, Null)](#1.3-First-Look-(Head,-Shape,-Type,-Null))
    *  1.4 [Handling Null Values](#1.4-Handling-Null-Values)
        * 1.4.1 [Categorical Null Values](#1.4.1-Categorical-Null-Values)
        * 1.4.2 [Numerical Null Values](#1.4.2-Numerical-Null-Values)
            * 1.4.2a [Lot Frontage](#1.4.2a-Lot-Frontage)
            * 1.4.2b [Garage Yr Blt](#1.4.2b-Garage-Yr-Blt)
            * 1.4.2c [Mas Vnr Area](#1.4.2c-Mas-Vnr-Area)
    *  1.5 [Mapping of Ordinal Data](#1.5-Mapping-of-Ordinal-Data)
    *  1.6 [Standardizing Column Names](#1.6-Standardizing-Column-Names)
* 2. [EDA](#2.-EDA)
    *  2.1 [EDA - Numerical](#2.1-EDA---Numerical)
        * 2.1.1 [Numerical Above Threshold](#2.1.1-Numerical-Above-Threshold)
        * 2.1.2a [Numerical Within Threshold 1](#2.1.2a-Numerical-Within-Threshold-1)
        * 2.1.2b [Numerical Within Threshold 2](#2.1.2b-Numerical-Within-Threshold-2)
        * 2.1.2c [Numerical Within Threshold 3](#2.1.2c-Numerical-Within-Threshold-3)
    *  2.2 [EDA - Ordinal](#2.2-EDA---Ordinal)
        * 2.2.1 [Ordinal Above Threshold](#2.2.1-Ordinal-Above-Threshold)
        * 2.2.2 [Ordinal Within Threshold](#2.2.2-Ordinal-Within-Threshold)
    *  2.3 [EDA - Nominal](#2.3-EDA---Nominal)
        * 2.3.1 [Nominal Above Threshold](#2.3.1-Nominal-Above-Threshold)
        * 2.3.2 [Nominal Within Threshold](#2.3.2-Nominal-Within-Threshold)
* 3. [Feature Selection](#3.-Feature-Selection/Engineering)
    *  3.1 [Low Correlation With 'saleprice'](#3.1-Low-Correlation-With-'saleprice')
    *  3.2 [Reduction of Multicollinearity](#3.2-Reduction-of-Multicollinearity)
* 4. [Model Selection](#4.-Model-Selection)
    *  4.1 [Baseline Model](#4.1-Baseline-Model)
    *  4.2 [Iterative Optimization of RMSE](#4.2-Iterative-Optimization-of-RMSE)
    *  4.3 [Regression Metrics Analysis](#4.3-Regression-Metrics-Analysis)
* 5. [Final Model Analysis](#5.-Final-Model-Analysis)
    *  5.1 [Comparison of Baseline and Final Model](#5.1-Comparison-of-Baseline-and-Final-Model)
    *  5.2 [Analysis of Final Model](#5.2-Analysis-of-Final-Model)
* 6. [Kaggle Submission](#6.-Kaggle-Submission)
    *  6.1 [Test Set Cleaning](#6.1-Test-Set-Cleaning)
    *  6.2 [Test Set Prediction & Results](#6.2-Test-Set-Prediction-&-Results)

* 7. [Conclusion](#7.-Conclusion)
    *  7.1 [Business Recommendations](#7.1-Business-Recommendations)
    *  7.2 [Limitations](#7.2-Limitations)
    *  7.3 [Conclusion](#7.3-Conclusion)
    *  7.4 [Further Work](#7.4-Further-Work)
    *  7.5 [Citations](#7.5-Citations)


* [Runtime](#Runtime)
***
## Data Dictionary
|#|Feature|Type|Description|Legend|
|:---|:---|:---|:---|:---|
|1|Id|Numerical|The record ID.|N/A|
|2|PID|Numerical|The sale ID number.|N/A|
|3|MS SubClass|Nominal|The building class.|20 1-STORY 1946 & NEWER ALL STYLES<br>30 1-STORY 1945 & OLDER<br>40 1-STORY W/FINISHED ATTIC ALL AGES<br>45 1-1/2 STORY - UNFINISHED ALL AGES<br>50 1-1/2 STORY FINISHED ALL AGES<br>60 2-STORY 1946 & NEWER<br>70 2-STORY 1945 & OLDER<br>75 2-1/2 STORY ALL AGES<br>80 SPLIT OR MULTI-LEVEL<br>85 SPLIT FOYER<br>90 DUPLEX - ALL STYLES AND AGES<br>120 1-STORY PUD (Planned Unit Development) - 1946 & NEWER<br>150 1-1/2 STORY PUD - ALL AGES<br>160 2-STORY PUD - 1946 & NEWER<br>180 PUD - MULTILEVEL - INCL SPLIT LEV/FOYER<br>190 2 FAMILY CONVERSION - ALL STYLES AND AGES
|4|MS Zoning|Nominal|Identifies the general zoning classification of the sale.|A Agriculture<br>C Commercial<br>FV Floating Village Residential<br>I Industrial<br>RH Residential High Density<br>RL Residential Low Density<br>RP Residential Low Density Park<br>RM Residential Medium Density|
|5|Lot Frontage|Numerical|Linear feet of street connected to property.|N/A|
|6|Lot Area|Numerical|Lot size in square feet.|N/A|
|7|Street|Nominal|Type of road access to property.|Grvl Gravel<br>Pave Paved|
|8|Alley|Nominal|Type of alley access to property.|Grvl Gravel<br>Pave Paved<br>NA No alley access|
|9|Lot Shape|Ordinal|General shape of property.|Reg Regular<br>IR1 Slightly irregular<br>IR2 Moderately Irregular<br>IR3 Irregular|
|10|Land Contour|Nominal|Flatness of the property.|Lvl Near Flat/Level<br>Bnk Banked - Quick and significant rise from street grade to building<br>HLS Hillside - Significant slope from side to side<br>Low Depression|
|11|Utilities|Ordinal|Type of utilities available.|AllPub All public Utilities (E,G,W,& S)<br>NoSewr Electricity, Gas, and Water (Septic Tank)<br>NoSeWa Electricity and Gas Only<br>ELO Electricity only|
|12|Lot Config|Nominal|Lot configuration.|Inside Inside lot<br>Corner Corner lot<br>CulDSac Cul-de-sac<br>FR2 Frontage on 2 sides of property<br>FR3 Frontage on 3 sides of property|
|13|Land Slope|Ordinal|Slope of property.|Gtl Gentle slope<br>Mod Moderate Slope<br>Sev Severe Slope|
|14|Neighborhood|Nominal|Physical locations within Ames city limits.|Blmngtn Bloomington Heights<br>Blueste Bluestem<br>BrDale Briardale<br>BrkSide Brookside<br>ClearCr Clear Creek<br>CollgCr College Creek<br>Crawfor Crawford<br>Edwards Edwards<br>Gilbert Gilbert<br>IDOTRR Iowa DOT and Rail Road<br>MeadowV Meadow Village<br>Mitchel Mitchell<br>Names North Ames<br>NoRidge Northridge<br>NPkVill Northpark Villa<br>NridgHt Northridge Heights<br>NWAmes Northwest Ames<br>OldTown Old Town<br>SWISU South & West of Iowa State University<br>Sawyer Sawyer<br>SawyerW Sawyer West<br>Somerst Somerset<br>StoneBr Stone Brook<br>Timber Timberland<br>Veenker Veenker|
|15|Condition 1|Nominal|Proximity to main road or railroad.|Artery Adjacent to arterial street<br>Feedr Adjacent to feeder street<br>Norm Normal<br>RRNn Within 200' of North-South Railroad<br>RRAn Adjacent to North-South Railroad<br>PosN Near positive off-site feature--park, greenbelt, etc.<br>PosA Adjacent to postive off-site feature<br>RRNe Within 200' of East-West Railroad<br>RRAe Adjacent to East-West Railroad|
|16|Condition 2|Nominal|Proximity to main road or railroad (if a second is present).|Artery Adjacent to arterial street<br>Feedr Adjacent to feeder street<br>Norm Normal<br>RRNn Within 200' of North-South Railroad<br>RRAn Adjacent to North-South Railroad<br>PosN Near positive off-site feature--park, greenbelt, etc.<br>PosA Adjacent to postive off-site feature<br>RRNe Within 200' of East-West Railroad<br>RRAe Adjacent to East-West Railroad|
|17|Bldg Type|Nominal|Type of dwelling.|1Fam Single-family Detached<br>2FmCon Two-family Conversion; originally built as one-family dwelling<br>Duplx Duplex<br>TwnhsE Townhouse End Unit<br>TwnhsI Townhouse Inside Unit|
|18|House Style|Nominal|Style of dwelling.|1Story One story<br>1.5Fin One and one-half story: 2nd level finished<br>1.5Unf One and one-half story: 2nd level unfinished<br>2Story Two story<br>2.5Fin Two and one-half story: 2nd level finished<br>2.5Unf Two and one-half story: 2nd level unfinished<br>SFoyer Split Foyer<br>SLvl Split Level|
|19|Overall Qual|Numerical|Overall material and finish quality.|10 Very Excellent<br>9 Excellent<br>8 Very Good<br>7 Good<br>6 Above Average<br>5 Average<br>4 Below Average<br>3 Fair<br>2 Poor<br>1 Very Poor|
|20|Overall Cond|Numerical|Overall condition rating.|10 Very Excellent<br>9 Excellent<br>8 Very Good<br>7 Good<br>6 Above Average<br>5 Average<br>4 Below Average<br>3 Fair<br>2 Poor<br>1 Very Poor|
|21|Year Built|Numerical|Original construction date.|N/A|
|22|Year Remod/Add|Numerical|Remodel date (same as construction date if no remodeling or additions).|N/A|
|23|Roof Style|Nominal|Type of roof.|Flat Flat<br>Gable Gable<br>Gambrel Gabrel (Barn)<br>Hip Hip<br>Mansard Mansard<br>Shed Shed|
|24|Roof Matl|Nominal|Roof material.|ClyTile Clay or Tile<br>CompShg Standard (Composite) Shingle<br>Membran Membrane<br>MetalMetal<br>Roll Roll<br>Tar&Grv Gravel & Tar<br>WdShake Wood Shakes<br>WdShngl Wood Shingles|
|25|Exterior 1st|Nominal|Exterior covering on house.|AsbShng Asbestos Shingles<br>AsphShn Asphalt Shingles<br>BrkComm Brick Common<br>BrkFace Brick Face<br>CBlock Cinder Block<br>CemntBd Cement Board<br>HdBoard Hard Board<br>ImStucc Imitation Stucco<br>MetalSd Metal Siding<br>Other Other<br>Plywood Plywood<br>PreCast PreCast<br>Stone Stone<br>Stucco Stucco<br>VinylSd Vinyl Siding<br>Wd Sdng Wood Siding<br>WdShing Wood Shingles|
|26|Exterior 2nd|Nominal|Exterior covering on house (if more than one material).|AsbShng Asbestos Shingles<br>AsphShn Asphalt Shingles<br>BrkComm Brick Common<br>BrkFace Brick Face<br>CBlock Cinder Block<br>CemntBd Cement Board<br>HdBoard Hard Board<br>ImStucc Imitation Stucco<br>MetalSd Metal Siding<br>Other Other<br>Plywood Plywood<br>PreCast PreCast<br>Stone Stone<br>Stucco Stucco<br>VinylSd Vinyl Siding<br>Wd Sdng Wood Siding<br>WdShing Wood Shingles|
|27|Mas Vnr Type|Nominal|Masonry veneer type.|BrkCmn Brick Common<br>BrkFace Brick Face<br>CBlock Cinder Block<br>None None<br>Stone Stone|
|28|Mas Vnr Area|Numerical|Masonry veneer area in square feet.|N/A|
|29|Exter Qual|Ordinal|Exterior material quality.|Ex Excellent<br>Gd Good<br>TA Average/Typical<br>Fa Fair<br>Po Poor|
|30|Exter Cond|Ordinal|Present condition of the material on the exterior.|Ex Excellent<br>Gd Good<br>TA Average/Typical<br>Fa Fair<br>Po Poor|
|31|Foundation|Nominal|Type of foundation.|BrkTil Brick & Tile<br>CBlock Cinder Block<br>PConc Poured Contrete<br>Slab Slab<br>Stone Stone<br>Wood Wood|
|32|Bsmt Qual|Ordinal|Height of the basement.|Ex Excellent (100+ inches)<br>Gd Good (90-99 inches)<br>TA Typical (80-89 inches)<br>Fa Fair (70-79 inches)<br>Po Poor (<70 inches)<br>NA No Basement|
|33|Bsmt Cond|Ordinal|General condition of the basement.|Ex Excellent<br>Gd Good<br>TA Typical - slight dampness allowed<br>Fa Fair - dampness or some cracking or settling<br>Po Poor - Severe cracking, settling, or wetness<br>NA No Basement|
|34|Bsmt Exposure|Ordinal|Walkout or garden level basement walls.|Gd Good Exposure<br>Av Average Exposure (split levels or foyers typically score average or above)<br>Mn Mimimum Exposure<br>No No Exposure<br>NA No Basement|
|35|BsmtFin Type 1|Ordinal|Quality of basement finished area.|GLQ Good Living Quarters<br>ALQ Average Living Quarters<br>BLQBelow Average Living Quarters<br>Rec Average Rec Room<br>LwQ Low Quality<br>Unf Unfinshed<br>NA No Basement|
|36|BsmtFin SF 1|Numerical|Type 1 finished square feet.|N/A|
|37|BsmtFin Type 2|Ordinal|Quality of second finished area (if present).|GLQ Good Living Quarters<br>ALQ Average Living Quarters<br>BLQ Below Average Living Quarters<br>Rec Average Rec Room<br>LwQ Low Quality<br>Unf Unfinshed<br>NA No Basement|
|38|BsmtFin SF 2|Numerical|Type 2 finished square feet.|N/A|
|39|Bsmt Unf SF|Numerical|Unfinished square feet of basement area.|N/A|
|40|Total Bsmt SF|Numerical|Total square feet of basement area.|N/A|
|41|Heating|Nominal|Type of heating.|Floor Floor Furnace<br>GasA Gas forced warm air furnace<br>GasW Gas hot water or steam heat<br>Grav Gravity furnace<br>OthW Hot water or steam heat other than gas<br>Wall Wall furnace|
|42|Heating QC|Ordinal|Heating quality and condition.|Ex Excellent<br>Gd Good<br>TA Average/Typical<br>Fa Fair<br>Po Poor|
|43|Central Air|Nominal|Central air conditioning.|N No<br>Y Yes|
|44|Electrical|Nominal|Electrical system.|SBrkr Standard Circuit Breakers & Romex<br>FuseA Fuse Box over 60 AMP and all Romex wiring (Average)<br>FuseF 60 AMP Fuse Box and mostly Romex wiring (Fair)<br>FuseP 60 AMP Fuse Box and mostly knob & tube wiring (poor)<br>Mix Mixed|
|45|1st Flr SF|Numerical|First Floor square feet.|N/A|
|46|2nd Flr SF|Numerical|Second floor square feet.|N/A|
|47|Low Qual Fin SF|Numerical|Low quality finished square feet (all floors).|N/A|
|48|Gr Liv Area|Numerical|Above grade (ground) living area square feet.|N/A|
|49|Bsmt Full Bath|Numerical|Basement full bathrooms.|N/A|
|50|Bsmt Half Bath|Numerical|Basement half bathrooms.|N/A|
|51|Full Bath|Numerical|Full bathrooms above grade.|N/A|
|52|Half Bath|Numerical|Half baths above grade.|N/A|
|53|Bedroom AbvGr|Numerical|Number of bedrooms above basement level.|N/A|
|54|Kitchen AbvGr|Numerical|Number of kitchens.|N/A|
|55|Kitchen Qual|Ordinal|Kitchen quality.|Ex Excellent<br>Gd Good<br>TA Typical/Average<br>Fa Fair<br>Po Poor|
|56|TotRms AbvGrd|Numerical|Total rooms above grade (does not include bathrooms).|N/A|
|57|Functional|Ordinal|Home functionality rating.|Typ Typical Functionality<br>Min1 Minor Deductions 1<br>Min2 Minor Deductions 2<br>Mod Moderate Deductions<br>Maj1 Major Deductions 1<br>Maj2 Major Deductions 2<br>Sev Severely Damaged<br>Sal Salvage only|
|58|Fireplaces|Numerical|Number of fireplaces.|N/A|
|59|Fireplace Qu|Ordinal|Fireplace quality.|Ex Excellent - Exceptional Masonry Fireplace<br>Gd Good - Masonry Fireplace in main level<br>TA Average - Prefabricated Fireplace in main living area or Masonry Fireplace in basement<br>Fa Fair - Prefabricated Fireplace in basement<br>Po Poor - Ben Franklin Stove<br>NA No Fireplace|
|60|Garage Type|Nominal|Garage location.|2Types More than one type of garage<br>Attchd Attached to home<br>Basment Basement Garage<br>BuiltIn Built-In (Garage part of house - typically has room above garage)<br>CarPort Car Port<br>Detchd Detached from home<br>NA No Garage|
|61|Garage Yr Blt|Numerical|Year garage was built.|N/A|
|62|Garage Finish|Ordinal|Interior finish of the garage.|Fin Finished<br>RFn Rough Finished<br>Unf Unfinished<br>NA No Garage|
|63|Garage Cars|Numerical|Size of garage in car capacity.|N/A|
|64|Garage Area|Numerical|Size of garage in square feet.|N/A|
|65|Garage Qual|Ordinal|Garage quality.|Ex Excellent<br>Gd Good<br>TA Typical/Average<br>Fa Fair<br>Po Poor<br>NA No Garage|
|66|Garage Cond|Ordinal|Garage condition.|Ex Excellent<br>Gd Good<br>TA Typical/Average<br>Fa Fair<br>Po Poor<br>NA No Garage|
|67|Paved Drive|Ordinal|Paved driveway.|Y Paved<br>P Partial Pavement<br>N Dirt/Gravel|
|68|Wood Deck SF|Numerical|Wood deck area in square feet|N/A|
|69|Open Porch SF|Numerical|Open porch area in square feet|N/A|
|70|Enclosed Porch|Numerical|Enclosed porch area in square feet|N/A|
|71|3Ssn Porch|Numerical|Three season porch area in square feet.|N/A|
|72|Screen Porch|Numerical|Screen porch area in square feet.|N/A|
|73|Pool Area|Numerical|Pool area in square feet.|N/A|
|74|Pool QC|Ordinal|Pool quality.|Ex Excellent<br>Gd Good<br>TA Average/Typical<br>Fa Fair<br>NA No Pool|
|75|Fence|Nominal|Fence quality.|GdPrv Good Privacy<br>MnPrv Minimum Privacy<br>GdWo Good Wood<br>MnWw Minimum Wood/Wire<br>NA No Fence|
|76|Misc Feature|Nominal|Miscellaneous feature not covered in other categories.|Elev Elevator<br>Gar2 2nd Garage (if not described in garage section)<br>Othr Other<br>Shed Shed (over 100 SF)<br>TenC Tennis Court<br>NA None|
|77|Misc Val|Numerical|$Value of miscellaneous feature.|N/A|
|78|Mo Sold|Numerical|Month Sold.|N/A|
|79|Yr Sold|Numerical|Year Sold.|N/A|
|80|Sale Type|Nominal|Type of sale.|WD Warranty Deed - ConventionalCWD Warranty Deed - Cash<br>VWD Warranty Deed - VA Loan<br>New Home just constructed and sold<br>COD Court Officer Deed/Estate<br>Con Contract 15% Down payment regular terms<br>ConLw Contract Low Down payment and low interest<br>ConLI Contract Low Interest<br>ConLD Contract Low Down<br>Oth Other|
|81|SalePrice|Numerical|The property's sale price in dollars. This is the target variable that we are trying to predict.|N/A|

***

## Conclusion & Recommendations
#### Findings

* **Space**
    * One square foot increase in above grade(ground) living area correlates with a saleprice increase of $17000

    * One square foot increase in garage area correlates with a saleprice increase of $6800

    * One square foot increase in lot frontage correlates with a saleprice **decrease** of $4300

    * One square foot increase on the first floor correlates with a saleprice increase of $3900

    * One square foot increase in lot area correlates with a saleprice increase of $3200

    * One square foot increase in the basement correlates with a saleprice increase of $2000

    * One square foot increase in masonry veneer correlates with a saleprice increase of $1900



* **Quality**
    * One grade increase in overall material and finish quality correlates with a saleprice increase of $17000

    * One grade increase in kitchen quality correlates with a saleprice increase of $7900

    * One grade increase in external material quality correlates with a saleprice increase of $6700
    
    * One grade increase in walkout or garden level basement walls correlates with a saleprice increase of $6300


* **Location**
    * A property in Northridge Heights correlates with a saleprice increase of $12000

    * A property in Stone Brook correlates with a saleprice increase of $9700

    * A property in Northridge correlates with a saleprice increase of $4900

    * A property in Somerset correlates with a saleprice increase of $3800


* **Type**

    * A 1-story planned unit development built in 1946 or newer correlates with a saleprice **decrease** of $8100

    * A 2-story planned unit development built in 1946 or newer correlates with a saleprice **decrease** of $5700

    * A 2 family conversion property correlates with a saleprice **decrease** of $2000

    * A 2-story home built in 1946 or newer correlates with a saleprice **decrease** of $240


* **Features**
    * Having one additional fireplace correlates with a saleprice increase of $6000

    * A property with exterior covering of wood siding correlates with a saleprice **decrease** of $5200

    * The more recently a property is remodelled correlates with a saleprice increase of $4500 per year.

    * One grade increase in basement finish correlates with saleprice increase of $4300

    * One grade increase in garage finish correlates with a saleprice increase of $4100

    * Having a hip roof style correlates with a saleprice increase of $3900

    * Having a secondary exterior covering wood correlates with a saleprice increase of $3700

    * One additional bathroom correlates with a saleprice increase of $2700

    * Not having a garage correlates with a saleprice increase of $1800

    * Having a secondary exterior covering of hard board correlates with a saleprice **decrease** of $990

    * Not having masonry veneer correlates with a saleprice increase of $980

---

#### Interpretation

* **Real Estate Developers (Primary Stakeholders)**

    * Build additional floors for livable space if the cost is less than $17000 per square foot

    * Increase garage area if cost is less than $6800 per square foot

    * Increase first story space if cost is less than $3900 per square foot

    * Increase lot area if cost is less than $3200 per square foot

    * Increase basement area if cost is less than $2000 per square foot

    * Increase masonry veneer if cost is less than $1900 per square foot

    * Increase quality of material and finish if cost per grade is less than $17000

    * Increase quality of kitchen if cost per grade is less than $7900

    * Increase quality of external material if cost per grade is less than $6700

    * Avoid developing planned unit development and 2 family conversion properties.

    * Add an additional fireplace if the cost is less than $6000

    * Avoid exterior covering of wood unless it can reduce cost by more than $5200

Although these are general actions that real estate developers can take, it should be noted that it may not be applicable for all cases. For example, we see that with fireplaces the saleprice does not significantly increase beyond 2 fireplaces. This means that developers should only consider increasing or adding features when these features reside are on the lower side of the spectrum.

* **Individuals Looking for a Home (Secondary Stakeholders)**

    * Buy a house without a fireplace and install it on your own as the cost will be significantly lower. [[1]](#7.3-Citations)
    * If on a tight budget, do consider planned development units as they can fetch for lower prices.
    * It may be wise to find a property with an unfurnished kitchen if you can keep furnishing costs low.
    * Avoid locations such as Northridge, Northridge Heights, Stone Brook, and Somerset if on a tight budget.

---

#### Answers to Questions

* What features are most relevant for a real estate developer to increase the price of a home?
    * Quality of walkout or garden level basement walls
    * Fireplace
    * Quality of garage finish
* In what ways can a real estate developer re-allocate flooring space to increase the price of a home?
    * Increase above ground living area
    * Increase garage area
    * Reduce lot frontage
* What feature quality is the most relevant to the price of a home?
    * Overall material and finish quality
    * External material quality
* What locations should prospective home-owners avoid if they are on a tight budget?
    * Northridge Heights
    * Stone Brook
    * Northridge
    * Somerset
* What features should home-owners exclude to reduce cost?
    * Fireplace
    * Basement Finish
***
#### Conclusion

In conclusion, this analysis has successfully identified key features for developers and prospective home-owners alike. A final regression model was also found with 30 features, having a RMSE within pre-defined limits (under 35000). 

Our final model consisted of 30 features utilizing a ordinary least squares model. Although our final model may have been slightly underfit, for a kaggle submission it is better to err on the side of underfitting due to the variability of a test dataset.

The findings suggests that homeowners tend to heavily favor living area above ground in favor of living area underground. It also suggests that many homeowners are willing to pay for better overall quality/materials. The data also points out that one of the best features for a developer to include is a fireplace.

Overall this analysis has beeen a success, however there is always room for improvement.
***
#### Further Work

* It may be worth exploring if constructing various models split by location, or housing type may give better results. For example, constructing a model for each housing type to see if we can more accurately pinpoint saleprice.


* Polynomial features could be modelled individually against saleprice to determine if they have a polynomial relationship with saleprice.


* K-nearest neighbors could be used to impute missing ordinal data.


* Iteration and sampling of RMSE values could be applied and then a categorization model could be built to classify these features as 'useful' or 'not useful'.