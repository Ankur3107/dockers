FROM tensorflow/tensorflow:2.0.0-gpu-py3

### Install General Packages

RUN pip install --no-cache-dir six==1.12.0 \
    pandas xlrd tqdm openpyxl \
    fuzzywuzzy pyyaml numba

### Install Visualization Packages

RUN pip install --no-cache-dir seaborn \
    plotly bokeh

### Install General ML Packages

RUN pip install --no-cache-dir scikit-learn hyperas \
    lightgbm xgboost imbalanced-learn \
    h5py scipy keras-tqdm

### Install NLP Packages

RUN pip install --no-cache-dir transformers sentencepiece \
    tensorflow_addons nlp_preprocessing \
    model-x tensorflow-hub lda2vec gensim textblob wordcloud \
    flashtext


RUN pip install spacy[cuda100] && \
    python -m spacy download en && python -m spacy download en_core_web_sm

WORKDIR /tf
EXPOSE 8888

RUN python3 -m ipykernel.kernelspec

CMD ["bash", "-c", "source /etc/bash.bashrc && jupyter notebook --notebook-dir=/tf --ip 0.0.0.0 --no-browser --allow-root"]