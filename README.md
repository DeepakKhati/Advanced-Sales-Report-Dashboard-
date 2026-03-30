# Awesome Chocolates — Advanced Sales Dashboard
## Power BI Advanced Project

## Project Overview
An advanced Power BI dashboard analyzing sales performance, 
profitability, shipment efficiency, and salesperson targets 
for Awesome Chocolates — a fictional chocolate company 
operating across 6 geographies.

## Technical Skills Demonstrated
- Power BI Desktop — multi-page report design
- Power Query — data cleaning, calculated columns
- DAX — intermediate to advanced measures
- Time Intelligence — MoM analysis, PREVIOUSMONTH, EDATE
- Calendar table — marked date table with custom columns
- Data Modeling — star schema with measures table
- Bookmarks & Action Buttons — navigation and interactivity
- Conditional Formatting — icon sets, color scales
- Parameters & Bins — dynamic shipment analysis
- Zoom Slicer — interactive shipment distribution

## DAX Measures Written

### Basic Measures
```dax
Total Sales = SUM(sales[Amount])
Total Boxes = SUM(sales[Boxes])
Total Shipment = COUNTROWS(sales)
Total Costs = SUM(sales[Costs])
Total Profit = [Total Sales] - [Total Costs]
Profit % = DIVIDE([Total Profit], [Total Sales])
```

### Time Intelligence
```dax
Total Sales (prev month) = 
    CALCULATE([Total Sales], 
    PREVIOUSMONTH('calendar'[Date]))

MoM Sales Change % = 
    VAR this_month = [Total Sales]
    VAR prev_month = [Total Sales (prev month)]
    RETURN DIVIDE(this_month - prev_month, prev_month)

Total Sales Latest Month = 
    VAR ld = [Latest Date]
    RETURN CALCULATE([Total Sales], 
    'calendar'[Start of Month] = ld)

Latest MoM Sales Change % = 
    VAR ld = [Latest Date]
    VAR this_month_sales = [Total Sales Latest Month]
    VAR prev_month_sales = 
        CALCULATE([Total Sales], 
        'calendar'[Start of Month] = EDATE(ld,-1))
    RETURN 
        DIVIDE(this_month_sales - prev_month_sales, 
        prev_month_sales)
```

### Performance Indicators
```dax
Profit Target = 0.60

Profit Target Indicator = 
    IF([Profit %] > [Profit Target], 2,
    IF([Profit %] > 0.9 * [Profit Target], 1, 0))
```

## Business Insights

### 1. Overall Performance
- Total revenue of $34M across 13 months (Feb 2023 — Feb 2024)
- Overall profit margin of 60.3% — healthy for FMCG sector
- 10.2% of shipments classified as Low Shipment Boxes (LSB)

### 2. Month on Month Trends
- Biggest single month drop: November 2023 at -19.9%
- Strong recovery in December 2023 at +28.9%
- Latest month (February 2024) showing -10.8% decline
- Seasonal pattern visible — Q4 volatility consistent

### 3. Salesperson Performance
- Kelci Walkden leads with $1,518K total sales
- Marney O'Breen has highest Profit % at 66.7%
- Madelene Upcott only salesperson below 60% profit target
- Most salespeople consistently hitting profit targets

### 4. Shipment Analysis
- Majority of shipments are under 500 boxes
- Long tail distribution — few very large shipments exist
- LSB rate of 10.2% indicates room for shipment optimization

## Dashboard Pages
- **Page 1** — Main KPI Dashboard with tabbed trend analysis
- **Page 2** — Month on Month Sales Analysis table
- **Page 3** — Shipment Distribution Analysis
- **Page 4** — Profit Target Indicator by Salesperson
- **Trend Toolkit** — Supporting trend analysis page

## Data Model
- actuals (fact table) — sales transactions
- calendar (dimension) — marked date table
- DSalesPersons (dimension) — salesperson details
- products (dimension) — product information
- _measures (virtual table) — all DAX measures organized

## Known Limitations
- Universal profit target of 60% applied to all salespersons
  regardless of experience or territory
- No marketing spend data available for ROI analysis
- Hardware constraints (i3, 8GB RAM) limited some 
  interactive features

  ## Business Questions Answered
1. Which salesperson is performing above/below target?
2. How are monthly sales trending vs previous month?
3. What is the shipment size distribution?
4. Which months show highest sales volatility?
5. Is the business hitting its 60% profit target?

## Tools Used
Power BI Desktop | Power Query | DAX | Time Intelligence

## Screenshots

## KPI Dashboard with Trend analysis
![Page 1](https://github.com/DeepakKhati/Advanced-Sales-Report-Dashboard-/blob/main/Screenshots/01_LSB_by_products.png)

## Month on Month Sales Analysis
![Page 2](https://github.com/DeepakKhati/Advanced-Sales-Report-Dashboard-/blob/main/Screenshots/02_Total_sales_at_SOM.png)

## Main Dashboard 
![Page 3](https://github.com/DeepakKhati/Advanced-Sales-Report-Dashboard-/blob/main/Screenshots/03_main_sales_report.png)


## Shipment Distribution Analysis
![Page 4](https://github.com/DeepakKhati/Advanced-Sales-Report-Dashboard-/blob/main/Screenshots/04_Total_shipment.png)

## Profit Target Indicator By Salesperson
![Page 5](https://github.com/DeepakKhati/Advanced-Sales-Report-Dashboard-/blob/main/Screenshots/05_target_per_salesperson.png)
