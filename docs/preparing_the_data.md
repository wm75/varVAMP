## Preparing your data

The input data is just an alignment of your viral sequences. To generate this from scratch, you can `cat` your FASTA sequences into one multi-FASTA file...
```shell
cat *.fasta > my_sequences.fasta
```
...and then align these sequences with e.g. [MAFFT](https://mafft.cbrc.jp/alignment/software/)
```shell
mafft my_sequences.fasta > my_alignment.fasta
```
**That's already it. Your input is ready for varVAMP!**

### BUT...
If your sequences are too diverse, also varVAMP will not perform well. Therefore, the input alignment must be phylogenetically meaningful. To analyze this you can calculate a tree with tools like [iqtree](http://www.iqtree.org/) and then use [TreeCluster](https://github.com/niemasd/TreeCluster) to get phylogenetically related sequence clusters. However, this can be also computationally intensive.

We have had good experience in using varVAMP with the sequence identity-based clustering algorithm [vsearch](https://github.com/torognes/vsearch). A good starting point is a sequence identity between 0.8 and 0.85. For such clusters varVAMP should perform reasonably well.

To do this, install vsearch and cluster your sequences via:

```shell
vsearch --cluster_fast <my_sequences.fasta> --clusters <output_dir> --id <float>
```

## You just want to test out varVAMP?

No worries, we got you! Test it with an alignment for [Hepatitis E virus](../example_data). These sequences were pre-selected with `vsearch --id 0.83` from available HepE sequences in GenBank and aligned with MAFFT! varVAMP should finish in seconds with the standard settings.


#### [Previous: Installation](./installation.md)&emsp;&emsp;[Next: Usage](./usage.md)