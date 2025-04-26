# Start by defining the base image for the build stage (named 'BUILD_IMAGE')
FROM ubuntu:latest AS build_image

# Update package list and install 'wget' (for downloading files) and 'unzip' (for extracting zip files)
RUN apt update && apt install wget unzip -y
RUN wget https://www.tooplate.com/zip-templates/2128_tween_agency.zip

# Unzip the downloaded file, change into the extracted directory, 
# then tar (compress) the contents into 'tween.tgz' and move it to the /root directory
RUN unzip 2128_tween_agency.zip && cd 2128_tween_agency && tar -czf tween.tgz * && mv tween.tgz /root/tween.tgz

# ----

# Define the second stage, starting from a fresh Ubuntu image
FROM ubuntu:latest
LABEL "project"="Marketing"
ENV DEBIAN_FRONTEND=noninteractive

# ----

# Update package list and install Apache2 (web server), Git (version control), and wget (file downloader)
RUN apt update && apt install apache2 git wget -y

# Copy the 'tween.tgz' file from the build stage (/root/tween.tgz) into the Apache web root directory (/var/www/html/)
COPY --from=build_image /root/tween.tgz /var/www/html/

# Change to the Apache web root directory and extract the 'tween.tgz' tarball
RUN cd /var/www/html/ && tar xzf tween.tgz

# Define the default command to run when the container starts (start Apache in the foreground)
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

# Create a volume for storing Apache logs, allowing data persistence across container restarts
VOLUME /var/log/apache2

# Set the working directory for the following commands to /var/www/html/
WORKDIR /var/www/html/

EXPOSE 80

