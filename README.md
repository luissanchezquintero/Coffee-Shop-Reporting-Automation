# Automated Monthly Sales Reporting | Excel + Power Query

Business problem
A fictional three-location coffee shop needs to replace manual monthly spreadsheet consolidation and repetitive management-report updates. The goal is to accept a new monthly Excel file, apply the same data-preparation rules, and refresh an interactive dashboard with traceable, validated results.
This is a self-directed portfolio simulation, not work delivered to a paying client. The underlying dataset comes from Maven Analytics' Coffee Shop Sales Data Playground. The original transaction dates were shifted to 2026 for the reporting exercise, and controlled data-quality issues were introduced to test the workflow.

Solution
Built an Excel reporting system that:
- Discovers eligible monthly Excel files in a designated local folder using a Power Query folder connection.
- Extracts a consistently named Excel Table (tblSales) from each workbook and combine its transaction records.
- Standardizes dates, time, text, store names, numeric values, and missing product classifications.
- Audits duplicate transaction IDs and removes duplicates in the cleaned reporting layer.
- Preserves the source file name for tracing transactions back to the original workbook.
- Feeds PivotTables, KPI calculations, three charts, and store/category slicers.
- Supports user initiated refresh when a new monthly file is added; it is not unattended or scheduled automation.
  
Reporting workflow
Monthly Excel files → Power Query folder ingestion → Raw staging → Cleaning & validation → Excel Table → PivotTables → KPI dashboard

The dashboard provides revenue, transactions, units sold, average order value, monthly revenue trends, store revenue, product-category revenue, month-over-month growth, and year-to-date revenue. Slicers support store and product-category analysis.

Validation and Automation Tests
A temporary Sales_2026_07 Excel workbook was added during testing with 10 transactions, 16 units, and $47.95 in sales.
-Transaction count increased from 149,116 to 149,126.
-Total revenue increased from $698,812.33 to $698,860.28. 
-Units sold increased from 214,470 to 214,486.
-Rollback - removing July and refreshing restored the six month baseline.
Troubleshooting example: The initial July test reused existing transaction IDs, causing the deduplication step to exclude valid records. Unique July IDs resolved the issue. This revealed an important limitation: conflicting IDs should be flagged and investigated before automatic removal in a production implementation.

Limitations
- The sales data is fictional; dates were shifted to 2026 for this portfolio exercise.
- This is user initiated refresh, not a background or scheduled job.
- The source data lacks cost of goods sold and operating expenses, so the model reports revenue, not profit.
- The tested YTD logic covers one reporting year; multi-year rollovers would require further validation.
- A local file path may need to be changed on another computer.
- The duplicate-ID removal approach requires an exception-handling process for conflicting source records in a real deployment.
- No measured time savings or client financial impact is claimed.
