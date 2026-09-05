FROM public.ecr.aws/docker/library/python:3.10-alpine

ENV FLASK_RUN_HOST=0.0.0.0

RUN adduser -u 1000 -D app

RUN apk update && \
    apk add \
      pcre \
      pcre-dev \
      build-base \
      gcc \
      linux-headers \
      openssl \
      libffi-dev && \
    pip install pipenv

WORKDIR /app

COPY Pipfile* ./

RUN pipenv install --system --deploy

COPY . .

RUN pip install gunicorn

EXPOSE 5000

CMD ["gunicorn", "--bind", "0.0.0.0:5000", "app:app"]