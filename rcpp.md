## Rcpp notes

- top of cpp file:

      #include <Rcpp.h>
      using namespace Rcpp;

- before function definition:

      // [[Rcpp::export]]

- In R:

      Rcpp::sourceCpp("myfile.cpp")

- check for user interrupt, just:

      checkUserInterrupt(); // but for fibonacci example took like 10x longer

- random number generation

      RNGScope scope;


---

```
double, int, bool
NumericVector, IntegerVector, LogicalVector
NumericMatrix, IntegerMatrix
x.size()
x.rows()
x.cols()
std::min()
std::max()
NumericVector out(n)
NumericVector out = NumericVector::create( 1.5, 2.3 );
NA_REAL, NA_INTEGER, NA_LOGICAL
NumericVector::is_na()
break / continue
rep_len(x, n)
R::pnorm etc (see /usr/src/Rcpp/inst/include/Rcpp/Rmath.h)
R_NilValue
Rf_isNull()
```

---

## Package

- `DESCRIPTION`:

      Imports: Rcpp (>= 0.11.2)
      LinkingTo: Rcpp

- `NAMESPACE`:

      useDynLib(my_pkg)
      importFrom(Rcpp, sourceCpp)

- Might instead have

      LinkingTo: Rcpp, RcppEigen
