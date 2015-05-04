#### Build a php image for officialy released php version

1. change the placeholder *{YOUR_VERSION}* through a real one( for example 5.4.39)
in **released/Dockerfile** 
2. and build an image with

     $ docker build -t {your_name}/php:{your_version} released   
