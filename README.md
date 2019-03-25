# my_dockerfiles
to store Dockerfiles to make docker images

# notes for making small docker images:
### 1. use the RUN, COPY, ADD commands as few as possible, because every one of them will construct a layer which maker image bigger  

### 2. combine multiple into one RUN command to reduce image size

### 3. the build context should contain files as less as possible

### 4. use .dockerignore to ignore large file in the build context

### 5. append the following commands after using apt-get to install packages: 
&& apt-get -y clean all \
&& apt-get -y autoremove \
&& rm -rf /var/lib/apt/lists/* \

### 6. use option  "--no-install-recommends" to make apt-get not to install unesessary packages.

### 7. use "--squash" option for docker build command to combine all layers into one, which can largely reduce the final image size.

### 8. If you install packages from source, after you build and make install them, use "make clean" to clean all the intermediate files. Finally remove all source files and tarballs.

### 9. Remove any files unesessary, such as the source files build directories and static libraries. 

 
