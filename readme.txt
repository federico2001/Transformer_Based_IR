To run the jupyter lab file that emulates the exact same operating system, python version and required libraries in 'production' please run the jupyter lab through this Dockerfile:

docker build --no-cache -t jupyter_lab_image .

docker run -p 8080:8080 -v "$(pwd)":/app jupyter_lab_image
