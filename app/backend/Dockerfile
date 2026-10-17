FROM python:3.13-slim

COPY requirements.txt .
RUN pip install -r requirements.txt \
 && pip uninstall -y pip \
 && useradd --uid 10001 --no-create-home --shell /usr/sbin/nologin app


USER 10001
ARG APP_VERSION=dev
ENV APP_VERSION=${APP_VERSION}
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PIP_NO_CACHE_DIR=1 \
    PIP_DISABLE_PIP_VERSION_CHECK=1


COPY taskboard ./taskboard

EXPOSE 8000
CMD ["uvicorn", "taskboard.main:app", "--host", "0.0.0.0", "--port", "8000", "--proxy-headers", "--forwarded-allow-ips", "*"]