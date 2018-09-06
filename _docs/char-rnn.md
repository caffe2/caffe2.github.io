---
docid: char-rnn
title: RNNs and LSTM Networks
layout: docs
permalink: /docs/RNNs-and-LSTM-networks.html
---

**Code:** [char_rnn.py](https://github.com/pytorch/pytorch/blob/master/caffe2/python/examples/char_rnn.py)

Are you interested in creating a chat bot or doing language processing with Deep Learning? This tutorial will show you one of [Caffe2's example Python scripts](https://github.com/pytorch/pytorch/tree/master/caffe2/python/examples) that you can run out of the box and modify to start you project from using a working Recurrent Neural Network (RNN). This particular RNN is a Long Short Term Memory (LSTM) network, where the network is capable of learning and maintaining a memory overtime while showing gradual improvement. For more information, you might want to [check out A. Karpathy's blog](http://karpathy.github.io/2015/05/21/rnn-effectiveness/) and his [RNN project](https://github.com/karpathy/char-rnn), the inspiration for this Caffe2 variation of the code he posted. It goes into further technical detail with some great animations and examples.

What's fascinating about this script is that you can throw a variety of data sources at, like the works of Shakespeare, and not only will it "learn" English, grammar, and spelling, it will also pick up on the nuances of structure and prose used in his works. Likewise you can feed it speeches from Obama, and while the output might sound like typical political rhetoric from a 3AM C-SPAN filibuster, you'll spot a familiar cadence and rhythm that you can almost hear in the nearly intelligible words.

Fed source code, it will learn that language's structure and mimic code that, while may not compile, at first glance seems reasonable.

Grab and combine sources from the [Project Gutenburg](https://www.gutenberg.org/) of ancient cookbooks and create an AI that spits out recipes reminiscent of feasts from The Game of Thrones. Feed it even larger sets of data and see what unique creations might be born from your own LSTM network.

## Usage Example - Shakespeare

First you'll want to [download some Shakespeare](../static/datasets/shakespeare.txt) as your training data. Save this right in the `/caffe2_root/caffe2/python/examples` directory.

Then run the script, passing in the shakespeare.txt file as an argument for `--train_data` and sit back for a bit.

```bash
python char_rnn.py --train_data shakespeare.txt
```

Output will be something like this initially:

```
---------- Iteration 5500 ----------
Bonge adpold,
Youre on, of your ins encisgath no housr the hould:
go restibless.

OTNOUS:
Ot of your vese the hisghts ank our he wirmshe so ir demand!
If lorst in and envire lake's Remans a weaker your with a am do entice, I his still.

DEBUG:char_rnn:Loss since last report: 48.8397690892
DEBUG:char_rnn:Smooth loss: 50.3314862722
Characters Per Second: 8379
Iterations Per Second: 335
```

As you let it run for a while, it will eventually begin to form into real words and understandable sentences. Let it run while we check out some other parameters.

### Using Your GPU and the Other Options

If you have a GPU on your computer then try out the setting for that by adding `--gpu`.

```bash
python char_rnn.py --train_data shakespeare.txt --gpu
```

You may also want to adjust some of the other optional parameters to increase performance or the effect of the training.

* `--gpu`: enables the network to utilize GPU resources, massively increasing the speed of training (or learning)
* `--seq_length`: this is the number of characters in one continuous sequence that are grabbed from the training data and passed into the network; defaults to 25
* `--batch_size`: defaults to 1
* `--iters_to_report`: this is how often the scripts provides a little output to show it's current status; defaults to 500
* `--hidden_size`: this is the size of the neural network's hidden layer; defaults to 100



### Meanwhile What's Cleopatra Doing?

Even after just a few minutes you can see changes in the output that are getting close to Shakespeare, or English at least, with a sort of screenplay structure. You can see in the output below that we're at the 184,000 iteration of the network. The loss has dropped from around 50% when we first started, down to 35% quite quickly.

```
---------- Iteration 184000 ----------
Lent parture there are do, brother's chawne
A father would conquer I will my seem.

Second Vreture aporier service the sidgethines, when the blood lie without again toediers
So be would be offers' true yaunder,,
And I will onseling say?

CLEOPATRA:
When he do. Tyouth from whell?

DEBUG:char_rnn:Loss since last report: 35.090320313
DEBUG:char_rnn:Smooth loss: 35.1464676378
Characters Per Second: 8267
Iterations Per Second: 330
```

### Example Parameter Changes

Here's another example of running the RNN for about 10 minutes, but increasing the `batch_size` to 32, the `hidden_size` to 512, and the `seq_length` to 32. Note how the screenplay format is evident, with names and dialogue after, and the loss is now 23%.

```
python char_rnn.py --train_data shakespeare.txt --gpu --batch_size 32 --hidden_size 512 --seq_length 32

---------- Iteration 26000 ----------
;
Of chave you the tixle, and to yo as my son, Brenis a fair,

DUKE EINIOR:
Who kous! I dre. Shall with thee,
The malice and tongue Guilty of it owed by thee
That teaching the heavier fates of death of grace
As I chid the poor hair to kiss our field;
Meat thou before the seven blow with letters out,
And turn my virtues are ourselves; there are ye dead;
And melted legs contracted in such ones,
Some beer whose aim must be supposed both blind.

ISABELLA:
A warrior of the sway.

SIR HUGH EVANS:
For a
DEBUG:char_rnn:Loss since last report: 0.254487129331
DEBUG:char_rnn:Smooth loss: 0.232923667422
Characters Per Second: 32311
Iterations Per Second: 31
```

### Notes

When acquiring data sources for this script, try to get all plain ASCII text rather than UTF-8 or other formats if you want it to run out of the box. Otherwise, you're going to need to preprocess it or modify the script to handle the different formats.
