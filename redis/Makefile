#
# Convenience Makefile providing a few common top-level targets.
#

cmake_build_dir=build
arch=`uname -s | tr A-Z a-z`-`uname -m`

all: build-it

build-it:
	@test -e $(cmake_build_dir)/config.status || ./configure
	-@test -e $(cmake_build_dir)/CMakeCache.txt && \
      test $(cmake_build_dir)/CMakeCache.txt -ot `cat $(cmake_build_dir)/CMakeCache.txt | grep BRO_DIST | cut -d '=' -f 2`/build/CMakeCache.txt && \
      echo Updating stale CMake cache && \
      touch $(cmake_build_dir)/CMakeCache.txt
	( cd $(cmake_build_dir) && make )

install:
	( cd $(cmake_build_dir) && $(MAKE) install )

clean:
	( cd $(cmake_build_dir) && $(MAKE) clean )

distclean:
	rm -rf $(cmake_build_dir)

test:
	if [ -f build/lib/Bro-* ]; then make -C tests; else echo "Plugin not built."; fi
