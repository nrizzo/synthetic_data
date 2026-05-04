.PHONY : all clean
all: mapthin installdir

mapthin:
	g++ -O3 MapThin/src/*.cpp -o mapthin
installdir:
	(cd libplinkio && mkdir build && cd build && cmake -D CMAKE_INSTALL_PREFIX=../../installdir ../ && make && make test && make install)

clean:
	rm -Rf installdir mapthin libplinkio/build
