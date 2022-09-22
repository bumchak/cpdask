FROM quay.io/condaforge/miniforge3

RUN wget -O /usr/local/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64
RUN chmod +x /usr/local/bin/dumb-init

RUN conda install --yes \
	-c conda-forge \
	python=3.10 \
    python-blosc==1.10.2 \
    zarr==2.12.0 \
	pyarrow==9.0.0 \  
	dask==2022.6.0 \
	distributed==2022.6.0 \
	numpy==1.23.3 \
	pandas==1.4.4 \
	xarray==0.19.0 \
	fsspec==2021.8.1 \
	s3fs \
	&& find /opt/conda/ -type f,l -name '*.a' -delete \
    && find /opt/conda/ -type f,l -name '*.pyc' -delete \
    && find /opt/conda/ -type f,l -name '*.js.map' -delete \
    && find /opt/conda/lib/python*/site-packages/bokeh/server/static -type f,l -name '*.js' -not -name '*.min.js' -delete \
    && rm -rf /opt/conda/pkgs
	
	

COPY prepare.sh /usr/bin/prepare.sh
RUN chmod +x /usr/bin/prepare.sh

RUN mkdir /opt/app /etc/dask
COPY dask.yaml /etc/dask/

ENTRYPOINT ["/usr/local/bin/dumb-init", "/usr/bin/prepare.sh"]
