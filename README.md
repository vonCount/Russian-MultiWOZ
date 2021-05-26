# RussianMultiWOZ
We create a Russian version of the MultiWOZ benchmark.

# Data structure

# FAQ

<h2>Benchmarks</h2>
<h3>Belief Tracking</h3>
<h3>Policy Optimization</h3>
<h3>Natural Language Generation</h3>
<h3>End-to-End Modelling</h3>

# Requirements
Python 2 with pip, pytorch==0.4.1

# Quick start
In repo directory:

## Preprocessing
To download and pre-process the data run:

```python create_delex_data.py```

## Training
To train the model run:

```python train.py [--args=value]```

Some of these args include:

```
// hyperparamters for model learning
--max_epochs        : numbers of epochs
--batch_size        : numbers of turns per batch
--lr_rate           : initial learning rate
--clip              : size of clipping
--l2_norm           : l2-regularization weight
--dropout           : dropout rate
--optim             : optimization method

// network structure
--emb_size          : word vectors emedding size
--use_attn          : whether to use attention
--hid_size_enc      : size of RNN hidden cell
--hid_size_pol      : size of policy hidden output
--hid_size_dec      : size of RNN hidden cell
--cell_type         : specify RNN type
```

## Testing
To evaluate the trained model, run:

```python test.py [--args=value]```

To evaluate the outside model, run:

```python evaluate.py```

where in line 611 you need to load your generation predictions.


# Benchmark results

```
```


# References
If you use any source codes or datasets included in this toolkit in your
work, please cite the corresponding papers. The bibtex are listed below:
```

```

# License

# Bug Report
If you have found any bugs in the code, please contact: ianikitin93 at gmail dot com
