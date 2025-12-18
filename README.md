# Scarf Production Dashboard Project

## Project Background ##

@rajaslempang.jogja is a growing custom scarf producer that provides customized embroidered scarves for graduation accessories with over thousand customers. @rajaslempang.jogja is capable of producing up to a hundred scarves per day. With a growing business, a production monitoring tool is needed to monitor production performance with ease, displayed on a single dashboard. The main information to be displayed is accumulated productivity, downtime, and running hours, as well as average running hours, frequency of trouble occurred for each machine and trouble type. 
This project is expected to build a production monitoring dahsboard that provides quick overview of production performance. 

## Summary ##

![Production Monitoring Dashboard](https://github.com/Dwisetiyawan/Scarf-Production-Dashboard-Project/blob/main/Documentation/Production%20Monitoring%20Dashboard.gif)

*Production Monitoring Dashboard*

With the dashboard above, key informations in production process such as productivity, downtime, running hour, and frequency of trouble occured can be monitored in a single display. Machine selection button created for user to select which machine to be highlighted on the charts, so user could easily see how the performance of the machine selected showed on each chart. Accumulating productivity shows how many pieces product (scarf) are produced by each machine per hour over an accumulated period of time. Accumulating running hours indicates the total time each machine has operated over a specified period. Average running hours indicates the average time of ech machine operated in a day. Accumulating downtime shows how much time is lost because of the stopped production process during production in a day over an accumulated period of time. The causes of downtime for each machine are shown on the trouble frequency chart, showing how many times trouble occurred at each machine over an accumulated period of time. Another trouble frequency chart created to monitor how many times specific type of trouble occured during specified period. The types of troubles shown on the chart are collected based on actual troubles from the owner's experience. Both of the trouble frequency chart created to help user decide which machine or which type of trouble should prioritize to be fixed.  

![Daily Production Monitoring]()

*Daily Production Monitoring*

Besides the main dashboard, daily production monitoring is created to monitor the daily production trend, as shown by the chart for each machine includes information about productivity, running hours, and downtime. The information from daily production monitoring is expected to give a better understanding of how the production process runs daily.

## Caveats ##

- Trouble types collected: 

        a. Jarum patah (broken needle)
        b. Bundet bawah (tangled thread at lower part)
        c. Bundet atas (tangled thread at upper part)
        d. Benang putus (snapped thread)
        e. Sensor lepas (detached sensor)
        f. Mesin mati (sudden power loss)
- Running Hours Calculation = stop time - start time - downtime
- Productivity Calculation = product quantity (pcs) / running  hours (hours)

## Skills Used ## 
- Data Validation to make filtered list, filtering the result showed based on machine chosen
- Table for storing production data such as start time, stop time, downtime start, downtime stop, and downtime cause, which collected on each machine whenever it is operated. 
- Bar Chart for visual comparison of  accumulated productivity, downtime, and running hours, as well as average running hours, frequency of trouble occurred for each machine and trouble type.
- Line Chart to show daily trend of productivity, running, and downtime of each machine. 
- Formulas & Functions :
    
    1. Utilize sum function with nested if to sum up the downtime based on the machine
        ```
        =SUM(IF(([@Machine]=Table5[Machine]);Table5[Downtime]))
        ```

    2. Utilize count function with nested if to count frequency of trouble occurred based on the machine and the trouble type 
        ``` 
        =COUNT(IF((Table5[Machine]=A15)*
        (Table5[Downtime]<>0);Table5[Downtime]))

        =COUNTIFS(Table5[Machine];Calculation!H15;
        Table5[Downtime Cause];Calculation!$I$14:$N$14;
        Table5[Downtime];"<>0")
        ```
    3. Utilize average function with nested if to calculate the average running hours based on the machine
        ```
        =AVERAGE(IF((Table4[Machine]=Calculation!$O2);Table4[Average Running Hour])) 
        ```
    4. Utilize sort function to sort accumulated productivity, downtime, running hours, average running hours, frequency of trouble based on the value by descending order
        ``` 
        =SORT($A$15:$B$23;2;1)
        ```
    5. Utilize if function to make the chosen machine highlighted on the chart
        ```
        =IF($C2<>Machine;$D2;NA())
        =IF($C2=Machine;$D2;NA())
        ```