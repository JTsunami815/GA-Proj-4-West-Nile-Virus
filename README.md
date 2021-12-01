# GA Project 4 - West Nile Virus Prevention
___
___
## Authors
___
* Clara Gan
* Luka Chua
* Ronnette Chan
* Nixon Cheng
* Johnny Tseng
___
___
## Contents:
___
* [Executive Summary](#Executive-Summary)
* [Context & Background](#Context-&-Background)
* [Problem Statement](#Problem-Statement)
* [Resources](#Resources)
* [Data Dictionary](#Data-Dictionary)
* [Insights](#Insights)
* [Conclusion](#Conclusion)
* [Recommendation for the Future](#Recommendation-for-the-Future)
___
___
## Executive Summary
___

Our notebooks will consist of 3 main phases. The cleaning, the exploring and pre-processing, and the modeling, conclusions, and recommendations.  Each will do a particular job that will lead to the next stage of the process.  

The data cleaning process allowed us to do some basic modification as well as the filtration of the datasets provided.  The train, test, and spray CSV files did not require too much cleaning but we have found that the weather required the most attention.  In the weather CSV file, we address some duplicates as well as missing information.  By converting to the right data types and dropping the duplicates, the weather CSV file was able to merge with other CSV files for the EDA portion.

In the EDA process, we looked into the relationships of a few features that we believe have a correlation to each other.  Features like temperature, various mosquito species, blocks, and others to the West Nile Virus variation.  We also feature engineered a new column called, 'pesticides' where we believe it can provide us a better indication for the score results we will be looking for. After everything is done, we continued forward to the modeling phase.

In modeling, we brought forward our dataset from EDA and had it go through 10 different model studies to assist us in finding the best model outcome.  There was a problem that we were required to solve before we were able to proceed.  The West Nile Virus carrying mosquitoes was dwarfed by the others that were not carrying.  Knowing so, we had to make sure that our imbalanced data become balanced.  To do so, we went with SMOTE and ADASYN as well as stratified the 'y' variable to balance the data out. The reason for this was to make sure that we minimize false negatives and prevent false positives which would cause any lawsuit due to negligence.  Some had more parameters compared to others but all at the end helped us find our best precision and recall scores.  

After running all 10 different model studies, our best performing model was **Light Gradient Boost (SMOTE)** 

Here is a table of all the models that were done. (Not in any particular ranking)
![alt text](https://git.generalassemb.ly/jtsunami815/Project_4-West_Nile_Virus_Prevention/blob/master/media/model_comparison_table.png.png)
___
[Return to Contents](#Contents)
___
## Context & Background
___
We are a private environmental consulting firm that is looking to assist the city of Chicago to understand the pros and cons of the methods have been using as of now to reduce the mosquito population.  Especially the ones that are West Nile Virus carriers.  By providing them recommendations through evidence-based data and models, it will hopefully keep the citizens safe from future breakouts like back in 2007.

The West Nile virus (WNV) is most commonly spread to people by the bite of an infected mosquito, mostly the species of Culex. This generally occurs during summer and fall, with a peak period for disease transmissions from mid-August to mid-October. Only a little less than 20 percent of those infected with the virus will develop West Nile fever with mild symptoms of fever, headache, body aches, a skin rash on the chest or back, and swollen lymph glands. While most people with milder symptoms recover completely, the fatigue and weakness can last for weeks or months. [(Source)](https://www.cdc.gov/westnile/index.html) However, one in 150 people infected will develop a severe infection in the form of encephalitis (inflammation of the brain) or meningitis (inflammation of the membranes that surround the brain and spinal cord), which can potentially lead to complications such as partial paralysis, impaired judgment, seizures, and memory loss. [(Source)](https://www.ninds.nih.gov/Disorders/Patient-Caregiver-Education/Fact-Sheets/Meningitis-and-Encephalitis-Fact-Sheet)

As there are no vaccines to prevent the onset of the virus or medications to treat WNV in people, the best course of action is to target the transmission vectors of the disease, the mosquitoes. According to the [Association for Professionals in Infection Control and Epidemiology](https://apic.org/monthly_alerts/mosquitoes-west-nile-virus-and-you/), the six strategies to avoid mosquito bites are:

Apply insect repellent containing DEET before going outdoors
Be aware that the early morning and evening hours are peak mosquito hours and try to avoid outdoor activities during these times
wear long sleeves, long pants, and socks when spending time outdoors if possible, especially during peak mosquito hours. Spray clothes with repellent containing permethrin or DEET as mosquitoes can bite through thin clothing
Reduce the number of mosquitoes on an individual property by eliminating or reducing standing pools of water where mosquitoes lay their eggs.
Reduce the number of mosquitoes inside the house by patching, repairing, or replacing screens with holes or screens that don’t fit tightly to the door or window frame. Install and close screen doors if the outside doors are propped open.
Report dead birds to the local health department as birds can be infected with the WNV and pass it on to mosquitoes or other birds
The City of Chicago is the most populous city in the U.S. state of Illinois and the third most populous city in the United States. The city lies within the typical hot-summer humid continental climate and experiences four distinct seasons with frequent heat waves during summer. [(Source)](https://www.weather.gov/) When large numbers of nuisance or infected mosquitoes are found or when people in a large area are getting sick, airplanes and helicopters can treat very large areas with insecticides in a process known as aerial spraying. [(Source)](https://www.chicago.gov/city/en/depts/cdph/provdrs/healthy_communities/news/2020/august/city-to-spray-insecticide-thursday-to-kill-mosquitoes.html)
___
[Return to Contents](#Contents)
___
## Problem Statement
___
The West Nile virus (WNV) is the leading cause of mosquito-borne diseases in the continental United States. While only less than a fifth of those infected with the virus will develop mild symptoms, one in 150 people infected will develop severe infections in the form of encephalitis or meningitis. Intervention measures in the form of aerial spraying have been deployed to contain the spread of the virus in affected areas within the city of Chicago. As part of the Disease And Treatment Agency, division of Societal Cures In Epidemiology and New Creative Engineering (DATA-SCIENCE) team, we have been tasked to determine the environmental factors affecting the transmission of the WNV, as well as to improve the city's intervention efforts against the main vectors of the virus, the mosquitoes. Specifically, to control the spread of the virus, we are looking to predict the presence of WNV, plan and schedule the pesticide spraying in preparation for the transmission season, and minimise spending on the pesticides while maintaining the effectiveness of the intervention program.
___
[Return to Contents](#Contents)
___
## Resources
___
**Data:**
* [Train CSV]
* [Test CSV]
* [Weather CSV]
* [Spray CSV]

**3rd Party**
- [CDC - West Nile virus](https://www.cdc.gov/westnile/index.html)
- [COVID-19](https://www.ninds.nih.gov/Disorders/Patient-Caregiver-Education/Fact-Sheets/Meningitis-and-Encephalitis-Fact-Sheet)
- [Mosquitoes, West Nile Virus, and you](https://apic.org/monthly_alerts/mosquitoes-west-nile-virus-and-you/)
- [National Weather Service](https://www.weather.gov/)
- [Chicago](https://www.chicago.gov/city/en/depts/cdph/provdrs/healthy_communities/news/2020/august/city-to-spray-insecticide-thursday-to-kill-mosquitoes.html)
___
[Return to Contents](#Contents)
___
## Data Dictionary
___
### Dictionary Key:
___

   |Feature|Type|Dataset|Description|
|- | -|- | -|
|**species**|object|combined|Species of mosquito|
|**block**|float64|combined|Block number of address|
|**street**|object|combined|Street name|
|**trap**|object|combined|Id of the trap|
|**latitude**|float64|combined|Latitude|
|**longitude**|float64|combined|Longitude|
|**addressaccuracy**|float64|combined|Number of mosquitoes caught in this trap|
|**nummosquitos**|float64|combined|Need to Fill|
|**wnvpresent**|float64|combined|whether West Nile Virus was present in these mosquitos|
|**tavg**|float64|combined|Average Temperature|
|**dewpoint**|float64|combined|Average Dew Point|
|**wetbulb**|float64|combined|Average Wet Bulb|
|**preciptotal**|float64|combined|Precipitation in inches|
|**stnpressure**|float64|combined|Average Station Pressure|
|**sealevel**|float64|combined|Sea level|
|**resultspeed**|float64|combined|Resultant wind speed|
|**resultdir**|float64|combined|Resultant direction|
|**avgspeed**|float64|combined|Average wind speed|
|**year**|int64|combined|Year the WNV test was performed|
|**month**|int64|combined|Month the WNV test was performed|
|**day**|int64|combined|Day the WNV test was performed|
|**pesticide**|category|combined|Presence of Presticide|
___
[Return to Contents](#Contents)
___
## Insights
___
The recent epidemic of the West Nile Virus in Chicago has been troubling the Department of Public Health. Though it may be impossible to fully eliminate the West Nile Virus, our goal is to curb the West Nile Virus and keep it at a controllable level for the Department of Public Health to manage. Since we know that that the West Nile Virus and the pesticides go hand in hand in keeping the West Nile Virus under control, our objective is to find the optimal level of pesticides that is to be sprayed across Chicago, while minimising the negative consequences from the utilization of the pesticides - since pesticides are a double-edged sword in the fight against the West Nile Virus.

**Costs**

There are varying costs due to the deployment of pesticides. We will look into the 3 kinds of the cost incurred: direct cost, indirect cost, and intangible cost (if applicable). 

1. Direct Cost
The obvious direct cost from the deployment of pesticides is that it is expensive.
Chicago engages in Integrated Vector Management (IVM) programs that make evidence-based control decisions with information derived from well-designed surveillance systems, and that utilize a diversity of ecologically-appropriate control tools, can effectively reduce vector abundance and human West Nile Virus risk [(Source)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7092639/). Hence, with such a targeted approach, pesticides are not mindlessly sprayed across Chicago, and the expenditure on the pesticides is optimally reduced as well. In 2020, Chicago sprayed on South Lawndale, Brighton Park, Archer Heights and on the 41st Ward of Chicago [(Source)](https://www.chicago.gov/city/en/depts/cdph/provdrs/healthy_communities/news/2020/august/city-to-spray-insecticide-thursday-to-kill-mosquitoes0.html). The total sprayed area is 11.4 km² + 7.045 km² +  5.206 km² + 45.014 km² = 68.665 km². Since the cost of deploying aerial spraying of common mosquito pesticides cost **USD 0.92** for half an acre, the total cost of aerial spraying on the targeted areas of Chicago would alone cost **USD 31,898.88**. Though this would kill mosquito larvae and adult mosquitoes [(Source)](https://www.cdc.gov/mosquitoes/mosquito-control/community/aerial-spraying.html), we can expect regular aerial spraying to be conducted across Chicago during the summer months and breeding season to fully keep the West Nile Virus under control. Assuming that the maximum number of sprays of 25 are conducted across Chicago on a yearly basis [(Source)](https://www.mercercounty.org/home/showdocument?id=2626#:~:text=Do%20not%20spray%20more%20than,applications%20per%20site%20per%20year.), this would cost **USD 797,472.08** for the Department of Public Health and relevant government disease control centres on the spraying of pesticides alone. This does not include the labour cost, transportation cost and others. 

2. Indirect Cost
A possible indirect cost could be the higher tax rates imposed on the residents of Chicago. The costs of the deployment of pesticides from the hired & paid workers for the spraying of the pesticides by pest control agencies, to the purchase of large quantities of pesticides, all these varying costs incurred from the deployment of the pesticides will eventually be a shared cost borne by both the state Illinois, Chicago city, and the residents of Chicago. This eventual increase in higher taxes may be a huge financial burden for the residents of Chicago who are of the lower-income category. 

3. Intangible Cost
Notwithstanding the above, the increased taxes could lead to intangible costs such as a lower quality of life due to a higher cost of living. The slightest increase in the percentage of tax could lead to a significantly lower quality of life - especially for those in the lower-income category where every dollar counts. Even for the middle-income earners, an increase in tax could imply that one has to live more cautiously and may sacrifice non-essential expenditure like entertainment expenditure for example. 

**Benefits**

Likewise, for benefits, there are varying benefits due to the deployment of pesticides. We will look into the 4 kinds of benefits incurred: direct benefit, indirect benefit, intangible benefit, and competitive benefit (if applicable).

1. Direct Benefit
The biggest direct benefit of the use of pesticides is the decrease in people contacting the West Nile Virus. From our model analysis, the model Light Gradient Boost with a SMOTE resampler is the best performing model. This will result in a drop in the probability of the unemployed residents in Chicago due to the being patients who contracted the West Nile Virus, or as caregivers of this patients. Having a steady and higher employment rate in Chicago 

2. Indirect Benefit
Additionally, the indirect benefit from the use of pesticides to curb the West Nile Virus is the potential decrease in medical costs incurred due to the West Nile Virus. Since there is no vaccine for the West Nile Virus or medication to treat patients with the West Nile Virus [(Source)](https://www.cdc.gov/westnile/index.html#:~:text=There%20are%20no%20vaccines%20to,a%20fever%20and%20other%20symptoms.), the symptoms can only be treated. For serious cases though, patients may need to be hospitalized and as such, huge hospitalization medical expenses may be incurred. Hence, the use of pesticides would significantly decrease the probability of medical expenditure due to contracting the West Nile Virus.
In 2020, the state Illinois (which Chicago is a city of) had a total of 42 patients who contracted the West Nile Virus, of which 4 patients had passed away from the virus [(Source)](https://public.dph.illinois.gov/wnvpublic/wnvglance.aspx?year=2021). Taking previous data that provided a breakdown of cost per patient in Sacramento, CA from [(Source)](https://wwwnc.cdc.gov/eid/article/16/3/09-0667_article) and use it for Chicago, this is what it would cost to be a patient with West Nile Virus Neuroinvasive Disease (WNND) [(Source)] (https://pubmed.ncbi.nlm.nih.gov/16983682/):

**BASELINE**
* Outpatient cost (For all treatments) = ~USD 6,317.00
* Inpatient cost (For all treatments)=  ~USD 33,143.00
* Patient in nursing home (For all treatments) = ~USD 18,097.00
* Productivity loss (Assuming the patient is still working and below 60 years old) = ~USD 10,800.00
* Productivity loss (Assuming the patient is still working and above 60 years old) = ~USD 7,500.00

42 patients will have an equivalent of around **USD 265,000.00** if assuming all patients are outpatients or **USD 1,845,606.00** if assuming all patients are inpatients and are below 60 years old.
***(NOTE: These costs are based on Sacromento, CA cost of living so will have to scale it by 1.07 for Chicago, IL)***

3. Intangible Benefit
Intangible benefits such as improved morale and increased living satisfaction for the residents of Chicago during the summer months & West Nile Virus Season as the residents can live with greater assurance and relatively lower levels of fear of contracting the West Nile Virus. 

4. Competitive Benefit
The regular use of pesticides can give the city of Chicago a competitive edge over other cities. Chicago can stand out from her neighbouring cities and even promote herself as a choice destination for a safe summer vacation with a reduced risk of contracting the West Nile Virus. 

**Conclusion**

Comparing the costs and benefits, though it is expensive to use pesticides in the fight against the West Nile Virus, the savings and benefits that the use of pesticides bring is more than sufficient for the government to continue spending on pesticides. But more than that, we cannot put a pricetag on human lives. To ensure the safety of citizens of Chicago as well a well-being of its neighboring cities from a viral pandamic like what we are experiencing right now with COVID-19 [(Source)](https://www.chicago.gov/city/en/sites/covid-19/home/covid-dashboard.html), the benefits of preventing an add-on factor on top of an ongoing pandemic will definitely outweight the cost.
___
[Return to Contents](#Contents)
___
## Conclusion
___
Our analysis provides a foundation for the implementation of a statistically rigorous system for real-time forecast of seasonal WNV outbreaks and their use as a quantitative decision support tool for public health officials and mosquito control programs. We found that () () () are among the top determinants of the presence of WNV in Chicago base on the Light Gradient Boosting classifier model with a (some %?). We have presented a cross-benefit analysis of deploying pesticides to combat the WNV, concluding that the benefits would outweigh the costs of deployment. We also discussed future directions with regards to climate change and public awareness to improve Chicago's intervention programme for WNV.
___
[Return to Contents](#Contents)
___
## Recommendation for the Future
___
**Focus on Education**

The government officials and the disease control centres can heavily invest resources in curbing the spread of the West Nile Virus during the summer months, which are the peak of the breeding season and spread of the virus. However, such efforts can come to a naught if the residents of Chicago do not work hand in hand with the government officials and the disease control centres. All the aerial spraying of the pesticides and the surveillance of the mosquitos will go to waste, if the residents themselves do not do their part to reduce the breeding sites of mosquitos. For example, students can be educated from a young age in schools to remove any stagnant water like the excess water on flower plates, improve drainage & remove debris on roofs and canals, and by turning water pails upside down. 

**Seek less invasive solutions against the West Nile Virus**

We cannot deny that the use of pesticides, albeit an effective & necessary one, is an aggresive solution in reducing the spread of West Nile Virus. 

The problem statement has presented itself as more of an ecology problem given that the main target we are dealing with is the mosquitoes. However, the most important problem which Chicago are most likely to be interested in is the healthcare-associated costs that come from this problem since West Nile Virus has the potential to cause severe forms of diseases, such as encephalitis and meningitis, that can lead to paralysis, long term disability and coma. As such, cost-effectiveness analysis can be conducted using healthcare costs (in terms of US dollars) and quality-adjusted life years (QALY) as an indicator of effectiveness. A decision tree / markov model for economic evaluation can be drawn using the above parameters (cost and effectiveness) to calculate the incremental cost-effectiveness ratio (ICER) which can then be used to evaluate the interventions given a certain budget. This analysis takes into account which intervention is being used (in our case the intervention would be the pesticide and the control will be not using pesticide), what forms of diseases can develop in each arm, and its associated probability. At the end of the decision tree / markov model, the cost and effectiveness will be computed, combined and compared to return the ICER value. However, as of now, there is no available QALY data for West Nile Virus. Therefore, we recommend that research should be conducted to obtain these data when the intervention is being deployed so that a more robust cost-effectiveness analysis to be conducted to evaluate the use of pesticides. 

**Referenced URLs:**
https://www.hopkinsmedicine.org/health/conditions-and-diseases/west-nile-virus#:~:text=Humans%20get%20West%20Nile%20from,to%20prevent%20West%20Nile%20virus.

Changing trends in global climates have affected patterns of infectious disease transmission. Changes in weather such as increased rainfall, extreme weather events, such as flooding, and more violent heat waves have impacted patterns of insect activity and have also created environments that better suit the transmission of viruses. For example, warmer temperatures can result in a longer season yearly for mosquitoes to be active transmission vectors of WNV as they migrate within one territory or between territories, potentially increasing the spread of if WNV. The WNV, first reported in Uganda in 1937, is an example of mosquito-borne viruses emerging in continents that they had never previously reached in the past 20 years. Hence, more environment-based data could be collected to conduct multi-year investigations of the complex relationship between climate change and WNV transmission for the city to adopt a multi-faceted approach for mosquito control. Other areas of improvement include investigating the development of resistance to pesticides in the mosquito populations and increasing the involvement of the public in combating and preventing a WNV outbreak.
___
[Return to Contents](#Contents)
___
