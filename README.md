# Credit Line Increase Model Card

# Basic Information

•Person or organization developing model: Agnes, agnes@gmc.com

• Model date: August, 2022

• Model version: 1.0.2

• License: MIT

• Model implementation code: [DNSC_6301_Project.ipynb](https://github.com/Agnes-Ngue/Hello-world/blob/main/GWU_DNSC_6301_project.ipynb)

•Intended Use

    * Primary intended uses: This model is an example probability of default classifier, with an example use case for determining eligibility for a             credit line increase.

    * Primary intended users: Students in GWU DNSC 6301 bootcamp.

    * Out-of-scope use cases: Any use beyond an educational example is out-of-scope.
                       




# Training Data

• Data dictionary:

| Name      | Modeling Role            | Measurement Level | Description                                     |
|-----------|--------------------------|-------------------|-------------------------------------------------|
| ID        | ID                       | int               | unique row indentifier                          |
| LIMIT_BAL | input                    | float             | amount of previously awarded credit             |
| SEX       | demographic information  | int               | 1 = male; 2 = female                            |
| RACE      | demographic information  | int               | 1 = hispanic; 2 = black; 3 = white; 4 = asian   |
| EDUCATION | demographic information  | int               | 1 = graduate school; 2 = university; 3 = high school; 4 = others |
| MARRIAGE  | demographic information  | int               | 1 = married; 2 = single; 3 = others             |
| AGE       | demographic information  | int               | age in years                                    |
|PAY_0, PAY_2 - PAY_6     | inputs                   | int        | history of past payment; PAY_0 = the repayment status in September, 2005; PAY_2 = the repayment status in August, 2005; ...; PAY_6 = the repayment status in April, 2005. The measurement scale for the repayment status is: -1 = pay duly; 1 = payment delay for one month; 2 = payment delay for two months; ...; 8 = payment delay for eight months; 9 = payment delay for nine months and above |
| BILL_AMT1 - BILL_AMT6    | inputs  | float | amount of bill statement; BILL_AMNT1 = amount of bill statement in September, 2005; BILL_AMT2 = amount of bill statement in August, 2005; ...; BILL_AMT6 = amount of bill statement in April, 2005           |
| PAY_AMT1 - PAY_AMT6     | inputs  | float | amount of previous payment; PAY_AMT1 = amount paid in September, 2005; PAY_AMT2 = amount paid in August, 2005; ...; PAY_AMT6 = amount paid in April, 2005                                    |
| DELINQ_NEXT    | target  | int | whether a customer's next payment is delinquent (late), 1 = late; 0 = on-time                                       |

• Source of training data: GWU Blackboard, email jphall@gwu.edu for more information


• How training data was divided into training and validation data: 50% training, 25% validation, 25% test


• Number of rows in training and validation data:

    * Training rows: 15,000
    
    * Validation rows: 7,500
    
    
    
    
# Test Data

• Source of test data: GWU Blackboard, email jphall@gwu.edu for more information

• Number of rows in test data: 7,500

• State any differences in columns between training and test data: None



# Model details


• Columns used as inputs in the final model: 'LIMIT_BAL', 'PAY_0', 'PAY_2', 'PAY_3', 'PAY_4', 'PAY_5', 'PAY_6', 'BILL_AMT1', 'BILL_AMT2', 'BILL_AMT3', 'BILL_AMT4', 'BILL_AMT5', 'BILL_AMT6', 'PAY_AMT1', 'PAY_AMT2', 'PAY_AMT3', 'PAY_AMT4', 'PAY_AMT5', 'PAY_AMT6'

• Column(s) used as target(s) in the final model: 'DELINQ_NEXT'

• Type of model: Decision Tree

• Software used to implement the model: Python, scikit-learn

• Version of the modeling software: 0.22.2.post1

• Hyperparameters or other settings of your model:

    DecisionTreeClassifier   (ccp_alpha=0.0, class_weight=None, criterion='gini',
                             max_depth=6, max_features=None, max_leaf_nodes=None,
                             min_impurity_decrease=0.0, min_impurity_split=None,
                             min_samples_leaf=1, min_samples_split=2,
                             min_weight_fraction_leaf=0.0, presort='deprecated',
                             random_state=12345, splitter='best')`


# Quantitative Analysis

• Correlation Heatmap       


![image](https://user-images.githubusercontent.com/111556214/186575609-18b8e494-6bb5-48b7-9eef-2b818c1081cc.png)


○ Metrics used to evaluate your final model (AUC and AIR): 

○ State the final values, neatly -- as bullets or a table, of the metrics for all data: training, validation, and test data

○ Provide any plots related to your data or final model -- be sure to label the plots!


# Load and analyze data 

• Names of the columns in the training data

        Index(['ID', 'LIMIT_BAL', 'SEX', 'RACE', 'EDUCATION', 'MARRIAGE', 'AGE',
               'PAY_0', 'PAY_2', 'PAY_3', 'PAY_4', 'PAY_5', 'PAY_6', 'BILL_AMT1',
               'BILL_AMT2', 'BILL_AMT3', 'BILL_AMT4', 'BILL_AMT5', 'BILL_AMT6',
               'PAY_AMT1', 'PAY_AMT2', 'PAY_AMT3', 'PAY_AMT4', 'PAY_AMT5', 'PAY_AMT6',
               'DELINQ_NEXT'],
              dtype='object')

• Determine whether any missing values exist in the training data: 'there are no missing values'

• basic descriptive statistics for the data  

|index|ID|LIMIT\_BAL|SEX|RACE|EDUCATION|MARRIAGE|AGE|PAY\_0|PAY\_2|PAY\_3|PAY\_4|PAY\_5|PAY\_6|BILL\_AMT1|BILL\_AMT2|BILL\_AMT3|BILL\_AMT4|BILL\_AMT5|BILL\_AMT6|PAY\_AMT1|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|count|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|30000\.0|
|mean|15000\.5|167484\.32266666667|1\.6037333333333332|2\.721966666666667|1\.8531333333333333|1\.5518666666666667|35\.4855|-0\.0167|-0\.13376666666666667|-0\.1662|-0\.22066666666666668|-0\.2662|-0\.2911|51223\.3309|49179\.07516666667|47013\.1548|43262\.94896666666|40311\.40096666667|38871\.7604|5663\.5805|
|std|8660\.398374208891|129747\.66156720239|0\.48912919609026045|1\.0943966628653183|0\.7903486597207291|0\.5219696006132486|9\.217904068090188|1\.1238015279973348|1\.1971859730345533|1\.1968675684465735|1\.1691386224023375|1\.1331874060027483|1\.1499876256079027|73635\.86057552956|71173\.76878252835|69349\.38742703684|64332\.85613391631|60797\.15577026487|59554\.10753674573|16563\.280354025766|
|min|1\.0|10000\.0|1\.0|1\.0|0\.0|0\.0|21\.0|-2\.0|-2\.0|-2\.0|-2\.0|-2\.0|-2\.0|-165580\.0|-69777\.0|-157264\.0|-170000\.0|-81334\.0|-339603\.0|0\.0|
|25%|7500\.75|50000\.0|1\.0|2\.0|1\.0|1\.0|28\.0|-1\.0|-1\.0|-1\.0|-1\.0|-1\.0|-1\.0|3558\.75|2984\.75|2666\.25|2326\.75|1763\.0|1256\.0|1000\.0|
|50%|15000\.5|140000\.0|2\.0|3\.0|2\.0|2\.0|34\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|22381\.5|21200\.0|20088\.5|19052\.0|18104\.5|17071\.0|2100\.0|
|75%|22500\.25|240000\.0|2\.0|4\.0|2\.0|2\.0|41\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|67091\.0|64006\.25|60164\.75|54506\.0|50190\.5|49198\.25|5006\.0|
|max|30000\.0|1000000\.0|2\.0|4\.0|6\.0|3\.0|79\.0|8\.0|8\.0|8\.0|8\.0|8\.0|8\.0|964511\.0|983931\.0|1664089\.0|891586\.0|927171\.0|961664\.0|873552\.0|


• The Pearson correlation matrix for the data 

|index|ID|LIMIT\_BAL|SEX|RACE|EDUCATION|MARRIAGE|AGE|PAY\_0|PAY\_2|PAY\_3|PAY\_4|PAY\_5|PAY\_6|BILL\_AMT1|BILL\_AMT2|BILL\_AMT3|BILL\_AMT4|BILL\_AMT5|BILL\_AMT6|PAY\_AMT1|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|ID|1\.0|0\.026179157746200676|0\.018497494176208946|-0\.0007102065338193472|0\.03917673481156991|-0\.029079425318771064|0\.018677734490293255|-0\.030574932272971513|-0\.011214868262343643|-0\.01849355375769933|-0\.0027348897819592004|-0\.022199231870021336|-0\.020270134067212064|0\.019388673917611145|0\.017981897457701318|0\.024354050018843155|0\.040350602942506635|0\.01670530315635218|0\.016729618316253813|0\.009742443464325092|
|LIMIT\_BAL|0\.026179157746200676|1\.0|0\.02475523511164408|0\.044173026578891675|-0\.2191606982292116|-0\.10813941027801287|0\.14471279755733674|-0\.2712143321347179|-0\.29638210099648243|-0\.2861229539031144|-0\.267460009639393|-0\.2494113948241093|-0\.23519539948542492|0\.28542986496498995|0\.27831436399776105|0\.28323578358168416|0\.29398762371598486|0\.29556233765823164|0\.29038895064794745|0\.1952359152322094|
|SEX|0\.018497494176208946|0\.02475523511164408|1\.0|0\.006148749854590956|0\.014231936162206107|-0\.03138884007085218|-0\.0908736465273919|-0\.05764287886698678|-0\.07077100316682232|-0\.06609605640043047|-0\.060173238366203696|-0\.055063885035226384|-0\.044007788187657874|-0\.03364186958914916|-0\.031183472229667317|-0\.024563311681403167|-0\.02187967907348509|-0\.017005180187325976|-0\.016733126348159072|-0\.00024245456294142142|
|RACE|-0\.0007102065338193472|0\.044173026578891675|0\.006148749854590956|1\.0|-0\.0127955003008222|0\.0070095169916305445|0\.0012839240637674137|-0\.10248713899221379|-0\.08298645557341092|-0\.07454738082082236|-0\.07225921773723935|-0\.0673156345068685|-0\.05493481654028164|0\.004232183602562254|0\.0024588210917865696|0\.0005427412255774552|0\.00037565765065118885|0\.002096489670050675|0\.0027561414727044244|0\.030069238440955968|
|EDUCATION|0\.03917673481156991|-0\.2191606982292116|0\.014231936162206107|-0\.0127955003008222|1\.0|-0\.14346434041144784|0\.1750606614880855|0\.10536399793532485|0\.12156555247067018|0\.1140249028571366|0\.10879345615278765|0\.09752016063019563|0\.08231598637746822|0\.023581180737114394|0\.01874877080832243|0\.013002400711998924|-0\.0004513453087491106|-0\.007566503046841711|-0\.009098954697455372|-0\.03745618391311648|
|MARRIAGE|-0\.029079425318771064|-0\.10813941027801287|-0\.03138884007085218|0\.0070095169916305445|-0\.14346434041144784|1\.0|-0\.41416991848813445|0\.019917190483426727|0\.02419906728119339|0\.03268767333723676|0\.03312154891405528|0\.03562917036655554|0\.034344765997445445|-0\.02347180191012958|-0\.021601779859030307|-0\.024909451022500993|-0\.023343846915375947|-0\.02539339799127468|-0\.02120682480007915|-0\.005978999780835323|
|AGE|0\.018677734490293255|0\.14471279755733674|-0\.0908736465273919|0\.0012839240637674137|0\.1750606614880855|-0\.41416991848813445|1\.0|-0\.03944737618411981|-0\.05014777620685522|-0\.05304843725816334|-0\.049721673995377226|-0\.05382597641308578|-0\.04877342642832421|0\.05623853326056659|0\.05428307435034244|0\.053709705178660236|0\.051353093243321435|0\.04934504811261178|0\.047612677990511255|0\.026146679056989194|
|PAY\_0|-0\.030574932272971513|-0\.2712143321347179|-0\.05764287886698678|-0\.10248713899221379|0\.10536399793532485|0\.019917190483426727|-0\.03944737618411981|1\.0|0\.6721643825483142|0\.5742450926204379|0\.5388406268712334|0\.5094260636654446|0\.4745530860641517|0\.18706843147380112|0\.18985910889354435|0\.17978528216681916|0\.1791247706258787|0\.18063462540120856|0\.1769802956414379|-0\.0792687111854195|
|PAY\_2|-0\.011214868262343643|-0\.29638210099648243|-0\.07077100316682232|-0\.08298645557341092|0\.12156555247067018|0\.02419906728119339|-0\.05014777620685522|0\.6721643825483142|1\.0|0\.7665516829341017|0\.6620671310239591|0\.6227802453768703|0\.5755008617793054|0\.23488652660358378|0\.23525694274352654|0\.22414585503162604|0\.22223651161283825|0\.22134837303342783|0\.2194033512866795|-0\.08070070981016696|
|PAY\_3|-0\.01849355375769933|-0\.2861229539031144|-0\.06609605640043047|-0\.07454738082082236|0\.1140249028571366|0\.03268767333723676|-0\.05304843725816334|0\.5742450926204379|0\.7665516829341017|1\.0|0\.7773588733012726|0\.6867745109947853|0\.6326835927184455|0\.20847288868976013|0\.23729453440292753|0\.2274943266955615|0\.22720228070078952|0\.22514519307202235|0\.2223267374363066|0\.0012948143319480216|
|PAY\_4|-0\.0027348897819592004|-0\.267460009639393|-0\.060173238366203696|-0\.07225921773723935|0\.10879345615278765|0\.03312154891405528|-0\.049721673995377226|0\.5388406268712334|0\.6620671310239591|0\.7773588733012726|1\.0|0\.8198353114868158|0\.7164494815807845|0\.20281206938744922|0\.2258163160680882|0\.24498313796206864|0\.2459172041984382|0\.24290205842488452|0\.2391541296058393|-0\.009362135754402232|
|PAY\_5|-0\.022199231870021336|-0\.2494113948241093|-0\.055063885035226384|-0\.0673156345068685|0\.09752016063019563|0\.03562917036655554|-0\.05382597641308578|0\.5094260636654446|0\.6227802453768703|0\.6867745109947853|0\.8198353114868158|1\.0|0\.8169001604176753|0\.2066839642440959|0\.22691326699152847|0\.24333468092023638|0\.271915006998107|0\.2697830901511351|0\.26250925166841726|-0\.006088757138842231|
|PAY\_6|-0\.020270134067212064|-0\.23519539948542492|-0\.044007788187657874|-0\.05493481654028164|0\.08231598637746822|0\.034344765997445445|-0\.04877342642832421|0\.4745530860641517|0\.5755008617793054|0\.6326835927184455|0\.7164494815807845|0\.8169001604176753|1\.0|0\.20737313129566123|0\.22692443093066755|0\.24118114604232158|0\.2663560690339078|0\.29089374494860704|0\.28509099069256866|-0\.0014962890433180716|
|BILL\_AMT1|0\.019388673917611145|0\.28542986496498995|-0\.03364186958914916|0\.004232183602562254|0\.023581180737114394|-0\.02347180191012958|0\.05623853326056659|0\.18706843147380112|0\.23488652660358378|0\.20847288868976013|0\.20281206938744922|0\.2066839642440959|0\.20737313129566123|1\.0|0\.9514836727518136|0\.8922785291271761|0\.8602721890293095|0\.8297786058330013|0\.8026501885528455|0\.14027727757532418|
|BILL\_AMT2|0\.017981897457701318|0\.27831436399776105|-0\.031183472229667317|0\.0024588210917865696|0\.01874877080832243|-0\.021601779859030307|0\.05428307435034244|0\.18985910889354435|0\.23525694274352654|0\.23729453440292753|0\.2258163160680882|0\.22691326699152847|0\.22692443093066755|0\.9514836727518136|1\.0|0\.9283262592714855|0\.8924822912577209|0\.859778307271445|0\.8315935591018213|0\.28036535701409987|
|BILL\_AMT3|0\.024354050018843155|0\.28323578358168416|-0\.024563311681403167|0\.0005427412255774552|0\.013002400711998924|-0\.024909451022500993|0\.053709705178660236|0\.17978528216681916|0\.22414585503162604|0\.2274943266955615|0\.24498313796206864|0\.24333468092023638|0\.24118114604232158|0\.8922785291271761|0\.9283262592714855|1\.0|0\.9239694565909823|0\.8839096973620155|0\.8533200905940468|0\.24433523760815992|
|BILL\_AMT4|0\.040350602942506635|0\.29398762371598486|-0\.02187967907348509|0\.00037565765065118885|-0\.0004513453087491106|-0\.023343846915375947|0\.051353093243321435|0\.1791247706258787|0\.22223651161283825|0\.22720228070078952|0\.2459172041984382|0\.271915006998107|0\.2663560690339078|0\.8602721890293095|0\.8924822912577209|0\.9239694565909823|1\.0|0\.9401344040880004|0\.9009409547978421|0\.23301185215343712|
|BILL\_AMT5|0\.01670530315635218|0\.29556233765823164|-0\.017005180187325976|0\.002096489670050675|-0\.007566503046841711|-0\.02539339799127468|0\.04934504811261178|0\.18063462540120856|0\.22134837303342783|0\.22514519307202235|0\.24290205842488452|0\.2697830901511351|0\.29089374494860704|0\.8297786058330013|0\.859778307271445|0\.8839096973620155|0\.9401344040880004|1\.0|0\.9461968070521957|0\.2170308237780502|
|BILL\_AMT6|0\.016729618316253813|0\.29038895064794745|-0\.016733126348159072|0\.0027561414727044244|-0\.009098954697455372|-0\.02120682480007915|0\.047612677990511255|0\.1769802956414379|0\.2194033512866795|0\.2223267374363066|0\.2391541296058393|0\.26250925166841726|0\.28509099069256866|0\.8026501885528455|0\.8315935591018213|0\.8533200905940468|0\.9009409547978421|0\.9461968070521957|1\.0|0\.199965006163385|
|PAY\_AMT1|0\.009742443464325092|0\.1952359152322094|-0\.00024245456294142142|0\.030069238440955968|-0\.03745618391311648|-0\.005978999780835323|0\.026146679056989194|-0\.0792687111854195|-0\.08070070981016696|0\.0012948143319480216|-0\.009362135754402232|-0\.006088757138842231|-0\.0014962890433180716|0\.14027727757532418|0\.28036535701409987|0\.24433523760815992|0\.23301185215343712|0\.2170308237780502|0\.199965006163385|1\.0|
|PAY\_AMT2|0\.008406120336439189|0\.17840795368370507|-0\.0013909096590868529|0\.012680871851513873|-0\.030038186562838978|-0\.008092702837779889|0\.021784893392614194|-0\.0701005211939387|-0\.05898999903461283|-0\.06679339566551329|-0\.001943656607903994|-0\.003191332307052815|-0\.005223268144054586|0\.0993550349727683|0\.10085087751752875|0\.3169359771796906|0\.20756372904207548|0\.1812464910522769|0\.1726629374180296|0\.2855755286868426|
|PAY\_AMT3|0\.03915053548888941|0\.21016674772338803|-0\.008596624911743908|0\.0218535515924394|-0\.039943140867107346|-0\.0035413519467573816|0\.029247353045011425|-0\.07056083767035479|-0\.055901231300968315|-0\.05331077958610196|-0\.0692352035676869|0\.009062362681555539|0\.005833774192896976|0\.15688713847568506|0\.1507181937016751|0\.1300111816244208|0\.3000225291116479|0\.25230486173062916|0\.23376979332693368|0\.2521911389524029|
|PAY\_AMT4|0\.007793129725698235|0\.20324241022458292|-0\.0022289715070058893|0\.026046606838673932|-0\.03821816611134147|-0\.01265927889271911|0\.021379005615589863|-0\.06400488888773119|-0\.04685841151354558|-0\.04606653388796151|-0\.04346142965539442|-0\.05829886530946838|0\.019017863282441618|0\.15830253328354005|0\.14739810422001154|0\.14340460499244426|0\.13019140778780797|0\.2931184631844312|0\.2502368249334362|0\.1995579311706798|
|PAY\_AMT5|0\.0006521877787619749|0\.21720243239549614|-0\.001667161800474087|0\.02214779222933898|-0\.040358454928196924|-0\.0012047569155652466|0\.02284997355855876|-0\.058189885949777295|-0\.037093079770128594|-0\.03586307056136118|-0\.033589534748121486|-0\.03333650421280087|-0\.04643364107299659|0\.16702571208291594|0\.1579574116239642|0\.17971235040649314|0\.16043303762900443|0\.1415741799596068|0\.3077288895011546|0\.14845927501534273|
|PAY\_AMT6|0\.0029997807225257667|0\.21959536860441753|-0\.002766022282891727|0\.02025934528026774|-0\.03719990308916937|-0\.006640941925653474|0\.0194781529698698|-0\.058673214376070426|-0\.03650037552721859|-0\.035861083718773175|-0\.026565087967650867|-0\.023027450987595774|-0\.025299338462285336|0\.17934112200688435|0\.17425616563434326|0\.18232596615205338|0\.1776369941867446|0\.16418445035361773|0\.11549416685164447|0\.1857352554457264|
|DELINQ\_NEXT|-0\.013951954838986251|-0\.1535198763935072|-0\.03996057770544172|-0\.30381063245236567|0\.028006077656250204|-0\.024339215683404438|0\.013889834301962887|0\.32479372847862237|0\.2635512016721678|0\.23525251372491712|0\.21661363684242388|0\.2041489138761645|0\.18686636165354611|-0\.019644197143221562|-0\.014193218088215756|-0\.014075518043214726|-0\.010156495880289674|-0\.006760463841014779|-0\.005372314914815558|-0\.07292948777785163|

• Plot histograms for all the columns in the data 

![image](https://user-images.githubusercontent.com/111556214/186588790-fe0ed26c-fb99-411d-9893-30ac99cce9b7.png)

# Training a decision tree model

● Partition the data into training, validation, and test sets

Training data: 15000 rows and 20 columns

Validation data: 7500 rows and 20 columns

Testing data: 7500 rows and 20 columns

● Train a decision tree model (without using demographic variables) (Up to 6 pts.):

○ Using validation-based early stopping and cross-validation (1 pt.) 

○ Display an iteration plot 

![image](https://user-images.githubusercontent.com/111556214/186597967-896b0156-d2c6-4f1c-a017-f644408d19f8.png)


○ Plot the decision tree 



○ Display the test error 




                       
# Quantitative Analysis

• Correlation Heatmap       


![image](https://user-images.githubusercontent.com/111556214/186575609-18b8e494-6bb5-48b7-9eef-2b818c1081cc.png)


    
