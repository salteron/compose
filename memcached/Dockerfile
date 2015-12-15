FROM scratchy

RUN apt-get install -y -q memcached
RUN echo "exec memcached -u memcache" >> /root/init.sh

EXPOSE 11211

ENTRYPOINT ["/root/init.sh"]

# run script: docker run -d -p 11211:11211 --restart=always memcached
