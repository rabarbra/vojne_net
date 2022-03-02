FROM python:3.9-alpine

ARG YOUR_ENV

ENV YOUR_ENV=${YOUR_ENV} \
    PYTHONFAULTHANDLER=1 \
    PYTHONUNBUFFERED=1 \
    PYTHONHASHSEED=random \
    PIP_NO_CACHE_DIR=off \
    PIP_DISABLE_PIP_VERSION_CHECK=on \
    PIP_DEFAULT_TIMEOUT=100

RUN python -m pip install --upgrade pip && pip install poetry

WORKDIR /vojne_net/backend
COPY pyproject.toml poetry.lock /vojne_net/backend/

RUN poetry config virtualenvs.create false \
  && poetry install $(test "$YOUR_ENV" == production && echo "--no-dev") --no-interaction --no-ansi

COPY ./app /vojne_net/backend/