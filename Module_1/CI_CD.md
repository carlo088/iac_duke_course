#### shh
To ssh into azureVM from my MacOS
```
ssh -i ~/Documents/azureVM/myKey.pem azureuser@13.69.50.184
```
#### When using a Virtual Code Editor
One needs to clone the repo with SSH. First create keys:
```
ssh-keygen -t rsa
```
Then get the path where the key is stored and:
```
cat /path/to/key/id_rsa.pub
```
Then copy the key. Go to GitHhub -> Profile -> Settings -> SSH ang GPG keys -> New SSH key and paste the copied key. Then go to repo, code, and copy the SSH address. Afterwards:
```
git clone $"SSH address"
```

#### venv
First create and then source a venv inside the project folder
```
python -m venv ~./iac_duke_course
source ~./iac_duke_course/bin/activate
```

#### makefile
```
install:
	pip install --upgrade pip
	pip install -r requirements.txt

format:
	black *.py

lint:
	pylint --disable=R,C hello.py

test:
	python -m pytest --vv --cov=hello test_hello.py

all: install lint test
 ```

1. Install -> upgrade to have latest version and then install all requirements. To build project: ```make install```
2. Format -> to format code to "black" standard.  To format code: ```make format```
3. Lint -> pylint is the tool, with these settings only "warnings and errors", then tell which files to look to. To check code: ```make lint```
4. Test -> pytest is the tool with the script to run to test. To test: ```make test```

#### GitHub Actions
In GitHub, select Actions and then "set up a workflow yoursel".
In ```.github/workflows/``` one will find ```main.yml```. Already has a template: whenever one pushes new code to the repo, a set of tests gets done. If one already has a ```Makefile```, this becomes trivial.
```
name: Python 3.8
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Set up Python 3.8
      uses: actions/setup-python@v1
      with:
        python-version: 3.8
    - name: Install dependencies
      run: |
        make install
    - name: Lint with Pylint
      run: |
        make lint
    - name: Test with Pytest
      run: |
        make test
    - name: Format code with Python black
      run: |
        make format
```
On every ```push```, run on ```ubuntu```, set up ```python``` and then use the ```make``` commands.

#### Azure Cloud
Azure Cloud is using a different version of python. This means that I can add to the Makefile a different install that takes a different requirements file.
```
install-azure:
	pip install --upgrade pip
	pip install -r requirements-azure.txt
 ```
Then I can also build another build for the GitHub Actions.

#### GCP Google Cloud Engine
Example of app deployed on GCP. Can access port to see the Flask App. Through GCP settings, one can connect app to GitHub repo of app code to have a Continuos Delivery. At every push on repo, trigger activates and updates app on the GCP.
