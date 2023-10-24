## iac_duke_course
Infrastructure as Code project for Duke's Coursera Cloud Computing course 

After having cloned the repo, cd in ./iac_duke_course.

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

1. Install -> upgrade to have latest version and then install all requirements. To build project: ```make format```
2. Format -> to format code to "black" standard.  To format code: ```make format```
3. Lint -> pylint is the tool, with these settings only "warnings and errors", then tell which files to look to. To check code: ```make lint```
4. Test -> pytest is the tool with the script to run to test. To test: ```make format```

Finally
```
make install
```
