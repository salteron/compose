FROM scratchy

RUN apt-get update
RUN apt-get install -y -q libmysqlclient-dev curl

# Sphinx
RUN curl -o /root/sphinx.deb http://sphinxsearch.com/files/sphinxsearch_2.2.10-release-0ubuntu12~precise_amd64.deb
RUN apt-get -y -q install libodbc1 unixodbc libpq5
RUN dpkg -i /root/sphinx.deb
RUN rm /root/sphinx.deb

RUN mkdir -p /sphinx/data /sphinx/log /sphinx/conf
ADD sphinx.conf /sphinx/conf/

RUN echo "sleep 5" >> /root/init.sh
RUN echo "indexer --config /sphinx/conf/sphinx.conf --all" >> /root/init.sh
RUN echo "exec searchd --nodetach --config /sphinx/conf/sphinx.conf" >> /root/init.sh

ENTRYPOINT ["/root/init.sh"]
