#create python virtual environment(venv)
python3 -m venv venv

#activate venv
source venv/bin/activate

#install all requirements
pip install -r requirements.txt

#install rabbitmq(message broker)
brew install rabbitmq

#run rabbitmq
brew services start rabbitmq

#run FastApi app
uvicorn main:app --port 9000 --reload

#run Celery
celery -A main.celery worker --loglevel=info -Q universities,university

#run Celery Flower
celery -A main.celery flower --port=5555

#go to http://localhost:9000/docs and check out app