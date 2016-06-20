FROM ubuntu:14.04

ARG ANDROID_STUDIO_URL='https://dl.google.com/dl/android/studio/ide-zips/2.1.2.0/android-studio-ide-143.2915827-linux.zip'
# by default: Lenovo vendor
ARG ID_DEVICE_VENDOR=17ef

# Install java8
RUN apt-get update && apt-get install -y --force-yes \
		software-properties-common \
	&& add-apt-repository -y ppa:webupd8team/java 
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get update && apt-get install -y --force-yes \
		oracle-java8-installer 

# Install dependencies
RUN dpkg --add-architecture i386 && apt-get update && apt-get install -y --force-yes \
		curl \
        unzip \
        libc6-i386 \
        lib32z1 \
        lib32ncurses5 \
        lib32bz2-1.0 \
        lib32stdc++6 \
        libxtst6 \
        libxrender1 \
        libXi6	

# Get Android Studio
RUN curl $ANDROID_STUDIO_URL > /tmp/studio.zip \
		&& unzip -d /opt /tmp/studio.zip \
		&& rm /tmp/studio.zip

# Create a default rule to devices
RUN echo "SUBSYSTEM==\"usb\", ATTR{idVendor}==\"${ID_DEVICE_VENDOR}\", MODE=\"0666\", GROUP=\"plugdev\"" > /etc/udev/rules.d/51-android.rules
RUN chmod a+r /etc/udev/rules.d/51-android.rules

RUN apt-get clean

# Setup enviroment
ENV PATH ${PATH}:/opt/android-studio/bin

CMD studio.sh