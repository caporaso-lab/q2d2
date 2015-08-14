

## Installation (conda-based)

```bash
conda create -n q2d2 python=3.4 scikit-bio ipython-notebook
source activate q2d2
git clone https://github.com/gregcaporaso/q2d2.git
cd q2d2
pip install -e .
```

## Usage

Run the following commands to generate analysis notebooks:

```bash
q2d2 seqs_to_biom --sequences-filepath $PWD/example-data/keyboard/seqs.fna --analysis-root my-analysis
q2d2 biom_to_pcoa --analysis-root my-analysis --metadata-filepath $PWD/example-data/keyboard/sample-md.tsv --color-by Subject
q2d2 biom_to_adiv --analysis-root my-analysis --metadata-filepath $PWD/example-data/keyboard/sample-md.tsv --collated-alpha-filepath $PWD/example-data/keyboard/q191/faith-pd-collated.tsv
q2d2 biom_to_taxa_plots --analysis-root my-analysis --metadata-filepath $PWD/example-data/keyboard/sample-md.tsv --otu-metadata-filepath $PWD/example-data/keyboard/q191/otu-md.tsv --otu-table-filepath $PWD/example-data/keyboard/q191/otu-table.tsv
q2d2 start_server --analysis-root my-analysis
```

Follow the instructions from the previous command to interact with the analysis notebooks.
