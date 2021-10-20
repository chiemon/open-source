apt-get install  libboost-all-dev liblmdb-dev libatlas-base-dev libhdf5-serial-dev libleveldb-dev libsnappy-dev

for req in $(cat requirements.txt) pydot; do pip install $req; done

cmake -DBUILD_python=ON \
    -DBUILD_docs=OFF \
    -DPYTHON_LIBRARIES=/anaconda3/envs/caffe-1.0/lib \
    -DPYTHON_INCLUDE_DIR=/anaconda3/envs/caffe-1.0/include/python3.8 \
    -DPYTHON_EXECUTABLE=/anaconda3/envs/caffe-1.0/bin/python ..

make all -j$(nproc)

make pycaffe -j$(nproc)

make test

make runtest

cd caffe/python
pwd > /anaconda3/envs/caffe-1.0/lib/python3.8/site-packages/caffe.pth

python -c "import sys;sys.path.append('/workspace/local/caffe-1.0/python');import caffe;from caffe import layers as L;from caffe import params as P;print(caffe.__version__, caffe.__file__)"
or
python -c "import caffe;from caffe import layers as L;from caffe import params as P;print(caffe.__version__, caffe.__file__)"

Error: libboost_python.so: undefined reference to `PyClass_Type

cd /usr/lib/x86_64-linux-gnu/
unlink libboost_python.so
ln -s libboost_python-py35.so libboost_python.so


cmake -DBUILD_python=ON \
    -DBUILD_docs=OFF \
    -DPYTHON_LIBRARIES=/anaconda3/envs/caffe-ssd/lib \
    -DPYTHON_INCLUDE_DIR=/anaconda3/envs/caffe-ssd/include/python3.8 \
    -DPYTHON_EXECUTABLE=/anaconda3/envs/caffe-ssd/bin/python ..