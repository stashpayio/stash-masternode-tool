## Building the Stash Masternode Tool executable on macOS

You can build Stash Masternode Tool for macOS by opening the Terminal app and running the following commands:

* Install *Homebrew*:

  ```
  /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
  ```

  Installation takes about 5 minutes to complete.

* Install *Python 3*:

  ```
  brew install python3
  ```

* After the installation process completes, make sure that the Python version installed is 3.6 or newer. SMT won't compile on older versions of Python, or even older versions of Python 3:

  ```
  python3 --version
  ```

  You should see a response similar to the following:

  `Python 3.6.4`

* Install *libusb*:

  ```
  brew install libusb
  ```

* Install *virtualenv*:

  ```
  pip3 install virtualenv
  ```

* Create a Python virtual environment for SMT:

  ```
  cd ~
  mkdir projects
  mkdir projects/virtualenvs
  cd projects/virtualenvs
  virtualenv -p python3 smt
  ```

* Activate the new virtual environment:

  ```
  source smt/bin/activate
  ```

* Download the SMT source from GitHub:

  ```
  cd ~/projects
  git clone https://github.com/stashpayio/stash-masternode-tool
  ```

* Install the SMT Python requirements:

  ```
  cd stash-masternode-tool
  pip install -r requirements.txt
  ```

* Build the SMT executable:

  ```
  pyinstaller --distpath=../dist/mac --workpath=../build/mac stash_masternode_tool.spec
  ```


Once the build has completed successfully, a compressed macOS executable file will be created in the ***~/projects/dist/all*** directory. An uncompressed app package (*StashMasternodeTool.app*) can be found in the ***~/projects/dist/mac*** directory.

* Troubleshooting

  If you receive this error (using PyInstaller 3.6):
  ```
  ModuleNotFoundError: No module named 'pkg_resources.py2_warn'
  ```
  This can be fixed in two different ways:

  A. By installing the latest PyInstaller from the git repo (tested with PyInstaller 4.0.dev0+g3e6f7dc7)
  ```
  pip uninstall pyinstaller
  pip install git+https://github.com/pyinstaller/pyinstaller.git
  ```
  B. By downgrading setuptools before v45.0.0 (tested with setuptools 44.1.0)
  ```
  pip install --upgrade 'setuptools<45.0.0'
  ```