
**Problem Statement**

You are a data analyst for the Austin Police Department (APD), responsible for examining over 1.76 million 911 calls to improve response times, identify critical incidents, assess mental health impacts, and report on the effectiveness of resource allocation. Your task is to use SQL queries to analyze trends, performance metrics, and safety issues, helping to enhance both officer and community safety.

1.**Improving Response Times**
Problem: The department wants to understand the factors that affect response times. You are tasked with identifying patterns where response times are high and suggesting changes to reduce these times.

2.**Identifying Mental Health-Related Incidents**
Problem: The city council is concerned about mental health-related incidents and wants a report detailing how often these incidents occur, their outcomes, and any patterns.

3.**Assessing Resource Allocation and Unit Efficiency**
Problem: The APD needs to optimize the number of units dispatched to incidents, ensuring enough officers are present without over-allocating resources.

4.**Analyzing Incidents by Day of Week and Hour**
Problem: The department wants to understand peak times for different types of incidents to adjust patrol schedules accordingly.

5.**Monitoring High-Priority Incidents**
Problem: High-priority incidents (priority level 0 or 1) need special attention to ensure that they are being handled efficiently. The APD wants a report showing these incidents, their outcomes, and any injuries sustained by officers or civilians.

6.**Geospatial Analysis of Incident Locations**
Problem: The APD wants to understand how incidents are distributed across different council districts and census block groups to better allocate resources.

**Additional Case Studies**:

•	**Incident outcome analysis**, exploring how different types of incidents (initial vs. final problem descriptions) are resolved.

•	**Officer workload analysis**, examining which officers or sectors handle the most incidents or experience the longest time on scene.

**Deliverables**:

•	Design and develop an interactive, real-time dashboard to help the police gain insights and monitor key metrics from the 911 calls. The dashboard should allow police chiefs and department heads to access the latest data and analyze trends for efficient decision-making.
•	Prepare a professional presentation for police chiefs, summarizing key findings and actionable insights derived from the analysis.
Tools:
Any tool aside Excel that can handle large amounts of Data:

Underwent cleaning and preprocessing of data with PYTHON  using the Pandas library Dataframe

**Deadline**:
•	10 days from the start date.

**Success Criteria**:
1.	Effective Real-Time Monitoring : DONE
2.	Improved Operational Efficiency : DONE
3.	Data-Driven Decision Making : DONE
4.	Comprehensive and Actionable Presentation :DONE
5.	User-Friendly and Scalable Dashboard : DONE
6.	Stakeholder Satisfaction : DONE


**Key Questions**
•	**WHAT IS THE TOTAL NUMBER OF INCIDENTS THAT OCCURED IN EACH SECTOR?**

**ANSWER**:
Calculate the total no of incidents first then use it together inside a chart or table 
To help us understand the number of incidents for each sector 
Use a table with Both incident and sector column

             Dax Measures: Total incident = COUNTROWS('df') Total Number of Incidents given as: 952,802

**Total No. Of Incidents by sector**
![Screenshot (299)](https://github.com/user-attachments/assets/10ccccc5-78da-48df-a7c9-a90627ff6420)

•	**WHAT ARE THE TOP 5 BUSIEST GEOGRAPHIC AREAS IN TERMS OF 911 CALLS, AND WHAT IS THE AVERAGE RESPONSE TIME FOR EACH OF THESE AREAS ?**

         ANSWER:
              Funnel KPI bringing together the Geo ID and the total incidents 

**Total Incident By GeoID**
![Screenshot (323)](https://github.com/user-attachments/assets/e8378c1a-c09e-4c83-9d74-503955cf9174)

•**IDENTIFY SECTORS WHERE MENTAL HEALTH-RELATED INCIDENTS MAKE UP MORE THAN 30% OF THE TOTAL INCIDENTS.**
         
          ANSWER: On further Analysis there is no one is greater Greater than 30% as on further filtering down nothing appeared
   **Mental Health % by sector**       
 ![Screenshot (300)](https://github.com/user-attachments/assets/fe162622-c49f-45ad-84c4-5fe9f9cd3aca)

•**WHAT ARE THE BUSIEST DAYS OF THE WEEK, AND HOW DO THE TYPE OF INCIDENTS DIFFER ACROSS THOSE DAYS?**

         ANSWER: Only one incident type and as such there is no difference or disparity , incident Number will be used instead  plotted against response day

**Busiest Day of the week by No of Incidents**
 ![Screenshot (301)](https://github.com/user-attachments/assets/7ee71ec9-3085-4a4d-ac04-e28dbaab062c)       

•**WHAT IS THE AVERAGE RESPONSE TIME FOR ALL INCIDENTS INVOLVING MENTAL HEALTH ISSUES ?**

      ANSWER: The average was calculated to be 44.29secs which was calculated with the following 
       Dax: AverageResponseTimeMH = CALCULATE(AVERAGE(df[Response Datetime]),df[Mental Health Flag] = "Mental Health Incident")

    


•**WHICH TYPES OF INCIDENTS HAVE RESPONSE TIMES THAT ARE ABOVE THE OVERALL AVERAGE RESPONSE TIME?**

       ANSWER: On further analysis through using the only one given incident type which is (Dispatched incident) and addition of incident numbers to give further clearance of every single dispatched incident it was found that all the types of incidents  posses response times that are greater than the earlier calculated response time(45,565k) While being compared to the other average response time which was (44,929k)

**Average Total Response Time by incident Type**
 ![Screenshot (302)](https://github.com/user-attachments/assets/a17a0a4c-dc82-43a8-950c-5e1cc93ef19f)

•	**FIND THE GEOGRAPHIC AREAS WHERE THE AVERAGE NUMBER OF UNITS DISPATCHED IS GREATER THAN THE AVERAGE NUMBER OF UNITS DISPATCHED ACROSS ALL AREAS.**

     ANSWER: The Geographic area’s  have the same average of units being dispatched towards their Area’s: (1.93) as the overall averageof units being dispatched which is (1.93) on viewing on the table.

  **Overall Average Units Dispatched**
  ![Screenshot (303)](https://github.com/user-attachments/assets/62d19501-6ca8-4388-8cda-317d756df1a5)

•**WHICH SECTORS HAVE THE HIGHEST PERCENTAGE OF RECLASSIFIED CALLS (WHERE THE FINAL PROBLEM DESCRIPTION DIFFERS FROM THE INITIAL ONE)?**

         ANSWER:The other row possess the highest number/percentage of reclassified calls ,Calculated through the following steps or measures: First creating another column (RECLASSIFICATION INDICATOR COLUMN) Which compares both the initial problem description and final problem description in order to create a column that shows differences between what was initially described and the final description in each of the individual entries  Done by the following

         Dax function:  ReclassifiedFlag = 
    IF('df'[Initial Problem Description] <> 'df'[Final Problem Description], 1, 0) 

    If theres a difference theres a 1 
    And if there wasn’t any difference theres a 0
    
    Then weve already calculated the total number of incidents (MEASURE) 
    Then calculate all the total reclassified calls with the DAX
    
    TotalReclassifiedCalls = 
    CALCULATE(
        SUM('df'[ReclassifiedFlag]),
        ALLEXCEPT('df', 'df'[Sector])
    )
    
    Then calculate the percentage of the TotalReclassifiedcalls: 
    ReclassificationPercentage = 
    DIVIDE([TotalReclassifiedCalls], [Total incident], 0)
    On seeing the visualisation it was found out that the Other Sector had the highest number of reclassified calls percentage being 1.00 compared to the other sectors.

**Reclassification calls percentage by sector**
![Screenshot (304)](https://github.com/user-attachments/assets/ede6ba10-3828-493e-8ebb-f7ca1e433d71)    

•	**WHAT IS THE CUMMULATIVE NUMBER OF CALLS THROUGHOUT EACH DAY , AND HOW DOES THIS CUMMULATIVE TOTAL CHANGE BY SECTOR?**

      ANSWER : Now lets handle this firstly  to do this I  have to create a column to aggregate all the calls  by day , I used the response datetime to do this : 
      DAX MEASURE : 
      CallDate = 
      DATE(YEAR('df'[Response Datetime]), MONTH('df'[Response Datetime]), DAY('df'[Response Datetime]))
      
      Thereby after I had to create a measure that calculates the total number of calls from before all the way  down to today , creating the measure;
              CumulativeCalls = 
    CALCULATE(
        COUNT('df'[Incident Number]),
        FILTER(
            ALL('df'[CallDate]),
            'df'[CallDate] <= MAX('df'[CallDate])
        )
    ) 
    
    Now to finally end it I  have to measure the changes in the calls by sector so I calculate the measure :
    
    CumulativeCallsBySector = 
    CALCULATE(
        [CumulativeCalls],
        ALLEXCEPT('df', 'df'[Sector], 'df'[CallDate])
    )
    Then illustrate the visualisation and we see the cumulative total calls by sector yearly being: 
    Adam: 110,002
    Airport: 16,489
    Baker: 101,156
    Charlie: 105,073
    David: 125,807
    Edward: 137,978
    Frank: 113,261
    George: 52,699
    Henry: 94,855
    Ida: 95,481
    Other: 1
**Cummulative Calls By Sector by Day and Sector**
![Screenshot (306)](https://github.com/user-attachments/assets/09500272-b056-4de2-8737-8da885021ffd)
       
•	**FOR EACH SECTOR, RANK THE GEOGRAPHIC AREAS BY TOTAL NUMBER of 911 CALLS AND SHOW THE RESPONSE TIME FOR EACH AREA.**

       ANSWER:
         First we had to calculate the total number of 911 calls which would be gotten from the incident numbers ; 
    TotalCallsPerArea = COUNT(df[Incident Number])

    Then we calculate the average response time for each area by the sector; 
    AvgResponseTimePerArea = AVERAGE(df[Response Time])
    With the highest being the 137978 Edward and the   lowest being  Airport (16,489)

**Total Calls Per Area By GeoID And Sector**
![Screenshot (307)](https://github.com/user-attachments/assets/50b9bf87-aa5d-4840-b88b-e6b54d6c269c)

•**WHAT ARE THE MOST COMMON TYPES OF INCIDENTS THAT OCCUR BETWEEN 10 PM and 6 AM?**

    ANSWER:
    Trick question , theres only one incident type so no matter what I calculate na the same incident type go dey 10 PM and 6 AM(Dispatched Incident)

•**WHAT PERCENTAGE OF INCIDENTS REQUIRED MORE THAN 3 UNITS TO BE DISPATCHED?**

    ANSWER:
    To achieve this firstly we have to calculate the number of incidents that surpassed 3 units being sent there so I used the calculate dax function to count the incidents going through them and give me the ones that have units arrived greater than 3

    IncidentsMoreThan3Units = 
    CALCULATE(
        COUNT('df'[Incident Number]),
        'df'[Number of Units Arrived] > 3
    )

    Next I had a descision to make, I could choose , I firstly decided to use the percentage format in the tab onto the more than three incidents measure I calculated but it didn’t really narrow down the percentage to how I would like it giving me (7246k% ) which wasn’t too good for my liking  I decided to create a percentage measure using the following dax formula with the total incidents:

    PercentageMoreThan3Units = 
    DIVIDE([IncidentsMoreThan3Units], [Total incident], 0) * 100

    And then getting the final percentage answer as (7.62%)

**Percent Of Incidents That Require More than 3 units**
![Screenshot (308)](https://github.com/user-attachments/assets/5a0db8b9-beb2-4a6a-8601-d8e64405c27a)

•**HOW DO RESPONSE TIMES COMPARE ACROSS DIFFERENT PRIORITIES FOR EACH TYPE OF INCIDENT?**

       ANSWER:
    To do this I utilised through visualisation the  response times and how they compare or have compared over time with respect to the  incident types and the priority levels and found out interesting insights, I will be representing priority level with (p and then the number i.e p0, p1,p2,p3) like for instance the range of priority  with respect to the number of incidents were as follows with  2021;  having p0 = 20,603 incidents , p1 = 32550 incidents , p2 = 79,133 incidents , p3 = 25904 incidents.
    2022; having  p0 = 36227 incidents , p1 = 55,184 incidents , p2 = 147872 incidents , p3 = 53,039 incidents. 
    2023; having p0 = 35,051 incidents , p1 = 51270 incidents , p2 = 145242 incidents ,  p3 = 54577 incidents.
    2024; having p0 = 28905 incidents , p1 = 38629 incidents , p2 = 107328 incidents , p3 = 41288 incidents .

**Response Time Comparison Across Different Priorities**
![Screenshot (309)](https://github.com/user-attachments/assets/d40128cc-d4b6-43d7-9587-776cc3d31858)

•**WHICH GEOGRAPHIC AREAS HAVE THE HIGHEST NUMBER OF INCIDENTS INVOLVING OFFICER INJURIES OR FATAILITIES ?**

       ANSWER:
    I Created a measure that  counts the officer incident kill/injury counts that are greater than 0 that is 1 , since they were represented by if there was no inury(0) and if there was injury(1) :

    OfficerInjuryIncidents = 
    CALCULATE(
        COUNT('df'[Incident Number]),
        'df'[Officer Injured/Killed Count] > 0
    )
    Then visualising with the GeoID , It was found out there was only 1 Geographic area having the incident count of an officer either being killed or injured  

**Officer Injury Incidents By GeoID**
![Screenshot (310)](https://github.com/user-attachments/assets/2a42179f-69f5-4594-aa60-dce4322ad8e1)

•**WHICH COUNCIL DISTRICTS HAVE THE HIGHEST AVEREAGE RESPONSE TIMES?**

       ANSWER:
    On calculation of the average response time in total  with the following Dax formula:
    AverageResponseTime in Total = CALCULATE(AVERAGE(df[Response Datetime]))
    A total answer of (44.96k) was gotten as the average response time this was then used in stacked column chart with the council district to visualise that in general all council districts have or are in the range of the common average response time

**Average Response Time In Total By Council District**
![Screenshot (312)](https://github.com/user-attachments/assets/cb805dfb-73a0-4166-8965-0d133eeb7359)

•**HOW MANY INCIDENTS INVOLVE SERIOUS INJURY OR DEATH (EITHER OFFICERS OR SUBJECTS) RELATED TO MENTAL HEALTH?**

    ANSWER:
    To calculate this I had to create a dax new measure to try and get both columns containing the officers and subjects that were injured  and factor that in with the mental health flag column to make sure that only the “Mental Health Incidents ” were selected :
    
    SeriousInjuryMentalHealthIncidentsO&S = 
    CALCULATE(
        COUNT('df'[Incident Number]),
        'df'[Mental Health Flag] = "Mental Health     Incident", 
        OR(
            'df'[Officer Injured/Killed Count] > 0,
            'df'[Subject Injured/Killed Count] > 0
        )
    )
    Then with the new measure being visualised with a card the figure stood at only (4) incidents

**Serious Injury Mental Health Incidents Involving Either Officer Or Subjects**

![Screenshot (313)](https://github.com/user-attachments/assets/86590d46-1c7c-4c3a-9041-f3c7b3c95373)

•**FIND THE AVERAGE RESPONSE TIME FOR EACH INCIDENT TYPE AND COMPARE IT WITH THE OVERALL AVERAGE RESPONSE TIME.**

       ANSWER:
    Calculate the average response time first using the following dax formula:

    AverageResponseTime in Total = CALCULATE(AVERAGE(df[Response Datetime]))

    And then you calculate the average with the incident type , I used a dax formula that pertained to selecting a “Specific Incident Type” and since there was only one Incident type: DISPATCHED INCIDENT 
    It made it easier:

    AverageResponseTime IT = 
    CALCULATE(
        AVERAGE(df[Response Datetime]),
        df[Incident Type] = "Dispatched Incident"
    )

    On the matter of their correlation I found out that the Comparison between the two are by and large the same with the average response time being (44,962.83) and the average response time in respect to the incident type being (44,962.83)as well.

**Comparison between Average Response Time in Total and Average Respose Time By Incident Type**
![Screenshot (324)](https://github.com/user-attachments/assets/1bc63422-5823-42f8-b802-0c441dfdaeba)

•**FOR EACH DAY OF THE WEEK, CALCULATE THE DIFFERENCE BETWEEN THE AVERAGE RESPONSE TIME FOR THAT DAY AND THE AVERAGE RESPONSE TIME FOR ALL DAYS COMBINED.**

       ANSWER:
    There was no difference Found

•**WHAT ARE THE TOP 3 MOST FREQUENT FINAL PROBLEM DESCRIPTIONS?**

     ANSWER:
    The three most frequent final problem descriptions are: Trespass Urgent, Disturbance Other, Suspicious Persons, which I got by first creating the average response time by day measure:

         AvgResponseTimeByDay = CALCULATE(AVERAGE(df[Response Datetime]), ALLEXCEPT(df, df[Response Day of Week]))

    And then creating a measure to calculate the difference between the averageresponseTimebyDay and the overall averageresponsetime:

    ResponseTimeDifference = [AvgResponseTimeByDay] - [AverageResponseTime in Total]

    Then visualsing the final problem description with the final problem description count

    FinalProblemDescriptionCount = COUNT(df[Final Problem Description])

**Final Problem Description Count**
![Screenshot (314)](https://github.com/user-attachments/assets/1d398ab6-b41f-4a89-8af3-5086372378f7)

•**WHAT ARE THE BUSIEST TIMES OF THE DAY, AND HOW DO INCIDENT TYPES VARY BY TIME?**

       ANSWER:
    To solve this I  first had to look at the total number of incidents calculated , then I had to create a column as hour of the day to use to figure out for different hours of the day ranging(1-24)i.e 24 hrs  in a day for each hr the total incidents per that particular time
    So the following dax formula was created;

    HourOfDay = HOUR(df[Response Datetime])
    Then using this for illustration along side the total No. of incidents and incident Type was able to give a visualisation showing the varying incident cases per time of days with the 17th hour of days being the most busy and judging by my discretion; this would be by around (4pm) with incidents at this time totalling up to: (51920) with hour 5 being the time with the lowest value of incidents (19731)


**Total Incident by Hour Of Day and Incident Type**
![Screenshot (315)](https://github.com/user-attachments/assets/409486d7-4e47-4e7e-b908-5176e824e033)

•**WHAT IS THE TOTAL NUMBER OF MENTAL HEALTH RELATED INCIDENTS, AND HOW HAS THIS CHANGED OVER TIME?**

      ANSWER:
    Using the Already calculated mental health incident count , with the response datetime 
    I’m able to visualise the trend of mental health incidents overtime 
    Using this visualisation we can see that there has been a yearly decline in the amount of mental health related incidents with movement steadily going from (24,493) as at 2021 then the sudden spike upwards to as  high as  (39,848) MH incidents in 2022 , then a movement to (33867) in 2023 , then a very big drop in incidents 2024 (24708).

**Mental Health Incident Count by Year, Month And Day**
![Screenshot (316)](https://github.com/user-attachments/assets/a0fa8032-c138-44e5-a00a-5af0df3cccaf)

•	**WHAT IS THE AVERAGE TIME SPENT ON SCENE BY UNITS ACROSS DIFFERENT TYPE OF INCIDENTS?**

       ANSWER:
    Firstly I calculate the average time spent by units on the scene by incident type; 
    AvgTimeOnSceneByIncidentType = 
    CALCULATE(AVERAGE(df[Unit Time on Scene]), ALLEXCEPT(df, df[Incident Type]))

    Then I use the measure calculated with the incident type to visualise and since there’s only one incident type , its preety easy to calculate that the average time spent on scene by incident type is (6090.75)

**Average Time Spent On Scene Across Different Types Of Incidents**
![Screenshot (317)](https://github.com/user-attachments/assets/b45c2842-f4d3-4b6a-a36e-b88f139f511c) 

•**WHAT IS THE DISTRIBUTION OF RESPONSE TIMES ACROSS THE SECTORS, AND WHICH SECTORS HAVE THE FASTEST AND SLOWEST RESPONSE TIMES?**

    ANSWER:
    Calculated the average response time per sector with the following dax formula making a measure as:
    AvgResponseTimePerSector = 
    CALCULATE(AVERAGE(df[Response Datetime]), ALLEXCEPT(df, df[Sector]))
    Others have the fastest response time with a response time of: (45,034) and slowest response time being that of ida: (44,952)

**Distribution Of Response Times Across Different Sectors**
![Screenshot (318)](https://github.com/user-attachments/assets/934fbdf8-4c7c-4187-b73c-d1a9bd9cade6)

•**WHICH INCIDENTS HAVE THE LONGEST ON SCENE-TIME, AND HOW DOES THIS CORELLATE WITH THE INCIDENT TYPE OR PRIORITY LEVEL?**

       ANSWER:
    So here I had to first identify the longest on scene time with the following Dax;

    LongestTimeSpentOnScene = MAX(df[Unit Time on Scene])
    I then bring out a table for visualisation since we are dealing with the incident type and with the priority level  we use the combination of the : incident type , the priority level , longest time spent on scene and average time spent on scene  to show the Max and Avg time  amongst the priorities and the incidents.

    The incident type of “Dispatched incidents” being the only incident type  had a longest time on scene total value of (24,60453) when later broken down also to see the longest times spent on scene by priority level ; priority 2 had a value of (84,9306), priority 3 had a value of (124,2710) , prority 1had a value of (1348648)  and priority 0 a value of (2460453) then each having varying average times spent on scene: Dispatched Incident have an average time on scene of: (6,090.75), priority 2 having an average time on scene of (4,324.04) , priority 3 has an average time of (4,055.83) and priority 1 has an average of (8,509.10) and priority 0 having an average of  (12, 493.82)

    Then to show the correlation amongst the incident type and priority level we use a scatter plot, to show the average time spent on scene with respect to incident type and priority level


**Average Time On Scene By Incident Type And Priority Level**
  ![Screenshot (319)](https://github.com/user-attachments/assets/80a4a475-6939-46a5-8ae5-209b2518005c)

•**WHICH TYPES OF INCIDENTS TYPICALLY REQUIRE REPORTS  TO BE WRITTEN, AND HOW FREQUENTLY DO THESE OCCUR?**

    ANSWER:
    Firstly I have to get the incidents that do require reports to be written, by creating a measure to count/isolate the “Yeses” under the report written flag column:

    DAX MEASURE:
    ReportRequiredCount = 
    CALCULATE(COUNT(df[Incident Number]), 
              df[Report Written Flag] = "Yes"
    )
    Then I calculated the total number of incidents by incident type 

    TotalIncidentsByType = COUNT(df[Incident Number])

    Then finally creating a report frequency type measure to  give the frequency of each incident type as a percentage.

    ReportFrequencyByType = 
    DIVIDE([ReportRequiredCount], [TotalIncidentsByType], 0)

    Then visualise on a clustered bar chart using the reportfrequencybytype  and the incident type
    And that  eventually gave a final result of (0.26)

**Frequently Report Written Type Of Incidents**
![Screenshot (320)](https://github.com/user-attachments/assets/33a40efa-2339-4bf8-9b07-26b62264b2ed)

•**HOW MANY INCIDENTS WERE INITIATED BY OFFICERS IN THE FIELD COMPARED TO THOSE DISPATCHED VIA 911 CALLS?**

       ANSWER:
    Theres no column which provides a way to discern how calls are initiated.

•**WHAT IS THE AVERAGE NUMBER OF UNITS DISPATCHE TO INCIDENTS BASED ON THE INCIDENT TYPE?**

      ANSWER:
    To get I  simply calaculated the average of the number of units dispatched with respect to the incident type:

    AverageNoofunitsdispatchedPIT = 
    CALCULATE(
        AVERAGE(df[Number of Units Arrived]),
        ALLEXCEPT(df, df[Incident Type])
    )

    Then the total number for the average is released at(1.93) on a card

**Average Number Of Incidents Dispatched Per Incident Type**
![Screenshot (321)](https://github.com/user-attachments/assets/d9950ef5-ced5-49a0-b0bc-c0c38e7e4a86)

•**HOW DO INCIDENTS INVOLVING OFFICER INJURIES CORRELATE WITH MENTAL HEALTTH RELATED FLAGS, AND WHICH SECTORS HAVE THE HIGHEST OCCURENCE OF THESE INCIDENTS?**

      ANSWER:
    Created a measure to find out the officer injuries incidents that coincide with mental health related cases :
    OfficerInjuryMentalHealthIncidents = 
    CALCULATE(
        COUNT(df[Incident Number]),
        df[Officer Injured/Killed Count] > 0,
        df[Mental Health Flag] = "Yes"
    )
    And found out that there aren’t any cases like that and as such there is no correlation

**Corellation**
![Screenshot (322)](https://github.com/user-attachments/assets/86656818-e8f7-42f8-9c9d-beec1515fc79)
