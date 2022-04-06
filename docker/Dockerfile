from ubuntu:18.04
RUN apt-get update &&\
    apt-get install -y git &&\
    apt-get install -y wget &&\
    wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh &&\
    bash Miniconda3-latest-Linux-x86_64.sh -b -p /miniconda &&\
    rm -rf Miniconda3-latest-Linux-x86_64.sh
WORKDIR /home/

RUN mkdir Notebooks
ENV PATH=$PATH:/miniconda/bin

COPY . .

RUN conda env create -f ./signal.yml &&\
    conda clean -afy
#RUN conda init bash &&\
    #echo "conda activate signal" > ~/.bashrc

#RUN conda create --name signal python=3.7
#RUN conda install -n signal -c conda-forge notebook
RUN echo "source activate signal" > ~/.bashrc
ENV PATH=$PATH:/miniconda/envs/signal/bin

EXPOSE 8888
#CMD ["bash", "-c", "/miniconda/envs/signal/bin/jupyter notebook \
#  --notebook-dir=/home/Notebooks --ip='*' --port=8888 \
#  --no-browser --allow-root"]
CMD ["bash"]
