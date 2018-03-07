# Prerequisites

## Hardware
We have tested this software on
* Windows (Win 7 x64)
* Ubuntu 16.04 LTS.

Both systems had 16GB RAM. We have not tested other configurations.

## Software
### External tools
[Kraken](https://ccb.jhu.edu/software/kraken/), a metagenomic classifier

### Languages
The following are required:

python3 >= 3.5.2.  
R > 3.3.0.

No testing has been done with earlier versions.  It is unlikely the software will work with python 2.7.

### Python packages
The following modules which are not part of the python3 standard library are required

numpy  
scipy  
pandas  
tables  
Biopython  

On Windows systems, we used numpy+mkl windows binaries [available here](https://www.lfd.uci.edu/~gohlke/pythonlibs/)
and installed other dependencies using pip3.

## R modules
## Test data
Some test data is supplied when cloning the github repository, but some test files (including vcf files) are too large to be installed from github.
You can obtain this data as below:
```
cd testdata
wget ****
gunzip *

```
You can also do so by running the get_test_data.py script in the src/ directory.

```
cd src
python3 get_test_data.py
```