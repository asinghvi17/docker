
<!-- README.md is generated from README.Rmd. Please edit that file -->

# Geocomputation with R in Docker

<!-- badges: start -->
[![](https://img.shields.io/docker/pulls/geocompr/geocompr.svg)](https://hub.docker.com/r/geocompr/geocompr:)
<!-- badges: end -->

This repo provides docker images on which to run code in *Geocomputation
with R*. Docker can save time by removing pain and reducing time
associated with setting-up your operating system to work with the latest
geographic packages.

To get started, after you [install
Docker](https://docs.docker.com/get-docker/), try running the following
command:

``` bash
docker run -e PASSWORD=pw --rm -p 8786:8787 geocompr/geocompr:rstudio_preview
```

Then open a browser at <http://localhost:8786/> and you should see
something like this:

![](https://user-images.githubusercontent.com/1825120/79639334-33eb9f00-8183-11ea-8358-588fe17afe25.png)
If so congratulations 🎉 you can proceed to open the `geocompr.Rproj`
project or other files in the `geocompr` folder, which contains a
complete copy of the source code and example data needed to build the
html version of the book. Use this resource to play with the examples,
develop new answers to the questions at the end of each page, or even to
generate reproducible examples to illustrate
[issues](https://github.com/Robinlovelace/geocompr/issues) with the
books contents.

If not, see documentation on using Docker at websites such as
[docker.com](https://docs.docker.com/get-started/) and
<https://www.rocker-project.org/>.

## Sharing folders with Docker

To share files on your computer with the Docker container you will need
to share volumes. You can do this using the `-v` argument as shown
below, which shares your current working directory with the Docker
container. If you run these commands in a terminal that has access to
Docker, like `bash` or Windows `PowerShell` you should get a local copy
of *Geocomputation with R* on your computer that you can use for testing
and development purposes, e.g. to test changes before submitting a Pull
Request to improve the book:

``` bash
# download repo with Windows Powershell or a Unix terminal
git clone https://github.com/Robinlovelace/geocompr.git 
# or download manually from https://github.com/Robinlovelace/geocompr/archive/master.zip
cd geocompr # navigate into the repo
# on linux and mac with password:
docker run -d -p 8786:8787 -v $(pwd):/home/rstudio/data -e USERID=$UID -e PASSWORD=pw geocompr/geocompr
# on linux and mac without password:
docker run -d -p 8786:8787 -e DISABLE_AUTH=TRUE -v $(pwd):/home/rstudio/geocompr  geocompr/geocompr
# on windows without a password:
docker run -d -p 8786:8787 -v ${pwd}:/home/rstudio/data -e DISABLE_AUTH=TRUE robinlovelace/geocompr
```

![](https://user-images.githubusercontent.com/1825120/39538109-9b50e7ac-4e33-11e8-93b3-e00e95a79294.png)

If you see something like this after following the steps above,
congratulations: it worked\! See
[github.com/rocker-org](https://github.com/rocker-org/rocker/wiki/Using-the-RStudio-image#running-rstudio-server)
for more info.

From this point to *build* the book you can open projects in the
`geocompr` directory from the project box in the top-right hand corner,
and knit `index.Rmd` with the little `knit` button above the the RStudio
script panel (`Ctl+Shift+B` should do the same job).

There are various versions of the `geocompr` Docker image available. The
default is `rstudio_preview`, but you can get other images, as outlined
below.

## Versions

Building on the
[rocker-org](https://github.com/rocker-org/rocker-versioned/blob/master/README.md)
project, we provide various versions for testing and development,
including builds that use more up-to-date versions of OSGeo packages
such as GDAL provided by the [UbuntuGIS software
repository](https://wiki.ubuntu.com/UbuntuGIS), as shown below:

| image                                                                      | description                                  | size                                                                               |
| -------------------------------------------------------------------------- | -------------------------------------------- | ---------------------------------------------------------------------------------- |
| [geocompr](https://hub.docker.com/r/geocompr/geocompr)                     | Default repos on Ubuntu                      | ![](https://img.shields.io/docker/image-size/geocompr/geocompr?sort=date)          |
| [geocompr:default\_repos](https://hub.docker.com/r/geocompr/geocompr)      | Default repos on Ubuntu                      | ![](https://img.shields.io/docker/image-size/geocompr/geocompr/default_repos)      |
| [geocompr:ubuntugis\_stable](https://hub.docker.com/r/geocompr/geocompr)   | UbuntuGIS stable repo                        | ![](https://img.shields.io/docker/image-size/geocompr/geocompr/ubuntugis_stable)   |
| [geocompr:ubuntugis\_unstable](https://hub.docker.com/r/geocompr/geocompr) | UbuntuGIS unstable repos on Ubuntu           | ![](https://img.shields.io/docker/image-size/geocompr/geocompr/ubuntugis_unstable) |
| [geocompr:rstudio\_preview](https://hub.docker.com/r/geocompr/geocompr)    | UbuntuGIS Unstable repos and RStudio Preview | ![](https://img.shields.io/docker/image-size/geocompr/geocompr/rstudio_preview)    |
| [geocompr:rstudio\_devel](https://hub.docker.com/r/geocompr/geocompr)      | UbuntuGIS Unstable repos and R devel         | ![](https://img.shields.io/docker/image-size/geocompr/geocompr/rstudio_devel)      |

Add :tagname to geocompr/geocompr to get the tag you’re interested in.

To run the `rstudio_preview` version, for example, run the following
command (with port and password set to a port of your preference):

``` bash
docker run -e PASSWORD=pw --rm -p 8786:8787 geocompr/geocompr:rstudio_preview
```

Adding `_buildbook` to a tag will give you an image with the pre-built
book (added by default in the `rstudio_` versions), e.g.:

``` bash
docker run -e PASSWORD=pw --rm -p 8786:8787 geocompr/geocompr:ubuntugis_unstable_buildbook
```

## Details

The base image is `rockerdev/geospatial:3.6.3` from
[github.com/rocker-org/rocker-versioned2](https://github.com/rocker-org/rocker-versioned2/blob/master/dockerfiles/Dockerfile_geospatial_3.6.3).

To build on different system configurations we provide tags that
correspond to the following categories:

`baseimage-ubuntugis-setup-rpackages-buildbook`

The default base image is `rockerdev/geospatial:3.6.3`. More images may
be added in the future.

``` r
baseimage = c(
  rockerdev_geospatial_3.6.3 = ""
)
```

Ubuntugis options include using the `ubuntugis-unstable` and
`ubuntugis-stable` repos.

``` r
ubuntugis = c(
  no_ubuntugis = "default_repos",
  ubuntugis_unstable = "ubuntugis_unstable",
  ubuntugis_stable = "ubuntugis_stable"
)
```

Setup options can include RStudio settings (yet to be added).

R package options relate to which R packages are installed on the image
(yet to be added).

Buildbook options report whether or not the book is built:

``` r
buildbook = c(
  no = "",
  yes = "buildbook"
)
```

We will create a ‘build matrix’ covering all combinations of these
options (excluding the base image for now):

``` r
g = expand.grid(ubuntugis, buildbook, stringsAsFactors = FALSE)
g
#>                 Var1      Var2
#> 1      default_repos          
#> 2 ubuntugis_unstable          
#> 3   ubuntugis_stable          
#> 4      default_repos buildbook
#> 5 ubuntugis_unstable buildbook
#> 6   ubuntugis_stable buildbook
```

These can be converted into tags as follows:

``` r
tag_df = tidyr::unite(g, tag)
tags = gsub(pattern = "__|^_|_$", replacement = "", tag_df$tag)
tags
#> [1] "default_repos"                "ubuntugis_unstable"          
#> [3] "ubuntugis_stable"             "default_repos_buildbook"     
#> [5] "ubuntugis_unstable_buildbook" "ubuntugis_stable_buildbook"
```

We could write code to auto-generate Dockerfiles, as demonstrated in
[rocker-org/rocker-versioned2](https://github.com/rocker-org/rocker-versioned2).

For now, to start the project going, we will manually edit the files,
which can be created as follows:

``` r
new_dockerfiles = paste0("dockerfiles/Dockerfile_", tags)
new_dockerfiles
lapply(new_dockerfiles, file.copy, from = "rockerdev-ubuntugis-bookbuild/Dockerfile", TRUE)
```

Edit these files as appropriate:

``` r
file.edit("dockerfiles/Dockerfile_ubuntugis_unstable")
```

Create a folder for each Dockerfile:

``` r
lapply(tags, dir.create)
lapply(tags, function(x) {
  file.copy(
    from = paste0("dockerfiles/Dockerfile_", x),
    , to = paste0(x, "/Dockerfile"),
    overwrite = TRUE)
})
```

Test the build in a terminal, e.g. with the following command

``` bash
docker build ubuntugis_unstable
```
