## LOHHLA-singlesample ##
A modified version of LOHHLA for single sample analysis.  
The official lohhla (https://bitbucket.org/mcgranahanlab/lohhla/src/master/LOHHLAscript.R) is designed for multiregional sampling & sequencing. There are many restrictions in the script that are uncompatible with single sample LOHHLA analysis:  
1. The name of BAM file must be sample.bam, other ways of naming such as sample.dedupped.bam, sample.sorted.bam will lead to a malformed output name.  
2. A folder BAMdir should be created for each patient, and all BAM files of this patient must be placed in this folder. If BAM files of more than two patients are placed in the same folder, LOHHLA will collapse.  
3. The original LOHHLA requires >= 2 files in the BAMdir, or it will exit. However, if you are dealing with single sample sequencing, and running without normalBAMfile, it is impossible to have >= 2 files for one patient.

We modified the LOHHLAscript.R to make it compatible with single sample analysis. As there is no requirement for multi-sample in the model of LOHHLA, there is no reason that the software cannot run on single sample.   

## NOTE ##
This is not the official distribution site for LOHHLA, just a modification to make LOHHLA compatible with single sample analysis. If you are looking for LOHHLA please go to:  
https://bitbucket.org/mcgranahanlab/lohhla/src/master/

If you use lohhla-singlesample for your analysis, be sure to cite the original LOHHLA paper:  
McGranahan, N., et al. (2017) Allele-specific HLA loss and immune escape in lung cancer evolution. Cell, 171(6), 1259-1271.

## Installation ##
Before running LOHHLA-singlesample, you should install the standard version of LOHHLA following the user guide in https://bitbucket.org/mcgranahanlab/lohhla/src/master/. After successful intallation, replace the LOHHLAscript.R with LOHHLAscript_ss.R.

## Usage ##
The parameter -BAMdir is removed from LOHHLAscript_ss.R. And a new parameter -tumorBAMfile is added. LOHHLAscript_ss.R could be run as follows:  

```
Rscript LOHHLAscript_ss.R --HLAexonLoc ${HLAexonfile} \
				                  --HLAfastaLoc ${HLAfastafile} \
				                  --novoDir ${novodir} \
				                  --gatkDir ${gatkdir} \
				                  --CopyNumLoc ${purityfile} \
				                  --patientId ${sample} \
				                  --outputDir ${outdir} \
				                  --tumorBAMfile ${tumorbamfile} \
				                  --normalBAMfile ${normalbamfile} \
				                  --hlaPath ${hlatypefile} \
				                  --mappingStep TRUE \
				                  --minCoverageFilter 10 \
				                  --fishingStep TRUE \
				                  --cleanUp TRUE
```
