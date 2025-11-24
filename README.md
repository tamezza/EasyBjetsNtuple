# EasyBjetsNtuple

## Ntuple production for Run3

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
#the data for run2 *p6490 (actually *p6467) and run3 *p7019
data_Run2_p6490.txt  data_Run3_p7019.txt

Then go to:

cd EasyJets/easyjet/XbbCalib/scripts/grid/

# I want to change the p-tag in Zbbj_MC as the one in Zbby, here I can open both in vim in tabular way using -p but remeber when you save the changes do `:xa`, `a` used for all
vim -p Zbbj_MC.sh Zbby.sh # are in (git)-[croland-bjes]

#I want to change a p-tag number in the all samples with a new one I can do `:%s/old-p-tag/new-p-tag/gc`then you can press `y` for one by one or just `a`for all
`:%s/old-p-tag/new-p-tag/gc`then `a`

cd easyjet/XbbCalib/share/

# Also change the compaignName in the `confg-file`, usually I put the date when I am submitting the job
vim Zbbj_data_run3.sh compaignName="bjes_18Nov2025_NoMuon"

```

for `MuonInJet` the only change we have to do with respect using the `bJR00v00/01` is to change the `confg-file` to include muons `do_muons: true` and make sure to make the compaignName different from 
the one we used in the bJR00v00/01, otherwise when we submit it will consider we submitting the same

```bash
cd easyjet/XbbCalib/share/

# Change the `confg-file` to include muons
vim RunConfig_Zbbj-MC.yaml
In large_R_jet: 'runMuonJetPtCorr: true'

# Change compaignName
cd EasyJets/easyjet/XbbCalib/scripts/grid/
vim Zbbj_MC.sh compaignName="bjes_26_june_mu_corr"

```

Once we did all necessary Modification/editions its time to setup easyjet and submit the job

```bash

cd /EasyJets/easyjet
setupATLAS
cd ../build
source ../easyjet/setup.sh
cmake ../easyjet/
make -j4
source */setup.sh
cd ..
cd run
lsetup pyamivms
vms
lsetup panda
source ../easyjet/XbbCalib/scripts/grid/Zbbj_data_run3.sh

```

## easyjet_ntuples
The created ntuples by easyjet are downloaded and stored in `easyjet_ntuples`

```bash
#/data/atlas/tamezza/BJetCalib_Run3/easyjet_ntuples

cd Zbbj_bjes_22Nov2025
rucio list-dids "user.tamezza.bjes_22Nov2025_NoMuon.700855.%TREE" | awk '{print $2}' > list_zbbj.txt
cat list_zbbj.txt
vim list_zbbj.txt
rucio download `cat list_zbbj.txt`

cd Dijets_bjes_22Nov2025
rucio list-dids "user.tamezza.bjes_22Nov2025_NoMuon.8011%TREE" | awk '{print $2}' > list_dijets.txt
cat list_dijets.txt
vim list_dijets.txt
rucio download `cat list_dijets.txt`

cd Data_bjes_22Nov2025
rucio list-dids "user.tamezza.bjes_22Nov2025_NoMuon.data%TREE" | awk '{print $2}' > list_data.txt
cat list_data.txt
vim list_data.txt
rucio download `cat list_data.txt`
```

## Ntuplesource ../easyjet/XbbCalib/scripts/grid/Zbbj_DATA_run3.sh
 Post-Processing for Run3









