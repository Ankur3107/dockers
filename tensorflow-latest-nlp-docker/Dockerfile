FROM tensorflow/tensorflow:latest-gpu-py3-jupyter
 
ADD clean-layer.sh  /tmp/clean-layer.sh

RUN pip install seaborn python-dateutil dask && \
    pip install pyyaml joblib pytagcloud husl geopy ml_metrics mne pyshp && \
    pip install -U spacy[cuda100]

RUN python -m spacy download en


RUN pip install gensim && \
    pip install wordcloud && \
    # chainer
    pip install chainer
    
# scikit-learn dependencies
RUN pip install scipy && \
    pip install scikit-learn && \
    # HDF5 support
    pip install h5py && \
    pip install biopython && \
    # PUDB, for local debugging convenience
    pip install pudb && \
    pip install imbalanced-learn && \
    # Convex Optimization library
    # Latest version fails to install, see https://github.com/cvxopt/cvxopt/issues/77
    #    and https://github.com/cvxopt/cvxopt/issues/80
    # pip install cvxopt && \
    # Profiling and other utilities
    pip install line_profiler && \
    pip install orderedmultidict && \
    pip install smhasher && \
    pip install bokeh && \
    pip install numba && \
    pip install datashader

# New Packages

COPY new_packages/requirements.txt requirements.txt

RUN pip install -r requirements.txt
