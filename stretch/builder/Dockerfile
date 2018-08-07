FROM yangxuan8282/raspbian

RUN set -xe \
  && apt-get update && apt-get upgrade -y \
  && apt-get install -y dirmngr

ADD sources.list /etc/apt/sources.list
ADD raspi.list /etc/apt/sources.list.d/raspi.list
ADD build.sh /root/

RUN set -xe \
  && apt-key adv --keyserver keyserver.ubuntu.com --recv 82B129927FA3303E \
  && apt-get update && apt-get upgrade -y
#  && apt-get install -y build-essentials

RUN apt-get install -y ccache \
  && export PATH=/usr/lib/ccache:$PATH

RUN apt-get install -y sudo libraspberrypi-dev fakeroot \
  && useradd -g sudo -ms /bin/bash pi \
  && echo "pi:raspberry" | chpasswd \
  && echo "pi ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers \
  && sed -i 's/#force_color_prompt=yes/force_color_prompt=yes/g' /home/pi/.bashrc \
  && su pi sh -c 'mkdir -p /home/pi/work' \
  && mv /root/build.sh /home/pi/work/ \
  && chown pi /home/pi/work/build.sh \
  && rm -rf /var/lib/apt/lists/*

WORKDIR /home/pi/work
USER pi
