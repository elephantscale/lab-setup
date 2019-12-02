# Setting up Spark-ML environment


## Step 1: Access your VM
Instructor will provide details.  
You can access the VM by IP address using a browser.

## Step 2: Access Jupyter Labs page
Click on Jupyter 'Access'.  
You should see a running instance of Jupyter Lab

## Step 3: Open `Terminal` in Jupyter Lab
This would give you access to shell access to the VM

## Step 4: Install Spark
```bash
$   cd
$   wget https://archive.apache.org/dist/spark/spark-2.3.0/spark-2.3.0-bin-hadoop2.7.tgz
$   rm -rf  spark   # cleanup existing spark installation (if any)
$   tar xvf   spark-2.3.0-bin-hadoop2.7.tgz
$   mv  spark-2.3.0-bin-hadoop2.7    spark
```

## Step 5: Get the labs

```bash
$   git clone  git@github.com:elephantscale/spark-labs.git

```

## Step 6: Get the data

```bash
$  cd ~/data;  git pull;   cd
```

## Step 7: Open `Readme.ipynb` file
- In Jupyter Labs, navigate to `spark-labs`  directory
- and open `README.ipynb`




```python
 
```
