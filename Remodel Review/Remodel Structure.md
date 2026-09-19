

**Input structure:**

Two files. 

"Prod_data" = what came before.

"Remodel_data" = what exists now.


Each of these files contains a detailed output of a typical media mix model. There is spend data per media channel, other delivery data associated as well as attributed revenue and orders. The transaction level data is typically split out into different outcomes, as denoted by the "Business Outcome" column. There is also a 'productCategory' column. When that says anything other than "All", we need to look at things with that added layer.


#### Analysis
The overall purpose of this tool is to show how things change between the "Prod Data" file and the "Remodel data file".

Point 1: How did the buckets of paid media, unpaid, and baseline change?
This is basiaclly a percentage each of these buckets makes up as a portion of the total revenue, by outcome, by product category.
	In setup, please give me functionality to identify what channels fall into what bucket

Point 2: How did paid media contribution change?
This would be a sorted list of top spenders and top revenue drivers by outcome, by product category.
- Important note: This is a percentage each channel contributes to revenue driven by paid media specifically, NOT grand total revenue.

Point 3: Detailed View
- Spend, revenue, contribution to total revenue, iROAS by channel, by outcome, by product category


