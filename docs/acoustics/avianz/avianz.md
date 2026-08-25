# Usage
## Run AviaNZ on Waratah/SDC

1. Open MobaXterm and start an ssh session
2. Load slurm
```bash
module load slurm
```
3. Adjust AviaNZ script to your site and copy to your MobaXterm ssh session (right-click to paste -> continue -> enter)
```bash
sbatch \
--job-name=WEB1_avianz \
--mail-user={EMAIL}@dcceew.nsw.gov.au \
/mnt/scratch_lustre/ww_wbfa_scratch/scripts/avianz.sh \
-d /mnt/scratch_lustre/ww_wbfa_scratch/data/acoustic_data/uploads/Murrumbidgee/202526 \
-s WEB1 \
-m 8 -M 10 \
-t 17 -T 23 \
-r Southern_Bell_Frog_GV_130125 \
-c 5
```
Details:  
--job-name (Name of job on Waratah - emails will reference this job name)  
--mail-user (Where slurm emails go when script: Begins, Fails, or Completes)  
/mnt/scratch_lustre/ww_wbfa_scratch/scripts/avianz.sh (script location - don't change)  
-d (directory with site folder in it)  
-s (site folder)  
-m (start month of interest - 8 = August)  
-M (end month of interest - 10 = October)  
-t (start time - 17 = 5pm)  
-T (end time - 07 = 7am)  
-r (recogniser name saved in recoginsers folder)   
-c (clip duration - 5 = first 5mins of file)  


## Retrieve AviaNZ files from Waratah
1. Login to remote PC - Use instead of your laptop because it has faster internet and will keep running if you close down your laptop
2. Open MobaXterm and a bash terminal - [Download](https://mobaxterm.mobatek.net/download-home-edition.html) the portable edition of MobaXterm which has the necessary plugins for using the bash terminal
3. Adjust rsync script:
    - USERNAME (replace with Waratah username)
    - HOSTNAME (replace with Waratah Host name sdclogin...)
    - filepaths (Currently this will copy the NIM1 folder to the 05_2025-26 folder on the m drive)
```bash
rsync -av --progress --no-times --no-perms -e ssh {USERNAME}@{HOSTNAME}:/mnt/scratch_lustre/ww_wbfa_scratch/data/avianz/processed/NIM1 "/drives/m/themes/wetlands/EFlowMonitoring/Murrumbidgee/40_FrogData/02_Audio/data/05_2025-26/"
```