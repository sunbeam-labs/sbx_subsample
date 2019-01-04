# sbx_subsample
This is an extension to the [Sunbeam pipeline](https://github.com/sunbeam-labs/sunbeam) to subsample reads after host decontamination and quality control.

## Installing

Clone the repo into your sunbeam `extensions/` folder, installing requirements through Conda, and adding the new options to your existing configuration file. Make sure you've [installed Sunbeam](https://sunbeam.readthedocs.io/en/latest/quickstart.html) first!

    source activate sunbeam
    cd $SUNBEAM_DIR
    git clone https://github.com/louiejtaylor/sbx_subsample/ extensions/sbx_subsample
    conda install --file extensions/sbx_subsample/requirements.txt

Add the options to your config file (replace "sunbeam_config.yml" with the name of your config file).

    cat $SUNBEAM_DIR/extensions/sbx_subsample/config.yml >> sunbeam_config.yml

Make sure to edit the config file to include the number of reads you'd like to sample.

## Running

As this extension replaces an intermediate step of the Sunbeam pipeline, you must run `all_subsample` before running any step that uses quality-controlled reads (for example: `all_annotate`, `all_classify`, `all_mapping`, etc.).

For example, if you want to annotate contigs built from subsampled reads, first run:

    sunbeam run --configfile sunbeam_config.yml all_subsample

This will leave you with quality-controlled reads, subsampled to the target number. The starting (non-subsampled), decontaminated files will be backed up in `sunbeam_output/qc/decontam/full/`. Then, run downstream steps as usual:

    sunbeam run --configfile sunbeam_config.yml all_annotate

## Contents

 - `requirements.txt` specifies the extension's dependencies
 - `config.yml` contains configuration options that can be specified by the user when running an extension
 - `sbx_template.rules` contains the rules (logic/commands run) of the extension
 
    

