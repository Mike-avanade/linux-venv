# Global python3/anaconda virtual enviroment

This is a virtual enviroment for global access and use, called `virt`
The virtual enviroment is located at `/opt/virt` 

Another virtual enviroment has been created with conda, called `vconda`
The virtual enviroment is located at `~/anaconda3` 

both can only be accessed through WSL

- [python3 virtual enviroment](#virt-python3-virtual-enviroment)
- [anaconda virtual enviroment](#vconda-anaconda-virtual-enviroment)
- [Package management](#package-management)
- [VScode integration](#integration-in-vscode)

## [VIRT]: python3 virtual enviroment

please dont use this virtual enviroment for large projects with different packages versions, if your are going to use this for Azure integrations with AI and Data science, then better use the [anaconda virtual enviroment](#vconda-anaconda-virtual-enviroment)

To create the virtual environment, run the following command in your terminal:
```bash
sudo python3 -m venv /opt/virt
```
This will create a new virtual environment named `virt` at `/opt/virt`.

### activation function

a custom function in `~/.bashrc` has been created to activate this virtual enviroment:

```bash
function virt() {
    source /opt/virt/bin/activate
    echo "[SYSPY] Global virtual enviroment running..."
}
```

in order to activate just type `virt` in the console:

```bash
mike@AVAPC:/mnt/c/Users/mike.maranon/Desktop/codes$ virt
[SYSPY] Global virtual enviroment running...
(virt) mike@AVAPC:/mnt/c/Users/mike.maranon/Desktop/codes$
```

## [VCONDA]: anaconda virtual enviroment

this virtual enviroment is recommended for data science and AI projects, specially with Azure integrations.

Follow those commands for anaconda instalation:
```bash
# 1. Download the latest Anaconda installer (64-bit)
wget https://repo.anaconda.com/archive/Anaconda3-latest-Linux-x86_64.sh -O ~/anaconda.sh

# 2. Make the installer executable
chmod +x ~/anaconda.sh

# 3. Run the installer
./anaconda.sh

# 4. Initialize Anaconda (adds it to PATH automatically)
source ~/.bashrc

# 5. Verify installation
conda --version
```

### Activation function

a custom function in `~/.bashrc` has been created to activate this virtual enviroment:

```bash
function vconda() {
    source ~/anaconda3/bin/activate
    echo "[CONDA] Global virtual enviroment running..."
}
```

in order to activate just type `vconda` in the console:

```bash
mike@AVAPC:/mnt/c/Users/mike.maranon/Desktop/codes$ vconda
[CONDA] Global virtual enviroment running...
(base) mike@AVAPC:/mnt/c/Users/mike.maranon/Desktop/codes$
```

## Package management

to get the list of packages: 
```bash
cd /mnt/c/Users/mike.maranon/Desktop/codes/.linux-venv 

# python3 venv
pip freeze > virt-requirements.txt

# vconda venv
conda freeze > vconda-requirements.txt
```

to install a list of delimited packages:
```bash
cd /mnt/c/Users/mike.maranon/Desktop/codes/.linux-venv 

# python3 venv
pip install -r virt-requirements.txt

# vconda venv
conda install -r vconda-requirements.txt
```

---

**Extra recommendation for conda:**
To clone a complete environment (including channels and versions), you can use:

```bash
conda env export > environment.yml
conda env create -f environment.yml
```
This is useful for sharing or reproducing complex environments.


## Integration in VScode

Press `Ctrl+Shift+P` and type `>Python: Select Interpreter`.
Look for the **interpreter** in the virtual enviroment path:

- python3: `/opt/virt/bin/python3`
- anaconda: `~/anaconda3/bin/python`

To ensure which interpreter you are using:
```bash
# python3 venv
(virt) mike@AVAPC:/mnt/c/Users/mike.maranon/Desktop/codes/.linux-venv$ which python
/opt/virt/bin/python

# vconda venv
(base) mike@AVAPC-083306703:/mnt/c/Users/mike.maranon/Desktop/codes/.linux-venv$ which conda
/home/mike/anaconda3/bin/conda
(base) mike@AVAPC-083306703:/mnt/c/Users/mike.maranon/Desktop/codes/.linux-venv$ which python
/home/mike/anaconda3/bin/python
```

To check the python version:
```bash
# python3 venv
(virt) mike@AVAPC:/mnt/c/Users/mike.maranon/Desktop/codes/.linux-venv$ python --version
Python 3.13.5

# vconda venv
(base) mike@AVAPC-083306703:/mnt/c/Users/mike.maranon/Desktop/codes/.linux-venv$ python --version
Python 3.11.7
(base) mike@AVAPC-083306703:/mnt/c/Users/mike.maranon/Desktop/codes/.linux-venv$ conda --version
conda 24.11.3
```