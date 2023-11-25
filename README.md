# dockercompose_file
Creating a Docker Compose file to set up Jenkins, SonarQube, and Nexus can help you manage and run these services together.
Below is an example Docker Compose file (docker-compose.yml) that you can use. Note that you may need to adjust version numbers and configurations based on your specific requirements:

version: '3'

services:
  jenkins:
    image: jenkins/jenkins:lts
    ports:
      - "8080:8080"
    volumes:
      - jenkins_home:/var/jenkins_home
    networks:
      - dev-net

  sonarqube:
    image: sonarqube:latest
    ports:
      - "9000:9000"
    networks:
      - dev-net

  nexus:
    image: sonatype/nexus3
    ports:
      - "8081:8081"
    volumes:
      - nexus_data:/nexus-data
    networks:
      - dev-net

networks:
  dev-net:

volumes:
  jenkins_home:
  nexus_data:
  
Save this file as docker-compose.yml and then run the following command in the directory where the file is located:

docker-compose up -d

This Docker Compose configuration does the following:

Sets up Jenkins with its home directory persisted in a volume (jenkins_home).
Sets up SonarQube with port 9000 exposed.
Sets up Nexus with port 8081 exposed and its data persisted in a volume (nexus_data).
Creates a custom bridge network (dev-net) so that the services can communicate with each other.
Make sure Docker and Docker Compose are installed on your system before running the above commands. You can customize this configuration based on your specific needs and configurations for Jenkins, SonarQube, and Nexus.

After running the docker-compose up -d command, you can access Jenkins at http://localhost:8080, SonarQube at http://localhost:9000, and Nexus at http://localhost:8081. Note that it may take a few moments for the services to start up initially.
