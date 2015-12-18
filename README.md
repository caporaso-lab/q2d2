# q2d2: QIIME 2 is documentation-driven (a public prototype)

This repository is a publicly accessible prototype of some ideas that we're exploring for QIIME 2. For some information on what's coming in QIIME 2, see [@gregcaporaso's blog post, "Toward QIIME 2"](https://qiime.wordpress.com/2015/10/30/toward-qiime-2/).

**This repository is not QIIME 2 - that doesn't exist yet.** The code in this repository is untested and highly experimental. You should not use this for any real analysis, only for exploring the documentation-driven interface and interactive visualizations. If you're interested in using the underlying methods (e.g., UniFrac, Faith PD, ANOSIM), those are generally available in [scikit-bio 0.4.1](http://scikit-bio.org/) and later.

## Installation (conda-based)

We only support installation of Q2D2 using ``conda``. Other methods may work, but we'll keep these instructions up-to-date. This will install a working development environment for Q2D2.

```bash
conda create -n q2d2 -c https://conda.anaconda.org/biocore python=3.5 scikit-bio jupyter pyyaml
source activate q2d2
pip install https://github.com/rossant/ipymd/archive/master.zip
git clone https://github.com/gregcaporaso/q2d2.git
cd q2d2
pip install -e .
```

## Usage: Graphical interface

### Launch the server

Run the following commands to launch the Q2D2/Jupyter server:

```bash
mkdir my-study
cd my-study
q2d2 serve
```

### Load data files

You'll be prompted to load files in the web browser window that opens. The following table describes the input files.

|  File type  | Example location  | Description  |
|---|:-:|---|
| ``sample_metadata``  |  ``q2d2/example-data/keyboard/sample-md.tsv`` | Per-sample metadata (e.g., a QIIME 1 mapping file). These can be validated with [Keemei](http://keemei.qiime.org/).  |
| ``otu-metadata`` |  ``q2d2/example-data/keyboard/q191/otu-md.tsv`` | Per-otu metadata (e.g., a QIIME 1 *taxonomy map*, such as those resulting from running ``assign_taxonomy.py``). |
| ``tree``  |  ``q2d2/example-data/keyboard/q191/rep-set.tre`` | A rooted phylogenetic tree containing all of the OTU IDs in ``unrarefied_biom``. A tree generated by QIIME 1's ``make_phylogeny.py`` (i.e., FastTree2) **will not** work directly, as that will be an unrooted tree. An approach for rooting an unrooted trees is described in scikit-bio's [#1227](https://github.com/biocore/scikit-bio/issues/1227#issue-121285751). |
| ``unrarefied_biom``  |  ``q2d2/example-data/keyboard/q191/otu-table.tsv`` | An unrarefied BIOM table in "classic" (i.e., tab-separated text format). This can be created with a QIIME 1 workflow, and then converted to tab-separated text with ``biom convert --to-tsv``. You should not include an sample or observation/OTU metadata in this file, as that should be provided in ``otu-metadata``. (This will be updated to support any BIOM-formatted file.) |
| ``rarefied_biom``  |  None provided, can be generated using the *Rarefy BIOM Table* workflow. | A rarefied BIOM table (i.e., where all samples have the same number of counts, and that number is greater than 0). The same format restrictions apply as for ``unrarefied_biom``. |

## Usage: Command line interface

This will work, but is legacy functionality and will likely be removed. It doesn't offer any benefits over the command line interface

```bash
q2d2 create-study --study-id my-study --sample-metadata-filepath $PWD/example-data/keyboard/sample-md.tsv --otu-metadata-filepath $PWD/example-data/keyboard/q191/otu-md.tsv --tree-filepath $PWD/example-data/keyboard/q191/rep-set.tre --unrarefied-biom-filepath $PWD/example-data/keyboard/q191/otu-table.tsv
ipython notebook my-study/index.md
```
