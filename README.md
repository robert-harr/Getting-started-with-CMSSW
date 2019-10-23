# Getting-started-with-CMSSW
Documenting my setup to run analysis code.

See https://uscms.org/uscms_at_work/physics/computing/getstarted/index.shtml for basic information on accounts and logging in to cms-lpc nodes.  Basic information about CERN lxplus accounts and logins is found in the Workbook https://twiki.cern.ch/twiki/bin/view/CMSPublic/WorkBook.

At the LPC, first need to source the CMS setup (not needed on lxplus).  
```
source /cvmfs/cms.cern.ch/cmsset_default.sh
voms-proxy-init --rfc --voms cms
```
I added this to my .bash_profile so it will execute automatically on login (I hope).

Every so often one needs to update the certificate in order to have access to data.  The certificates are stored in the ~/.globus directory.

Next setup a release in the nobackup directory.  The recommended default release at the time is CMSSW_9_3_2.
```
cd nobackup
cmsrel CMSSW_9_4_6_patch1
cd CMSSW_9_4_6_patch1/src
cmsenv
```
Now we are supposed to have the required pieces to build an executable in this release.  Time to get some code.
I am starting with Nabin's code to look at H->cc events and see what passes the L1 ditau trigger.  I need Nabin's code and the jet tooolbox code.  Then use scram to build the code.
```
git clone https://github.com/nabinpoudyal3/Dhadron.git hTocc/Dhadron
git clone https://github.com/cms-jet/JetToolbox.git JMEAnalysis/JetToolbox -b jetToolbox_94X_v4
scram b -j 18
```
After successful compilattion this is run with the command
```
cmsRun hTocc/Dhadron/test/reCluster_cfg.py
```
This will run over the file specified by default, presently a file that Nabin copied to his nobackup area.

Now try the whole thing again but with CMSSW_10_2_14.
