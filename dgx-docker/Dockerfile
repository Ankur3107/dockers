FROM nvcr.io/nvidia/tensorflow:19.08-py3

ADD clean-layer.sh  /tmp/clean-layer.sh

RUN pip install seaborn python-dateutil dask && \
    pip install pyyaml joblib pytagcloud husl geopy ml_metrics mne pyshp && \
    pip install -U spacy[cuda100] && \
    python -m spacy download en && python -m spacy download en_core_web_lg

RUN pip install gensim && \
    pip install wordcloud && \
    # chainer
    pip install chainer && \
    # NLTK Project datasets
    mkdir -p /usr/share/nltk_data && \
    # NLTK Downloader no longer continues smoothly after an error, so we explicitly list
    # the corpuses that work
    # "yes | ..." answers yes to the retry prompt in case of an error. See b/133762095.
    yes | python -m nltk.downloader -d /usr/share/nltk_data abc alpino averaged_perceptron_tagger \
    basque_grammars biocreative_ppi bllip_wsj_no_aux \
    book_grammars brown brown_tei cess_cat cess_esp chat80 city_database cmudict \
    comtrans conll2000 conll2002 conll2007 crubadan dependency_treebank \
    europarl_raw floresta gazetteers genesis gutenberg \
    ieer inaugural indian jeita kimmo knbc large_grammars lin_thesaurus mac_morpho machado \
    masc_tagged maxent_ne_chunker maxent_treebank_pos_tagger moses_sample movie_reviews \
    mte_teip5 names nps_chat omw opinion_lexicon paradigms \
    pil pl196x porter_test ppattach problem_reports product_reviews_1 product_reviews_2 propbank \
    pros_cons ptb punkt qc reuters rslp rte sample_grammars semcor senseval sentence_polarity \
    sentiwordnet shakespeare sinica_treebank smultron snowball_data spanish_grammars \
    state_union stopwords subjectivity swadesh switchboard tagsets timit toolbox treebank \
    twitter_samples udhr2 udhr unicode_samples universal_tagset universal_treebanks_v20 \
    vader_lexicon verbnet webtext word2vec_sample wordnet wordnet_ic words ycoe && \
    # Stop-words
    pip install stop-words && \
    pip install --upgrade scikit-image

# b/128333086: Set PROJ_LIB to points to the proj4 cartographic library.
ENV PROJ_LIB=/opt/conda/share/proj


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

RUN pip install kmeans-smote --no-dependencies && \
    # Add google PAIR-code Facets
    cd /opt/ && git clone https://github.com/PAIR-code/facets && cd facets/ && jupyter nbextension install facets-dist/ --user && \
    export PYTHONPATH=$PYTHONPATH:/opt/facets/facets_overview/python/ && \
    pip install tensorpack && \
    pip install pycountry && pip install iso3166 && \
    pip install pydash && \
    pip install kmodes --no-dependencies && \
    pip install librosa && \
    pip install polyglot && \
    pip install mmh3 && \
    pip install fbpca && \
    pip install sentencepiece && \
    pip install cufflinks && \
    pip install glmnet_py && \
    pip install lime && \
    pip install memory_profiler


# install cython & cysignals before pyfasttext
RUN pip install --upgrade cython && \
    pip install --upgrade cysignals && \
    pip install pyfasttext && \
    # ktext has an explicit dependency on Keras 2.2.4 which is not
    # compatible with TensorFlow 2.0 (support was added in Keras 2.3.0).
    # Add the package back once it is fixed upstream.
    # pip install ktext && \
    pip install fasttext && \
    apt-get install -y libhunspell-dev && pip install hunspell && \
    # b/138723119: annoy's latest version 1.16 was failing
    pip install annoy==1.15.2 && \
    # Need to use CountEncoder from category_encoders before it's officially released
    pip install git+https://github.com/scikit-learn-contrib/categorical-encoding.git && \
    # TODO(b/143373325) Revert to 0.6.0 to avoid regression in 0.7.0. Go back to
    # latest when 0.8.0 is released.
    pip install google-cloud-automl==0.6.0 && \
    # Newer version crashes (latest = 1.14.0) when running tensorflow.
    # python -c "from google.cloud import bigquery; import tensorflow". This flow is common because bigquery is imported in kaggle_gcp.py
    # which is loaded at startup.
    pip install google-cloud-bigquery==1.12.1 && \
    pip install google-cloud-storage && \
    pip install ortools && \
    pip install scattertext && \
    # Pandas data reader
    pip install pandas-datareader && \
    pip install pykoko && \
    pip install wordsegment && \
    pip install pyahocorasick && \
    pip install wordbatch && \
    pip install emoji && \
    # Add Japanese morphological analysis engine
    pip install janome && \
    pip install wfdb && \
    pip install vecstack && \
    pip install sklearn-contrib-lightning && \
    # yellowbrick machine learning visualization library
    pip install yellowbrick && \
    pip install mlcrate && \
    # Required to display Altair charts in Jupyter notebook
    pip install vega3 && \
    jupyter nbextension install --sys-prefix --py vega3

RUN pip install mpld3 && \
    pip install mplleaflet && \
    pip install gpxpy && \
    pip install arrow && \
    pip install nilearn && \
    pip install nibabel && \
    pip install pronouncing && \
    pip install markovify && \
    pip install rf_perm_feat_import && \
    pip install imgaug && \
    pip install preprocessing && \
    pip install Baker && \
    pip install path.py && \
    pip install Geohash && \
    pip install deap && \
    pip install tpot && \
    pip install scikit-optimize && \
    pip install haversine && \
    pip install toolz cytoolz && \
    pip install sacred && \
    pip install plotly && \
    pip install git+https://github.com/nicta/dora.git && \
    pip install git+https://github.com/hyperopt/hyperopt.git && \
    # tflean. Deep learning library featuring a higher-level API for TensorFlow. http://tflearn.org
    pip install git+https://github.com/tflearn/tflearn.git && \
    pip install fitter && \
    pip install langid && \
    # Delorean. Useful for dealing with datetime
    pip install delorean && \
    pip install trueskill && \
    pip install heamy && \
    pip install vida && \
    # Useful data exploration libraries (for missing data and generating reports)
    pip install missingno && \
    pip install pandas-profiling && \
    pip install s2sphere && \
    pip install git+https://github.com/fmfn/BayesianOptimization.git && \
    pip install matplotlib-venn && \
    pip install pyldavis && \
    pip install mlxtend && \
    pip install altair && \
    pip install pystan && \
    pip install ImageHash && \
    pip install ecos && \
    pip install CVXcanon && \
    pip install fancyimpute && \
    pip install git+https://github.com/pymc-devs/pymc3 && \
    pip install tifffile && \
    pip install spectral && \
    pip install descartes && \
    pip install geojson && \
    pip install pysal && \
    pip install pyflux && \
    pip install terminalplot && \
    pip install raccoon && \
    pip install pydicom && \
    pip install wavio && \
    pip install SimpleITK && \
    pip install hmmlearn && \
    pip install bayespy && \
    pip install gplearn && \
    pip install PyAstronomy && \
    pip install squarify && \
    pip install fuzzywuzzy && \
    pip install python-louvain && \
    pip install pyexcel-ods && \
    pip install sklearn-pandas && \
    pip install stemming && \
    pip install fbprophet && \
    pip install holoviews



