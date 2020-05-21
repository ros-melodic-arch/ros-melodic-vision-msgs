pkgdesc="ROS - Messages for interfacing with various computer vision pipelines, such as object detectors."
url='https://wiki.ros.org/vision_msgs'

pkgname='ros-melodic-vision-msgs'
pkgver='1.0.0'
arch=('any')
pkgrel=1
license=('Apache License 2.0')

ros_makedepends=(ros-melodic-std-msgs
  ros-melodic-message-runtime
  ros-melodic-catkin
  ros-melodic-geometry-msgs
  ros-melodic-message-generation
  ros-melodic-sensor-msgs)
makedepends=('cmake' 'ros-build-tools'
  ${ros_makedepends[@]})

ros_depends=(ros-melodic-geometry-msgs
  ros-melodic-message-runtime
  ros-melodic-message-generation
  ros-melodic-sensor-msgs
  ros-melodic-std-msgs)
depends=(${ros_depends[@]})

_dir="vision_msgs-${pkgver}"
source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/Kukanani/vision_msgs/archive/${pkgver}.tar.gz")
sha256sums=('c3d9bb2b7eb3dec393e87b7c6d6eeb772ab57aed4cd80c00ef5da6240373aecd')

build() {
  # Use ROS environment variables
  source /usr/share/ros-build-tools/clear-ros-env.sh
  [ -f /opt/ros/melodic/setup.bash ] && source /opt/ros/melodic/setup.bash

  # Create build directory
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build

  # Fix Python2/Python3 conflicts
  /usr/share/ros-build-tools/fix-python-scripts.sh -v 3 ${srcdir}/${_dir}

  # Build project
  cmake ${srcdir}/${_dir} \
        -DCMAKE_BUILD_TYPE=Release \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/melodic \
        -DPYTHON_EXECUTABLE=/usr/bin/python3 \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
