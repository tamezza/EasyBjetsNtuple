# EasyBjetsNtuple
Ntuple production for Run3

go to lpnatlas: `tamezza@lpnatlas02.in2p3.fr` in home create a folder call it for example `EasyJets`; that will be your working directory where you will clone and install `easyjet`:

```bash
cd EasyJets
git clone https://gitlab.cern.ch/croland/easyjet.git
# you will need to: mkdir build run
git checkout croland-bjes
```

Everything looks fine now its time to check the scripts for submitting jobs

```bash
cd EasyJets/easyjet/XbbCalib/datasets/data/
ls
#the data for run2 *p6490 (actually *p6467) and run3 *p6700
data_Run2_p6490.txt  data_Run3_p6700.txt

cd EasyJets/easyjet/XbbCalib/scripts/grid/
# I want to change the p-tag in Zbbj_MC as the one in Zbby, here I can open both in vim in tabular way using -p but remeber when you save the changes do `:xa`, `a` used for all
vim -p Zbbj_MC.sh Zbby.sh # are in (git)-[croland-bjes]
#I want to change a p-tag number in the all samples with a new one I can do `:%s/old-p-tag/new-p-tag/gc`then you can press `y` for one by one or just `a`for all
`:%s/old-p-tag/new-p-tag/gc`then `a`
# Also change the compaignName, usually I put the date when I am submitting the job
vim Zbbj_MC.sh compaignName="bjes_26_june"

```
