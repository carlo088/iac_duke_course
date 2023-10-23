# iac_duke_course
Infrastructure as Code project for Duke's Coursera Cloud Computing course 





### Makefil

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
