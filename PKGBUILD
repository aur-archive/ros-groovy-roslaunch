pkgdesc="ROS - tool for easily launching multiple ROS nodes."
url='http://www.ros.org/'

pkgname='ros-groovy-roslaunch'
pkgver='1.9.50'
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')
makedepends=('ros-build-tools')

depends=(ros-groovy-rosclean
  ros-groovy-catkin
  python2-rospkg
  ros-groovy-rosout
  ros-groovy-rosmaster
  ros-groovy-rosgraph-msgs
  python2-paramiko
  python2-netifaces
  python2-yaml)

build() {
  [ -f /opt/ros/groovy/setup.bash ] && source /opt/ros/groovy/setup.bash
  if [ -d ${srcdir}/roslaunch ]; then
    cd ${srcdir}/roslaunch
    git fetch origin --tags
    git reset --hard release/groovy/roslaunch/${pkgver}-0
  else
    git clone -b release/groovy/roslaunch/${pkgver}-0 git://github.com/ros-gbp/ros_comm-release.git ${srcdir}/roslaunch
  fi
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/roslaunch
  cmake ${srcdir}/roslaunch -DCATKIN_BUILD_BINARY_PACKAGE=ON -DCMAKE_INSTALL_PREFIX=/opt/ros/groovy -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
