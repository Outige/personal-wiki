# Quickstart - python

This file aims to be a quick wiki to getting started with python AWS Lambdas

---

# Creating a lambda with non out of the box dependencies

The gist is that you need to create a local folder with your lambda code and the python dependencies installed locally.

```bash
mkdir lambda-package
cd lambda-package
touch lambda_function.py # just add your custom code here
pip3 install numpy -t .
cd ..
zip lambda-package lambda-package.zip # just zip your code
```

Then you can through the Lambda console upload the zip and you're almost good to go. One catch is that you'll see `Runtime setting info > Handler info` and it'll say something like `lambda_function.lambda_handler` which basically means that the lambda is expecting you to have a `lambda_handler.py` file to be in the root dir and in that file there should be a `def lambda_handler(event, context):` method. Usually happens is that when you upload the zip your code and the dependencies will be in a folder named after the zip and so you'd either want a `Handler info` like `lambda-package.lambda_function.lambda_handler` or just move the code and dependencies to the root.

- [How to install a Python Dependency on AWS Lambda (2023)](https://www.youtube.com/watch?v=iluJFDUh-ck&t=219s): Basically just followed this tutorial.


## Psycopg2 - pyhton3.8+

It seems like some dependencies aren't as simple to install as others. That's the case for Psycopg2 (talking to a postgres db).

- Go to AWS Cloud9
- Create a new environment and open the environment and dump in the following commands
```bash
sudo amazon-linux-extras install python3.8

curl -O https://bootstrap.pypa.io/get-pip.py

python3.8 get-pip.py --user

sudo python3.8 -m pip install psycopg2-binary -t python/

zip -r dependancies.zip python

```
- Then download dependencies.zip
- Then create new Lambda layer with python3.8+ and upload the dependencies.zip to the layer
- Then go back to your lambda and add your new layer and you are good to go with importing psycopg

Resources
- [Github link to commands](https://github.com/SumeriLal/psycopg2_requests_lambda/blob/main/python_dependancies_cloud9.txt)
- [How to Install Custom Python Packages or psycopg2 in AWS Lambda Function](https://www.youtube.com/watch?v=80h9lXE07z0)
- [This is supposed to be a download to the assets but it doesn't work](../../../assets/dependancies.zip){:download="awesome-file"}
