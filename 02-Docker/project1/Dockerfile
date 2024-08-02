#download based image from dockerhub.com
FROM python:3.12-slim

# create new app folder in linux image
WORKDIR /app 

#Copy from based-operating-system to linux image
#Copy source destination
# copy everything from source-operating-system to linux image
COPY . ./app/

# run python file code
# CMD python ./app/my_code.py
ENTRYPOINT ["python", "./app/my_code.py"]

