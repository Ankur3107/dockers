FROM nvcr.io/nvidia/tensorflow:19.08-py3

ADD clean-layer.sh  /tmp/clean-layer.sh

RUN pip install seaborn python-dateutil dask && \
    pip install pyyaml joblib pytagcloud husl geopy ml_metrics mne pyshp && \
    pip install -U spacy[cuda100] && \
    python -m spacy download en && python -m spacy download en_core_web_lg
