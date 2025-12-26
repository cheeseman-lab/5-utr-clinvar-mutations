# 5' UTR Length Change Analysis

## Motivation

The 5' UTR plays a critical role in translation regulation. Short 5' UTRs (< 40-50 bp) can reduce translation efficiency, affect ribosome scanning, and impact upstream open reading frame (uORF) usage. Additionally, 5' UTR length can influence start codon selection in genes with alternative translation initiation sites, potentially shifting the balance between full-length and N-terminally truncated protein isoforms.

Despite this biological importance, systematic analysis of ClinVar variants that alter 5' UTR length has been limited. Previous approaches relied on HGVS notation to identify 5' UTR variants, which can be unreliable due to transcript version differences and lack of genomic coordinate validation.

This analysis identifies ClinVar indels where both genomic coordinates fall within annotated 5' UTR regions and the variant causes the UTR to cross biologically relevant length thresholds (10, 20, 30, 40, 50 bp).

## Key Findings

- **988 indels** have both start and stop coordinates within GENCODE v47 MANE Select 5' UTRs
- **166 variants** cause ≥10 bp length changes
- **17 variants** cross at least one biologically relevant threshold
- **5 threshold-crossing variants** are in genes with documented truncated isoforms (VHL, CSTB)

The most notable finding: VHL has 10 variants affecting its 5' UTR, where isoform balance between VHL30 (full-length) and VHL19 (N-truncated) has proven clinical significance.

## Documentation

- [Methods](docs/methods.md) - Detailed methodology and data sources
- [Truncated Isoforms Analysis](docs/truncated-isoforms.md) - Biological analysis of variants in genes with alternative translation

## Usage

```bash
python run_analysis.py                              # Default: min-size=10, thresholds=10,20,30,40,50
python run_analysis.py --min-size 5 --thresholds "20,40,60"
python run_analysis.py --force-download             # Re-download data files
```

## Output

Results are written to `results/`:
- `5utr_variants_min10bp.csv` - All variants with ≥10 bp size changes
- `5utr_variants_min10bp_cross{N}bp.csv` - Variants crossing each threshold
- `5utr_length_changes_min10bp_cross{N}bp.png` - Slope plots

## Requirements

- Python 3.8+
- pandas, matplotlib
- wget

## License

MIT License - see [LICENSE](LICENSE)
