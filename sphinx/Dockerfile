FROM scratchy

RUN apt-get install -y -q libmysqlclient-dev curl

# Sphinx
RUN curl -o /root/sphinx.deb http://sphinxsearch.com/files/sphinxsearch_2.2.10-release-0ubuntu12~precise_amd64.deb
RUN apt-get -y -q install libodbc1 unixodbc libpq5
RUN dpkg -i /root/sphinx.deb
RUN rm /root/sphinx.deb

RUN echo "sleep 5" >> /root/init.sh
RUN echo "indexer --config /sphinx/conf/development.sphinx.conf --all" >> /root/init.sh
RUN echo "exec searchd --nodetach --config /sphinx/conf/development.sphinx.conf" >> /root/init.sh

EXPOSE 9306 10809

ENTRYPOINT ["/root/init.sh"]

RUN mkdir -p /sphinx/data /sphinx/log /sphinx/conf

# run script: docker run -d -p 9306:9306 --restart=always -v ~/rails_applications/blizko/config:/sphinx/conf:ro --link db:db sphinx


