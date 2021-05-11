FROM markajadriano/ubuntu18-nginx:7.3

ARG SITE_URL
ENV CERT="/C=NZ/ST=Wellington/L=SilverStripe/O=NinjaFoxes/CN=${SITE_URL}"

RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/nginx-selfsigned.key -out /etc/ssl/certs/nginx-selfsigned.crt \
	-subj ${CERT} \
	&& openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048

COPY snippets/self-signed.conf /etc/nginx/snippets/self-signed.conf
COPY snippets/ssl-params.conf /etc/nginx/snippets/ssl-params.conf

# Install cron
RUN apt-get update && apt-get install -y cron

RUN echo 'alias ondebug="sudo phpenmod -s cli xdebug"' >> ~/.bashrc  && \
	echo 'alias offdebug="sudo phpdismod -s cli xdebug"' >> ~/.bashrc && \
	echo 'alias compose1="composer self-update 1.10.17"' >> ~/.bashrc && \
	echo 'alias compose2="composer self-update --rollback"' >> ~/.bashrc && \
	echo 'alias qwerty="sake dev/tasks/ProcessJobQueueTask"' >> ~/.bashrc && \
	echo 'alias sconfig="sake dev/tasks/SearchConfigure"' >> ~/.bashrc && \
	echo 'alias reindex="sake dev/tasks/SearchReindex"' >> ~/.bashrc


RUN sed -i "s/local.site/${SITE_URL}/g" /etc/nginx/sites-available/default

CMD "/usr/bin/supervisord"
