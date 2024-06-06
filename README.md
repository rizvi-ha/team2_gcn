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

# Running the model

### Training and Validation to Leaderboard
```
python encoding.py --path ./dataset/IND-WhoIsWho/pid_to_info_all.json --save_path ./dataset/roberta_embeddings.pkl

python build_graph.py --author_dir ./dataset/IND-WhoIsWho/train_author.json  --save_dir ./dataset/train.pkl --embeddings_dir ./dataset/roberta_embeddings.pkl --pub_dir ./dataset/IND-WhoIsWho/pid_to_info_all.json

python build_graph.py --author_dir ./dataset/IND-WhoIsWho/ind_valid_author.json --save_dir ./dataset/valid.pkl --embeddings_dir ./dataset/roberta_embeddings.pkl --pub_dir ./dataset/IND-WhoIsWho/pid_to_info_all.json

python train.py  --train_dir ./dataset/train.pkl  --test_dir ./dataset/valid.pkl --saved_dir gcn --log_name gcn-log [--usecoo] [--usecov] [--threshold 0.5]
```
`gcn/res.json` is the submission json, and `gcn-log` is the relevant log file. `[...]` are optional params.

### Final submission after training and validating on the Leaderboard

```
wget https://open-data-set.oss-cn-beijing.aliyuncs.com/oag-benchmark/kddcup-2024/IND-WhoIsWho/IND-test-public.zip
```
<UNZIP AND MOVE TO dataset/IND-test-public>
then run:
```zsh
python build_graph.py --author_dir ./dataset/IND-test-public/ind_test_author_filter_public.json --save_dir ./dataset/test.pkl --embeddings_dir ./dataset/roberta_embeddings.pkl --pub_dir ./dataset/IND-WhoIsWho/pid_to_info_all.json
```
to build `test.pkl` and then:
```zsh
python train.py  --train_dir ./dataset/train.pkl  --test_dir ./dataset/test.pkl --saved_dir gcn --log_name gcn-log [--usecoo] [--usecov] [--threshold 0.5]
```
or possibly:
```zsh
python train.py  --train_dir ./dataset/train.pkl  --eval_dir ./dataset/valid.pkl --test_dir ./dataset/test.pkl --saved_dir gcn --log_name gcn-log [--usecoo] [--usecov] [--threshold 0.5]
```
to get a final `gcn/res.json` to submit to https://www.biendata.xyz/competition/ind_kdd_2024/final-submission/
