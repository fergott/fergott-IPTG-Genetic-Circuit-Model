# fergott-IPTG-Genetic-Circuit-Model
Dataset citation: David J. Ross (2020), LacI protein genotype-phenotype landscape data, National Institute of Standards and Technology, https://doi.org/10.18434/M32259 (Version: 1.0, Accessed 2026-10-10)

LacI wild-type Hill fits
Fits Hill dose-response curves to wild-type LacI (lac repressor) sensor data from the LacI deep mutational scanning dataset, and compares the fitted parameters with the ones reported by the authors.

What it does
1.Loads the variant table from an HDF file (one row per barcoded variant).
2.Selects wild-type barcodes with those parameters: 0 LacI amino acid mutations, confident CDS, more than 5000 total counts, and no           mutations in the tetA, KAN, Ori, YFP and insulator plasmid regions.
3.The top 10 by read count are kept (max_variants).
4.Takes the median (0.5 quantile) of sensor_GP_g_quantiles at the 12 IPTG concentrations as the curve, and estimates sd from the 5-95%       range.
5.Fits log10 of the Hill equation with lmfit (free parameters: G0, Ginf, EC50, n), weighted by 1/sd.
6.Compares the fits with the authors' log_low_level, log_high_level, log_ic50 and log_n.


Requirements
Python 3, numpy, pandas, matplotlib, lmfit, and tables (needed by pandas.read_hdf).

pip install numpy pandas matplotlib lmfit tables

run in the Jupyter notebook.


Outputs
results/wt_fits.csv: our fitted G0, Ginf, EC50, n, the authors' values, and the reduced chi-squared for each barcode.

figures/wt_curves_fits.png: measured curves (median ± sd) with Hill fits.

figures/ours_vs_authors.png: our parameters against the authors', with a dashed identity line.

A printed summary (mean ± sd across barcodes) of each parameter and the mean ours/authors ratio.


TO DO: 
Build a dynamic ODE model 
Compose a genetic circuit

