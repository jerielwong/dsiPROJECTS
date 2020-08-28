# Ames, Iowa Housing Analysis and Modelling
***
## Problem Statement
Problem

Difficulty in setting the price for a house when there are so many factors to be considered.

For example, in a 2 factor analysis, for a same house size of 789 sq ft , one that is in the heart of the city and one at the suburbs, what should be the ideal selling price given sq ft and location.

The difficulty increases as we factor more parameters, such as sq ft, location, amenities of the house, in this case 3 parameters.

#Solution

Through data science, we use historical data of realised prices of property and its parameters, we study the relationship and formulate a model/equation to predict the price of next house being produced.

#Purpose / Why the need for such a model ?

As a seller of a house, the self-interest, would not be setting a selling price worth less than what model predicts the selling price should be, i.e. not being short changed

As a buyer of a house, the self-interest, would not be over-paying for a property.

## Points to consider
* What features are most relevant for a real estate developer to increase the price of a home?
* In what ways can a real estate developer re-allocate flooring space to increase the price of a home?
* What feature quality is the most relevant to the price of a home?
* What locations should prospective home-owners avoid if they are on a tight budget?
* What features should home-owners exclude to reduce cost?

We will determine this analysis successfuly if we can produce a model with 25-30 features that has a RMSE under 35000, and is able to provide meaningful answers to our business problems.
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


***
#### Conclusion

Conclusion of pricing features

After analysis of the features 
The features that are useful for predict price includes the following 
1st Floor SF 
Gr Liv Area 
Garage Area
Most important feature would be Overall Qual of the house that has the highetst impact on the house 

Limitations

Hyperparameter tuning: A predefined range of values was passed in to tune the hyperparameters for our regularisation models. There is a possibility that there are values outside of the predefined range that could have produced better results.

Other external factors not taken into account: The value of a house is not purely determined by the features we have analysed. There are many other factors which could affect house demand and supply, such as the current economic climate, housing policies, demographic changes, proximity of the house to amenities like malls and schools, and so on. Predictions from our model are limited in its accuracy as it does not consider these factors.

Limited timeframe: Our data comprised only transactions between 2006–2010. This is a pretty short timeframe, which makes it hard to capture actual general trends in sale prices of houses in Ames. The housing market within the 2006-2010 timeframe could be very different from how it is in present time.

***
