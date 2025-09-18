# Global python3 virtual enviroment

This is a virtual enviroment for global access and use, called `virt`
The virtual enviroment is located at `/opt/virt` 

Another virtual enviroment has been created with conda, called `vconda`
The virtual enviroment is located at `~/anaconda3` 

both can only be accessed through WSL

- [python3 virtual enviroment](#virt-python3-virtual-enviroment)
- [anaconda virtual enviroment](#vconda-anaconda-virtual-enviroment)

## [VIRT]: python3 virtual enviroment

please dont use this virtual enviroment for large projects with different packages versions, if your are going to use this for Azure integrations with AI and Data science, then better use the [anaconda virtual enviroment](#vconda-anaconda-virtual-enviroment)

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

### Integration in VScode

Press `Ctrl+Shift+P` and type `>Python: Select Interpreter`.
Look for the **interpreter** in the virtual enviroment path (in my case `/opt/virt/bin/python3`)

To ensure which interpreter you are using:
```bash
(virt) mike@AVAPC:/mnt/c/Users/mike.maranon/Desktop/codes/.linux-venv$ which python
/opt/virt/bin/python
```

To check the python version:
```bash
(virt) mike@AVAPC:/mnt/c/Users/mike.maranon/Desktop/codes/.linux-venv$ python --version
Python 3.13.5
```

## [VCONDA]: anaconda virtual enviroment

this virtual enviroment is recommended for data science and AI projects, specially with Azure integrations

### activation function

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