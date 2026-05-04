# phased-output branch
Tentative development branch of [HAPNEST](https://github.com/intervene-EU-H2020/synthetic_data) to output **phased** genotype data in [PLINK2](https://www.cog-genomics.org/plink/2.0/) format. After setting up things, run the different stages of the pipeline as configured by `config.yaml` with
```sh
conda activate hapnest && export JULIA_DEPOT_PATH=$(pwd)/.juliadepot
DATA_DIR="$(pwd)/data" ./commands/fetch
julia --threads 1 run_program.jl --genotype --config config.yaml
julia run_program.jl --phenotype --config config.yaml
julia --project=$(pwd) run_program.jl --evaluation --config config.yaml
```

## setup
The dependencies can be obtained in different ways. For example, on Ubuntu you can get Julia from the Snap store, `plink`, `plink2`, `king`, `vcftools`, `bcftools` from the bioconda channel, and `mapthin`, `libplinkio` from GitHub as follows:
```sh
snap install julia --classic
conda create --name hapnest
conda activate hapnest
conda install bioconda::plink bioconda::plink2 bioconda::king bioconda::vcftools bioconda::bcftools
git submodule update --init --recursive dependencies
make -C dependencies && make -C algorithms/phenotype
mkdir .juliadepot && export JULIA_DEPOT_PATH=$(pwd)/.juliadepot
julia --project=$(pwd) -e "using Pkg; Pkg.add(url=\"https://github.com/tanhevg/GpABC.jl\"); Pkg.instantiate(); using Conda; Conda.add(\"python=3.10\"); Conda.add(\"libpython-static=3.10\"); Conda.add(\"bed-reader\"; channel=\"conda-forge\"); Pkg.build(\"PyCall\")"
```

Note that `bcftools` is a new dependency compared to the main HAPNEST branch.
