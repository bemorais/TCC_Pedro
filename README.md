# Analysis of Proteins Related to EMT and the USP5-RPS27A Pathway Using MRM Strategy by Mass Spectrometry
A panel containing 14 proteins was optimized from injections of a mix that included all control and treatment conditions. The best peptides were selected using the PREGO tool, and those that did not show a good signal after the first run were discarded. In the second run of the mix, the retention time windows were narrowed to 4 minutes for most peptides. Peptides that still did not perform well after the second run were discarded, and the samples were then run individually in triplicate injections. An internal quantification standard was added to the samples for normalization, and the peptide selected for this was TIMP1.

# Table Processing Before Analysis

## 1 -  Download and Generate the Pivot Table

- I opened the downloaded .csv file in Excel and saved it as .xls with the name AreasRelatorio.xls, placing it in the Data folder.

- I deleted the 'Peptide Modified Sequence' and 'Library Intensity' columns, and created a new column called 'Area' to calculate 'Total Area' - 'Total Background'. After this, I copied and pasted the values as "values only" into a new column. I then deleted the original 'Total Area', 'Total Background', and the formula-based 'Area' column, keeping only the copied values.

- In the pivot table, I set the following: Columns: 'Replicate Name';
Rows: 'Protein Name' and 'Peptide Sequence';
Values: 'Sum of Areas'

- I copied the pivot table to a new sheet to make some modifications, **pasting values only**.

## 2 - Simplifying the Pivot Table for Python Script

- I removed the sum of Areas, as it was not needed for the next steps, since we would normalize the data using the synthetic peptide added to the sample.

- The replicates were named as follows: 'CTRL_A549_1'	'CTRL_A549_2'	'CTRL_A549_3'	'SAHA_A549_1'	'SAHA_A549_2'	'SAHA_A549_3'	'TGFB_A549_1' 'TGFB_A549_2'	'TGFB_A549_3'

- I renamed 'Row labels' to 'Protein_Peptide'.

- I modified the peptide names by adding the protein ID (e.g., 'P04406|G3P_HUMAN') before the peptide sequence.

- After reviewing the table, I decided to remove 'P63261|ACTG_HUMAN_GYSFTTTAER' because its intensity was disproportionately high compared to the others, and since it's actin, there’s a high chance it was a contaminant.

## 3 - Normalizing Areas

- I normalized the areas using the formula: Area / TIMP Area for the replicate * **10** (this value was arbitrarily chosen and consistently applied).

- The values were pasted into a new sheet named 'Normalized', which I used for plotting graphs.
    

# look at the .ipynb in order 1 - QQ-plot; 2 - Heatmap; 3 - BarCode