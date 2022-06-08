### Используя исходники лабораторной работы номер 6.

```bash
$ mkdir -p cmake
$ wget https://raw.githubusercontent.com/cpp-pm/gate/master/cmake/HunterGate.cmake -O cmake/HunterGate.cmake
$ gsed -i '/cmake_minimum_required(VERSION 3.4)/a\

include("cmake/HunterGate.cmake")
HunterGate(
    URL "https://github.com/cpp-pm/hunter/archive/v0.23.251.tar.gz"
    SHA1 "5659b15dc0884d4b03dbd95710e6a1fa0fc3258d"
)
' CMakeLists.txt
```

### Предварительно создаем релиз нашего проекта (lab07), и посчитать его хэш SHA1

```bash
wget https://github.com/nik-olay-93/lab07/archive/refs/tags/v1.0.tar.gz

openssl sha1 v1.0.tar.gz
```

## 1. Необходимо сделать форк исходного репозитория hunter, затем редактировать hunter.cmake

```bash
git checkout -b pr.formatter_lib
```

```bash
mkdir cmake/projects/formatter_lib
cd cmake/projects/formatter_lib
vim hunter.cmake
```

```cmake
include(hunter_add_version)
include(hunter_cacheable)
include(hunter_download)
include(hunter_pick_scheme)
hunter_add_version(
	PACKAGE_NAME
	formatter_lib
	VERSION
	1.0.0
	URL
	https://github.com/nik-olay-93/lab07/archive/refs/tags/v1.0.tar.gz
	SHA1
 	bcd5a3fb752d728b801869969fac946321262299
)


hunter_pick_scheme(DEFAULT url_sha1_cmake)
hunter_cacheable(formatter_lib)
hunter_download(PACKAGE_NAME formatter_lib)
```

## 2. Необходимо сделать commit и pull-request

```bash
git add cmake/projects/formatter_lib

git commit -m "Add 'formatter_lib' package"

git checkout pr.formatter_lib
git push -u origin pr.formatter_lib
```
