FROM python:3.11-slim AS base

RUN apt-get update && apt-get install -y curl

WORKDIR /usr/local/app

COPY requirements.txt ./requirements.txt 

RUN pip install -r requirements.txt



FROM base AS dev

RUN pip install watchdog

ENV FLASK_ENV=development

CMD [ "python","app.py" ]



FROM base AS final

COPY . .

EXPOSE 80

CMD ["gunicorn", "app:app", "-b", "0.0.0.0:80", "--log-file", "-", "--access-logfile", "-", "--workers", "4", "--keep-alive", "0"]


