# debian_based_setup
This is how I setup my computer for bioinformatics and personal usage.
I really like [Willi Mutschler's guides](https://mutschler.eu/linux/install-guides/]

Current: Pop!_OS 20.04 LTS 5.4.0-7642-generic (NVIDIA)

## [zsh](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH) + [Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh) + [spaceship](https://github.com/denysdovhan/spaceship-prompt) 
then I increase the history size and ignore command duplications
```
export HISTFILESIZE=1000000000
export HISTSIZE=1000000000
setopt HIST_IGNORE_ALL_DUPS
```

## Install Java Development Kit builds
```
sudo apt install default-jre default-jdk

java -version
```

## Install media codecs and addons
```
sudo apt install ubuntu-restricted-extras
sudo apt install ubuntu-restricted-addons
sudo apt install vlc
```

## Intel(R) Graphics Compute Runtime for OpenCL(TM) drivers
```
sudo apt install intel-opencl-icd
```
## NVidia_GTX_1050 driver (for Ubuntu)
```
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update
sudo apt install nvidia-driver-XXX  #current 455.28
sudo reboot
```
if Ubuntu freezes after installation, try the solution of [Mari Linhares](https://gist.github.com/mari-linhares/cef4cb3440408e44963d1447a7db5ae0)

## Installing R (current 3.6.1)
```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
sudo add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/'
sudo apt update
sudo apt install r-base r-base-dev
```

Installing packages and dependencies for genetic analyses on Ubuntu 18.04, recomended by [Grunwald lab](https://grunwaldlab.github.io/)
```
sudo apt install build-essential libcurl4-gnutls-dev libxml2-dev libssl-dev
```

[*units* package - r-quantities](https://github.com/r-quantities/units)
```
sudo apt install libudunits2-dev
```
[*sf* package - r-spatial](https://github.com/r-spatial/sf)
```
sudo add-apt-repository ppa:ubuntugis/ubuntugis-unstable
sudo apt update
sudo apt install libgdal-dev libgeos-dev libproj-dev 

```
Installing packages

Install *devtools* and *bioconductor* packages
```
sudo -i R
install.packages("devtools")
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install() #for package installation 
install.packages('units')
install.packages('sf')
# After installing this packages, other dependencies will be installed automatically.
install.packages('adegenet')
require(devtools)
devtools::install_github(repo = "grunwaldlab/poppr", build_vignettes = TRUE)
install_github("dwinter/mmod")
```

Download RStudio (IDE)
```
cd ~/Downloads
sudo gdebi rstudio-XXX.deb
```
## Install VCFTools
```
git clone https://github.com/vcftools/vcftools.git
cd vcftools
./autogen.sh
./configure
make
make install
```

## install ANGSD: Analysis of next generation Sequencing Data 
```
wget http://popgen.dk/software/download/angsd/angsd0.930.tar.gz
tar xf angsd0.930.tar.gz 
cd htslib/;make;cd ..
cd angsd/
make HTSSRC=../htslib
```

## Install iPyrad
Follow the instructions at [iPyrad.docs](https://ipyrad.readthedocs.io/en/latest/3-installation.html).

## Install Stacks
Download [Stacks](http://catchenlab.life.illinois.edu/stacks/) and extract.
```
tar xfvz stacks-2.xx.tar.gz
cd stacks-2.xx
./configure
make -j 8 #number of processors available 
sudo make install

```
## Install samtools, bcftools and htslib (following [Biostars](https://www.biostars.org/p/328831/) tutorial)

```
sudo apt update
sudo apt install gcc
sudo apt install make libbz2-dev zlib1g-dev libncurses5-dev libncursesw5-dev liblzma-dev

```
# Install HTSLIB
```
git clone https://github.com/samtools/htslib.git
cd htslib
git submodule update --init --recursive
autoreconf -i
./configure
make
sudo make install
```
# Install SAMTOOLS
```
wget https://github.com/samtools/samtools/releases/download/1.9/samtools-1.9.tar.bz2
tar -vxjf samtools-1.9.tar.bz2
cd samtools-1.9
make
```
# Install BCFTools
```
cd ..
wget https://github.com/samtools/bcftools/releases/download/1.9/bcftools-1.9.tar.bz2
tar -vxjf bcftools-1.9.tar.bz2
cd bcftools-1.9
make
```
```
Export To Path And Refresh
export PATH="$PATH:/usr/bin/bcftools-1.9"
export PATH="$PATH:/usr/bin/samtools-1.9"
export PATH="$PATH:/usr/bin/htslib-1.9"
source ~/.profile
```

## Install [VSEARCH](https://github.com/torognes/vsearch)
```
wget https://github.com/torognes/vsearch/archive/vXXXXXXXX.tar.gz
tar xzf vXXXXXXXX.tar.gz
cd vsearch-vXXXXXXXX
./autogen.sh
./configure
make
make install  # as root or sudo make install
```

## Install QGIS LTR 
```
sudo sh -c 'echo "deb http://qgis.org/ubuntu-ltr bionic main" >> /etc/apt/sources.list'
sudo sh -c 'echo "deb-src http://qgis.org/ubuntu-ltr bionic main" >> /etc/apt/sources.list'

wget -O - https://qgis.org/downloads/qgis-2019.gpg.key | gpg --import
gpg --fingerprint 51F523511C7028C3
gpg --export --armor 51F523511C7028C3 | sudo apt-key add -

sudo apt update
sudo apt install qgis qgis-plugin-grass

```

## Install Zotero reference manager

Download [Zotero](https://www.zotero.org/download/) and extract.

```
sudo mv Zotero_linux-x86_64 /opt
sudo ln -s /opt/Zotero_linux-x86_64/zotero /usr/bin/zotero
sudo add-apt-repository ppa:smathot/cogscinl
sudo apt update 

```
To add Zotero on Applications tab
```
sudo ln -s /opt/Zotero-5.0.76_linux-x86_64/Zotero_linux-x86_64/zotero.desktop /usr/share/applications/zotero.desktop

```
Open as root
```
sudo zotero
```
# to install [qnotero](http://www.cogsci.nl/qnotero)

## Install Tweak tools for  
```
sudo add-apt-repository universe
sudo apt install gnome-tweak-tool
```
## themes
```
apt search arc-theme
sudo apt install arc-theme 
sudo add-apt-repository ppa:papirus/papirus
sudo apt install papirus-icon-theme 
```


# Install Steam from official package
```
sudo dpkg --add-architecture i386
sudo apt update
sudo apt install wget gdebi-core libgl1-mesa-dri:i386 libgl1-mesa-glx:i386
wget http://media.steampowered.com/client/installer/steam.deb
sudo gdebi steam.deb
```

## Install programs via Snap
> Skype, spotify, whatsapp.desktop, Discord, etc.. check the list.

# Install Visual Studio Code
```
sudo apt install code

```

