#
# NOTE: Use the Makefiles to build this image correctly.
#

ARG BASE_IMG=<jupyter>
FROM $BASE_IMG

# install - usefull linux packages
USER root
RUN apt-get -yq update \
 && apt-get -yq install --no-install-recommends \
    # for latex
    cm-super \
    dvipng \
    # for matplotlib
    ffmpeg \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
USER $NB_UID

# install - conda packages
# NOTE: we use mamba to speed things up
RUN mamba install -y -q \
    altair \
    beautifulsoup4==4.12.2 \
    bokeh==3.1.1 \
    bottleneck \
    brotli \
    cloudpickle \
    dask==2023.5.0 \
    dill \
    h5py \
    ipympl \
    matplotlib==3.7.0 \
    numba \
    numexpr \
    openblas==0.3.24 \
    openpyxl \
    pandas==2.0.3 \
    patsy \
    protobuf \
    pytables==3.8.0 \
    scikit-image==0.21.0 \
    scikit-learn==1.3.1 \
    scipy==1.10.1 \
    seaborn==0.13.0 \
    sqlalchemy==2.0.22 \
    statsmodels \
    sympy \
    vincent \
    xlrd \
 && mamba clean -a -f -y

# install - requirements.txt
COPY --chown=${NB_USER}:users requirements.txt /tmp
RUN python3 -m pip install -r /tmp/requirements.txt --quiet --no-cache-dir \
 && rm -f /tmp/requirements.txt