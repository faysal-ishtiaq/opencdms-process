OpenCDMS Process library
========================
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) [![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
<!--
[![](https://img.shields.io/pypi/v/opencdms.svg)](https://pypi.python.org/pypi/opencdms) [![Travis-CI Build](https://img.shields.io/travis/opencdms/pyopencdms.svg)](https://travis-ci.com/opencdms/pyopencdms) [![Documentation Status](https://readthedocs.org/projects/opencdms/badge/?version=latest)](https://opencdms.readthedocs.io/en/latest/?badge=latest) [![Updates](https://pyup.io/repos/github/opencdms/opencdms/shield.svg)](https://pyup.io/repos/github/opencdms/opencdms/)
-->
## Overview

`opencdms.process` has dependencies on external R libraries. The development may also include dependencies running on node.js to allow the same JavaScript validation code to be executed the browser and also on the server. If a user does not have the necessary dependencies then useful error messages should be provided.

## Example

### Create a virtual environment for OpenCDMS development

These instructions are for Debian/Ubuntu Linux. At the time of writing
(October 2020) only Ubuntu 18.04 is supported. If you run into problems then
please raise a [new issue](https://github.com/opencdms/opencdms-process/issues/new).

```
# Create a directory for the project from user's home directory (~)
mkdir -p ~/opencdms/processes
cd ~/opencdms/processes

# Clone opencdms-process, pyopencdms and opencdms-test-data
git clone https://github.com/opencdms/opencdms-process.git
git clone https://github.com/opencdms/pyopencdms.git
git clone https://github.com/opencdms/opencdms-test-data.git

# Create a virtual environment for installing Python dependencies
python3 -m venv opencdms-env

# Activate the virtual environment (the leading `.` is equivalent to `source`)
. opencdms-env/bin/activate

# Install dependencies used by `opencdms-process` and `pyopencdms`
pip3 install -r ~/opencdms/processes/git/opencdms-process/requirements.txt
pip3 install -r ~/opencdms/processes/git/pyopencdms/requirements.txt
pip3 install -r ~/opencdms/processes/git/pyopencdms/requirements_dev.txt

# Add `opencdms` to the virtual environment's python path
# If you used the system's `python3` to create the virtualenv then this will likely
# be `python3.6` on Ubuntu 18.04 and `python3.7` on Ubunutu 20.04
echo $HOME"/opencdms/processes/git/pyopencdms/" > opencdms-env/lib/python3.6/site-packages/opencdms.pth

```

### Example python commands

```
import os
from pathlib import Path

from opencdms import MidasOpen

# Instead of using a database connection string, the MIDAS Open
# provider requires the root directory for the MIDAS Open data.
connection = os.path.join(
    Path.home(), 'opencdms-dev', 'git', 'opencdms-test-data')

# All instances of CDMS Providers act as an active session
session = MidasOpen(connection)

filters = {
    'src_id': 838,
    'period': 'hourly',
    'year': 1991,
    'elements': ['wind_speed', 'wind_direction'],
}

# Get observations using filters
obs = session.obs(**filters)

# Save observations to CSV file
obs.to_csv('example_observations.csv')

```

<!--
  * Free software: MIT license
  * Documentation: https://opencdms.readthedocs.io.

  Features
  --------
  * TODO
-->
