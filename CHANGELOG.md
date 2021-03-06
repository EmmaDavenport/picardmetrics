# Change Log

# 0.1.4 - 2015-05-22

## Fixed

-   The `picard collate` command now tolerates missing files and will still
	collate the existing files.

-   The collated output file `PREFIX-alignment-metrics.tsv` no longer has
	extra blanks lines.

-   Fix the invocation of `md5sum -c` in `test/test.sh`.

-   Some systems like CentOS don't have an up-to-date version of coreutils.
	So, I replaced the invocation of `realpath` with a Bash function that does
	produces the same output.

## Changed

-   The `rnaseq_metrics` function will generate a sequence dictionary for the
	rRNA intervals_list file on-the-fly by taking it from the BAM file. The
	sequence dictionary consists of the BAM header lines starting with '@SQ'.

    -   The script `scripts/make_rRNA_intervals` no longer downloads
    	chromosome sizes from UCSC.

-   The `sort_sam` function checks if the output BAM is correct.

-   The reference genome sequence is no longer copied to RAM.

-   The script `scripts/make_refFlat` no longer downloads the reference
	genome. The user must use their own anyway.

-   In `scripts/install_deps`, roll back to Picard 1.126 because of a
	conflicting change introduced in Picard 1.130. See here for more details:
    https://github.com/broadinstitute/picard/issues/212

# 0.1.3 - 2015-04-23

## Fixed

-   The `collate_` functions did not correctly check for the number of metrics
    files. This affects output generated using `picardmetrics` without `-r`.

## Changed

-   The output BAM file is now deleted after a successful run.

-   Added option `-k` to optionally keep the output BAM file.

-   The configuration file is now called `picardmetrics.conf` instead of
    `.picardmetricsrc`.

## Added

-   Added extra commands to the Makefile to ease installation of dependencies
    and download of human reference data.

    -   Now h38 is downloaded by default instead of hg19. The user can modify
        the script to get different versions.

# 0.1.2 - 2015-04-09

## Fixed

-   In `collate_all`, check for `prefix-rnaseq-metrics.tsv` file before
    attempting to merge the files into `prefix-all-metrics.tsv`.
    
    -   Warnings are no longer printed when a user tries to collate output
        files after running picardmetrics without the '-r' option.

-   The tests have been updated: the md5sum of final output files is checked.
    This is more robust than checking content of log files.

## Changed

-   Removed regular expression from `is_bam` function, so the script will run
    with Bash version 2 released prior to 2004.

-   Previously, output files were written to a directory called
    'picardmetrics' created in the BAM file's directory. Currently, the output
    files are written to a user-specified directory or the current directory
    by default.

-   The `collate_` functions previously accepted the BAM files output by
    picardmetrics as an argument. Now, the `collate_` functions accept a
    directory instead and search for the appropriately named files. This means
    that the BAM files created by Picard may be deleted after running
    picardmetrics.

# 0.1.1 - 2015-03-20

## Changed

-   Write output files to `project1/sample1/picardmetrics` instead of
    `project1/sample1/`.

# 0.1 - 2015-03-16

-   Initial release.
