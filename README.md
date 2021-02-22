# Secure Federated Submodel Learning

# 1. General introduction

---

In this project, we build a simulation platform in Python, for testing our work on Secure Federated Submodel Learning (SFSL) which was accepted by ACM MobiCom 2020, and for comparing with Google's Federated Learning (FL)-based baselines. Two key advantages of our code framework over many existing FL codes lie in (1) the socket communication module between the cloud server and each client; and (2) the security and privacy preservation modules, such as secret sharing-based secure aggregation. In particular, these two modules are of significant importance to go from simulation to deployment, according to our deployment practice on Android, iOS, Linux, and embedded devices with Alibaba's [MNN](https://github.com/alibaba/MNN) for on-device training. Further, as an exemplary application, we use the click-through-rate (CTR) prediction task, the Deep Interest Network (DIN) model, and Taobao dataset. If you find our work and code useful, please consider citing our papers as follows:
[MobiCom Version] Chaoyue Niu, Fan Wu, Shaojie Tang, Lifeng Hua, Rongfei Jia, Chengfei Lv, Zhihua Wu, and Guihai Chen, Billion-Scale Federated Learning on Mobile Clients: A Submodel Design with Tunable Privacy, in Proc. of MobiCom, pp. 405 - 418, 2020. [[PDF](https://dl.acm.org/doi/10.1145/3372224.3419188), [Slides](https://niuchaoyue.github.io/res/ppt/MOBICOM20.pptx), [Video](https://www.youtube.com/watch?v=V1Wgqvcy-Pk&ab_channel=ACMSIGMOBILEONLINE)]
[ArXiv Version] Chaoyue Niu, Fan Wu, Shaojie Tang, Lifeng Hua, Rongfei Jia, Chengfei Lv, Zhihua Wu, and Guihai Chen, Secure Federated Submodel Learning, arXiv: 1911.02254. [[PDF](http://arxiv.org/abs/1911.02254)]
# 2. File instruction

---

## taobao_data_process/

- process raw Taobao log for centralized learning
- split training set by user for Federated Submodel Learning (FSL)

**Notes: **Our 30-day Taobao dataset cannot be released due to the restriction of Alibaba. Yet, some public datasets for CTR prediction are available from [Alimama](https://tianchi.aliyun.com/dataset/dataDetail?dataId=56), [Amazon](http://snap.stanford.edu/data/amazon/productGraph/categoryFiles/), etc. 
## plain/

- Centralized_DIN: train DIN with SGD
- FedAvg (Federated Averaging): averaging the chosen clients' full model updates with the weights being their full training set sizes  
- FedSubAvg (Federated Submodel Averaging): averaging the chosen clients' submodel updates with the weights being their relevant training set sizes

**Notes:** The implementation of DIN mainly refers to the released code of Deep Interest Evolution Network ([DIEN](https://github.com/mouna99/dien)).
## secure/

- SFL (Secure FL): FL with secure aggregation
- SFSL: FSL with tunable local differential privacy

**Notes: **Secure aggregation is based on secret sharing. The building blocks of our SFSL include Private Set Union (PSU) (that builds on Bloom filter, randomization, and secure aggregation), randomized response, and secure aggregation. 
# 3. Dependence

---

We suggest you to manage Python's enviroments and packages mainly with Anaconda and with its pip just as an alternative (i.e., if the package is not available from anaconda). The full list of packages that we use is shown as follows:
(fed) root@niuchaoyue:~# conda list
# packages in environment at /root/anaconda2/envs/fed:
#
# Name                          Version                   Build  Channel
_libgcc_mutex                 0.1                          main
_tflow_select                   2.1.0                       gpu
absl-py                           0.8.0                        py27_0
asn1crypto                     0.24.0                      py27_0
astor                               0.8.0                        py27_0
backports                       1.0                           py_2
backports.weakref          1.0.post1                 py_1
blas                                 1.0                          mkl
c-ares                              1.15.0                     h7b6447c_1001
ca-certificates                  2019.8.28               0
**certifi **                             2019.9.11               py27_0
cffi                                   1.12.3                     py27h2e261b9_0
**chardet**                           3.0.4                       py27_1003
click                                 7.0                          py27_0
**cryptography                 2.7**                         py27h1ba5d50_0
cudatoolkit                      9.2                          0
cudnn                              7.6.0                       cuda9.2_0
cupti                                9.2.148                   0
**dnspython**                      1.16.0                     py27_0
enum34                           1.1.6                       py27_1
**eventlet**                           0.25.1                    pypi_0    pypi     <pip install>
**flask**                                 1.1.1                      py_0
**flask-socketio **                 4.2.1                      py_0
funcsigs                            1.0.2                      py27_0
futures                              3.3.0                      py27_0
gast                                  0.3.2                      py_0
gmp                                  6.1.2                     h6c8ec71_1
**gmpy2 **                             2.0.8                     py27h10f8cd9_2
**greenlet**                           0.4.15                    py27h7b6447c_0
grpcio                               1.16.1                    py27hf8bcb03_1
h5py                                  2.9.0                     py27h7918eee_0
hdf5                                  1.10.4                    hb1b8bf9_0
**idna**                                  2.8                         py27_0
intel-openmp                    2019.4                   243
ipaddress                          1.0.22                     py27_0
**itsdangerous**                   1.1.0                       py27_0
**jinja2**                                2.10.1                     py27_0
**keras-applications          1.0.8**                       py_0
**keras-preprocessing       1.0.9**                       py_0
libedit                               3.1.20181209          hc058e9b_0
libffi                                  3.2.1                        hd88cf55_4
libgcc-ng                           9.1.0                       hdf63c60_0
libgfortran-ng                   7.3.0                        hdf63c60_0
libprotobuf                        3.9.2                       hd408876_0
libstdcxx-ng                       9.1.0                       hdf63c60_0
linecache2                         1.0.0                       py27_0
markdown                         3.1.1                       py27_0
**markupsafe**                      1.1.1                       py27h7b6447c_0
mkl                                    2019.4                    243
mkl-service                        2.3.0                       py27he904b0f_0
mkl_fft                               1.0.14                     py27ha843d7b_0
mkl_random                      1.1.0                       py27hd6b4f25_0
mock                                 3.0.5                       py27_0
**monotonic**                       1.5                          py_0
mpc                                   1.1.0                       h10f8cd9_1
mpfr                                  4.0.1                       hdf1c602_3
ncurses                              6.1                          he6710b0_1
numpy                               1.16.4                     py27h7e9f1db_0
numpy-base                      1.16.4                     py27hde5b4d6_0
openssl                              1.1.1d                     h7b6447c_2
**pandas                              0.24.2**                    py27he6710b0_0
pip                                     19.2.3                     py27_0
protobuf                            3.9.2                       py27he6710b0_0
pycparser                           2.19                       py27_0
**pycryptodome                 3.8.2**                      py27hb69a4c5_0
pyopenssl                          19.0.0                     py27_0
pysocks                              1.7.1                      py27_0
**python                              2.7.16**                    h9bab390_7
python-dateutil                  2.8.0                      py27_0
**python-engineio**              3.9.3                      py_0
**python-socketio**               4.3.1                      py_0
pytz                                    2019.2                   py_0
readline                              7.0                         h7b6447c_5
**requests                            **2.22.0                     py27_0
scipy                                  1.2.1                       py27h7c811a0_0
**secretsharing                    0.2.6**                     pypi_0    pypi    <pip install>
setuptools                          41.2.0                    py27_0
**six**                                      1.12.0                    py27_0
sqlite                                  3.29.0                    h7b6447c_0
tensorboard                       1.12.2                    py27he6710b0_0
tensorflow                          1.12.0                    gpu_py27h2a0f108_0
tensorflow-base                 1.12.0                    gpu_py27had579c0_0
**tensorflow-gpu                1.12.0**                   h0d30ee6_0
termcolor                           1.1.0                      py27_1
tk                                        8.6.8                      hbc83047_0
traceback2                          1.4.0                      py27_0
unittest2                             1.1.0                      py27_0
**urllib3**                                1.24.2                    py27_0
**utilitybelt**                           0.2.6                     pypi_0    pypi    <pip install>
**werkzeug **                          0.16.0                    py_0
wheel                                  0.33.6                    py27_0
zlib                                      1.2.11                    h7b6447c_3
# 4. Acknowledgement

---

We would like to sincerely thank Renjie Gu, Hongtao Lv, and Hejun Xiao, mainly for their contributions to the data processing, the socket communication, and the model compression modules. We also want to thank the edge-AI group in Taobao for great engineering support.
