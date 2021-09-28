# build environment
FROM alpine:3.14 as base-image

RUN apk update && apk add python3 python3-dev py3-pip build-base py3-cffi libressl-dev libffi-dev
RUN printf "installed python version: \n" && python3 --version
RUN pip install --upgrade pip && pip install wheel
RUN printf "installed pip version: \n" && pip --version
WORKDIR /root
COPY ./requirements-pinned.txt .
RUN pip install --user -r requirements-pinned.txt
COPY . .
RUN pip install --user .

# release image build
FROM alpine:3.14 AS built-image
LABEL maintainer="Santiago Torres Arias <santiagotorres@purdue.edu>"

RUN apk update && apk add python3
COPY --from=base-image /root/.local /root/.local
ENV PATH=/root/.local/bin:$PATH
RUN mkdir /workspace
WORKDIR /workspace
