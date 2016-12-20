# neuralnets

Experimentations with Theano and TensorFlow

These scripts are run on AWS EC2 GPU "g2.2x" instance based on AMI (Ireland) :
    
    cs231n_caffe_torch7_keras_lasagne_v2 (ami-e8a1fe9b)
    
At EC2 configuration time, to setup Jupyter web I follow this tutorial :
    
    http://efavdb.com/deep-learning-with-jupyter-on-aws/
    
To re-use the same folder across multiple EC2 launches I use AWS EFS :
```
($ sudo apt-get upgrade ?)
$ sudo apt-get -y install nfs-common
($ reboot ?)
$ cd caffe
$ mkdir neuralnets
$ cd ..
$ sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2 $(curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone).YOUR_EFS_HERE.efs.YOUR_ZONE_HERE.amazonaws.com:/ caffe/neuralnets
($ clone Git repo in neuralnets directory?)
```

The EC2 AMI comes with Theano but TensorFlow needs to be installed :
```
($ sudo easy_install --upgrade pip ?)
$ pip install tensorflow
```

To run Theano script with GPU :
```
$ cd caffe/neuralnets/nb_theano
$ THEANO_FLAGS='floatX=float32,device=gpu' python dA.py
```
    
