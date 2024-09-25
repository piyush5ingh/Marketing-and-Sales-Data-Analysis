# Marketing-and-Sales-Data-Analysis

## Overview
This project focuses on analyzing marketing and sales data using Power BI and DAX formulas. The goal is to uncover insights about sales performance, marketing effectiveness, and trends over time.

## Dataset

You can download the dataset here: [Dataset Link](https://1drv.ms/f/c/c9e4d94d1be77dfb/EhGsAcGP2dpJkxYonqGPoFQBSHgzCa_rAfzSS4W6bVDiPg?e=IDQ24D)

The dataset consists of four tables:
1. **Sales Data**: Information on deals closed, sales team size, and lead source.
2. **Sales Representative**: Sales representatives and accounts.
3. **Marketing Budget**: Marketing spend by industry.
4. **Lead Code**: Codes for different lead sources.

## KPIs Analyzed
- **Sales by Industry**: The total sales grouped by industry.
- **Sales Representative Performance**: Performance based on total sales handled by each rep.
- **Marketing Budget Allocation**: Comparing marketing budget vs. sales.
- **Sales by Lead Source**: Breakdown of total sales by lead source.
- **Month-over-Month (MoM) Growth**: Monthly growth in sales.
- **Year-over-Year (YoY) Growth**: Annual growth comparison.
- **Customer Acquisition Costs (CAC)**: Cost of acquiring new customers.
- **Marketing ROI**: Return on marketing investment.
- **Revenue to Marketing Spend Ratio**: Revenue generated per dollar spent on marketing.

1. **Sales Data**:
   - Key columns: Account Number, Age, Amount, Close Date, Created Date, Industry, Lead Source, Size of Sales Team, Stage, Team Size Code, and Type.

2. **Sales Representative**:
   - Key columns: Account Number and Sales Rep.

3. **Marketing Budget**:
   - Key columns: Industry and Annual Marketing Budget, showing marketing expenditure for various industries.

4. **Lead Code**:
   - Key columns: Lead Source and Lead Code, defining the codes for different lead sources.

## KPIs (Key Performance Indicators)
I conducted an analysis using the available data to identify trends and key insights. Here’s what I focused on:

- **Sales Amount by Industry**: The total sales by industry.
- **Sales Representative Performance**: Total sales handled by each representative.
- **Marketing Budget Allocation by Industry**: Comparing marketing budget vs. sales by industry.
- **Sales by Lead Source**: Total sales based on different lead sources.
- **Sales Year-over-Year (YoY) and Month-over-Month (MoM)**: Growth metrics for periodic performance.
- **Revenue over Investment**: Measures how much return (or profit) is generated for every dollar spent.
- **Customer Acquisition Costs (CAC)**: Indicates the efficiency of customer acquisition strategies.
- **Conversion Rate (Deals Closed vs. Leads Generated)**: The percentage of leads that convert into closed sales.
- **Revenue to Marketing Spend Ratio**: Measures how much revenue is generated per dollar spent on marketing.

## DAX Formulas for KPIs

1. **Total Sales Amount**:
   ```DAX
   Total Sales = SUM('Sales Data'[Amount])
   ```
   - **Explanation**: Sums up the total sales amount from the Sales Data table.

2. **Sales by Industry**:
   ```DAX
   Sales by Industry = CALCULATE(SUM('Sales Data'[Amount]), ALLEXCEPT('Sales Data', 'Sales Data'[Industry]))
   ```
   - **Explanation**: Calculates the sum of sales grouped by industry while ignoring all filters except the industry filter.

3. **Sales by Sales Representative**:
   ```DAX
   SalesRep = CALCULATE(SUM('Sales Data'[Amount]), RELATED('Sales Representative'[Sales Rep]))
   ```
   - **Explanation**: Totals sales per representative using the relationship between the Sales Data and Sales Representative tables.

4. **Average Deal Size**:
   ```DAX
   Average Deal Size = AVERAGE('Sales Data'[Amount])
   ```
   - **Explanation**: Averages the deal size by averaging the `Amount` column.

5. **Sales Cycle Length (Average Age of Deals)**:
   ```DAX
   Avg Sales Cycle Length = AVERAGE('Sales Data'[Age])
   ```
   - **Explanation**: Averages the age (in days) of deals to calculate the sales cycle length.

6. **Conversion Rate (Deals Closed vs. Leads Generated)**:
   ```DAX
   Conversion Rate = DIVIDE(
       CALCULATE(COUNTROWS('Sales Data'), 'Sales Data'[Stage] = "Closed Won"),
       COUNTROWS('Sales Data')
   )
   ```
   - **Explanation**: Calculates the percentage of leads converted into closed sales.

7. **Marketing ROI**:
   ```DAX
   Marketing ROI = DIVIDE(
       SUM('Sales Data'[Amount]) - SUM('Marketing Budget'[Marketing Budget]),
       SUM('Marketing Budget'[Marketing Budget])
   )
   ```
   - **Explanation**: Measures the return on investment for marketing by comparing sales revenue with marketing spend.

8. **Lead Source Effectiveness**:
   ```DAX
   Sales by Lead Source = CALCULATE(
       SUM('Sales Data'[Amount]), 
       ALLEXCEPT('Sales Data', 'Sales Data'[Lead Source])
   )
   ```
   - **Explanation**: Totals sales based on different lead sources.

9. **Customer Acquisition Cost (CAC)**:
   ```DAX
   CAC = DIVIDE(
       SUM('Sales Data'[Marketing Spending]),
       COUNTROWS(FILTER('Sales Data', 'Sales Data'[Stage] = "Closed Won"))
   )
   ```
   - **Explanation**: Calculates the average cost to acquire a new customer by dividing marketing expenses by the number of closed deals.

10. **MoM (Month-over-Month) Growth**:
    ```DAX
    MoM Growth = DIVIDE(
        [Total Sales] - CALCULATE([Total Sales], PREVIOUSMONTH('Date'[Date])),
        CALCULATE([Total Sales], PREVIOUSMONTH('Date'[Date]))
    ) * 100
    ```

11. **YoY (Year-over-Year) Growth**:
    ```DAX
    YoY Growth = DIVIDE(
        [Total Sales] - CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Date'[Date])),
        CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Date'[Date]))
    ) * 100
    ```

12. **Revenue to Marketing Spend Ratio**:
    ```DAX
    Revenue Efficiency = DIVIDE([Total Sales], [Total Marketing Budget])
    ```
## Power BI Reports

You can view the Power BI report here: [View Power BI Report](https://app.powerbi.com/links/VJnLhfPFDU?ctid=5b4c02d4-75cb-4676-baff-6204a8ee6e4c&pbi_source=linkShare)


    ## How to Use
1. Download the `.pbix` file and open it in Power BI Desktop.
2. Load the data and view the dashboard to interact with the visuals.
3. Review the DAX formulas used to calculate each KPI.

