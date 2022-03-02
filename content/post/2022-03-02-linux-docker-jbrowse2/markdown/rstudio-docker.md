```shell
docker run -d --name rstudio -p 8787:8787 -v $(pwd):/home/rstudio -e PASSWORD=1234  -e ROOT=TRUE rocker/rstudio
```

```shell
docker run -itd --name rstudio -p 8787:8787 -v /home:/home rocker/rstudio /bin/bash
```

