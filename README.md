Hi guys, here are some instructions on getting this running in
a console environment. You should probably be doing this in a 
Google Cloud VM as described in *week 4 discussion slides*, rather than on
your own computer.

# First time setup

### Cloning the Repo

```

git clone https://github.com/rizvi-ha/team2_gcn.git

cd team2_gcn

```

### Setting up Python environment

```

python3 -m venv venv

source venv/bin/activate

pip install -r requirements.txt

```

### Downloading the data 

```

wget https://www.dropbox.com/scl/fi/o8du146aafl3vrb87tm45/IND-WhoIsWho.zip?rlkey=cg6tbubqo532hb1ljaz70tlxe&dl=1

```

wait a min or two... then run

```

unzip IND-WhoIsWho.zip?rlkey=cg6tbubqo532hb1ljaz70tlxe

rm -rf __MACOSX

mkdir dataset

mv IND-WhoIsWho dataset

rm IND-WhoIsWho.zip?rlkey=cg6tbubqo532hb1ljaz70tlxe

rm wget-log

```

# Everytime you reopen terminal

### Pull any updates from GitHub

if there's merge conflicts or anything like that let Hassan know, but this usually should
go smoothly.

```

git pull origin

```

### Jump into the python environment

```

source venv/bin/activate

```