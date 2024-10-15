# nallo-resources

This document contains examples of resources that _could_ be used with https://github.com/genomic-medicine-sweden/nallo.

## SVDB databases

SVDB QUERY can use the "Structural Variant" set from gnomAD v4.1.0 (https://storage.googleapis.com/gcp-public-data--gnomad/release/4.1/genome_sv/gnomad.v4.1.sv.sites.vcf.gz). This dataset includes CNVs with annotations not compatible with SVDB. One way to solve this is to simply remove them:

```
zcat gnomad.v4.1.sv.sites.vcf.gz | grep -v "CNV" | bcftools view --output-type z --output gnomad.v4.1.sv.sites_no_cnv.vcf.gz
```

It can also use SVs from ColoRSdb (https://zenodo.org/records/13145123/files/CoLoRSdb.GRCh38.v1.1.0.pbsv.jasmine.vcf.gz) without modification. The input file to `--svdb_dbs` could then look like:

```
filename,in_freq_info_key,in_allele_count_info_key,out_freq_info_key,out_allele_count_info_key
/home/proj/stage/workflows/nallo/references/references_dev/CoLoRSdb.GRCh38.v1.1.0.pbsv.jasmine.vcf.gz,AF,AC,colorsdb_af,colorsdb_ac
/home/proj/stage/workflows/nallo/references/references_dev/gnomad.v4.1.sv.sites_no_cnv.vcf.gz,AF,AC,gnomad_af,gnomad_ac
```
