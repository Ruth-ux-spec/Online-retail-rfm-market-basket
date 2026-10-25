Online Retail Analytics: RFM Segmentation & Market Basket

Module 2 Practice Lab | CadetX Internship
Author: Ruth Okoye

Business Question

"Which customers and products actually make us money, and who is about to stop buying?"

Dataset

	•	Source: Online Retail dataset (UK giftware wholesaler), Online Retail.xlsx
	•	Size: 541,909 transaction rows, 8 columns (InvoiceNo, StockCode, Description, Quantity, InvoiceDate, UnitPrice, CustomerID, Country)
	•	Period: 1 December 2010 to 9 December 2011

The dataset is not included in this repository because of its size.

Tools

Python, Pandas, NumPy, mlxtend (Apriori), Jupyter Notebook

What I Did and What I Found

Task 1: Load and clean

	•	Loaded the file with Pandas.
	•	Dropped 135,080 rows with no CustomerID, because RFM needs a customer.
	•	Removed cancelled orders (invoice numbers starting with "C").
	•	Result: 397,924 clean rows.

Task 2: Total sales

	•	Kept only rows with Quantity > 0.
	•	Created TotalSales = Quantity * UnitPrice.
	•	Result: median line value about £11.80, mean about £22.39. The maximum (£168,469.60) is an outlier, likely a bulk order.

Task 3: Monthly revenue and top countries

	•	Grouped revenue by month and by country.
	•	Peak month: November 2011 at about £1.16M. Revenue builds from September, which fits pre-Christmas stocking.
	•	December 2011 looks low only because the data ends on 9 December.
	•	Top country: United Kingdom at about £7.31M, far ahead of the Netherlands (about £285k), EIRE, Germany and France.

Task 4: RFM segmentation

	•	Recency: days since last purchase. Frequency: number of invoices. Monetary: total spend.
	•	Scored each from 1 to 5 using quintiles and grouped customers into segments.

Segment	Customers
Champions	1,139
Lost	913
About to Sleep	870
Loyal Customers	821
New / Promising	320
At Risk (Big Spenders)	276

	•	Champions (average recency 13 days, about 10 orders, about £5,204 spend) bring in the most money.
	•	At Risk customers spent about £1,571 each on average but have not bought in about 137 days. They are the priority to win back.
	•	About to Sleep and Lost are lower value.

Task 5: Market basket analysis

	•	Used UK invoices only (16,649 invoices) and products appearing on at least 100 invoices (1,066 products).
	•	Ran Apriori with 2% minimum support: 235 frequent itemsets and 76 association rules (in Jupyter with mlxtend).
	•	Strongest rules: the Pink, Green and Roses Regency Teacup and Saucer sets, with lift of about 19 to 24.
	•	Other pairs: Gardeners Kneeling Pads (lift about 16), Alarm Clock Bakelike colours (about 14), wooden frames and Paper Chain Kits (about 11).
	•	In the CadetX Practice Lab, mlxtend could not be installed (it needs a newer pandas), so support, confidence and lift for product pairs were calculated directly with Pandas and NumPy.

Recommendations

	1.	Protect Champions and Loyal customers: reward them, since they bring in most of the revenue.
	2.	Win back At Risk customers first: contact them with a targeted offer, because they have a high spend history.
	3.	Cross-sell design variants: when a customer adds one Regency teacup set (or another product design), suggest the other designs, or bundle them.
	4.	Prepare for the autumn peak: stock and marketing should build from September to November.

Limitations

	•	Results are for one year of data from one UK wholesaler.
	•	The December 2011 figure is incomplete.
	•	Market basket rules were built on UK invoices only.
	•	Segment rules (the R and F score cut-offs) are a common convention, not the only valid choice.

How to Run

	1.	Download the dataset and place Online Retail.xlsx in the same folder as the notebook.
	2.	Install the requirements: pip install pandas numpy openpyxl mlxtend
	3.	Open the notebook in Jupyter and choose Run All Cells.
