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
 ```

1. Install -> upgrade to have latest version and then install all requirements
2. Format -> to format code to "black" standard
3. Lint -> pylint is the tool, with these settings only "warnings and errors", then tell which files to look to
4. Test -> pytest is the tool with the script to run to test
