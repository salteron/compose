FROM scratchy

RUN apt-get install -y -q redis-server
RUN echo "exec redis-server" >> /root/init.sh

ENTRYPOINT ["/root/init.sh"]

EXPOSE 6379

# run script: docker run -d -p 6379:6379 --restart=always redis
# check script: redis-cli