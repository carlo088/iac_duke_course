## iac_duke_course
Infrastructure as Code project for Duke's Coursera Cloud Computing course 

After having cloned the repo, ```cd in iac_duke_course```.

#### shh
To ssh into azureVM from my MacOS
```
ssh -i ~/Documents/azureVM/myKey.pem azureuser@13.69.50.184
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
In ```.github/workflows/``` one will find ```main.yml". Already hae a template: whenever one pushes new code to the repo, a set of tests gets done. If one already has a ```Makefile```, this becomes trivial.
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
On every ```push```, run on ```ubunt```u, set up ```python``` and then use the ```make``` commands
