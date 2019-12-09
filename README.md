# Home Credit Default Risk Prediction:  A Comparison of LightGBM & XGBoost
   Dania Etienne and Justin LoMonaco, Matthew Barta and Wesley Boyd

# Motivation
There are many consumers out there seeking loans, yet lacking the substantial credit history to easily show creditors whether or not the applicant is predictably reliable in paying back the loan. This is a problem that disproportionately affects college-aged students because they have not had an opportunity to build credit as they are just beginning their time as a young adult.  A solution to this would be to use readily available information about potential clients to create a profile of their likelihood to repay the loan based on the likelihood of previous clients with similar information. This would open up more channels of credit opportunity for those of us, like the members of this group, who might not otherwise have a chance to receive a loan due to lack of a credit history, despite being an ideal candidate to repay it back otherwise.

# Dataset
The dataset consists of 9 CSV files that together form around 2.5 gigabytes of raw data. There is an additional CSV file in the dataset used to describe the meaning of the columns of the other CSV file. There are two files, application_test and application_train, that can be used to provide a baseline for the algorithms we will use to predict the chances of a client paying back a line. In order to provide the best predictions, however, we will be using the data within the 7 other CSV files.

# Running the Project 

  1. In AWS, set the region to us-east-2, Ohio.
  2. Launch an EC2 instance with the AMI ami-054eaaeb377484366. This EC2 has Spark preconfigured.
  3. Set the instance type to t2.xlarge.
  4. Set the storage size to 16+ GB.

## SSH into the EC2 and install the following dependencies.

## S3FS
Run the following commands:
pip install s3fs
nano ~/.aws/credentials

Change the key and key ID to match your credentials

## Installing LightGBM with IPython

Run the following commands:
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

## Installing XGBoost with IPython

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

