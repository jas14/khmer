.. vim: set filetype=rst

=======================================
Blog posts and additional documentation
=======================================

Hashtable and filtering
=======================

The basic inexact-matching approach used by the hashtable code is
described in this blog post:

   http://ivory.idyll.org/blog/jul-10/kmer-filtering

A test data set (soil metagenomics, 88m reads, 10gb) is here:

   http://angus.ged.msu.edu.s3.amazonaws.com/88m-reads.fa.gz

Illumina read abundance profiles
================================

khmer can be used to look at systematic variations in k-mer statistics
across Illumina reads; see, for example, this blog post:

   http://ivory.idyll.org/blog/jul-10/illumina-read-phenomenology

The `fasta-to-abundance-hist
<http://github.com/ctb/khmer/blob/master/sandbox/fasta-to-abundance-hist.py>`__
and `abundance-hist-by-position
<http://github.com/ctb/khmer/blob/master/sandbox/abundance-hist-by-position.py>`__
scripts can be used to generate the k-mer abundance profile data, after
loading all the k-mer counts into a .ct file::

   # first, load all the k-mer counts:
   load-into-counting.py -k 20 -x 1e7 25k.ct data/25k.fq.gz

   # then, build the '.freq' file that contains all of the counts by position
   python sandbox/fasta-to-abundance-hist.py 25k.ct data/25k.fq.gz

   # sum across positions.
   python sandbox/abundance-hist-by-position.py data/25k.fq.gz.freq > out.dist

The hashtable method 'dump_kmers_by_abundance' can be used to dump
high abundance k-mers, but we don't have a script handy to do that yet.

You can assess high/low abundance k-mer distributions with the
`hi-lo-abundance-by-position script <http://github.com/ctb/khmer/blob/master/sandbox/hi-lo-abundance-by-position.py>`__::

   load-into-counting.py -k 20 25k.ct data/25k.fq.gz
   python sandbox/hi-lo-abundance-by-position.py 25k.ct data/25k.fq.gz

This will produce two output files, <filename>.pos.abund=1 and
<filename>.pos.abund=255.
