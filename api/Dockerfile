# Get the version of python in pipenv
FROM python:3.9

# Create a wrkdir to save files to during the composition below, otherwise when interacting with the docker container
# later all the files created in the image will be all over the place instead of the neatly stored "app" folder:
WORKDIR /app

# State the port the service is running on, needed to use this URL due to dev in codespaces:
# https://jrodriguez5909-silver-garbanzo-59q97prwg5924vw7-5050.preview.app.github.dev/
EXPOSE 5050

# First need to download requirements from the Pipfile
COPY Pipfile Pipfile.lock ./

# Install pipenv items. Note I had to make modifications to this due to debugging:
RUN pip install pipenv
RUN pipenv requirements > requirements.txt
RUN pipenv install -r requirements.txt
# Had to add this line and explictly install all requirements due to persistent error
RUN pip install flask==1.1.2 requests==2.25.1 python-dotenv==0.15.0 flask-cors==3.0.10 pymongo==3.11.3
# I think I could have just run `pip install -r requirements.txt` instead and that would've worked

# Continue building the image file with all other files in the root directory to the /app root dir
COPY . ./

# This does the same as running the flask service in the terminal during development phase
CMD ["python", "main.py"]