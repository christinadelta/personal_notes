### Steps to install the HDDM python toolbox - on Mac  

The HDDM (Hierarchical Drift Diffusion Model) is a python-based toolbox, used in Psychology and Cognitive Neuroscience to estimate 
desicion making. The developers of the toolbox suggest installing it through Anaconda because it's very straightforward, you just need 
to download and install anaconda (if you don't already have it) and then on the command line type:

    conda install -c pymc hddm 
and that's it. 
Using Anaconda with Python is a great option (especially for people working in data science), but I want to experiment with **pip** and the lightweight **virtual environments** (venv) with their own independent packages in their site directories. 
Installing hddm with pip is trickier and it leads to a lot of errors. I managed to install it a few days ago and when I ran one of the tutorials provided by the HDDM developers, everything seemed to work. So, here are the steps that I used: 

#### Step 1. Create a HDDM dedicated venv 

    python3 -m venv /path/to/env/hddm_env
activate the environment :

    source hddm_env/bin/activate 
#### Step 2. Install libraries, compilers, etc. using pip

install NumPy:

    pip install numpy 

install Cython and gfortran compiler:

    pip install Cython 
to install gfortran I used brew. I tried with:

    pip isntall gcc 
    
   but I was getting errors and searching on google led me here [web](https://github.com/pySTEPS/pysteps/issues/37). So the commands I used are:
   
    brew update 
and then:

    brew install gcc
#### Step 3. Set environment variables
Then next step was to set 2 environment variables. I don't recall where exactly I got this insight, I think I started by searching this [web](https://github.com/hddm-devs/hddm/issues/51), and that led me to the solution. Anyhow, first set the environment CFLAGS:

    export CFLAGS="-I /path/to/venv/hddm_env/lib/python3.7/site-packages/numpy/core/include $CFLAGS"

 Next, set the 2nd environment variable (again, the help came from the website listed above):

    env LDFLAGS="-L$(brew --prefix openssl)/lib" CFLAGS="-I$(brew --prefix openssl)/include" pip install git+https://github.com/hddm-devs/hddm.git

this is supposed to install hddm and the rest of the packages (pandas, kabuki etc..) using pip, but it didn't work for me. So what I did next was to install those packages one by one (as suggested at the HDDM official website: [web](http://ski.clps.brown.edu/hddm_docs/)):

    pip install pandas
    pip install kabuki
    pip install pymc 
    pip install hddm
And finally no errors!

#### Step 4. Check that HDDM works properly

Once this was done, I just had to check that hddm was installed properly so I tried one of their tutorials (see here: [web](http://ski.clps.brown.edu/hddm_docs/tutorial.html)), and everything worked smoothly without problems or errors.. 
Phew!!
