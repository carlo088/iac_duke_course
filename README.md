# iac_duke_course
Infrastructure as Code project for Duke's Coursera Cloud Computing course 

After having cloned the repo, cd in ./iac_duke_course.

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
