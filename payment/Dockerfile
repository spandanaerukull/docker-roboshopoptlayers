#stage 1: Builder stage
FROM python:3.9 .23-alpine3.22 AS builder 
WORKDIR /build
# install build dependencies
RUN apk add --no-cache python3-dev build-base linux-headers pcre-dev
COPY requirements.txt .
RUN pip3 install --no-cache-dir --prefix=/install -r requirements.txt


#stage 2: Final image
FROM python:3.9.23-alpine3.22
EXPOSE 8080
WORKDIR /opt/server
# runtime dependiencies only
RUN apk add --no-cache pcre
# creat app user
RUN addgroup -s roboshop && adduser -s roboshop -G roboshop
USER roboshop
# copy installed python packages from builder 
COPY --from=builder /install /usr/local
# copy application code
COPY --chown=roboshop:roboshop payment.ini .
COPY --chown=roboshop:roboshop *.py .
CMD ["uwsgi", "--ini", "payment.ini"] 






# FROM python:3.9
# EXPOSE 8080
# WORKDIR /opt/server
# COPY requirements.txt .
# COPY *.py .
# COPY payment.ini .
# RUN pip3 install -r requirements.txt
# CMD ["uwsgi", "--ini", "payment.ini"]





































