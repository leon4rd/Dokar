FROM amirulandalib/mltb-alpine-docker:latest

WORKDIR /usr/src/app

RUN chmod 777 /usr/src/app
RUN wget https://raw.githubusercontent.com/chestereckhart/mirror-leech-telegram-bot/master/requirements.txt

RUN pip3 install --no-cache-dir -r requirements.txt
