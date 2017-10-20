## OpenCPU

- API for R

<https://www.opencpu.org/api.html#api-package>

seems like you use `POST` to run a function

and then read the output using a key that is returned from previous request

    $ curl localhost:5732/ocpu/library/stats/R/rnorm -d "n=5&mean=500"
    /ocpu/tmp/x02d4eab0e7/R/.val
    /ocpu/tmp/x02d4eab0e7/stdout
    /ocpu/tmp/x02d4eab0e7/source
    /ocpu/tmp/x02d4eab0e7/console
    /ocpu/tmp/x02d4eab0e7/info
    /ocpu/tmp/x02d4eab0e7/files/DESCRIPTION
    $ curl localhost:5732/ocpu/tmp/x02d4eab0e7/R/.val/json
