# crawler

## Setup

### Download npm graph

* `wget https://skimdb.npmjs.com/registry/_design/scratch/_view/byField -o data.json` (~700MB)

### Extract downloading information

* `cat data.json | jq -r '.rows | map({name: .value.name, tarball: .value.dist.tarball})' > short_data.json`

### Create a csv file mapping names to tarball urls

* `cat short_data.json | jq -r 'map([.name, .tarball] | join(",")) | join("\n")' > short_data.csv`


### Download all tarballs

* `cat short_data.csv | cut -d "," -f2 > files.txt`
* `wget -i files.txt`

## Things to measure

* shortest / longest / most common identifier name
* graph: identifier lengths
* max number of function args
* longest function body
* ES6 / ES7 feature adoption (arrow-functions vs normal, const/let vs var)
* longest file
* graph: number of dependencies
* most dependencies / most depended on
* graph: current version, number of versions, using semver?
* parsing errors => open up issues / pull requests
* graph: age of package, age of last version
