# The image you are going to inherit your Dockerfile from
FROM python:3.9-alpine
# Set the /django_blog directory as the working directory
WORKDIR /app
#create a group and add user to the group
RUN addgroup systemUserGroup && \
    adduser -D -G systemUserGroup developer && \
    chown developer:systemUserGroup /app && \
    chmod -R 755 /app
#grant executable permission to the group
RUN chmod g+x /app
# Create a user that can run your container
USER developer
ENV PYTHONUNBUFFERED 1
# Set environment variables for AWS RDS and S3
ENV DB_HOST=${DB_HOST}
ENV DB_NAME=${DB_NAME}
ENV DB_PORT=${DB_PORT}
ENV DB_USER=${DB_USER}
ENV DB_PASSWORD=${DB_PASSWORD}
ENV DJANGO_SECRET=${DJANGO_SECRET}
ENV AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}
ENV AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}
ENV AWS_STORAGE_BUCKET_NAME=${AWS_STORAGE_BUCKET_NAME}
ENV AWS_S3_REGION_NAME=${AWS_S3_REGION_NAME}
ENV AWS_S3_ENDPOINT_URL=${AWS_S3_ENDPOINT_URL}
ENV ALLOWED_HOSTS=${ALLOWED_HOSTS}
# Copy the requirements.txt file adjacent to the Dockerfile
COPY ./requirements.txt requirements.txt
# Install the requirements.txt file in Docker image
RUN pip install -r requirements.txt
ENV DEBUG=${DEBUG}
# copy the django project into the container image
COPY . .
CMD python3 manage.py makemigrations && \
    python3 manage.py migrate && \
    python3 manage.py runserver 0.0.0.0:8000

# CMD ["python3", "manage.py", "runserver", "0.0.0.0:8000"]
