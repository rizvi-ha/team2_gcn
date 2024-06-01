# GCN 

## Running Steps

``` 
python encoding.py --path your_pub_dir --save_path embedding_save_path

python build_graph.py --author_dir train_author_path --pub_dir your_pub_dir --save_dir save_path --embeddings_dir embedding_save_path

python build_graph.py --author_dir test_author_path --pub_dir your_pub_dir --save_dir save_path --embeddings_dir embedding_save_path

python train.py --train_dir train.pkl --test_dir valid.pkl
```

- build_graph.py and encoding.py in GCN and GCCAD are the same

## Running Steps Specific to us

```
python encoding.py --path ./dataset/IND-WhoIsWho/pid_to_info_all.json --save_path ./dataset/roberta_embeddings.pkl

python build_graph.py --author_dir ./dataset/IND-WhoIsWho/train_author.json  --save_dir ./dataset/train.pkl --embeddings_dir ./dataset/roberta_embeddings.pkl --pub_dir ./dataset/IND-WhoIsWho/pid_to_info_all.json

python build_graph.py --author_dir ./dataset/IND-WhoIsWho/ind_valid_author.json --save_dir ./dataset/valid.pkl --embeddings_dir ./dataset/roberta_embeddings.pkl --pub_dir ./dataset/IND-WhoIsWho/pid_to_info_all.json

python train.py  --train_dir ./dataset/train.pkl  --test_dir ./dataset/valid.pkl --saved_dir gcn --log_name gcn-log [--usecoo] [--usecov] [--threshold 0.5]
```
