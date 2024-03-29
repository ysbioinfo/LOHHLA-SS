## LOHHLA-SS ##
A modified version of LOHHLA for Single Sample analysis.

The official LOHHLA (https://bitbucket.org/mcgranahanlab/lohhla/src/master/LOHHLAscript.R) is designed for multiregional sampling & sequencing. There are many restrictions in the script that are uncompatible with single sample LOHHLA analysis:  
1. The name of BAM file must be sample.bam, other ways of naming such as sample.dedupped.bam, sample.sorted.bam will lead to a malformed output name.  
2. A folder BAMdir should be created for each patient, and all BAM files of this patient must be placed in this folder. If BAM files of more than two patients are placed in the same folder, LOHHLA will collapse.  
3. The original LOHHLA requires >= 2 files in the BAMdir, or it will exit. However, if you are dealing with single sample sequencing, and running without normalBAMfile, it is impossible to have >= 2 files for one patient.

We modified the LOHHLAscript.R to make it compatible with single sample analysis. As there is no requirement for multi-sample in the model of LOHHLA, there is no reason that the software cannot run on single sample.   

## NOTE ##
This is not the official distribution site for LOHHLA, just a modification to make LOHHLA compatible with single sample analysis. If you are looking for LOHHLA please go to:  
https://bitbucket.org/mcgranahanlab/lohhla/src/master/

If you use LOHHLA-SS for your analysis, be sure to cite the original LOHHLA paper:  
McGranahan, N., et al. (2017) Allele-specific HLA loss and immune escape in lung cancer evolution. Cell, 171(6), 1259-1271.

## Installation ##
Before running LOHHLA-SS, you should install the standard version of LOHHLA following the user guide in https://bitbucket.org/mcgranahanlab/lohhla/src/master/. After successful intallation, replace the LOHHLAscript.R with LOHHLAscript_SS.R.
Some notes for LOHHLA installation:
1. please use Novoalign V3 which is free for non-profitable use.
2. please use samtools 1.xxx, or the pipeline will corrupt.
3. please also install jellyfish which is not declared in LOHHLA official site
4. the picard required by LOHHLA is not a single picard command, but an old version of picard, which contains several .jar files.
## Usage ##
The parameter -BAMdir is removed from LOHHLAscript_SS.R. And a new parameter -tumorBAMfile is added. LOHHLAscript_SS.R could be run as follows:  

```
Rscript LOHHLAscript_SS.R --HLAexonLoc /path/to/HLAexonfile \
                          --HLAfastaLoc /path/to/HLAfastafile \
                          --novoDir /path/to/novoDir \
                          --gatkDir /path/to/gatkDir \
                          --CopyNumLoc /path/to/purityfile \
                          --patientId patient \
                          --outputDir /path/to/outdir \
                          --tumorBAMfile /path/to/tumorbamfile \
                          --normalBAMfile /path/to/normalbamfile \
                          --hlaPath /path/to/hlatypefile \
                          --mappingStep TRUE \
                          --minCoverageFilter 10 \
                          --fishingStep TRUE \
                          --cleanUp TRUE
```

For the explanation of result and other usage of LOHHLA, please refer to the official site.
