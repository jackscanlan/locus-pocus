# Locus-Pocus
Tools for finding and extracting barcoding and other taxonomically informative loci

> There's nothing really here yet! I'm just trying to get my thoughts together on the best way to approach building these tools.

### Intended usages

Aligning sequences (from small regions/contigs, to organelles/plasmids, to complete assemblies)
- Use [PGGB](https://github.com/pangenome/pggb) for whole genomes
    - [Estimate divergence](https://pggb.readthedocs.io/en/latest/rst/tutorials/divergence_estimation.html) across all input sequences to guide the selection of appropriate parameters 
    - Discard regions that have presence-absence in one or more samples, unless that occurs in a flagged 'low-quality' sample that may be incomplete
- Use MAFFT for small regions with known total colinearity (i.e. only SNPs and indels allowed), or minimap2 for larger regions with no assumption of colinearity (ie. rearrangements allowed)
- Conversion of MAF to MSA format?
    - [mafTools](https://github.com/dentearl/mafTools) could be useful

Find regions in alignments that resolve known splits between inputs, i.e. contain taxonomically or diagnostically informative information
- Inputs/parameters:
    - One or more MSAs (user-made or from package)
    - Sequence groupings (phylogenetic tree or list of groups); default is to assume all sequences must be distinct from each other
        - for example, multiple sequences from the same species (an 'allowed non-distinct group') can be grouped so that the distinct locus doesn't separate members of the group
    - Maximum size of output locus
- Outputs:
    - MSA subset that contains the discriminating locus
    - Conserved regions that could be useful for primer-binding?
    - Distance tree of samples based solely on output locus sequence (ie. showing it works), optionally coloured by allowed groupings 

Find and extract specified loci from one or more genome assemblies or transcriptomes
- Inputs:
    - profile Hidden Markov Model (pHMM) of the sequence to be searched for (see [Barrnap](https://github.com/tseemann/barrnap) for similar idea)
        - Alternatively, a .fasta of trusted sequences that can be used to generate a pHMM
    - Assemblies available locally or with accessions for download from public repositories
- Needs method to parse multiple hits (multi-copy loci)
- If phylogeny of sequences is input, do a 'sanity check' to see if the distance tree from the final loci sequences is similar to the input phylogeny?
- Mode to pull out pseudogenes to add to a 'decoy' database - ie. known pseudogenous barcode sequences from genomes that we don't want to assume are novel taxa
    - If sequence is similar but fails pHMM (contains frameshifts etc.), add to this? 



### Inspiration/related projects
- Ribosomal Operon Database ([ROD](https://github.com/krabberod/ROD))
    - see preprint: https://www.biorxiv.org/content/10.1101/2024.04.19.590225v1
