## rmarkdown slides

For two columns in Rmarkdown-based slides, John Muschelli suggested
the following:

```
<div id="wrap">
<div id="left_col">

BLAHBLAH

</div>
<div id="right_col">

BLAHBLAH

</div>
</div>


#CSS
#wrap {
   width:100%;
   margin:0 auto;
}
#left_col {
   float:left;
   width:60%;
}
#right_col {
   float:right;
   width:35%;
}
```
