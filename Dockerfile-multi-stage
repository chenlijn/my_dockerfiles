FROM pacv/dev:cuda10.0-cudnn7-py36-mx1.14.0-tf1.13.1-caffe2-pytorch1.0-cv3.4.5-thrift0.11.0-v0.3

RUN cd ~\
&& yum remove -y cuda-compat-10-1 \
&& yum install -y cuda-compat-10-0  curl curl-devel \
&& echo "export LD_LIBRARY_PATH=/usr/local/lib:/usr/local/lib64:/usr/local/nvidia/lib:/usr/local/nvidia/lib64:/usr/lib:/usr/lib64" >> ~/.bashrc \
&& yum clean all \
&& rm -rf /var/cache/* \
&& rm -rf /tmp/* \
&& rm -rf ~/.cache

# stage 2: build a new image excluding all history from the previous one 
FROM scratch
COPY --from=0 / /   # copy all things from previeous image into new image

LABEL maintainer "Lijian Chen <chenlijian535@pingan.com.cn>"

# the critical environment variables should be set, docker needs them to run properly.
ENV CUDA_VERSION 10.0.130
ENV CUDA_PKG_VERSION 10-0-$CUDA_VERSION-1
ENV PATH /usr/local/nvidia/bin:/usr/local/cuda/bin:${PATH}
ENV LD_LIBRARY_PATH /usr/local/nvidia/lib:/usr/local/nvidia/lib64

# nvidia-container-runtime
ENV NVIDIA_VISIBLE_DEVICES all
ENV NVIDIA_DRIVER_CAPABILITIES compute,utility
ENV NVIDIA_REQUIRE_CUDA "cuda>=10.0 brand=tesla,driver>=384,driver<385"
ENV LIBRARY_PATH /usr/local/cuda/lib64/stubs
ENV CUDNN_VERSION 7.5.0.56
LABEL com.nvidia.cudnn.version="${CUDNN_VERSION}"

WORKDIR /root/


