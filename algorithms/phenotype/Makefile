.PHONY: clean
mkfile_dir := $(shell dirname $(abspath $(lastword $(MAKEFILE_LIST))))
deps_dir := $(shell dirname $(shell dirname ${mkfile_dir}))/dependencies
include_dir := ${deps_dir}/installdir/include
lib_dir := ${deps_dir}/installdir/lib

phenoalg:
	make -C "${deps_dir}"
	gcc Main.c Support.c -Wl,-rpath,"${lib_dir}" -L"${lib_dir}" -lm -lgsl -fPIC -lblas -lplinkio -I ${include_dir} -o phenoalg

clean:
	make -C "${deps_dir}" clean
	rm -Rf phenoalg
