# Home Credit Default Risk Prediction:  A Comparison of LightGBM & XGBoost
   Dania Etienne, Justin LoMonaco, Matthew Barta, and Wesley Boyd

# Motivation
There are many consumers out there seeking loans, yet lacking the substantial credit history to easily show creditors whether or not the applicant is predictably reliable in paying back the loan. This is a problem that disproportionately affects college-aged students because they have not had an opportunity to build credit as they are just beginning their time as a young adult.  A solution to this would be to use readily available information about potential clients to create a profile of their likelihood to repay the loan based on the likelihood of previous clients with similar information. This would open up more channels of credit opportunity for those of us, like the members of this group, who might not otherwise have a chance to receive a loan due to lack of a credit history, despite being an ideal candidate to repay it back otherwise.

# Dataset
The dataset consists of 9 CSV files that together form around 2.5 gigabytes of raw data. There is an additional CSV file in the dataset used to describe the meaning of the columns of the other CSV file. There are two files, application_test and application_train, that can be used to provide a baseline for the algorithms we will use to predict the chances of a client paying back a line. In order to provide the best predictions, however, we will be using the data within the 7 other CSV files.

# Running the Project 

  1. In AWS, set the region to us-east-2, Ohio.
  2. Launch an EC2 instance with the AMI ami-054eaaeb377484366. This EC2 has Spark preconfigured.
  3. Set the instance type to t2.xlarge.
  4. Set the storage size to 16+ GB.
  
  5. Install scala using the following command:
  ```
  sudo apt-get install python scala ipython -y
  ```
   
  6. Install spark with the following commands:
  ```
      wget http://archive.apache.org/dist/spark/spark-2.2.0/spark-2.2.0-bin-hadoop2.7.tgz
      tar -zxvf spark-2.2.0-bin-hadoop2.7.tgz
   ```
   
  7. Open ~/.profile and append the following lines:
  ```
   export SPARK_HOME='/home/ubuntu/spark-2.2.0-bin-hadoop2.7'
   export PATH=$SPARK_HOME:$PATH
   export PYTHONPATH=$SPARK_HOME/python:$PYTHONPATH
  ```
   
  8. Run the following command:
  ```
   source ~/.profile
   wget https://repo.continuum.io/archive/Anaconda3-4.2.0-Linux-x86_64.sh
   bash Anaconda3-4.2.0-Linux-x86_64.sh
   which python /usr/bin/python
   source .bashrc
  ```
   
  8. Open ipython and run the following commands: 
  ```
  from IPython.lib import passwd
  passwd()
  ```
  
  9. Exit and run the following commands:
  ```
   jupyter notebook --generate-config 
   mkdir certs 
   cd certs 
   sudo openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem 
   cd ~/.jupyter/
   ```
   
  10. Open jupyter_notebook_config.py and append the following lines to the start of the file:
  ```
     c = get_config()

     # Kernel config
     c.IPKernelApp.pylab = 'inline'
     # if you want plotting support always in your notebook# Notebook config
     c.NotebookApp.certfile = u'/home/ubuntu/certs/mycert.pem'
     #location of your certificate file
     # Set ip to '*' to bind on all interfaces (ips) for the public server
     c.NotebookApp.ip = '*'
     c.NotebookApp.open_browser = False
     #so that the ipython notebook does not opens up a browser by default
     c.NotebookApp.password = u'YOUR JUPYTER NOTEBOOK PASSWORD'
     #the encrypted password we generated above
     # It is a good idea to put it on a known, fixed port
     c.NotebookApp.port = 8888”
  ```
  
  11. Exit and run the following commands:
  ```
      echo "export PATH=$PATH:/home/ubuntu/spark-2.2.0-bin-hadoop2.7" >> ~/.profile
      echo "export PYSPARK_DRIVER_PYTHON=ipython" >> ~/.profile
      echo "export PYSPARK_DRIVER_PYTHON_OPTS='notebook' pyspark" >> ~/.profile
      source ~/.profile
   ```
   
  12. Type pyspark to open up the ipython notebook

## SSH into the EC2 and install the following dependencies.

## S3FS
Run the following commands:
```
pip install s3fs
nano ~/.aws/credentials
```

Change the key and key ID to match your credentials


## Installing LightGBM with IPython

```
sudo apt install cmake
git clone --recursive https://github.com/microsoft/LightGBM
cd LightGBM
mkdir build
cd build
cmake -DUSE_OPENMP=OFF ..
make -j4
cd ../python-package
python setup.py install
pip install setuptools wheel numpy scipy scikit-learn -U
conda update scikit-learn
```

## Installing XGBoost with IPython

```
git clone --recursive https://github.com/dmlc/xgboost
cd xgboost
mkdir build
cd build
cmake ..
cd ..
make -j4
cd ~
export PYTHONPATH=~/xgboost/python-package
conda update pandas
```

