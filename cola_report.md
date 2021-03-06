cola Report for recount2:SRP014574
==================

**Date**: 2019-12-25 23:21:35 CET, **cola version**: 1.3.2

----------------------------------------------------------------

<style type='text/css'>

body, td, th {
   font-family: Arial,Helvetica,sans-serif;
   background-color: white;
   font-size: 13px;
  max-width: 800px;
  margin: auto;
  margin-left:210px;
  padding: 0px 10px 0px 10px;
  border-left: 1px solid #EEEEEE;
  line-height: 150%;
}

tt, code, pre {
   font-family: 'DejaVu Sans Mono', 'Droid Sans Mono', 'Lucida Console', Consolas, Monaco, 

monospace;
}

h1 {
   font-size:2.2em;
}

h2 {
   font-size:1.8em;
}

h3 {
   font-size:1.4em;
}

h4 {
   font-size:1.0em;
}

h5 {
   font-size:0.9em;
}

h6 {
   font-size:0.8em;
}

a {
  text-decoration: none;
  color: #0366d6;
}

a:hover {
  text-decoration: underline;
}

a:visited {
   color: #0366d6;
}

pre, img {
  max-width: 100%;
}
pre {
  overflow-x: auto;
}
pre code {
   display: block; padding: 0.5em;
}

code {
  font-size: 92%;
  border: 1px solid #ccc;
}

code[class] {
  background-color: #F8F8F8;
}

table, td, th {
  border: 1px solid #ccc;
}

blockquote {
   color:#666666;
   margin:0;
   padding-left: 1em;
   border-left: 0.5em #EEE solid;
}

hr {
   height: 0px;
   border-bottom: none;
   border-top-width: thin;
   border-top-style: dotted;
   border-top-color: #999999;
}

@media print {
   * {
      background: transparent !important;
      color: black !important;
      filter:none !important;
      -ms-filter: none !important;
   }

   body {
      font-size:12pt;
      max-width:100%;
   }

   a, a:visited {
      text-decoration: underline;
   }

   hr {
      visibility: hidden;
      page-break-before: always;
   }

   pre, blockquote {
      padding-right: 1em;
      page-break-inside: avoid;
   }

   tr, img {
      page-break-inside: avoid;
   }

   img {
      max-width: 100% !important;
   }

   @page :left {
      margin: 15mm 20mm 15mm 10mm;
   }

   @page :right {
      margin: 15mm 10mm 15mm 20mm;
   }

   p, h2, h3 {
      orphans: 3; widows: 3;
   }

   h2, h3 {
      page-break-after: avoid;
   }
}
</style>




## Summary





All available functions which can be applied to this `res_list` object:


```r
res_list
```

```
#> A 'ConsensusPartitionList' object with 24 methods.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows are extracted by 'SD, CV, MAD, ATC' methods.
#>   Subgroups are detected by 'hclust, kmeans, skmeans, pam, mclust, NMF' method.
#>   Number of partitions are tried for k = 2, 3, 4, 5, 6.
#>   Performed in total 30000 partitions by row resampling.
#> 
#> Following methods can be applied to this 'ConsensusPartitionList' object:
#>  [1] "cola_report"           "collect_classes"       "collect_plots"         "collect_stats"        
#>  [5] "colnames"              "functional_enrichment" "get_anno_col"          "get_anno"             
#>  [9] "get_classes"           "get_matrix"            "get_membership"        "get_stats"            
#> [13] "is_best_k"             "is_stable_k"           "ncol"                  "nrow"                 
#> [17] "rownames"              "show"                  "suggest_best_k"        "test_to_known_factors"
#> [21] "top_rows_heatmap"      "top_rows_overlap"     
#> 
#> You can get result for a single method by, e.g. object["SD", "hclust"] or object["SD:hclust"]
#> or a subset of methods by object[c("SD", "CV")], c("hclust", "kmeans")]
```

The call of `run_all_consensus_partition_methods()` was:


```
#> run_all_consensus_partition_methods(data = mat, mc.cores = 4)
```

Dimension of the input matrix:


```r
mat = get_matrix(res_list)
dim(mat)
```

```
#> [1] 16748    53
```

### Density distribution

The density distribution for each sample is visualized as in one column in the
following heatmap. The clustering is based on the distance which is the
Kolmogorov-Smirnov statistic between two distributions.




```r
library(ComplexHeatmap)
densityHeatmap(mat, ylab = "value", cluster_columns = TRUE, show_column_names = FALSE,
    mc.cores = 4)
```

![plot of chunk density-heatmap](figure_cola/density-heatmap-1.png)





### Suggest the best k



Folowing table shows the best `k` (number of partitions) for each combination
of top-value methods and partition methods. Clicking on the method name in
the table goes to the section for a single combination of methods.

[The cola vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13)
explains the definition of the metrics used for determining the best
number of partitions.


```r
suggest_best_k(res_list)
```


|                            | The best k| 1-PAC| Mean silhouette| Concordance|   |Optional k |
|:---------------------------|----------:|-----:|---------------:|-----------:|:--|:----------|
|[SD:hclust](#SD-hclust)     |          2| 1.000|           0.977|       0.992|** |           |
|[SD:kmeans](#SD-kmeans)     |          2| 1.000|           0.993|       0.994|** |           |
|[SD:NMF](#SD-NMF)           |          2| 1.000|           0.982|       0.991|** |           |
|[CV:hclust](#CV-hclust)     |          2| 1.000|           0.979|       0.988|** |           |
|[CV:kmeans](#CV-kmeans)     |          2| 1.000|           1.000|       1.000|** |           |
|[CV:skmeans](#CV-skmeans)   |          3| 1.000|           1.000|       1.000|** |2          |
|[CV:pam](#CV-pam)           |          2| 1.000|           0.975|       0.991|** |           |
|[MAD:hclust](#MAD-hclust)   |          2| 1.000|           0.986|       0.994|** |           |
|[MAD:kmeans](#MAD-kmeans)   |          2| 1.000|           0.980|       0.992|** |           |
|[ATC:kmeans](#ATC-kmeans)   |          2| 1.000|           0.995|       0.993|** |           |
|[CV:mclust](#CV-mclust)     |          3| 0.986|           0.951|       0.979|** |2          |
|[ATC:hclust](#ATC-hclust)   |          6| 0.985|           0.922|       0.970|** |5          |
|[ATC:mclust](#ATC-mclust)   |          4| 0.976|           0.920|       0.969|** |2          |
|[ATC:pam](#ATC-pam)         |          6| 0.969|           0.928|       0.972|** |2,4,5      |
|[MAD:pam](#MAD-pam)         |          6| 0.964|           0.928|       0.974|** |2,5        |
|[MAD:NMF](#MAD-NMF)         |          2| 0.958|           0.940|       0.976|** |           |
|[SD:skmeans](#SD-skmeans)   |          5| 0.953|           0.953|       0.956|** |2,4        |
|[MAD:skmeans](#MAD-skmeans) |          6| 0.936|           0.812|       0.892|*  |2,4,5      |
|[CV:NMF](#CV-NMF)           |          4| 0.935|           0.981|       0.969|*  |2          |
|[ATC:NMF](#ATC-NMF)         |          3| 0.922|           0.940|       0.974|*  |           |
|[SD:pam](#SD-pam)           |          6| 0.918|           0.883|       0.953|*  |2,5        |
|[SD:mclust](#SD-mclust)     |          6| 0.918|           0.860|       0.934|*  |5          |
|[MAD:mclust](#MAD-mclust)   |          6| 0.915|           0.878|       0.944|*  |2          |
|[ATC:skmeans](#ATC-skmeans) |          6| 0.904|           0.872|       0.909|*  |2,3        |

\*\*: 1-PAC > 0.95, \*: 1-PAC > 0.9




### CDF of consensus matrices

Cumulative distribution function curves of consensus matrix for all methods.




```r
collect_plots(res_list, fun = plot_ecdf)
```

![plot of chunk collect-plots](figure_cola/collect-plots-1.png)



### Consensus heatmap

Consensus heatmaps for all methods. ([What is a consensus heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_9))


<style type='text/css'>



.ui-helper-hidden {
	display: none;
}
.ui-helper-hidden-accessible {
	border: 0;
	clip: rect(0 0 0 0);
	height: 1px;
	margin: -1px;
	overflow: hidden;
	padding: 0;
	position: absolute;
	width: 1px;
}
.ui-helper-reset {
	margin: 0;
	padding: 0;
	border: 0;
	outline: 0;
	line-height: 1.3;
	text-decoration: none;
	font-size: 100%;
	list-style: none;
}
.ui-helper-clearfix:before,
.ui-helper-clearfix:after {
	content: "";
	display: table;
	border-collapse: collapse;
}
.ui-helper-clearfix:after {
	clear: both;
}
.ui-helper-zfix {
	width: 100%;
	height: 100%;
	top: 0;
	left: 0;
	position: absolute;
	opacity: 0;
	filter:Alpha(Opacity=0); 
}

.ui-front {
	z-index: 100;
}



.ui-state-disabled {
	cursor: default !important;
	pointer-events: none;
}



.ui-icon {
	display: inline-block;
	vertical-align: middle;
	margin-top: -.25em;
	position: relative;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
}

.ui-widget-icon-block {
	left: 50%;
	margin-left: -8px;
	display: block;
}




.ui-widget-overlay {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
}
.ui-accordion .ui-accordion-header {
	display: block;
	cursor: pointer;
	position: relative;
	margin: 2px 0 0 0;
	padding: .5em .5em .5em .7em;
	font-size: 100%;
}
.ui-accordion .ui-accordion-content {
	padding: 1em 2.2em;
	border-top: 0;
	overflow: auto;
}
.ui-autocomplete {
	position: absolute;
	top: 0;
	left: 0;
	cursor: default;
}
.ui-menu {
	list-style: none;
	padding: 0;
	margin: 0;
	display: block;
	outline: 0;
}
.ui-menu .ui-menu {
	position: absolute;
}
.ui-menu .ui-menu-item {
	margin: 0;
	cursor: pointer;
	
	list-style-image: url("data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7");
}
.ui-menu .ui-menu-item-wrapper {
	position: relative;
	padding: 3px 1em 3px .4em;
}
.ui-menu .ui-menu-divider {
	margin: 5px 0;
	height: 0;
	font-size: 0;
	line-height: 0;
	border-width: 1px 0 0 0;
}
.ui-menu .ui-state-focus,
.ui-menu .ui-state-active {
	margin: -1px;
}


.ui-menu-icons {
	position: relative;
}
.ui-menu-icons .ui-menu-item-wrapper {
	padding-left: 2em;
}


.ui-menu .ui-icon {
	position: absolute;
	top: 0;
	bottom: 0;
	left: .2em;
	margin: auto 0;
}


.ui-menu .ui-menu-icon {
	left: auto;
	right: 0;
}
.ui-button {
	padding: .4em 1em;
	display: inline-block;
	position: relative;
	line-height: normal;
	margin-right: .1em;
	cursor: pointer;
	vertical-align: middle;
	text-align: center;
	-webkit-user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	user-select: none;

	
	overflow: visible;
}

.ui-button,
.ui-button:link,
.ui-button:visited,
.ui-button:hover,
.ui-button:active {
	text-decoration: none;
}


.ui-button-icon-only {
	width: 2em;
	box-sizing: border-box;
	text-indent: -9999px;
	white-space: nowrap;
}


input.ui-button.ui-button-icon-only {
	text-indent: 0;
}


.ui-button-icon-only .ui-icon {
	position: absolute;
	top: 50%;
	left: 50%;
	margin-top: -8px;
	margin-left: -8px;
}

.ui-button.ui-icon-notext .ui-icon {
	padding: 0;
	width: 2.1em;
	height: 2.1em;
	text-indent: -9999px;
	white-space: nowrap;

}

input.ui-button.ui-icon-notext .ui-icon {
	width: auto;
	height: auto;
	text-indent: 0;
	white-space: normal;
	padding: .4em 1em;
}



input.ui-button::-moz-focus-inner,
button.ui-button::-moz-focus-inner {
	border: 0;
	padding: 0;
}
.ui-controlgroup {
	vertical-align: middle;
	display: inline-block;
}
.ui-controlgroup > .ui-controlgroup-item {
	float: left;
	margin-left: 0;
	margin-right: 0;
}
.ui-controlgroup > .ui-controlgroup-item:focus,
.ui-controlgroup > .ui-controlgroup-item.ui-visual-focus {
	z-index: 9999;
}
.ui-controlgroup-vertical > .ui-controlgroup-item {
	display: block;
	float: none;
	width: 100%;
	margin-top: 0;
	margin-bottom: 0;
	text-align: left;
}
.ui-controlgroup-vertical .ui-controlgroup-item {
	box-sizing: border-box;
}
.ui-controlgroup .ui-controlgroup-label {
	padding: .4em 1em;
}
.ui-controlgroup .ui-controlgroup-label span {
	font-size: 80%;
}
.ui-controlgroup-horizontal .ui-controlgroup-label + .ui-controlgroup-item {
	border-left: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label + .ui-controlgroup-item {
	border-top: none;
}
.ui-controlgroup-horizontal .ui-controlgroup-label.ui-widget-content {
	border-right: none;
}
.ui-controlgroup-vertical .ui-controlgroup-label.ui-widget-content {
	border-bottom: none;
}


.ui-controlgroup-vertical .ui-spinner-input {

	
	width: 75%;
	width: calc( 100% - 2.4em );
}
.ui-controlgroup-vertical .ui-spinner .ui-spinner-up {
	border-top-style: solid;
}

.ui-checkboxradio-label .ui-icon-background {
	box-shadow: inset 1px 1px 1px #ccc;
	border-radius: .12em;
	border: none;
}
.ui-checkboxradio-radio-label .ui-icon-background {
	width: 16px;
	height: 16px;
	border-radius: 1em;
	overflow: visible;
	border: none;
}
.ui-checkboxradio-radio-label.ui-checkboxradio-checked .ui-icon,
.ui-checkboxradio-radio-label.ui-checkboxradio-checked:hover .ui-icon {
	background-image: none;
	width: 8px;
	height: 8px;
	border-width: 4px;
	border-style: solid;
}
.ui-checkboxradio-disabled {
	pointer-events: none;
}
.ui-datepicker {
	width: 17em;
	padding: .2em .2em 0;
	display: none;
}
.ui-datepicker .ui-datepicker-header {
	position: relative;
	padding: .2em 0;
}
.ui-datepicker .ui-datepicker-prev,
.ui-datepicker .ui-datepicker-next {
	position: absolute;
	top: 2px;
	width: 1.8em;
	height: 1.8em;
}
.ui-datepicker .ui-datepicker-prev-hover,
.ui-datepicker .ui-datepicker-next-hover {
	top: 1px;
}
.ui-datepicker .ui-datepicker-prev {
	left: 2px;
}
.ui-datepicker .ui-datepicker-next {
	right: 2px;
}
.ui-datepicker .ui-datepicker-prev-hover {
	left: 1px;
}
.ui-datepicker .ui-datepicker-next-hover {
	right: 1px;
}
.ui-datepicker .ui-datepicker-prev span,
.ui-datepicker .ui-datepicker-next span {
	display: block;
	position: absolute;
	left: 50%;
	margin-left: -8px;
	top: 50%;
	margin-top: -8px;
}
.ui-datepicker .ui-datepicker-title {
	margin: 0 2.3em;
	line-height: 1.8em;
	text-align: center;
}
.ui-datepicker .ui-datepicker-title select {
	font-size: 1em;
	margin: 1px 0;
}
.ui-datepicker select.ui-datepicker-month,
.ui-datepicker select.ui-datepicker-year {
	width: 45%;
}
.ui-datepicker table {
	width: 100%;
	font-size: .9em;
	border-collapse: collapse;
	margin: 0 0 .4em;
}
.ui-datepicker th {
	padding: .7em .3em;
	text-align: center;
	font-weight: bold;
	border: 0;
}
.ui-datepicker td {
	border: 0;
	padding: 1px;
}
.ui-datepicker td span,
.ui-datepicker td a {
	display: block;
	padding: .2em;
	text-align: right;
	text-decoration: none;
}
.ui-datepicker .ui-datepicker-buttonpane {
	background-image: none;
	margin: .7em 0 0 0;
	padding: 0 .2em;
	border-left: 0;
	border-right: 0;
	border-bottom: 0;
}
.ui-datepicker .ui-datepicker-buttonpane button {
	float: right;
	margin: .5em .2em .4em;
	cursor: pointer;
	padding: .2em .6em .3em .6em;
	width: auto;
	overflow: visible;
}
.ui-datepicker .ui-datepicker-buttonpane button.ui-datepicker-current {
	float: left;
}


.ui-datepicker.ui-datepicker-multi {
	width: auto;
}
.ui-datepicker-multi .ui-datepicker-group {
	float: left;
}
.ui-datepicker-multi .ui-datepicker-group table {
	width: 95%;
	margin: 0 auto .4em;
}
.ui-datepicker-multi-2 .ui-datepicker-group {
	width: 50%;
}
.ui-datepicker-multi-3 .ui-datepicker-group {
	width: 33.3%;
}
.ui-datepicker-multi-4 .ui-datepicker-group {
	width: 25%;
}
.ui-datepicker-multi .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-multi .ui-datepicker-group-middle .ui-datepicker-header {
	border-left-width: 0;
}
.ui-datepicker-multi .ui-datepicker-buttonpane {
	clear: left;
}
.ui-datepicker-row-break {
	clear: both;
	width: 100%;
	font-size: 0;
}


.ui-datepicker-rtl {
	direction: rtl;
}
.ui-datepicker-rtl .ui-datepicker-prev {
	right: 2px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next {
	left: 2px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-prev:hover {
	right: 1px;
	left: auto;
}
.ui-datepicker-rtl .ui-datepicker-next:hover {
	left: 1px;
	right: auto;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane {
	clear: right;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button {
	float: left;
}
.ui-datepicker-rtl .ui-datepicker-buttonpane button.ui-datepicker-current,
.ui-datepicker-rtl .ui-datepicker-group {
	float: right;
}
.ui-datepicker-rtl .ui-datepicker-group-last .ui-datepicker-header,
.ui-datepicker-rtl .ui-datepicker-group-middle .ui-datepicker-header {
	border-right-width: 0;
	border-left-width: 1px;
}


.ui-datepicker .ui-icon {
	display: block;
	text-indent: -99999px;
	overflow: hidden;
	background-repeat: no-repeat;
	left: .5em;
	top: .3em;
}
.ui-dialog {
	position: absolute;
	top: 0;
	left: 0;
	padding: .2em;
	outline: 0;
}
.ui-dialog .ui-dialog-titlebar {
	padding: .4em 1em;
	position: relative;
}
.ui-dialog .ui-dialog-title {
	float: left;
	margin: .1em 0;
	white-space: nowrap;
	width: 90%;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-dialog .ui-dialog-titlebar-close {
	position: absolute;
	right: .3em;
	top: 50%;
	width: 20px;
	margin: -10px 0 0 0;
	padding: 1px;
	height: 20px;
}
.ui-dialog .ui-dialog-content {
	position: relative;
	border: 0;
	padding: .5em 1em;
	background: none;
	overflow: auto;
}
.ui-dialog .ui-dialog-buttonpane {
	text-align: left;
	border-width: 1px 0 0 0;
	background-image: none;
	margin-top: .5em;
	padding: .3em 1em .5em .4em;
}
.ui-dialog .ui-dialog-buttonpane .ui-dialog-buttonset {
	float: right;
}
.ui-dialog .ui-dialog-buttonpane button {
	margin: .5em .4em .5em 0;
	cursor: pointer;
}
.ui-dialog .ui-resizable-n {
	height: 2px;
	top: 0;
}
.ui-dialog .ui-resizable-e {
	width: 2px;
	right: 0;
}
.ui-dialog .ui-resizable-s {
	height: 2px;
	bottom: 0;
}
.ui-dialog .ui-resizable-w {
	width: 2px;
	left: 0;
}
.ui-dialog .ui-resizable-se,
.ui-dialog .ui-resizable-sw,
.ui-dialog .ui-resizable-ne,
.ui-dialog .ui-resizable-nw {
	width: 7px;
	height: 7px;
}
.ui-dialog .ui-resizable-se {
	right: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-sw {
	left: 0;
	bottom: 0;
}
.ui-dialog .ui-resizable-ne {
	right: 0;
	top: 0;
}
.ui-dialog .ui-resizable-nw {
	left: 0;
	top: 0;
}
.ui-draggable .ui-dialog-titlebar {
	cursor: move;
}
.ui-draggable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable {
	position: relative;
}
.ui-resizable-handle {
	position: absolute;
	font-size: 0.1px;
	display: block;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-resizable-disabled .ui-resizable-handle,
.ui-resizable-autohide .ui-resizable-handle {
	display: none;
}
.ui-resizable-n {
	cursor: n-resize;
	height: 7px;
	width: 100%;
	top: -5px;
	left: 0;
}
.ui-resizable-s {
	cursor: s-resize;
	height: 7px;
	width: 100%;
	bottom: -5px;
	left: 0;
}
.ui-resizable-e {
	cursor: e-resize;
	width: 7px;
	right: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-w {
	cursor: w-resize;
	width: 7px;
	left: -5px;
	top: 0;
	height: 100%;
}
.ui-resizable-se {
	cursor: se-resize;
	width: 12px;
	height: 12px;
	right: 1px;
	bottom: 1px;
}
.ui-resizable-sw {
	cursor: sw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	bottom: -5px;
}
.ui-resizable-nw {
	cursor: nw-resize;
	width: 9px;
	height: 9px;
	left: -5px;
	top: -5px;
}
.ui-resizable-ne {
	cursor: ne-resize;
	width: 9px;
	height: 9px;
	right: -5px;
	top: -5px;
}
.ui-progressbar {
	height: 2em;
	text-align: left;
	overflow: hidden;
}
.ui-progressbar .ui-progressbar-value {
	margin: -1px;
	height: 100%;
}
.ui-progressbar .ui-progressbar-overlay {
	background: url("data:image/gif;base64,R0lGODlhKAAoAIABAAAAAP///yH/C05FVFNDQVBFMi4wAwEAAAAh+QQJAQABACwAAAAAKAAoAAACkYwNqXrdC52DS06a7MFZI+4FHBCKoDeWKXqymPqGqxvJrXZbMx7Ttc+w9XgU2FB3lOyQRWET2IFGiU9m1frDVpxZZc6bfHwv4c1YXP6k1Vdy292Fb6UkuvFtXpvWSzA+HycXJHUXiGYIiMg2R6W459gnWGfHNdjIqDWVqemH2ekpObkpOlppWUqZiqr6edqqWQAAIfkECQEAAQAsAAAAACgAKAAAApSMgZnGfaqcg1E2uuzDmmHUBR8Qil95hiPKqWn3aqtLsS18y7G1SzNeowWBENtQd+T1JktP05nzPTdJZlR6vUxNWWjV+vUWhWNkWFwxl9VpZRedYcflIOLafaa28XdsH/ynlcc1uPVDZxQIR0K25+cICCmoqCe5mGhZOfeYSUh5yJcJyrkZWWpaR8doJ2o4NYq62lAAACH5BAkBAAEALAAAAAAoACgAAAKVDI4Yy22ZnINRNqosw0Bv7i1gyHUkFj7oSaWlu3ovC8GxNso5fluz3qLVhBVeT/Lz7ZTHyxL5dDalQWPVOsQWtRnuwXaFTj9jVVh8pma9JjZ4zYSj5ZOyma7uuolffh+IR5aW97cHuBUXKGKXlKjn+DiHWMcYJah4N0lYCMlJOXipGRr5qdgoSTrqWSq6WFl2ypoaUAAAIfkECQEAAQAsAAAAACgAKAAAApaEb6HLgd/iO7FNWtcFWe+ufODGjRfoiJ2akShbueb0wtI50zm02pbvwfWEMWBQ1zKGlLIhskiEPm9R6vRXxV4ZzWT2yHOGpWMyorblKlNp8HmHEb/lCXjcW7bmtXP8Xt229OVWR1fod2eWqNfHuMjXCPkIGNileOiImVmCOEmoSfn3yXlJWmoHGhqp6ilYuWYpmTqKUgAAIfkECQEAAQAsAAAAACgAKAAAApiEH6kb58biQ3FNWtMFWW3eNVcojuFGfqnZqSebuS06w5V80/X02pKe8zFwP6EFWOT1lDFk8rGERh1TTNOocQ61Hm4Xm2VexUHpzjymViHrFbiELsefVrn6XKfnt2Q9G/+Xdie499XHd2g4h7ioOGhXGJboGAnXSBnoBwKYyfioubZJ2Hn0RuRZaflZOil56Zp6iioKSXpUAAAh+QQJAQABACwAAAAAKAAoAAACkoQRqRvnxuI7kU1a1UU5bd5tnSeOZXhmn5lWK3qNTWvRdQxP8qvaC+/yaYQzXO7BMvaUEmJRd3TsiMAgswmNYrSgZdYrTX6tSHGZO73ezuAw2uxuQ+BbeZfMxsexY35+/Qe4J1inV0g4x3WHuMhIl2jXOKT2Q+VU5fgoSUI52VfZyfkJGkha6jmY+aaYdirq+lQAACH5BAkBAAEALAAAAAAoACgAAAKWBIKpYe0L3YNKToqswUlvznigd4wiR4KhZrKt9Upqip61i9E3vMvxRdHlbEFiEXfk9YARYxOZZD6VQ2pUunBmtRXo1Lf8hMVVcNl8JafV38aM2/Fu5V16Bn63r6xt97j09+MXSFi4BniGFae3hzbH9+hYBzkpuUh5aZmHuanZOZgIuvbGiNeomCnaxxap2upaCZsq+1kAACH5BAkBAAEALAAAAAAoACgAAAKXjI8By5zf4kOxTVrXNVlv1X0d8IGZGKLnNpYtm8Lr9cqVeuOSvfOW79D9aDHizNhDJidFZhNydEahOaDH6nomtJjp1tutKoNWkvA6JqfRVLHU/QUfau9l2x7G54d1fl995xcIGAdXqMfBNadoYrhH+Mg2KBlpVpbluCiXmMnZ2Sh4GBqJ+ckIOqqJ6LmKSllZmsoq6wpQAAAh+QQJAQABACwAAAAAKAAoAAAClYx/oLvoxuJDkU1a1YUZbJ59nSd2ZXhWqbRa2/gF8Gu2DY3iqs7yrq+xBYEkYvFSM8aSSObE+ZgRl1BHFZNr7pRCavZ5BW2142hY3AN/zWtsmf12p9XxxFl2lpLn1rseztfXZjdIWIf2s5dItwjYKBgo9yg5pHgzJXTEeGlZuenpyPmpGQoKOWkYmSpaSnqKileI2FAAACH5BAkBAAEALAAAAAAoACgAAAKVjB+gu+jG4kORTVrVhRlsnn2dJ3ZleFaptFrb+CXmO9OozeL5VfP99HvAWhpiUdcwkpBH3825AwYdU8xTqlLGhtCosArKMpvfa1mMRae9VvWZfeB2XfPkeLmm18lUcBj+p5dnN8jXZ3YIGEhYuOUn45aoCDkp16hl5IjYJvjWKcnoGQpqyPlpOhr3aElaqrq56Bq7VAAAOw==");
	height: 100%;
	filter: alpha(opacity=25); 
	opacity: 0.25;
}
.ui-progressbar-indeterminate .ui-progressbar-value {
	background-image: none;
}
.ui-selectable {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-selectable-helper {
	position: absolute;
	z-index: 100;
	border: 1px dotted black;
}
.ui-selectmenu-menu {
	padding: 0;
	margin: 0;
	position: absolute;
	top: 0;
	left: 0;
	display: none;
}
.ui-selectmenu-menu .ui-menu {
	overflow: auto;
	overflow-x: hidden;
	padding-bottom: 1px;
}
.ui-selectmenu-menu .ui-menu .ui-selectmenu-optgroup {
	font-size: 1em;
	font-weight: bold;
	line-height: 1.5;
	padding: 2px 0.4em;
	margin: 0.5em 0 0 0;
	height: auto;
	border: 0;
}
.ui-selectmenu-open {
	display: block;
}
.ui-selectmenu-text {
	display: block;
	margin-right: 20px;
	overflow: hidden;
	text-overflow: ellipsis;
}
.ui-selectmenu-button.ui-button {
	text-align: left;
	white-space: nowrap;
	width: 14em;
}
.ui-selectmenu-icon.ui-icon {
	float: right;
	margin-top: 0;
}
.ui-slider {
	position: relative;
	text-align: left;
}
.ui-slider .ui-slider-handle {
	position: absolute;
	z-index: 2;
	width: 1.2em;
	height: 1.2em;
	cursor: default;
	-ms-touch-action: none;
	touch-action: none;
}
.ui-slider .ui-slider-range {
	position: absolute;
	z-index: 1;
	font-size: .7em;
	display: block;
	border: 0;
	background-position: 0 0;
}


.ui-slider.ui-state-disabled .ui-slider-handle,
.ui-slider.ui-state-disabled .ui-slider-range {
	filter: inherit;
}

.ui-slider-horizontal {
	height: .8em;
}
.ui-slider-horizontal .ui-slider-handle {
	top: -.3em;
	margin-left: -.6em;
}
.ui-slider-horizontal .ui-slider-range {
	top: 0;
	height: 100%;
}
.ui-slider-horizontal .ui-slider-range-min {
	left: 0;
}
.ui-slider-horizontal .ui-slider-range-max {
	right: 0;
}

.ui-slider-vertical {
	width: .8em;
	height: 100px;
}
.ui-slider-vertical .ui-slider-handle {
	left: -.3em;
	margin-left: 0;
	margin-bottom: -.6em;
}
.ui-slider-vertical .ui-slider-range {
	left: 0;
	width: 100%;
}
.ui-slider-vertical .ui-slider-range-min {
	bottom: 0;
}
.ui-slider-vertical .ui-slider-range-max {
	top: 0;
}
.ui-sortable-handle {
	-ms-touch-action: none;
	touch-action: none;
}
.ui-spinner {
	position: relative;
	display: inline-block;
	overflow: hidden;
	padding: 0;
	vertical-align: middle;
}
.ui-spinner-input {
	border: none;
	background: none;
	color: inherit;
	padding: .222em 0;
	margin: .2em 0;
	vertical-align: middle;
	margin-left: .4em;
	margin-right: 2em;
}
.ui-spinner-button {
	width: 1.6em;
	height: 50%;
	font-size: .5em;
	padding: 0;
	margin: 0;
	text-align: center;
	position: absolute;
	cursor: default;
	display: block;
	overflow: hidden;
	right: 0;
}

.ui-spinner a.ui-spinner-button {
	border-top-style: none;
	border-bottom-style: none;
	border-right-style: none;
}
.ui-spinner-up {
	top: 0;
}
.ui-spinner-down {
	bottom: 0;
}
.ui-tabs {
	position: relative;
	padding: .2em;
}
.ui-tabs .ui-tabs-nav {
	margin: 0;
	padding: .2em .2em 0;
}
.ui-tabs .ui-tabs-nav li {
	list-style: none;
	float: left;
	position: relative;
	top: 0;
	margin: 1px .2em 0 0;
	border-bottom-width: 0;
	padding: 0;
	white-space: nowrap;
}
.ui-tabs .ui-tabs-nav .ui-tabs-anchor {
	float: left;
	padding: .5em 1em;
	text-decoration: none;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active {
	margin-bottom: -1px;
	padding-bottom: 1px;
}
.ui-tabs .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-state-disabled .ui-tabs-anchor,
.ui-tabs .ui-tabs-nav li.ui-tabs-loading .ui-tabs-anchor {
	cursor: text;
}
.ui-tabs-collapsible .ui-tabs-nav li.ui-tabs-active .ui-tabs-anchor {
	cursor: pointer;
}
.ui-tabs .ui-tabs-panel {
	display: block;
	border-width: 0;
	padding: 1em 1.4em;
	background: none;
}
.ui-tooltip {
	padding: 8px;
	position: absolute;
	z-index: 9999;
	max-width: 300px;
}
body .ui-tooltip {
	border-width: 2px;
}

.ui-widget {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget .ui-widget {
	font-size: 1em;
}
.ui-widget input,
.ui-widget select,
.ui-widget textarea,
.ui-widget button {
	font-family: Arial,Helvetica,sans-serif;
	font-size: 1em;
}
.ui-widget.ui-widget-content {
	border: 1px solid #c5c5c5;
}
.ui-widget-content {
	border: 1px solid #dddddd;
	background: #ffffff;
	color: #333333;
}
.ui-widget-content a {
	color: #333333;
}
.ui-widget-header {
	border: 1px solid #dddddd;
	background: #e9e9e9;
	color: #333333;
	font-weight: bold;
}
.ui-widget-header a {
	color: #333333;
}


.ui-state-default,
.ui-widget-content .ui-state-default,
.ui-widget-header .ui-state-default,
.ui-button,


html .ui-button.ui-state-disabled:hover,
html .ui-button.ui-state-disabled:active {
	border: 1px solid #c5c5c5;
	background: #f6f6f6;
	font-weight: normal;
	color: #454545;
}
.ui-state-default a,
.ui-state-default a:link,
.ui-state-default a:visited,
a.ui-button,
a:link.ui-button,
a:visited.ui-button,
.ui-button {
	color: #454545;
	text-decoration: none;
}
.ui-state-hover,
.ui-widget-content .ui-state-hover,
.ui-widget-header .ui-state-hover,
.ui-state-focus,
.ui-widget-content .ui-state-focus,
.ui-widget-header .ui-state-focus,
.ui-button:hover,
.ui-button:focus {
	border: 1px solid #cccccc;
	background: #ededed;
	font-weight: normal;
	color: #2b2b2b;
}
.ui-state-hover a,
.ui-state-hover a:hover,
.ui-state-hover a:link,
.ui-state-hover a:visited,
.ui-state-focus a,
.ui-state-focus a:hover,
.ui-state-focus a:link,
.ui-state-focus a:visited,
a.ui-button:hover,
a.ui-button:focus {
	color: #2b2b2b;
	text-decoration: none;
}

.ui-visual-focus {
	box-shadow: 0 0 3px 1px rgb(94, 158, 214);
}
.ui-state-active,
.ui-widget-content .ui-state-active,
.ui-widget-header .ui-state-active,
a.ui-button:active,
.ui-button:active,
.ui-button.ui-state-active:hover {
	border: 1px solid #003eff;
	background: #007fff;
	font-weight: normal;
	color: #ffffff;
}
.ui-icon-background,
.ui-state-active .ui-icon-background {
	border: #003eff;
	background-color: #ffffff;
}
.ui-state-active a,
.ui-state-active a:link,
.ui-state-active a:visited {
	color: #ffffff;
	text-decoration: none;
}


.ui-state-highlight,
.ui-widget-content .ui-state-highlight,
.ui-widget-header .ui-state-highlight {
	border: 1px solid #dad55e;
	background: #fffa90;
	color: #777620;
}
.ui-state-checked {
	border: 1px solid #dad55e;
	background: #fffa90;
}
.ui-state-highlight a,
.ui-widget-content .ui-state-highlight a,
.ui-widget-header .ui-state-highlight a {
	color: #777620;
}
.ui-state-error,
.ui-widget-content .ui-state-error,
.ui-widget-header .ui-state-error {
	border: 1px solid #f1a899;
	background: #fddfdf;
	color: #5f3f3f;
}
.ui-state-error a,
.ui-widget-content .ui-state-error a,
.ui-widget-header .ui-state-error a {
	color: #5f3f3f;
}
.ui-state-error-text,
.ui-widget-content .ui-state-error-text,
.ui-widget-header .ui-state-error-text {
	color: #5f3f3f;
}
.ui-priority-primary,
.ui-widget-content .ui-priority-primary,
.ui-widget-header .ui-priority-primary {
	font-weight: bold;
}
.ui-priority-secondary,
.ui-widget-content .ui-priority-secondary,
.ui-widget-header .ui-priority-secondary {
	opacity: .7;
	filter:Alpha(Opacity=70); 
	font-weight: normal;
}
.ui-state-disabled,
.ui-widget-content .ui-state-disabled,
.ui-widget-header .ui-state-disabled {
	opacity: .35;
	filter:Alpha(Opacity=35); 
	background-image: none;
}
.ui-state-disabled .ui-icon {
	filter:Alpha(Opacity=35); 
}




.ui-icon {
	width: 16px;
	height: 16px;
}
.ui-icon,
.ui-widget-content .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-widget-header .ui-icon {
	background-image: url("images/ui-icons_444444_256x240.png");
}
.ui-state-hover .ui-icon,
.ui-state-focus .ui-icon,
.ui-button:hover .ui-icon,
.ui-button:focus .ui-icon {
	background-image: url("images/ui-icons_555555_256x240.png");
}
.ui-state-active .ui-icon,
.ui-button:active .ui-icon {
	background-image: url("images/ui-icons_ffffff_256x240.png");
}
.ui-state-highlight .ui-icon,
.ui-button .ui-state-highlight.ui-icon {
	background-image: url("images/ui-icons_777620_256x240.png");
}
.ui-state-error .ui-icon,
.ui-state-error-text .ui-icon {
	background-image: url("images/ui-icons_cc0000_256x240.png");
}
.ui-button .ui-icon {
	background-image: url("images/ui-icons_777777_256x240.png");
}


.ui-icon-blank { background-position: 16px 16px; }
.ui-icon-caret-1-n { background-position: 0 0; }
.ui-icon-caret-1-ne { background-position: -16px 0; }
.ui-icon-caret-1-e { background-position: -32px 0; }
.ui-icon-caret-1-se { background-position: -48px 0; }
.ui-icon-caret-1-s { background-position: -65px 0; }
.ui-icon-caret-1-sw { background-position: -80px 0; }
.ui-icon-caret-1-w { background-position: -96px 0; }
.ui-icon-caret-1-nw { background-position: -112px 0; }
.ui-icon-caret-2-n-s { background-position: -128px 0; }
.ui-icon-caret-2-e-w { background-position: -144px 0; }
.ui-icon-triangle-1-n { background-position: 0 -16px; }
.ui-icon-triangle-1-ne { background-position: -16px -16px; }
.ui-icon-triangle-1-e { background-position: -32px -16px; }
.ui-icon-triangle-1-se { background-position: -48px -16px; }
.ui-icon-triangle-1-s { background-position: -65px -16px; }
.ui-icon-triangle-1-sw { background-position: -80px -16px; }
.ui-icon-triangle-1-w { background-position: -96px -16px; }
.ui-icon-triangle-1-nw { background-position: -112px -16px; }
.ui-icon-triangle-2-n-s { background-position: -128px -16px; }
.ui-icon-triangle-2-e-w { background-position: -144px -16px; }
.ui-icon-arrow-1-n { background-position: 0 -32px; }
.ui-icon-arrow-1-ne { background-position: -16px -32px; }
.ui-icon-arrow-1-e { background-position: -32px -32px; }
.ui-icon-arrow-1-se { background-position: -48px -32px; }
.ui-icon-arrow-1-s { background-position: -65px -32px; }
.ui-icon-arrow-1-sw { background-position: -80px -32px; }
.ui-icon-arrow-1-w { background-position: -96px -32px; }
.ui-icon-arrow-1-nw { background-position: -112px -32px; }
.ui-icon-arrow-2-n-s { background-position: -128px -32px; }
.ui-icon-arrow-2-ne-sw { background-position: -144px -32px; }
.ui-icon-arrow-2-e-w { background-position: -160px -32px; }
.ui-icon-arrow-2-se-nw { background-position: -176px -32px; }
.ui-icon-arrowstop-1-n { background-position: -192px -32px; }
.ui-icon-arrowstop-1-e { background-position: -208px -32px; }
.ui-icon-arrowstop-1-s { background-position: -224px -32px; }
.ui-icon-arrowstop-1-w { background-position: -240px -32px; }
.ui-icon-arrowthick-1-n { background-position: 1px -48px; }
.ui-icon-arrowthick-1-ne { background-position: -16px -48px; }
.ui-icon-arrowthick-1-e { background-position: -32px -48px; }
.ui-icon-arrowthick-1-se { background-position: -48px -48px; }
.ui-icon-arrowthick-1-s { background-position: -64px -48px; }
.ui-icon-arrowthick-1-sw { background-position: -80px -48px; }
.ui-icon-arrowthick-1-w { background-position: -96px -48px; }
.ui-icon-arrowthick-1-nw { background-position: -112px -48px; }
.ui-icon-arrowthick-2-n-s { background-position: -128px -48px; }
.ui-icon-arrowthick-2-ne-sw { background-position: -144px -48px; }
.ui-icon-arrowthick-2-e-w { background-position: -160px -48px; }
.ui-icon-arrowthick-2-se-nw { background-position: -176px -48px; }
.ui-icon-arrowthickstop-1-n { background-position: -192px -48px; }
.ui-icon-arrowthickstop-1-e { background-position: -208px -48px; }
.ui-icon-arrowthickstop-1-s { background-position: -224px -48px; }
.ui-icon-arrowthickstop-1-w { background-position: -240px -48px; }
.ui-icon-arrowreturnthick-1-w { background-position: 0 -64px; }
.ui-icon-arrowreturnthick-1-n { background-position: -16px -64px; }
.ui-icon-arrowreturnthick-1-e { background-position: -32px -64px; }
.ui-icon-arrowreturnthick-1-s { background-position: -48px -64px; }
.ui-icon-arrowreturn-1-w { background-position: -64px -64px; }
.ui-icon-arrowreturn-1-n { background-position: -80px -64px; }
.ui-icon-arrowreturn-1-e { background-position: -96px -64px; }
.ui-icon-arrowreturn-1-s { background-position: -112px -64px; }
.ui-icon-arrowrefresh-1-w { background-position: -128px -64px; }
.ui-icon-arrowrefresh-1-n { background-position: -144px -64px; }
.ui-icon-arrowrefresh-1-e { background-position: -160px -64px; }
.ui-icon-arrowrefresh-1-s { background-position: -176px -64px; }
.ui-icon-arrow-4 { background-position: 0 -80px; }
.ui-icon-arrow-4-diag { background-position: -16px -80px; }
.ui-icon-extlink { background-position: -32px -80px; }
.ui-icon-newwin { background-position: -48px -80px; }
.ui-icon-refresh { background-position: -64px -80px; }
.ui-icon-shuffle { background-position: -80px -80px; }
.ui-icon-transfer-e-w { background-position: -96px -80px; }
.ui-icon-transferthick-e-w { background-position: -112px -80px; }
.ui-icon-folder-collapsed { background-position: 0 -96px; }
.ui-icon-folder-open { background-position: -16px -96px; }
.ui-icon-document { background-position: -32px -96px; }
.ui-icon-document-b { background-position: -48px -96px; }
.ui-icon-note { background-position: -64px -96px; }
.ui-icon-mail-closed { background-position: -80px -96px; }
.ui-icon-mail-open { background-position: -96px -96px; }
.ui-icon-suitcase { background-position: -112px -96px; }
.ui-icon-comment { background-position: -128px -96px; }
.ui-icon-person { background-position: -144px -96px; }
.ui-icon-print { background-position: -160px -96px; }
.ui-icon-trash { background-position: -176px -96px; }
.ui-icon-locked { background-position: -192px -96px; }
.ui-icon-unlocked { background-position: -208px -96px; }
.ui-icon-bookmark { background-position: -224px -96px; }
.ui-icon-tag { background-position: -240px -96px; }
.ui-icon-home { background-position: 0 -112px; }
.ui-icon-flag { background-position: -16px -112px; }
.ui-icon-calendar { background-position: -32px -112px; }
.ui-icon-cart { background-position: -48px -112px; }
.ui-icon-pencil { background-position: -64px -112px; }
.ui-icon-clock { background-position: -80px -112px; }
.ui-icon-disk { background-position: -96px -112px; }
.ui-icon-calculator { background-position: -112px -112px; }
.ui-icon-zoomin { background-position: -128px -112px; }
.ui-icon-zoomout { background-position: -144px -112px; }
.ui-icon-search { background-position: -160px -112px; }
.ui-icon-wrench { background-position: -176px -112px; }
.ui-icon-gear { background-position: -192px -112px; }
.ui-icon-heart { background-position: -208px -112px; }
.ui-icon-star { background-position: -224px -112px; }
.ui-icon-link { background-position: -240px -112px; }
.ui-icon-cancel { background-position: 0 -128px; }
.ui-icon-plus { background-position: -16px -128px; }
.ui-icon-plusthick { background-position: -32px -128px; }
.ui-icon-minus { background-position: -48px -128px; }
.ui-icon-minusthick { background-position: -64px -128px; }
.ui-icon-close { background-position: -80px -128px; }
.ui-icon-closethick { background-position: -96px -128px; }
.ui-icon-key { background-position: -112px -128px; }
.ui-icon-lightbulb { background-position: -128px -128px; }
.ui-icon-scissors { background-position: -144px -128px; }
.ui-icon-clipboard { background-position: -160px -128px; }
.ui-icon-copy { background-position: -176px -128px; }
.ui-icon-contact { background-position: -192px -128px; }
.ui-icon-image { background-position: -208px -128px; }
.ui-icon-video { background-position: -224px -128px; }
.ui-icon-script { background-position: -240px -128px; }
.ui-icon-alert { background-position: 0 -144px; }
.ui-icon-info { background-position: -16px -144px; }
.ui-icon-notice { background-position: -32px -144px; }
.ui-icon-help { background-position: -48px -144px; }
.ui-icon-check { background-position: -64px -144px; }
.ui-icon-bullet { background-position: -80px -144px; }
.ui-icon-radio-on { background-position: -96px -144px; }
.ui-icon-radio-off { background-position: -112px -144px; }
.ui-icon-pin-w { background-position: -128px -144px; }
.ui-icon-pin-s { background-position: -144px -144px; }
.ui-icon-play { background-position: 0 -160px; }
.ui-icon-pause { background-position: -16px -160px; }
.ui-icon-seek-next { background-position: -32px -160px; }
.ui-icon-seek-prev { background-position: -48px -160px; }
.ui-icon-seek-end { background-position: -64px -160px; }
.ui-icon-seek-start { background-position: -80px -160px; }

.ui-icon-seek-first { background-position: -80px -160px; }
.ui-icon-stop { background-position: -96px -160px; }
.ui-icon-eject { background-position: -112px -160px; }
.ui-icon-volume-off { background-position: -128px -160px; }
.ui-icon-volume-on { background-position: -144px -160px; }
.ui-icon-power { background-position: 0 -176px; }
.ui-icon-signal-diag { background-position: -16px -176px; }
.ui-icon-signal { background-position: -32px -176px; }
.ui-icon-battery-0 { background-position: -48px -176px; }
.ui-icon-battery-1 { background-position: -64px -176px; }
.ui-icon-battery-2 { background-position: -80px -176px; }
.ui-icon-battery-3 { background-position: -96px -176px; }
.ui-icon-circle-plus { background-position: 0 -192px; }
.ui-icon-circle-minus { background-position: -16px -192px; }
.ui-icon-circle-close { background-position: -32px -192px; }
.ui-icon-circle-triangle-e { background-position: -48px -192px; }
.ui-icon-circle-triangle-s { background-position: -64px -192px; }
.ui-icon-circle-triangle-w { background-position: -80px -192px; }
.ui-icon-circle-triangle-n { background-position: -96px -192px; }
.ui-icon-circle-arrow-e { background-position: -112px -192px; }
.ui-icon-circle-arrow-s { background-position: -128px -192px; }
.ui-icon-circle-arrow-w { background-position: -144px -192px; }
.ui-icon-circle-arrow-n { background-position: -160px -192px; }
.ui-icon-circle-zoomin { background-position: -176px -192px; }
.ui-icon-circle-zoomout { background-position: -192px -192px; }
.ui-icon-circle-check { background-position: -208px -192px; }
.ui-icon-circlesmall-plus { background-position: 0 -208px; }
.ui-icon-circlesmall-minus { background-position: -16px -208px; }
.ui-icon-circlesmall-close { background-position: -32px -208px; }
.ui-icon-squaresmall-plus { background-position: -48px -208px; }
.ui-icon-squaresmall-minus { background-position: -64px -208px; }
.ui-icon-squaresmall-close { background-position: -80px -208px; }
.ui-icon-grip-dotted-vertical { background-position: 0 -224px; }
.ui-icon-grip-dotted-horizontal { background-position: -16px -224px; }
.ui-icon-grip-solid-vertical { background-position: -32px -224px; }
.ui-icon-grip-solid-horizontal { background-position: -48px -224px; }
.ui-icon-gripsmall-diagonal-se { background-position: -64px -224px; }
.ui-icon-grip-diagonal-se { background-position: -80px -224px; }





.ui-corner-all,
.ui-corner-top,
.ui-corner-left,
.ui-corner-tl {
	border-top-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-top,
.ui-corner-right,
.ui-corner-tr {
	border-top-right-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-left,
.ui-corner-bl {
	border-bottom-left-radius: 3px;
}
.ui-corner-all,
.ui-corner-bottom,
.ui-corner-right,
.ui-corner-br {
	border-bottom-right-radius: 3px;
}


.ui-widget-overlay {
	background: #aaaaaa;
	opacity: .3;
	filter: Alpha(Opacity=30); 
}
.ui-widget-shadow {
	-webkit-box-shadow: 0px 0px 5px #666666;
	box-shadow: 0px 0px 5px #666666;
} 
</style>
<script src='js/jquery-1.12.4.js'></script>
<script src='js/jquery-ui.js'></script>

<script>
$( function() {
	$( '#tabs-collect-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-collect-consensus-heatmap'>
<ul>
<li><a href='#tab-collect-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-collect-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-collect-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-collect-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-collect-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-collect-consensus-heatmap-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-1-1.png" alt="plot of chunk tab-collect-consensus-heatmap-1"/></p>

</div>
<div id='tab-collect-consensus-heatmap-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-2-1.png" alt="plot of chunk tab-collect-consensus-heatmap-2"/></p>

</div>
<div id='tab-collect-consensus-heatmap-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-3-1.png" alt="plot of chunk tab-collect-consensus-heatmap-3"/></p>

</div>
<div id='tab-collect-consensus-heatmap-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-4-1.png" alt="plot of chunk tab-collect-consensus-heatmap-4"/></p>

</div>
<div id='tab-collect-consensus-heatmap-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = consensus_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-consensus-heatmap-5-1.png" alt="plot of chunk tab-collect-consensus-heatmap-5"/></p>

</div>
</div>



### Membership heatmap

Membership heatmaps for all methods. ([What is a membership heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_12))


<script>
$( function() {
	$( '#tabs-collect-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-collect-membership-heatmap'>
<ul>
<li><a href='#tab-collect-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-collect-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-collect-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-collect-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-collect-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-collect-membership-heatmap-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-1-1.png" alt="plot of chunk tab-collect-membership-heatmap-1"/></p>

</div>
<div id='tab-collect-membership-heatmap-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-2-1.png" alt="plot of chunk tab-collect-membership-heatmap-2"/></p>

</div>
<div id='tab-collect-membership-heatmap-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-3-1.png" alt="plot of chunk tab-collect-membership-heatmap-3"/></p>

</div>
<div id='tab-collect-membership-heatmap-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-4-1.png" alt="plot of chunk tab-collect-membership-heatmap-4"/></p>

</div>
<div id='tab-collect-membership-heatmap-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = membership_heatmap, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-membership-heatmap-5-1.png" alt="plot of chunk tab-collect-membership-heatmap-5"/></p>

</div>
</div>



### Signature heatmap

Signature heatmaps for all methods. ([What is a signature heatmap?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_22))


Note in following heatmaps, rows are scaled.



<script>
$( function() {
	$( '#tabs-collect-get-signatures' ).tabs();
} );
</script>
<div id='tabs-collect-get-signatures'>
<ul>
<li><a href='#tab-collect-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-collect-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-collect-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-collect-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-collect-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-collect-get-signatures-1'>
<pre><code class="r">collect_plots(res_list, k = 2, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-1-1.png" alt="plot of chunk tab-collect-get-signatures-1"/></p>

</div>
<div id='tab-collect-get-signatures-2'>
<pre><code class="r">collect_plots(res_list, k = 3, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-2-1.png" alt="plot of chunk tab-collect-get-signatures-2"/></p>

</div>
<div id='tab-collect-get-signatures-3'>
<pre><code class="r">collect_plots(res_list, k = 4, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-3-1.png" alt="plot of chunk tab-collect-get-signatures-3"/></p>

</div>
<div id='tab-collect-get-signatures-4'>
<pre><code class="r">collect_plots(res_list, k = 5, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-4-1.png" alt="plot of chunk tab-collect-get-signatures-4"/></p>

</div>
<div id='tab-collect-get-signatures-5'>
<pre><code class="r">collect_plots(res_list, k = 6, fun = get_signatures, mc.cores = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-get-signatures-5-1.png" alt="plot of chunk tab-collect-get-signatures-5"/></p>

</div>
</div>



### Statistics table

The statistics used for measuring the stability of consensus partitioning.
([How are they
defined?](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13))


<script>
$( function() {
	$( '#tabs-get-stats-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-get-stats-from-consensus-partition-list'>
<ul>
<li><a href='#tab-get-stats-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-get-stats-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-get-stats-from-consensus-partition-list-1'>
<pre><code class="r">get_stats(res_list, k = 2)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      2 1.000           0.982       0.991          0.482 0.521   0.521
#&gt; CV:NMF      2 1.000           1.000       1.000          0.479 0.521   0.521
#&gt; MAD:NMF     2 0.958           0.940       0.976          0.487 0.512   0.512
#&gt; ATC:NMF     2 0.778           0.901       0.951          0.465 0.512   0.512
#&gt; SD:skmeans  2 1.000           1.000       1.000          0.479 0.521   0.521
#&gt; CV:skmeans  2 1.000           1.000       1.000          0.479 0.521   0.521
#&gt; MAD:skmeans 2 1.000           1.000       1.000          0.479 0.521   0.521
#&gt; ATC:skmeans 2 1.000           1.000       1.000          0.506 0.495   0.495
#&gt; SD:mclust   2 0.566           0.896       0.924          0.466 0.531   0.531
#&gt; CV:mclust   2 1.000           0.957       0.981          0.456 0.543   0.543
#&gt; MAD:mclust  2 1.000           0.994       0.997          0.470 0.531   0.531
#&gt; ATC:mclust  2 1.000           1.000       1.000          0.469 0.531   0.531
#&gt; SD:kmeans   2 1.000           0.993       0.994          0.477 0.521   0.521
#&gt; CV:kmeans   2 1.000           1.000       1.000          0.479 0.521   0.521
#&gt; MAD:kmeans  2 1.000           0.980       0.992          0.475 0.521   0.521
#&gt; ATC:kmeans  2 1.000           0.995       0.993          0.503 0.495   0.495
#&gt; SD:pam      2 1.000           0.992       0.997          0.471 0.531   0.531
#&gt; CV:pam      2 1.000           0.975       0.991          0.475 0.521   0.521
#&gt; MAD:pam     2 1.000           0.991       0.996          0.471 0.531   0.531
#&gt; ATC:pam     2 1.000           1.000       1.000          0.506 0.495   0.495
#&gt; SD:hclust   2 1.000           0.977       0.992          0.474 0.531   0.531
#&gt; CV:hclust   2 1.000           0.979       0.988          0.476 0.521   0.521
#&gt; MAD:hclust  2 1.000           0.986       0.994          0.472 0.531   0.531
#&gt; ATC:hclust  2 0.713           0.915       0.951          0.498 0.495   0.495
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-2'>
<pre><code class="r">get_stats(res_list, k = 3)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      3 0.591           0.504       0.748          0.302 0.955   0.914
#&gt; CV:NMF      3 0.729           0.971       0.914          0.365 0.803   0.621
#&gt; MAD:NMF     3 0.556           0.631       0.730          0.282 0.920   0.844
#&gt; ATC:NMF     3 0.922           0.940       0.974          0.349 0.826   0.672
#&gt; SD:skmeans  3 0.792           0.896       0.918          0.395 0.803   0.621
#&gt; CV:skmeans  3 1.000           1.000       1.000          0.411 0.803   0.621
#&gt; MAD:skmeans 3 0.761           0.804       0.872          0.387 0.803   0.621
#&gt; ATC:skmeans 3 0.902           0.952       0.963          0.248 0.826   0.661
#&gt; SD:mclust   3 0.792           0.689       0.822          0.394 0.793   0.611
#&gt; CV:mclust   3 0.986           0.951       0.979          0.486 0.753   0.555
#&gt; MAD:mclust  3 0.634           0.794       0.856          0.356 0.826   0.672
#&gt; ATC:mclust  3 0.793           0.879       0.885          0.355 0.826   0.672
#&gt; SD:kmeans   3 0.620           0.559       0.729          0.321 0.898   0.805
#&gt; CV:kmeans   3 0.704           0.925       0.841          0.322 0.803   0.621
#&gt; MAD:kmeans  3 0.640           0.460       0.681          0.334 0.849   0.721
#&gt; ATC:kmeans  3 0.710           0.662       0.755          0.276 0.747   0.528
#&gt; SD:pam      3 0.806           0.752       0.873          0.409 0.791   0.607
#&gt; CV:pam      3 0.732           0.829       0.893          0.365 0.833   0.680
#&gt; MAD:pam     3 0.787           0.785       0.866          0.413 0.791   0.607
#&gt; ATC:pam     3 0.779           0.806       0.911          0.310 0.728   0.501
#&gt; SD:hclust   3 0.731           0.801       0.875          0.188 0.935   0.877
#&gt; CV:hclust   3 0.716           0.889       0.797          0.288 0.803   0.621
#&gt; MAD:hclust  3 0.653           0.823       0.865          0.358 0.826   0.672
#&gt; ATC:hclust  3 0.771           0.846       0.920          0.318 0.852   0.701
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-3'>
<pre><code class="r">get_stats(res_list, k = 4)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      4 0.753           0.825       0.859         0.1826 0.724   0.450
#&gt; CV:NMF      4 0.935           0.981       0.969         0.1307 0.928   0.778
#&gt; MAD:NMF     4 0.697           0.706       0.788         0.1742 0.798   0.543
#&gt; ATC:NMF     4 0.713           0.787       0.864         0.1653 0.873   0.666
#&gt; SD:skmeans  4 0.961           0.945       0.959         0.1086 0.898   0.703
#&gt; CV:skmeans  4 0.896           0.840       0.923         0.0860 0.907   0.725
#&gt; MAD:skmeans 4 1.000           0.964       0.974         0.1140 0.898   0.703
#&gt; ATC:skmeans 4 0.848           0.714       0.856         0.1208 0.931   0.807
#&gt; SD:mclust   4 0.814           0.801       0.841         0.1441 0.872   0.639
#&gt; CV:mclust   4 0.824           0.895       0.875         0.0923 0.935   0.797
#&gt; MAD:mclust  4 0.838           0.892       0.898         0.1684 0.896   0.707
#&gt; ATC:mclust  4 0.976           0.920       0.969         0.1729 0.898   0.715
#&gt; SD:kmeans   4 0.602           0.350       0.586         0.1380 0.651   0.310
#&gt; CV:kmeans   4 0.569           0.847       0.820         0.1245 1.000   1.000
#&gt; MAD:kmeans  4 0.682           0.824       0.775         0.1386 0.791   0.520
#&gt; ATC:kmeans  4 0.774           0.872       0.890         0.1318 0.905   0.718
#&gt; SD:pam      4 0.807           0.810       0.850         0.1235 0.877   0.649
#&gt; CV:pam      4 0.729           0.793       0.891         0.1200 0.865   0.642
#&gt; MAD:pam     4 0.850           0.918       0.941         0.1187 0.888   0.674
#&gt; ATC:pam     4 0.919           0.884       0.945         0.1154 0.889   0.677
#&gt; SD:hclust   4 0.600           0.462       0.765         0.2541 0.895   0.774
#&gt; CV:hclust   4 0.759           0.774       0.882         0.1785 0.963   0.886
#&gt; MAD:hclust  4 0.722           0.738       0.847         0.1199 0.936   0.821
#&gt; ATC:hclust  4 0.820           0.874       0.896         0.1006 0.931   0.801
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-4'>
<pre><code class="r">get_stats(res_list, k = 5)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      5 0.820           0.782       0.877         0.0759 0.888   0.594
#&gt; CV:NMF      5 0.742           0.755       0.853         0.0787 0.925   0.713
#&gt; MAD:NMF     5 0.819           0.776       0.863         0.0867 0.871   0.546
#&gt; ATC:NMF     5 0.749           0.806       0.846         0.0598 0.954   0.836
#&gt; SD:skmeans  5 0.953           0.953       0.956         0.0902 0.928   0.722
#&gt; CV:skmeans  5 0.796           0.628       0.787         0.0658 0.980   0.926
#&gt; MAD:skmeans 5 0.903           0.956       0.943         0.0856 0.928   0.722
#&gt; ATC:skmeans 5 0.894           0.813       0.902         0.0576 0.924   0.753
#&gt; SD:mclust   5 0.922           0.890       0.932         0.0743 0.935   0.744
#&gt; CV:mclust   5 0.767           0.637       0.770         0.0474 0.900   0.666
#&gt; MAD:mclust  5 0.824           0.890       0.918         0.0785 0.936   0.747
#&gt; ATC:mclust  5 0.839           0.883       0.897         0.0435 1.000   1.000
#&gt; SD:kmeans   5 0.649           0.841       0.801         0.0765 0.869   0.532
#&gt; CV:kmeans   5 0.709           0.565       0.682         0.0746 0.908   0.715
#&gt; MAD:kmeans  5 0.695           0.855       0.789         0.0731 0.935   0.741
#&gt; ATC:kmeans  5 0.832           0.854       0.827         0.0662 0.973   0.896
#&gt; SD:pam      5 0.939           0.911       0.961         0.0838 0.935   0.744
#&gt; CV:pam      5 0.802           0.778       0.893         0.0807 0.914   0.696
#&gt; MAD:pam     5 0.971           0.940       0.975         0.0859 0.935   0.744
#&gt; ATC:pam     5 1.000           0.961       0.985         0.0429 0.970   0.884
#&gt; SD:hclust   5 0.726           0.675       0.799         0.0635 0.778   0.457
#&gt; CV:hclust   5 0.820           0.664       0.837         0.0666 0.934   0.778
#&gt; MAD:hclust  5 0.688           0.440       0.760         0.0661 0.838   0.539
#&gt; ATC:hclust  5 0.933           0.952       0.950         0.0610 0.948   0.812
</code></pre>

</div>
<div id='tab-get-stats-from-consensus-partition-list-5'>
<pre><code class="r">get_stats(res_list, k = 6)
</code></pre>

<pre><code>#&gt;             k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#&gt; SD:NMF      6 0.832           0.759       0.884         0.0355 0.974   0.864
#&gt; CV:NMF      6 0.773           0.609       0.803         0.0442 0.970   0.848
#&gt; MAD:NMF     6 0.783           0.761       0.864         0.0343 0.959   0.794
#&gt; ATC:NMF     6 0.774           0.746       0.825         0.0358 0.971   0.886
#&gt; SD:skmeans  6 0.910           0.871       0.892         0.0304 1.000   1.000
#&gt; CV:skmeans  6 0.798           0.679       0.763         0.0509 0.884   0.563
#&gt; MAD:skmeans 6 0.936           0.812       0.892         0.0299 0.985   0.922
#&gt; ATC:skmeans 6 0.904           0.872       0.909         0.0361 0.931   0.740
#&gt; SD:mclust   6 0.918           0.860       0.934         0.0316 0.949   0.753
#&gt; CV:mclust   6 0.753           0.580       0.774         0.0462 0.910   0.652
#&gt; MAD:mclust  6 0.915           0.878       0.944         0.0289 0.965   0.824
#&gt; ATC:mclust  6 0.850           0.829       0.885         0.0289 0.936   0.770
#&gt; SD:kmeans   6 0.736           0.819       0.819         0.0544 1.000   1.000
#&gt; CV:kmeans   6 0.713           0.383       0.703         0.0542 0.896   0.618
#&gt; MAD:kmeans  6 0.766           0.827       0.820         0.0477 1.000   1.000
#&gt; ATC:kmeans  6 0.785           0.760       0.755         0.0464 0.922   0.675
#&gt; SD:pam      6 0.918           0.883       0.953         0.0158 0.988   0.939
#&gt; CV:pam      6 0.894           0.857       0.925         0.0428 0.959   0.813
#&gt; MAD:pam     6 0.964           0.928       0.974         0.0150 0.988   0.939
#&gt; ATC:pam     6 0.969           0.928       0.972         0.0741 0.939   0.735
#&gt; SD:hclust   6 0.686           0.589       0.767         0.0583 0.900   0.650
#&gt; CV:hclust   6 0.806           0.742       0.789         0.0417 0.922   0.683
#&gt; MAD:hclust  6 0.836           0.758       0.858         0.0689 0.889   0.581
#&gt; ATC:hclust  6 0.985           0.922       0.970         0.0304 0.987   0.942
</code></pre>

</div>
</div>

Following heatmap plots the partition for each combination of methods and the
lightness correspond to the silhouette scores for samples in each method. On
top the consensus subgroup is inferred from all methods by taking the mean
silhouette scores as weight.


<script>
$( function() {
	$( '#tabs-collect-stats-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-collect-stats-from-consensus-partition-list'>
<ul>
<li><a href='#tab-collect-stats-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-collect-stats-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-collect-stats-from-consensus-partition-list-1'>
<pre><code class="r">collect_stats(res_list, k = 2)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-1-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-1"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-2'>
<pre><code class="r">collect_stats(res_list, k = 3)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-2-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-2"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-3'>
<pre><code class="r">collect_stats(res_list, k = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-3-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-3"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-4'>
<pre><code class="r">collect_stats(res_list, k = 5)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-4-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-4"/></p>

</div>
<div id='tab-collect-stats-from-consensus-partition-list-5'>
<pre><code class="r">collect_stats(res_list, k = 6)
</code></pre>

<p><img src="figure_cola/tab-collect-stats-from-consensus-partition-list-5-1.png" alt="plot of chunk tab-collect-stats-from-consensus-partition-list-5"/></p>

</div>
</div>

### Partition from all methods



Collect partitions from all methods:


<script>
$( function() {
	$( '#tabs-collect-classes-from-consensus-partition-list' ).tabs();
} );
</script>
<div id='tabs-collect-classes-from-consensus-partition-list'>
<ul>
<li><a href='#tab-collect-classes-from-consensus-partition-list-1'>k = 2</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-2'>k = 3</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-3'>k = 4</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-4'>k = 5</a></li>
<li><a href='#tab-collect-classes-from-consensus-partition-list-5'>k = 6</a></li>
</ul>
<div id='tab-collect-classes-from-consensus-partition-list-1'>
<pre><code class="r">collect_classes(res_list, k = 2)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-1-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-1"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-2'>
<pre><code class="r">collect_classes(res_list, k = 3)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-2-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-2"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-3'>
<pre><code class="r">collect_classes(res_list, k = 4)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-3-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-3"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-4'>
<pre><code class="r">collect_classes(res_list, k = 5)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-4-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-4"/></p>

</div>
<div id='tab-collect-classes-from-consensus-partition-list-5'>
<pre><code class="r">collect_classes(res_list, k = 6)
</code></pre>

<p><img src="figure_cola/tab-collect-classes-from-consensus-partition-list-5-1.png" alt="plot of chunk tab-collect-classes-from-consensus-partition-list-5"/></p>

</div>
</div>



### Top rows overlap


Overlap of top rows from different top-row methods:


<script>
$( function() {
	$( '#tabs-top-rows-overlap-by-euler' ).tabs();
} );
</script>
<div id='tabs-top-rows-overlap-by-euler'>
<ul>
<li><a href='#tab-top-rows-overlap-by-euler-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-overlap-by-euler-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-overlap-by-euler-1'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 1000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-1-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-1"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-2'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 2000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-2-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-2"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-3'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 3000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-3-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-3"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-4'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 4000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-4-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-4"/></p>

</div>
<div id='tab-top-rows-overlap-by-euler-5'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 5000, method = &quot;euler&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-euler-5-1.png" alt="plot of chunk tab-top-rows-overlap-by-euler-5"/></p>

</div>
</div>

Also visualize the correspondance of rankings between different top-row methods:


<script>
$( function() {
	$( '#tabs-top-rows-overlap-by-correspondance' ).tabs();
} );
</script>
<div id='tabs-top-rows-overlap-by-correspondance'>
<ul>
<li><a href='#tab-top-rows-overlap-by-correspondance-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-overlap-by-correspondance-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-overlap-by-correspondance-1'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 1000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-1-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-1"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-2'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 2000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-2-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-2"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-3'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 3000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-3-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-3"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-4'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 4000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-4-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-4"/></p>

</div>
<div id='tab-top-rows-overlap-by-correspondance-5'>
<pre><code class="r">top_rows_overlap(res_list, top_n = 5000, method = &quot;correspondance&quot;)
</code></pre>

<p><img src="figure_cola/tab-top-rows-overlap-by-correspondance-5-1.png" alt="plot of chunk tab-top-rows-overlap-by-correspondance-5"/></p>

</div>
</div>


Heatmaps of the top rows:



<script>
$( function() {
	$( '#tabs-top-rows-heatmap' ).tabs();
} );
</script>
<div id='tabs-top-rows-heatmap'>
<ul>
<li><a href='#tab-top-rows-heatmap-1'>top_n = 1000</a></li>
<li><a href='#tab-top-rows-heatmap-2'>top_n = 2000</a></li>
<li><a href='#tab-top-rows-heatmap-3'>top_n = 3000</a></li>
<li><a href='#tab-top-rows-heatmap-4'>top_n = 4000</a></li>
<li><a href='#tab-top-rows-heatmap-5'>top_n = 5000</a></li>
</ul>
<div id='tab-top-rows-heatmap-1'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 1000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-1-1.png" alt="plot of chunk tab-top-rows-heatmap-1"/></p>

</div>
<div id='tab-top-rows-heatmap-2'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 2000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-2-1.png" alt="plot of chunk tab-top-rows-heatmap-2"/></p>

</div>
<div id='tab-top-rows-heatmap-3'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 3000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-3-1.png" alt="plot of chunk tab-top-rows-heatmap-3"/></p>

</div>
<div id='tab-top-rows-heatmap-4'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 4000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-4-1.png" alt="plot of chunk tab-top-rows-heatmap-4"/></p>

</div>
<div id='tab-top-rows-heatmap-5'>
<pre><code class="r">top_rows_heatmap(res_list, top_n = 5000)
</code></pre>

<p><img src="figure_cola/tab-top-rows-heatmap-5-1.png" alt="plot of chunk tab-top-rows-heatmap-5"/></p>

</div>
</div>



 
## Results for each method


---------------------------------------------------




### SD:hclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "hclust"]
# you can also extract it by
# res = res_list["SD:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-hclust-collect-plots](figure_cola/SD-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-hclust-select-partition-number](figure_cola/SD-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.977       0.992         0.4738 0.531   0.531
#> 3 3 0.731           0.801       0.875         0.1876 0.935   0.877
#> 4 4 0.600           0.462       0.765         0.2541 0.895   0.774
#> 5 5 0.726           0.675       0.799         0.0635 0.778   0.457
#> 6 6 0.686           0.589       0.767         0.0583 0.900   0.650
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-classes'>
<ul>
<li><a href='#tab-SD-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-hclust-get-classes-1'>
<p><a id='tab-SD-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR547975     2  0.0000      1.000 0.000 1.000
#&gt; SRR547973     2  0.0000      1.000 0.000 1.000
#&gt; SRR547968     2  0.0000      1.000 0.000 1.000
#&gt; SRR547980     2  0.0000      1.000 0.000 1.000
#&gt; SRR545058     1  0.0000      0.987 1.000 0.000
#&gt; SRR546225     1  0.9866      0.240 0.568 0.432
#&gt; SRR546226     1  0.0000      0.987 1.000 0.000
#&gt; SRR546227     1  0.0000      0.987 1.000 0.000
#&gt; SRR546228     1  0.0000      0.987 1.000 0.000
#&gt; SRR546229     1  0.0000      0.987 1.000 0.000
#&gt; SRR546230     1  0.0000      0.987 1.000 0.000
#&gt; SRR546231     1  0.0000      0.987 1.000 0.000
#&gt; SRR546232     1  0.0000      0.987 1.000 0.000
#&gt; SRR546233     1  0.0000      0.987 1.000 0.000
#&gt; SRR546234     1  0.0672      0.979 0.992 0.008
#&gt; SRR546235     1  0.0000      0.987 1.000 0.000
#&gt; SRR546236     1  0.0000      0.987 1.000 0.000
#&gt; SRR546237     1  0.0000      0.987 1.000 0.000
#&gt; SRR546238     1  0.0000      0.987 1.000 0.000
#&gt; SRR546239     1  0.0000      0.987 1.000 0.000
#&gt; SRR546240     1  0.0000      0.987 1.000 0.000
#&gt; SRR547969     2  0.0000      1.000 0.000 1.000
#&gt; SRR547970     2  0.0000      1.000 0.000 1.000
#&gt; SRR547971     2  0.0000      1.000 0.000 1.000
#&gt; SRR547972     2  0.0000      1.000 0.000 1.000
#&gt; SRR547974     2  0.0000      1.000 0.000 1.000
#&gt; SRR547976     2  0.0000      1.000 0.000 1.000
#&gt; SRR547978     2  0.0000      1.000 0.000 1.000
#&gt; SRR547979     2  0.0000      1.000 0.000 1.000
#&gt; SRR547981     2  0.0000      1.000 0.000 1.000
#&gt; SRR547982     2  0.0000      1.000 0.000 1.000
#&gt; SRR547983     2  0.0000      1.000 0.000 1.000
#&gt; SRR547989     2  0.0000      1.000 0.000 1.000
#&gt; SRR547990     2  0.0000      1.000 0.000 1.000
#&gt; SRR547991     2  0.0000      1.000 0.000 1.000
#&gt; SRR547992     2  0.0000      1.000 0.000 1.000
#&gt; SRR801424     1  0.0000      0.987 1.000 0.000
#&gt; SRR801425     1  0.0000      0.987 1.000 0.000
#&gt; SRR801426     1  0.0000      0.987 1.000 0.000
#&gt; SRR801427     1  0.0000      0.987 1.000 0.000
#&gt; SRR801428     1  0.0000      0.987 1.000 0.000
#&gt; SRR801429     1  0.0000      0.987 1.000 0.000
#&gt; SRR801430     1  0.0000      0.987 1.000 0.000
#&gt; SRR801431     1  0.0000      0.987 1.000 0.000
#&gt; SRR801432     1  0.0000      0.987 1.000 0.000
#&gt; SRR801433     1  0.0000      0.987 1.000 0.000
#&gt; SRR825135     1  0.0000      0.987 1.000 0.000
#&gt; SRR825136     1  0.0000      0.987 1.000 0.000
#&gt; SRR825137     1  0.0000      0.987 1.000 0.000
#&gt; SRR825139     1  0.0000      0.987 1.000 0.000
#&gt; SRR825140     1  0.0000      0.987 1.000 0.000
#&gt; SRR825141     1  0.0000      0.987 1.000 0.000
#&gt; SRR825143     1  0.0000      0.987 1.000 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-1-a').click(function(){
  $('#tab-SD-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-2'>
<p><a id='tab-SD-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     3  0.4887      0.842 0.000 0.228 0.772
#&gt; SRR547973     2  0.0000      0.806 0.000 1.000 0.000
#&gt; SRR547968     2  0.0000      0.806 0.000 1.000 0.000
#&gt; SRR547980     3  0.6140      0.758 0.000 0.404 0.596
#&gt; SRR545058     1  0.0237      0.921 0.996 0.000 0.004
#&gt; SRR546225     1  0.8548      0.269 0.568 0.312 0.120
#&gt; SRR546226     1  0.0000      0.922 1.000 0.000 0.000
#&gt; SRR546227     1  0.0000      0.922 1.000 0.000 0.000
#&gt; SRR546228     1  0.0237      0.921 0.996 0.000 0.004
#&gt; SRR546229     1  0.0237      0.921 0.996 0.000 0.004
#&gt; SRR546230     1  0.0000      0.922 1.000 0.000 0.000
#&gt; SRR546231     1  0.0000      0.922 1.000 0.000 0.000
#&gt; SRR546232     1  0.0000      0.922 1.000 0.000 0.000
#&gt; SRR546233     1  0.2066      0.902 0.940 0.000 0.060
#&gt; SRR546234     1  0.0661      0.918 0.988 0.004 0.008
#&gt; SRR546235     1  0.0237      0.921 0.996 0.000 0.004
#&gt; SRR546236     1  0.0237      0.921 0.996 0.000 0.004
#&gt; SRR546237     1  0.0000      0.922 1.000 0.000 0.000
#&gt; SRR546238     1  0.0237      0.921 0.996 0.000 0.004
#&gt; SRR546239     1  0.0000      0.922 1.000 0.000 0.000
#&gt; SRR546240     1  0.0000      0.922 1.000 0.000 0.000
#&gt; SRR547969     2  0.4452      0.535 0.000 0.808 0.192
#&gt; SRR547970     3  0.4887      0.842 0.000 0.228 0.772
#&gt; SRR547971     3  0.6140      0.758 0.000 0.404 0.596
#&gt; SRR547972     2  0.0000      0.806 0.000 1.000 0.000
#&gt; SRR547974     3  0.4887      0.842 0.000 0.228 0.772
#&gt; SRR547976     2  0.0000      0.806 0.000 1.000 0.000
#&gt; SRR547978     3  0.6140      0.758 0.000 0.404 0.596
#&gt; SRR547979     2  0.0000      0.806 0.000 1.000 0.000
#&gt; SRR547981     3  0.4887      0.842 0.000 0.228 0.772
#&gt; SRR547982     2  0.0000      0.806 0.000 1.000 0.000
#&gt; SRR547983     2  0.6260     -0.384 0.000 0.552 0.448
#&gt; SRR547989     2  0.6260     -0.384 0.000 0.552 0.448
#&gt; SRR547990     3  0.4842      0.837 0.000 0.224 0.776
#&gt; SRR547991     3  0.6140      0.758 0.000 0.404 0.596
#&gt; SRR547992     2  0.0000      0.806 0.000 1.000 0.000
#&gt; SRR801424     1  0.4796      0.835 0.780 0.000 0.220
#&gt; SRR801425     1  0.4842      0.834 0.776 0.000 0.224
#&gt; SRR801426     1  0.4842      0.834 0.776 0.000 0.224
#&gt; SRR801427     1  0.4796      0.835 0.780 0.000 0.220
#&gt; SRR801428     1  0.4796      0.835 0.780 0.000 0.220
#&gt; SRR801429     1  0.4842      0.834 0.776 0.000 0.224
#&gt; SRR801430     1  0.4796      0.835 0.780 0.000 0.220
#&gt; SRR801431     1  0.4842      0.834 0.776 0.000 0.224
#&gt; SRR801432     1  0.4842      0.834 0.776 0.000 0.224
#&gt; SRR801433     1  0.4796      0.835 0.780 0.000 0.220
#&gt; SRR825135     1  0.0237      0.921 0.996 0.000 0.004
#&gt; SRR825136     1  0.0000      0.922 1.000 0.000 0.000
#&gt; SRR825137     1  0.0237      0.921 0.996 0.000 0.004
#&gt; SRR825139     1  0.0000      0.922 1.000 0.000 0.000
#&gt; SRR825140     1  0.0000      0.922 1.000 0.000 0.000
#&gt; SRR825141     1  0.0237      0.921 0.996 0.000 0.004
#&gt; SRR825143     1  0.0000      0.922 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-2-a').click(function(){
  $('#tab-SD-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-3'>
<p><a id='tab-SD-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     3  0.2281     0.6965 0.000 0.000 0.904 0.096
#&gt; SRR547973     2  0.0000     0.8292 0.000 1.000 0.000 0.000
#&gt; SRR547968     2  0.0000     0.8292 0.000 1.000 0.000 0.000
#&gt; SRR547980     3  0.4713     0.4455 0.000 0.360 0.640 0.000
#&gt; SRR545058     1  0.4992     0.2612 0.524 0.000 0.000 0.476
#&gt; SRR546225     1  0.8809     0.1002 0.456 0.312 0.116 0.116
#&gt; SRR546226     1  0.0000     0.5148 1.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000     0.5148 1.000 0.000 0.000 0.000
#&gt; SRR546228     1  0.4992     0.2612 0.524 0.000 0.000 0.476
#&gt; SRR546229     1  0.4999     0.2547 0.508 0.000 0.000 0.492
#&gt; SRR546230     1  0.0000     0.5148 1.000 0.000 0.000 0.000
#&gt; SRR546231     1  0.4961     0.2763 0.552 0.000 0.000 0.448
#&gt; SRR546232     1  0.0000     0.5148 1.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.2589     0.3839 0.884 0.000 0.000 0.116
#&gt; SRR546234     1  0.5147     0.2581 0.536 0.004 0.000 0.460
#&gt; SRR546235     1  0.4999     0.2547 0.508 0.000 0.000 0.492
#&gt; SRR546236     1  0.4992     0.2612 0.524 0.000 0.000 0.476
#&gt; SRR546237     1  0.1211     0.5019 0.960 0.000 0.000 0.040
#&gt; SRR546238     1  0.4999     0.2547 0.508 0.000 0.000 0.492
#&gt; SRR546239     1  0.0188     0.5121 0.996 0.000 0.000 0.004
#&gt; SRR546240     1  0.1211     0.5019 0.960 0.000 0.000 0.040
#&gt; SRR547969     2  0.3726     0.6205 0.000 0.788 0.212 0.000
#&gt; SRR547970     3  0.2281     0.6965 0.000 0.000 0.904 0.096
#&gt; SRR547971     3  0.4804     0.4131 0.000 0.384 0.616 0.000
#&gt; SRR547972     2  0.0000     0.8292 0.000 1.000 0.000 0.000
#&gt; SRR547974     3  0.2281     0.6965 0.000 0.000 0.904 0.096
#&gt; SRR547976     2  0.0000     0.8292 0.000 1.000 0.000 0.000
#&gt; SRR547978     3  0.4804     0.4131 0.000 0.384 0.616 0.000
#&gt; SRR547979     2  0.0000     0.8292 0.000 1.000 0.000 0.000
#&gt; SRR547981     3  0.2281     0.6965 0.000 0.000 0.904 0.096
#&gt; SRR547982     2  0.0000     0.8292 0.000 1.000 0.000 0.000
#&gt; SRR547983     2  0.4985    -0.0302 0.000 0.532 0.468 0.000
#&gt; SRR547989     2  0.4985    -0.0302 0.000 0.532 0.468 0.000
#&gt; SRR547990     3  0.0188     0.6831 0.000 0.000 0.996 0.004
#&gt; SRR547991     3  0.4804     0.4131 0.000 0.384 0.616 0.000
#&gt; SRR547992     2  0.0000     0.8292 0.000 1.000 0.000 0.000
#&gt; SRR801424     1  0.4877    -0.1056 0.592 0.000 0.000 0.408
#&gt; SRR801425     4  0.2345     0.7739 0.100 0.000 0.000 0.900
#&gt; SRR801426     4  0.3764     0.9407 0.216 0.000 0.000 0.784
#&gt; SRR801427     1  0.4877    -0.1056 0.592 0.000 0.000 0.408
#&gt; SRR801428     1  0.4877    -0.1056 0.592 0.000 0.000 0.408
#&gt; SRR801429     4  0.3764     0.9407 0.216 0.000 0.000 0.784
#&gt; SRR801430     1  0.4877    -0.1056 0.592 0.000 0.000 0.408
#&gt; SRR801431     4  0.3764     0.9407 0.216 0.000 0.000 0.784
#&gt; SRR801432     4  0.3764     0.9407 0.216 0.000 0.000 0.784
#&gt; SRR801433     1  0.4877    -0.1056 0.592 0.000 0.000 0.408
#&gt; SRR825135     1  0.4999     0.2547 0.508 0.000 0.000 0.492
#&gt; SRR825136     1  0.0000     0.5148 1.000 0.000 0.000 0.000
#&gt; SRR825137     1  0.4999     0.2547 0.508 0.000 0.000 0.492
#&gt; SRR825139     1  0.0000     0.5148 1.000 0.000 0.000 0.000
#&gt; SRR825140     1  0.0000     0.5148 1.000 0.000 0.000 0.000
#&gt; SRR825141     1  0.4999     0.2547 0.508 0.000 0.000 0.492
#&gt; SRR825143     1  0.0000     0.5148 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-3-a').click(function(){
  $('#tab-SD-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-4'>
<p><a id='tab-SD-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR547975     5  0.3177      0.883 0.000 0.000 0.000 0.208 0.792
#&gt; SRR547973     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547968     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547980     4  0.1211      0.774 0.000 0.016 0.000 0.960 0.024
#&gt; SRR545058     3  0.4420      0.695 0.448 0.000 0.548 0.000 0.004
#&gt; SRR546225     1  0.8314     -0.194 0.432 0.308 0.132 0.044 0.084
#&gt; SRR546226     1  0.0000      0.701 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000      0.701 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.4420      0.695 0.448 0.000 0.548 0.000 0.004
#&gt; SRR546229     3  0.4752      0.706 0.428 0.000 0.556 0.004 0.012
#&gt; SRR546230     1  0.0000      0.701 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.4802      0.638 0.480 0.000 0.504 0.004 0.012
#&gt; SRR546232     1  0.0000      0.701 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.2230      0.638 0.884 0.000 0.116 0.000 0.000
#&gt; SRR546234     3  0.4732      0.669 0.468 0.004 0.520 0.004 0.004
#&gt; SRR546235     3  0.4752      0.706 0.428 0.000 0.556 0.004 0.012
#&gt; SRR546236     3  0.4420      0.695 0.448 0.000 0.548 0.000 0.004
#&gt; SRR546237     1  0.1043      0.658 0.960 0.000 0.040 0.000 0.000
#&gt; SRR546238     3  0.4752      0.706 0.428 0.000 0.556 0.004 0.012
#&gt; SRR546239     1  0.0162      0.700 0.996 0.000 0.004 0.000 0.000
#&gt; SRR546240     1  0.1043      0.658 0.960 0.000 0.040 0.000 0.000
#&gt; SRR547969     4  0.4291      0.271 0.000 0.464 0.000 0.536 0.000
#&gt; SRR547970     5  0.3177      0.883 0.000 0.000 0.000 0.208 0.792
#&gt; SRR547971     4  0.0510      0.796 0.000 0.016 0.000 0.984 0.000
#&gt; SRR547972     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547974     5  0.3177      0.883 0.000 0.000 0.000 0.208 0.792
#&gt; SRR547976     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547978     4  0.0510      0.796 0.000 0.016 0.000 0.984 0.000
#&gt; SRR547979     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547981     5  0.2966      0.864 0.000 0.000 0.000 0.184 0.816
#&gt; SRR547982     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547983     4  0.2930      0.764 0.000 0.164 0.000 0.832 0.004
#&gt; SRR547989     4  0.2930      0.764 0.000 0.164 0.000 0.832 0.004
#&gt; SRR547990     5  0.3949      0.433 0.000 0.000 0.000 0.332 0.668
#&gt; SRR547991     4  0.0510      0.796 0.000 0.016 0.000 0.984 0.000
#&gt; SRR547992     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR801424     1  0.4887      0.437 0.536 0.000 0.444 0.008 0.012
#&gt; SRR801425     3  0.0771      0.437 0.000 0.000 0.976 0.004 0.020
#&gt; SRR801426     3  0.2674      0.379 0.084 0.000 0.888 0.008 0.020
#&gt; SRR801427     1  0.4227      0.460 0.580 0.000 0.420 0.000 0.000
#&gt; SRR801428     1  0.4887      0.437 0.536 0.000 0.444 0.008 0.012
#&gt; SRR801429     3  0.2674      0.379 0.084 0.000 0.888 0.008 0.020
#&gt; SRR801430     1  0.4887      0.437 0.536 0.000 0.444 0.008 0.012
#&gt; SRR801431     3  0.2674      0.379 0.084 0.000 0.888 0.008 0.020
#&gt; SRR801432     3  0.2674      0.379 0.084 0.000 0.888 0.008 0.020
#&gt; SRR801433     1  0.4887      0.437 0.536 0.000 0.444 0.008 0.012
#&gt; SRR825135     3  0.4752      0.706 0.428 0.000 0.556 0.004 0.012
#&gt; SRR825136     1  0.0000      0.701 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825137     3  0.4752      0.706 0.428 0.000 0.556 0.004 0.012
#&gt; SRR825139     1  0.0000      0.701 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825140     1  0.0000      0.701 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.4752      0.706 0.428 0.000 0.556 0.004 0.012
#&gt; SRR825143     1  0.0000      0.701 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-4-a').click(function(){
  $('#tab-SD-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-hclust-get-classes-5'>
<p><a id='tab-SD-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR547975     5  0.0146     0.9106 0.000 0.000 0.000 0.000 0.996 0.004
#&gt; SRR547973     2  0.0000     0.9985 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547968     2  0.0000     0.9985 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547980     6  0.2048     0.8131 0.000 0.000 0.000 0.000 0.120 0.880
#&gt; SRR545058     3  0.2793     0.7292 0.000 0.000 0.800 0.200 0.000 0.000
#&gt; SRR546225     4  0.6487     0.0918 0.000 0.268 0.200 0.488 0.000 0.044
#&gt; SRR546226     1  0.5350     0.5213 0.476 0.000 0.108 0.416 0.000 0.000
#&gt; SRR546227     1  0.5858     0.4824 0.476 0.000 0.224 0.300 0.000 0.000
#&gt; SRR546228     3  0.2793     0.7292 0.000 0.000 0.800 0.200 0.000 0.000
#&gt; SRR546229     3  0.0000     0.8244 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546230     1  0.5350     0.5213 0.476 0.000 0.108 0.416 0.000 0.000
#&gt; SRR546231     3  0.1398     0.7821 0.052 0.000 0.940 0.008 0.000 0.000
#&gt; SRR546232     1  0.5350     0.5213 0.476 0.000 0.108 0.416 0.000 0.000
#&gt; SRR546233     1  0.4868     0.5043 0.592 0.000 0.076 0.332 0.000 0.000
#&gt; SRR546234     3  0.3592     0.5401 0.000 0.000 0.656 0.344 0.000 0.000
#&gt; SRR546235     3  0.0000     0.8244 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546236     3  0.2762     0.7315 0.000 0.000 0.804 0.196 0.000 0.000
#&gt; SRR546237     1  0.5984     0.4488 0.444 0.000 0.276 0.280 0.000 0.000
#&gt; SRR546238     3  0.0000     0.8244 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546239     1  0.5867     0.4747 0.480 0.000 0.240 0.280 0.000 0.000
#&gt; SRR546240     1  0.5984     0.4488 0.444 0.000 0.276 0.280 0.000 0.000
#&gt; SRR547969     6  0.3851     0.2328 0.000 0.460 0.000 0.000 0.000 0.540
#&gt; SRR547970     5  0.0146     0.9106 0.000 0.000 0.000 0.000 0.996 0.004
#&gt; SRR547971     6  0.1765     0.8304 0.000 0.000 0.000 0.000 0.096 0.904
#&gt; SRR547972     2  0.0000     0.9985 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547974     5  0.1588     0.9024 0.000 0.000 0.000 0.072 0.924 0.004
#&gt; SRR547976     2  0.0000     0.9985 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547978     6  0.1765     0.8304 0.000 0.000 0.000 0.000 0.096 0.904
#&gt; SRR547979     2  0.0000     0.9985 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547981     5  0.2882     0.8170 0.000 0.000 0.000 0.180 0.812 0.008
#&gt; SRR547982     2  0.0260     0.9910 0.000 0.992 0.000 0.000 0.000 0.008
#&gt; SRR547983     6  0.1501     0.7853 0.000 0.076 0.000 0.000 0.000 0.924
#&gt; SRR547989     6  0.1501     0.7853 0.000 0.076 0.000 0.000 0.000 0.924
#&gt; SRR547990     4  0.5868    -0.4691 0.000 0.000 0.000 0.448 0.348 0.204
#&gt; SRR547991     6  0.1765     0.8304 0.000 0.000 0.000 0.000 0.096 0.904
#&gt; SRR547992     2  0.0000     0.9985 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR801424     1  0.0000     0.3899 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR801425     3  0.4429     0.2988 0.424 0.000 0.548 0.028 0.000 0.000
#&gt; SRR801426     1  0.4434    -0.2013 0.544 0.000 0.428 0.028 0.000 0.000
#&gt; SRR801427     1  0.2020     0.4232 0.896 0.000 0.008 0.096 0.000 0.000
#&gt; SRR801428     1  0.0000     0.3899 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR801429     1  0.4434    -0.2013 0.544 0.000 0.428 0.028 0.000 0.000
#&gt; SRR801430     1  0.0000     0.3899 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR801431     1  0.4434    -0.2013 0.544 0.000 0.428 0.028 0.000 0.000
#&gt; SRR801432     1  0.4434    -0.2013 0.544 0.000 0.428 0.028 0.000 0.000
#&gt; SRR801433     1  0.0000     0.3899 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR825135     3  0.0000     0.8244 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR825136     1  0.5350     0.5213 0.476 0.000 0.108 0.416 0.000 0.000
#&gt; SRR825137     3  0.0000     0.8244 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR825139     1  0.5350     0.5213 0.476 0.000 0.108 0.416 0.000 0.000
#&gt; SRR825140     1  0.5350     0.5213 0.476 0.000 0.108 0.416 0.000 0.000
#&gt; SRR825141     3  0.0000     0.8244 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR825143     1  0.5350     0.5213 0.476 0.000 0.108 0.416 0.000 0.000
</code></pre>

<script>
$('#tab-SD-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-hclust-get-classes-5-a').click(function(){
  $('#tab-SD-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-SD-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-signatures'>
<ul>
<li><a href='#tab-SD-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-1-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-1"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-2-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-2"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-3-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-3"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-4-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-4"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-5-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-hclust-signature_compare](figure_cola/SD-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-SD-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-hclust-collect-classes](figure_cola/SD-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:kmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "kmeans"]
# you can also extract it by
# res = res_list["SD:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-kmeans-collect-plots](figure_cola/SD-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-kmeans-select-partition-number](figure_cola/SD-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.993       0.994         0.4770 0.521   0.521
#> 3 3 0.620           0.559       0.729         0.3211 0.898   0.805
#> 4 4 0.602           0.350       0.586         0.1380 0.651   0.310
#> 5 5 0.649           0.841       0.801         0.0765 0.869   0.532
#> 6 6 0.736           0.819       0.819         0.0544 1.000   1.000
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-classes'>
<ul>
<li><a href='#tab-SD-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-kmeans-get-classes-1'>
<p><a id='tab-SD-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR547975     2  0.0000      0.993 0.000 1.000
#&gt; SRR547973     2  0.0000      0.993 0.000 1.000
#&gt; SRR547968     2  0.0000      0.993 0.000 1.000
#&gt; SRR547980     2  0.0000      0.993 0.000 1.000
#&gt; SRR545058     1  0.0672      0.997 0.992 0.008
#&gt; SRR546225     2  0.5408      0.857 0.124 0.876
#&gt; SRR546226     1  0.0672      0.997 0.992 0.008
#&gt; SRR546227     1  0.0672      0.997 0.992 0.008
#&gt; SRR546228     1  0.0672      0.997 0.992 0.008
#&gt; SRR546229     1  0.0672      0.997 0.992 0.008
#&gt; SRR546230     1  0.0672      0.997 0.992 0.008
#&gt; SRR546231     1  0.0672      0.997 0.992 0.008
#&gt; SRR546232     1  0.0672      0.997 0.992 0.008
#&gt; SRR546233     1  0.0672      0.997 0.992 0.008
#&gt; SRR546234     1  0.0672      0.997 0.992 0.008
#&gt; SRR546235     1  0.0672      0.997 0.992 0.008
#&gt; SRR546236     1  0.0672      0.997 0.992 0.008
#&gt; SRR546237     1  0.0672      0.997 0.992 0.008
#&gt; SRR546238     1  0.0672      0.997 0.992 0.008
#&gt; SRR546239     1  0.0672      0.997 0.992 0.008
#&gt; SRR546240     1  0.0672      0.997 0.992 0.008
#&gt; SRR547969     2  0.0000      0.993 0.000 1.000
#&gt; SRR547970     2  0.0000      0.993 0.000 1.000
#&gt; SRR547971     2  0.0000      0.993 0.000 1.000
#&gt; SRR547972     2  0.0000      0.993 0.000 1.000
#&gt; SRR547974     2  0.0000      0.993 0.000 1.000
#&gt; SRR547976     2  0.0000      0.993 0.000 1.000
#&gt; SRR547978     2  0.0000      0.993 0.000 1.000
#&gt; SRR547979     2  0.0000      0.993 0.000 1.000
#&gt; SRR547981     2  0.0000      0.993 0.000 1.000
#&gt; SRR547982     2  0.0000      0.993 0.000 1.000
#&gt; SRR547983     2  0.0000      0.993 0.000 1.000
#&gt; SRR547989     2  0.0000      0.993 0.000 1.000
#&gt; SRR547990     2  0.0000      0.993 0.000 1.000
#&gt; SRR547991     2  0.0000      0.993 0.000 1.000
#&gt; SRR547992     2  0.0000      0.993 0.000 1.000
#&gt; SRR801424     1  0.0000      0.994 1.000 0.000
#&gt; SRR801425     1  0.0000      0.994 1.000 0.000
#&gt; SRR801426     1  0.0000      0.994 1.000 0.000
#&gt; SRR801427     1  0.0000      0.994 1.000 0.000
#&gt; SRR801428     1  0.0000      0.994 1.000 0.000
#&gt; SRR801429     1  0.0000      0.994 1.000 0.000
#&gt; SRR801430     1  0.0000      0.994 1.000 0.000
#&gt; SRR801431     1  0.0000      0.994 1.000 0.000
#&gt; SRR801432     1  0.0000      0.994 1.000 0.000
#&gt; SRR801433     1  0.0000      0.994 1.000 0.000
#&gt; SRR825135     1  0.0672      0.997 0.992 0.008
#&gt; SRR825136     1  0.0672      0.997 0.992 0.008
#&gt; SRR825137     1  0.0672      0.997 0.992 0.008
#&gt; SRR825139     1  0.0672      0.997 0.992 0.008
#&gt; SRR825140     1  0.0672      0.997 0.992 0.008
#&gt; SRR825141     1  0.0672      0.997 0.992 0.008
#&gt; SRR825143     1  0.0672      0.997 0.992 0.008
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-1-a').click(function(){
  $('#tab-SD-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-2'>
<p><a id='tab-SD-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     2   0.543     0.8572 0.284 0.716 0.000
#&gt; SRR547973     2   0.000     0.8699 0.000 1.000 0.000
#&gt; SRR547968     2   0.000     0.8699 0.000 1.000 0.000
#&gt; SRR547980     2   0.543     0.8572 0.284 0.716 0.000
#&gt; SRR545058     3   0.000     0.5048 0.000 0.000 1.000
#&gt; SRR546225     2   0.559     0.5033 0.000 0.696 0.304
#&gt; SRR546226     3   0.620     0.1482 0.424 0.000 0.576
#&gt; SRR546227     3   0.620     0.1482 0.424 0.000 0.576
#&gt; SRR546228     3   0.000     0.5048 0.000 0.000 1.000
#&gt; SRR546229     3   0.000     0.5048 0.000 0.000 1.000
#&gt; SRR546230     3   0.620     0.1482 0.424 0.000 0.576
#&gt; SRR546231     3   0.000     0.5048 0.000 0.000 1.000
#&gt; SRR546232     3   0.620     0.1482 0.424 0.000 0.576
#&gt; SRR546233     3   0.620     0.1482 0.424 0.000 0.576
#&gt; SRR546234     3   0.116     0.4907 0.028 0.000 0.972
#&gt; SRR546235     3   0.000     0.5048 0.000 0.000 1.000
#&gt; SRR546236     3   0.000     0.5048 0.000 0.000 1.000
#&gt; SRR546237     3   0.620     0.1482 0.424 0.000 0.576
#&gt; SRR546238     3   0.000     0.5048 0.000 0.000 1.000
#&gt; SRR546239     3   0.620     0.1482 0.424 0.000 0.576
#&gt; SRR546240     3   0.618     0.1531 0.416 0.000 0.584
#&gt; SRR547969     2   0.000     0.8699 0.000 1.000 0.000
#&gt; SRR547970     2   0.543     0.8572 0.284 0.716 0.000
#&gt; SRR547971     2   0.543     0.8572 0.284 0.716 0.000
#&gt; SRR547972     2   0.000     0.8699 0.000 1.000 0.000
#&gt; SRR547974     2   0.543     0.8572 0.284 0.716 0.000
#&gt; SRR547976     2   0.000     0.8699 0.000 1.000 0.000
#&gt; SRR547978     2   0.543     0.8572 0.284 0.716 0.000
#&gt; SRR547979     2   0.000     0.8699 0.000 1.000 0.000
#&gt; SRR547981     2   0.543     0.8572 0.284 0.716 0.000
#&gt; SRR547982     2   0.000     0.8699 0.000 1.000 0.000
#&gt; SRR547983     2   0.103     0.8712 0.024 0.976 0.000
#&gt; SRR547989     2   0.103     0.8712 0.024 0.976 0.000
#&gt; SRR547990     2   0.543     0.8572 0.284 0.716 0.000
#&gt; SRR547991     2   0.543     0.8572 0.284 0.716 0.000
#&gt; SRR547992     2   0.000     0.8699 0.000 1.000 0.000
#&gt; SRR801424     1   0.571     0.9949 0.680 0.000 0.320
#&gt; SRR801425     3   0.550     0.0939 0.292 0.000 0.708
#&gt; SRR801426     3   0.556     0.0839 0.300 0.000 0.700
#&gt; SRR801427     1   0.565     0.9795 0.688 0.000 0.312
#&gt; SRR801428     1   0.571     0.9949 0.680 0.000 0.320
#&gt; SRR801429     3   0.556     0.0839 0.300 0.000 0.700
#&gt; SRR801430     1   0.571     0.9949 0.680 0.000 0.320
#&gt; SRR801431     3   0.556     0.0839 0.300 0.000 0.700
#&gt; SRR801432     3   0.556     0.0839 0.300 0.000 0.700
#&gt; SRR801433     1   0.571     0.9949 0.680 0.000 0.320
#&gt; SRR825135     3   0.000     0.5048 0.000 0.000 1.000
#&gt; SRR825136     3   0.620     0.1482 0.424 0.000 0.576
#&gt; SRR825137     3   0.000     0.5048 0.000 0.000 1.000
#&gt; SRR825139     3   0.620     0.1482 0.424 0.000 0.576
#&gt; SRR825140     3   0.620     0.1482 0.424 0.000 0.576
#&gt; SRR825141     3   0.000     0.5048 0.000 0.000 1.000
#&gt; SRR825143     3   0.620     0.1482 0.424 0.000 0.576
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-2-a').click(function(){
  $('#tab-SD-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-3'>
<p><a id='tab-SD-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     2  0.0000    0.86958 0.000 1.000 0.000 0.000
#&gt; SRR547973     1  0.5147   -0.32851 0.536 0.460 0.000 0.004
#&gt; SRR547968     1  0.4977   -0.32617 0.540 0.460 0.000 0.000
#&gt; SRR547980     2  0.1302    0.86581 0.000 0.956 0.000 0.044
#&gt; SRR545058     3  0.0336    0.86218 0.008 0.000 0.992 0.000
#&gt; SRR546225     3  0.7623    0.10469 0.308 0.200 0.488 0.004
#&gt; SRR546226     1  0.7836   -0.06845 0.388 0.000 0.264 0.348
#&gt; SRR546227     1  0.7836   -0.06845 0.388 0.000 0.264 0.348
#&gt; SRR546228     3  0.0336    0.86218 0.008 0.000 0.992 0.000
#&gt; SRR546229     3  0.0469    0.85716 0.012 0.000 0.988 0.000
#&gt; SRR546230     1  0.7836   -0.06845 0.388 0.000 0.264 0.348
#&gt; SRR546231     3  0.0469    0.86423 0.012 0.000 0.988 0.000
#&gt; SRR546232     1  0.7836   -0.06845 0.388 0.000 0.264 0.348
#&gt; SRR546233     1  0.7836   -0.06845 0.388 0.000 0.264 0.348
#&gt; SRR546234     3  0.1256    0.83100 0.008 0.000 0.964 0.028
#&gt; SRR546235     3  0.0469    0.86423 0.012 0.000 0.988 0.000
#&gt; SRR546236     3  0.0336    0.86473 0.008 0.000 0.992 0.000
#&gt; SRR546237     1  0.7836   -0.06845 0.388 0.000 0.264 0.348
#&gt; SRR546238     3  0.0000    0.86390 0.000 0.000 1.000 0.000
#&gt; SRR546239     4  0.7836   -0.00294 0.348 0.000 0.264 0.388
#&gt; SRR546240     1  0.7830   -0.07881 0.400 0.000 0.268 0.332
#&gt; SRR547969     1  0.5392   -0.33416 0.528 0.460 0.000 0.012
#&gt; SRR547970     2  0.0000    0.86958 0.000 1.000 0.000 0.000
#&gt; SRR547971     2  0.1557    0.86367 0.000 0.944 0.000 0.056
#&gt; SRR547972     1  0.4977   -0.32617 0.540 0.460 0.000 0.000
#&gt; SRR547974     2  0.0000    0.86958 0.000 1.000 0.000 0.000
#&gt; SRR547976     1  0.4977   -0.32617 0.540 0.460 0.000 0.000
#&gt; SRR547978     2  0.1716    0.86180 0.000 0.936 0.000 0.064
#&gt; SRR547979     1  0.4977   -0.32617 0.540 0.460 0.000 0.000
#&gt; SRR547981     2  0.0000    0.86958 0.000 1.000 0.000 0.000
#&gt; SRR547982     1  0.4977   -0.32617 0.540 0.460 0.000 0.000
#&gt; SRR547983     2  0.6389    0.33056 0.448 0.488 0.000 0.064
#&gt; SRR547989     2  0.6389    0.33056 0.448 0.488 0.000 0.064
#&gt; SRR547990     2  0.0000    0.86958 0.000 1.000 0.000 0.000
#&gt; SRR547991     2  0.1716    0.86180 0.000 0.936 0.000 0.064
#&gt; SRR547992     1  0.4977   -0.32617 0.540 0.460 0.000 0.000
#&gt; SRR801424     4  0.3172    0.59182 0.000 0.000 0.160 0.840
#&gt; SRR801425     3  0.6121   -0.10537 0.052 0.000 0.552 0.396
#&gt; SRR801426     4  0.6277    0.18839 0.056 0.000 0.468 0.476
#&gt; SRR801427     4  0.4088    0.57413 0.040 0.000 0.140 0.820
#&gt; SRR801428     4  0.3172    0.59182 0.000 0.000 0.160 0.840
#&gt; SRR801429     4  0.6247    0.27006 0.056 0.000 0.428 0.516
#&gt; SRR801430     4  0.3172    0.59182 0.000 0.000 0.160 0.840
#&gt; SRR801431     4  0.6252    0.26300 0.056 0.000 0.432 0.512
#&gt; SRR801432     4  0.6252    0.26300 0.056 0.000 0.432 0.512
#&gt; SRR801433     4  0.3172    0.59182 0.000 0.000 0.160 0.840
#&gt; SRR825135     3  0.0000    0.86390 0.000 0.000 1.000 0.000
#&gt; SRR825136     4  0.7842   -0.02028 0.360 0.000 0.264 0.376
#&gt; SRR825137     3  0.0469    0.86423 0.012 0.000 0.988 0.000
#&gt; SRR825139     4  0.7842   -0.02028 0.360 0.000 0.264 0.376
#&gt; SRR825140     1  0.7836   -0.06845 0.388 0.000 0.264 0.348
#&gt; SRR825141     3  0.0469    0.86423 0.012 0.000 0.988 0.000
#&gt; SRR825143     1  0.7836   -0.06845 0.388 0.000 0.264 0.348
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-3-a').click(function(){
  $('#tab-SD-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-4'>
<p><a id='tab-SD-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR547975     5  0.0000      0.906 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547973     2  0.4280      0.950 0.000 0.676 0.004 0.008 0.312
#&gt; SRR547968     2  0.3857      0.955 0.000 0.688 0.000 0.000 0.312
#&gt; SRR547980     5  0.2482      0.886 0.000 0.000 0.024 0.084 0.892
#&gt; SRR545058     3  0.3807      0.888 0.116 0.056 0.820 0.008 0.000
#&gt; SRR546225     3  0.6875      0.472 0.052 0.296 0.560 0.020 0.072
#&gt; SRR546226     1  0.0000      0.941 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0703      0.939 0.976 0.024 0.000 0.000 0.000
#&gt; SRR546228     3  0.3807      0.888 0.116 0.056 0.820 0.008 0.000
#&gt; SRR546229     3  0.4665      0.871 0.116 0.056 0.780 0.048 0.000
#&gt; SRR546230     1  0.0000      0.941 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.4473      0.854 0.116 0.112 0.768 0.004 0.000
#&gt; SRR546232     1  0.0703      0.939 0.976 0.024 0.000 0.000 0.000
#&gt; SRR546233     1  0.0162      0.941 0.996 0.004 0.000 0.000 0.000
#&gt; SRR546234     3  0.4147      0.873 0.136 0.056 0.796 0.012 0.000
#&gt; SRR546235     3  0.3474      0.897 0.116 0.044 0.836 0.004 0.000
#&gt; SRR546236     3  0.2727      0.901 0.116 0.016 0.868 0.000 0.000
#&gt; SRR546237     1  0.1732      0.914 0.920 0.080 0.000 0.000 0.000
#&gt; SRR546238     3  0.3106      0.899 0.116 0.020 0.856 0.008 0.000
#&gt; SRR546239     1  0.3898      0.829 0.804 0.116 0.000 0.080 0.000
#&gt; SRR546240     1  0.2248      0.900 0.900 0.088 0.012 0.000 0.000
#&gt; SRR547969     2  0.4385      0.947 0.000 0.672 0.012 0.004 0.312
#&gt; SRR547970     5  0.0000      0.906 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547971     5  0.3622      0.858 0.000 0.000 0.048 0.136 0.816
#&gt; SRR547972     2  0.3857      0.955 0.000 0.688 0.000 0.000 0.312
#&gt; SRR547974     5  0.0290      0.905 0.000 0.000 0.000 0.008 0.992
#&gt; SRR547976     2  0.4009      0.954 0.000 0.684 0.004 0.000 0.312
#&gt; SRR547978     5  0.3821      0.849 0.000 0.000 0.052 0.148 0.800
#&gt; SRR547979     2  0.4009      0.954 0.000 0.684 0.004 0.000 0.312
#&gt; SRR547981     5  0.0290      0.905 0.000 0.000 0.000 0.008 0.992
#&gt; SRR547982     2  0.3857      0.955 0.000 0.688 0.000 0.000 0.312
#&gt; SRR547983     2  0.6562      0.822 0.000 0.536 0.052 0.080 0.332
#&gt; SRR547989     2  0.6562      0.822 0.000 0.536 0.052 0.080 0.332
#&gt; SRR547990     5  0.0451      0.904 0.000 0.000 0.004 0.008 0.988
#&gt; SRR547991     5  0.3821      0.849 0.000 0.000 0.052 0.148 0.800
#&gt; SRR547992     2  0.3857      0.955 0.000 0.688 0.000 0.000 0.312
#&gt; SRR801424     4  0.6082      0.657 0.292 0.092 0.024 0.592 0.000
#&gt; SRR801425     4  0.5826      0.357 0.040 0.032 0.384 0.544 0.000
#&gt; SRR801426     4  0.4939      0.581 0.044 0.008 0.272 0.676 0.000
#&gt; SRR801427     4  0.6187      0.509 0.412 0.080 0.020 0.488 0.000
#&gt; SRR801428     4  0.6082      0.657 0.292 0.092 0.024 0.592 0.000
#&gt; SRR801429     4  0.4066      0.676 0.044 0.000 0.188 0.768 0.000
#&gt; SRR801430     4  0.6082      0.657 0.292 0.092 0.024 0.592 0.000
#&gt; SRR801431     4  0.4066      0.676 0.044 0.000 0.188 0.768 0.000
#&gt; SRR801432     4  0.4066      0.676 0.044 0.000 0.188 0.768 0.000
#&gt; SRR801433     4  0.6082      0.657 0.292 0.092 0.024 0.592 0.000
#&gt; SRR825135     3  0.2796      0.901 0.116 0.008 0.868 0.008 0.000
#&gt; SRR825136     1  0.2504      0.884 0.896 0.040 0.000 0.064 0.000
#&gt; SRR825137     3  0.3474      0.897 0.116 0.044 0.836 0.004 0.000
#&gt; SRR825139     1  0.2504      0.884 0.896 0.040 0.000 0.064 0.000
#&gt; SRR825140     1  0.0000      0.941 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.3474      0.897 0.116 0.044 0.836 0.004 0.000
#&gt; SRR825143     1  0.0000      0.941 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-4-a').click(function(){
  $('#tab-SD-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-kmeans-get-classes-5'>
<p><a id='tab-SD-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5 p6
#&gt; SRR547975     5  0.3111      0.898 0.000 0.156 0.008 0.016 0.820 NA
#&gt; SRR547973     2  0.1269      0.914 0.000 0.956 0.012 0.020 0.000 NA
#&gt; SRR547968     2  0.0405      0.929 0.000 0.988 0.004 0.008 0.000 NA
#&gt; SRR547980     5  0.5138      0.880 0.000 0.156 0.012 0.012 0.688 NA
#&gt; SRR545058     3  0.2809      0.864 0.040 0.000 0.884 0.008 0.044 NA
#&gt; SRR546225     3  0.6739      0.620 0.024 0.160 0.620 0.048 0.060 NA
#&gt; SRR546226     1  0.0146      0.906 0.996 0.000 0.000 0.000 0.004 NA
#&gt; SRR546227     1  0.1152      0.901 0.952 0.000 0.000 0.000 0.004 NA
#&gt; SRR546228     3  0.2809      0.864 0.040 0.000 0.884 0.008 0.044 NA
#&gt; SRR546229     3  0.4761      0.830 0.040 0.000 0.764 0.048 0.044 NA
#&gt; SRR546230     1  0.0000      0.906 1.000 0.000 0.000 0.000 0.000 NA
#&gt; SRR546231     3  0.4395      0.810 0.040 0.000 0.760 0.000 0.068 NA
#&gt; SRR546232     1  0.1265      0.901 0.948 0.000 0.000 0.000 0.008 NA
#&gt; SRR546233     1  0.0603      0.903 0.980 0.000 0.000 0.000 0.004 NA
#&gt; SRR546234     3  0.4124      0.832 0.048 0.000 0.804 0.012 0.060 NA
#&gt; SRR546235     3  0.3301      0.862 0.040 0.000 0.848 0.000 0.056 NA
#&gt; SRR546236     3  0.1391      0.874 0.040 0.000 0.944 0.000 0.000 NA
#&gt; SRR546237     1  0.2491      0.870 0.868 0.000 0.000 0.000 0.020 NA
#&gt; SRR546238     3  0.3123      0.862 0.040 0.000 0.860 0.004 0.024 NA
#&gt; SRR546239     1  0.4836      0.754 0.688 0.000 0.000 0.064 0.028 NA
#&gt; SRR546240     1  0.3092      0.854 0.840 0.000 0.012 0.000 0.028 NA
#&gt; SRR547969     2  0.0520      0.927 0.000 0.984 0.000 0.008 0.000 NA
#&gt; SRR547970     5  0.3111      0.898 0.000 0.156 0.008 0.016 0.820 NA
#&gt; SRR547971     5  0.5335      0.857 0.000 0.156 0.008 0.000 0.620 NA
#&gt; SRR547972     2  0.0146      0.930 0.000 0.996 0.000 0.004 0.000 NA
#&gt; SRR547974     5  0.2558      0.897 0.000 0.156 0.000 0.000 0.840 NA
#&gt; SRR547976     2  0.0405      0.929 0.000 0.988 0.004 0.008 0.000 NA
#&gt; SRR547978     5  0.5459      0.836 0.000 0.156 0.004 0.000 0.580 NA
#&gt; SRR547979     2  0.0508      0.928 0.000 0.984 0.004 0.012 0.000 NA
#&gt; SRR547981     5  0.2558      0.897 0.000 0.156 0.000 0.000 0.840 NA
#&gt; SRR547982     2  0.0146      0.930 0.000 0.996 0.000 0.004 0.000 NA
#&gt; SRR547983     2  0.4526      0.720 0.000 0.720 0.008 0.040 0.020 NA
#&gt; SRR547989     2  0.4526      0.720 0.000 0.720 0.008 0.040 0.020 NA
#&gt; SRR547990     5  0.3051      0.896 0.000 0.156 0.004 0.012 0.824 NA
#&gt; SRR547991     5  0.5459      0.836 0.000 0.156 0.004 0.000 0.580 NA
#&gt; SRR547992     2  0.0146      0.929 0.000 0.996 0.000 0.004 0.000 NA
#&gt; SRR801424     4  0.5893      0.669 0.172 0.000 0.016 0.540 0.000 NA
#&gt; SRR801425     4  0.5136      0.399 0.004 0.000 0.272 0.640 0.024 NA
#&gt; SRR801426     4  0.3593      0.594 0.004 0.000 0.176 0.788 0.008 NA
#&gt; SRR801427     4  0.6233      0.509 0.332 0.000 0.012 0.432 0.000 NA
#&gt; SRR801428     4  0.5893      0.669 0.172 0.000 0.016 0.540 0.000 NA
#&gt; SRR801429     4  0.2006      0.682 0.004 0.000 0.104 0.892 0.000 NA
#&gt; SRR801430     4  0.5893      0.669 0.172 0.000 0.016 0.540 0.000 NA
#&gt; SRR801431     4  0.2006      0.682 0.004 0.000 0.104 0.892 0.000 NA
#&gt; SRR801432     4  0.2006      0.682 0.004 0.000 0.104 0.892 0.000 NA
#&gt; SRR801433     4  0.5893      0.669 0.172 0.000 0.016 0.540 0.000 NA
#&gt; SRR825135     3  0.2763      0.868 0.040 0.000 0.884 0.004 0.024 NA
#&gt; SRR825136     1  0.3579      0.804 0.808 0.000 0.000 0.064 0.008 NA
#&gt; SRR825137     3  0.3301      0.862 0.040 0.000 0.848 0.000 0.056 NA
#&gt; SRR825139     1  0.3579      0.804 0.808 0.000 0.000 0.064 0.008 NA
#&gt; SRR825140     1  0.0000      0.906 1.000 0.000 0.000 0.000 0.000 NA
#&gt; SRR825141     3  0.3360      0.861 0.040 0.000 0.844 0.000 0.060 NA
#&gt; SRR825143     1  0.0146      0.906 0.996 0.000 0.000 0.000 0.004 NA
</code></pre>

<script>
$('#tab-SD-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-kmeans-get-classes-5-a').click(function(){
  $('#tab-SD-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-SD-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-signatures'>
<ul>
<li><a href='#tab-SD-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-kmeans-signature_compare](figure_cola/SD-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-SD-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-kmeans-collect-classes](figure_cola/SD-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "skmeans"]
# you can also extract it by
# res = res_list["SD:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 5.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-skmeans-collect-plots](figure_cola/SD-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-skmeans-select-partition-number](figure_cola/SD-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.4795 0.521   0.521
#> 3 3 0.792           0.896       0.918         0.3954 0.803   0.621
#> 4 4 0.961           0.945       0.959         0.1086 0.898   0.703
#> 5 5 0.953           0.953       0.956         0.0902 0.928   0.722
#> 6 6 0.910           0.871       0.892         0.0304 1.000   1.000
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 5
#> attr(,"optional")
#> [1] 2 4
```

There is also optional best $k$ = 2 4 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-classes'>
<ul>
<li><a href='#tab-SD-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-skmeans-get-classes-1'>
<p><a id='tab-SD-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1 p2
#&gt; SRR547975     2       0          1  0  1
#&gt; SRR547973     2       0          1  0  1
#&gt; SRR547968     2       0          1  0  1
#&gt; SRR547980     2       0          1  0  1
#&gt; SRR545058     1       0          1  1  0
#&gt; SRR546225     2       0          1  0  1
#&gt; SRR546226     1       0          1  1  0
#&gt; SRR546227     1       0          1  1  0
#&gt; SRR546228     1       0          1  1  0
#&gt; SRR546229     1       0          1  1  0
#&gt; SRR546230     1       0          1  1  0
#&gt; SRR546231     1       0          1  1  0
#&gt; SRR546232     1       0          1  1  0
#&gt; SRR546233     1       0          1  1  0
#&gt; SRR546234     1       0          1  1  0
#&gt; SRR546235     1       0          1  1  0
#&gt; SRR546236     1       0          1  1  0
#&gt; SRR546237     1       0          1  1  0
#&gt; SRR546238     1       0          1  1  0
#&gt; SRR546239     1       0          1  1  0
#&gt; SRR546240     1       0          1  1  0
#&gt; SRR547969     2       0          1  0  1
#&gt; SRR547970     2       0          1  0  1
#&gt; SRR547971     2       0          1  0  1
#&gt; SRR547972     2       0          1  0  1
#&gt; SRR547974     2       0          1  0  1
#&gt; SRR547976     2       0          1  0  1
#&gt; SRR547978     2       0          1  0  1
#&gt; SRR547979     2       0          1  0  1
#&gt; SRR547981     2       0          1  0  1
#&gt; SRR547982     2       0          1  0  1
#&gt; SRR547983     2       0          1  0  1
#&gt; SRR547989     2       0          1  0  1
#&gt; SRR547990     2       0          1  0  1
#&gt; SRR547991     2       0          1  0  1
#&gt; SRR547992     2       0          1  0  1
#&gt; SRR801424     1       0          1  1  0
#&gt; SRR801425     1       0          1  1  0
#&gt; SRR801426     1       0          1  1  0
#&gt; SRR801427     1       0          1  1  0
#&gt; SRR801428     1       0          1  1  0
#&gt; SRR801429     1       0          1  1  0
#&gt; SRR801430     1       0          1  1  0
#&gt; SRR801431     1       0          1  1  0
#&gt; SRR801432     1       0          1  1  0
#&gt; SRR801433     1       0          1  1  0
#&gt; SRR825135     1       0          1  1  0
#&gt; SRR825136     1       0          1  1  0
#&gt; SRR825137     1       0          1  1  0
#&gt; SRR825139     1       0          1  1  0
#&gt; SRR825140     1       0          1  1  0
#&gt; SRR825141     1       0          1  1  0
#&gt; SRR825143     1       0          1  1  0
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-1-a').click(function(){
  $('#tab-SD-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-2'>
<p><a id='tab-SD-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     2  0.0237      0.998 0.000 0.996 0.004
#&gt; SRR547973     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547968     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547980     2  0.0237      0.998 0.000 0.996 0.004
#&gt; SRR545058     3  0.5327      0.867 0.272 0.000 0.728
#&gt; SRR546225     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR546226     1  0.0000      0.887 1.000 0.000 0.000
#&gt; SRR546227     1  0.0000      0.887 1.000 0.000 0.000
#&gt; SRR546228     3  0.5327      0.867 0.272 0.000 0.728
#&gt; SRR546229     3  0.3816      0.823 0.148 0.000 0.852
#&gt; SRR546230     1  0.0000      0.887 1.000 0.000 0.000
#&gt; SRR546231     3  0.5327      0.867 0.272 0.000 0.728
#&gt; SRR546232     1  0.0000      0.887 1.000 0.000 0.000
#&gt; SRR546233     1  0.0000      0.887 1.000 0.000 0.000
#&gt; SRR546234     3  0.5431      0.854 0.284 0.000 0.716
#&gt; SRR546235     3  0.5327      0.867 0.272 0.000 0.728
#&gt; SRR546236     3  0.5327      0.867 0.272 0.000 0.728
#&gt; SRR546237     1  0.0000      0.887 1.000 0.000 0.000
#&gt; SRR546238     3  0.5291      0.865 0.268 0.000 0.732
#&gt; SRR546239     1  0.0000      0.887 1.000 0.000 0.000
#&gt; SRR546240     1  0.0000      0.887 1.000 0.000 0.000
#&gt; SRR547969     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547970     2  0.0237      0.998 0.000 0.996 0.004
#&gt; SRR547971     2  0.0237      0.998 0.000 0.996 0.004
#&gt; SRR547972     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547974     2  0.0237      0.998 0.000 0.996 0.004
#&gt; SRR547976     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547978     2  0.0237      0.998 0.000 0.996 0.004
#&gt; SRR547979     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547981     2  0.0237      0.998 0.000 0.996 0.004
#&gt; SRR547982     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547983     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547989     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547990     2  0.0237      0.998 0.000 0.996 0.004
#&gt; SRR547991     2  0.0237      0.998 0.000 0.996 0.004
#&gt; SRR547992     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR801424     1  0.5397      0.726 0.720 0.000 0.280
#&gt; SRR801425     3  0.0237      0.757 0.004 0.000 0.996
#&gt; SRR801426     3  0.0237      0.757 0.004 0.000 0.996
#&gt; SRR801427     1  0.5397      0.726 0.720 0.000 0.280
#&gt; SRR801428     1  0.5397      0.726 0.720 0.000 0.280
#&gt; SRR801429     3  0.0237      0.757 0.004 0.000 0.996
#&gt; SRR801430     1  0.5397      0.726 0.720 0.000 0.280
#&gt; SRR801431     3  0.0237      0.757 0.004 0.000 0.996
#&gt; SRR801432     3  0.0237      0.757 0.004 0.000 0.996
#&gt; SRR801433     1  0.5397      0.726 0.720 0.000 0.280
#&gt; SRR825135     3  0.5327      0.867 0.272 0.000 0.728
#&gt; SRR825136     1  0.0000      0.887 1.000 0.000 0.000
#&gt; SRR825137     3  0.5327      0.867 0.272 0.000 0.728
#&gt; SRR825139     1  0.0000      0.887 1.000 0.000 0.000
#&gt; SRR825140     1  0.0000      0.887 1.000 0.000 0.000
#&gt; SRR825141     3  0.5327      0.867 0.272 0.000 0.728
#&gt; SRR825143     1  0.0000      0.887 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-2-a').click(function(){
  $('#tab-SD-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-3'>
<p><a id='tab-SD-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     2  0.1890      0.968 0.000 0.936 0.008 0.056
#&gt; SRR547973     2  0.0000      0.974 0.000 1.000 0.000 0.000
#&gt; SRR547968     2  0.0000      0.974 0.000 1.000 0.000 0.000
#&gt; SRR547980     2  0.1890      0.968 0.000 0.936 0.008 0.056
#&gt; SRR545058     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR546225     2  0.0000      0.974 0.000 1.000 0.000 0.000
#&gt; SRR546226     1  0.0000      0.961 1.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000      0.961 1.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR546229     3  0.0376      0.994 0.004 0.000 0.992 0.004
#&gt; SRR546230     1  0.0000      0.961 1.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR546232     1  0.0000      0.961 1.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.0000      0.961 1.000 0.000 0.000 0.000
#&gt; SRR546234     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR546235     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR546236     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR546237     1  0.0000      0.961 1.000 0.000 0.000 0.000
#&gt; SRR546238     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR546239     1  0.3123      0.843 0.844 0.000 0.000 0.156
#&gt; SRR546240     1  0.0000      0.961 1.000 0.000 0.000 0.000
#&gt; SRR547969     2  0.0000      0.974 0.000 1.000 0.000 0.000
#&gt; SRR547970     2  0.1890      0.968 0.000 0.936 0.008 0.056
#&gt; SRR547971     2  0.1890      0.968 0.000 0.936 0.008 0.056
#&gt; SRR547972     2  0.0000      0.974 0.000 1.000 0.000 0.000
#&gt; SRR547974     2  0.1890      0.968 0.000 0.936 0.008 0.056
#&gt; SRR547976     2  0.0000      0.974 0.000 1.000 0.000 0.000
#&gt; SRR547978     2  0.1890      0.968 0.000 0.936 0.008 0.056
#&gt; SRR547979     2  0.0000      0.974 0.000 1.000 0.000 0.000
#&gt; SRR547981     2  0.1890      0.968 0.000 0.936 0.008 0.056
#&gt; SRR547982     2  0.0000      0.974 0.000 1.000 0.000 0.000
#&gt; SRR547983     2  0.0000      0.974 0.000 1.000 0.000 0.000
#&gt; SRR547989     2  0.0000      0.974 0.000 1.000 0.000 0.000
#&gt; SRR547990     2  0.1890      0.968 0.000 0.936 0.008 0.056
#&gt; SRR547991     2  0.1890      0.968 0.000 0.936 0.008 0.056
#&gt; SRR547992     2  0.0000      0.974 0.000 1.000 0.000 0.000
#&gt; SRR801424     4  0.1637      0.892 0.060 0.000 0.000 0.940
#&gt; SRR801425     4  0.4522      0.600 0.000 0.000 0.320 0.680
#&gt; SRR801426     4  0.3311      0.805 0.000 0.000 0.172 0.828
#&gt; SRR801427     4  0.3837      0.755 0.224 0.000 0.000 0.776
#&gt; SRR801428     4  0.1637      0.892 0.060 0.000 0.000 0.940
#&gt; SRR801429     4  0.1557      0.894 0.000 0.000 0.056 0.944
#&gt; SRR801430     4  0.1637      0.892 0.060 0.000 0.000 0.940
#&gt; SRR801431     4  0.1557      0.894 0.000 0.000 0.056 0.944
#&gt; SRR801432     4  0.1557      0.894 0.000 0.000 0.056 0.944
#&gt; SRR801433     4  0.1637      0.892 0.060 0.000 0.000 0.940
#&gt; SRR825135     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR825136     1  0.2704      0.877 0.876 0.000 0.000 0.124
#&gt; SRR825137     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR825139     1  0.2704      0.877 0.876 0.000 0.000 0.124
#&gt; SRR825140     1  0.0000      0.961 1.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR825143     1  0.0000      0.961 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-3-a').click(function(){
  $('#tab-SD-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-4'>
<p><a id='tab-SD-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR547975     5  0.1732      0.998 0.000 0.080 0.000 0.000 0.920
#&gt; SRR547973     2  0.0000      0.989 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547968     2  0.0000      0.989 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547980     5  0.1792      0.997 0.000 0.084 0.000 0.000 0.916
#&gt; SRR545058     3  0.0162      0.996 0.000 0.000 0.996 0.000 0.004
#&gt; SRR546225     2  0.1608      0.932 0.000 0.928 0.000 0.000 0.072
#&gt; SRR546226     1  0.0000      0.958 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000      0.958 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.0162      0.996 0.000 0.000 0.996 0.000 0.004
#&gt; SRR546229     3  0.0404      0.988 0.000 0.000 0.988 0.012 0.000
#&gt; SRR546230     1  0.0000      0.958 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.0000      0.997 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546232     1  0.0000      0.958 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.0510      0.951 0.984 0.000 0.000 0.016 0.000
#&gt; SRR546234     3  0.0510      0.989 0.000 0.000 0.984 0.000 0.016
#&gt; SRR546235     3  0.0000      0.997 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546236     3  0.0162      0.996 0.000 0.000 0.996 0.000 0.004
#&gt; SRR546237     1  0.0000      0.958 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546238     3  0.0000      0.997 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546239     1  0.3264      0.824 0.820 0.000 0.000 0.164 0.016
#&gt; SRR546240     1  0.0000      0.958 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547969     2  0.0000      0.989 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547970     5  0.1732      0.998 0.000 0.080 0.000 0.000 0.920
#&gt; SRR547971     5  0.1792      0.997 0.000 0.084 0.000 0.000 0.916
#&gt; SRR547972     2  0.0000      0.989 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547974     5  0.1732      0.998 0.000 0.080 0.000 0.000 0.920
#&gt; SRR547976     2  0.0000      0.989 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547978     5  0.1792      0.997 0.000 0.084 0.000 0.000 0.916
#&gt; SRR547979     2  0.0000      0.989 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547981     5  0.1732      0.998 0.000 0.080 0.000 0.000 0.920
#&gt; SRR547982     2  0.0000      0.989 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547983     2  0.0609      0.976 0.000 0.980 0.000 0.000 0.020
#&gt; SRR547989     2  0.0609      0.976 0.000 0.980 0.000 0.000 0.020
#&gt; SRR547990     5  0.1732      0.998 0.000 0.080 0.000 0.000 0.920
#&gt; SRR547991     5  0.1792      0.997 0.000 0.084 0.000 0.000 0.916
#&gt; SRR547992     2  0.0000      0.989 0.000 1.000 0.000 0.000 0.000
#&gt; SRR801424     4  0.1386      0.902 0.032 0.000 0.000 0.952 0.016
#&gt; SRR801425     4  0.4477      0.660 0.000 0.000 0.252 0.708 0.040
#&gt; SRR801426     4  0.3075      0.848 0.000 0.000 0.092 0.860 0.048
#&gt; SRR801427     4  0.3177      0.764 0.208 0.000 0.000 0.792 0.000
#&gt; SRR801428     4  0.1386      0.902 0.032 0.000 0.000 0.952 0.016
#&gt; SRR801429     4  0.1197      0.900 0.000 0.000 0.000 0.952 0.048
#&gt; SRR801430     4  0.1386      0.902 0.032 0.000 0.000 0.952 0.016
#&gt; SRR801431     4  0.1197      0.900 0.000 0.000 0.000 0.952 0.048
#&gt; SRR801432     4  0.1197      0.900 0.000 0.000 0.000 0.952 0.048
#&gt; SRR801433     4  0.1386      0.902 0.032 0.000 0.000 0.952 0.016
#&gt; SRR825135     3  0.0000      0.997 0.000 0.000 1.000 0.000 0.000
#&gt; SRR825136     1  0.2727      0.876 0.868 0.000 0.000 0.116 0.016
#&gt; SRR825137     3  0.0000      0.997 0.000 0.000 1.000 0.000 0.000
#&gt; SRR825139     1  0.2677      0.879 0.872 0.000 0.000 0.112 0.016
#&gt; SRR825140     1  0.0000      0.958 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0000      0.997 0.000 0.000 1.000 0.000 0.000
#&gt; SRR825143     1  0.0000      0.958 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-4-a').click(function(){
  $('#tab-SD-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-skmeans-get-classes-5'>
<p><a id='tab-SD-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5 p6
#&gt; SRR547975     5  0.0146      0.979 0.000 0.004 0.000 0.000 0.996 NA
#&gt; SRR547973     2  0.0713      0.930 0.000 0.972 0.000 0.000 0.000 NA
#&gt; SRR547968     2  0.0146      0.939 0.000 0.996 0.000 0.000 0.000 NA
#&gt; SRR547980     5  0.0891      0.975 0.000 0.008 0.000 0.000 0.968 NA
#&gt; SRR545058     3  0.1267      0.920 0.000 0.000 0.940 0.000 0.000 NA
#&gt; SRR546225     2  0.4932      0.544 0.000 0.556 0.000 0.000 0.072 NA
#&gt; SRR546226     1  0.0146      0.901 0.996 0.000 0.000 0.000 0.000 NA
#&gt; SRR546227     1  0.0458      0.900 0.984 0.000 0.000 0.000 0.000 NA
#&gt; SRR546228     3  0.1267      0.920 0.000 0.000 0.940 0.000 0.000 NA
#&gt; SRR546229     3  0.2178      0.892 0.000 0.000 0.868 0.000 0.000 NA
#&gt; SRR546230     1  0.0146      0.901 0.996 0.000 0.000 0.000 0.000 NA
#&gt; SRR546231     3  0.0937      0.921 0.000 0.000 0.960 0.000 0.000 NA
#&gt; SRR546232     1  0.0458      0.900 0.984 0.000 0.000 0.000 0.000 NA
#&gt; SRR546233     1  0.2118      0.857 0.888 0.000 0.000 0.104 0.000 NA
#&gt; SRR546234     3  0.3714      0.705 0.000 0.000 0.656 0.000 0.004 NA
#&gt; SRR546235     3  0.0000      0.931 0.000 0.000 1.000 0.000 0.000 NA
#&gt; SRR546236     3  0.0146      0.931 0.000 0.000 0.996 0.000 0.000 NA
#&gt; SRR546237     1  0.1075      0.893 0.952 0.000 0.000 0.000 0.000 NA
#&gt; SRR546238     3  0.2048      0.909 0.000 0.000 0.880 0.000 0.000 NA
#&gt; SRR546239     1  0.4313      0.706 0.668 0.000 0.000 0.284 0.000 NA
#&gt; SRR546240     1  0.1219      0.892 0.948 0.000 0.004 0.000 0.000 NA
#&gt; SRR547969     2  0.0713      0.931 0.000 0.972 0.000 0.000 0.000 NA
#&gt; SRR547970     5  0.0146      0.979 0.000 0.004 0.000 0.000 0.996 NA
#&gt; SRR547971     5  0.1297      0.969 0.000 0.012 0.000 0.000 0.948 NA
#&gt; SRR547972     2  0.0000      0.939 0.000 1.000 0.000 0.000 0.000 NA
#&gt; SRR547974     5  0.0146      0.979 0.000 0.004 0.000 0.000 0.996 NA
#&gt; SRR547976     2  0.0146      0.939 0.000 0.996 0.000 0.000 0.000 NA
#&gt; SRR547978     5  0.1625      0.960 0.000 0.012 0.000 0.000 0.928 NA
#&gt; SRR547979     2  0.0146      0.939 0.000 0.996 0.000 0.000 0.000 NA
#&gt; SRR547981     5  0.0146      0.979 0.000 0.004 0.000 0.000 0.996 NA
#&gt; SRR547982     2  0.0000      0.939 0.000 1.000 0.000 0.000 0.000 NA
#&gt; SRR547983     2  0.2129      0.893 0.000 0.904 0.000 0.000 0.040 NA
#&gt; SRR547989     2  0.2129      0.893 0.000 0.904 0.000 0.000 0.040 NA
#&gt; SRR547990     5  0.0146      0.979 0.000 0.004 0.000 0.000 0.996 NA
#&gt; SRR547991     5  0.1625      0.960 0.000 0.012 0.000 0.000 0.928 NA
#&gt; SRR547992     2  0.0000      0.939 0.000 1.000 0.000 0.000 0.000 NA
#&gt; SRR801424     4  0.0000      0.765 0.000 0.000 0.000 1.000 0.000 NA
#&gt; SRR801425     4  0.5329      0.673 0.000 0.000 0.104 0.452 0.000 NA
#&gt; SRR801426     4  0.4377      0.758 0.000 0.000 0.024 0.540 0.000 NA
#&gt; SRR801427     4  0.3052      0.617 0.216 0.000 0.000 0.780 0.000 NA
#&gt; SRR801428     4  0.0000      0.765 0.000 0.000 0.000 1.000 0.000 NA
#&gt; SRR801429     4  0.3782      0.782 0.000 0.000 0.000 0.588 0.000 NA
#&gt; SRR801430     4  0.0000      0.765 0.000 0.000 0.000 1.000 0.000 NA
#&gt; SRR801431     4  0.3765      0.784 0.000 0.000 0.000 0.596 0.000 NA
#&gt; SRR801432     4  0.3765      0.784 0.000 0.000 0.000 0.596 0.000 NA
#&gt; SRR801433     4  0.0000      0.765 0.000 0.000 0.000 1.000 0.000 NA
#&gt; SRR825135     3  0.1863      0.914 0.000 0.000 0.896 0.000 0.000 NA
#&gt; SRR825136     1  0.3490      0.738 0.724 0.000 0.000 0.268 0.000 NA
#&gt; SRR825137     3  0.0000      0.931 0.000 0.000 1.000 0.000 0.000 NA
#&gt; SRR825139     1  0.3490      0.738 0.724 0.000 0.000 0.268 0.000 NA
#&gt; SRR825140     1  0.0146      0.901 0.996 0.000 0.000 0.000 0.000 NA
#&gt; SRR825141     3  0.0632      0.929 0.000 0.000 0.976 0.000 0.000 NA
#&gt; SRR825143     1  0.0146      0.901 0.996 0.000 0.000 0.000 0.000 NA
</code></pre>

<script>
$('#tab-SD-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-skmeans-get-classes-5-a').click(function(){
  $('#tab-SD-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-SD-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-signatures'>
<ul>
<li><a href='#tab-SD-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-skmeans-signature_compare](figure_cola/SD-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-SD-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-skmeans-collect-classes](figure_cola/SD-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:pam*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "pam"]
# you can also extract it by
# res = res_list["SD:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-pam-collect-plots](figure_cola/SD-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-pam-select-partition-number](figure_cola/SD-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.992       0.997         0.4711 0.531   0.531
#> 3 3 0.806           0.752       0.873         0.4088 0.791   0.607
#> 4 4 0.807           0.810       0.850         0.1235 0.877   0.649
#> 5 5 0.939           0.911       0.961         0.0838 0.935   0.744
#> 6 6 0.918           0.883       0.953         0.0158 0.988   0.939
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 5
```

There is also optional best $k$ = 2 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-classes'>
<ul>
<li><a href='#tab-SD-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-pam-get-classes-1'>
<p><a id='tab-SD-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette   p1   p2
#&gt; SRR547975     2    0.00      1.000 0.00 1.00
#&gt; SRR547973     2    0.00      1.000 0.00 1.00
#&gt; SRR547968     2    0.00      1.000 0.00 1.00
#&gt; SRR547980     2    0.00      1.000 0.00 1.00
#&gt; SRR545058     1    0.00      0.995 1.00 0.00
#&gt; SRR546225     1    0.68      0.780 0.82 0.18
#&gt; SRR546226     1    0.00      0.995 1.00 0.00
#&gt; SRR546227     1    0.00      0.995 1.00 0.00
#&gt; SRR546228     1    0.00      0.995 1.00 0.00
#&gt; SRR546229     1    0.00      0.995 1.00 0.00
#&gt; SRR546230     1    0.00      0.995 1.00 0.00
#&gt; SRR546231     1    0.00      0.995 1.00 0.00
#&gt; SRR546232     1    0.00      0.995 1.00 0.00
#&gt; SRR546233     1    0.00      0.995 1.00 0.00
#&gt; SRR546234     1    0.00      0.995 1.00 0.00
#&gt; SRR546235     1    0.00      0.995 1.00 0.00
#&gt; SRR546236     1    0.00      0.995 1.00 0.00
#&gt; SRR546237     1    0.00      0.995 1.00 0.00
#&gt; SRR546238     1    0.00      0.995 1.00 0.00
#&gt; SRR546239     1    0.00      0.995 1.00 0.00
#&gt; SRR546240     1    0.00      0.995 1.00 0.00
#&gt; SRR547969     2    0.00      1.000 0.00 1.00
#&gt; SRR547970     2    0.00      1.000 0.00 1.00
#&gt; SRR547971     2    0.00      1.000 0.00 1.00
#&gt; SRR547972     2    0.00      1.000 0.00 1.00
#&gt; SRR547974     2    0.00      1.000 0.00 1.00
#&gt; SRR547976     2    0.00      1.000 0.00 1.00
#&gt; SRR547978     2    0.00      1.000 0.00 1.00
#&gt; SRR547979     2    0.00      1.000 0.00 1.00
#&gt; SRR547981     2    0.00      1.000 0.00 1.00
#&gt; SRR547982     2    0.00      1.000 0.00 1.00
#&gt; SRR547983     2    0.00      1.000 0.00 1.00
#&gt; SRR547989     2    0.00      1.000 0.00 1.00
#&gt; SRR547990     2    0.00      1.000 0.00 1.00
#&gt; SRR547991     2    0.00      1.000 0.00 1.00
#&gt; SRR547992     2    0.00      1.000 0.00 1.00
#&gt; SRR801424     1    0.00      0.995 1.00 0.00
#&gt; SRR801425     1    0.00      0.995 1.00 0.00
#&gt; SRR801426     1    0.00      0.995 1.00 0.00
#&gt; SRR801427     1    0.00      0.995 1.00 0.00
#&gt; SRR801428     1    0.00      0.995 1.00 0.00
#&gt; SRR801429     1    0.00      0.995 1.00 0.00
#&gt; SRR801430     1    0.00      0.995 1.00 0.00
#&gt; SRR801431     1    0.00      0.995 1.00 0.00
#&gt; SRR801432     1    0.00      0.995 1.00 0.00
#&gt; SRR801433     1    0.00      0.995 1.00 0.00
#&gt; SRR825135     1    0.00      0.995 1.00 0.00
#&gt; SRR825136     1    0.00      0.995 1.00 0.00
#&gt; SRR825137     1    0.00      0.995 1.00 0.00
#&gt; SRR825139     1    0.00      0.995 1.00 0.00
#&gt; SRR825140     1    0.00      0.995 1.00 0.00
#&gt; SRR825141     1    0.00      0.995 1.00 0.00
#&gt; SRR825143     1    0.00      0.995 1.00 0.00
</code></pre>

<script>
$('#tab-SD-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-1-a').click(function(){
  $('#tab-SD-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-2'>
<p><a id='tab-SD-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547973     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547968     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547980     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR545058     3  0.0000      0.775 0.000 0.000 1.000
#&gt; SRR546225     3  0.1267      0.756 0.004 0.024 0.972
#&gt; SRR546226     1  0.6126      0.699 0.600 0.000 0.400
#&gt; SRR546227     1  0.6126      0.699 0.600 0.000 0.400
#&gt; SRR546228     3  0.0000      0.775 0.000 0.000 1.000
#&gt; SRR546229     3  0.1163      0.754 0.028 0.000 0.972
#&gt; SRR546230     1  0.6126      0.699 0.600 0.000 0.400
#&gt; SRR546231     3  0.0000      0.775 0.000 0.000 1.000
#&gt; SRR546232     1  0.6126      0.699 0.600 0.000 0.400
#&gt; SRR546233     1  0.6126      0.699 0.600 0.000 0.400
#&gt; SRR546234     3  0.1163      0.754 0.028 0.000 0.972
#&gt; SRR546235     3  0.0000      0.775 0.000 0.000 1.000
#&gt; SRR546236     3  0.0000      0.775 0.000 0.000 1.000
#&gt; SRR546237     1  0.6126      0.699 0.600 0.000 0.400
#&gt; SRR546238     3  0.0000      0.775 0.000 0.000 1.000
#&gt; SRR546239     3  0.5431      0.210 0.284 0.000 0.716
#&gt; SRR546240     3  0.6111     -0.230 0.396 0.000 0.604
#&gt; SRR547969     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547970     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547971     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547972     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547974     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547976     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547978     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547979     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547981     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547982     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547983     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547989     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547990     2  0.0424      0.991 0.000 0.992 0.008
#&gt; SRR547991     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547992     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR801424     1  0.0000      0.568 1.000 0.000 0.000
#&gt; SRR801425     3  0.6126      0.433 0.400 0.000 0.600
#&gt; SRR801426     3  0.6244      0.404 0.440 0.000 0.560
#&gt; SRR801427     1  0.0000      0.568 1.000 0.000 0.000
#&gt; SRR801428     1  0.0000      0.568 1.000 0.000 0.000
#&gt; SRR801429     1  0.5254      0.163 0.736 0.000 0.264
#&gt; SRR801430     1  0.0000      0.568 1.000 0.000 0.000
#&gt; SRR801431     3  0.6126      0.433 0.400 0.000 0.600
#&gt; SRR801432     3  0.6225      0.413 0.432 0.000 0.568
#&gt; SRR801433     1  0.0000      0.568 1.000 0.000 0.000
#&gt; SRR825135     3  0.0000      0.775 0.000 0.000 1.000
#&gt; SRR825136     1  0.6126      0.699 0.600 0.000 0.400
#&gt; SRR825137     3  0.0000      0.775 0.000 0.000 1.000
#&gt; SRR825139     1  0.6126      0.699 0.600 0.000 0.400
#&gt; SRR825140     1  0.6126      0.699 0.600 0.000 0.400
#&gt; SRR825141     3  0.0000      0.775 0.000 0.000 1.000
#&gt; SRR825143     1  0.6126      0.699 0.600 0.000 0.400
</code></pre>

<script>
$('#tab-SD-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-2-a').click(function(){
  $('#tab-SD-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-3'>
<p><a id='tab-SD-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     2  0.0000      0.782 0.000 1.000 0.000 0.000
#&gt; SRR547973     2  0.4817      0.813 0.000 0.612 0.000 0.388
#&gt; SRR547968     2  0.4817      0.813 0.000 0.612 0.000 0.388
#&gt; SRR547980     2  0.0000      0.782 0.000 1.000 0.000 0.000
#&gt; SRR545058     3  0.0000      0.978 0.000 0.000 1.000 0.000
#&gt; SRR546225     3  0.0188      0.975 0.004 0.000 0.996 0.000
#&gt; SRR546226     1  0.0000      0.913 1.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000      0.913 1.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.0000      0.978 0.000 0.000 1.000 0.000
#&gt; SRR546229     3  0.0188      0.975 0.004 0.000 0.996 0.000
#&gt; SRR546230     1  0.0000      0.913 1.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.0000      0.978 0.000 0.000 1.000 0.000
#&gt; SRR546232     1  0.0000      0.913 1.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.0000      0.913 1.000 0.000 0.000 0.000
#&gt; SRR546234     3  0.0188      0.975 0.004 0.000 0.996 0.000
#&gt; SRR546235     3  0.0000      0.978 0.000 0.000 1.000 0.000
#&gt; SRR546236     3  0.0000      0.978 0.000 0.000 1.000 0.000
#&gt; SRR546237     1  0.0000      0.913 1.000 0.000 0.000 0.000
#&gt; SRR546238     3  0.0000      0.978 0.000 0.000 1.000 0.000
#&gt; SRR546239     1  0.4957      0.402 0.668 0.000 0.320 0.012
#&gt; SRR546240     1  0.3649      0.619 0.796 0.000 0.204 0.000
#&gt; SRR547969     2  0.4817      0.813 0.000 0.612 0.000 0.388
#&gt; SRR547970     2  0.0000      0.782 0.000 1.000 0.000 0.000
#&gt; SRR547971     2  0.0000      0.782 0.000 1.000 0.000 0.000
#&gt; SRR547972     2  0.4817      0.813 0.000 0.612 0.000 0.388
#&gt; SRR547974     2  0.0000      0.782 0.000 1.000 0.000 0.000
#&gt; SRR547976     2  0.4817      0.813 0.000 0.612 0.000 0.388
#&gt; SRR547978     2  0.0000      0.782 0.000 1.000 0.000 0.000
#&gt; SRR547979     2  0.4817      0.813 0.000 0.612 0.000 0.388
#&gt; SRR547981     2  0.0000      0.782 0.000 1.000 0.000 0.000
#&gt; SRR547982     2  0.4817      0.813 0.000 0.612 0.000 0.388
#&gt; SRR547983     2  0.4817      0.813 0.000 0.612 0.000 0.388
#&gt; SRR547989     2  0.4817      0.813 0.000 0.612 0.000 0.388
#&gt; SRR547990     2  0.3219      0.623 0.000 0.836 0.164 0.000
#&gt; SRR547991     2  0.0000      0.782 0.000 1.000 0.000 0.000
#&gt; SRR547992     2  0.4817      0.813 0.000 0.612 0.000 0.388
#&gt; SRR801424     4  0.4817      0.689 0.388 0.000 0.000 0.612
#&gt; SRR801425     3  0.3610      0.692 0.000 0.000 0.800 0.200
#&gt; SRR801426     4  0.5244      0.417 0.012 0.000 0.388 0.600
#&gt; SRR801427     4  0.4866      0.671 0.404 0.000 0.000 0.596
#&gt; SRR801428     4  0.4817      0.689 0.388 0.000 0.000 0.612
#&gt; SRR801429     4  0.6071      0.685 0.324 0.000 0.064 0.612
#&gt; SRR801430     4  0.4817      0.689 0.388 0.000 0.000 0.612
#&gt; SRR801431     4  0.4830      0.406 0.000 0.000 0.392 0.608
#&gt; SRR801432     4  0.4978      0.420 0.004 0.000 0.384 0.612
#&gt; SRR801433     4  0.4817      0.689 0.388 0.000 0.000 0.612
#&gt; SRR825135     3  0.0000      0.978 0.000 0.000 1.000 0.000
#&gt; SRR825136     1  0.0188      0.910 0.996 0.000 0.000 0.004
#&gt; SRR825137     3  0.0000      0.978 0.000 0.000 1.000 0.000
#&gt; SRR825139     1  0.0336      0.906 0.992 0.000 0.000 0.008
#&gt; SRR825140     1  0.0000      0.913 1.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0000      0.978 0.000 0.000 1.000 0.000
#&gt; SRR825143     1  0.0000      0.913 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-3-a').click(function(){
  $('#tab-SD-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-4'>
<p><a id='tab-SD-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR547975     5  0.0000      0.989 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547973     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547968     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547980     5  0.0000      0.989 0.000 0.000 0.000 0.000 1.000
#&gt; SRR545058     3  0.0000      0.972 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546225     3  0.1270      0.927 0.052 0.000 0.948 0.000 0.000
#&gt; SRR546226     1  0.0000      0.922 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000      0.922 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.0000      0.972 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546229     3  0.0000      0.972 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546230     1  0.0000      0.922 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.0000      0.972 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546232     1  0.0000      0.922 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.0000      0.922 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546234     3  0.0963      0.943 0.036 0.000 0.964 0.000 0.000
#&gt; SRR546235     3  0.0000      0.972 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546236     3  0.0000      0.972 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546237     1  0.0000      0.922 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546238     3  0.0000      0.972 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546239     1  0.5579      0.456 0.600 0.000 0.100 0.300 0.000
#&gt; SRR546240     1  0.3143      0.717 0.796 0.000 0.204 0.000 0.000
#&gt; SRR547969     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547970     5  0.0000      0.989 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547971     5  0.0000      0.989 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547972     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547974     5  0.1792      0.905 0.000 0.084 0.000 0.000 0.916
#&gt; SRR547976     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547978     5  0.0000      0.989 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547979     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547981     5  0.0000      0.989 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547982     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547983     2  0.0162      0.997 0.000 0.996 0.000 0.004 0.000
#&gt; SRR547989     2  0.0162      0.997 0.000 0.996 0.000 0.004 0.000
#&gt; SRR547990     5  0.0000      0.989 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547991     5  0.0000      0.989 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547992     2  0.0000      0.999 0.000 1.000 0.000 0.000 0.000
#&gt; SRR801424     4  0.0162      0.879 0.004 0.000 0.000 0.996 0.000
#&gt; SRR801425     3  0.3109      0.719 0.000 0.000 0.800 0.200 0.000
#&gt; SRR801426     4  0.4118      0.492 0.004 0.000 0.336 0.660 0.000
#&gt; SRR801427     4  0.4192      0.364 0.404 0.000 0.000 0.596 0.000
#&gt; SRR801428     4  0.0162      0.879 0.004 0.000 0.000 0.996 0.000
#&gt; SRR801429     4  0.0162      0.879 0.004 0.000 0.000 0.996 0.000
#&gt; SRR801430     4  0.0162      0.879 0.004 0.000 0.000 0.996 0.000
#&gt; SRR801431     4  0.2424      0.791 0.000 0.000 0.132 0.868 0.000
#&gt; SRR801432     4  0.0162      0.877 0.000 0.000 0.004 0.996 0.000
#&gt; SRR801433     4  0.0162      0.879 0.004 0.000 0.000 0.996 0.000
#&gt; SRR825135     3  0.0000      0.972 0.000 0.000 1.000 0.000 0.000
#&gt; SRR825136     1  0.1197      0.896 0.952 0.000 0.000 0.048 0.000
#&gt; SRR825137     3  0.0000      0.972 0.000 0.000 1.000 0.000 0.000
#&gt; SRR825139     1  0.2561      0.818 0.856 0.000 0.000 0.144 0.000
#&gt; SRR825140     1  0.0000      0.922 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0000      0.972 0.000 0.000 1.000 0.000 0.000
#&gt; SRR825143     1  0.0000      0.922 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-4-a').click(function(){
  $('#tab-SD-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-pam-get-classes-5'>
<p><a id='tab-SD-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR547975     5  0.0000      0.957 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547973     2  0.0000      0.966 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547968     2  0.0000      0.966 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547980     5  0.0000      0.957 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR545058     3  0.0000      0.970 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546225     3  0.1141      0.921 0.052 0.000 0.948 0.000 0.000 0.000
#&gt; SRR546226     1  0.0000      0.913 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000      0.913 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.0000      0.970 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546229     3  0.0000      0.970 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546230     1  0.0000      0.913 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.0000      0.970 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546232     1  0.0000      0.913 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.0000      0.913 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546234     3  0.0865      0.938 0.036 0.000 0.964 0.000 0.000 0.000
#&gt; SRR546235     3  0.0000      0.970 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546236     3  0.0000      0.970 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546237     1  0.0000      0.913 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546238     3  0.0000      0.970 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546239     1  0.4986      0.455 0.600 0.000 0.096 0.304 0.000 0.000
#&gt; SRR546240     1  0.2823      0.685 0.796 0.000 0.204 0.000 0.000 0.000
#&gt; SRR547969     2  0.2996      0.703 0.000 0.772 0.000 0.000 0.000 0.228
#&gt; SRR547970     5  0.0000      0.957 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547971     5  0.0000      0.957 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547972     2  0.0000      0.966 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547974     5  0.3288      0.597 0.000 0.276 0.000 0.000 0.724 0.000
#&gt; SRR547976     2  0.0000      0.966 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547978     5  0.0000      0.957 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547979     2  0.0000      0.966 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547981     5  0.0000      0.957 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547982     2  0.0000      0.966 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547983     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547989     6  0.0000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547990     5  0.0000      0.957 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547991     5  0.0000      0.957 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547992     2  0.0000      0.966 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR801424     4  0.0000      0.846 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR801425     3  0.2793      0.719 0.000 0.000 0.800 0.200 0.000 0.000
#&gt; SRR801426     4  0.3578      0.478 0.000 0.000 0.340 0.660 0.000 0.000
#&gt; SRR801427     4  0.3765      0.358 0.404 0.000 0.000 0.596 0.000 0.000
#&gt; SRR801428     4  0.0000      0.846 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR801429     4  0.0000      0.846 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR801430     4  0.0000      0.846 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR801431     4  0.2178      0.733 0.000 0.000 0.132 0.868 0.000 0.000
#&gt; SRR801432     4  0.0000      0.846 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR801433     4  0.0000      0.846 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR825135     3  0.0000      0.970 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR825136     1  0.1075      0.885 0.952 0.000 0.000 0.048 0.000 0.000
#&gt; SRR825137     3  0.0000      0.970 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR825139     1  0.2340      0.801 0.852 0.000 0.000 0.148 0.000 0.000
#&gt; SRR825140     1  0.0000      0.913 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0000      0.970 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR825143     1  0.0000      0.913 1.000 0.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-pam-get-classes-5-a').click(function(){
  $('#tab-SD-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-pam-membership-heatmap'>
<ul>
<li><a href='#tab-SD-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-signatures'>
<ul>
<li><a href='#tab-SD-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-1-1.png" alt="plot of chunk tab-SD-pam-get-signatures-1"/></p>

</div>
<div id='tab-SD-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-2-1.png" alt="plot of chunk tab-SD-pam-get-signatures-2"/></p>

</div>
<div id='tab-SD-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-3-1.png" alt="plot of chunk tab-SD-pam-get-signatures-3"/></p>

</div>
<div id='tab-SD-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-4-1.png" alt="plot of chunk tab-SD-pam-get-signatures-4"/></p>

</div>
<div id='tab-SD-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-5-1.png" alt="plot of chunk tab-SD-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-pam-signature_compare](figure_cola/SD-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-pam-dimension-reduction'>
<ul>
<li><a href='#tab-SD-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-pam-collect-classes](figure_cola/SD-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:mclust*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "mclust"]
# you can also extract it by
# res = res_list["SD:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-mclust-collect-plots](figure_cola/SD-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-mclust-select-partition-number](figure_cola/SD-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.566           0.896       0.924         0.4664 0.531   0.531
#> 3 3 0.792           0.689       0.822         0.3940 0.793   0.611
#> 4 4 0.814           0.801       0.841         0.1441 0.872   0.639
#> 5 5 0.922           0.890       0.932         0.0743 0.935   0.744
#> 6 6 0.918           0.860       0.934         0.0316 0.949   0.753
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 5
```

There is also optional best $k$ = 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-classes'>
<ul>
<li><a href='#tab-SD-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-mclust-get-classes-1'>
<p><a id='tab-SD-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR547975     2   0.000      0.999 0.000 1.000
#&gt; SRR547973     2   0.000      0.999 0.000 1.000
#&gt; SRR547968     2   0.000      0.999 0.000 1.000
#&gt; SRR547980     2   0.000      0.999 0.000 1.000
#&gt; SRR545058     1   0.760      0.843 0.780 0.220
#&gt; SRR546225     1   0.999      0.345 0.516 0.484
#&gt; SRR546226     1   0.000      0.865 1.000 0.000
#&gt; SRR546227     1   0.000      0.865 1.000 0.000
#&gt; SRR546228     1   0.760      0.843 0.780 0.220
#&gt; SRR546229     1   0.760      0.843 0.780 0.220
#&gt; SRR546230     1   0.000      0.865 1.000 0.000
#&gt; SRR546231     1   0.760      0.843 0.780 0.220
#&gt; SRR546232     1   0.000      0.865 1.000 0.000
#&gt; SRR546233     1   0.000      0.865 1.000 0.000
#&gt; SRR546234     1   0.760      0.843 0.780 0.220
#&gt; SRR546235     1   0.760      0.843 0.780 0.220
#&gt; SRR546236     1   0.760      0.843 0.780 0.220
#&gt; SRR546237     1   0.000      0.865 1.000 0.000
#&gt; SRR546238     1   0.760      0.843 0.780 0.220
#&gt; SRR546239     1   0.000      0.865 1.000 0.000
#&gt; SRR546240     1   0.000      0.865 1.000 0.000
#&gt; SRR547969     2   0.000      0.999 0.000 1.000
#&gt; SRR547970     2   0.000      0.999 0.000 1.000
#&gt; SRR547971     2   0.000      0.999 0.000 1.000
#&gt; SRR547972     2   0.000      0.999 0.000 1.000
#&gt; SRR547974     2   0.000      0.999 0.000 1.000
#&gt; SRR547976     2   0.000      0.999 0.000 1.000
#&gt; SRR547978     2   0.000      0.999 0.000 1.000
#&gt; SRR547979     2   0.000      0.999 0.000 1.000
#&gt; SRR547981     2   0.000      0.999 0.000 1.000
#&gt; SRR547982     2   0.000      0.999 0.000 1.000
#&gt; SRR547983     2   0.000      0.999 0.000 1.000
#&gt; SRR547989     2   0.000      0.999 0.000 1.000
#&gt; SRR547990     2   0.141      0.975 0.020 0.980
#&gt; SRR547991     2   0.000      0.999 0.000 1.000
#&gt; SRR547992     2   0.000      0.999 0.000 1.000
#&gt; SRR801424     1   0.000      0.865 1.000 0.000
#&gt; SRR801425     1   0.760      0.843 0.780 0.220
#&gt; SRR801426     1   0.760      0.843 0.780 0.220
#&gt; SRR801427     1   0.000      0.865 1.000 0.000
#&gt; SRR801428     1   0.000      0.865 1.000 0.000
#&gt; SRR801429     1   0.760      0.843 0.780 0.220
#&gt; SRR801430     1   0.000      0.865 1.000 0.000
#&gt; SRR801431     1   0.760      0.843 0.780 0.220
#&gt; SRR801432     1   0.760      0.843 0.780 0.220
#&gt; SRR801433     1   0.000      0.865 1.000 0.000
#&gt; SRR825135     1   0.760      0.843 0.780 0.220
#&gt; SRR825136     1   0.000      0.865 1.000 0.000
#&gt; SRR825137     1   0.760      0.843 0.780 0.220
#&gt; SRR825139     1   0.000      0.865 1.000 0.000
#&gt; SRR825140     1   0.000      0.865 1.000 0.000
#&gt; SRR825141     1   0.760      0.843 0.780 0.220
#&gt; SRR825143     1   0.000      0.865 1.000 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-1-a').click(function(){
  $('#tab-SD-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-2'>
<p><a id='tab-SD-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     2  0.0592      0.929 0.000 0.988 0.012
#&gt; SRR547973     2  0.2625      0.942 0.000 0.916 0.084
#&gt; SRR547968     2  0.2625      0.942 0.000 0.916 0.084
#&gt; SRR547980     2  0.0000      0.934 0.000 1.000 0.000
#&gt; SRR545058     3  0.6305      0.714 0.484 0.000 0.516
#&gt; SRR546225     1  0.9528     -0.266 0.484 0.288 0.228
#&gt; SRR546226     1  0.0000      0.705 1.000 0.000 0.000
#&gt; SRR546227     1  0.0000      0.705 1.000 0.000 0.000
#&gt; SRR546228     3  0.6305      0.714 0.484 0.000 0.516
#&gt; SRR546229     3  0.6305      0.714 0.484 0.000 0.516
#&gt; SRR546230     1  0.0000      0.705 1.000 0.000 0.000
#&gt; SRR546231     1  0.6295     -0.665 0.528 0.000 0.472
#&gt; SRR546232     1  0.0000      0.705 1.000 0.000 0.000
#&gt; SRR546233     1  0.0000      0.705 1.000 0.000 0.000
#&gt; SRR546234     3  0.6305      0.714 0.484 0.000 0.516
#&gt; SRR546235     3  0.6305      0.714 0.484 0.000 0.516
#&gt; SRR546236     3  0.6305      0.714 0.484 0.000 0.516
#&gt; SRR546237     1  0.0000      0.705 1.000 0.000 0.000
#&gt; SRR546238     3  0.6305      0.714 0.484 0.000 0.516
#&gt; SRR546239     1  0.0000      0.705 1.000 0.000 0.000
#&gt; SRR546240     1  0.0000      0.705 1.000 0.000 0.000
#&gt; SRR547969     2  0.2625      0.942 0.000 0.916 0.084
#&gt; SRR547970     2  0.0592      0.929 0.000 0.988 0.012
#&gt; SRR547971     2  0.0000      0.934 0.000 1.000 0.000
#&gt; SRR547972     2  0.2625      0.942 0.000 0.916 0.084
#&gt; SRR547974     2  0.0000      0.934 0.000 1.000 0.000
#&gt; SRR547976     2  0.2625      0.942 0.000 0.916 0.084
#&gt; SRR547978     2  0.0000      0.934 0.000 1.000 0.000
#&gt; SRR547979     2  0.2625      0.942 0.000 0.916 0.084
#&gt; SRR547981     2  0.0592      0.929 0.000 0.988 0.012
#&gt; SRR547982     2  0.2625      0.942 0.000 0.916 0.084
#&gt; SRR547983     2  0.2625      0.942 0.000 0.916 0.084
#&gt; SRR547989     2  0.2625      0.942 0.000 0.916 0.084
#&gt; SRR547990     2  0.6661      0.218 0.400 0.588 0.012
#&gt; SRR547991     2  0.0000      0.934 0.000 1.000 0.000
#&gt; SRR547992     2  0.2625      0.942 0.000 0.916 0.084
#&gt; SRR801424     1  0.6126      0.436 0.600 0.000 0.400
#&gt; SRR801425     3  0.2625      0.513 0.084 0.000 0.916
#&gt; SRR801426     3  0.2625      0.513 0.084 0.000 0.916
#&gt; SRR801427     1  0.6126      0.436 0.600 0.000 0.400
#&gt; SRR801428     1  0.6126      0.436 0.600 0.000 0.400
#&gt; SRR801429     3  0.2625      0.513 0.084 0.000 0.916
#&gt; SRR801430     1  0.6126      0.436 0.600 0.000 0.400
#&gt; SRR801431     3  0.2625      0.513 0.084 0.000 0.916
#&gt; SRR801432     3  0.2625      0.513 0.084 0.000 0.916
#&gt; SRR801433     1  0.6126      0.436 0.600 0.000 0.400
#&gt; SRR825135     3  0.6305      0.714 0.484 0.000 0.516
#&gt; SRR825136     1  0.0000      0.705 1.000 0.000 0.000
#&gt; SRR825137     3  0.6305      0.714 0.484 0.000 0.516
#&gt; SRR825139     1  0.0000      0.705 1.000 0.000 0.000
#&gt; SRR825140     1  0.0000      0.705 1.000 0.000 0.000
#&gt; SRR825141     3  0.6305      0.714 0.484 0.000 0.516
#&gt; SRR825143     1  0.0000      0.705 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-2-a').click(function(){
  $('#tab-SD-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-3'>
<p><a id='tab-SD-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     2  0.1452      0.817 0.000 0.956 0.036 0.008
#&gt; SRR547973     2  0.4746      0.783 0.000 0.632 0.000 0.368
#&gt; SRR547968     2  0.4746      0.783 0.000 0.632 0.000 0.368
#&gt; SRR547980     2  0.0000      0.836 0.000 1.000 0.000 0.000
#&gt; SRR545058     3  0.0000      0.939 0.000 0.000 1.000 0.000
#&gt; SRR546225     3  0.2466      0.856 0.000 0.028 0.916 0.056
#&gt; SRR546226     1  0.0000      0.973 1.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000      0.973 1.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.0000      0.939 0.000 0.000 1.000 0.000
#&gt; SRR546229     3  0.1940      0.912 0.000 0.000 0.924 0.076
#&gt; SRR546230     1  0.0000      0.973 1.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.1867      0.917 0.000 0.000 0.928 0.072
#&gt; SRR546232     1  0.0000      0.973 1.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.0000      0.973 1.000 0.000 0.000 0.000
#&gt; SRR546234     3  0.1389      0.900 0.000 0.000 0.952 0.048
#&gt; SRR546235     3  0.1637      0.925 0.000 0.000 0.940 0.060
#&gt; SRR546236     3  0.0000      0.939 0.000 0.000 1.000 0.000
#&gt; SRR546237     1  0.0000      0.973 1.000 0.000 0.000 0.000
#&gt; SRR546238     3  0.0000      0.939 0.000 0.000 1.000 0.000
#&gt; SRR546239     1  0.0000      0.973 1.000 0.000 0.000 0.000
#&gt; SRR546240     1  0.0000      0.973 1.000 0.000 0.000 0.000
#&gt; SRR547969     2  0.4746      0.783 0.000 0.632 0.000 0.368
#&gt; SRR547970     2  0.1389      0.817 0.000 0.952 0.000 0.048
#&gt; SRR547971     2  0.0000      0.836 0.000 1.000 0.000 0.000
#&gt; SRR547972     2  0.4746      0.783 0.000 0.632 0.000 0.368
#&gt; SRR547974     2  0.0000      0.836 0.000 1.000 0.000 0.000
#&gt; SRR547976     2  0.4746      0.783 0.000 0.632 0.000 0.368
#&gt; SRR547978     2  0.0000      0.836 0.000 1.000 0.000 0.000
#&gt; SRR547979     2  0.4746      0.783 0.000 0.632 0.000 0.368
#&gt; SRR547981     2  0.1389      0.817 0.000 0.952 0.000 0.048
#&gt; SRR547982     2  0.4746      0.783 0.000 0.632 0.000 0.368
#&gt; SRR547983     2  0.0336      0.836 0.000 0.992 0.000 0.008
#&gt; SRR547989     2  0.0336      0.836 0.000 0.992 0.000 0.008
#&gt; SRR547990     2  0.2926      0.779 0.000 0.896 0.056 0.048
#&gt; SRR547991     2  0.0000      0.836 0.000 1.000 0.000 0.000
#&gt; SRR547992     2  0.4746      0.783 0.000 0.632 0.000 0.368
#&gt; SRR801424     4  0.4907      0.380 0.420 0.000 0.000 0.580
#&gt; SRR801425     4  0.4955      0.462 0.000 0.000 0.444 0.556
#&gt; SRR801426     4  0.4955      0.462 0.000 0.000 0.444 0.556
#&gt; SRR801427     1  0.4072      0.555 0.748 0.000 0.000 0.252
#&gt; SRR801428     4  0.4907      0.380 0.420 0.000 0.000 0.580
#&gt; SRR801429     4  0.4955      0.462 0.000 0.000 0.444 0.556
#&gt; SRR801430     4  0.4907      0.380 0.420 0.000 0.000 0.580
#&gt; SRR801431     4  0.4955      0.462 0.000 0.000 0.444 0.556
#&gt; SRR801432     4  0.4955      0.462 0.000 0.000 0.444 0.556
#&gt; SRR801433     4  0.4907      0.380 0.420 0.000 0.000 0.580
#&gt; SRR825135     3  0.0000      0.939 0.000 0.000 1.000 0.000
#&gt; SRR825136     1  0.0000      0.973 1.000 0.000 0.000 0.000
#&gt; SRR825137     3  0.1637      0.925 0.000 0.000 0.940 0.060
#&gt; SRR825139     1  0.0000      0.973 1.000 0.000 0.000 0.000
#&gt; SRR825140     1  0.0000      0.973 1.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.1867      0.917 0.000 0.000 0.928 0.072
#&gt; SRR825143     1  0.0000      0.973 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-3-a').click(function(){
  $('#tab-SD-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-4'>
<p><a id='tab-SD-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR547975     5  0.0162      0.975 0.000 0.004 0.000 0.000 0.996
#&gt; SRR547973     2  0.0000      0.917 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547968     2  0.0000      0.917 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547980     5  0.0963      0.980 0.000 0.036 0.000 0.000 0.964
#&gt; SRR545058     3  0.0000      0.983 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546225     3  0.1518      0.958 0.000 0.016 0.952 0.020 0.012
#&gt; SRR546226     1  0.0000      0.966 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000      0.966 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.0000      0.983 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546229     3  0.1341      0.944 0.000 0.000 0.944 0.056 0.000
#&gt; SRR546230     1  0.0000      0.966 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.0404      0.980 0.000 0.000 0.988 0.012 0.000
#&gt; SRR546232     1  0.0000      0.966 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.0290      0.964 0.992 0.000 0.000 0.008 0.000
#&gt; SRR546234     3  0.1012      0.971 0.000 0.000 0.968 0.020 0.012
#&gt; SRR546235     3  0.0404      0.980 0.000 0.000 0.988 0.012 0.000
#&gt; SRR546236     3  0.0404      0.980 0.000 0.000 0.988 0.012 0.000
#&gt; SRR546237     1  0.0000      0.966 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546238     3  0.0000      0.983 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546239     1  0.0290      0.964 0.992 0.000 0.000 0.008 0.000
#&gt; SRR546240     1  0.0290      0.964 0.992 0.000 0.000 0.008 0.000
#&gt; SRR547969     2  0.0000      0.917 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547970     5  0.0000      0.974 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547971     5  0.0963      0.980 0.000 0.036 0.000 0.000 0.964
#&gt; SRR547972     2  0.0000      0.917 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547974     5  0.0963      0.980 0.000 0.036 0.000 0.000 0.964
#&gt; SRR547976     2  0.0000      0.917 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547978     5  0.0963      0.980 0.000 0.036 0.000 0.000 0.964
#&gt; SRR547979     2  0.0000      0.917 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547981     5  0.0000      0.974 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547982     2  0.0000      0.917 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547983     2  0.3999      0.513 0.000 0.656 0.000 0.000 0.344
#&gt; SRR547989     2  0.3983      0.520 0.000 0.660 0.000 0.000 0.340
#&gt; SRR547990     5  0.0000      0.974 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547991     5  0.0963      0.980 0.000 0.036 0.000 0.000 0.964
#&gt; SRR547992     2  0.0000      0.917 0.000 1.000 0.000 0.000 0.000
#&gt; SRR801424     4  0.2773      0.639 0.164 0.000 0.000 0.836 0.000
#&gt; SRR801425     4  0.4126      0.665 0.000 0.000 0.380 0.620 0.000
#&gt; SRR801426     4  0.3983      0.708 0.000 0.000 0.340 0.660 0.000
#&gt; SRR801427     1  0.3983      0.445 0.660 0.000 0.000 0.340 0.000
#&gt; SRR801428     4  0.1043      0.709 0.040 0.000 0.000 0.960 0.000
#&gt; SRR801429     4  0.3983      0.708 0.000 0.000 0.340 0.660 0.000
#&gt; SRR801430     4  0.1043      0.709 0.040 0.000 0.000 0.960 0.000
#&gt; SRR801431     4  0.3983      0.708 0.000 0.000 0.340 0.660 0.000
#&gt; SRR801432     4  0.3983      0.708 0.000 0.000 0.340 0.660 0.000
#&gt; SRR801433     4  0.1043      0.709 0.040 0.000 0.000 0.960 0.000
#&gt; SRR825135     3  0.0000      0.983 0.000 0.000 1.000 0.000 0.000
#&gt; SRR825136     1  0.0290      0.964 0.992 0.000 0.000 0.008 0.000
#&gt; SRR825137     3  0.0000      0.983 0.000 0.000 1.000 0.000 0.000
#&gt; SRR825139     1  0.0290      0.964 0.992 0.000 0.000 0.008 0.000
#&gt; SRR825140     1  0.0000      0.966 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0404      0.980 0.000 0.000 0.988 0.012 0.000
#&gt; SRR825143     1  0.0000      0.966 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-4-a').click(function(){
  $('#tab-SD-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-mclust-get-classes-5'>
<p><a id='tab-SD-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR547975     5  0.0000      0.870 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547973     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547968     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547980     5  0.1075      0.880 0.000 0.048 0.000 0.000 0.952 0.000
#&gt; SRR545058     3  0.0363      0.912 0.000 0.000 0.988 0.012 0.000 0.000
#&gt; SRR546225     3  0.4959      0.637 0.004 0.000 0.696 0.112 0.172 0.016
#&gt; SRR546226     1  0.0146      0.985 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR546227     1  0.0260      0.984 0.992 0.000 0.000 0.000 0.000 0.008
#&gt; SRR546228     3  0.0363      0.912 0.000 0.000 0.988 0.012 0.000 0.000
#&gt; SRR546229     3  0.2416      0.846 0.000 0.000 0.844 0.156 0.000 0.000
#&gt; SRR546230     1  0.0260      0.985 0.992 0.000 0.000 0.000 0.000 0.008
#&gt; SRR546231     3  0.1910      0.873 0.000 0.000 0.892 0.108 0.000 0.000
#&gt; SRR546232     1  0.0146      0.985 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR546233     1  0.0937      0.960 0.960 0.000 0.000 0.000 0.000 0.040
#&gt; SRR546234     3  0.2547      0.863 0.004 0.000 0.868 0.112 0.000 0.016
#&gt; SRR546235     3  0.0458      0.910 0.000 0.000 0.984 0.016 0.000 0.000
#&gt; SRR546236     3  0.1957      0.873 0.000 0.000 0.888 0.112 0.000 0.000
#&gt; SRR546237     1  0.0363      0.977 0.988 0.000 0.000 0.000 0.000 0.012
#&gt; SRR546238     3  0.0363      0.912 0.000 0.000 0.988 0.012 0.000 0.000
#&gt; SRR546239     1  0.0146      0.985 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR546240     1  0.0363      0.977 0.988 0.000 0.000 0.000 0.000 0.012
#&gt; SRR547969     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547970     5  0.0000      0.870 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547971     5  0.1075      0.880 0.000 0.048 0.000 0.000 0.952 0.000
#&gt; SRR547972     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547974     5  0.0937      0.880 0.000 0.040 0.000 0.000 0.960 0.000
#&gt; SRR547976     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547978     5  0.1204      0.877 0.000 0.056 0.000 0.000 0.944 0.000
#&gt; SRR547979     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547981     5  0.0000      0.870 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547982     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547983     5  0.3838      0.329 0.000 0.448 0.000 0.000 0.552 0.000
#&gt; SRR547989     5  0.3838      0.329 0.000 0.448 0.000 0.000 0.552 0.000
#&gt; SRR547990     5  0.0000      0.870 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547991     5  0.1141      0.879 0.000 0.052 0.000 0.000 0.948 0.000
#&gt; SRR547992     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR801424     6  0.2823      0.716 0.204 0.000 0.000 0.000 0.000 0.796
#&gt; SRR801425     4  0.3867      0.161 0.000 0.000 0.488 0.512 0.000 0.000
#&gt; SRR801426     4  0.1610      0.786 0.000 0.000 0.084 0.916 0.000 0.000
#&gt; SRR801427     6  0.3823      0.331 0.436 0.000 0.000 0.000 0.000 0.564
#&gt; SRR801428     6  0.0458      0.786 0.016 0.000 0.000 0.000 0.000 0.984
#&gt; SRR801429     4  0.0000      0.821 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR801430     6  0.0458      0.786 0.016 0.000 0.000 0.000 0.000 0.984
#&gt; SRR801431     4  0.0000      0.821 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR801432     4  0.0000      0.821 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR801433     6  0.0458      0.786 0.016 0.000 0.000 0.000 0.000 0.984
#&gt; SRR825135     3  0.0363      0.912 0.000 0.000 0.988 0.012 0.000 0.000
#&gt; SRR825136     1  0.1007      0.956 0.956 0.000 0.000 0.000 0.000 0.044
#&gt; SRR825137     3  0.0000      0.909 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR825139     1  0.0363      0.983 0.988 0.000 0.000 0.000 0.000 0.012
#&gt; SRR825140     1  0.0146      0.985 0.996 0.000 0.000 0.000 0.000 0.004
#&gt; SRR825141     3  0.0458      0.910 0.000 0.000 0.984 0.016 0.000 0.000
#&gt; SRR825143     1  0.0260      0.984 0.992 0.000 0.000 0.000 0.000 0.008
</code></pre>

<script>
$('#tab-SD-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-mclust-get-classes-5-a').click(function(){
  $('#tab-SD-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-SD-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-signatures'>
<ul>
<li><a href='#tab-SD-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-1-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-1"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-2-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-2"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-3-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-3"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-4-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-4"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-5-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-mclust-signature_compare](figure_cola/SD-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-SD-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-mclust-collect-classes](figure_cola/SD-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### SD:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["SD", "NMF"]
# you can also extract it by
# res = res_list["SD:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'SD' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk SD-NMF-collect-plots](figure_cola/SD-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk SD-NMF-select-partition-number](figure_cola/SD-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.982       0.991         0.4823 0.521   0.521
#> 3 3 0.591           0.504       0.748         0.3021 0.955   0.914
#> 4 4 0.753           0.825       0.859         0.1826 0.724   0.450
#> 5 5 0.820           0.782       0.877         0.0759 0.888   0.594
#> 6 6 0.832           0.759       0.884         0.0355 0.974   0.864
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-SD-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-classes'>
<ul>
<li><a href='#tab-SD-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-SD-NMF-get-classes-1'>
<p><a id='tab-SD-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR547975     2   0.000      0.998 0.000 1.000
#&gt; SRR547973     2   0.000      0.998 0.000 1.000
#&gt; SRR547968     2   0.000      0.998 0.000 1.000
#&gt; SRR547980     2   0.000      0.998 0.000 1.000
#&gt; SRR545058     1   0.000      0.987 1.000 0.000
#&gt; SRR546225     2   0.242      0.957 0.040 0.960
#&gt; SRR546226     1   0.000      0.987 1.000 0.000
#&gt; SRR546227     1   0.000      0.987 1.000 0.000
#&gt; SRR546228     1   0.000      0.987 1.000 0.000
#&gt; SRR546229     1   0.000      0.987 1.000 0.000
#&gt; SRR546230     1   0.000      0.987 1.000 0.000
#&gt; SRR546231     1   0.000      0.987 1.000 0.000
#&gt; SRR546232     1   0.000      0.987 1.000 0.000
#&gt; SRR546233     1   0.000      0.987 1.000 0.000
#&gt; SRR546234     1   0.000      0.987 1.000 0.000
#&gt; SRR546235     1   0.000      0.987 1.000 0.000
#&gt; SRR546236     1   0.000      0.987 1.000 0.000
#&gt; SRR546237     1   0.000      0.987 1.000 0.000
#&gt; SRR546238     1   0.242      0.953 0.960 0.040
#&gt; SRR546239     1   0.000      0.987 1.000 0.000
#&gt; SRR546240     1   0.000      0.987 1.000 0.000
#&gt; SRR547969     2   0.000      0.998 0.000 1.000
#&gt; SRR547970     2   0.000      0.998 0.000 1.000
#&gt; SRR547971     2   0.000      0.998 0.000 1.000
#&gt; SRR547972     2   0.000      0.998 0.000 1.000
#&gt; SRR547974     2   0.000      0.998 0.000 1.000
#&gt; SRR547976     2   0.000      0.998 0.000 1.000
#&gt; SRR547978     2   0.000      0.998 0.000 1.000
#&gt; SRR547979     2   0.000      0.998 0.000 1.000
#&gt; SRR547981     2   0.000      0.998 0.000 1.000
#&gt; SRR547982     2   0.000      0.998 0.000 1.000
#&gt; SRR547983     2   0.000      0.998 0.000 1.000
#&gt; SRR547989     2   0.000      0.998 0.000 1.000
#&gt; SRR547990     2   0.000      0.998 0.000 1.000
#&gt; SRR547991     2   0.000      0.998 0.000 1.000
#&gt; SRR547992     2   0.000      0.998 0.000 1.000
#&gt; SRR801424     1   0.000      0.987 1.000 0.000
#&gt; SRR801425     1   0.204      0.960 0.968 0.032
#&gt; SRR801426     1   0.416      0.908 0.916 0.084
#&gt; SRR801427     1   0.000      0.987 1.000 0.000
#&gt; SRR801428     1   0.000      0.987 1.000 0.000
#&gt; SRR801429     1   0.000      0.987 1.000 0.000
#&gt; SRR801430     1   0.000      0.987 1.000 0.000
#&gt; SRR801431     1   0.000      0.987 1.000 0.000
#&gt; SRR801432     1   0.827      0.659 0.740 0.260
#&gt; SRR801433     1   0.000      0.987 1.000 0.000
#&gt; SRR825135     1   0.000      0.987 1.000 0.000
#&gt; SRR825136     1   0.000      0.987 1.000 0.000
#&gt; SRR825137     1   0.000      0.987 1.000 0.000
#&gt; SRR825139     1   0.000      0.987 1.000 0.000
#&gt; SRR825140     1   0.000      0.987 1.000 0.000
#&gt; SRR825141     1   0.000      0.987 1.000 0.000
#&gt; SRR825143     1   0.000      0.987 1.000 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-1-a').click(function(){
  $('#tab-SD-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-2'>
<p><a id='tab-SD-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     2  0.0000     0.7528 0.000 1.000 0.000
#&gt; SRR547973     2  0.6302     0.6691 0.000 0.520 0.480
#&gt; SRR547968     2  0.6302     0.6691 0.000 0.520 0.480
#&gt; SRR547980     2  0.0000     0.7528 0.000 1.000 0.000
#&gt; SRR545058     1  0.6062     0.4891 0.616 0.000 0.384
#&gt; SRR546225     2  0.9055     0.0853 0.196 0.552 0.252
#&gt; SRR546226     1  0.0747     0.5222 0.984 0.000 0.016
#&gt; SRR546227     1  0.0237     0.5190 0.996 0.000 0.004
#&gt; SRR546228     1  0.6062     0.4891 0.616 0.000 0.384
#&gt; SRR546229     1  0.6062     0.4891 0.616 0.000 0.384
#&gt; SRR546230     1  0.1289     0.4982 0.968 0.000 0.032
#&gt; SRR546231     1  0.6062     0.4891 0.616 0.000 0.384
#&gt; SRR546232     1  0.2165     0.5263 0.936 0.000 0.064
#&gt; SRR546233     1  0.3267     0.3977 0.884 0.000 0.116
#&gt; SRR546234     1  0.6062     0.4891 0.616 0.000 0.384
#&gt; SRR546235     1  0.6062     0.4891 0.616 0.000 0.384
#&gt; SRR546236     1  0.6062     0.4891 0.616 0.000 0.384
#&gt; SRR546237     1  0.3482     0.5247 0.872 0.000 0.128
#&gt; SRR546238     1  0.9348     0.2098 0.448 0.168 0.384
#&gt; SRR546239     1  0.0592     0.5215 0.988 0.000 0.012
#&gt; SRR546240     1  0.4235     0.5212 0.824 0.000 0.176
#&gt; SRR547969     2  0.6291     0.6742 0.000 0.532 0.468
#&gt; SRR547970     2  0.0237     0.7505 0.000 0.996 0.004
#&gt; SRR547971     2  0.0000     0.7528 0.000 1.000 0.000
#&gt; SRR547972     2  0.6302     0.6691 0.000 0.520 0.480
#&gt; SRR547974     2  0.0000     0.7528 0.000 1.000 0.000
#&gt; SRR547976     2  0.5785     0.7227 0.000 0.668 0.332
#&gt; SRR547978     2  0.0000     0.7528 0.000 1.000 0.000
#&gt; SRR547979     2  0.6299     0.6708 0.000 0.524 0.476
#&gt; SRR547981     2  0.0424     0.7479 0.000 0.992 0.008
#&gt; SRR547982     2  0.6302     0.6691 0.000 0.520 0.480
#&gt; SRR547983     2  0.5291     0.7367 0.000 0.732 0.268
#&gt; SRR547989     2  0.5291     0.7367 0.000 0.732 0.268
#&gt; SRR547990     2  0.0000     0.7528 0.000 1.000 0.000
#&gt; SRR547991     2  0.0000     0.7528 0.000 1.000 0.000
#&gt; SRR547992     2  0.6302     0.6691 0.000 0.520 0.480
#&gt; SRR801424     1  0.3619     0.3661 0.864 0.000 0.136
#&gt; SRR801425     1  0.6518     0.3027 0.512 0.004 0.484
#&gt; SRR801426     3  0.6026     0.2487 0.376 0.000 0.624
#&gt; SRR801427     1  0.3619     0.3661 0.864 0.000 0.136
#&gt; SRR801428     1  0.3686     0.3579 0.860 0.000 0.140
#&gt; SRR801429     1  0.6215    -0.5990 0.572 0.000 0.428
#&gt; SRR801430     1  0.3941     0.3202 0.844 0.000 0.156
#&gt; SRR801431     1  0.6204    -0.2584 0.576 0.000 0.424
#&gt; SRR801432     3  0.6521     0.4113 0.496 0.004 0.500
#&gt; SRR801433     1  0.3941     0.3202 0.844 0.000 0.156
#&gt; SRR825135     1  0.6062     0.4891 0.616 0.000 0.384
#&gt; SRR825136     1  0.2165     0.4669 0.936 0.000 0.064
#&gt; SRR825137     1  0.6062     0.4891 0.616 0.000 0.384
#&gt; SRR825139     1  0.1289     0.4982 0.968 0.000 0.032
#&gt; SRR825140     1  0.0237     0.5190 0.996 0.000 0.004
#&gt; SRR825141     1  0.6062     0.4891 0.616 0.000 0.384
#&gt; SRR825143     1  0.1163     0.5011 0.972 0.000 0.028
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-2-a').click(function(){
  $('#tab-SD-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-3'>
<p><a id='tab-SD-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     2  0.0188      0.996 0.000 0.996 0.000 0.004
#&gt; SRR547973     4  0.1059      0.873 0.016 0.012 0.000 0.972
#&gt; SRR547968     4  0.1059      0.873 0.016 0.012 0.000 0.972
#&gt; SRR547980     2  0.0188      0.996 0.000 0.996 0.000 0.004
#&gt; SRR545058     3  0.0188      0.902 0.004 0.000 0.996 0.000
#&gt; SRR546225     3  0.6761      0.426 0.000 0.168 0.608 0.224
#&gt; SRR546226     1  0.3688      0.847 0.792 0.000 0.208 0.000
#&gt; SRR546227     1  0.3688      0.847 0.792 0.000 0.208 0.000
#&gt; SRR546228     3  0.0188      0.902 0.004 0.000 0.996 0.000
#&gt; SRR546229     3  0.1635      0.876 0.044 0.000 0.948 0.008
#&gt; SRR546230     1  0.3444      0.853 0.816 0.000 0.184 0.000
#&gt; SRR546231     3  0.0188      0.902 0.004 0.000 0.996 0.000
#&gt; SRR546232     1  0.3801      0.839 0.780 0.000 0.220 0.000
#&gt; SRR546233     1  0.2704      0.839 0.876 0.000 0.124 0.000
#&gt; SRR546234     3  0.0188      0.902 0.004 0.000 0.996 0.000
#&gt; SRR546235     3  0.0188      0.902 0.004 0.000 0.996 0.000
#&gt; SRR546236     3  0.0188      0.902 0.004 0.000 0.996 0.000
#&gt; SRR546237     1  0.3907      0.829 0.768 0.000 0.232 0.000
#&gt; SRR546238     3  0.0188      0.899 0.000 0.004 0.996 0.000
#&gt; SRR546239     1  0.3726      0.845 0.788 0.000 0.212 0.000
#&gt; SRR546240     1  0.4431      0.754 0.696 0.000 0.304 0.000
#&gt; SRR547969     4  0.1022      0.874 0.000 0.032 0.000 0.968
#&gt; SRR547970     2  0.0000      0.994 0.000 1.000 0.000 0.000
#&gt; SRR547971     2  0.0188      0.996 0.000 0.996 0.000 0.004
#&gt; SRR547972     4  0.0592      0.877 0.000 0.016 0.000 0.984
#&gt; SRR547974     2  0.0188      0.996 0.000 0.996 0.000 0.004
#&gt; SRR547976     4  0.3300      0.801 0.008 0.144 0.000 0.848
#&gt; SRR547978     2  0.0336      0.993 0.000 0.992 0.000 0.008
#&gt; SRR547979     4  0.0817      0.877 0.000 0.024 0.000 0.976
#&gt; SRR547981     2  0.0000      0.994 0.000 1.000 0.000 0.000
#&gt; SRR547982     4  0.0592      0.877 0.000 0.016 0.000 0.984
#&gt; SRR547983     4  0.4331      0.647 0.000 0.288 0.000 0.712
#&gt; SRR547989     4  0.4331      0.647 0.000 0.288 0.000 0.712
#&gt; SRR547990     2  0.0000      0.994 0.000 1.000 0.000 0.000
#&gt; SRR547991     2  0.0707      0.983 0.000 0.980 0.000 0.020
#&gt; SRR547992     4  0.0779      0.877 0.004 0.016 0.000 0.980
#&gt; SRR801424     1  0.2413      0.764 0.916 0.000 0.064 0.020
#&gt; SRR801425     3  0.4381      0.753 0.200 0.008 0.780 0.012
#&gt; SRR801426     3  0.5820      0.667 0.232 0.000 0.684 0.084
#&gt; SRR801427     1  0.1182      0.783 0.968 0.000 0.016 0.016
#&gt; SRR801428     1  0.1890      0.761 0.936 0.000 0.008 0.056
#&gt; SRR801429     1  0.6801     -0.213 0.456 0.000 0.096 0.448
#&gt; SRR801430     1  0.2271      0.747 0.916 0.000 0.008 0.076
#&gt; SRR801431     3  0.4644      0.730 0.228 0.000 0.748 0.024
#&gt; SRR801432     4  0.6958      0.442 0.232 0.000 0.184 0.584
#&gt; SRR801433     1  0.2048      0.756 0.928 0.000 0.008 0.064
#&gt; SRR825135     3  0.0188      0.902 0.004 0.000 0.996 0.000
#&gt; SRR825136     1  0.3123      0.849 0.844 0.000 0.156 0.000
#&gt; SRR825137     3  0.0188      0.902 0.004 0.000 0.996 0.000
#&gt; SRR825139     1  0.3444      0.853 0.816 0.000 0.184 0.000
#&gt; SRR825140     1  0.3688      0.847 0.792 0.000 0.208 0.000
#&gt; SRR825141     3  0.0188      0.902 0.004 0.000 0.996 0.000
#&gt; SRR825143     1  0.3444      0.853 0.816 0.000 0.184 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-3-a').click(function(){
  $('#tab-SD-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-4'>
<p><a id='tab-SD-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR547975     5  0.0000      0.956 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547973     2  0.2338      0.848 0.004 0.884 0.000 0.112 0.000
#&gt; SRR547968     2  0.1908      0.861 0.000 0.908 0.000 0.092 0.000
#&gt; SRR547980     5  0.1041      0.947 0.004 0.000 0.000 0.032 0.964
#&gt; SRR545058     3  0.0290      0.957 0.000 0.000 0.992 0.008 0.000
#&gt; SRR546225     2  0.4383      0.278 0.000 0.572 0.424 0.004 0.000
#&gt; SRR546226     1  0.0609      0.866 0.980 0.000 0.020 0.000 0.000
#&gt; SRR546227     1  0.0609      0.866 0.980 0.000 0.020 0.000 0.000
#&gt; SRR546228     3  0.0000      0.956 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546229     3  0.3177      0.737 0.000 0.000 0.792 0.208 0.000
#&gt; SRR546230     1  0.0566      0.865 0.984 0.000 0.012 0.004 0.000
#&gt; SRR546231     3  0.0162      0.954 0.000 0.000 0.996 0.004 0.000
#&gt; SRR546232     1  0.0865      0.863 0.972 0.000 0.024 0.004 0.000
#&gt; SRR546233     1  0.0579      0.863 0.984 0.000 0.008 0.008 0.000
#&gt; SRR546234     3  0.0693      0.944 0.000 0.012 0.980 0.008 0.000
#&gt; SRR546235     3  0.0290      0.957 0.000 0.000 0.992 0.008 0.000
#&gt; SRR546236     3  0.0000      0.956 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546237     1  0.3318      0.685 0.800 0.000 0.192 0.008 0.000
#&gt; SRR546238     3  0.1430      0.936 0.000 0.004 0.944 0.052 0.000
#&gt; SRR546239     1  0.2707      0.780 0.876 0.000 0.024 0.100 0.000
#&gt; SRR546240     1  0.4470      0.427 0.616 0.000 0.372 0.012 0.000
#&gt; SRR547969     2  0.2411      0.848 0.008 0.884 0.000 0.108 0.000
#&gt; SRR547970     5  0.0703      0.949 0.000 0.000 0.000 0.024 0.976
#&gt; SRR547971     5  0.0324      0.955 0.004 0.000 0.000 0.004 0.992
#&gt; SRR547972     2  0.0963      0.869 0.000 0.964 0.000 0.036 0.000
#&gt; SRR547974     5  0.0000      0.956 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547976     2  0.2370      0.861 0.000 0.904 0.000 0.056 0.040
#&gt; SRR547978     5  0.3163      0.884 0.012 0.012 0.000 0.128 0.848
#&gt; SRR547979     2  0.1197      0.874 0.000 0.952 0.000 0.048 0.000
#&gt; SRR547981     5  0.0703      0.949 0.000 0.000 0.000 0.024 0.976
#&gt; SRR547982     2  0.0404      0.876 0.000 0.988 0.000 0.012 0.000
#&gt; SRR547983     2  0.3584      0.819 0.012 0.820 0.000 0.148 0.020
#&gt; SRR547989     2  0.3584      0.819 0.012 0.820 0.000 0.148 0.020
#&gt; SRR547990     5  0.0000      0.956 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547991     5  0.3878      0.852 0.012 0.036 0.000 0.144 0.808
#&gt; SRR547992     2  0.1043      0.875 0.000 0.960 0.000 0.040 0.000
#&gt; SRR801424     4  0.4171      0.491 0.396 0.000 0.000 0.604 0.000
#&gt; SRR801425     4  0.4390      0.216 0.004 0.000 0.428 0.568 0.000
#&gt; SRR801426     4  0.4173      0.485 0.012 0.000 0.300 0.688 0.000
#&gt; SRR801427     1  0.4210     -0.113 0.588 0.000 0.000 0.412 0.000
#&gt; SRR801428     4  0.4249      0.429 0.432 0.000 0.000 0.568 0.000
#&gt; SRR801429     4  0.4443      0.647 0.084 0.048 0.068 0.800 0.000
#&gt; SRR801430     4  0.4161      0.495 0.392 0.000 0.000 0.608 0.000
#&gt; SRR801431     4  0.3759      0.587 0.016 0.000 0.220 0.764 0.000
#&gt; SRR801432     4  0.4221      0.627 0.016 0.072 0.112 0.800 0.000
#&gt; SRR801433     4  0.4210      0.468 0.412 0.000 0.000 0.588 0.000
#&gt; SRR825135     3  0.1410      0.930 0.000 0.000 0.940 0.060 0.000
#&gt; SRR825136     1  0.0451      0.864 0.988 0.000 0.008 0.004 0.000
#&gt; SRR825137     3  0.0162      0.957 0.000 0.000 0.996 0.004 0.000
#&gt; SRR825139     1  0.1195      0.850 0.960 0.000 0.012 0.028 0.000
#&gt; SRR825140     1  0.0609      0.866 0.980 0.000 0.020 0.000 0.000
#&gt; SRR825141     3  0.0880      0.948 0.000 0.000 0.968 0.032 0.000
#&gt; SRR825143     1  0.0404      0.865 0.988 0.000 0.012 0.000 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-4-a').click(function(){
  $('#tab-SD-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-SD-NMF-get-classes-5'>
<p><a id='tab-SD-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR547975     5  0.0790      0.844 0.000 0.000 0.000 0.000 0.968 0.032
#&gt; SRR547973     2  0.0692      0.851 0.000 0.976 0.000 0.004 0.000 0.020
#&gt; SRR547968     2  0.0603      0.852 0.000 0.980 0.000 0.004 0.000 0.016
#&gt; SRR547980     5  0.3620      0.505 0.000 0.000 0.000 0.000 0.648 0.352
#&gt; SRR545058     3  0.0363      0.943 0.000 0.000 0.988 0.012 0.000 0.000
#&gt; SRR546225     2  0.3979      0.436 0.000 0.628 0.360 0.000 0.000 0.012
#&gt; SRR546226     1  0.0000      0.859 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000      0.859 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.0260      0.942 0.000 0.000 0.992 0.008 0.000 0.000
#&gt; SRR546229     3  0.3684      0.554 0.000 0.000 0.664 0.332 0.000 0.004
#&gt; SRR546230     1  0.0000      0.859 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.0000      0.939 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546232     1  0.0260      0.855 0.992 0.000 0.008 0.000 0.000 0.000
#&gt; SRR546233     1  0.0000      0.859 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546234     3  0.0717      0.925 0.000 0.016 0.976 0.000 0.000 0.008
#&gt; SRR546235     3  0.0632      0.943 0.000 0.000 0.976 0.024 0.000 0.000
#&gt; SRR546236     3  0.0000      0.939 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546237     1  0.2482      0.729 0.848 0.000 0.148 0.000 0.000 0.004
#&gt; SRR546238     3  0.1806      0.899 0.000 0.000 0.908 0.088 0.000 0.004
#&gt; SRR546239     1  0.3725      0.694 0.804 0.000 0.040 0.128 0.000 0.028
#&gt; SRR546240     1  0.3991      0.155 0.524 0.000 0.472 0.000 0.000 0.004
#&gt; SRR547969     2  0.4026      0.378 0.000 0.612 0.000 0.012 0.000 0.376
#&gt; SRR547970     5  0.0520      0.836 0.000 0.000 0.000 0.008 0.984 0.008
#&gt; SRR547971     5  0.3684      0.462 0.000 0.000 0.000 0.000 0.628 0.372
#&gt; SRR547972     2  0.1524      0.849 0.000 0.932 0.000 0.008 0.000 0.060
#&gt; SRR547974     5  0.0820      0.842 0.000 0.000 0.000 0.016 0.972 0.012
#&gt; SRR547976     2  0.0790      0.850 0.000 0.968 0.000 0.000 0.032 0.000
#&gt; SRR547978     6  0.2378      0.804 0.000 0.000 0.000 0.000 0.152 0.848
#&gt; SRR547979     2  0.0937      0.861 0.000 0.960 0.000 0.000 0.000 0.040
#&gt; SRR547981     5  0.0725      0.832 0.000 0.000 0.000 0.012 0.976 0.012
#&gt; SRR547982     2  0.1007      0.860 0.000 0.956 0.000 0.000 0.000 0.044
#&gt; SRR547983     6  0.2520      0.846 0.000 0.108 0.000 0.012 0.008 0.872
#&gt; SRR547989     6  0.2520      0.846 0.000 0.108 0.000 0.012 0.008 0.872
#&gt; SRR547990     5  0.0937      0.841 0.000 0.000 0.000 0.000 0.960 0.040
#&gt; SRR547991     6  0.2219      0.822 0.000 0.000 0.000 0.000 0.136 0.864
#&gt; SRR547992     2  0.0713      0.861 0.000 0.972 0.000 0.000 0.000 0.028
#&gt; SRR801424     4  0.3668      0.704 0.228 0.000 0.000 0.744 0.000 0.028
#&gt; SRR801425     4  0.3528      0.449 0.000 0.000 0.296 0.700 0.000 0.004
#&gt; SRR801426     4  0.2402      0.682 0.000 0.000 0.140 0.856 0.000 0.004
#&gt; SRR801427     1  0.3866     -0.270 0.516 0.000 0.000 0.484 0.000 0.000
#&gt; SRR801428     4  0.4009      0.651 0.288 0.000 0.000 0.684 0.000 0.028
#&gt; SRR801429     4  0.1396      0.741 0.012 0.008 0.024 0.952 0.000 0.004
#&gt; SRR801430     4  0.3863      0.681 0.260 0.000 0.000 0.712 0.000 0.028
#&gt; SRR801431     4  0.1152      0.738 0.000 0.000 0.044 0.952 0.000 0.004
#&gt; SRR801432     4  0.1003      0.735 0.000 0.020 0.016 0.964 0.000 0.000
#&gt; SRR801433     4  0.4009      0.651 0.288 0.000 0.000 0.684 0.000 0.028
#&gt; SRR825135     3  0.1141      0.930 0.000 0.000 0.948 0.052 0.000 0.000
#&gt; SRR825136     1  0.0260      0.856 0.992 0.000 0.000 0.000 0.000 0.008
#&gt; SRR825137     3  0.0547      0.943 0.000 0.000 0.980 0.020 0.000 0.000
#&gt; SRR825139     1  0.0692      0.845 0.976 0.000 0.000 0.020 0.000 0.004
#&gt; SRR825140     1  0.0000      0.859 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0790      0.940 0.000 0.000 0.968 0.032 0.000 0.000
#&gt; SRR825143     1  0.0000      0.859 1.000 0.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-SD-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-SD-NMF-get-classes-5-a').click(function(){
  $('#tab-SD-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-SD-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-SD-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-SD-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-SD-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-SD-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-SD-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-SD-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-SD-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-SD-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-signatures'>
<ul>
<li><a href='#tab-SD-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-1-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-1"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-2-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-2"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-3-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-3"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-4-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-4"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-5-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-SD-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-SD-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-SD-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk SD-NMF-signature_compare](figure_cola/SD-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-SD-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-SD-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-SD-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-SD-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-SD-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-SD-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-SD-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-SD-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk SD-NMF-collect-classes](figure_cola/SD-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:hclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "hclust"]
# you can also extract it by
# res = res_list["CV:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-hclust-collect-plots](figure_cola/CV-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-hclust-select-partition-number](figure_cola/CV-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.979       0.988         0.4764 0.521   0.521
#> 3 3 0.716           0.889       0.797         0.2883 0.803   0.621
#> 4 4 0.759           0.774       0.882         0.1785 0.963   0.886
#> 5 5 0.820           0.664       0.837         0.0666 0.934   0.778
#> 6 6 0.806           0.742       0.789         0.0417 0.922   0.683
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-classes'>
<ul>
<li><a href='#tab-CV-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-hclust-get-classes-1'>
<p><a id='tab-CV-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR547975     2   0.000      0.986 0.000 1.000
#&gt; SRR547973     2   0.000      0.986 0.000 1.000
#&gt; SRR547968     2   0.000      0.986 0.000 1.000
#&gt; SRR547980     2   0.000      0.986 0.000 1.000
#&gt; SRR545058     1   0.184      0.983 0.972 0.028
#&gt; SRR546225     2   0.821      0.646 0.256 0.744
#&gt; SRR546226     1   0.000      0.987 1.000 0.000
#&gt; SRR546227     1   0.000      0.987 1.000 0.000
#&gt; SRR546228     1   0.184      0.983 0.972 0.028
#&gt; SRR546229     1   0.163      0.985 0.976 0.024
#&gt; SRR546230     1   0.000      0.987 1.000 0.000
#&gt; SRR546231     1   0.000      0.987 1.000 0.000
#&gt; SRR546232     1   0.000      0.987 1.000 0.000
#&gt; SRR546233     1   0.000      0.987 1.000 0.000
#&gt; SRR546234     1   0.163      0.985 0.976 0.024
#&gt; SRR546235     1   0.184      0.983 0.972 0.028
#&gt; SRR546236     1   0.163      0.985 0.976 0.024
#&gt; SRR546237     1   0.000      0.987 1.000 0.000
#&gt; SRR546238     1   0.184      0.983 0.972 0.028
#&gt; SRR546239     1   0.000      0.987 1.000 0.000
#&gt; SRR546240     1   0.000      0.987 1.000 0.000
#&gt; SRR547969     2   0.000      0.986 0.000 1.000
#&gt; SRR547970     2   0.000      0.986 0.000 1.000
#&gt; SRR547971     2   0.000      0.986 0.000 1.000
#&gt; SRR547972     2   0.000      0.986 0.000 1.000
#&gt; SRR547974     2   0.000      0.986 0.000 1.000
#&gt; SRR547976     2   0.000      0.986 0.000 1.000
#&gt; SRR547978     2   0.000      0.986 0.000 1.000
#&gt; SRR547979     2   0.000      0.986 0.000 1.000
#&gt; SRR547981     2   0.000      0.986 0.000 1.000
#&gt; SRR547982     2   0.000      0.986 0.000 1.000
#&gt; SRR547983     2   0.000      0.986 0.000 1.000
#&gt; SRR547989     2   0.000      0.986 0.000 1.000
#&gt; SRR547990     2   0.000      0.986 0.000 1.000
#&gt; SRR547991     2   0.000      0.986 0.000 1.000
#&gt; SRR547992     2   0.000      0.986 0.000 1.000
#&gt; SRR801424     1   0.000      0.987 1.000 0.000
#&gt; SRR801425     1   0.184      0.983 0.972 0.028
#&gt; SRR801426     1   0.184      0.983 0.972 0.028
#&gt; SRR801427     1   0.000      0.987 1.000 0.000
#&gt; SRR801428     1   0.000      0.987 1.000 0.000
#&gt; SRR801429     1   0.184      0.983 0.972 0.028
#&gt; SRR801430     1   0.000      0.987 1.000 0.000
#&gt; SRR801431     1   0.184      0.983 0.972 0.028
#&gt; SRR801432     1   0.184      0.983 0.972 0.028
#&gt; SRR801433     1   0.000      0.987 1.000 0.000
#&gt; SRR825135     1   0.163      0.985 0.976 0.024
#&gt; SRR825136     1   0.000      0.987 1.000 0.000
#&gt; SRR825137     1   0.184      0.983 0.972 0.028
#&gt; SRR825139     1   0.000      0.987 1.000 0.000
#&gt; SRR825140     1   0.000      0.987 1.000 0.000
#&gt; SRR825141     1   0.163      0.985 0.976 0.024
#&gt; SRR825143     1   0.000      0.987 1.000 0.000
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-1-a').click(function(){
  $('#tab-CV-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-2'>
<p><a id='tab-CV-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     2  0.5621      0.848 0.308 0.692 0.000
#&gt; SRR547973     2  0.0000      0.882 0.000 1.000 0.000
#&gt; SRR547968     2  0.0000      0.882 0.000 1.000 0.000
#&gt; SRR547980     2  0.4002      0.872 0.160 0.840 0.000
#&gt; SRR545058     3  0.1163      0.921 0.028 0.000 0.972
#&gt; SRR546225     2  0.8101      0.586 0.132 0.640 0.228
#&gt; SRR546226     1  0.6291      0.946 0.532 0.000 0.468
#&gt; SRR546227     1  0.6215      0.950 0.572 0.000 0.428
#&gt; SRR546228     3  0.1163      0.921 0.028 0.000 0.972
#&gt; SRR546229     3  0.0237      0.942 0.004 0.000 0.996
#&gt; SRR546230     1  0.6291      0.946 0.532 0.000 0.468
#&gt; SRR546231     3  0.3192      0.779 0.112 0.000 0.888
#&gt; SRR546232     1  0.6215      0.950 0.572 0.000 0.428
#&gt; SRR546233     1  0.6291      0.946 0.532 0.000 0.468
#&gt; SRR546234     3  0.1289      0.918 0.032 0.000 0.968
#&gt; SRR546235     3  0.0000      0.943 0.000 0.000 1.000
#&gt; SRR546236     3  0.1289      0.918 0.032 0.000 0.968
#&gt; SRR546237     1  0.6215      0.950 0.572 0.000 0.428
#&gt; SRR546238     3  0.0000      0.943 0.000 0.000 1.000
#&gt; SRR546239     1  0.6180      0.947 0.584 0.000 0.416
#&gt; SRR546240     3  0.5363      0.156 0.276 0.000 0.724
#&gt; SRR547969     2  0.0000      0.882 0.000 1.000 0.000
#&gt; SRR547970     2  0.6180      0.801 0.416 0.584 0.000
#&gt; SRR547971     2  0.5431      0.855 0.284 0.716 0.000
#&gt; SRR547972     2  0.0000      0.882 0.000 1.000 0.000
#&gt; SRR547974     2  0.5431      0.855 0.284 0.716 0.000
#&gt; SRR547976     2  0.0237      0.882 0.004 0.996 0.000
#&gt; SRR547978     2  0.5431      0.855 0.284 0.716 0.000
#&gt; SRR547979     2  0.0000      0.882 0.000 1.000 0.000
#&gt; SRR547981     2  0.5810      0.838 0.336 0.664 0.000
#&gt; SRR547982     2  0.0000      0.882 0.000 1.000 0.000
#&gt; SRR547983     2  0.0000      0.882 0.000 1.000 0.000
#&gt; SRR547989     2  0.0000      0.882 0.000 1.000 0.000
#&gt; SRR547990     2  0.6180      0.801 0.416 0.584 0.000
#&gt; SRR547991     2  0.5431      0.855 0.284 0.716 0.000
#&gt; SRR547992     2  0.0000      0.882 0.000 1.000 0.000
#&gt; SRR801424     1  0.6180      0.947 0.584 0.000 0.416
#&gt; SRR801425     3  0.0000      0.943 0.000 0.000 1.000
#&gt; SRR801426     3  0.0000      0.943 0.000 0.000 1.000
#&gt; SRR801427     1  0.6291      0.946 0.532 0.000 0.468
#&gt; SRR801428     1  0.6180      0.947 0.584 0.000 0.416
#&gt; SRR801429     3  0.0000      0.943 0.000 0.000 1.000
#&gt; SRR801430     1  0.6180      0.947 0.584 0.000 0.416
#&gt; SRR801431     3  0.0000      0.943 0.000 0.000 1.000
#&gt; SRR801432     3  0.0000      0.943 0.000 0.000 1.000
#&gt; SRR801433     1  0.6180      0.947 0.584 0.000 0.416
#&gt; SRR825135     3  0.0237      0.942 0.004 0.000 0.996
#&gt; SRR825136     1  0.6291      0.946 0.532 0.000 0.468
#&gt; SRR825137     3  0.0000      0.943 0.000 0.000 1.000
#&gt; SRR825139     1  0.6252      0.951 0.556 0.000 0.444
#&gt; SRR825140     1  0.6291      0.946 0.532 0.000 0.468
#&gt; SRR825141     3  0.0237      0.942 0.004 0.000 0.996
#&gt; SRR825143     1  0.6291      0.946 0.532 0.000 0.468
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-2-a').click(function(){
  $('#tab-CV-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-3'>
<p><a id='tab-CV-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     2  0.4624      0.332 0.000 0.660 0.000 0.340
#&gt; SRR547973     2  0.0000      0.764 0.000 1.000 0.000 0.000
#&gt; SRR547968     2  0.0000      0.764 0.000 1.000 0.000 0.000
#&gt; SRR547980     2  0.3356      0.612 0.000 0.824 0.000 0.176
#&gt; SRR545058     3  0.4599      0.725 0.212 0.000 0.760 0.028
#&gt; SRR546225     2  0.7886     -0.112 0.212 0.504 0.016 0.268
#&gt; SRR546226     1  0.1118      0.904 0.964 0.000 0.036 0.000
#&gt; SRR546227     1  0.0927      0.898 0.976 0.000 0.008 0.016
#&gt; SRR546228     3  0.4599      0.725 0.212 0.000 0.760 0.028
#&gt; SRR546229     3  0.0817      0.914 0.024 0.000 0.976 0.000
#&gt; SRR546230     1  0.1118      0.904 0.964 0.000 0.036 0.000
#&gt; SRR546231     3  0.3166      0.847 0.116 0.000 0.868 0.016
#&gt; SRR546232     1  0.0927      0.898 0.976 0.000 0.008 0.016
#&gt; SRR546233     1  0.1118      0.904 0.964 0.000 0.036 0.000
#&gt; SRR546234     3  0.2521      0.886 0.064 0.000 0.912 0.024
#&gt; SRR546235     3  0.0592      0.915 0.016 0.000 0.984 0.000
#&gt; SRR546236     3  0.4538      0.725 0.216 0.000 0.760 0.024
#&gt; SRR546237     1  0.0927      0.898 0.976 0.000 0.008 0.016
#&gt; SRR546238     3  0.0707      0.914 0.020 0.000 0.980 0.000
#&gt; SRR546239     1  0.3870      0.856 0.788 0.000 0.004 0.208
#&gt; SRR546240     3  0.4857      0.668 0.284 0.000 0.700 0.016
#&gt; SRR547969     2  0.0000      0.764 0.000 1.000 0.000 0.000
#&gt; SRR547970     4  0.3942      0.866 0.000 0.236 0.000 0.764
#&gt; SRR547971     2  0.4643      0.326 0.000 0.656 0.000 0.344
#&gt; SRR547972     2  0.0000      0.764 0.000 1.000 0.000 0.000
#&gt; SRR547974     2  0.4522      0.383 0.000 0.680 0.000 0.320
#&gt; SRR547976     2  0.0188      0.762 0.000 0.996 0.000 0.004
#&gt; SRR547978     2  0.4643      0.326 0.000 0.656 0.000 0.344
#&gt; SRR547979     2  0.0000      0.764 0.000 1.000 0.000 0.000
#&gt; SRR547981     4  0.4790      0.662 0.000 0.380 0.000 0.620
#&gt; SRR547982     2  0.0000      0.764 0.000 1.000 0.000 0.000
#&gt; SRR547983     2  0.0000      0.764 0.000 1.000 0.000 0.000
#&gt; SRR547989     2  0.0000      0.764 0.000 1.000 0.000 0.000
#&gt; SRR547990     4  0.3942      0.866 0.000 0.236 0.000 0.764
#&gt; SRR547991     2  0.4643      0.326 0.000 0.656 0.000 0.344
#&gt; SRR547992     2  0.0000      0.764 0.000 1.000 0.000 0.000
#&gt; SRR801424     1  0.3870      0.856 0.788 0.000 0.004 0.208
#&gt; SRR801425     3  0.0592      0.915 0.016 0.000 0.984 0.000
#&gt; SRR801426     3  0.0592      0.915 0.016 0.000 0.984 0.000
#&gt; SRR801427     1  0.1118      0.904 0.964 0.000 0.036 0.000
#&gt; SRR801428     1  0.3870      0.856 0.788 0.000 0.004 0.208
#&gt; SRR801429     3  0.0592      0.915 0.016 0.000 0.984 0.000
#&gt; SRR801430     1  0.3870      0.856 0.788 0.000 0.004 0.208
#&gt; SRR801431     3  0.0592      0.915 0.016 0.000 0.984 0.000
#&gt; SRR801432     3  0.0592      0.915 0.016 0.000 0.984 0.000
#&gt; SRR801433     1  0.3870      0.856 0.788 0.000 0.004 0.208
#&gt; SRR825135     3  0.0921      0.913 0.028 0.000 0.972 0.000
#&gt; SRR825136     1  0.1118      0.904 0.964 0.000 0.036 0.000
#&gt; SRR825137     3  0.0592      0.915 0.016 0.000 0.984 0.000
#&gt; SRR825139     1  0.4348      0.856 0.780 0.000 0.024 0.196
#&gt; SRR825140     1  0.1118      0.904 0.964 0.000 0.036 0.000
#&gt; SRR825141     3  0.0707      0.914 0.020 0.000 0.980 0.000
#&gt; SRR825143     1  0.1118      0.904 0.964 0.000 0.036 0.000
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-3-a').click(function(){
  $('#tab-CV-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-4'>
<p><a id='tab-CV-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR547975     5  0.4307      0.448 0.000 0.496 0.000 0.000 0.504
#&gt; SRR547973     2  0.0000      0.887 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547968     2  0.0000      0.887 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547980     2  0.3707      0.252 0.000 0.716 0.000 0.000 0.284
#&gt; SRR545058     3  0.3863      0.512 0.000 0.000 0.740 0.248 0.012
#&gt; SRR546225     2  0.6206      0.102 0.000 0.504 0.000 0.344 0.152
#&gt; SRR546226     1  0.3730      0.864 0.712 0.000 0.000 0.288 0.000
#&gt; SRR546227     1  0.3266      0.856 0.796 0.000 0.004 0.200 0.000
#&gt; SRR546228     3  0.3863      0.512 0.000 0.000 0.740 0.248 0.012
#&gt; SRR546229     3  0.0451      0.731 0.000 0.000 0.988 0.004 0.008
#&gt; SRR546230     1  0.3730      0.864 0.712 0.000 0.000 0.288 0.000
#&gt; SRR546231     3  0.5691     -0.360 0.084 0.000 0.600 0.308 0.008
#&gt; SRR546232     1  0.3266      0.856 0.796 0.000 0.004 0.200 0.000
#&gt; SRR546233     1  0.3730      0.864 0.712 0.000 0.000 0.288 0.000
#&gt; SRR546234     3  0.1764      0.692 0.000 0.000 0.928 0.064 0.008
#&gt; SRR546235     3  0.3838      0.213 0.000 0.000 0.716 0.280 0.004
#&gt; SRR546236     3  0.3756      0.516 0.000 0.000 0.744 0.248 0.008
#&gt; SRR546237     1  0.3266      0.856 0.796 0.000 0.004 0.200 0.000
#&gt; SRR546238     3  0.0324      0.732 0.000 0.000 0.992 0.004 0.004
#&gt; SRR546239     1  0.0162      0.807 0.996 0.000 0.000 0.004 0.000
#&gt; SRR546240     4  0.5731      0.000 0.084 0.000 0.436 0.480 0.000
#&gt; SRR547969     2  0.0000      0.887 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547970     5  0.3550      0.449 0.000 0.020 0.000 0.184 0.796
#&gt; SRR547971     5  0.4249      0.590 0.000 0.432 0.000 0.000 0.568
#&gt; SRR547972     2  0.0000      0.887 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547974     5  0.4294      0.525 0.000 0.468 0.000 0.000 0.532
#&gt; SRR547976     2  0.0963      0.848 0.000 0.964 0.000 0.000 0.036
#&gt; SRR547978     5  0.4256      0.587 0.000 0.436 0.000 0.000 0.564
#&gt; SRR547979     2  0.0000      0.887 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547981     5  0.2377      0.576 0.000 0.128 0.000 0.000 0.872
#&gt; SRR547982     2  0.0000      0.887 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547983     2  0.0404      0.879 0.000 0.988 0.000 0.000 0.012
#&gt; SRR547989     2  0.0404      0.879 0.000 0.988 0.000 0.000 0.012
#&gt; SRR547990     5  0.3621      0.448 0.000 0.020 0.000 0.192 0.788
#&gt; SRR547991     5  0.4256      0.587 0.000 0.436 0.000 0.000 0.564
#&gt; SRR547992     2  0.0000      0.887 0.000 1.000 0.000 0.000 0.000
#&gt; SRR801424     1  0.0162      0.807 0.996 0.000 0.000 0.004 0.000
#&gt; SRR801425     3  0.0162      0.731 0.000 0.000 0.996 0.000 0.004
#&gt; SRR801426     3  0.0162      0.734 0.000 0.000 0.996 0.000 0.004
#&gt; SRR801427     1  0.3730      0.864 0.712 0.000 0.000 0.288 0.000
#&gt; SRR801428     1  0.0162      0.807 0.996 0.000 0.000 0.004 0.000
#&gt; SRR801429     3  0.0162      0.734 0.000 0.000 0.996 0.000 0.004
#&gt; SRR801430     1  0.0162      0.807 0.996 0.000 0.000 0.004 0.000
#&gt; SRR801431     3  0.0162      0.734 0.000 0.000 0.996 0.000 0.004
#&gt; SRR801432     3  0.0162      0.734 0.000 0.000 0.996 0.000 0.004
#&gt; SRR801433     1  0.0162      0.807 0.996 0.000 0.000 0.004 0.000
#&gt; SRR825135     3  0.0451      0.731 0.000 0.000 0.988 0.008 0.004
#&gt; SRR825136     1  0.3730      0.864 0.712 0.000 0.000 0.288 0.000
#&gt; SRR825137     3  0.3838      0.213 0.000 0.000 0.716 0.280 0.004
#&gt; SRR825139     1  0.1478      0.813 0.936 0.000 0.000 0.064 0.000
#&gt; SRR825140     1  0.3730      0.864 0.712 0.000 0.000 0.288 0.000
#&gt; SRR825141     3  0.3957      0.209 0.000 0.000 0.712 0.280 0.008
#&gt; SRR825143     1  0.3730      0.864 0.712 0.000 0.000 0.288 0.000
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-4-a').click(function(){
  $('#tab-CV-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-hclust-get-classes-5'>
<p><a id='tab-CV-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR547975     5  0.3890    0.47635 0.000 0.400 0.000 0.004 0.596 0.000
#&gt; SRR547973     2  0.0000    0.87535 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547968     2  0.0000    0.87535 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547980     2  0.3695    0.10512 0.000 0.624 0.000 0.000 0.376 0.000
#&gt; SRR545058     3  0.4031    0.64319 0.004 0.000 0.736 0.048 0.000 0.212
#&gt; SRR546225     2  0.6770    0.15604 0.004 0.492 0.000 0.160 0.076 0.268
#&gt; SRR546226     1  0.0000    0.89626 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.2046    0.81875 0.908 0.000 0.000 0.032 0.000 0.060
#&gt; SRR546228     3  0.4031    0.64319 0.004 0.000 0.736 0.048 0.000 0.212
#&gt; SRR546229     3  0.0935    0.81993 0.004 0.000 0.964 0.000 0.000 0.032
#&gt; SRR546230     1  0.0000    0.89626 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     6  0.3932    0.73760 0.004 0.000 0.248 0.028 0.000 0.720
#&gt; SRR546232     1  0.2046    0.81875 0.908 0.000 0.000 0.032 0.000 0.060
#&gt; SRR546233     1  0.0000    0.89626 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546234     3  0.3242    0.71910 0.004 0.000 0.816 0.032 0.000 0.148
#&gt; SRR546235     6  0.3747    0.77495 0.000 0.000 0.396 0.000 0.000 0.604
#&gt; SRR546236     3  0.4632    0.56652 0.004 0.000 0.620 0.048 0.000 0.328
#&gt; SRR546237     1  0.2046    0.81875 0.908 0.000 0.000 0.032 0.000 0.060
#&gt; SRR546238     3  0.0858    0.82030 0.004 0.000 0.968 0.000 0.000 0.028
#&gt; SRR546239     4  0.3866    1.00000 0.484 0.000 0.000 0.516 0.000 0.000
#&gt; SRR546240     6  0.6123    0.60678 0.200 0.000 0.236 0.028 0.000 0.536
#&gt; SRR547969     2  0.0000    0.87535 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547970     5  0.4129    0.33169 0.000 0.000 0.000 0.424 0.564 0.012
#&gt; SRR547971     5  0.3515    0.60888 0.000 0.324 0.000 0.000 0.676 0.000
#&gt; SRR547972     2  0.0000    0.87535 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547974     5  0.3684    0.54169 0.000 0.372 0.000 0.000 0.628 0.000
#&gt; SRR547976     2  0.1007    0.84085 0.000 0.956 0.000 0.000 0.044 0.000
#&gt; SRR547978     5  0.3531    0.60713 0.000 0.328 0.000 0.000 0.672 0.000
#&gt; SRR547979     2  0.0000    0.87535 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547981     5  0.0935    0.55979 0.000 0.032 0.000 0.004 0.964 0.000
#&gt; SRR547982     2  0.0000    0.87535 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547983     2  0.1141    0.84055 0.000 0.948 0.000 0.000 0.052 0.000
#&gt; SRR547989     2  0.1141    0.84055 0.000 0.948 0.000 0.000 0.052 0.000
#&gt; SRR547990     5  0.4780    0.32871 0.000 0.000 0.000 0.392 0.552 0.056
#&gt; SRR547991     5  0.3531    0.60713 0.000 0.328 0.000 0.000 0.672 0.000
#&gt; SRR547992     2  0.0000    0.87535 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR801424     4  0.3866    1.00000 0.484 0.000 0.000 0.516 0.000 0.000
#&gt; SRR801425     3  0.0713    0.81722 0.000 0.000 0.972 0.000 0.000 0.028
#&gt; SRR801426     3  0.0146    0.82794 0.000 0.000 0.996 0.000 0.000 0.004
#&gt; SRR801427     1  0.0000    0.89626 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR801428     4  0.3866    1.00000 0.484 0.000 0.000 0.516 0.000 0.000
#&gt; SRR801429     3  0.0146    0.82794 0.000 0.000 0.996 0.000 0.000 0.004
#&gt; SRR801430     4  0.3866    1.00000 0.484 0.000 0.000 0.516 0.000 0.000
#&gt; SRR801431     3  0.0146    0.82794 0.000 0.000 0.996 0.000 0.000 0.004
#&gt; SRR801432     3  0.0146    0.82794 0.000 0.000 0.996 0.000 0.000 0.004
#&gt; SRR801433     4  0.3866    1.00000 0.484 0.000 0.000 0.516 0.000 0.000
#&gt; SRR825135     3  0.2146    0.73771 0.004 0.000 0.880 0.000 0.000 0.116
#&gt; SRR825136     1  0.0000    0.89626 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR825137     6  0.3747    0.77495 0.000 0.000 0.396 0.000 0.000 0.604
#&gt; SRR825139     1  0.3151    0.00555 0.748 0.000 0.000 0.252 0.000 0.000
#&gt; SRR825140     1  0.0000    0.89626 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     6  0.3838    0.67087 0.000 0.000 0.448 0.000 0.000 0.552
#&gt; SRR825143     1  0.0000    0.89626 1.000 0.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-hclust-get-classes-5-a').click(function(){
  $('#tab-CV-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-CV-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-signatures'>
<ul>
<li><a href='#tab-CV-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-1-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-1"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-2-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-2"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-3-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-3"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-4-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-4"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-5-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-hclust-signature_compare](figure_cola/CV-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-CV-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-hclust-collect-classes](figure_cola/CV-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:kmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "kmeans"]
# you can also extract it by
# res = res_list["CV:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-kmeans-collect-plots](figure_cola/CV-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-kmeans-select-partition-number](figure_cola/CV-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.4795 0.521   0.521
#> 3 3 0.704           0.925       0.841         0.3219 0.803   0.621
#> 4 4 0.569           0.847       0.820         0.1245 1.000   1.000
#> 5 5 0.709           0.565       0.682         0.0746 0.908   0.715
#> 6 6 0.713           0.383       0.703         0.0542 0.896   0.618
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-classes'>
<ul>
<li><a href='#tab-CV-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-kmeans-get-classes-1'>
<p><a id='tab-CV-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1 p2
#&gt; SRR547975     2       0          1  0  1
#&gt; SRR547973     2       0          1  0  1
#&gt; SRR547968     2       0          1  0  1
#&gt; SRR547980     2       0          1  0  1
#&gt; SRR545058     1       0          1  1  0
#&gt; SRR546225     2       0          1  0  1
#&gt; SRR546226     1       0          1  1  0
#&gt; SRR546227     1       0          1  1  0
#&gt; SRR546228     1       0          1  1  0
#&gt; SRR546229     1       0          1  1  0
#&gt; SRR546230     1       0          1  1  0
#&gt; SRR546231     1       0          1  1  0
#&gt; SRR546232     1       0          1  1  0
#&gt; SRR546233     1       0          1  1  0
#&gt; SRR546234     1       0          1  1  0
#&gt; SRR546235     1       0          1  1  0
#&gt; SRR546236     1       0          1  1  0
#&gt; SRR546237     1       0          1  1  0
#&gt; SRR546238     1       0          1  1  0
#&gt; SRR546239     1       0          1  1  0
#&gt; SRR546240     1       0          1  1  0
#&gt; SRR547969     2       0          1  0  1
#&gt; SRR547970     2       0          1  0  1
#&gt; SRR547971     2       0          1  0  1
#&gt; SRR547972     2       0          1  0  1
#&gt; SRR547974     2       0          1  0  1
#&gt; SRR547976     2       0          1  0  1
#&gt; SRR547978     2       0          1  0  1
#&gt; SRR547979     2       0          1  0  1
#&gt; SRR547981     2       0          1  0  1
#&gt; SRR547982     2       0          1  0  1
#&gt; SRR547983     2       0          1  0  1
#&gt; SRR547989     2       0          1  0  1
#&gt; SRR547990     2       0          1  0  1
#&gt; SRR547991     2       0          1  0  1
#&gt; SRR547992     2       0          1  0  1
#&gt; SRR801424     1       0          1  1  0
#&gt; SRR801425     1       0          1  1  0
#&gt; SRR801426     1       0          1  1  0
#&gt; SRR801427     1       0          1  1  0
#&gt; SRR801428     1       0          1  1  0
#&gt; SRR801429     1       0          1  1  0
#&gt; SRR801430     1       0          1  1  0
#&gt; SRR801431     1       0          1  1  0
#&gt; SRR801432     1       0          1  1  0
#&gt; SRR801433     1       0          1  1  0
#&gt; SRR825135     1       0          1  1  0
#&gt; SRR825136     1       0          1  1  0
#&gt; SRR825137     1       0          1  1  0
#&gt; SRR825139     1       0          1  1  0
#&gt; SRR825140     1       0          1  1  0
#&gt; SRR825141     1       0          1  1  0
#&gt; SRR825143     1       0          1  1  0
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-1-a').click(function(){
  $('#tab-CV-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-2'>
<p><a id='tab-CV-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     2  0.3412      0.915 0.124 0.876 0.000
#&gt; SRR547973     2  0.0000      0.925 0.000 1.000 0.000
#&gt; SRR547968     2  0.0237      0.925 0.004 0.996 0.000
#&gt; SRR547980     2  0.2356      0.921 0.072 0.928 0.000
#&gt; SRR545058     3  0.0000      0.955 0.000 0.000 1.000
#&gt; SRR546225     2  0.5327      0.868 0.272 0.728 0.000
#&gt; SRR546226     1  0.6140      0.939 0.596 0.000 0.404
#&gt; SRR546227     1  0.5948      0.924 0.640 0.000 0.360
#&gt; SRR546228     3  0.0000      0.955 0.000 0.000 1.000
#&gt; SRR546229     3  0.0747      0.952 0.016 0.000 0.984
#&gt; SRR546230     1  0.6140      0.939 0.596 0.000 0.404
#&gt; SRR546231     3  0.1643      0.929 0.044 0.000 0.956
#&gt; SRR546232     1  0.5948      0.924 0.640 0.000 0.360
#&gt; SRR546233     1  0.6140      0.939 0.596 0.000 0.404
#&gt; SRR546234     3  0.0000      0.955 0.000 0.000 1.000
#&gt; SRR546235     3  0.1411      0.939 0.036 0.000 0.964
#&gt; SRR546236     3  0.0892      0.949 0.020 0.000 0.980
#&gt; SRR546237     1  0.5948      0.924 0.640 0.000 0.360
#&gt; SRR546238     3  0.0000      0.955 0.000 0.000 1.000
#&gt; SRR546239     1  0.5733      0.919 0.676 0.000 0.324
#&gt; SRR546240     1  0.5948      0.924 0.640 0.000 0.360
#&gt; SRR547969     2  0.0424      0.925 0.008 0.992 0.000
#&gt; SRR547970     2  0.5397      0.865 0.280 0.720 0.000
#&gt; SRR547971     2  0.5397      0.867 0.280 0.720 0.000
#&gt; SRR547972     2  0.0237      0.925 0.004 0.996 0.000
#&gt; SRR547974     2  0.3412      0.915 0.124 0.876 0.000
#&gt; SRR547976     2  0.0237      0.925 0.004 0.996 0.000
#&gt; SRR547978     2  0.4002      0.907 0.160 0.840 0.000
#&gt; SRR547979     2  0.0000      0.925 0.000 1.000 0.000
#&gt; SRR547981     2  0.5397      0.865 0.280 0.720 0.000
#&gt; SRR547982     2  0.0237      0.925 0.004 0.996 0.000
#&gt; SRR547983     2  0.0424      0.925 0.008 0.992 0.000
#&gt; SRR547989     2  0.0424      0.925 0.008 0.992 0.000
#&gt; SRR547990     2  0.5431      0.864 0.284 0.716 0.000
#&gt; SRR547991     2  0.4002      0.907 0.160 0.840 0.000
#&gt; SRR547992     2  0.0237      0.925 0.004 0.996 0.000
#&gt; SRR801424     1  0.5785      0.921 0.668 0.000 0.332
#&gt; SRR801425     3  0.1411      0.942 0.036 0.000 0.964
#&gt; SRR801426     3  0.1643      0.938 0.044 0.000 0.956
#&gt; SRR801427     1  0.5905      0.925 0.648 0.000 0.352
#&gt; SRR801428     1  0.5785      0.921 0.668 0.000 0.332
#&gt; SRR801429     3  0.1860      0.931 0.052 0.000 0.948
#&gt; SRR801430     1  0.5785      0.921 0.668 0.000 0.332
#&gt; SRR801431     3  0.1860      0.931 0.052 0.000 0.948
#&gt; SRR801432     3  0.1860      0.931 0.052 0.000 0.948
#&gt; SRR801433     1  0.5785      0.921 0.668 0.000 0.332
#&gt; SRR825135     3  0.0000      0.955 0.000 0.000 1.000
#&gt; SRR825136     1  0.5988      0.939 0.632 0.000 0.368
#&gt; SRR825137     3  0.1411      0.939 0.036 0.000 0.964
#&gt; SRR825139     1  0.5988      0.939 0.632 0.000 0.368
#&gt; SRR825140     1  0.6140      0.939 0.596 0.000 0.404
#&gt; SRR825141     3  0.1411      0.939 0.036 0.000 0.964
#&gt; SRR825143     1  0.6140      0.939 0.596 0.000 0.404
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-2-a').click(function(){
  $('#tab-CV-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-3'>
<p><a id='tab-CV-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3 p4
#&gt; SRR547975     2  0.4630      0.841 0.036 0.768 0.000 NA
#&gt; SRR547973     2  0.1042      0.861 0.008 0.972 0.000 NA
#&gt; SRR547968     2  0.0188      0.858 0.004 0.996 0.000 NA
#&gt; SRR547980     2  0.3793      0.854 0.044 0.844 0.000 NA
#&gt; SRR545058     3  0.0927      0.899 0.008 0.000 0.976 NA
#&gt; SRR546225     2  0.6446      0.714 0.020 0.508 0.032 NA
#&gt; SRR546226     1  0.3074      0.882 0.848 0.000 0.152 NA
#&gt; SRR546227     1  0.4234      0.868 0.816 0.000 0.132 NA
#&gt; SRR546228     3  0.0804      0.899 0.008 0.000 0.980 NA
#&gt; SRR546229     3  0.2918      0.883 0.008 0.000 0.876 NA
#&gt; SRR546230     1  0.3074      0.882 0.848 0.000 0.152 NA
#&gt; SRR546231     3  0.4100      0.797 0.036 0.000 0.816 NA
#&gt; SRR546232     1  0.3931      0.868 0.832 0.000 0.128 NA
#&gt; SRR546233     1  0.3074      0.882 0.848 0.000 0.152 NA
#&gt; SRR546234     3  0.1059      0.899 0.016 0.000 0.972 NA
#&gt; SRR546235     3  0.2214      0.885 0.028 0.000 0.928 NA
#&gt; SRR546236     3  0.0927      0.898 0.008 0.000 0.976 NA
#&gt; SRR546237     1  0.4740      0.866 0.788 0.000 0.132 NA
#&gt; SRR546238     3  0.0927      0.899 0.016 0.000 0.976 NA
#&gt; SRR546239     1  0.6442      0.818 0.632 0.000 0.124 NA
#&gt; SRR546240     1  0.5674      0.838 0.720 0.000 0.132 NA
#&gt; SRR547969     2  0.0524      0.858 0.004 0.988 0.000 NA
#&gt; SRR547970     2  0.5290      0.734 0.008 0.516 0.000 NA
#&gt; SRR547971     2  0.5987      0.743 0.040 0.520 0.000 NA
#&gt; SRR547972     2  0.0188      0.858 0.004 0.996 0.000 NA
#&gt; SRR547974     2  0.4630      0.841 0.036 0.768 0.000 NA
#&gt; SRR547976     2  0.1913      0.860 0.020 0.940 0.000 NA
#&gt; SRR547978     2  0.5073      0.834 0.056 0.744 0.000 NA
#&gt; SRR547979     2  0.0336      0.859 0.008 0.992 0.000 NA
#&gt; SRR547981     2  0.5597      0.737 0.020 0.516 0.000 NA
#&gt; SRR547982     2  0.0188      0.858 0.004 0.996 0.000 NA
#&gt; SRR547983     2  0.1722      0.857 0.048 0.944 0.000 NA
#&gt; SRR547989     2  0.1722      0.857 0.048 0.944 0.000 NA
#&gt; SRR547990     2  0.5167      0.732 0.004 0.508 0.000 NA
#&gt; SRR547991     2  0.5073      0.834 0.056 0.744 0.000 NA
#&gt; SRR547992     2  0.0188      0.858 0.004 0.996 0.000 NA
#&gt; SRR801424     1  0.6660      0.799 0.592 0.000 0.120 NA
#&gt; SRR801425     3  0.3498      0.872 0.008 0.000 0.832 NA
#&gt; SRR801426     3  0.4086      0.846 0.008 0.000 0.776 NA
#&gt; SRR801427     1  0.4181      0.875 0.820 0.000 0.128 NA
#&gt; SRR801428     1  0.6660      0.799 0.592 0.000 0.120 NA
#&gt; SRR801429     3  0.4086      0.846 0.008 0.000 0.776 NA
#&gt; SRR801430     1  0.6660      0.799 0.592 0.000 0.120 NA
#&gt; SRR801431     3  0.4086      0.846 0.008 0.000 0.776 NA
#&gt; SRR801432     3  0.4086      0.846 0.008 0.000 0.776 NA
#&gt; SRR801433     1  0.6660      0.799 0.592 0.000 0.120 NA
#&gt; SRR825135     3  0.0779      0.899 0.016 0.000 0.980 NA
#&gt; SRR825136     1  0.2973      0.882 0.856 0.000 0.144 NA
#&gt; SRR825137     3  0.2214      0.885 0.028 0.000 0.928 NA
#&gt; SRR825139     1  0.5476      0.859 0.736 0.000 0.144 NA
#&gt; SRR825140     1  0.3074      0.882 0.848 0.000 0.152 NA
#&gt; SRR825141     3  0.2124      0.886 0.028 0.000 0.932 NA
#&gt; SRR825143     1  0.3074      0.882 0.848 0.000 0.152 NA
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-3-a').click(function(){
  $('#tab-CV-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-4'>
<p><a id='tab-CV-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR547975     2  0.5213      0.205 0.056 0.628 0.000 0.004 0.312
#&gt; SRR547973     2  0.1630      0.741 0.016 0.944 0.000 0.004 0.036
#&gt; SRR547968     2  0.0162      0.755 0.004 0.996 0.000 0.000 0.000
#&gt; SRR547980     2  0.4522      0.534 0.060 0.744 0.000 0.004 0.192
#&gt; SRR545058     3  0.2313      0.811 0.040 0.000 0.912 0.004 0.044
#&gt; SRR546225     5  0.7556      0.648 0.080 0.316 0.080 0.028 0.496
#&gt; SRR546226     4  0.6880      0.128 0.380 0.000 0.072 0.472 0.076
#&gt; SRR546227     1  0.5330      0.808 0.548 0.000 0.056 0.396 0.000
#&gt; SRR546228     3  0.2237      0.811 0.040 0.000 0.916 0.004 0.040
#&gt; SRR546229     3  0.4335      0.782 0.064 0.000 0.776 0.008 0.152
#&gt; SRR546230     4  0.6880      0.128 0.380 0.000 0.072 0.472 0.076
#&gt; SRR546231     3  0.6283      0.581 0.232 0.000 0.624 0.080 0.064
#&gt; SRR546232     1  0.5263      0.749 0.576 0.000 0.056 0.368 0.000
#&gt; SRR546233     4  0.6880      0.128 0.380 0.000 0.072 0.472 0.076
#&gt; SRR546234     3  0.2237      0.810 0.040 0.000 0.916 0.004 0.040
#&gt; SRR546235     3  0.3080      0.790 0.060 0.000 0.872 0.008 0.060
#&gt; SRR546236     3  0.2390      0.810 0.044 0.000 0.908 0.004 0.044
#&gt; SRR546237     1  0.5611      0.806 0.528 0.000 0.056 0.408 0.008
#&gt; SRR546238     3  0.1653      0.812 0.024 0.000 0.944 0.004 0.028
#&gt; SRR546239     4  0.4960     -0.156 0.264 0.000 0.048 0.680 0.008
#&gt; SRR546240     1  0.6220      0.628 0.512 0.000 0.052 0.392 0.044
#&gt; SRR547969     2  0.0955      0.747 0.028 0.968 0.000 0.000 0.004
#&gt; SRR547970     5  0.5477      0.838 0.024 0.360 0.000 0.032 0.584
#&gt; SRR547971     5  0.5652      0.771 0.088 0.360 0.000 0.000 0.552
#&gt; SRR547972     2  0.0000      0.756 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547974     2  0.5213      0.205 0.056 0.628 0.000 0.004 0.312
#&gt; SRR547976     2  0.2393      0.708 0.016 0.900 0.000 0.004 0.080
#&gt; SRR547978     2  0.5918      0.125 0.168 0.592 0.000 0.000 0.240
#&gt; SRR547979     2  0.0854      0.753 0.012 0.976 0.000 0.004 0.008
#&gt; SRR547981     5  0.4362      0.823 0.004 0.360 0.000 0.004 0.632
#&gt; SRR547982     2  0.0000      0.756 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547983     2  0.2497      0.710 0.112 0.880 0.000 0.004 0.004
#&gt; SRR547989     2  0.2497      0.710 0.112 0.880 0.000 0.004 0.004
#&gt; SRR547990     5  0.5792      0.836 0.052 0.356 0.000 0.024 0.568
#&gt; SRR547991     2  0.5918      0.125 0.168 0.592 0.000 0.000 0.240
#&gt; SRR547992     2  0.0000      0.756 0.000 1.000 0.000 0.000 0.000
#&gt; SRR801424     4  0.1270      0.326 0.000 0.000 0.052 0.948 0.000
#&gt; SRR801425     3  0.4812      0.771 0.076 0.000 0.740 0.012 0.172
#&gt; SRR801426     3  0.6554      0.723 0.080 0.000 0.624 0.116 0.180
#&gt; SRR801427     4  0.6546      0.149 0.324 0.000 0.056 0.544 0.076
#&gt; SRR801428     4  0.1270      0.326 0.000 0.000 0.052 0.948 0.000
#&gt; SRR801429     3  0.6788      0.708 0.080 0.000 0.600 0.140 0.180
#&gt; SRR801430     4  0.1270      0.326 0.000 0.000 0.052 0.948 0.000
#&gt; SRR801431     3  0.6788      0.708 0.080 0.000 0.600 0.140 0.180
#&gt; SRR801432     3  0.6788      0.708 0.080 0.000 0.600 0.140 0.180
#&gt; SRR801433     4  0.1270      0.326 0.000 0.000 0.052 0.948 0.000
#&gt; SRR825135     3  0.1653      0.812 0.024 0.000 0.944 0.004 0.028
#&gt; SRR825136     4  0.6784      0.128 0.380 0.000 0.064 0.480 0.076
#&gt; SRR825137     3  0.3145      0.788 0.060 0.000 0.868 0.008 0.064
#&gt; SRR825139     4  0.5817      0.206 0.204 0.000 0.064 0.672 0.060
#&gt; SRR825140     4  0.6838      0.114 0.384 0.000 0.068 0.472 0.076
#&gt; SRR825141     3  0.3078      0.789 0.056 0.000 0.872 0.008 0.064
#&gt; SRR825143     4  0.6880      0.128 0.380 0.000 0.072 0.472 0.076
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-4-a').click(function(){
  $('#tab-CV-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-kmeans-get-classes-5'>
<p><a id='tab-CV-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR547975     5  0.5001    0.15501 0.000 0.460 0.004 0.020 0.492 0.024
#&gt; SRR547973     2  0.1917    0.72375 0.000 0.928 0.004 0.016 0.036 0.016
#&gt; SRR547968     2  0.0291    0.74663 0.000 0.992 0.000 0.004 0.000 0.004
#&gt; SRR547980     2  0.5162    0.06601 0.000 0.560 0.004 0.028 0.376 0.032
#&gt; SRR545058     3  0.1621    0.61773 0.020 0.000 0.944 0.012 0.008 0.016
#&gt; SRR546225     5  0.8663    0.39425 0.008 0.160 0.264 0.104 0.332 0.132
#&gt; SRR546226     1  0.0363    0.47433 0.988 0.000 0.012 0.000 0.000 0.000
#&gt; SRR546227     1  0.5129   -0.02363 0.656 0.000 0.012 0.004 0.100 0.228
#&gt; SRR546228     3  0.1312    0.62311 0.020 0.000 0.956 0.004 0.008 0.012
#&gt; SRR546229     3  0.5239   -0.60192 0.012 0.000 0.504 0.436 0.028 0.020
#&gt; SRR546230     1  0.0363    0.47433 0.988 0.000 0.012 0.000 0.000 0.000
#&gt; SRR546231     3  0.7414    0.19604 0.024 0.000 0.388 0.112 0.124 0.352
#&gt; SRR546232     1  0.5056    0.00485 0.668 0.000 0.012 0.004 0.100 0.216
#&gt; SRR546233     1  0.0363    0.47433 0.988 0.000 0.012 0.000 0.000 0.000
#&gt; SRR546234     3  0.2182    0.60128 0.020 0.000 0.916 0.028 0.004 0.032
#&gt; SRR546235     3  0.5113    0.55655 0.012 0.000 0.724 0.112 0.052 0.100
#&gt; SRR546236     3  0.1452    0.62831 0.020 0.000 0.948 0.020 0.000 0.012
#&gt; SRR546237     1  0.5302   -0.10953 0.624 0.000 0.012 0.004 0.100 0.260
#&gt; SRR546238     3  0.1976    0.61702 0.020 0.000 0.928 0.020 0.024 0.008
#&gt; SRR546239     6  0.5430    0.00000 0.376 0.000 0.008 0.024 0.048 0.544
#&gt; SRR546240     1  0.6369   -0.32305 0.488 0.000 0.012 0.028 0.136 0.336
#&gt; SRR547969     2  0.0458    0.74323 0.000 0.984 0.000 0.016 0.000 0.000
#&gt; SRR547970     5  0.6022    0.63391 0.000 0.180 0.004 0.080 0.620 0.116
#&gt; SRR547971     5  0.4554    0.58808 0.000 0.184 0.000 0.036 0.728 0.052
#&gt; SRR547972     2  0.0146    0.74642 0.000 0.996 0.000 0.004 0.000 0.000
#&gt; SRR547974     5  0.5069    0.15610 0.000 0.456 0.004 0.024 0.492 0.024
#&gt; SRR547976     2  0.3376    0.62967 0.000 0.828 0.004 0.020 0.124 0.024
#&gt; SRR547978     2  0.6734   -0.16213 0.000 0.412 0.000 0.136 0.372 0.080
#&gt; SRR547979     2  0.1231    0.73823 0.000 0.960 0.004 0.012 0.012 0.012
#&gt; SRR547981     5  0.4745    0.63373 0.000 0.184 0.000 0.048 0.716 0.052
#&gt; SRR547982     2  0.0146    0.74684 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR547983     2  0.3791    0.65548 0.000 0.816 0.004 0.096 0.040 0.044
#&gt; SRR547989     2  0.3791    0.65548 0.000 0.816 0.004 0.096 0.040 0.044
#&gt; SRR547990     5  0.6219    0.63013 0.000 0.180 0.004 0.088 0.600 0.128
#&gt; SRR547991     2  0.6734   -0.16213 0.000 0.412 0.000 0.136 0.372 0.080
#&gt; SRR547992     2  0.0291    0.74663 0.000 0.992 0.000 0.004 0.000 0.004
#&gt; SRR801424     1  0.5604   -0.23159 0.452 0.000 0.000 0.144 0.000 0.404
#&gt; SRR801425     3  0.5065   -0.66505 0.004 0.000 0.492 0.456 0.028 0.020
#&gt; SRR801426     4  0.3993    0.97966 0.008 0.000 0.400 0.592 0.000 0.000
#&gt; SRR801427     1  0.1889    0.41692 0.920 0.000 0.004 0.056 0.000 0.020
#&gt; SRR801428     1  0.5604   -0.23159 0.452 0.000 0.000 0.144 0.000 0.404
#&gt; SRR801429     4  0.4066    0.99329 0.012 0.000 0.392 0.596 0.000 0.000
#&gt; SRR801430     1  0.5604   -0.23159 0.452 0.000 0.000 0.144 0.000 0.404
#&gt; SRR801431     4  0.4066    0.99329 0.012 0.000 0.392 0.596 0.000 0.000
#&gt; SRR801432     4  0.4066    0.99329 0.012 0.000 0.392 0.596 0.000 0.000
#&gt; SRR801433     1  0.5604   -0.23159 0.452 0.000 0.000 0.144 0.000 0.404
#&gt; SRR825135     3  0.2333    0.61665 0.020 0.000 0.912 0.028 0.024 0.016
#&gt; SRR825136     1  0.0146    0.46605 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; SRR825137     3  0.5113    0.55655 0.012 0.000 0.724 0.112 0.052 0.100
#&gt; SRR825139     1  0.3101    0.10695 0.756 0.000 0.000 0.000 0.000 0.244
#&gt; SRR825140     1  0.0363    0.47433 0.988 0.000 0.012 0.000 0.000 0.000
#&gt; SRR825141     3  0.5212    0.55075 0.012 0.000 0.716 0.116 0.056 0.100
#&gt; SRR825143     1  0.0363    0.47433 0.988 0.000 0.012 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-kmeans-get-classes-5-a').click(function(){
  $('#tab-CV-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-CV-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-signatures'>
<ul>
<li><a href='#tab-CV-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-kmeans-signature_compare](figure_cola/CV-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-CV-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-kmeans-collect-classes](figure_cola/CV-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:skmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "skmeans"]
# you can also extract it by
# res = res_list["CV:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-skmeans-collect-plots](figure_cola/CV-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-skmeans-select-partition-number](figure_cola/CV-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.4795 0.521   0.521
#> 3 3 1.000           1.000       1.000         0.4113 0.803   0.621
#> 4 4 0.896           0.840       0.923         0.0860 0.907   0.725
#> 5 5 0.796           0.628       0.787         0.0658 0.980   0.926
#> 6 6 0.798           0.679       0.763         0.0509 0.884   0.563
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-classes'>
<ul>
<li><a href='#tab-CV-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-skmeans-get-classes-1'>
<p><a id='tab-CV-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1 p2
#&gt; SRR547975     2       0          1  0  1
#&gt; SRR547973     2       0          1  0  1
#&gt; SRR547968     2       0          1  0  1
#&gt; SRR547980     2       0          1  0  1
#&gt; SRR545058     1       0          1  1  0
#&gt; SRR546225     2       0          1  0  1
#&gt; SRR546226     1       0          1  1  0
#&gt; SRR546227     1       0          1  1  0
#&gt; SRR546228     1       0          1  1  0
#&gt; SRR546229     1       0          1  1  0
#&gt; SRR546230     1       0          1  1  0
#&gt; SRR546231     1       0          1  1  0
#&gt; SRR546232     1       0          1  1  0
#&gt; SRR546233     1       0          1  1  0
#&gt; SRR546234     1       0          1  1  0
#&gt; SRR546235     1       0          1  1  0
#&gt; SRR546236     1       0          1  1  0
#&gt; SRR546237     1       0          1  1  0
#&gt; SRR546238     1       0          1  1  0
#&gt; SRR546239     1       0          1  1  0
#&gt; SRR546240     1       0          1  1  0
#&gt; SRR547969     2       0          1  0  1
#&gt; SRR547970     2       0          1  0  1
#&gt; SRR547971     2       0          1  0  1
#&gt; SRR547972     2       0          1  0  1
#&gt; SRR547974     2       0          1  0  1
#&gt; SRR547976     2       0          1  0  1
#&gt; SRR547978     2       0          1  0  1
#&gt; SRR547979     2       0          1  0  1
#&gt; SRR547981     2       0          1  0  1
#&gt; SRR547982     2       0          1  0  1
#&gt; SRR547983     2       0          1  0  1
#&gt; SRR547989     2       0          1  0  1
#&gt; SRR547990     2       0          1  0  1
#&gt; SRR547991     2       0          1  0  1
#&gt; SRR547992     2       0          1  0  1
#&gt; SRR801424     1       0          1  1  0
#&gt; SRR801425     1       0          1  1  0
#&gt; SRR801426     1       0          1  1  0
#&gt; SRR801427     1       0          1  1  0
#&gt; SRR801428     1       0          1  1  0
#&gt; SRR801429     1       0          1  1  0
#&gt; SRR801430     1       0          1  1  0
#&gt; SRR801431     1       0          1  1  0
#&gt; SRR801432     1       0          1  1  0
#&gt; SRR801433     1       0          1  1  0
#&gt; SRR825135     1       0          1  1  0
#&gt; SRR825136     1       0          1  1  0
#&gt; SRR825137     1       0          1  1  0
#&gt; SRR825139     1       0          1  1  0
#&gt; SRR825140     1       0          1  1  0
#&gt; SRR825141     1       0          1  1  0
#&gt; SRR825143     1       0          1  1  0
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-1-a').click(function(){
  $('#tab-CV-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-2'>
<p><a id='tab-CV-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1 p2 p3
#&gt; SRR547975     2       0          1  0  1  0
#&gt; SRR547973     2       0          1  0  1  0
#&gt; SRR547968     2       0          1  0  1  0
#&gt; SRR547980     2       0          1  0  1  0
#&gt; SRR545058     3       0          1  0  0  1
#&gt; SRR546225     2       0          1  0  1  0
#&gt; SRR546226     1       0          1  1  0  0
#&gt; SRR546227     1       0          1  1  0  0
#&gt; SRR546228     3       0          1  0  0  1
#&gt; SRR546229     3       0          1  0  0  1
#&gt; SRR546230     1       0          1  1  0  0
#&gt; SRR546231     3       0          1  0  0  1
#&gt; SRR546232     1       0          1  1  0  0
#&gt; SRR546233     1       0          1  1  0  0
#&gt; SRR546234     3       0          1  0  0  1
#&gt; SRR546235     3       0          1  0  0  1
#&gt; SRR546236     3       0          1  0  0  1
#&gt; SRR546237     1       0          1  1  0  0
#&gt; SRR546238     3       0          1  0  0  1
#&gt; SRR546239     1       0          1  1  0  0
#&gt; SRR546240     1       0          1  1  0  0
#&gt; SRR547969     2       0          1  0  1  0
#&gt; SRR547970     2       0          1  0  1  0
#&gt; SRR547971     2       0          1  0  1  0
#&gt; SRR547972     2       0          1  0  1  0
#&gt; SRR547974     2       0          1  0  1  0
#&gt; SRR547976     2       0          1  0  1  0
#&gt; SRR547978     2       0          1  0  1  0
#&gt; SRR547979     2       0          1  0  1  0
#&gt; SRR547981     2       0          1  0  1  0
#&gt; SRR547982     2       0          1  0  1  0
#&gt; SRR547983     2       0          1  0  1  0
#&gt; SRR547989     2       0          1  0  1  0
#&gt; SRR547990     2       0          1  0  1  0
#&gt; SRR547991     2       0          1  0  1  0
#&gt; SRR547992     2       0          1  0  1  0
#&gt; SRR801424     1       0          1  1  0  0
#&gt; SRR801425     3       0          1  0  0  1
#&gt; SRR801426     3       0          1  0  0  1
#&gt; SRR801427     1       0          1  1  0  0
#&gt; SRR801428     1       0          1  1  0  0
#&gt; SRR801429     3       0          1  0  0  1
#&gt; SRR801430     1       0          1  1  0  0
#&gt; SRR801431     3       0          1  0  0  1
#&gt; SRR801432     3       0          1  0  0  1
#&gt; SRR801433     1       0          1  1  0  0
#&gt; SRR825135     3       0          1  0  0  1
#&gt; SRR825136     1       0          1  1  0  0
#&gt; SRR825137     3       0          1  0  0  1
#&gt; SRR825139     1       0          1  1  0  0
#&gt; SRR825140     1       0          1  1  0  0
#&gt; SRR825141     3       0          1  0  0  1
#&gt; SRR825143     1       0          1  1  0  0
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-2-a').click(function(){
  $('#tab-CV-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-3'>
<p><a id='tab-CV-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     2  0.0336      0.986 0.000 0.992 0.000 0.008
#&gt; SRR547973     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR547968     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR547980     2  0.0336      0.986 0.000 0.992 0.000 0.008
#&gt; SRR545058     3  0.0000      0.973 0.000 0.000 1.000 0.000
#&gt; SRR546225     2  0.1211      0.978 0.000 0.960 0.000 0.040
#&gt; SRR546226     1  0.0188      0.880 0.996 0.000 0.000 0.004
#&gt; SRR546227     1  0.1389      0.868 0.952 0.000 0.000 0.048
#&gt; SRR546228     3  0.0000      0.973 0.000 0.000 1.000 0.000
#&gt; SRR546229     3  0.2081      0.903 0.000 0.000 0.916 0.084
#&gt; SRR546230     1  0.0188      0.880 0.996 0.000 0.000 0.004
#&gt; SRR546231     3  0.1661      0.913 0.004 0.000 0.944 0.052
#&gt; SRR546232     1  0.0000      0.879 1.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.0188      0.880 0.996 0.000 0.000 0.004
#&gt; SRR546234     3  0.0000      0.973 0.000 0.000 1.000 0.000
#&gt; SRR546235     3  0.0000      0.973 0.000 0.000 1.000 0.000
#&gt; SRR546236     3  0.0000      0.973 0.000 0.000 1.000 0.000
#&gt; SRR546237     1  0.1637      0.863 0.940 0.000 0.000 0.060
#&gt; SRR546238     3  0.0000      0.973 0.000 0.000 1.000 0.000
#&gt; SRR546239     4  0.4996     -0.228 0.484 0.000 0.000 0.516
#&gt; SRR546240     1  0.1716      0.861 0.936 0.000 0.000 0.064
#&gt; SRR547969     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR547970     2  0.1211      0.978 0.000 0.960 0.000 0.040
#&gt; SRR547971     2  0.1211      0.978 0.000 0.960 0.000 0.040
#&gt; SRR547972     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR547974     2  0.0336      0.986 0.000 0.992 0.000 0.008
#&gt; SRR547976     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR547978     2  0.1118      0.979 0.000 0.964 0.000 0.036
#&gt; SRR547979     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR547981     2  0.1211      0.978 0.000 0.960 0.000 0.040
#&gt; SRR547982     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR547983     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR547989     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR547990     2  0.1211      0.978 0.000 0.960 0.000 0.040
#&gt; SRR547991     2  0.1118      0.979 0.000 0.964 0.000 0.036
#&gt; SRR547992     2  0.0000      0.987 0.000 1.000 0.000 0.000
#&gt; SRR801424     4  0.2760      0.615 0.128 0.000 0.000 0.872
#&gt; SRR801425     3  0.2589      0.867 0.000 0.000 0.884 0.116
#&gt; SRR801426     4  0.4985      0.159 0.000 0.000 0.468 0.532
#&gt; SRR801427     1  0.3219      0.715 0.836 0.000 0.000 0.164
#&gt; SRR801428     4  0.2760      0.615 0.128 0.000 0.000 0.872
#&gt; SRR801429     4  0.4431      0.535 0.000 0.000 0.304 0.696
#&gt; SRR801430     4  0.2760      0.615 0.128 0.000 0.000 0.872
#&gt; SRR801431     4  0.4585      0.494 0.000 0.000 0.332 0.668
#&gt; SRR801432     4  0.4431      0.535 0.000 0.000 0.304 0.696
#&gt; SRR801433     4  0.2760      0.615 0.128 0.000 0.000 0.872
#&gt; SRR825135     3  0.0000      0.973 0.000 0.000 1.000 0.000
#&gt; SRR825136     1  0.4804      0.437 0.616 0.000 0.000 0.384
#&gt; SRR825137     3  0.0000      0.973 0.000 0.000 1.000 0.000
#&gt; SRR825139     1  0.4830      0.419 0.608 0.000 0.000 0.392
#&gt; SRR825140     1  0.0188      0.880 0.996 0.000 0.000 0.004
#&gt; SRR825141     3  0.0000      0.973 0.000 0.000 1.000 0.000
#&gt; SRR825143     1  0.0188      0.880 0.996 0.000 0.000 0.004
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-3-a').click(function(){
  $('#tab-CV-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-4'>
<p><a id='tab-CV-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR547975     2  0.3305      0.828 0.000 0.776 0.000 0.000 0.224
#&gt; SRR547973     2  0.0290      0.845 0.000 0.992 0.000 0.000 0.008
#&gt; SRR547968     2  0.0000      0.844 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547980     2  0.3003      0.833 0.000 0.812 0.000 0.000 0.188
#&gt; SRR545058     3  0.0290      0.912 0.000 0.000 0.992 0.000 0.008
#&gt; SRR546225     2  0.4150      0.760 0.000 0.612 0.000 0.000 0.388
#&gt; SRR546226     1  0.0000      0.696 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.3910      0.517 0.720 0.000 0.000 0.008 0.272
#&gt; SRR546228     3  0.0162      0.913 0.000 0.000 0.996 0.000 0.004
#&gt; SRR546229     3  0.4367      0.405 0.000 0.000 0.620 0.372 0.008
#&gt; SRR546230     1  0.0000      0.696 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.4269      0.574 0.000 0.000 0.684 0.016 0.300
#&gt; SRR546232     1  0.3266      0.588 0.796 0.000 0.000 0.004 0.200
#&gt; SRR546233     1  0.0000      0.696 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546234     3  0.0671      0.910 0.000 0.000 0.980 0.004 0.016
#&gt; SRR546235     3  0.0451      0.913 0.000 0.000 0.988 0.004 0.008
#&gt; SRR546236     3  0.0510      0.908 0.000 0.000 0.984 0.000 0.016
#&gt; SRR546237     1  0.4323      0.428 0.656 0.000 0.000 0.012 0.332
#&gt; SRR546238     3  0.0566      0.911 0.000 0.000 0.984 0.012 0.004
#&gt; SRR546239     5  0.6304      0.000 0.248 0.000 0.000 0.220 0.532
#&gt; SRR546240     1  0.5020      0.372 0.620 0.000 0.020 0.016 0.344
#&gt; SRR547969     2  0.0000      0.844 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547970     2  0.4219      0.750 0.000 0.584 0.000 0.000 0.416
#&gt; SRR547971     2  0.4101      0.776 0.000 0.628 0.000 0.000 0.372
#&gt; SRR547972     2  0.0000      0.844 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547974     2  0.3210      0.830 0.000 0.788 0.000 0.000 0.212
#&gt; SRR547976     2  0.0703      0.845 0.000 0.976 0.000 0.000 0.024
#&gt; SRR547978     2  0.3913      0.798 0.000 0.676 0.000 0.000 0.324
#&gt; SRR547979     2  0.0162      0.844 0.000 0.996 0.000 0.000 0.004
#&gt; SRR547981     2  0.4210      0.753 0.000 0.588 0.000 0.000 0.412
#&gt; SRR547982     2  0.0000      0.844 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547983     2  0.0000      0.844 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547989     2  0.0000      0.844 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547990     2  0.4219      0.750 0.000 0.584 0.000 0.000 0.416
#&gt; SRR547991     2  0.3913      0.798 0.000 0.676 0.000 0.000 0.324
#&gt; SRR547992     2  0.0000      0.844 0.000 1.000 0.000 0.000 0.000
#&gt; SRR801424     4  0.5240      0.124 0.056 0.000 0.000 0.584 0.360
#&gt; SRR801425     4  0.4557     -0.174 0.000 0.000 0.476 0.516 0.008
#&gt; SRR801426     4  0.2813      0.515 0.000 0.000 0.168 0.832 0.000
#&gt; SRR801427     1  0.2171      0.630 0.912 0.000 0.000 0.064 0.024
#&gt; SRR801428     4  0.5240      0.124 0.056 0.000 0.000 0.584 0.360
#&gt; SRR801429     4  0.1908      0.547 0.000 0.000 0.092 0.908 0.000
#&gt; SRR801430     4  0.5240      0.124 0.056 0.000 0.000 0.584 0.360
#&gt; SRR801431     4  0.2338      0.546 0.000 0.000 0.112 0.884 0.004
#&gt; SRR801432     4  0.2068      0.547 0.000 0.000 0.092 0.904 0.004
#&gt; SRR801433     4  0.5240      0.124 0.056 0.000 0.000 0.584 0.360
#&gt; SRR825135     3  0.0579      0.912 0.000 0.000 0.984 0.008 0.008
#&gt; SRR825136     1  0.6040     -0.338 0.556 0.000 0.000 0.152 0.292
#&gt; SRR825137     3  0.0451      0.913 0.000 0.000 0.988 0.004 0.008
#&gt; SRR825139     1  0.6072     -0.350 0.552 0.000 0.000 0.156 0.292
#&gt; SRR825140     1  0.0000      0.696 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0451      0.913 0.000 0.000 0.988 0.004 0.008
#&gt; SRR825143     1  0.0000      0.696 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-4-a').click(function(){
  $('#tab-CV-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-skmeans-get-classes-5'>
<p><a id='tab-CV-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR547975     2  0.3659     0.0259 0.000 0.636 0.000 0.000 0.364 0.000
#&gt; SRR547973     2  0.1075     0.8085 0.000 0.952 0.000 0.000 0.048 0.000
#&gt; SRR547968     2  0.0000     0.8303 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547980     2  0.3428     0.2650 0.000 0.696 0.000 0.000 0.304 0.000
#&gt; SRR545058     3  0.1088     0.8554 0.000 0.000 0.960 0.016 0.024 0.000
#&gt; SRR546225     5  0.4111     0.7119 0.000 0.296 0.004 0.024 0.676 0.000
#&gt; SRR546226     1  0.0000     0.7216 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.6925     0.4439 0.496 0.000 0.000 0.184 0.132 0.188
#&gt; SRR546228     3  0.0692     0.8579 0.000 0.000 0.976 0.004 0.020 0.000
#&gt; SRR546229     4  0.4765     0.4561 0.000 0.000 0.320 0.624 0.040 0.016
#&gt; SRR546230     1  0.0000     0.7216 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.7323     0.1900 0.000 0.000 0.420 0.224 0.160 0.196
#&gt; SRR546232     1  0.5184     0.5874 0.664 0.000 0.000 0.184 0.132 0.020
#&gt; SRR546233     1  0.0000     0.7216 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546234     3  0.2069     0.8373 0.000 0.000 0.908 0.020 0.068 0.004
#&gt; SRR546235     3  0.1480     0.8593 0.000 0.000 0.940 0.040 0.020 0.000
#&gt; SRR546236     3  0.1649     0.8603 0.000 0.000 0.932 0.032 0.036 0.000
#&gt; SRR546237     1  0.7348     0.3358 0.404 0.000 0.000 0.212 0.144 0.240
#&gt; SRR546238     3  0.2854     0.7998 0.000 0.000 0.860 0.088 0.048 0.004
#&gt; SRR546239     6  0.4769     0.5332 0.048 0.000 0.000 0.204 0.044 0.704
#&gt; SRR546240     1  0.8521     0.1893 0.288 0.000 0.076 0.216 0.156 0.264
#&gt; SRR547969     2  0.0146     0.8305 0.000 0.996 0.000 0.000 0.004 0.000
#&gt; SRR547970     5  0.3337     0.8140 0.000 0.260 0.000 0.004 0.736 0.000
#&gt; SRR547971     5  0.3672     0.7806 0.000 0.368 0.000 0.000 0.632 0.000
#&gt; SRR547972     2  0.0000     0.8303 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547974     2  0.3695    -0.0364 0.000 0.624 0.000 0.000 0.376 0.000
#&gt; SRR547976     2  0.1714     0.7626 0.000 0.908 0.000 0.000 0.092 0.000
#&gt; SRR547978     5  0.3979     0.6659 0.000 0.456 0.000 0.004 0.540 0.000
#&gt; SRR547979     2  0.0632     0.8254 0.000 0.976 0.000 0.000 0.024 0.000
#&gt; SRR547981     5  0.3351     0.8198 0.000 0.288 0.000 0.000 0.712 0.000
#&gt; SRR547982     2  0.0000     0.8303 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547983     2  0.0508     0.8293 0.000 0.984 0.000 0.004 0.012 0.000
#&gt; SRR547989     2  0.0508     0.8293 0.000 0.984 0.000 0.004 0.012 0.000
#&gt; SRR547990     5  0.3337     0.8140 0.000 0.260 0.000 0.004 0.736 0.000
#&gt; SRR547991     5  0.3979     0.6659 0.000 0.456 0.000 0.004 0.540 0.000
#&gt; SRR547992     2  0.0000     0.8303 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR801424     6  0.0458     0.7363 0.016 0.000 0.000 0.000 0.000 0.984
#&gt; SRR801425     4  0.5058     0.6633 0.000 0.000 0.200 0.684 0.040 0.076
#&gt; SRR801426     4  0.3841     0.8021 0.000 0.000 0.028 0.716 0.000 0.256
#&gt; SRR801427     1  0.1501     0.6799 0.924 0.000 0.000 0.000 0.000 0.076
#&gt; SRR801428     6  0.0458     0.7363 0.016 0.000 0.000 0.000 0.000 0.984
#&gt; SRR801429     4  0.3508     0.7988 0.000 0.000 0.004 0.704 0.000 0.292
#&gt; SRR801430     6  0.0458     0.7363 0.016 0.000 0.000 0.000 0.000 0.984
#&gt; SRR801431     4  0.3690     0.8010 0.000 0.000 0.012 0.700 0.000 0.288
#&gt; SRR801432     4  0.3508     0.7988 0.000 0.000 0.004 0.704 0.000 0.292
#&gt; SRR801433     6  0.0458     0.7363 0.016 0.000 0.000 0.000 0.000 0.984
#&gt; SRR825135     3  0.2631     0.8179 0.000 0.000 0.876 0.076 0.044 0.004
#&gt; SRR825136     6  0.3937     0.4026 0.424 0.000 0.000 0.004 0.000 0.572
#&gt; SRR825137     3  0.1700     0.8577 0.000 0.000 0.928 0.048 0.024 0.000
#&gt; SRR825139     6  0.3810     0.4004 0.428 0.000 0.000 0.000 0.000 0.572
#&gt; SRR825140     1  0.0000     0.7216 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.2237     0.8520 0.000 0.000 0.896 0.068 0.036 0.000
#&gt; SRR825143     1  0.0000     0.7216 1.000 0.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-skmeans-get-classes-5-a').click(function(){
  $('#tab-CV-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-CV-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-signatures'>
<ul>
<li><a href='#tab-CV-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-skmeans-signature_compare](figure_cola/CV-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-CV-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-skmeans-collect-classes](figure_cola/CV-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:pam**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "pam"]
# you can also extract it by
# res = res_list["CV:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-pam-collect-plots](figure_cola/CV-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-pam-select-partition-number](figure_cola/CV-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.975       0.991         0.4747 0.521   0.521
#> 3 3 0.732           0.829       0.893         0.3654 0.833   0.680
#> 4 4 0.729           0.793       0.891         0.1200 0.865   0.642
#> 5 5 0.802           0.778       0.893         0.0807 0.914   0.696
#> 6 6 0.894           0.857       0.925         0.0428 0.959   0.813
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-classes'>
<ul>
<li><a href='#tab-CV-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-pam-get-classes-1'>
<p><a id='tab-CV-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR547975     2  0.0000      0.975 0.000 1.000
#&gt; SRR547973     2  0.0000      0.975 0.000 1.000
#&gt; SRR547968     2  0.0000      0.975 0.000 1.000
#&gt; SRR547980     2  0.0000      0.975 0.000 1.000
#&gt; SRR545058     1  0.0000      1.000 1.000 0.000
#&gt; SRR546225     2  0.9954      0.150 0.460 0.540
#&gt; SRR546226     1  0.0000      1.000 1.000 0.000
#&gt; SRR546227     1  0.0000      1.000 1.000 0.000
#&gt; SRR546228     1  0.0000      1.000 1.000 0.000
#&gt; SRR546229     1  0.0000      1.000 1.000 0.000
#&gt; SRR546230     1  0.0000      1.000 1.000 0.000
#&gt; SRR546231     1  0.0000      1.000 1.000 0.000
#&gt; SRR546232     1  0.0000      1.000 1.000 0.000
#&gt; SRR546233     1  0.0000      1.000 1.000 0.000
#&gt; SRR546234     1  0.0000      1.000 1.000 0.000
#&gt; SRR546235     1  0.0000      1.000 1.000 0.000
#&gt; SRR546236     1  0.0000      1.000 1.000 0.000
#&gt; SRR546237     1  0.0000      1.000 1.000 0.000
#&gt; SRR546238     1  0.0000      1.000 1.000 0.000
#&gt; SRR546239     1  0.0000      1.000 1.000 0.000
#&gt; SRR546240     1  0.0000      1.000 1.000 0.000
#&gt; SRR547969     2  0.0000      0.975 0.000 1.000
#&gt; SRR547970     2  0.0000      0.975 0.000 1.000
#&gt; SRR547971     2  0.0000      0.975 0.000 1.000
#&gt; SRR547972     2  0.0000      0.975 0.000 1.000
#&gt; SRR547974     2  0.0000      0.975 0.000 1.000
#&gt; SRR547976     2  0.0000      0.975 0.000 1.000
#&gt; SRR547978     2  0.0000      0.975 0.000 1.000
#&gt; SRR547979     2  0.0000      0.975 0.000 1.000
#&gt; SRR547981     2  0.0000      0.975 0.000 1.000
#&gt; SRR547982     2  0.0000      0.975 0.000 1.000
#&gt; SRR547983     2  0.0000      0.975 0.000 1.000
#&gt; SRR547989     2  0.0000      0.975 0.000 1.000
#&gt; SRR547990     2  0.0938      0.964 0.012 0.988
#&gt; SRR547991     2  0.0000      0.975 0.000 1.000
#&gt; SRR547992     2  0.0000      0.975 0.000 1.000
#&gt; SRR801424     1  0.0000      1.000 1.000 0.000
#&gt; SRR801425     1  0.0000      1.000 1.000 0.000
#&gt; SRR801426     1  0.0000      1.000 1.000 0.000
#&gt; SRR801427     1  0.0000      1.000 1.000 0.000
#&gt; SRR801428     1  0.0000      1.000 1.000 0.000
#&gt; SRR801429     1  0.0000      1.000 1.000 0.000
#&gt; SRR801430     1  0.0000      1.000 1.000 0.000
#&gt; SRR801431     1  0.0000      1.000 1.000 0.000
#&gt; SRR801432     1  0.0000      1.000 1.000 0.000
#&gt; SRR801433     1  0.0000      1.000 1.000 0.000
#&gt; SRR825135     1  0.0000      1.000 1.000 0.000
#&gt; SRR825136     1  0.0000      1.000 1.000 0.000
#&gt; SRR825137     1  0.0000      1.000 1.000 0.000
#&gt; SRR825139     1  0.0000      1.000 1.000 0.000
#&gt; SRR825140     1  0.0000      1.000 1.000 0.000
#&gt; SRR825141     1  0.0000      1.000 1.000 0.000
#&gt; SRR825143     1  0.0000      1.000 1.000 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-1-a').click(function(){
  $('#tab-CV-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-2'>
<p><a id='tab-CV-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     2  0.0000      0.968 0.000 1.000 0.000
#&gt; SRR547973     2  0.0000      0.968 0.000 1.000 0.000
#&gt; SRR547968     2  0.0000      0.968 0.000 1.000 0.000
#&gt; SRR547980     2  0.0000      0.968 0.000 1.000 0.000
#&gt; SRR545058     3  0.0592      0.928 0.012 0.000 0.988
#&gt; SRR546225     2  0.9147      0.105 0.260 0.540 0.200
#&gt; SRR546226     1  0.4555      0.822 0.800 0.000 0.200
#&gt; SRR546227     1  0.4555      0.822 0.800 0.000 0.200
#&gt; SRR546228     3  0.0592      0.928 0.012 0.000 0.988
#&gt; SRR546229     1  0.6260      0.606 0.552 0.000 0.448
#&gt; SRR546230     1  0.4555      0.822 0.800 0.000 0.200
#&gt; SRR546231     3  0.4605      0.730 0.204 0.000 0.796
#&gt; SRR546232     1  0.4555      0.822 0.800 0.000 0.200
#&gt; SRR546233     1  0.4555      0.822 0.800 0.000 0.200
#&gt; SRR546234     1  0.6252      0.612 0.556 0.000 0.444
#&gt; SRR546235     3  0.0592      0.928 0.012 0.000 0.988
#&gt; SRR546236     3  0.0592      0.928 0.012 0.000 0.988
#&gt; SRR546237     1  0.4555      0.822 0.800 0.000 0.200
#&gt; SRR546238     1  0.6295      0.523 0.528 0.000 0.472
#&gt; SRR546239     1  0.4235      0.621 0.824 0.000 0.176
#&gt; SRR546240     1  0.4555      0.822 0.800 0.000 0.200
#&gt; SRR547969     2  0.0000      0.968 0.000 1.000 0.000
#&gt; SRR547970     2  0.0592      0.965 0.000 0.988 0.012
#&gt; SRR547971     2  0.0592      0.965 0.000 0.988 0.012
#&gt; SRR547972     2  0.0000      0.968 0.000 1.000 0.000
#&gt; SRR547974     2  0.0000      0.968 0.000 1.000 0.000
#&gt; SRR547976     2  0.0000      0.968 0.000 1.000 0.000
#&gt; SRR547978     2  0.0592      0.965 0.000 0.988 0.012
#&gt; SRR547979     2  0.0000      0.968 0.000 1.000 0.000
#&gt; SRR547981     2  0.0592      0.965 0.000 0.988 0.012
#&gt; SRR547982     2  0.0000      0.968 0.000 1.000 0.000
#&gt; SRR547983     2  0.0000      0.968 0.000 1.000 0.000
#&gt; SRR547989     2  0.0000      0.968 0.000 1.000 0.000
#&gt; SRR547990     2  0.0892      0.959 0.000 0.980 0.020
#&gt; SRR547991     2  0.0592      0.965 0.000 0.988 0.012
#&gt; SRR547992     2  0.0000      0.968 0.000 1.000 0.000
#&gt; SRR801424     1  0.0000      0.709 1.000 0.000 0.000
#&gt; SRR801425     3  0.0592      0.928 0.012 0.000 0.988
#&gt; SRR801426     1  0.6260      0.606 0.552 0.000 0.448
#&gt; SRR801427     1  0.4555      0.822 0.800 0.000 0.200
#&gt; SRR801428     1  0.1643      0.701 0.956 0.000 0.044
#&gt; SRR801429     1  0.5363      0.560 0.724 0.000 0.276
#&gt; SRR801430     1  0.4235      0.621 0.824 0.000 0.176
#&gt; SRR801431     3  0.5706      0.632 0.320 0.000 0.680
#&gt; SRR801432     1  0.5098      0.531 0.752 0.000 0.248
#&gt; SRR801433     1  0.0000      0.709 1.000 0.000 0.000
#&gt; SRR825135     3  0.0592      0.928 0.012 0.000 0.988
#&gt; SRR825136     1  0.4555      0.822 0.800 0.000 0.200
#&gt; SRR825137     3  0.0592      0.928 0.012 0.000 0.988
#&gt; SRR825139     1  0.4555      0.822 0.800 0.000 0.200
#&gt; SRR825140     1  0.4555      0.822 0.800 0.000 0.200
#&gt; SRR825141     3  0.0592      0.928 0.012 0.000 0.988
#&gt; SRR825143     1  0.4555      0.822 0.800 0.000 0.200
</code></pre>

<script>
$('#tab-CV-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-2-a').click(function(){
  $('#tab-CV-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-3'>
<p><a id='tab-CV-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     2  0.0000     0.9529 0.000 1.000 0.000 0.000
#&gt; SRR547973     2  0.0000     0.9529 0.000 1.000 0.000 0.000
#&gt; SRR547968     2  0.0000     0.9529 0.000 1.000 0.000 0.000
#&gt; SRR547980     2  0.2530     0.9223 0.000 0.888 0.112 0.000
#&gt; SRR545058     3  0.2814     0.9209 0.132 0.000 0.868 0.000
#&gt; SRR546225     1  0.5097     0.2497 0.568 0.428 0.004 0.000
#&gt; SRR546226     1  0.0000     0.8351 1.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000     0.8351 1.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.2814     0.9209 0.132 0.000 0.868 0.000
#&gt; SRR546229     1  0.4933     0.0407 0.568 0.000 0.432 0.000
#&gt; SRR546230     1  0.0000     0.8351 1.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.3105     0.7197 0.012 0.000 0.868 0.120
#&gt; SRR546232     1  0.0000     0.8351 1.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.0000     0.8351 1.000 0.000 0.000 0.000
#&gt; SRR546234     1  0.3873     0.5641 0.772 0.000 0.228 0.000
#&gt; SRR546235     3  0.2814     0.9209 0.132 0.000 0.868 0.000
#&gt; SRR546236     3  0.2814     0.9209 0.132 0.000 0.868 0.000
#&gt; SRR546237     1  0.0000     0.8351 1.000 0.000 0.000 0.000
#&gt; SRR546238     3  0.5000     0.1272 0.496 0.000 0.504 0.000
#&gt; SRR546239     4  0.0336     0.8282 0.008 0.000 0.000 0.992
#&gt; SRR546240     1  0.0188     0.8322 0.996 0.000 0.004 0.000
#&gt; SRR547969     2  0.0000     0.9529 0.000 1.000 0.000 0.000
#&gt; SRR547970     2  0.3142     0.9128 0.000 0.860 0.132 0.008
#&gt; SRR547971     2  0.3142     0.9128 0.000 0.860 0.132 0.008
#&gt; SRR547972     2  0.0000     0.9529 0.000 1.000 0.000 0.000
#&gt; SRR547974     2  0.0000     0.9529 0.000 1.000 0.000 0.000
#&gt; SRR547976     2  0.0000     0.9529 0.000 1.000 0.000 0.000
#&gt; SRR547978     2  0.3142     0.9128 0.000 0.860 0.132 0.008
#&gt; SRR547979     2  0.0000     0.9529 0.000 1.000 0.000 0.000
#&gt; SRR547981     2  0.3142     0.9128 0.000 0.860 0.132 0.008
#&gt; SRR547982     2  0.0000     0.9529 0.000 1.000 0.000 0.000
#&gt; SRR547983     2  0.0000     0.9529 0.000 1.000 0.000 0.000
#&gt; SRR547989     2  0.0000     0.9529 0.000 1.000 0.000 0.000
#&gt; SRR547990     2  0.3598     0.9047 0.012 0.848 0.132 0.008
#&gt; SRR547991     2  0.3142     0.9128 0.000 0.860 0.132 0.008
#&gt; SRR547992     2  0.0000     0.9529 0.000 1.000 0.000 0.000
#&gt; SRR801424     4  0.0336     0.8282 0.008 0.000 0.000 0.992
#&gt; SRR801425     3  0.2814     0.9209 0.132 0.000 0.868 0.000
#&gt; SRR801426     1  0.6635     0.0195 0.524 0.000 0.388 0.088
#&gt; SRR801427     1  0.0000     0.8351 1.000 0.000 0.000 0.000
#&gt; SRR801428     4  0.0336     0.8282 0.008 0.000 0.000 0.992
#&gt; SRR801429     4  0.7585     0.3262 0.304 0.000 0.224 0.472
#&gt; SRR801430     4  0.0336     0.8282 0.008 0.000 0.000 0.992
#&gt; SRR801431     4  0.4746     0.4533 0.000 0.000 0.368 0.632
#&gt; SRR801432     4  0.4194     0.6606 0.008 0.000 0.228 0.764
#&gt; SRR801433     4  0.0336     0.8282 0.008 0.000 0.000 0.992
#&gt; SRR825135     3  0.2814     0.9209 0.132 0.000 0.868 0.000
#&gt; SRR825136     1  0.0000     0.8351 1.000 0.000 0.000 0.000
#&gt; SRR825137     3  0.2814     0.9209 0.132 0.000 0.868 0.000
#&gt; SRR825139     1  0.4866     0.3573 0.596 0.000 0.000 0.404
#&gt; SRR825140     1  0.0000     0.8351 1.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.2814     0.9209 0.132 0.000 0.868 0.000
#&gt; SRR825143     1  0.0000     0.8351 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-3-a').click(function(){
  $('#tab-CV-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-4'>
<p><a id='tab-CV-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR547975     2  0.0000     0.9416 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547973     2  0.0000     0.9416 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547968     2  0.0000     0.9416 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547980     2  0.3039     0.6813 0.000 0.808 0.000 0.000 0.192
#&gt; SRR545058     3  0.0000     0.9036 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546225     1  0.4383     0.2682 0.572 0.424 0.004 0.000 0.000
#&gt; SRR546226     1  0.0000     0.8476 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000     0.8476 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.0000     0.9036 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546229     1  0.6212     0.2938 0.516 0.000 0.324 0.000 0.160
#&gt; SRR546230     1  0.0000     0.8476 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.0000     0.9036 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546232     1  0.0000     0.8476 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.0000     0.8476 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546234     1  0.4125     0.6620 0.772 0.000 0.172 0.000 0.056
#&gt; SRR546235     3  0.0000     0.9036 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546236     3  0.0000     0.9036 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546237     1  0.0000     0.8476 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546238     1  0.4980     0.0963 0.488 0.000 0.484 0.000 0.028
#&gt; SRR546239     4  0.0000     0.8071 0.000 0.000 0.000 1.000 0.000
#&gt; SRR546240     1  0.0162     0.8452 0.996 0.000 0.004 0.000 0.000
#&gt; SRR547969     2  0.0000     0.9416 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547970     5  0.3586     0.8393 0.000 0.264 0.000 0.000 0.736
#&gt; SRR547971     5  0.2732     0.9647 0.000 0.160 0.000 0.000 0.840
#&gt; SRR547972     2  0.0000     0.9416 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547974     2  0.0000     0.9416 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547976     2  0.0000     0.9416 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547978     5  0.2732     0.9647 0.000 0.160 0.000 0.000 0.840
#&gt; SRR547979     2  0.0000     0.9416 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547981     2  0.4201     0.0649 0.000 0.592 0.000 0.000 0.408
#&gt; SRR547982     2  0.0000     0.9416 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547983     2  0.0000     0.9416 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547989     2  0.0000     0.9416 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547990     5  0.2732     0.9647 0.000 0.160 0.000 0.000 0.840
#&gt; SRR547991     5  0.2732     0.9647 0.000 0.160 0.000 0.000 0.840
#&gt; SRR547992     2  0.0000     0.9416 0.000 1.000 0.000 0.000 0.000
#&gt; SRR801424     4  0.0000     0.8071 0.000 0.000 0.000 1.000 0.000
#&gt; SRR801425     3  0.2732     0.7592 0.000 0.000 0.840 0.000 0.160
#&gt; SRR801426     3  0.8379    -0.1175 0.284 0.000 0.340 0.216 0.160
#&gt; SRR801427     1  0.0000     0.8476 1.000 0.000 0.000 0.000 0.000
#&gt; SRR801428     4  0.0000     0.8071 0.000 0.000 0.000 1.000 0.000
#&gt; SRR801429     4  0.7886     0.4395 0.200 0.000 0.168 0.472 0.160
#&gt; SRR801430     4  0.0000     0.8071 0.000 0.000 0.000 1.000 0.000
#&gt; SRR801431     4  0.5961     0.5054 0.000 0.000 0.260 0.580 0.160
#&gt; SRR801432     4  0.5378     0.6280 0.000 0.000 0.172 0.668 0.160
#&gt; SRR801433     4  0.0000     0.8071 0.000 0.000 0.000 1.000 0.000
#&gt; SRR825135     3  0.0000     0.9036 0.000 0.000 1.000 0.000 0.000
#&gt; SRR825136     1  0.0000     0.8476 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825137     3  0.0000     0.9036 0.000 0.000 1.000 0.000 0.000
#&gt; SRR825139     1  0.4192     0.3812 0.596 0.000 0.000 0.404 0.000
#&gt; SRR825140     1  0.0000     0.8476 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0000     0.9036 0.000 0.000 1.000 0.000 0.000
#&gt; SRR825143     1  0.0000     0.8476 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-4-a').click(function(){
  $('#tab-CV-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-pam-get-classes-5'>
<p><a id='tab-CV-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR547975     2  0.0146      0.925 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR547973     2  0.0000      0.926 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547968     2  0.0000      0.926 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547980     2  0.3488      0.801 0.000 0.780 0.000 0.000 0.036 0.184
#&gt; SRR545058     3  0.0000      0.997 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546225     1  0.3797      0.266 0.580 0.420 0.000 0.000 0.000 0.000
#&gt; SRR546226     1  0.0000      0.872 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0363      0.869 0.988 0.000 0.000 0.012 0.000 0.000
#&gt; SRR546228     3  0.0000      0.997 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546229     4  0.2762      0.689 0.196 0.000 0.000 0.804 0.000 0.000
#&gt; SRR546230     1  0.0000      0.872 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.0363      0.987 0.000 0.000 0.988 0.012 0.000 0.000
#&gt; SRR546232     1  0.0363      0.869 0.988 0.000 0.000 0.012 0.000 0.000
#&gt; SRR546233     1  0.0000      0.872 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546234     1  0.2793      0.682 0.800 0.000 0.000 0.200 0.000 0.000
#&gt; SRR546235     3  0.0000      0.997 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546236     3  0.0260      0.990 0.000 0.000 0.992 0.008 0.000 0.000
#&gt; SRR546237     1  0.0363      0.869 0.988 0.000 0.000 0.012 0.000 0.000
#&gt; SRR546238     1  0.5527      0.126 0.460 0.000 0.408 0.132 0.000 0.000
#&gt; SRR546239     6  0.2762      0.986 0.000 0.000 0.000 0.196 0.000 0.804
#&gt; SRR546240     1  0.0363      0.869 0.988 0.000 0.000 0.012 0.000 0.000
#&gt; SRR547969     2  0.0260      0.923 0.000 0.992 0.000 0.000 0.000 0.008
#&gt; SRR547970     5  0.2378      0.783 0.000 0.152 0.000 0.000 0.848 0.000
#&gt; SRR547971     5  0.0000      0.947 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547972     2  0.0000      0.926 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547974     2  0.0000      0.926 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547976     2  0.0000      0.926 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547978     5  0.0000      0.947 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547979     2  0.0000      0.926 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547981     2  0.3782      0.335 0.000 0.588 0.000 0.000 0.412 0.000
#&gt; SRR547982     2  0.0000      0.926 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547983     2  0.2664      0.829 0.000 0.816 0.000 0.000 0.000 0.184
#&gt; SRR547989     2  0.2664      0.829 0.000 0.816 0.000 0.000 0.000 0.184
#&gt; SRR547990     5  0.0000      0.947 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547991     5  0.0000      0.947 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547992     2  0.0000      0.926 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR801424     6  0.2664      0.996 0.000 0.000 0.000 0.184 0.000 0.816
#&gt; SRR801425     4  0.2762      0.718 0.000 0.000 0.196 0.804 0.000 0.000
#&gt; SRR801426     4  0.0725      0.866 0.012 0.000 0.012 0.976 0.000 0.000
#&gt; SRR801427     1  0.0000      0.872 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR801428     6  0.2664      0.996 0.000 0.000 0.000 0.184 0.000 0.816
#&gt; SRR801429     4  0.0363      0.866 0.012 0.000 0.000 0.988 0.000 0.000
#&gt; SRR801430     6  0.2664      0.996 0.000 0.000 0.000 0.184 0.000 0.816
#&gt; SRR801431     4  0.0363      0.856 0.000 0.000 0.000 0.988 0.000 0.012
#&gt; SRR801432     4  0.0363      0.866 0.012 0.000 0.000 0.988 0.000 0.000
#&gt; SRR801433     6  0.2664      0.996 0.000 0.000 0.000 0.184 0.000 0.816
#&gt; SRR825135     3  0.0000      0.997 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR825136     1  0.0000      0.872 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR825137     3  0.0000      0.997 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR825139     1  0.3765      0.367 0.596 0.000 0.000 0.000 0.000 0.404
#&gt; SRR825140     1  0.0000      0.872 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0000      0.997 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR825143     1  0.0000      0.872 1.000 0.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-pam-get-classes-5-a').click(function(){
  $('#tab-CV-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-pam-membership-heatmap'>
<ul>
<li><a href='#tab-CV-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-signatures'>
<ul>
<li><a href='#tab-CV-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-1-1.png" alt="plot of chunk tab-CV-pam-get-signatures-1"/></p>

</div>
<div id='tab-CV-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-2-1.png" alt="plot of chunk tab-CV-pam-get-signatures-2"/></p>

</div>
<div id='tab-CV-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-3-1.png" alt="plot of chunk tab-CV-pam-get-signatures-3"/></p>

</div>
<div id='tab-CV-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-4-1.png" alt="plot of chunk tab-CV-pam-get-signatures-4"/></p>

</div>
<div id='tab-CV-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-5-1.png" alt="plot of chunk tab-CV-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-pam-signature_compare](figure_cola/CV-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-pam-dimension-reduction'>
<ul>
<li><a href='#tab-CV-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-pam-collect-classes](figure_cola/CV-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:mclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "mclust"]
# you can also extract it by
# res = res_list["CV:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-mclust-collect-plots](figure_cola/CV-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-mclust-select-partition-number](figure_cola/CV-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.957       0.981         0.4557 0.543   0.543
#> 3 3 0.986           0.951       0.979         0.4860 0.753   0.555
#> 4 4 0.824           0.895       0.875         0.0923 0.935   0.797
#> 5 5 0.767           0.637       0.770         0.0474 0.900   0.666
#> 6 6 0.753           0.580       0.774         0.0462 0.910   0.652
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-classes'>
<ul>
<li><a href='#tab-CV-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-mclust-get-classes-1'>
<p><a id='tab-CV-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR547975     2  0.1414      0.960 0.020 0.980
#&gt; SRR547973     2  0.0000      0.972 0.000 1.000
#&gt; SRR547968     2  0.0000      0.972 0.000 1.000
#&gt; SRR547980     2  0.0376      0.971 0.004 0.996
#&gt; SRR545058     1  0.0672      0.983 0.992 0.008
#&gt; SRR546225     1  0.0672      0.983 0.992 0.008
#&gt; SRR546226     1  0.0000      0.984 1.000 0.000
#&gt; SRR546227     1  0.0000      0.984 1.000 0.000
#&gt; SRR546228     1  0.0672      0.983 0.992 0.008
#&gt; SRR546229     1  0.0672      0.983 0.992 0.008
#&gt; SRR546230     1  0.0000      0.984 1.000 0.000
#&gt; SRR546231     1  0.0000      0.984 1.000 0.000
#&gt; SRR546232     1  0.0000      0.984 1.000 0.000
#&gt; SRR546233     1  0.0000      0.984 1.000 0.000
#&gt; SRR546234     1  0.0672      0.983 0.992 0.008
#&gt; SRR546235     1  0.0672      0.983 0.992 0.008
#&gt; SRR546236     1  0.0672      0.983 0.992 0.008
#&gt; SRR546237     1  0.0000      0.984 1.000 0.000
#&gt; SRR546238     1  0.0672      0.983 0.992 0.008
#&gt; SRR546239     1  0.0000      0.984 1.000 0.000
#&gt; SRR546240     1  0.0000      0.984 1.000 0.000
#&gt; SRR547969     2  0.0000      0.972 0.000 1.000
#&gt; SRR547970     2  0.7376      0.750 0.208 0.792
#&gt; SRR547971     2  0.0376      0.971 0.004 0.996
#&gt; SRR547972     2  0.0000      0.972 0.000 1.000
#&gt; SRR547974     2  0.1184      0.963 0.016 0.984
#&gt; SRR547976     2  0.0000      0.972 0.000 1.000
#&gt; SRR547978     2  0.0376      0.971 0.004 0.996
#&gt; SRR547979     2  0.0000      0.972 0.000 1.000
#&gt; SRR547981     2  0.7376      0.750 0.208 0.792
#&gt; SRR547982     2  0.0000      0.972 0.000 1.000
#&gt; SRR547983     2  0.0000      0.972 0.000 1.000
#&gt; SRR547989     2  0.0000      0.972 0.000 1.000
#&gt; SRR547990     1  0.9754      0.277 0.592 0.408
#&gt; SRR547991     2  0.0376      0.971 0.004 0.996
#&gt; SRR547992     2  0.0000      0.972 0.000 1.000
#&gt; SRR801424     1  0.0000      0.984 1.000 0.000
#&gt; SRR801425     1  0.0672      0.983 0.992 0.008
#&gt; SRR801426     1  0.0672      0.983 0.992 0.008
#&gt; SRR801427     1  0.0000      0.984 1.000 0.000
#&gt; SRR801428     1  0.0000      0.984 1.000 0.000
#&gt; SRR801429     1  0.0672      0.983 0.992 0.008
#&gt; SRR801430     1  0.0000      0.984 1.000 0.000
#&gt; SRR801431     1  0.0672      0.983 0.992 0.008
#&gt; SRR801432     1  0.0672      0.983 0.992 0.008
#&gt; SRR801433     1  0.0000      0.984 1.000 0.000
#&gt; SRR825135     1  0.0672      0.983 0.992 0.008
#&gt; SRR825136     1  0.0000      0.984 1.000 0.000
#&gt; SRR825137     1  0.0672      0.983 0.992 0.008
#&gt; SRR825139     1  0.0000      0.984 1.000 0.000
#&gt; SRR825140     1  0.0000      0.984 1.000 0.000
#&gt; SRR825141     1  0.0672      0.983 0.992 0.008
#&gt; SRR825143     1  0.0000      0.984 1.000 0.000
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-1-a').click(function(){
  $('#tab-CV-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-2'>
<p><a id='tab-CV-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR547973     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR547968     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR547980     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR545058     3  0.0000      0.951 0.000 0.000 1.000
#&gt; SRR546225     3  0.7104      0.385 0.032 0.360 0.608
#&gt; SRR546226     1  0.0000      0.990 1.000 0.000 0.000
#&gt; SRR546227     1  0.0237      0.988 0.996 0.000 0.004
#&gt; SRR546228     3  0.0000      0.951 0.000 0.000 1.000
#&gt; SRR546229     3  0.0000      0.951 0.000 0.000 1.000
#&gt; SRR546230     1  0.0000      0.990 1.000 0.000 0.000
#&gt; SRR546231     3  0.5859      0.461 0.344 0.000 0.656
#&gt; SRR546232     1  0.0237      0.988 0.996 0.000 0.004
#&gt; SRR546233     1  0.0000      0.990 1.000 0.000 0.000
#&gt; SRR546234     3  0.1163      0.927 0.028 0.000 0.972
#&gt; SRR546235     3  0.0000      0.951 0.000 0.000 1.000
#&gt; SRR546236     3  0.0000      0.951 0.000 0.000 1.000
#&gt; SRR546237     1  0.0237      0.988 0.996 0.000 0.004
#&gt; SRR546238     3  0.0000      0.951 0.000 0.000 1.000
#&gt; SRR546239     1  0.0237      0.988 0.996 0.000 0.004
#&gt; SRR546240     1  0.3619      0.834 0.864 0.000 0.136
#&gt; SRR547969     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR547970     2  0.1163      0.967 0.028 0.972 0.000
#&gt; SRR547971     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR547972     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR547974     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR547976     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR547978     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR547979     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR547981     2  0.1163      0.967 0.028 0.972 0.000
#&gt; SRR547982     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR547983     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR547989     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR547990     2  0.3933      0.871 0.028 0.880 0.092
#&gt; SRR547991     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR547992     2  0.0000      0.990 0.000 1.000 0.000
#&gt; SRR801424     1  0.0000      0.990 1.000 0.000 0.000
#&gt; SRR801425     3  0.0000      0.951 0.000 0.000 1.000
#&gt; SRR801426     3  0.0000      0.951 0.000 0.000 1.000
#&gt; SRR801427     1  0.0000      0.990 1.000 0.000 0.000
#&gt; SRR801428     1  0.0000      0.990 1.000 0.000 0.000
#&gt; SRR801429     3  0.0000      0.951 0.000 0.000 1.000
#&gt; SRR801430     1  0.0000      0.990 1.000 0.000 0.000
#&gt; SRR801431     3  0.0000      0.951 0.000 0.000 1.000
#&gt; SRR801432     3  0.0000      0.951 0.000 0.000 1.000
#&gt; SRR801433     1  0.0000      0.990 1.000 0.000 0.000
#&gt; SRR825135     3  0.0000      0.951 0.000 0.000 1.000
#&gt; SRR825136     1  0.0000      0.990 1.000 0.000 0.000
#&gt; SRR825137     3  0.0000      0.951 0.000 0.000 1.000
#&gt; SRR825139     1  0.0000      0.990 1.000 0.000 0.000
#&gt; SRR825140     1  0.0237      0.988 0.996 0.000 0.004
#&gt; SRR825141     3  0.0000      0.951 0.000 0.000 1.000
#&gt; SRR825143     1  0.0000      0.990 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-2-a').click(function(){
  $('#tab-CV-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-3'>
<p><a id='tab-CV-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     4  0.4989      0.837 0.000 0.472 0.000 0.528
#&gt; SRR547973     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR547968     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR547980     4  0.4994      0.826 0.000 0.480 0.000 0.520
#&gt; SRR545058     3  0.0000      0.940 0.000 0.000 1.000 0.000
#&gt; SRR546225     3  0.6166      0.607 0.012 0.064 0.660 0.264
#&gt; SRR546226     1  0.0000      0.901 1.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.2704      0.853 0.876 0.000 0.000 0.124
#&gt; SRR546228     3  0.0000      0.940 0.000 0.000 1.000 0.000
#&gt; SRR546229     3  0.0000      0.940 0.000 0.000 1.000 0.000
#&gt; SRR546230     1  0.0000      0.901 1.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.5962      0.718 0.128 0.000 0.692 0.180
#&gt; SRR546232     1  0.2868      0.847 0.864 0.000 0.000 0.136
#&gt; SRR546233     1  0.0000      0.901 1.000 0.000 0.000 0.000
#&gt; SRR546234     3  0.2589      0.889 0.000 0.000 0.884 0.116
#&gt; SRR546235     3  0.1474      0.927 0.000 0.000 0.948 0.052
#&gt; SRR546236     3  0.2760      0.885 0.000 0.000 0.872 0.128
#&gt; SRR546237     1  0.3074      0.838 0.848 0.000 0.000 0.152
#&gt; SRR546238     3  0.0000      0.940 0.000 0.000 1.000 0.000
#&gt; SRR546239     1  0.3764      0.859 0.784 0.000 0.000 0.216
#&gt; SRR546240     1  0.3881      0.812 0.812 0.000 0.016 0.172
#&gt; SRR547969     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR547970     4  0.4857      0.789 0.000 0.284 0.016 0.700
#&gt; SRR547971     4  0.4898      0.858 0.000 0.416 0.000 0.584
#&gt; SRR547972     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR547974     4  0.4992      0.832 0.000 0.476 0.000 0.524
#&gt; SRR547976     2  0.0336      0.989 0.000 0.992 0.000 0.008
#&gt; SRR547978     4  0.4948      0.859 0.000 0.440 0.000 0.560
#&gt; SRR547979     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR547981     4  0.4844      0.801 0.000 0.300 0.012 0.688
#&gt; SRR547982     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR547983     2  0.0336      0.989 0.000 0.992 0.000 0.008
#&gt; SRR547989     2  0.0336      0.989 0.000 0.992 0.000 0.008
#&gt; SRR547990     4  0.4831      0.784 0.000 0.280 0.016 0.704
#&gt; SRR547991     4  0.4948      0.859 0.000 0.440 0.000 0.560
#&gt; SRR547992     2  0.0000      0.995 0.000 1.000 0.000 0.000
#&gt; SRR801424     1  0.3764      0.851 0.784 0.000 0.000 0.216
#&gt; SRR801425     3  0.0817      0.936 0.000 0.000 0.976 0.024
#&gt; SRR801426     3  0.0188      0.940 0.000 0.000 0.996 0.004
#&gt; SRR801427     1  0.0000      0.901 1.000 0.000 0.000 0.000
#&gt; SRR801428     1  0.3764      0.851 0.784 0.000 0.000 0.216
#&gt; SRR801429     3  0.0336      0.940 0.000 0.000 0.992 0.008
#&gt; SRR801430     1  0.3764      0.851 0.784 0.000 0.000 0.216
#&gt; SRR801431     3  0.0336      0.940 0.000 0.000 0.992 0.008
#&gt; SRR801432     3  0.0336      0.940 0.000 0.000 0.992 0.008
#&gt; SRR801433     1  0.3764      0.851 0.784 0.000 0.000 0.216
#&gt; SRR825135     3  0.0000      0.940 0.000 0.000 1.000 0.000
#&gt; SRR825136     1  0.0000      0.901 1.000 0.000 0.000 0.000
#&gt; SRR825137     3  0.1557      0.925 0.000 0.000 0.944 0.056
#&gt; SRR825139     1  0.3311      0.866 0.828 0.000 0.000 0.172
#&gt; SRR825140     1  0.0000      0.901 1.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.1637      0.925 0.000 0.000 0.940 0.060
#&gt; SRR825143     1  0.0000      0.901 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-3-a').click(function(){
  $('#tab-CV-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-4'>
<p><a id='tab-CV-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR547975     2  0.4290     0.3809 0.000 0.680 0.000 0.016 0.304
#&gt; SRR547973     2  0.0290     0.7565 0.000 0.992 0.000 0.000 0.008
#&gt; SRR547968     2  0.0162     0.7556 0.000 0.996 0.000 0.000 0.004
#&gt; SRR547980     2  0.4206     0.4112 0.000 0.696 0.000 0.016 0.288
#&gt; SRR545058     3  0.0290     0.8499 0.000 0.000 0.992 0.000 0.008
#&gt; SRR546225     3  0.6378     0.4804 0.032 0.068 0.508 0.004 0.388
#&gt; SRR546226     1  0.4242     0.5600 0.572 0.000 0.000 0.428 0.000
#&gt; SRR546227     1  0.1251     0.5126 0.956 0.000 0.000 0.036 0.008
#&gt; SRR546228     3  0.0290     0.8499 0.000 0.000 0.992 0.000 0.008
#&gt; SRR546229     3  0.3386     0.8374 0.000 0.000 0.832 0.040 0.128
#&gt; SRR546230     1  0.4242     0.5600 0.572 0.000 0.000 0.428 0.000
#&gt; SRR546231     3  0.5996     0.4764 0.432 0.000 0.468 0.004 0.096
#&gt; SRR546232     1  0.1082     0.5100 0.964 0.000 0.000 0.028 0.008
#&gt; SRR546233     1  0.4242     0.5600 0.572 0.000 0.000 0.428 0.000
#&gt; SRR546234     3  0.4491     0.7145 0.012 0.000 0.648 0.004 0.336
#&gt; SRR546235     3  0.0955     0.8484 0.028 0.000 0.968 0.000 0.004
#&gt; SRR546236     3  0.3488     0.8261 0.024 0.000 0.808 0.000 0.168
#&gt; SRR546237     1  0.0693     0.5007 0.980 0.000 0.000 0.012 0.008
#&gt; SRR546238     3  0.1608     0.8363 0.000 0.000 0.928 0.000 0.072
#&gt; SRR546239     1  0.4030     0.2413 0.648 0.000 0.000 0.352 0.000
#&gt; SRR546240     1  0.2450     0.4052 0.896 0.000 0.076 0.000 0.028
#&gt; SRR547969     2  0.0162     0.7580 0.000 0.996 0.000 0.000 0.004
#&gt; SRR547970     5  0.4887     0.7678 0.032 0.296 0.004 0.004 0.664
#&gt; SRR547971     2  0.5080    -0.3076 0.012 0.524 0.000 0.016 0.448
#&gt; SRR547972     2  0.0000     0.7573 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547974     2  0.4184     0.4212 0.000 0.700 0.000 0.016 0.284
#&gt; SRR547976     2  0.0510     0.7560 0.000 0.984 0.000 0.000 0.016
#&gt; SRR547978     2  0.4482     0.2416 0.000 0.636 0.000 0.016 0.348
#&gt; SRR547979     2  0.0162     0.7579 0.000 0.996 0.000 0.000 0.004
#&gt; SRR547981     5  0.5155     0.5252 0.032 0.428 0.004 0.000 0.536
#&gt; SRR547982     2  0.0162     0.7556 0.000 0.996 0.000 0.000 0.004
#&gt; SRR547983     2  0.0404     0.7569 0.000 0.988 0.000 0.000 0.012
#&gt; SRR547989     2  0.0404     0.7569 0.000 0.988 0.000 0.000 0.012
#&gt; SRR547990     5  0.4413     0.7224 0.032 0.220 0.004 0.004 0.740
#&gt; SRR547991     2  0.4482     0.2416 0.000 0.636 0.000 0.016 0.348
#&gt; SRR547992     2  0.0162     0.7556 0.000 0.996 0.000 0.000 0.004
#&gt; SRR801424     4  0.1410     0.8516 0.060 0.000 0.000 0.940 0.000
#&gt; SRR801425     3  0.2917     0.8493 0.024 0.000 0.888 0.040 0.048
#&gt; SRR801426     3  0.3339     0.8383 0.000 0.000 0.836 0.040 0.124
#&gt; SRR801427     1  0.4242     0.5600 0.572 0.000 0.000 0.428 0.000
#&gt; SRR801428     4  0.1410     0.8516 0.060 0.000 0.000 0.940 0.000
#&gt; SRR801429     3  0.4451     0.7934 0.000 0.000 0.712 0.040 0.248
#&gt; SRR801430     4  0.1410     0.8516 0.060 0.000 0.000 0.940 0.000
#&gt; SRR801431     3  0.4161     0.8095 0.000 0.000 0.752 0.040 0.208
#&gt; SRR801432     3  0.4313     0.7976 0.000 0.000 0.732 0.040 0.228
#&gt; SRR801433     4  0.1410     0.8516 0.060 0.000 0.000 0.940 0.000
#&gt; SRR825135     3  0.0703     0.8522 0.000 0.000 0.976 0.000 0.024
#&gt; SRR825136     1  0.4242     0.5600 0.572 0.000 0.000 0.428 0.000
#&gt; SRR825137     3  0.1251     0.8479 0.036 0.000 0.956 0.000 0.008
#&gt; SRR825139     4  0.4114    -0.0611 0.376 0.000 0.000 0.624 0.000
#&gt; SRR825140     1  0.4235     0.5597 0.576 0.000 0.000 0.424 0.000
#&gt; SRR825141     3  0.1522     0.8488 0.044 0.000 0.944 0.000 0.012
#&gt; SRR825143     1  0.4242     0.5600 0.572 0.000 0.000 0.428 0.000
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-4-a').click(function(){
  $('#tab-CV-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-mclust-get-classes-5'>
<p><a id='tab-CV-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR547975     5  0.3868    -0.1554 0.000 0.492 0.000 0.000 0.508 0.000
#&gt; SRR547973     2  0.0547     0.6457 0.000 0.980 0.000 0.000 0.020 0.000
#&gt; SRR547968     2  0.0000     0.6443 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547980     2  0.3843     0.1743 0.000 0.548 0.000 0.000 0.452 0.000
#&gt; SRR545058     3  0.1387     0.7877 0.000 0.000 0.932 0.068 0.000 0.000
#&gt; SRR546225     3  0.5544     0.5937 0.004 0.076 0.676 0.104 0.140 0.000
#&gt; SRR546226     1  0.0000     0.6324 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.5059     0.4472 0.556 0.000 0.004 0.044 0.012 0.384
#&gt; SRR546228     3  0.1204     0.7901 0.000 0.000 0.944 0.056 0.000 0.000
#&gt; SRR546229     4  0.2854     0.8445 0.000 0.000 0.208 0.792 0.000 0.000
#&gt; SRR546230     1  0.0000     0.6324 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.6516     0.3141 0.004 0.000 0.480 0.148 0.048 0.320
#&gt; SRR546232     1  0.4969     0.4489 0.560 0.000 0.004 0.044 0.008 0.384
#&gt; SRR546233     1  0.1049     0.6088 0.960 0.000 0.000 0.000 0.008 0.032
#&gt; SRR546234     3  0.4143     0.6702 0.000 0.000 0.736 0.180 0.084 0.000
#&gt; SRR546235     3  0.0146     0.7887 0.000 0.000 0.996 0.004 0.000 0.000
#&gt; SRR546236     3  0.2783     0.7343 0.000 0.000 0.836 0.148 0.016 0.000
#&gt; SRR546237     1  0.5141     0.4447 0.552 0.000 0.004 0.044 0.016 0.384
#&gt; SRR546238     3  0.1387     0.7877 0.000 0.000 0.932 0.068 0.000 0.000
#&gt; SRR546239     6  0.4204    -0.3935 0.448 0.000 0.000 0.008 0.004 0.540
#&gt; SRR546240     1  0.7091     0.3468 0.440 0.000 0.080 0.044 0.080 0.356
#&gt; SRR547969     2  0.2378     0.7139 0.000 0.848 0.000 0.000 0.152 0.000
#&gt; SRR547970     5  0.3669     0.6821 0.000 0.140 0.016 0.044 0.800 0.000
#&gt; SRR547971     5  0.3795     0.3747 0.000 0.364 0.004 0.000 0.632 0.000
#&gt; SRR547972     2  0.2378     0.7139 0.000 0.848 0.000 0.000 0.152 0.000
#&gt; SRR547974     2  0.3810     0.2407 0.000 0.572 0.000 0.000 0.428 0.000
#&gt; SRR547976     2  0.2631     0.7066 0.000 0.820 0.000 0.000 0.180 0.000
#&gt; SRR547978     2  0.3867     0.0311 0.000 0.512 0.000 0.000 0.488 0.000
#&gt; SRR547979     2  0.2527     0.7117 0.000 0.832 0.000 0.000 0.168 0.000
#&gt; SRR547981     5  0.4023     0.6804 0.000 0.180 0.016 0.044 0.760 0.000
#&gt; SRR547982     2  0.0000     0.6443 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547983     2  0.2527     0.7099 0.000 0.832 0.000 0.000 0.168 0.000
#&gt; SRR547989     2  0.2491     0.7112 0.000 0.836 0.000 0.000 0.164 0.000
#&gt; SRR547990     5  0.3875     0.6585 0.000 0.124 0.028 0.052 0.796 0.000
#&gt; SRR547991     2  0.3864     0.0679 0.000 0.520 0.000 0.000 0.480 0.000
#&gt; SRR547992     2  0.0000     0.6443 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR801424     6  0.3717     0.7590 0.384 0.000 0.000 0.000 0.000 0.616
#&gt; SRR801425     3  0.3727     0.1718 0.000 0.000 0.612 0.388 0.000 0.000
#&gt; SRR801426     4  0.2969     0.8244 0.000 0.000 0.224 0.776 0.000 0.000
#&gt; SRR801427     1  0.1196     0.6006 0.952 0.000 0.000 0.000 0.008 0.040
#&gt; SRR801428     6  0.3852     0.7570 0.384 0.000 0.000 0.000 0.004 0.612
#&gt; SRR801429     4  0.1556     0.8900 0.000 0.000 0.080 0.920 0.000 0.000
#&gt; SRR801430     6  0.3717     0.7590 0.384 0.000 0.000 0.000 0.000 0.616
#&gt; SRR801431     4  0.2092     0.8905 0.000 0.000 0.124 0.876 0.000 0.000
#&gt; SRR801432     4  0.1714     0.8931 0.000 0.000 0.092 0.908 0.000 0.000
#&gt; SRR801433     6  0.3717     0.7590 0.384 0.000 0.000 0.000 0.000 0.616
#&gt; SRR825135     3  0.1863     0.7795 0.000 0.000 0.896 0.104 0.000 0.000
#&gt; SRR825136     1  0.1049     0.6088 0.960 0.000 0.000 0.000 0.008 0.032
#&gt; SRR825137     3  0.0146     0.7887 0.000 0.000 0.996 0.004 0.000 0.000
#&gt; SRR825139     1  0.3240     0.1226 0.752 0.000 0.000 0.000 0.004 0.244
#&gt; SRR825140     1  0.0436     0.6304 0.988 0.000 0.000 0.004 0.004 0.004
#&gt; SRR825141     3  0.1584     0.7779 0.000 0.000 0.928 0.064 0.008 0.000
#&gt; SRR825143     1  0.0000     0.6324 1.000 0.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-mclust-get-classes-5-a').click(function(){
  $('#tab-CV-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-CV-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-signatures'>
<ul>
<li><a href='#tab-CV-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-1-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-1"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-2-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-2"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-3-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-3"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-4-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-4"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-5-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-mclust-signature_compare](figure_cola/CV-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-CV-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-mclust-collect-classes](figure_cola/CV-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### CV:NMF*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["CV", "NMF"]
# you can also extract it by
# res = res_list["CV:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'CV' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk CV-NMF-collect-plots](figure_cola/CV-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk CV-NMF-select-partition-number](figure_cola/CV-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.4795 0.521   0.521
#> 3 3 0.729           0.971       0.914         0.3645 0.803   0.621
#> 4 4 0.935           0.981       0.969         0.1307 0.928   0.778
#> 5 5 0.742           0.755       0.853         0.0787 0.925   0.713
#> 6 6 0.773           0.609       0.803         0.0442 0.970   0.848
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-CV-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-classes'>
<ul>
<li><a href='#tab-CV-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-CV-NMF-get-classes-1'>
<p><a id='tab-CV-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1 p2
#&gt; SRR547975     2       0          1  0  1
#&gt; SRR547973     2       0          1  0  1
#&gt; SRR547968     2       0          1  0  1
#&gt; SRR547980     2       0          1  0  1
#&gt; SRR545058     1       0          1  1  0
#&gt; SRR546225     2       0          1  0  1
#&gt; SRR546226     1       0          1  1  0
#&gt; SRR546227     1       0          1  1  0
#&gt; SRR546228     1       0          1  1  0
#&gt; SRR546229     1       0          1  1  0
#&gt; SRR546230     1       0          1  1  0
#&gt; SRR546231     1       0          1  1  0
#&gt; SRR546232     1       0          1  1  0
#&gt; SRR546233     1       0          1  1  0
#&gt; SRR546234     1       0          1  1  0
#&gt; SRR546235     1       0          1  1  0
#&gt; SRR546236     1       0          1  1  0
#&gt; SRR546237     1       0          1  1  0
#&gt; SRR546238     1       0          1  1  0
#&gt; SRR546239     1       0          1  1  0
#&gt; SRR546240     1       0          1  1  0
#&gt; SRR547969     2       0          1  0  1
#&gt; SRR547970     2       0          1  0  1
#&gt; SRR547971     2       0          1  0  1
#&gt; SRR547972     2       0          1  0  1
#&gt; SRR547974     2       0          1  0  1
#&gt; SRR547976     2       0          1  0  1
#&gt; SRR547978     2       0          1  0  1
#&gt; SRR547979     2       0          1  0  1
#&gt; SRR547981     2       0          1  0  1
#&gt; SRR547982     2       0          1  0  1
#&gt; SRR547983     2       0          1  0  1
#&gt; SRR547989     2       0          1  0  1
#&gt; SRR547990     2       0          1  0  1
#&gt; SRR547991     2       0          1  0  1
#&gt; SRR547992     2       0          1  0  1
#&gt; SRR801424     1       0          1  1  0
#&gt; SRR801425     1       0          1  1  0
#&gt; SRR801426     1       0          1  1  0
#&gt; SRR801427     1       0          1  1  0
#&gt; SRR801428     1       0          1  1  0
#&gt; SRR801429     1       0          1  1  0
#&gt; SRR801430     1       0          1  1  0
#&gt; SRR801431     1       0          1  1  0
#&gt; SRR801432     1       0          1  1  0
#&gt; SRR801433     1       0          1  1  0
#&gt; SRR825135     1       0          1  1  0
#&gt; SRR825136     1       0          1  1  0
#&gt; SRR825137     1       0          1  1  0
#&gt; SRR825139     1       0          1  1  0
#&gt; SRR825140     1       0          1  1  0
#&gt; SRR825141     1       0          1  1  0
#&gt; SRR825143     1       0          1  1  0
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-1-a').click(function(){
  $('#tab-CV-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-2'>
<p><a id='tab-CV-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     2  0.4235      0.934 0.176 0.824 0.000
#&gt; SRR547973     2  0.0000      0.925 0.000 1.000 0.000
#&gt; SRR547968     2  0.0424      0.921 0.008 0.992 0.000
#&gt; SRR547980     2  0.4235      0.934 0.176 0.824 0.000
#&gt; SRR545058     3  0.0000      0.998 0.000 0.000 1.000
#&gt; SRR546225     2  0.4235      0.934 0.176 0.824 0.000
#&gt; SRR546226     1  0.4346      0.996 0.816 0.000 0.184
#&gt; SRR546227     1  0.4346      0.996 0.816 0.000 0.184
#&gt; SRR546228     3  0.0000      0.998 0.000 0.000 1.000
#&gt; SRR546229     3  0.0000      0.998 0.000 0.000 1.000
#&gt; SRR546230     1  0.4346      0.996 0.816 0.000 0.184
#&gt; SRR546231     3  0.0000      0.998 0.000 0.000 1.000
#&gt; SRR546232     1  0.4346      0.996 0.816 0.000 0.184
#&gt; SRR546233     1  0.4346      0.996 0.816 0.000 0.184
#&gt; SRR546234     3  0.0000      0.998 0.000 0.000 1.000
#&gt; SRR546235     3  0.0000      0.998 0.000 0.000 1.000
#&gt; SRR546236     3  0.0000      0.998 0.000 0.000 1.000
#&gt; SRR546237     1  0.4346      0.996 0.816 0.000 0.184
#&gt; SRR546238     3  0.0000      0.998 0.000 0.000 1.000
#&gt; SRR546239     1  0.4235      0.994 0.824 0.000 0.176
#&gt; SRR546240     1  0.4346      0.996 0.816 0.000 0.184
#&gt; SRR547969     2  0.0000      0.925 0.000 1.000 0.000
#&gt; SRR547970     2  0.4235      0.934 0.176 0.824 0.000
#&gt; SRR547971     2  0.4235      0.934 0.176 0.824 0.000
#&gt; SRR547972     2  0.0000      0.925 0.000 1.000 0.000
#&gt; SRR547974     2  0.4235      0.934 0.176 0.824 0.000
#&gt; SRR547976     2  0.3192      0.933 0.112 0.888 0.000
#&gt; SRR547978     2  0.4235      0.934 0.176 0.824 0.000
#&gt; SRR547979     2  0.0000      0.925 0.000 1.000 0.000
#&gt; SRR547981     2  0.4235      0.934 0.176 0.824 0.000
#&gt; SRR547982     2  0.0000      0.925 0.000 1.000 0.000
#&gt; SRR547983     2  0.0000      0.925 0.000 1.000 0.000
#&gt; SRR547989     2  0.0000      0.925 0.000 1.000 0.000
#&gt; SRR547990     2  0.4235      0.934 0.176 0.824 0.000
#&gt; SRR547991     2  0.4235      0.934 0.176 0.824 0.000
#&gt; SRR547992     2  0.0000      0.925 0.000 1.000 0.000
#&gt; SRR801424     1  0.4235      0.994 0.824 0.000 0.176
#&gt; SRR801425     3  0.0000      0.998 0.000 0.000 1.000
#&gt; SRR801426     3  0.0000      0.998 0.000 0.000 1.000
#&gt; SRR801427     1  0.4346      0.996 0.816 0.000 0.184
#&gt; SRR801428     1  0.4235      0.994 0.824 0.000 0.176
#&gt; SRR801429     3  0.0592      0.985 0.012 0.000 0.988
#&gt; SRR801430     1  0.4235      0.994 0.824 0.000 0.176
#&gt; SRR801431     3  0.0000      0.998 0.000 0.000 1.000
#&gt; SRR801432     3  0.0424      0.990 0.008 0.000 0.992
#&gt; SRR801433     1  0.4235      0.994 0.824 0.000 0.176
#&gt; SRR825135     3  0.0000      0.998 0.000 0.000 1.000
#&gt; SRR825136     1  0.4235      0.994 0.824 0.000 0.176
#&gt; SRR825137     3  0.0000      0.998 0.000 0.000 1.000
#&gt; SRR825139     1  0.4235      0.994 0.824 0.000 0.176
#&gt; SRR825140     1  0.4346      0.996 0.816 0.000 0.184
#&gt; SRR825141     3  0.0000      0.998 0.000 0.000 1.000
#&gt; SRR825143     1  0.4346      0.996 0.816 0.000 0.184
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-2-a').click(function(){
  $('#tab-CV-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-3'>
<p><a id='tab-CV-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR547973     4  0.3123      0.968 0.000 0.156 0.000 0.844
#&gt; SRR547968     4  0.0336      0.833 0.000 0.008 0.000 0.992
#&gt; SRR547980     2  0.0336      0.978 0.000 0.992 0.008 0.000
#&gt; SRR545058     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR546225     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR546226     1  0.0000      0.995 1.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000      0.995 1.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR546229     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR546230     1  0.0000      0.995 1.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR546232     1  0.0000      0.995 1.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.0000      0.995 1.000 0.000 0.000 0.000
#&gt; SRR546234     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR546235     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR546236     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR546237     1  0.0000      0.995 1.000 0.000 0.000 0.000
#&gt; SRR546238     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR546239     1  0.0188      0.993 0.996 0.000 0.000 0.004
#&gt; SRR546240     1  0.0000      0.995 1.000 0.000 0.000 0.000
#&gt; SRR547969     4  0.3074      0.969 0.000 0.152 0.000 0.848
#&gt; SRR547970     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR547971     2  0.0188      0.979 0.000 0.996 0.000 0.004
#&gt; SRR547972     4  0.3074      0.969 0.000 0.152 0.000 0.848
#&gt; SRR547974     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR547976     2  0.2814      0.818 0.000 0.868 0.000 0.132
#&gt; SRR547978     2  0.0524      0.977 0.000 0.988 0.008 0.004
#&gt; SRR547979     4  0.3172      0.967 0.000 0.160 0.000 0.840
#&gt; SRR547981     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR547982     4  0.2760      0.950 0.000 0.128 0.000 0.872
#&gt; SRR547983     4  0.3450      0.965 0.000 0.156 0.008 0.836
#&gt; SRR547989     4  0.3450      0.965 0.000 0.156 0.008 0.836
#&gt; SRR547990     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR547991     2  0.0524      0.977 0.000 0.988 0.008 0.004
#&gt; SRR547992     4  0.3123      0.968 0.000 0.156 0.000 0.844
#&gt; SRR801424     1  0.0188      0.993 0.996 0.000 0.000 0.004
#&gt; SRR801425     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR801426     3  0.0524      0.997 0.008 0.000 0.988 0.004
#&gt; SRR801427     1  0.0000      0.995 1.000 0.000 0.000 0.000
#&gt; SRR801428     1  0.0188      0.993 0.996 0.000 0.000 0.004
#&gt; SRR801429     3  0.0524      0.997 0.008 0.000 0.988 0.004
#&gt; SRR801430     1  0.1867      0.939 0.928 0.000 0.000 0.072
#&gt; SRR801431     3  0.0524      0.997 0.008 0.000 0.988 0.004
#&gt; SRR801432     3  0.0524      0.993 0.004 0.000 0.988 0.008
#&gt; SRR801433     1  0.0188      0.993 0.996 0.000 0.000 0.004
#&gt; SRR825135     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR825136     1  0.0000      0.995 1.000 0.000 0.000 0.000
#&gt; SRR825137     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR825139     1  0.0000      0.995 1.000 0.000 0.000 0.000
#&gt; SRR825140     1  0.0000      0.995 1.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0336      0.999 0.008 0.000 0.992 0.000
#&gt; SRR825143     1  0.0000      0.995 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-3-a').click(function(){
  $('#tab-CV-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-4'>
<p><a id='tab-CV-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR547975     5  0.0000      0.895 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547973     2  0.2669      0.934 0.000 0.876 0.000 0.020 0.104
#&gt; SRR547968     2  0.0609      0.853 0.000 0.980 0.000 0.020 0.000
#&gt; SRR547980     5  0.2408      0.863 0.000 0.016 0.000 0.092 0.892
#&gt; SRR545058     3  0.0404      0.884 0.000 0.000 0.988 0.012 0.000
#&gt; SRR546225     5  0.6448      0.568 0.000 0.080 0.148 0.132 0.640
#&gt; SRR546226     1  0.0404      0.822 0.988 0.000 0.000 0.012 0.000
#&gt; SRR546227     1  0.0880      0.818 0.968 0.000 0.000 0.032 0.000
#&gt; SRR546228     3  0.0290      0.884 0.000 0.000 0.992 0.008 0.000
#&gt; SRR546229     3  0.2280      0.833 0.000 0.000 0.880 0.120 0.000
#&gt; SRR546230     1  0.0000      0.823 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.3003      0.750 0.000 0.000 0.812 0.188 0.000
#&gt; SRR546232     1  0.2753      0.757 0.856 0.000 0.008 0.136 0.000
#&gt; SRR546233     1  0.0162      0.821 0.996 0.000 0.000 0.004 0.000
#&gt; SRR546234     3  0.1671      0.850 0.000 0.000 0.924 0.076 0.000
#&gt; SRR546235     3  0.0404      0.882 0.000 0.000 0.988 0.012 0.000
#&gt; SRR546236     3  0.2516      0.799 0.000 0.000 0.860 0.140 0.000
#&gt; SRR546237     1  0.3513      0.713 0.800 0.000 0.020 0.180 0.000
#&gt; SRR546238     3  0.1792      0.857 0.000 0.000 0.916 0.084 0.000
#&gt; SRR546239     1  0.5022      0.450 0.620 0.048 0.000 0.332 0.000
#&gt; SRR546240     1  0.4333      0.661 0.752 0.000 0.060 0.188 0.000
#&gt; SRR547969     2  0.3691      0.917 0.000 0.820 0.000 0.076 0.104
#&gt; SRR547970     5  0.0000      0.895 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547971     5  0.0510      0.893 0.000 0.000 0.000 0.016 0.984
#&gt; SRR547972     2  0.2074      0.938 0.000 0.896 0.000 0.000 0.104
#&gt; SRR547974     5  0.0000      0.895 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547976     5  0.3730      0.551 0.000 0.288 0.000 0.000 0.712
#&gt; SRR547978     5  0.2677      0.853 0.000 0.016 0.000 0.112 0.872
#&gt; SRR547979     2  0.2233      0.938 0.000 0.892 0.000 0.004 0.104
#&gt; SRR547981     5  0.0000      0.895 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547982     2  0.1671      0.928 0.000 0.924 0.000 0.000 0.076
#&gt; SRR547983     2  0.4171      0.898 0.000 0.784 0.000 0.112 0.104
#&gt; SRR547989     2  0.4171      0.898 0.000 0.784 0.000 0.112 0.104
#&gt; SRR547990     5  0.0000      0.895 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547991     5  0.2677      0.853 0.000 0.016 0.000 0.112 0.872
#&gt; SRR547992     2  0.2358      0.937 0.000 0.888 0.000 0.008 0.104
#&gt; SRR801424     4  0.4227      0.468 0.420 0.000 0.000 0.580 0.000
#&gt; SRR801425     3  0.2561      0.811 0.000 0.000 0.856 0.144 0.000
#&gt; SRR801426     3  0.4045      0.440 0.000 0.000 0.644 0.356 0.000
#&gt; SRR801427     1  0.1908      0.750 0.908 0.000 0.000 0.092 0.000
#&gt; SRR801428     4  0.4227      0.468 0.420 0.000 0.000 0.580 0.000
#&gt; SRR801429     4  0.4118      0.404 0.004 0.000 0.336 0.660 0.000
#&gt; SRR801430     4  0.5204      0.491 0.368 0.052 0.000 0.580 0.000
#&gt; SRR801431     4  0.4219      0.205 0.000 0.000 0.416 0.584 0.000
#&gt; SRR801432     4  0.4047      0.424 0.000 0.004 0.320 0.676 0.000
#&gt; SRR801433     4  0.4565      0.478 0.408 0.012 0.000 0.580 0.000
#&gt; SRR825135     3  0.0880      0.880 0.000 0.000 0.968 0.032 0.000
#&gt; SRR825136     1  0.2424      0.712 0.868 0.000 0.000 0.132 0.000
#&gt; SRR825137     3  0.0963      0.876 0.000 0.000 0.964 0.036 0.000
#&gt; SRR825139     1  0.4313      0.193 0.636 0.008 0.000 0.356 0.000
#&gt; SRR825140     1  0.0000      0.823 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0609      0.884 0.000 0.000 0.980 0.020 0.000
#&gt; SRR825143     1  0.0000      0.823 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-4-a').click(function(){
  $('#tab-CV-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-CV-NMF-get-classes-5'>
<p><a id='tab-CV-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR547975     5  0.0146    0.79190 0.000 0.000 0.000 0.004 0.996 0.000
#&gt; SRR547973     2  0.1991    0.86874 0.000 0.920 0.000 0.012 0.044 0.024
#&gt; SRR547968     2  0.0891    0.84623 0.000 0.968 0.000 0.008 0.000 0.024
#&gt; SRR547980     5  0.4078    0.69306 0.000 0.016 0.000 0.008 0.676 0.300
#&gt; SRR545058     3  0.2378    0.57877 0.000 0.000 0.848 0.000 0.000 0.152
#&gt; SRR546225     6  0.6697    0.36492 0.000 0.068 0.144 0.004 0.308 0.476
#&gt; SRR546226     1  0.0000    0.80626 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0146    0.80524 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; SRR546228     3  0.1075    0.64485 0.000 0.000 0.952 0.000 0.000 0.048
#&gt; SRR546229     3  0.2790    0.62095 0.000 0.000 0.840 0.140 0.000 0.020
#&gt; SRR546230     1  0.0260    0.80712 0.992 0.000 0.000 0.008 0.000 0.000
#&gt; SRR546231     6  0.4214    0.00776 0.004 0.000 0.460 0.008 0.000 0.528
#&gt; SRR546232     1  0.1265    0.78398 0.948 0.000 0.000 0.008 0.000 0.044
#&gt; SRR546233     1  0.0260    0.80712 0.992 0.000 0.000 0.008 0.000 0.000
#&gt; SRR546234     3  0.3737   -0.07246 0.000 0.000 0.608 0.000 0.000 0.392
#&gt; SRR546235     3  0.2597    0.54355 0.000 0.000 0.824 0.000 0.000 0.176
#&gt; SRR546236     3  0.3797   -0.19938 0.000 0.000 0.580 0.000 0.000 0.420
#&gt; SRR546237     1  0.3692    0.64071 0.736 0.000 0.012 0.008 0.000 0.244
#&gt; SRR546238     3  0.2163    0.64613 0.000 0.000 0.892 0.092 0.000 0.016
#&gt; SRR546239     4  0.5217    0.06787 0.392 0.000 0.000 0.512 0.000 0.096
#&gt; SRR546240     1  0.5173    0.14039 0.476 0.000 0.064 0.008 0.000 0.452
#&gt; SRR547969     2  0.2851    0.84601 0.000 0.868 0.000 0.016 0.036 0.080
#&gt; SRR547970     5  0.0547    0.78759 0.000 0.000 0.000 0.000 0.980 0.020
#&gt; SRR547971     5  0.1957    0.77532 0.000 0.000 0.000 0.000 0.888 0.112
#&gt; SRR547972     2  0.1010    0.87947 0.000 0.960 0.000 0.000 0.036 0.004
#&gt; SRR547974     5  0.0405    0.79220 0.000 0.000 0.000 0.004 0.988 0.008
#&gt; SRR547976     5  0.3789    0.47441 0.000 0.332 0.000 0.008 0.660 0.000
#&gt; SRR547978     5  0.4719    0.62334 0.000 0.024 0.000 0.016 0.564 0.396
#&gt; SRR547979     2  0.1268    0.87966 0.000 0.952 0.000 0.004 0.036 0.008
#&gt; SRR547981     5  0.0458    0.78925 0.000 0.000 0.000 0.000 0.984 0.016
#&gt; SRR547982     2  0.0935    0.87921 0.000 0.964 0.000 0.004 0.032 0.000
#&gt; SRR547983     2  0.4864    0.63814 0.000 0.600 0.000 0.020 0.036 0.344
#&gt; SRR547989     2  0.4864    0.63814 0.000 0.600 0.000 0.020 0.036 0.344
#&gt; SRR547990     5  0.0458    0.78925 0.000 0.000 0.000 0.000 0.984 0.016
#&gt; SRR547991     5  0.4719    0.62334 0.000 0.024 0.000 0.016 0.564 0.396
#&gt; SRR547992     2  0.1382    0.87749 0.000 0.948 0.000 0.008 0.036 0.008
#&gt; SRR801424     4  0.2520    0.70143 0.152 0.004 0.000 0.844 0.000 0.000
#&gt; SRR801425     3  0.3053    0.59989 0.000 0.000 0.812 0.168 0.000 0.020
#&gt; SRR801426     3  0.4199    0.29480 0.000 0.000 0.600 0.380 0.000 0.020
#&gt; SRR801427     1  0.1765    0.73121 0.904 0.000 0.000 0.096 0.000 0.000
#&gt; SRR801428     4  0.2527    0.69178 0.168 0.000 0.000 0.832 0.000 0.000
#&gt; SRR801429     4  0.4105    0.30054 0.000 0.000 0.348 0.632 0.000 0.020
#&gt; SRR801430     4  0.2826    0.70140 0.128 0.028 0.000 0.844 0.000 0.000
#&gt; SRR801431     4  0.3103    0.55183 0.000 0.000 0.208 0.784 0.000 0.008
#&gt; SRR801432     4  0.3245    0.58040 0.000 0.004 0.184 0.796 0.000 0.016
#&gt; SRR801433     4  0.2595    0.69706 0.160 0.004 0.000 0.836 0.000 0.000
#&gt; SRR825135     3  0.1616    0.66335 0.000 0.000 0.932 0.048 0.000 0.020
#&gt; SRR825136     1  0.4205    0.20754 0.564 0.016 0.000 0.420 0.000 0.000
#&gt; SRR825137     3  0.2738    0.55435 0.000 0.000 0.820 0.004 0.000 0.176
#&gt; SRR825139     1  0.3930    0.21831 0.576 0.004 0.000 0.420 0.000 0.000
#&gt; SRR825140     1  0.0260    0.80712 0.992 0.000 0.000 0.008 0.000 0.000
#&gt; SRR825141     3  0.1297    0.66357 0.000 0.000 0.948 0.040 0.000 0.012
#&gt; SRR825143     1  0.0260    0.80712 0.992 0.000 0.000 0.008 0.000 0.000
</code></pre>

<script>
$('#tab-CV-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-CV-NMF-get-classes-5-a').click(function(){
  $('#tab-CV-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-CV-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-CV-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-CV-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-CV-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-CV-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-CV-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-CV-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-CV-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-CV-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-signatures'>
<ul>
<li><a href='#tab-CV-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-1-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-1"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-2-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-2"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-3-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-3"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-4-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-4"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-5-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-CV-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-CV-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-CV-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk CV-NMF-signature_compare](figure_cola/CV-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-CV-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-CV-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-CV-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-CV-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-CV-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-CV-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-CV-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-CV-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk CV-NMF-collect-classes](figure_cola/CV-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:hclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "hclust"]
# you can also extract it by
# res = res_list["MAD:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-hclust-collect-plots](figure_cola/MAD-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-hclust-select-partition-number](figure_cola/MAD-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.986       0.994         0.4725 0.531   0.531
#> 3 3 0.653           0.823       0.865         0.3582 0.826   0.672
#> 4 4 0.722           0.738       0.847         0.1199 0.936   0.821
#> 5 5 0.688           0.440       0.760         0.0661 0.838   0.539
#> 6 6 0.836           0.758       0.858         0.0689 0.889   0.581
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-classes'>
<ul>
<li><a href='#tab-MAD-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-hclust-get-classes-1'>
<p><a id='tab-MAD-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR547975     2  0.0000      1.000 0.000 1.000
#&gt; SRR547973     2  0.0000      1.000 0.000 1.000
#&gt; SRR547968     2  0.0000      1.000 0.000 1.000
#&gt; SRR547980     2  0.0000      1.000 0.000 1.000
#&gt; SRR545058     1  0.0000      0.990 1.000 0.000
#&gt; SRR546225     1  0.8861      0.564 0.696 0.304
#&gt; SRR546226     1  0.0000      0.990 1.000 0.000
#&gt; SRR546227     1  0.0000      0.990 1.000 0.000
#&gt; SRR546228     1  0.0000      0.990 1.000 0.000
#&gt; SRR546229     1  0.0000      0.990 1.000 0.000
#&gt; SRR546230     1  0.0000      0.990 1.000 0.000
#&gt; SRR546231     1  0.0000      0.990 1.000 0.000
#&gt; SRR546232     1  0.0000      0.990 1.000 0.000
#&gt; SRR546233     1  0.0000      0.990 1.000 0.000
#&gt; SRR546234     1  0.0672      0.983 0.992 0.008
#&gt; SRR546235     1  0.0000      0.990 1.000 0.000
#&gt; SRR546236     1  0.0000      0.990 1.000 0.000
#&gt; SRR546237     1  0.0000      0.990 1.000 0.000
#&gt; SRR546238     1  0.0000      0.990 1.000 0.000
#&gt; SRR546239     1  0.0000      0.990 1.000 0.000
#&gt; SRR546240     1  0.0000      0.990 1.000 0.000
#&gt; SRR547969     2  0.0000      1.000 0.000 1.000
#&gt; SRR547970     2  0.0000      1.000 0.000 1.000
#&gt; SRR547971     2  0.0000      1.000 0.000 1.000
#&gt; SRR547972     2  0.0000      1.000 0.000 1.000
#&gt; SRR547974     2  0.0000      1.000 0.000 1.000
#&gt; SRR547976     2  0.0000      1.000 0.000 1.000
#&gt; SRR547978     2  0.0000      1.000 0.000 1.000
#&gt; SRR547979     2  0.0000      1.000 0.000 1.000
#&gt; SRR547981     2  0.0000      1.000 0.000 1.000
#&gt; SRR547982     2  0.0000      1.000 0.000 1.000
#&gt; SRR547983     2  0.0000      1.000 0.000 1.000
#&gt; SRR547989     2  0.0000      1.000 0.000 1.000
#&gt; SRR547990     2  0.0000      1.000 0.000 1.000
#&gt; SRR547991     2  0.0000      1.000 0.000 1.000
#&gt; SRR547992     2  0.0000      1.000 0.000 1.000
#&gt; SRR801424     1  0.0000      0.990 1.000 0.000
#&gt; SRR801425     1  0.0000      0.990 1.000 0.000
#&gt; SRR801426     1  0.0000      0.990 1.000 0.000
#&gt; SRR801427     1  0.0000      0.990 1.000 0.000
#&gt; SRR801428     1  0.0000      0.990 1.000 0.000
#&gt; SRR801429     1  0.0000      0.990 1.000 0.000
#&gt; SRR801430     1  0.0000      0.990 1.000 0.000
#&gt; SRR801431     1  0.0000      0.990 1.000 0.000
#&gt; SRR801432     1  0.0000      0.990 1.000 0.000
#&gt; SRR801433     1  0.0000      0.990 1.000 0.000
#&gt; SRR825135     1  0.0000      0.990 1.000 0.000
#&gt; SRR825136     1  0.0000      0.990 1.000 0.000
#&gt; SRR825137     1  0.0000      0.990 1.000 0.000
#&gt; SRR825139     1  0.0000      0.990 1.000 0.000
#&gt; SRR825140     1  0.0000      0.990 1.000 0.000
#&gt; SRR825141     1  0.0000      0.990 1.000 0.000
#&gt; SRR825143     1  0.0000      0.990 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-1-a').click(function(){
  $('#tab-MAD-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-2'>
<p><a id='tab-MAD-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     2   0.129      0.956 0.000 0.968 0.032
#&gt; SRR547973     2   0.254      0.947 0.000 0.920 0.080
#&gt; SRR547968     2   0.254      0.947 0.000 0.920 0.080
#&gt; SRR547980     2   0.129      0.956 0.000 0.968 0.032
#&gt; SRR545058     1   0.533      0.741 0.728 0.000 0.272
#&gt; SRR546225     1   0.683      0.491 0.692 0.260 0.048
#&gt; SRR546226     1   0.000      0.782 1.000 0.000 0.000
#&gt; SRR546227     1   0.000      0.782 1.000 0.000 0.000
#&gt; SRR546228     1   0.533      0.741 0.728 0.000 0.272
#&gt; SRR546229     1   0.550      0.724 0.708 0.000 0.292
#&gt; SRR546230     1   0.000      0.782 1.000 0.000 0.000
#&gt; SRR546231     1   0.522      0.744 0.740 0.000 0.260
#&gt; SRR546232     1   0.000      0.782 1.000 0.000 0.000
#&gt; SRR546233     1   0.000      0.782 1.000 0.000 0.000
#&gt; SRR546234     1   0.460      0.758 0.796 0.000 0.204
#&gt; SRR546235     1   0.543      0.732 0.716 0.000 0.284
#&gt; SRR546236     1   0.533      0.741 0.728 0.000 0.272
#&gt; SRR546237     1   0.000      0.782 1.000 0.000 0.000
#&gt; SRR546238     1   0.550      0.724 0.708 0.000 0.292
#&gt; SRR546239     1   0.000      0.782 1.000 0.000 0.000
#&gt; SRR546240     1   0.000      0.782 1.000 0.000 0.000
#&gt; SRR547969     2   0.254      0.947 0.000 0.920 0.080
#&gt; SRR547970     2   0.129      0.956 0.000 0.968 0.032
#&gt; SRR547971     2   0.129      0.956 0.000 0.968 0.032
#&gt; SRR547972     2   0.254      0.947 0.000 0.920 0.080
#&gt; SRR547974     2   0.116      0.956 0.000 0.972 0.028
#&gt; SRR547976     2   0.254      0.947 0.000 0.920 0.080
#&gt; SRR547978     2   0.129      0.956 0.000 0.968 0.032
#&gt; SRR547979     2   0.254      0.947 0.000 0.920 0.080
#&gt; SRR547981     2   0.129      0.956 0.000 0.968 0.032
#&gt; SRR547982     2   0.254      0.947 0.000 0.920 0.080
#&gt; SRR547983     2   0.000      0.956 0.000 1.000 0.000
#&gt; SRR547989     2   0.000      0.956 0.000 1.000 0.000
#&gt; SRR547990     2   0.129      0.956 0.000 0.968 0.032
#&gt; SRR547991     2   0.129      0.956 0.000 0.968 0.032
#&gt; SRR547992     2   0.254      0.947 0.000 0.920 0.080
#&gt; SRR801424     3   0.615      0.747 0.408 0.000 0.592
#&gt; SRR801425     3   0.327      0.759 0.116 0.000 0.884
#&gt; SRR801426     3   0.327      0.759 0.116 0.000 0.884
#&gt; SRR801427     3   0.615      0.747 0.408 0.000 0.592
#&gt; SRR801428     3   0.615      0.747 0.408 0.000 0.592
#&gt; SRR801429     3   0.327      0.759 0.116 0.000 0.884
#&gt; SRR801430     3   0.615      0.747 0.408 0.000 0.592
#&gt; SRR801431     3   0.327      0.759 0.116 0.000 0.884
#&gt; SRR801432     3   0.327      0.759 0.116 0.000 0.884
#&gt; SRR801433     3   0.615      0.747 0.408 0.000 0.592
#&gt; SRR825135     1   0.553      0.723 0.704 0.000 0.296
#&gt; SRR825136     1   0.000      0.782 1.000 0.000 0.000
#&gt; SRR825137     1   0.543      0.732 0.716 0.000 0.284
#&gt; SRR825139     1   0.000      0.782 1.000 0.000 0.000
#&gt; SRR825140     1   0.000      0.782 1.000 0.000 0.000
#&gt; SRR825141     1   0.543      0.732 0.716 0.000 0.284
#&gt; SRR825143     1   0.000      0.782 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-2-a').click(function(){
  $('#tab-MAD-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-3'>
<p><a id='tab-MAD-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     2  0.0000     0.8768 0.000 1.000 0.000 0.000
#&gt; SRR547973     3  0.0000     0.9247 0.000 0.000 1.000 0.000
#&gt; SRR547968     3  0.0000     0.9247 0.000 0.000 1.000 0.000
#&gt; SRR547980     2  0.2589     0.8806 0.000 0.884 0.116 0.000
#&gt; SRR545058     1  0.0707     0.6640 0.980 0.000 0.000 0.020
#&gt; SRR546225     1  0.7937     0.5624 0.600 0.176 0.128 0.096
#&gt; SRR546226     1  0.4866     0.7173 0.596 0.000 0.000 0.404
#&gt; SRR546227     1  0.4866     0.7173 0.596 0.000 0.000 0.404
#&gt; SRR546228     1  0.0707     0.6640 0.980 0.000 0.000 0.020
#&gt; SRR546229     1  0.0336     0.6473 0.992 0.000 0.000 0.008
#&gt; SRR546230     1  0.4866     0.7173 0.596 0.000 0.000 0.404
#&gt; SRR546231     1  0.1118     0.6681 0.964 0.000 0.000 0.036
#&gt; SRR546232     1  0.4866     0.7173 0.596 0.000 0.000 0.404
#&gt; SRR546233     1  0.4866     0.7173 0.596 0.000 0.000 0.404
#&gt; SRR546234     1  0.2611     0.6810 0.896 0.000 0.008 0.096
#&gt; SRR546235     1  0.0469     0.6578 0.988 0.000 0.000 0.012
#&gt; SRR546236     1  0.0707     0.6640 0.980 0.000 0.000 0.020
#&gt; SRR546237     1  0.4866     0.7173 0.596 0.000 0.000 0.404
#&gt; SRR546238     1  0.0336     0.6473 0.992 0.000 0.000 0.008
#&gt; SRR546239     1  0.4866     0.7173 0.596 0.000 0.000 0.404
#&gt; SRR546240     1  0.4866     0.7173 0.596 0.000 0.000 0.404
#&gt; SRR547969     3  0.4941    -0.0274 0.000 0.436 0.564 0.000
#&gt; SRR547970     2  0.0000     0.8768 0.000 1.000 0.000 0.000
#&gt; SRR547971     2  0.3266     0.8698 0.000 0.832 0.168 0.000
#&gt; SRR547972     3  0.0000     0.9247 0.000 0.000 1.000 0.000
#&gt; SRR547974     2  0.0336     0.8762 0.000 0.992 0.008 0.000
#&gt; SRR547976     3  0.0000     0.9247 0.000 0.000 1.000 0.000
#&gt; SRR547978     2  0.3266     0.8698 0.000 0.832 0.168 0.000
#&gt; SRR547979     3  0.0000     0.9247 0.000 0.000 1.000 0.000
#&gt; SRR547981     2  0.0000     0.8768 0.000 1.000 0.000 0.000
#&gt; SRR547982     3  0.0000     0.9247 0.000 0.000 1.000 0.000
#&gt; SRR547983     2  0.3801     0.8240 0.000 0.780 0.220 0.000
#&gt; SRR547989     2  0.3801     0.8240 0.000 0.780 0.220 0.000
#&gt; SRR547990     2  0.0000     0.8768 0.000 1.000 0.000 0.000
#&gt; SRR547991     2  0.3266     0.8698 0.000 0.832 0.168 0.000
#&gt; SRR547992     3  0.0000     0.9247 0.000 0.000 1.000 0.000
#&gt; SRR801424     4  0.0188     0.6606 0.004 0.000 0.000 0.996
#&gt; SRR801425     4  0.4855     0.6786 0.400 0.000 0.000 0.600
#&gt; SRR801426     4  0.4855     0.6786 0.400 0.000 0.000 0.600
#&gt; SRR801427     4  0.0188     0.6606 0.004 0.000 0.000 0.996
#&gt; SRR801428     4  0.0188     0.6606 0.004 0.000 0.000 0.996
#&gt; SRR801429     4  0.4855     0.6786 0.400 0.000 0.000 0.600
#&gt; SRR801430     4  0.0188     0.6606 0.004 0.000 0.000 0.996
#&gt; SRR801431     4  0.4855     0.6786 0.400 0.000 0.000 0.600
#&gt; SRR801432     4  0.4855     0.6786 0.400 0.000 0.000 0.600
#&gt; SRR801433     4  0.0188     0.6606 0.004 0.000 0.000 0.996
#&gt; SRR825135     1  0.0188     0.6455 0.996 0.000 0.000 0.004
#&gt; SRR825136     1  0.4866     0.7173 0.596 0.000 0.000 0.404
#&gt; SRR825137     1  0.0469     0.6578 0.988 0.000 0.000 0.012
#&gt; SRR825139     1  0.4866     0.7173 0.596 0.000 0.000 0.404
#&gt; SRR825140     1  0.4866     0.7173 0.596 0.000 0.000 0.404
#&gt; SRR825141     1  0.0469     0.6578 0.988 0.000 0.000 0.012
#&gt; SRR825143     1  0.4866     0.7173 0.596 0.000 0.000 0.404
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-3-a').click(function(){
  $('#tab-MAD-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-4'>
<p><a id='tab-MAD-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR547975     5  0.3895      0.666 0.320 0.000 0.000 0.000 0.680
#&gt; SRR547973     2  0.0000      0.926 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547968     2  0.0000      0.926 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547980     5  0.2389      0.733 0.004 0.116 0.000 0.000 0.880
#&gt; SRR545058     3  0.0703      0.684 0.024 0.000 0.976 0.000 0.000
#&gt; SRR546225     1  0.6159      0.000 0.552 0.120 0.320 0.004 0.004
#&gt; SRR546226     4  0.6790     -0.171 0.300 0.000 0.316 0.384 0.000
#&gt; SRR546227     3  0.4341      0.186 0.004 0.000 0.592 0.404 0.000
#&gt; SRR546228     3  0.0703      0.684 0.024 0.000 0.976 0.000 0.000
#&gt; SRR546229     3  0.0162      0.687 0.000 0.000 0.996 0.004 0.000
#&gt; SRR546230     4  0.6790     -0.171 0.300 0.000 0.316 0.384 0.000
#&gt; SRR546231     3  0.1082      0.675 0.008 0.000 0.964 0.028 0.000
#&gt; SRR546232     4  0.6752     -0.161 0.280 0.000 0.316 0.404 0.000
#&gt; SRR546233     4  0.6752     -0.161 0.280 0.000 0.316 0.404 0.000
#&gt; SRR546234     3  0.4276     -0.309 0.380 0.000 0.616 0.004 0.000
#&gt; SRR546235     3  0.0451      0.691 0.008 0.000 0.988 0.004 0.000
#&gt; SRR546236     3  0.0703      0.684 0.024 0.000 0.976 0.000 0.000
#&gt; SRR546237     3  0.4446      0.191 0.008 0.000 0.592 0.400 0.000
#&gt; SRR546238     3  0.0162      0.687 0.000 0.000 0.996 0.004 0.000
#&gt; SRR546239     3  0.4446      0.191 0.008 0.000 0.592 0.400 0.000
#&gt; SRR546240     3  0.4446      0.191 0.008 0.000 0.592 0.400 0.000
#&gt; SRR547969     2  0.4256      0.130 0.000 0.564 0.000 0.000 0.436
#&gt; SRR547970     5  0.3895      0.666 0.320 0.000 0.000 0.000 0.680
#&gt; SRR547971     5  0.2813      0.724 0.000 0.168 0.000 0.000 0.832
#&gt; SRR547972     2  0.0000      0.926 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547974     5  0.4165      0.664 0.320 0.008 0.000 0.000 0.672
#&gt; SRR547976     2  0.0000      0.926 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547978     5  0.2813      0.724 0.000 0.168 0.000 0.000 0.832
#&gt; SRR547979     2  0.0000      0.926 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547981     5  0.3895      0.666 0.320 0.000 0.000 0.000 0.680
#&gt; SRR547982     2  0.0000      0.926 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547983     5  0.3274      0.680 0.000 0.220 0.000 0.000 0.780
#&gt; SRR547989     5  0.3274      0.680 0.000 0.220 0.000 0.000 0.780
#&gt; SRR547990     5  0.2852      0.651 0.172 0.000 0.000 0.000 0.828
#&gt; SRR547991     5  0.2813      0.724 0.000 0.168 0.000 0.000 0.832
#&gt; SRR547992     2  0.0000      0.926 0.000 1.000 0.000 0.000 0.000
#&gt; SRR801424     4  0.0162      0.365 0.000 0.000 0.004 0.996 0.000
#&gt; SRR801425     4  0.5673      0.269 0.112 0.000 0.292 0.596 0.000
#&gt; SRR801426     4  0.5655      0.273 0.112 0.000 0.288 0.600 0.000
#&gt; SRR801427     4  0.0162      0.365 0.000 0.000 0.004 0.996 0.000
#&gt; SRR801428     4  0.0162      0.365 0.000 0.000 0.004 0.996 0.000
#&gt; SRR801429     4  0.5655      0.273 0.112 0.000 0.288 0.600 0.000
#&gt; SRR801430     4  0.0162      0.365 0.000 0.000 0.004 0.996 0.000
#&gt; SRR801431     4  0.5655      0.273 0.112 0.000 0.288 0.600 0.000
#&gt; SRR801432     4  0.5655      0.273 0.112 0.000 0.288 0.600 0.000
#&gt; SRR801433     4  0.0162      0.365 0.000 0.000 0.004 0.996 0.000
#&gt; SRR825135     3  0.0324      0.687 0.004 0.000 0.992 0.004 0.000
#&gt; SRR825136     4  0.6790     -0.171 0.300 0.000 0.316 0.384 0.000
#&gt; SRR825137     3  0.0451      0.691 0.008 0.000 0.988 0.004 0.000
#&gt; SRR825139     4  0.6790     -0.171 0.300 0.000 0.316 0.384 0.000
#&gt; SRR825140     4  0.6790     -0.171 0.300 0.000 0.316 0.384 0.000
#&gt; SRR825141     3  0.0324      0.691 0.004 0.000 0.992 0.004 0.000
#&gt; SRR825143     4  0.6790     -0.171 0.300 0.000 0.316 0.384 0.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-4-a').click(function(){
  $('#tab-MAD-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-hclust-get-classes-5'>
<p><a id='tab-MAD-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR547975     6  0.3578      0.956 0.000 0.000 0.000 0.000 0.340 0.660
#&gt; SRR547973     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547968     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547980     5  0.1531      0.706 0.000 0.004 0.000 0.000 0.928 0.068
#&gt; SRR545058     3  0.1821      0.795 0.040 0.000 0.928 0.008 0.000 0.024
#&gt; SRR546225     1  0.5619      0.437 0.580 0.100 0.020 0.000 0.004 0.296
#&gt; SRR546226     1  0.0000      0.868 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     3  0.4310      0.436 0.396 0.000 0.580 0.024 0.000 0.000
#&gt; SRR546228     3  0.1821      0.795 0.040 0.000 0.928 0.008 0.000 0.024
#&gt; SRR546229     3  0.0458      0.808 0.000 0.000 0.984 0.016 0.000 0.000
#&gt; SRR546230     1  0.0000      0.868 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.1088      0.804 0.016 0.000 0.960 0.024 0.000 0.000
#&gt; SRR546232     1  0.0777      0.849 0.972 0.000 0.004 0.024 0.000 0.000
#&gt; SRR546233     1  0.0632      0.851 0.976 0.000 0.000 0.024 0.000 0.000
#&gt; SRR546234     1  0.5323      0.351 0.580 0.000 0.312 0.004 0.004 0.100
#&gt; SRR546235     3  0.0458      0.811 0.016 0.000 0.984 0.000 0.000 0.000
#&gt; SRR546236     3  0.1821      0.795 0.040 0.000 0.928 0.008 0.000 0.024
#&gt; SRR546237     3  0.4301      0.442 0.392 0.000 0.584 0.024 0.000 0.000
#&gt; SRR546238     3  0.0363      0.808 0.000 0.000 0.988 0.012 0.000 0.000
#&gt; SRR546239     3  0.4301      0.442 0.392 0.000 0.584 0.024 0.000 0.000
#&gt; SRR546240     3  0.4301      0.442 0.392 0.000 0.584 0.024 0.000 0.000
#&gt; SRR547969     5  0.3756      0.322 0.000 0.400 0.000 0.000 0.600 0.000
#&gt; SRR547970     6  0.3578      0.956 0.000 0.000 0.000 0.000 0.340 0.660
#&gt; SRR547971     5  0.0146      0.778 0.000 0.004 0.000 0.000 0.996 0.000
#&gt; SRR547972     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547974     6  0.3861      0.946 0.000 0.008 0.000 0.000 0.352 0.640
#&gt; SRR547976     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547978     5  0.0146      0.778 0.000 0.004 0.000 0.000 0.996 0.000
#&gt; SRR547979     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547981     6  0.3578      0.920 0.000 0.000 0.000 0.000 0.340 0.660
#&gt; SRR547982     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547983     5  0.1204      0.771 0.000 0.056 0.000 0.000 0.944 0.000
#&gt; SRR547989     5  0.1204      0.771 0.000 0.056 0.000 0.000 0.944 0.000
#&gt; SRR547990     5  0.3727      0.373 0.000 0.000 0.000 0.000 0.612 0.388
#&gt; SRR547991     5  0.0146      0.778 0.000 0.004 0.000 0.000 0.996 0.000
#&gt; SRR547992     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR801424     4  0.3934      0.631 0.376 0.000 0.008 0.616 0.000 0.000
#&gt; SRR801425     4  0.0713      0.690 0.000 0.000 0.028 0.972 0.000 0.000
#&gt; SRR801426     4  0.0632      0.693 0.000 0.000 0.024 0.976 0.000 0.000
#&gt; SRR801427     4  0.3934      0.631 0.376 0.000 0.008 0.616 0.000 0.000
#&gt; SRR801428     4  0.3934      0.631 0.376 0.000 0.008 0.616 0.000 0.000
#&gt; SRR801429     4  0.0632      0.693 0.000 0.000 0.024 0.976 0.000 0.000
#&gt; SRR801430     4  0.3934      0.631 0.376 0.000 0.008 0.616 0.000 0.000
#&gt; SRR801431     4  0.0632      0.693 0.000 0.000 0.024 0.976 0.000 0.000
#&gt; SRR801432     4  0.0632      0.693 0.000 0.000 0.024 0.976 0.000 0.000
#&gt; SRR801433     4  0.3934      0.631 0.376 0.000 0.008 0.616 0.000 0.000
#&gt; SRR825135     3  0.0508      0.808 0.000 0.000 0.984 0.012 0.000 0.004
#&gt; SRR825136     1  0.0000      0.868 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR825137     3  0.0458      0.811 0.016 0.000 0.984 0.000 0.000 0.000
#&gt; SRR825139     1  0.0000      0.868 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR825140     1  0.0000      0.868 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0146      0.811 0.004 0.000 0.996 0.000 0.000 0.000
#&gt; SRR825143     1  0.0000      0.868 1.000 0.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-hclust-get-classes-5-a').click(function(){
  $('#tab-MAD-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-signatures'>
<ul>
<li><a href='#tab-MAD-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-1-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-1"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-2-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-2"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-3-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-3"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-4-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-4"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-5-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-hclust-signature_compare](figure_cola/MAD-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-hclust-collect-classes](figure_cola/MAD-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:kmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "kmeans"]
# you can also extract it by
# res = res_list["MAD:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-kmeans-collect-plots](figure_cola/MAD-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-kmeans-select-partition-number](figure_cola/MAD-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.980       0.992         0.4754 0.521   0.521
#> 3 3 0.640           0.460       0.681         0.3343 0.849   0.721
#> 4 4 0.682           0.824       0.775         0.1386 0.791   0.520
#> 5 5 0.695           0.855       0.789         0.0731 0.935   0.741
#> 6 6 0.766           0.827       0.820         0.0477 1.000   1.000
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-classes'>
<ul>
<li><a href='#tab-MAD-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-kmeans-get-classes-1'>
<p><a id='tab-MAD-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette  p1  p2
#&gt; SRR547975     2   0.000      0.979 0.0 1.0
#&gt; SRR547973     2   0.000      0.979 0.0 1.0
#&gt; SRR547968     2   0.000      0.979 0.0 1.0
#&gt; SRR547980     2   0.000      0.979 0.0 1.0
#&gt; SRR545058     1   0.000      1.000 1.0 0.0
#&gt; SRR546225     2   0.971      0.333 0.4 0.6
#&gt; SRR546226     1   0.000      1.000 1.0 0.0
#&gt; SRR546227     1   0.000      1.000 1.0 0.0
#&gt; SRR546228     1   0.000      1.000 1.0 0.0
#&gt; SRR546229     1   0.000      1.000 1.0 0.0
#&gt; SRR546230     1   0.000      1.000 1.0 0.0
#&gt; SRR546231     1   0.000      1.000 1.0 0.0
#&gt; SRR546232     1   0.000      1.000 1.0 0.0
#&gt; SRR546233     1   0.000      1.000 1.0 0.0
#&gt; SRR546234     1   0.000      1.000 1.0 0.0
#&gt; SRR546235     1   0.000      1.000 1.0 0.0
#&gt; SRR546236     1   0.000      1.000 1.0 0.0
#&gt; SRR546237     1   0.000      1.000 1.0 0.0
#&gt; SRR546238     1   0.000      1.000 1.0 0.0
#&gt; SRR546239     1   0.000      1.000 1.0 0.0
#&gt; SRR546240     1   0.000      1.000 1.0 0.0
#&gt; SRR547969     2   0.000      0.979 0.0 1.0
#&gt; SRR547970     2   0.000      0.979 0.0 1.0
#&gt; SRR547971     2   0.000      0.979 0.0 1.0
#&gt; SRR547972     2   0.000      0.979 0.0 1.0
#&gt; SRR547974     2   0.000      0.979 0.0 1.0
#&gt; SRR547976     2   0.000      0.979 0.0 1.0
#&gt; SRR547978     2   0.000      0.979 0.0 1.0
#&gt; SRR547979     2   0.000      0.979 0.0 1.0
#&gt; SRR547981     2   0.000      0.979 0.0 1.0
#&gt; SRR547982     2   0.000      0.979 0.0 1.0
#&gt; SRR547983     2   0.000      0.979 0.0 1.0
#&gt; SRR547989     2   0.000      0.979 0.0 1.0
#&gt; SRR547990     2   0.000      0.979 0.0 1.0
#&gt; SRR547991     2   0.000      0.979 0.0 1.0
#&gt; SRR547992     2   0.000      0.979 0.0 1.0
#&gt; SRR801424     1   0.000      1.000 1.0 0.0
#&gt; SRR801425     1   0.000      1.000 1.0 0.0
#&gt; SRR801426     1   0.000      1.000 1.0 0.0
#&gt; SRR801427     1   0.000      1.000 1.0 0.0
#&gt; SRR801428     1   0.000      1.000 1.0 0.0
#&gt; SRR801429     1   0.000      1.000 1.0 0.0
#&gt; SRR801430     1   0.000      1.000 1.0 0.0
#&gt; SRR801431     1   0.000      1.000 1.0 0.0
#&gt; SRR801432     1   0.000      1.000 1.0 0.0
#&gt; SRR801433     1   0.000      1.000 1.0 0.0
#&gt; SRR825135     1   0.000      1.000 1.0 0.0
#&gt; SRR825136     1   0.000      1.000 1.0 0.0
#&gt; SRR825137     1   0.000      1.000 1.0 0.0
#&gt; SRR825139     1   0.000      1.000 1.0 0.0
#&gt; SRR825140     1   0.000      1.000 1.0 0.0
#&gt; SRR825141     1   0.000      1.000 1.0 0.0
#&gt; SRR825143     1   0.000      1.000 1.0 0.0
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-1-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-2'>
<p><a id='tab-MAD-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     2   0.000     0.8932 0.000 1.000 0.000
#&gt; SRR547973     2   0.518     0.8931 0.256 0.744 0.000
#&gt; SRR547968     2   0.518     0.8931 0.256 0.744 0.000
#&gt; SRR547980     2   0.000     0.8932 0.000 1.000 0.000
#&gt; SRR545058     3   0.000     0.4159 0.000 0.000 1.000
#&gt; SRR546225     3   0.963    -0.1611 0.204 0.396 0.400
#&gt; SRR546226     3   0.631    -0.1529 0.496 0.000 0.504
#&gt; SRR546227     3   0.631    -0.1529 0.496 0.000 0.504
#&gt; SRR546228     3   0.000     0.4159 0.000 0.000 1.000
#&gt; SRR546229     3   0.175     0.3702 0.048 0.000 0.952
#&gt; SRR546230     3   0.631    -0.1529 0.496 0.000 0.504
#&gt; SRR546231     3   0.000     0.4159 0.000 0.000 1.000
#&gt; SRR546232     3   0.631    -0.1529 0.496 0.000 0.504
#&gt; SRR546233     1   0.631    -0.0022 0.508 0.000 0.492
#&gt; SRR546234     3   0.288     0.3490 0.096 0.000 0.904
#&gt; SRR546235     3   0.000     0.4159 0.000 0.000 1.000
#&gt; SRR546236     3   0.000     0.4159 0.000 0.000 1.000
#&gt; SRR546237     3   0.631    -0.1529 0.496 0.000 0.504
#&gt; SRR546238     3   0.000     0.4159 0.000 0.000 1.000
#&gt; SRR546239     3   0.631    -0.1529 0.496 0.000 0.504
#&gt; SRR546240     3   0.631    -0.1529 0.496 0.000 0.504
#&gt; SRR547969     2   0.518     0.8931 0.256 0.744 0.000
#&gt; SRR547970     2   0.000     0.8932 0.000 1.000 0.000
#&gt; SRR547971     2   0.000     0.8932 0.000 1.000 0.000
#&gt; SRR547972     2   0.518     0.8931 0.256 0.744 0.000
#&gt; SRR547974     2   0.000     0.8932 0.000 1.000 0.000
#&gt; SRR547976     2   0.518     0.8931 0.256 0.744 0.000
#&gt; SRR547978     2   0.000     0.8932 0.000 1.000 0.000
#&gt; SRR547979     2   0.518     0.8931 0.256 0.744 0.000
#&gt; SRR547981     2   0.000     0.8932 0.000 1.000 0.000
#&gt; SRR547982     2   0.518     0.8931 0.256 0.744 0.000
#&gt; SRR547983     2   0.440     0.8983 0.188 0.812 0.000
#&gt; SRR547989     2   0.440     0.8983 0.188 0.812 0.000
#&gt; SRR547990     2   0.000     0.8932 0.000 1.000 0.000
#&gt; SRR547991     2   0.000     0.8932 0.000 1.000 0.000
#&gt; SRR547992     2   0.518     0.8931 0.256 0.744 0.000
#&gt; SRR801424     1   0.604     0.8254 0.620 0.000 0.380
#&gt; SRR801425     3   0.510     0.1421 0.248 0.000 0.752
#&gt; SRR801426     3   0.510     0.1421 0.248 0.000 0.752
#&gt; SRR801427     1   0.590     0.7914 0.648 0.000 0.352
#&gt; SRR801428     1   0.604     0.8254 0.620 0.000 0.380
#&gt; SRR801429     3   0.510     0.1421 0.248 0.000 0.752
#&gt; SRR801430     1   0.604     0.8254 0.620 0.000 0.380
#&gt; SRR801431     3   0.510     0.1421 0.248 0.000 0.752
#&gt; SRR801432     3   0.510     0.1421 0.248 0.000 0.752
#&gt; SRR801433     1   0.604     0.8254 0.620 0.000 0.380
#&gt; SRR825135     3   0.000     0.4159 0.000 0.000 1.000
#&gt; SRR825136     3   0.631    -0.1529 0.496 0.000 0.504
#&gt; SRR825137     3   0.000     0.4159 0.000 0.000 1.000
#&gt; SRR825139     3   0.631    -0.1529 0.496 0.000 0.504
#&gt; SRR825140     3   0.631    -0.1529 0.496 0.000 0.504
#&gt; SRR825141     3   0.000     0.4159 0.000 0.000 1.000
#&gt; SRR825143     3   0.631    -0.1529 0.496 0.000 0.504
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-2-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-3'>
<p><a id='tab-MAD-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     2  0.1022      0.788 0.032 0.968 0.000 0.000
#&gt; SRR547973     2  0.6933      0.787 0.140 0.560 0.000 0.300
#&gt; SRR547968     2  0.6887      0.788 0.132 0.560 0.000 0.308
#&gt; SRR547980     2  0.0000      0.788 0.000 1.000 0.000 0.000
#&gt; SRR545058     3  0.0188      0.917 0.000 0.000 0.996 0.004
#&gt; SRR546225     3  0.8383      0.237 0.064 0.180 0.524 0.232
#&gt; SRR546226     1  0.4675      0.982 0.736 0.000 0.244 0.020
#&gt; SRR546227     1  0.3942      0.979 0.764 0.000 0.236 0.000
#&gt; SRR546228     3  0.0188      0.917 0.000 0.000 0.996 0.004
#&gt; SRR546229     3  0.1118      0.875 0.000 0.000 0.964 0.036
#&gt; SRR546230     1  0.4567      0.983 0.740 0.000 0.244 0.016
#&gt; SRR546231     3  0.1151      0.901 0.024 0.000 0.968 0.008
#&gt; SRR546232     1  0.3942      0.979 0.764 0.000 0.236 0.000
#&gt; SRR546233     1  0.4711      0.975 0.740 0.000 0.236 0.024
#&gt; SRR546234     3  0.1059      0.899 0.016 0.000 0.972 0.012
#&gt; SRR546235     3  0.0672      0.914 0.008 0.000 0.984 0.008
#&gt; SRR546236     3  0.0000      0.917 0.000 0.000 1.000 0.000
#&gt; SRR546237     1  0.3975      0.976 0.760 0.000 0.240 0.000
#&gt; SRR546238     3  0.0188      0.917 0.000 0.000 0.996 0.004
#&gt; SRR546239     1  0.3975      0.976 0.760 0.000 0.240 0.000
#&gt; SRR546240     1  0.4295      0.969 0.752 0.000 0.240 0.008
#&gt; SRR547969     2  0.6862      0.788 0.128 0.560 0.000 0.312
#&gt; SRR547970     2  0.1022      0.788 0.032 0.968 0.000 0.000
#&gt; SRR547971     2  0.0592      0.788 0.016 0.984 0.000 0.000
#&gt; SRR547972     2  0.6862      0.788 0.128 0.560 0.000 0.312
#&gt; SRR547974     2  0.1022      0.788 0.032 0.968 0.000 0.000
#&gt; SRR547976     2  0.6887      0.788 0.132 0.560 0.000 0.308
#&gt; SRR547978     2  0.0817      0.788 0.024 0.976 0.000 0.000
#&gt; SRR547979     2  0.6887      0.788 0.132 0.560 0.000 0.308
#&gt; SRR547981     2  0.1022      0.788 0.032 0.968 0.000 0.000
#&gt; SRR547982     2  0.6862      0.788 0.128 0.560 0.000 0.312
#&gt; SRR547983     2  0.5689      0.799 0.104 0.712 0.000 0.184
#&gt; SRR547989     2  0.5689      0.799 0.104 0.712 0.000 0.184
#&gt; SRR547990     2  0.1118      0.788 0.036 0.964 0.000 0.000
#&gt; SRR547991     2  0.0817      0.788 0.024 0.976 0.000 0.000
#&gt; SRR547992     2  0.6862      0.788 0.128 0.560 0.000 0.312
#&gt; SRR801424     4  0.6739      0.686 0.304 0.000 0.120 0.576
#&gt; SRR801425     4  0.4877      0.590 0.000 0.000 0.408 0.592
#&gt; SRR801426     4  0.4643      0.685 0.000 0.000 0.344 0.656
#&gt; SRR801427     4  0.6552      0.640 0.328 0.000 0.096 0.576
#&gt; SRR801428     4  0.6739      0.686 0.304 0.000 0.120 0.576
#&gt; SRR801429     4  0.4643      0.685 0.000 0.000 0.344 0.656
#&gt; SRR801430     4  0.6739      0.686 0.304 0.000 0.120 0.576
#&gt; SRR801431     4  0.4643      0.685 0.000 0.000 0.344 0.656
#&gt; SRR801432     4  0.4643      0.685 0.000 0.000 0.344 0.656
#&gt; SRR801433     4  0.6739      0.686 0.304 0.000 0.120 0.576
#&gt; SRR825135     3  0.0188      0.917 0.000 0.000 0.996 0.004
#&gt; SRR825136     1  0.4567      0.983 0.740 0.000 0.244 0.016
#&gt; SRR825137     3  0.0672      0.914 0.008 0.000 0.984 0.008
#&gt; SRR825139     1  0.4567      0.983 0.740 0.000 0.244 0.016
#&gt; SRR825140     1  0.4567      0.983 0.740 0.000 0.244 0.016
#&gt; SRR825141     3  0.0672      0.914 0.008 0.000 0.984 0.008
#&gt; SRR825143     1  0.4675      0.982 0.736 0.000 0.244 0.020
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-3-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-4'>
<p><a id='tab-MAD-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR547975     5  0.4415      0.929 0.000 0.388 0.008 0.000 0.604
#&gt; SRR547973     2  0.0898      0.888 0.000 0.972 0.020 0.008 0.000
#&gt; SRR547968     2  0.0162      0.907 0.000 0.996 0.004 0.000 0.000
#&gt; SRR547980     5  0.5834      0.917 0.000 0.388 0.032 0.040 0.540
#&gt; SRR545058     3  0.2856      0.904 0.104 0.000 0.872 0.008 0.016
#&gt; SRR546225     3  0.7135      0.402 0.072 0.320 0.528 0.036 0.044
#&gt; SRR546226     1  0.0324      0.967 0.992 0.000 0.000 0.004 0.004
#&gt; SRR546227     1  0.0579      0.964 0.984 0.000 0.000 0.008 0.008
#&gt; SRR546228     3  0.2856      0.904 0.104 0.000 0.872 0.008 0.016
#&gt; SRR546229     3  0.3986      0.877 0.080 0.000 0.828 0.044 0.048
#&gt; SRR546230     1  0.0162      0.968 0.996 0.000 0.000 0.000 0.004
#&gt; SRR546231     3  0.4911      0.842 0.104 0.000 0.740 0.012 0.144
#&gt; SRR546232     1  0.0693      0.965 0.980 0.000 0.000 0.008 0.012
#&gt; SRR546233     1  0.0324      0.964 0.992 0.000 0.000 0.004 0.004
#&gt; SRR546234     3  0.3707      0.884 0.116 0.000 0.828 0.012 0.044
#&gt; SRR546235     3  0.3727      0.896 0.104 0.000 0.824 0.004 0.068
#&gt; SRR546236     3  0.2392      0.906 0.104 0.000 0.888 0.004 0.004
#&gt; SRR546237     1  0.2077      0.925 0.908 0.000 0.000 0.008 0.084
#&gt; SRR546238     3  0.2828      0.904 0.104 0.000 0.872 0.004 0.020
#&gt; SRR546239     1  0.2017      0.928 0.912 0.000 0.000 0.008 0.080
#&gt; SRR546240     1  0.2621      0.897 0.876 0.000 0.004 0.008 0.112
#&gt; SRR547969     2  0.0000      0.908 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547970     5  0.4415      0.929 0.000 0.388 0.008 0.000 0.604
#&gt; SRR547971     5  0.6142      0.908 0.000 0.388 0.036 0.056 0.520
#&gt; SRR547972     2  0.0000      0.908 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547974     5  0.4299      0.928 0.000 0.388 0.000 0.004 0.608
#&gt; SRR547976     2  0.0162      0.907 0.000 0.996 0.004 0.000 0.000
#&gt; SRR547978     5  0.6533      0.889 0.000 0.388 0.048 0.072 0.492
#&gt; SRR547979     2  0.0162      0.907 0.000 0.996 0.004 0.000 0.000
#&gt; SRR547981     5  0.4517      0.925 0.000 0.388 0.000 0.012 0.600
#&gt; SRR547982     2  0.0000      0.908 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547983     2  0.4909      0.501 0.000 0.752 0.032 0.068 0.148
#&gt; SRR547989     2  0.4909      0.501 0.000 0.752 0.032 0.068 0.148
#&gt; SRR547990     5  0.4927      0.914 0.000 0.388 0.004 0.024 0.584
#&gt; SRR547991     5  0.6533      0.889 0.000 0.388 0.048 0.072 0.492
#&gt; SRR547992     2  0.0000      0.908 0.000 1.000 0.000 0.000 0.000
#&gt; SRR801424     4  0.6580      0.736 0.236 0.000 0.024 0.564 0.176
#&gt; SRR801425     4  0.4684      0.602 0.020 0.000 0.232 0.720 0.028
#&gt; SRR801426     4  0.3219      0.731 0.020 0.000 0.136 0.840 0.004
#&gt; SRR801427     4  0.6521      0.730 0.240 0.000 0.020 0.564 0.176
#&gt; SRR801428     4  0.6580      0.736 0.236 0.000 0.024 0.564 0.176
#&gt; SRR801429     4  0.3061      0.733 0.020 0.000 0.136 0.844 0.000
#&gt; SRR801430     4  0.6580      0.736 0.236 0.000 0.024 0.564 0.176
#&gt; SRR801431     4  0.3061      0.733 0.020 0.000 0.136 0.844 0.000
#&gt; SRR801432     4  0.3061      0.733 0.020 0.000 0.136 0.844 0.000
#&gt; SRR801433     4  0.6580      0.736 0.236 0.000 0.024 0.564 0.176
#&gt; SRR825135     3  0.2629      0.905 0.104 0.000 0.880 0.004 0.012
#&gt; SRR825136     1  0.0000      0.968 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825137     3  0.3727      0.896 0.104 0.000 0.824 0.004 0.068
#&gt; SRR825139     1  0.0000      0.968 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825140     1  0.0162      0.968 0.996 0.000 0.000 0.000 0.004
#&gt; SRR825141     3  0.3727      0.896 0.104 0.000 0.824 0.004 0.068
#&gt; SRR825143     1  0.0324      0.967 0.992 0.000 0.000 0.004 0.004
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-4-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-kmeans-get-classes-5'>
<p><a id='tab-MAD-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR547975     5  0.2806      0.883 0.000 0.000 0.008 0.008 0.840 0.144
#&gt; SRR547973     2  0.4203      0.865 0.000 0.752 0.016 0.008 0.188 0.036
#&gt; SRR547968     2  0.2948      0.898 0.000 0.804 0.000 0.000 0.188 0.008
#&gt; SRR547980     5  0.0291      0.867 0.000 0.000 0.004 0.000 0.992 0.004
#&gt; SRR545058     3  0.2819      0.848 0.060 0.032 0.876 0.000 0.000 0.032
#&gt; SRR546225     3  0.7008      0.438 0.028 0.256 0.516 0.024 0.024 0.152
#&gt; SRR546226     1  0.0436      0.941 0.988 0.004 0.004 0.000 0.000 0.004
#&gt; SRR546227     1  0.1088      0.933 0.960 0.024 0.000 0.000 0.000 0.016
#&gt; SRR546228     3  0.2819      0.848 0.060 0.032 0.876 0.000 0.000 0.032
#&gt; SRR546229     3  0.4631      0.825 0.044 0.044 0.772 0.036 0.000 0.104
#&gt; SRR546230     1  0.0436      0.941 0.988 0.004 0.004 0.000 0.000 0.004
#&gt; SRR546231     3  0.5621      0.740 0.064 0.084 0.632 0.000 0.000 0.220
#&gt; SRR546232     1  0.1168      0.935 0.956 0.028 0.000 0.000 0.000 0.016
#&gt; SRR546233     1  0.0405      0.937 0.988 0.000 0.004 0.008 0.000 0.000
#&gt; SRR546234     3  0.3847      0.824 0.068 0.056 0.812 0.000 0.000 0.064
#&gt; SRR546235     3  0.4090      0.839 0.064 0.040 0.788 0.000 0.000 0.108
#&gt; SRR546236     3  0.1524      0.858 0.060 0.008 0.932 0.000 0.000 0.000
#&gt; SRR546237     1  0.3241      0.861 0.824 0.064 0.000 0.000 0.000 0.112
#&gt; SRR546238     3  0.2706      0.853 0.060 0.016 0.880 0.000 0.000 0.044
#&gt; SRR546239     1  0.3241      0.861 0.824 0.064 0.000 0.000 0.000 0.112
#&gt; SRR546240     1  0.3965      0.811 0.764 0.072 0.004 0.000 0.000 0.160
#&gt; SRR547969     2  0.2697      0.899 0.000 0.812 0.000 0.000 0.188 0.000
#&gt; SRR547970     5  0.2806      0.883 0.000 0.000 0.008 0.008 0.840 0.144
#&gt; SRR547971     5  0.1493      0.851 0.000 0.000 0.004 0.004 0.936 0.056
#&gt; SRR547972     2  0.2697      0.899 0.000 0.812 0.000 0.000 0.188 0.000
#&gt; SRR547974     5  0.2300      0.884 0.000 0.000 0.000 0.000 0.856 0.144
#&gt; SRR547976     2  0.2948      0.898 0.000 0.804 0.000 0.000 0.188 0.008
#&gt; SRR547978     5  0.2094      0.839 0.000 0.000 0.008 0.016 0.908 0.068
#&gt; SRR547979     2  0.2948      0.898 0.000 0.804 0.000 0.000 0.188 0.008
#&gt; SRR547981     5  0.2491      0.881 0.000 0.000 0.000 0.000 0.836 0.164
#&gt; SRR547982     2  0.2697      0.899 0.000 0.812 0.000 0.000 0.188 0.000
#&gt; SRR547983     2  0.6587      0.477 0.000 0.444 0.024 0.056 0.396 0.080
#&gt; SRR547989     2  0.6587      0.477 0.000 0.444 0.024 0.056 0.396 0.080
#&gt; SRR547990     5  0.3449      0.846 0.000 0.000 0.008 0.016 0.780 0.196
#&gt; SRR547991     5  0.2094      0.839 0.000 0.000 0.008 0.016 0.908 0.068
#&gt; SRR547992     2  0.2697      0.899 0.000 0.812 0.000 0.000 0.188 0.000
#&gt; SRR801424     4  0.2653      0.761 0.144 0.000 0.012 0.844 0.000 0.000
#&gt; SRR801425     4  0.6162      0.592 0.000 0.016 0.200 0.476 0.000 0.308
#&gt; SRR801426     4  0.4963      0.737 0.000 0.000 0.100 0.612 0.000 0.288
#&gt; SRR801427     4  0.2593      0.756 0.148 0.000 0.008 0.844 0.000 0.000
#&gt; SRR801428     4  0.2653      0.761 0.144 0.000 0.012 0.844 0.000 0.000
#&gt; SRR801429     4  0.4946      0.739 0.000 0.000 0.100 0.616 0.000 0.284
#&gt; SRR801430     4  0.2653      0.761 0.144 0.000 0.012 0.844 0.000 0.000
#&gt; SRR801431     4  0.4946      0.739 0.000 0.000 0.100 0.616 0.000 0.284
#&gt; SRR801432     4  0.4946      0.739 0.000 0.000 0.100 0.616 0.000 0.284
#&gt; SRR801433     4  0.2653      0.761 0.144 0.000 0.012 0.844 0.000 0.000
#&gt; SRR825135     3  0.2340      0.857 0.060 0.016 0.900 0.000 0.000 0.024
#&gt; SRR825136     1  0.0146      0.942 0.996 0.000 0.004 0.000 0.000 0.000
#&gt; SRR825137     3  0.4090      0.839 0.064 0.040 0.788 0.000 0.000 0.108
#&gt; SRR825139     1  0.0146      0.942 0.996 0.000 0.004 0.000 0.000 0.000
#&gt; SRR825140     1  0.0291      0.941 0.992 0.004 0.000 0.000 0.000 0.004
#&gt; SRR825141     3  0.4219      0.837 0.064 0.040 0.776 0.000 0.000 0.120
#&gt; SRR825143     1  0.0436      0.941 0.988 0.004 0.004 0.000 0.000 0.004
</code></pre>

<script>
$('#tab-MAD-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-kmeans-get-classes-5-a').click(function(){
  $('#tab-MAD-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-signatures'>
<ul>
<li><a href='#tab-MAD-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-kmeans-signature_compare](figure_cola/MAD-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-kmeans-collect-classes](figure_cola/MAD-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:skmeans*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "skmeans"]
# you can also extract it by
# res = res_list["MAD:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-skmeans-collect-plots](figure_cola/MAD-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-skmeans-select-partition-number](figure_cola/MAD-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.4795 0.521   0.521
#> 3 3 0.761           0.804       0.872         0.3870 0.803   0.621
#> 4 4 1.000           0.964       0.974         0.1140 0.898   0.703
#> 5 5 0.903           0.956       0.943         0.0856 0.928   0.722
#> 6 6 0.936           0.812       0.892         0.0299 0.985   0.922
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 4 5
```

There is also optional best $k$ = 2 4 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-classes'>
<ul>
<li><a href='#tab-MAD-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-skmeans-get-classes-1'>
<p><a id='tab-MAD-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1 p2
#&gt; SRR547975     2       0          1  0  1
#&gt; SRR547973     2       0          1  0  1
#&gt; SRR547968     2       0          1  0  1
#&gt; SRR547980     2       0          1  0  1
#&gt; SRR545058     1       0          1  1  0
#&gt; SRR546225     2       0          1  0  1
#&gt; SRR546226     1       0          1  1  0
#&gt; SRR546227     1       0          1  1  0
#&gt; SRR546228     1       0          1  1  0
#&gt; SRR546229     1       0          1  1  0
#&gt; SRR546230     1       0          1  1  0
#&gt; SRR546231     1       0          1  1  0
#&gt; SRR546232     1       0          1  1  0
#&gt; SRR546233     1       0          1  1  0
#&gt; SRR546234     1       0          1  1  0
#&gt; SRR546235     1       0          1  1  0
#&gt; SRR546236     1       0          1  1  0
#&gt; SRR546237     1       0          1  1  0
#&gt; SRR546238     1       0          1  1  0
#&gt; SRR546239     1       0          1  1  0
#&gt; SRR546240     1       0          1  1  0
#&gt; SRR547969     2       0          1  0  1
#&gt; SRR547970     2       0          1  0  1
#&gt; SRR547971     2       0          1  0  1
#&gt; SRR547972     2       0          1  0  1
#&gt; SRR547974     2       0          1  0  1
#&gt; SRR547976     2       0          1  0  1
#&gt; SRR547978     2       0          1  0  1
#&gt; SRR547979     2       0          1  0  1
#&gt; SRR547981     2       0          1  0  1
#&gt; SRR547982     2       0          1  0  1
#&gt; SRR547983     2       0          1  0  1
#&gt; SRR547989     2       0          1  0  1
#&gt; SRR547990     2       0          1  0  1
#&gt; SRR547991     2       0          1  0  1
#&gt; SRR547992     2       0          1  0  1
#&gt; SRR801424     1       0          1  1  0
#&gt; SRR801425     1       0          1  1  0
#&gt; SRR801426     1       0          1  1  0
#&gt; SRR801427     1       0          1  1  0
#&gt; SRR801428     1       0          1  1  0
#&gt; SRR801429     1       0          1  1  0
#&gt; SRR801430     1       0          1  1  0
#&gt; SRR801431     1       0          1  1  0
#&gt; SRR801432     1       0          1  1  0
#&gt; SRR801433     1       0          1  1  0
#&gt; SRR825135     1       0          1  1  0
#&gt; SRR825136     1       0          1  1  0
#&gt; SRR825137     1       0          1  1  0
#&gt; SRR825139     1       0          1  1  0
#&gt; SRR825140     1       0          1  1  0
#&gt; SRR825141     1       0          1  1  0
#&gt; SRR825143     1       0          1  1  0
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-1-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-2'>
<p><a id='tab-MAD-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     2   0.000      0.992 0.000 1.000 0.000
#&gt; SRR547973     2   0.000      0.992 0.000 1.000 0.000
#&gt; SRR547968     2   0.000      0.992 0.000 1.000 0.000
#&gt; SRR547980     2   0.000      0.992 0.000 1.000 0.000
#&gt; SRR545058     3   0.619      0.746 0.420 0.000 0.580
#&gt; SRR546225     2   0.348      0.834 0.128 0.872 0.000
#&gt; SRR546226     1   0.000      0.789 1.000 0.000 0.000
#&gt; SRR546227     1   0.000      0.789 1.000 0.000 0.000
#&gt; SRR546228     3   0.619      0.746 0.420 0.000 0.580
#&gt; SRR546229     3   0.506      0.677 0.244 0.000 0.756
#&gt; SRR546230     1   0.000      0.789 1.000 0.000 0.000
#&gt; SRR546231     3   0.618      0.749 0.416 0.000 0.584
#&gt; SRR546232     1   0.000      0.789 1.000 0.000 0.000
#&gt; SRR546233     1   0.000      0.789 1.000 0.000 0.000
#&gt; SRR546234     3   0.627      0.702 0.452 0.000 0.548
#&gt; SRR546235     3   0.618      0.749 0.416 0.000 0.584
#&gt; SRR546236     3   0.619      0.746 0.420 0.000 0.580
#&gt; SRR546237     1   0.000      0.789 1.000 0.000 0.000
#&gt; SRR546238     3   0.619      0.746 0.420 0.000 0.580
#&gt; SRR546239     1   0.000      0.789 1.000 0.000 0.000
#&gt; SRR546240     1   0.000      0.789 1.000 0.000 0.000
#&gt; SRR547969     2   0.000      0.992 0.000 1.000 0.000
#&gt; SRR547970     2   0.000      0.992 0.000 1.000 0.000
#&gt; SRR547971     2   0.000      0.992 0.000 1.000 0.000
#&gt; SRR547972     2   0.000      0.992 0.000 1.000 0.000
#&gt; SRR547974     2   0.000      0.992 0.000 1.000 0.000
#&gt; SRR547976     2   0.000      0.992 0.000 1.000 0.000
#&gt; SRR547978     2   0.000      0.992 0.000 1.000 0.000
#&gt; SRR547979     2   0.000      0.992 0.000 1.000 0.000
#&gt; SRR547981     2   0.000      0.992 0.000 1.000 0.000
#&gt; SRR547982     2   0.000      0.992 0.000 1.000 0.000
#&gt; SRR547983     2   0.000      0.992 0.000 1.000 0.000
#&gt; SRR547989     2   0.000      0.992 0.000 1.000 0.000
#&gt; SRR547990     2   0.000      0.992 0.000 1.000 0.000
#&gt; SRR547991     2   0.000      0.992 0.000 1.000 0.000
#&gt; SRR547992     2   0.000      0.992 0.000 1.000 0.000
#&gt; SRR801424     1   0.625      0.495 0.556 0.000 0.444
#&gt; SRR801425     3   0.000      0.571 0.000 0.000 1.000
#&gt; SRR801426     3   0.000      0.571 0.000 0.000 1.000
#&gt; SRR801427     1   0.621      0.504 0.572 0.000 0.428
#&gt; SRR801428     1   0.625      0.495 0.556 0.000 0.444
#&gt; SRR801429     3   0.000      0.571 0.000 0.000 1.000
#&gt; SRR801430     1   0.625      0.495 0.556 0.000 0.444
#&gt; SRR801431     3   0.000      0.571 0.000 0.000 1.000
#&gt; SRR801432     3   0.000      0.571 0.000 0.000 1.000
#&gt; SRR801433     1   0.625      0.495 0.556 0.000 0.444
#&gt; SRR825135     3   0.618      0.749 0.416 0.000 0.584
#&gt; SRR825136     1   0.000      0.789 1.000 0.000 0.000
#&gt; SRR825137     3   0.618      0.749 0.416 0.000 0.584
#&gt; SRR825139     1   0.000      0.789 1.000 0.000 0.000
#&gt; SRR825140     1   0.000      0.789 1.000 0.000 0.000
#&gt; SRR825141     3   0.618      0.749 0.416 0.000 0.584
#&gt; SRR825143     1   0.000      0.789 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-2-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-3'>
<p><a id='tab-MAD-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     2  0.0657      0.978 0.000 0.984 0.004 0.012
#&gt; SRR547973     2  0.0469      0.977 0.000 0.988 0.000 0.012
#&gt; SRR547968     2  0.0469      0.977 0.000 0.988 0.000 0.012
#&gt; SRR547980     2  0.0657      0.978 0.000 0.984 0.004 0.012
#&gt; SRR545058     3  0.0188      0.980 0.004 0.000 0.996 0.000
#&gt; SRR546225     2  0.4019      0.749 0.196 0.792 0.000 0.012
#&gt; SRR546226     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.0188      0.980 0.004 0.000 0.996 0.000
#&gt; SRR546229     3  0.0188      0.980 0.004 0.000 0.996 0.000
#&gt; SRR546230     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.0188      0.980 0.004 0.000 0.996 0.000
#&gt; SRR546232     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR546234     3  0.3444      0.775 0.184 0.000 0.816 0.000
#&gt; SRR546235     3  0.0188      0.980 0.004 0.000 0.996 0.000
#&gt; SRR546236     3  0.0188      0.980 0.004 0.000 0.996 0.000
#&gt; SRR546237     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR546238     3  0.0188      0.980 0.004 0.000 0.996 0.000
#&gt; SRR546239     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR546240     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR547969     2  0.0469      0.977 0.000 0.988 0.000 0.012
#&gt; SRR547970     2  0.0657      0.978 0.000 0.984 0.004 0.012
#&gt; SRR547971     2  0.0657      0.978 0.000 0.984 0.004 0.012
#&gt; SRR547972     2  0.0469      0.977 0.000 0.988 0.000 0.012
#&gt; SRR547974     2  0.0657      0.978 0.000 0.984 0.004 0.012
#&gt; SRR547976     2  0.0469      0.977 0.000 0.988 0.000 0.012
#&gt; SRR547978     2  0.0657      0.978 0.000 0.984 0.004 0.012
#&gt; SRR547979     2  0.0469      0.977 0.000 0.988 0.000 0.012
#&gt; SRR547981     2  0.0657      0.978 0.000 0.984 0.004 0.012
#&gt; SRR547982     2  0.0469      0.977 0.000 0.988 0.000 0.012
#&gt; SRR547983     2  0.0000      0.978 0.000 1.000 0.000 0.000
#&gt; SRR547989     2  0.0000      0.978 0.000 1.000 0.000 0.000
#&gt; SRR547990     2  0.0657      0.978 0.000 0.984 0.004 0.012
#&gt; SRR547991     2  0.0657      0.978 0.000 0.984 0.004 0.012
#&gt; SRR547992     2  0.0469      0.977 0.000 0.988 0.000 0.012
#&gt; SRR801424     4  0.2149      0.935 0.088 0.000 0.000 0.912
#&gt; SRR801425     4  0.3074      0.813 0.000 0.000 0.152 0.848
#&gt; SRR801426     4  0.0817      0.930 0.000 0.000 0.024 0.976
#&gt; SRR801427     4  0.2149      0.935 0.088 0.000 0.000 0.912
#&gt; SRR801428     4  0.2149      0.935 0.088 0.000 0.000 0.912
#&gt; SRR801429     4  0.0817      0.930 0.000 0.000 0.024 0.976
#&gt; SRR801430     4  0.2149      0.935 0.088 0.000 0.000 0.912
#&gt; SRR801431     4  0.0817      0.930 0.000 0.000 0.024 0.976
#&gt; SRR801432     4  0.0817      0.930 0.000 0.000 0.024 0.976
#&gt; SRR801433     4  0.2149      0.935 0.088 0.000 0.000 0.912
#&gt; SRR825135     3  0.0188      0.980 0.004 0.000 0.996 0.000
#&gt; SRR825136     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR825137     3  0.0188      0.980 0.004 0.000 0.996 0.000
#&gt; SRR825139     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR825140     1  0.0000      1.000 1.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0188      0.980 0.004 0.000 0.996 0.000
#&gt; SRR825143     1  0.0000      1.000 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-3-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-4'>
<p><a id='tab-MAD-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR547975     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547973     2  0.2561      0.946 0.000 0.856 0.000 0.000 0.144
#&gt; SRR547968     2  0.2561      0.946 0.000 0.856 0.000 0.000 0.144
#&gt; SRR547980     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR545058     3  0.0290      0.983 0.000 0.008 0.992 0.000 0.000
#&gt; SRR546225     2  0.4424      0.801 0.084 0.768 0.004 0.000 0.144
#&gt; SRR546226     1  0.0000      0.994 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000      0.994 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.0290      0.983 0.000 0.008 0.992 0.000 0.000
#&gt; SRR546229     3  0.0290      0.983 0.000 0.008 0.992 0.000 0.000
#&gt; SRR546230     1  0.0000      0.994 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.0000      0.985 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546232     1  0.0000      0.994 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.1410      0.942 0.940 0.000 0.000 0.060 0.000
#&gt; SRR546234     3  0.2830      0.877 0.080 0.044 0.876 0.000 0.000
#&gt; SRR546235     3  0.0000      0.985 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546236     3  0.0000      0.985 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546237     1  0.0000      0.994 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546238     3  0.0290      0.983 0.000 0.008 0.992 0.000 0.000
#&gt; SRR546239     1  0.0000      0.994 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546240     1  0.0000      0.994 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547969     2  0.2561      0.946 0.000 0.856 0.000 0.000 0.144
#&gt; SRR547970     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547971     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547972     2  0.2561      0.946 0.000 0.856 0.000 0.000 0.144
#&gt; SRR547974     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547976     2  0.2561      0.946 0.000 0.856 0.000 0.000 0.144
#&gt; SRR547978     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547979     2  0.2561      0.946 0.000 0.856 0.000 0.000 0.144
#&gt; SRR547981     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547982     2  0.2561      0.946 0.000 0.856 0.000 0.000 0.144
#&gt; SRR547983     2  0.3774      0.804 0.000 0.704 0.000 0.000 0.296
#&gt; SRR547989     2  0.3774      0.804 0.000 0.704 0.000 0.000 0.296
#&gt; SRR547990     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547991     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547992     2  0.2561      0.946 0.000 0.856 0.000 0.000 0.144
#&gt; SRR801424     4  0.1544      0.920 0.068 0.000 0.000 0.932 0.000
#&gt; SRR801425     4  0.3866      0.840 0.000 0.096 0.096 0.808 0.000
#&gt; SRR801426     4  0.1908      0.913 0.000 0.092 0.000 0.908 0.000
#&gt; SRR801427     4  0.1544      0.920 0.068 0.000 0.000 0.932 0.000
#&gt; SRR801428     4  0.1544      0.920 0.068 0.000 0.000 0.932 0.000
#&gt; SRR801429     4  0.1908      0.913 0.000 0.092 0.000 0.908 0.000
#&gt; SRR801430     4  0.1544      0.920 0.068 0.000 0.000 0.932 0.000
#&gt; SRR801431     4  0.1908      0.913 0.000 0.092 0.000 0.908 0.000
#&gt; SRR801432     4  0.1908      0.913 0.000 0.092 0.000 0.908 0.000
#&gt; SRR801433     4  0.1544      0.920 0.068 0.000 0.000 0.932 0.000
#&gt; SRR825135     3  0.0290      0.983 0.000 0.008 0.992 0.000 0.000
#&gt; SRR825136     1  0.0162      0.992 0.996 0.000 0.000 0.004 0.000
#&gt; SRR825137     3  0.0000      0.985 0.000 0.000 1.000 0.000 0.000
#&gt; SRR825139     1  0.0162      0.992 0.996 0.000 0.000 0.004 0.000
#&gt; SRR825140     1  0.0000      0.994 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0000      0.985 0.000 0.000 1.000 0.000 0.000
#&gt; SRR825143     1  0.0000      0.994 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-4-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-skmeans-get-classes-5'>
<p><a id='tab-MAD-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR547975     5  0.0000      0.990 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547973     2  0.1765      0.917 0.000 0.924 0.000 0.000 0.052 0.024
#&gt; SRR547968     2  0.1141      0.936 0.000 0.948 0.000 0.000 0.052 0.000
#&gt; SRR547980     5  0.0603      0.988 0.000 0.004 0.000 0.000 0.980 0.016
#&gt; SRR545058     3  0.1267      0.903 0.000 0.000 0.940 0.000 0.000 0.060
#&gt; SRR546225     6  0.6041     -0.316 0.028 0.420 0.004 0.000 0.104 0.444
#&gt; SRR546226     1  0.0000      0.966 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0260      0.965 0.992 0.000 0.000 0.000 0.000 0.008
#&gt; SRR546228     3  0.1204      0.905 0.000 0.000 0.944 0.000 0.000 0.056
#&gt; SRR546229     3  0.1802      0.898 0.000 0.012 0.916 0.000 0.000 0.072
#&gt; SRR546230     1  0.0146      0.966 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; SRR546231     3  0.0632      0.915 0.000 0.000 0.976 0.000 0.000 0.024
#&gt; SRR546232     1  0.0260      0.965 0.992 0.000 0.000 0.000 0.000 0.008
#&gt; SRR546233     1  0.3050      0.712 0.764 0.000 0.000 0.236 0.000 0.000
#&gt; SRR546234     3  0.5071      0.432 0.020 0.040 0.532 0.000 0.000 0.408
#&gt; SRR546235     3  0.0000      0.922 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546236     3  0.0146      0.922 0.000 0.000 0.996 0.000 0.000 0.004
#&gt; SRR546237     1  0.0713      0.958 0.972 0.000 0.000 0.000 0.000 0.028
#&gt; SRR546238     3  0.1858      0.899 0.000 0.012 0.912 0.000 0.000 0.076
#&gt; SRR546239     1  0.0972      0.956 0.964 0.000 0.000 0.008 0.000 0.028
#&gt; SRR546240     1  0.0858      0.957 0.968 0.000 0.000 0.004 0.000 0.028
#&gt; SRR547969     2  0.1141      0.936 0.000 0.948 0.000 0.000 0.052 0.000
#&gt; SRR547970     5  0.0000      0.990 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547971     5  0.0603      0.988 0.000 0.004 0.000 0.000 0.980 0.016
#&gt; SRR547972     2  0.1141      0.936 0.000 0.948 0.000 0.000 0.052 0.000
#&gt; SRR547974     5  0.0000      0.990 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547976     2  0.1141      0.936 0.000 0.948 0.000 0.000 0.052 0.000
#&gt; SRR547978     5  0.0603      0.988 0.000 0.004 0.000 0.000 0.980 0.016
#&gt; SRR547979     2  0.1141      0.936 0.000 0.948 0.000 0.000 0.052 0.000
#&gt; SRR547981     5  0.0000      0.990 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547982     2  0.1141      0.936 0.000 0.948 0.000 0.000 0.052 0.000
#&gt; SRR547983     2  0.3404      0.735 0.000 0.760 0.000 0.000 0.224 0.016
#&gt; SRR547989     2  0.3404      0.735 0.000 0.760 0.000 0.000 0.224 0.016
#&gt; SRR547990     5  0.0000      0.990 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547991     5  0.0603      0.988 0.000 0.004 0.000 0.000 0.980 0.016
#&gt; SRR547992     2  0.1141      0.936 0.000 0.948 0.000 0.000 0.052 0.000
#&gt; SRR801424     4  0.0363      0.684 0.012 0.000 0.000 0.988 0.000 0.000
#&gt; SRR801425     6  0.4855     -0.632 0.000 0.000 0.056 0.460 0.000 0.484
#&gt; SRR801426     4  0.3823      0.472 0.000 0.000 0.000 0.564 0.000 0.436
#&gt; SRR801427     4  0.0632      0.672 0.024 0.000 0.000 0.976 0.000 0.000
#&gt; SRR801428     4  0.0363      0.684 0.012 0.000 0.000 0.988 0.000 0.000
#&gt; SRR801429     4  0.3823      0.472 0.000 0.000 0.000 0.564 0.000 0.436
#&gt; SRR801430     4  0.0363      0.684 0.012 0.000 0.000 0.988 0.000 0.000
#&gt; SRR801431     4  0.3823      0.472 0.000 0.000 0.000 0.564 0.000 0.436
#&gt; SRR801432     4  0.3823      0.472 0.000 0.000 0.000 0.564 0.000 0.436
#&gt; SRR801433     4  0.0363      0.684 0.012 0.000 0.000 0.988 0.000 0.000
#&gt; SRR825135     3  0.1625      0.904 0.000 0.012 0.928 0.000 0.000 0.060
#&gt; SRR825136     1  0.0363      0.964 0.988 0.000 0.000 0.012 0.000 0.000
#&gt; SRR825137     3  0.0000      0.922 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR825139     1  0.0260      0.965 0.992 0.000 0.000 0.008 0.000 0.000
#&gt; SRR825140     1  0.0146      0.966 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; SRR825141     3  0.0000      0.922 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR825143     1  0.0146      0.966 0.996 0.000 0.000 0.004 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-skmeans-get-classes-5-a').click(function(){
  $('#tab-MAD-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-signatures'>
<ul>
<li><a href='#tab-MAD-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-skmeans-signature_compare](figure_cola/MAD-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-skmeans-collect-classes](figure_cola/MAD-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:pam**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "pam"]
# you can also extract it by
# res = res_list["MAD:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-pam-collect-plots](figure_cola/MAD-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-pam-select-partition-number](figure_cola/MAD-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.991       0.996         0.4714 0.531   0.531
#> 3 3 0.787           0.785       0.866         0.4130 0.791   0.607
#> 4 4 0.850           0.918       0.941         0.1187 0.888   0.674
#> 5 5 0.971           0.940       0.975         0.0859 0.935   0.744
#> 6 6 0.964           0.928       0.974         0.0150 0.988   0.939
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 5
```

There is also optional best $k$ = 2 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-classes'>
<ul>
<li><a href='#tab-MAD-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-pam-get-classes-1'>
<p><a id='tab-MAD-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette  p1  p2
#&gt; SRR547975     2   0.000      1.000 0.0 1.0
#&gt; SRR547973     2   0.000      1.000 0.0 1.0
#&gt; SRR547968     2   0.000      1.000 0.0 1.0
#&gt; SRR547980     2   0.000      1.000 0.0 1.0
#&gt; SRR545058     1   0.000      0.994 1.0 0.0
#&gt; SRR546225     1   0.722      0.750 0.8 0.2
#&gt; SRR546226     1   0.000      0.994 1.0 0.0
#&gt; SRR546227     1   0.000      0.994 1.0 0.0
#&gt; SRR546228     1   0.000      0.994 1.0 0.0
#&gt; SRR546229     1   0.000      0.994 1.0 0.0
#&gt; SRR546230     1   0.000      0.994 1.0 0.0
#&gt; SRR546231     1   0.000      0.994 1.0 0.0
#&gt; SRR546232     1   0.000      0.994 1.0 0.0
#&gt; SRR546233     1   0.000      0.994 1.0 0.0
#&gt; SRR546234     1   0.000      0.994 1.0 0.0
#&gt; SRR546235     1   0.000      0.994 1.0 0.0
#&gt; SRR546236     1   0.000      0.994 1.0 0.0
#&gt; SRR546237     1   0.000      0.994 1.0 0.0
#&gt; SRR546238     1   0.000      0.994 1.0 0.0
#&gt; SRR546239     1   0.000      0.994 1.0 0.0
#&gt; SRR546240     1   0.000      0.994 1.0 0.0
#&gt; SRR547969     2   0.000      1.000 0.0 1.0
#&gt; SRR547970     2   0.000      1.000 0.0 1.0
#&gt; SRR547971     2   0.000      1.000 0.0 1.0
#&gt; SRR547972     2   0.000      1.000 0.0 1.0
#&gt; SRR547974     2   0.000      1.000 0.0 1.0
#&gt; SRR547976     2   0.000      1.000 0.0 1.0
#&gt; SRR547978     2   0.000      1.000 0.0 1.0
#&gt; SRR547979     2   0.000      1.000 0.0 1.0
#&gt; SRR547981     2   0.000      1.000 0.0 1.0
#&gt; SRR547982     2   0.000      1.000 0.0 1.0
#&gt; SRR547983     2   0.000      1.000 0.0 1.0
#&gt; SRR547989     2   0.000      1.000 0.0 1.0
#&gt; SRR547990     2   0.000      1.000 0.0 1.0
#&gt; SRR547991     2   0.000      1.000 0.0 1.0
#&gt; SRR547992     2   0.000      1.000 0.0 1.0
#&gt; SRR801424     1   0.000      0.994 1.0 0.0
#&gt; SRR801425     1   0.000      0.994 1.0 0.0
#&gt; SRR801426     1   0.000      0.994 1.0 0.0
#&gt; SRR801427     1   0.000      0.994 1.0 0.0
#&gt; SRR801428     1   0.000      0.994 1.0 0.0
#&gt; SRR801429     1   0.000      0.994 1.0 0.0
#&gt; SRR801430     1   0.000      0.994 1.0 0.0
#&gt; SRR801431     1   0.000      0.994 1.0 0.0
#&gt; SRR801432     1   0.000      0.994 1.0 0.0
#&gt; SRR801433     1   0.000      0.994 1.0 0.0
#&gt; SRR825135     1   0.000      0.994 1.0 0.0
#&gt; SRR825136     1   0.000      0.994 1.0 0.0
#&gt; SRR825137     1   0.000      0.994 1.0 0.0
#&gt; SRR825139     1   0.000      0.994 1.0 0.0
#&gt; SRR825140     1   0.000      0.994 1.0 0.0
#&gt; SRR825141     1   0.000      0.994 1.0 0.0
#&gt; SRR825143     1   0.000      0.994 1.0 0.0
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-1-a').click(function(){
  $('#tab-MAD-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-2'>
<p><a id='tab-MAD-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1 p2    p3
#&gt; SRR547975     2   0.000      1.000 0.000  1 0.000
#&gt; SRR547973     2   0.000      1.000 0.000  1 0.000
#&gt; SRR547968     2   0.000      1.000 0.000  1 0.000
#&gt; SRR547980     2   0.000      1.000 0.000  1 0.000
#&gt; SRR545058     3   0.000      0.760 0.000  0 1.000
#&gt; SRR546225     3   0.000      0.760 0.000  0 1.000
#&gt; SRR546226     1   0.613      0.776 0.600  0 0.400
#&gt; SRR546227     1   0.613      0.776 0.600  0 0.400
#&gt; SRR546228     3   0.000      0.760 0.000  0 1.000
#&gt; SRR546229     3   0.412      0.673 0.168  0 0.832
#&gt; SRR546230     1   0.613      0.776 0.600  0 0.400
#&gt; SRR546231     3   0.000      0.760 0.000  0 1.000
#&gt; SRR546232     1   0.613      0.776 0.600  0 0.400
#&gt; SRR546233     1   0.613      0.776 0.600  0 0.400
#&gt; SRR546234     3   0.000      0.760 0.000  0 1.000
#&gt; SRR546235     3   0.000      0.760 0.000  0 1.000
#&gt; SRR546236     3   0.000      0.760 0.000  0 1.000
#&gt; SRR546237     1   0.613      0.776 0.600  0 0.400
#&gt; SRR546238     3   0.000      0.760 0.000  0 1.000
#&gt; SRR546239     1   0.626      0.705 0.552  0 0.448
#&gt; SRR546240     3   0.614     -0.407 0.404  0 0.596
#&gt; SRR547969     2   0.000      1.000 0.000  1 0.000
#&gt; SRR547970     2   0.000      1.000 0.000  1 0.000
#&gt; SRR547971     2   0.000      1.000 0.000  1 0.000
#&gt; SRR547972     2   0.000      1.000 0.000  1 0.000
#&gt; SRR547974     2   0.000      1.000 0.000  1 0.000
#&gt; SRR547976     2   0.000      1.000 0.000  1 0.000
#&gt; SRR547978     2   0.000      1.000 0.000  1 0.000
#&gt; SRR547979     2   0.000      1.000 0.000  1 0.000
#&gt; SRR547981     2   0.000      1.000 0.000  1 0.000
#&gt; SRR547982     2   0.000      1.000 0.000  1 0.000
#&gt; SRR547983     2   0.000      1.000 0.000  1 0.000
#&gt; SRR547989     2   0.000      1.000 0.000  1 0.000
#&gt; SRR547990     2   0.000      1.000 0.000  1 0.000
#&gt; SRR547991     2   0.000      1.000 0.000  1 0.000
#&gt; SRR547992     2   0.000      1.000 0.000  1 0.000
#&gt; SRR801424     1   0.000      0.559 1.000  0 0.000
#&gt; SRR801425     3   0.613      0.547 0.400  0 0.600
#&gt; SRR801426     3   0.613      0.547 0.400  0 0.600
#&gt; SRR801427     1   0.000      0.559 1.000  0 0.000
#&gt; SRR801428     1   0.000      0.559 1.000  0 0.000
#&gt; SRR801429     3   0.618      0.532 0.416  0 0.584
#&gt; SRR801430     1   0.000      0.559 1.000  0 0.000
#&gt; SRR801431     3   0.613      0.547 0.400  0 0.600
#&gt; SRR801432     3   0.613      0.547 0.400  0 0.600
#&gt; SRR801433     1   0.000      0.559 1.000  0 0.000
#&gt; SRR825135     3   0.000      0.760 0.000  0 1.000
#&gt; SRR825136     1   0.613      0.776 0.600  0 0.400
#&gt; SRR825137     3   0.000      0.760 0.000  0 1.000
#&gt; SRR825139     1   0.613      0.776 0.600  0 0.400
#&gt; SRR825140     1   0.613      0.776 0.600  0 0.400
#&gt; SRR825141     3   0.000      0.760 0.000  0 1.000
#&gt; SRR825143     1   0.613      0.776 0.600  0 0.400
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-2-a').click(function(){
  $('#tab-MAD-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-3'>
<p><a id='tab-MAD-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     2  0.1792     0.9476 0.000 0.932 0.000 0.068
#&gt; SRR547973     2  0.1557     0.9433 0.000 0.944 0.000 0.056
#&gt; SRR547968     2  0.1557     0.9433 0.000 0.944 0.000 0.056
#&gt; SRR547980     2  0.1792     0.9476 0.000 0.932 0.000 0.068
#&gt; SRR545058     3  0.0000     0.9582 0.000 0.000 1.000 0.000
#&gt; SRR546225     3  0.0188     0.9541 0.000 0.000 0.996 0.004
#&gt; SRR546226     1  0.0000     0.9708 1.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000     0.9708 1.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.0000     0.9582 0.000 0.000 1.000 0.000
#&gt; SRR546229     3  0.0000     0.9582 0.000 0.000 1.000 0.000
#&gt; SRR546230     1  0.0000     0.9708 1.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.0000     0.9582 0.000 0.000 1.000 0.000
#&gt; SRR546232     1  0.0000     0.9708 1.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.0000     0.9708 1.000 0.000 0.000 0.000
#&gt; SRR546234     3  0.0000     0.9582 0.000 0.000 1.000 0.000
#&gt; SRR546235     3  0.0000     0.9582 0.000 0.000 1.000 0.000
#&gt; SRR546236     3  0.0000     0.9582 0.000 0.000 1.000 0.000
#&gt; SRR546237     1  0.0000     0.9708 1.000 0.000 0.000 0.000
#&gt; SRR546238     3  0.0000     0.9582 0.000 0.000 1.000 0.000
#&gt; SRR546239     1  0.1389     0.9216 0.952 0.000 0.048 0.000
#&gt; SRR546240     1  0.3569     0.7229 0.804 0.000 0.196 0.000
#&gt; SRR547969     2  0.1557     0.9433 0.000 0.944 0.000 0.056
#&gt; SRR547970     2  0.1792     0.9476 0.000 0.932 0.000 0.068
#&gt; SRR547971     2  0.1792     0.9476 0.000 0.932 0.000 0.068
#&gt; SRR547972     2  0.1557     0.9433 0.000 0.944 0.000 0.056
#&gt; SRR547974     2  0.1792     0.9476 0.000 0.932 0.000 0.068
#&gt; SRR547976     2  0.1557     0.9433 0.000 0.944 0.000 0.056
#&gt; SRR547978     2  0.1792     0.9476 0.000 0.932 0.000 0.068
#&gt; SRR547979     2  0.1557     0.9433 0.000 0.944 0.000 0.056
#&gt; SRR547981     2  0.1792     0.9476 0.000 0.932 0.000 0.068
#&gt; SRR547982     2  0.1557     0.9433 0.000 0.944 0.000 0.056
#&gt; SRR547983     2  0.0000     0.9486 0.000 1.000 0.000 0.000
#&gt; SRR547989     2  0.0188     0.9484 0.000 0.996 0.000 0.004
#&gt; SRR547990     2  0.1792     0.9476 0.000 0.932 0.000 0.068
#&gt; SRR547991     2  0.1792     0.9476 0.000 0.932 0.000 0.068
#&gt; SRR547992     2  0.1557     0.9433 0.000 0.944 0.000 0.056
#&gt; SRR801424     4  0.2704     0.8915 0.124 0.000 0.000 0.876
#&gt; SRR801425     3  0.4941     0.0744 0.000 0.000 0.564 0.436
#&gt; SRR801426     4  0.3610     0.7951 0.000 0.000 0.200 0.800
#&gt; SRR801427     4  0.3074     0.8723 0.152 0.000 0.000 0.848
#&gt; SRR801428     4  0.2704     0.8915 0.124 0.000 0.000 0.876
#&gt; SRR801429     4  0.3048     0.8664 0.016 0.000 0.108 0.876
#&gt; SRR801430     4  0.2704     0.8915 0.124 0.000 0.000 0.876
#&gt; SRR801431     4  0.3610     0.7951 0.000 0.000 0.200 0.800
#&gt; SRR801432     4  0.2704     0.8554 0.000 0.000 0.124 0.876
#&gt; SRR801433     4  0.2704     0.8915 0.124 0.000 0.000 0.876
#&gt; SRR825135     3  0.0000     0.9582 0.000 0.000 1.000 0.000
#&gt; SRR825136     1  0.0000     0.9708 1.000 0.000 0.000 0.000
#&gt; SRR825137     3  0.0000     0.9582 0.000 0.000 1.000 0.000
#&gt; SRR825139     1  0.0000     0.9708 1.000 0.000 0.000 0.000
#&gt; SRR825140     1  0.0000     0.9708 1.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0000     0.9582 0.000 0.000 1.000 0.000
#&gt; SRR825143     1  0.0000     0.9708 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-3-a').click(function(){
  $('#tab-MAD-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-4'>
<p><a id='tab-MAD-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR547975     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547973     2  0.0000      0.977 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547968     2  0.0000      0.977 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547980     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR545058     3  0.0000      0.960 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546225     3  0.0162      0.956 0.000 0.004 0.996 0.000 0.000
#&gt; SRR546226     1  0.0000      0.974 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000      0.974 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.0000      0.960 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546229     3  0.0000      0.960 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546230     1  0.0000      0.974 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.0000      0.960 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546232     1  0.0000      0.974 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.0000      0.974 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546234     3  0.0000      0.960 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546235     3  0.0000      0.960 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546236     3  0.0000      0.960 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546237     1  0.0000      0.974 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546238     3  0.0000      0.960 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546239     1  0.1197      0.931 0.952 0.000 0.048 0.000 0.000
#&gt; SRR546240     1  0.3074      0.750 0.804 0.000 0.196 0.000 0.000
#&gt; SRR547969     2  0.0000      0.977 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547970     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547971     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547972     2  0.0000      0.977 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547974     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547976     2  0.0000      0.977 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547978     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547979     2  0.0000      0.977 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547981     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547982     2  0.0000      0.977 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547983     2  0.2127      0.892 0.000 0.892 0.000 0.000 0.108
#&gt; SRR547989     2  0.1965      0.904 0.000 0.904 0.000 0.000 0.096
#&gt; SRR547990     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547991     5  0.0000      1.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547992     2  0.0000      0.977 0.000 1.000 0.000 0.000 0.000
#&gt; SRR801424     4  0.0000      0.941 0.000 0.000 0.000 1.000 0.000
#&gt; SRR801425     3  0.4256      0.133 0.000 0.000 0.564 0.436 0.000
#&gt; SRR801426     4  0.3109      0.763 0.000 0.000 0.200 0.800 0.000
#&gt; SRR801427     4  0.1121      0.915 0.044 0.000 0.000 0.956 0.000
#&gt; SRR801428     4  0.0000      0.941 0.000 0.000 0.000 1.000 0.000
#&gt; SRR801429     4  0.0000      0.941 0.000 0.000 0.000 1.000 0.000
#&gt; SRR801430     4  0.0000      0.941 0.000 0.000 0.000 1.000 0.000
#&gt; SRR801431     4  0.2891      0.795 0.000 0.000 0.176 0.824 0.000
#&gt; SRR801432     4  0.0000      0.941 0.000 0.000 0.000 1.000 0.000
#&gt; SRR801433     4  0.0000      0.941 0.000 0.000 0.000 1.000 0.000
#&gt; SRR825135     3  0.0000      0.960 0.000 0.000 1.000 0.000 0.000
#&gt; SRR825136     1  0.0000      0.974 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825137     3  0.0000      0.960 0.000 0.000 1.000 0.000 0.000
#&gt; SRR825139     1  0.0000      0.974 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825140     1  0.0000      0.974 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0000      0.960 0.000 0.000 1.000 0.000 0.000
#&gt; SRR825143     1  0.0000      0.974 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-4-a').click(function(){
  $('#tab-MAD-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-pam-get-classes-5'>
<p><a id='tab-MAD-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR547975     5   0.000      0.976 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547973     2   0.000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547968     2   0.000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547980     5   0.000      0.976 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR545058     3   0.000      0.954 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546225     3   0.026      0.946 0.000 0.008 0.992 0.000 0.000 0.000
#&gt; SRR546226     1   0.000      0.969 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1   0.000      0.969 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546228     3   0.000      0.954 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546229     3   0.000      0.954 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546230     1   0.000      0.969 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     3   0.000      0.954 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546232     1   0.000      0.969 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546233     1   0.000      0.969 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546234     3   0.000      0.954 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546235     3   0.000      0.954 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546236     3   0.000      0.954 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546237     1   0.000      0.969 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546238     3   0.000      0.954 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546239     1   0.107      0.918 0.952 0.000 0.048 0.000 0.000 0.000
#&gt; SRR546240     1   0.276      0.702 0.804 0.000 0.196 0.000 0.000 0.000
#&gt; SRR547969     2   0.191      0.879 0.000 0.892 0.000 0.000 0.000 0.108
#&gt; SRR547970     5   0.000      0.976 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547971     5   0.000      0.976 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547972     2   0.000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547974     5   0.238      0.792 0.000 0.152 0.000 0.000 0.848 0.000
#&gt; SRR547976     2   0.000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547978     5   0.000      0.976 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547979     2   0.000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547981     5   0.000      0.976 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547982     2   0.000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547983     6   0.000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547989     6   0.000      1.000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547990     5   0.000      0.976 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547991     5   0.000      0.976 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547992     2   0.000      0.984 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR801424     4   0.000      0.924 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR801425     3   0.382      0.132 0.000 0.000 0.564 0.436 0.000 0.000
#&gt; SRR801426     4   0.279      0.728 0.000 0.000 0.200 0.800 0.000 0.000
#&gt; SRR801427     4   0.101      0.889 0.044 0.000 0.000 0.956 0.000 0.000
#&gt; SRR801428     4   0.000      0.924 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR801429     4   0.000      0.924 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR801430     4   0.000      0.924 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR801431     4   0.260      0.760 0.000 0.000 0.176 0.824 0.000 0.000
#&gt; SRR801432     4   0.000      0.924 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR801433     4   0.000      0.924 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR825135     3   0.000      0.954 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR825136     1   0.000      0.969 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR825137     3   0.000      0.954 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR825139     1   0.000      0.969 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR825140     1   0.000      0.969 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     3   0.000      0.954 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR825143     1   0.000      0.969 1.000 0.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-pam-get-classes-5-a').click(function(){
  $('#tab-MAD-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-signatures'>
<ul>
<li><a href='#tab-MAD-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-1-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-1"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-2-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-2"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-3-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-3"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-4-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-4"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-5-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-pam-signature_compare](figure_cola/MAD-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-pam-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-pam-collect-classes](figure_cola/MAD-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:mclust*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "mclust"]
# you can also extract it by
# res = res_list["MAD:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-mclust-collect-plots](figure_cola/MAD-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-mclust-select-partition-number](figure_cola/MAD-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.994       0.997         0.4704 0.531   0.531
#> 3 3 0.634           0.794       0.856         0.3562 0.826   0.672
#> 4 4 0.838           0.892       0.898         0.1684 0.896   0.707
#> 5 5 0.824           0.890       0.918         0.0785 0.936   0.747
#> 6 6 0.915           0.878       0.944         0.0289 0.965   0.824
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-classes'>
<ul>
<li><a href='#tab-MAD-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-mclust-get-classes-1'>
<p><a id='tab-MAD-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR547975     2  0.0000      0.999 0.000 1.000
#&gt; SRR547973     2  0.0376      0.996 0.004 0.996
#&gt; SRR547968     2  0.0000      0.999 0.000 1.000
#&gt; SRR547980     2  0.0000      0.999 0.000 1.000
#&gt; SRR545058     1  0.0000      0.996 1.000 0.000
#&gt; SRR546225     1  0.5408      0.858 0.876 0.124
#&gt; SRR546226     1  0.0000      0.996 1.000 0.000
#&gt; SRR546227     1  0.0000      0.996 1.000 0.000
#&gt; SRR546228     1  0.0000      0.996 1.000 0.000
#&gt; SRR546229     1  0.0000      0.996 1.000 0.000
#&gt; SRR546230     1  0.0000      0.996 1.000 0.000
#&gt; SRR546231     1  0.0000      0.996 1.000 0.000
#&gt; SRR546232     1  0.0000      0.996 1.000 0.000
#&gt; SRR546233     1  0.0000      0.996 1.000 0.000
#&gt; SRR546234     1  0.0000      0.996 1.000 0.000
#&gt; SRR546235     1  0.0000      0.996 1.000 0.000
#&gt; SRR546236     1  0.0000      0.996 1.000 0.000
#&gt; SRR546237     1  0.0000      0.996 1.000 0.000
#&gt; SRR546238     1  0.0000      0.996 1.000 0.000
#&gt; SRR546239     1  0.0000      0.996 1.000 0.000
#&gt; SRR546240     1  0.0000      0.996 1.000 0.000
#&gt; SRR547969     2  0.0000      0.999 0.000 1.000
#&gt; SRR547970     2  0.0000      0.999 0.000 1.000
#&gt; SRR547971     2  0.0000      0.999 0.000 1.000
#&gt; SRR547972     2  0.0000      0.999 0.000 1.000
#&gt; SRR547974     2  0.0000      0.999 0.000 1.000
#&gt; SRR547976     2  0.0000      0.999 0.000 1.000
#&gt; SRR547978     2  0.0000      0.999 0.000 1.000
#&gt; SRR547979     2  0.0000      0.999 0.000 1.000
#&gt; SRR547981     2  0.0000      0.999 0.000 1.000
#&gt; SRR547982     2  0.0000      0.999 0.000 1.000
#&gt; SRR547983     2  0.0000      0.999 0.000 1.000
#&gt; SRR547989     2  0.0000      0.999 0.000 1.000
#&gt; SRR547990     2  0.1184      0.984 0.016 0.984
#&gt; SRR547991     2  0.0000      0.999 0.000 1.000
#&gt; SRR547992     2  0.0000      0.999 0.000 1.000
#&gt; SRR801424     1  0.0000      0.996 1.000 0.000
#&gt; SRR801425     1  0.0000      0.996 1.000 0.000
#&gt; SRR801426     1  0.0000      0.996 1.000 0.000
#&gt; SRR801427     1  0.0000      0.996 1.000 0.000
#&gt; SRR801428     1  0.0000      0.996 1.000 0.000
#&gt; SRR801429     1  0.0000      0.996 1.000 0.000
#&gt; SRR801430     1  0.0000      0.996 1.000 0.000
#&gt; SRR801431     1  0.0000      0.996 1.000 0.000
#&gt; SRR801432     1  0.0000      0.996 1.000 0.000
#&gt; SRR801433     1  0.0000      0.996 1.000 0.000
#&gt; SRR825135     1  0.0000      0.996 1.000 0.000
#&gt; SRR825136     1  0.0000      0.996 1.000 0.000
#&gt; SRR825137     1  0.0000      0.996 1.000 0.000
#&gt; SRR825139     1  0.0000      0.996 1.000 0.000
#&gt; SRR825140     1  0.0000      0.996 1.000 0.000
#&gt; SRR825141     1  0.0000      0.996 1.000 0.000
#&gt; SRR825143     1  0.0000      0.996 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-1-a').click(function(){
  $('#tab-MAD-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-2'>
<p><a id='tab-MAD-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     2   0.103      0.927 0.000 0.976 0.024
#&gt; SRR547973     2   0.304      0.919 0.000 0.896 0.104
#&gt; SRR547968     2   0.304      0.919 0.000 0.896 0.104
#&gt; SRR547980     2   0.103      0.927 0.000 0.976 0.024
#&gt; SRR545058     1   0.553      0.727 0.704 0.000 0.296
#&gt; SRR546225     1   0.760      0.507 0.656 0.260 0.084
#&gt; SRR546226     1   0.000      0.760 1.000 0.000 0.000
#&gt; SRR546227     1   0.000      0.760 1.000 0.000 0.000
#&gt; SRR546228     1   0.553      0.727 0.704 0.000 0.296
#&gt; SRR546229     1   0.553      0.727 0.704 0.000 0.296
#&gt; SRR546230     1   0.000      0.760 1.000 0.000 0.000
#&gt; SRR546231     1   0.470      0.739 0.788 0.000 0.212
#&gt; SRR546232     1   0.000      0.760 1.000 0.000 0.000
#&gt; SRR546233     1   0.000      0.760 1.000 0.000 0.000
#&gt; SRR546234     1   0.553      0.727 0.704 0.000 0.296
#&gt; SRR546235     1   0.553      0.727 0.704 0.000 0.296
#&gt; SRR546236     1   0.553      0.727 0.704 0.000 0.296
#&gt; SRR546237     1   0.000      0.760 1.000 0.000 0.000
#&gt; SRR546238     1   0.553      0.727 0.704 0.000 0.296
#&gt; SRR546239     1   0.000      0.760 1.000 0.000 0.000
#&gt; SRR546240     1   0.000      0.760 1.000 0.000 0.000
#&gt; SRR547969     2   0.304      0.919 0.000 0.896 0.104
#&gt; SRR547970     2   0.103      0.927 0.000 0.976 0.024
#&gt; SRR547971     2   0.103      0.927 0.000 0.976 0.024
#&gt; SRR547972     2   0.304      0.919 0.000 0.896 0.104
#&gt; SRR547974     2   0.103      0.927 0.000 0.976 0.024
#&gt; SRR547976     2   0.304      0.919 0.000 0.896 0.104
#&gt; SRR547978     2   0.103      0.927 0.000 0.976 0.024
#&gt; SRR547979     2   0.304      0.919 0.000 0.896 0.104
#&gt; SRR547981     2   0.103      0.927 0.000 0.976 0.024
#&gt; SRR547982     2   0.304      0.919 0.000 0.896 0.104
#&gt; SRR547983     2   0.000      0.928 0.000 1.000 0.000
#&gt; SRR547989     2   0.000      0.928 0.000 1.000 0.000
#&gt; SRR547990     2   0.670      0.430 0.328 0.648 0.024
#&gt; SRR547991     2   0.103      0.927 0.000 0.976 0.024
#&gt; SRR547992     2   0.304      0.919 0.000 0.896 0.104
#&gt; SRR801424     3   0.620      0.734 0.424 0.000 0.576
#&gt; SRR801425     3   0.348      0.740 0.128 0.000 0.872
#&gt; SRR801426     3   0.348      0.740 0.128 0.000 0.872
#&gt; SRR801427     3   0.620      0.734 0.424 0.000 0.576
#&gt; SRR801428     3   0.620      0.734 0.424 0.000 0.576
#&gt; SRR801429     3   0.348      0.740 0.128 0.000 0.872
#&gt; SRR801430     3   0.620      0.734 0.424 0.000 0.576
#&gt; SRR801431     3   0.348      0.740 0.128 0.000 0.872
#&gt; SRR801432     3   0.348      0.740 0.128 0.000 0.872
#&gt; SRR801433     3   0.620      0.734 0.424 0.000 0.576
#&gt; SRR825135     1   0.553      0.727 0.704 0.000 0.296
#&gt; SRR825136     1   0.000      0.760 1.000 0.000 0.000
#&gt; SRR825137     1   0.553      0.727 0.704 0.000 0.296
#&gt; SRR825139     1   0.000      0.760 1.000 0.000 0.000
#&gt; SRR825140     1   0.000      0.760 1.000 0.000 0.000
#&gt; SRR825141     1   0.553      0.727 0.704 0.000 0.296
#&gt; SRR825143     1   0.000      0.760 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-2-a').click(function(){
  $('#tab-MAD-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-3'>
<p><a id='tab-MAD-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     2  0.0000      0.891 0.000 1.000 0.000 0.000
#&gt; SRR547973     2  0.4661      0.846 0.256 0.728 0.000 0.016
#&gt; SRR547968     2  0.4661      0.846 0.256 0.728 0.000 0.016
#&gt; SRR547980     2  0.0000      0.891 0.000 1.000 0.000 0.000
#&gt; SRR545058     3  0.0469      0.975 0.000 0.000 0.988 0.012
#&gt; SRR546225     3  0.2262      0.918 0.040 0.012 0.932 0.016
#&gt; SRR546226     1  0.4103      0.995 0.744 0.000 0.000 0.256
#&gt; SRR546227     1  0.4103      0.995 0.744 0.000 0.000 0.256
#&gt; SRR546228     3  0.0000      0.979 0.000 0.000 1.000 0.000
#&gt; SRR546229     3  0.2081      0.882 0.000 0.000 0.916 0.084
#&gt; SRR546230     1  0.4103      0.995 0.744 0.000 0.000 0.256
#&gt; SRR546231     3  0.0000      0.979 0.000 0.000 1.000 0.000
#&gt; SRR546232     1  0.4103      0.995 0.744 0.000 0.000 0.256
#&gt; SRR546233     1  0.4661      0.977 0.728 0.000 0.016 0.256
#&gt; SRR546234     3  0.0592      0.972 0.000 0.000 0.984 0.016
#&gt; SRR546235     3  0.0000      0.979 0.000 0.000 1.000 0.000
#&gt; SRR546236     3  0.0000      0.979 0.000 0.000 1.000 0.000
#&gt; SRR546237     1  0.4103      0.995 0.744 0.000 0.000 0.256
#&gt; SRR546238     3  0.0469      0.975 0.000 0.000 0.988 0.012
#&gt; SRR546239     1  0.4103      0.995 0.744 0.000 0.000 0.256
#&gt; SRR546240     1  0.4737      0.973 0.728 0.000 0.020 0.252
#&gt; SRR547969     2  0.4661      0.846 0.256 0.728 0.000 0.016
#&gt; SRR547970     2  0.0000      0.891 0.000 1.000 0.000 0.000
#&gt; SRR547971     2  0.0000      0.891 0.000 1.000 0.000 0.000
#&gt; SRR547972     2  0.4661      0.846 0.256 0.728 0.000 0.016
#&gt; SRR547974     2  0.0000      0.891 0.000 1.000 0.000 0.000
#&gt; SRR547976     2  0.4661      0.846 0.256 0.728 0.000 0.016
#&gt; SRR547978     2  0.0000      0.891 0.000 1.000 0.000 0.000
#&gt; SRR547979     2  0.4661      0.846 0.256 0.728 0.000 0.016
#&gt; SRR547981     2  0.0000      0.891 0.000 1.000 0.000 0.000
#&gt; SRR547982     2  0.4661      0.846 0.256 0.728 0.000 0.016
#&gt; SRR547983     2  0.0000      0.891 0.000 1.000 0.000 0.000
#&gt; SRR547989     2  0.0000      0.891 0.000 1.000 0.000 0.000
#&gt; SRR547990     2  0.0592      0.882 0.000 0.984 0.000 0.016
#&gt; SRR547991     2  0.0000      0.891 0.000 1.000 0.000 0.000
#&gt; SRR547992     2  0.4661      0.846 0.256 0.728 0.000 0.016
#&gt; SRR801424     4  0.1406      0.730 0.024 0.000 0.016 0.960
#&gt; SRR801425     4  0.4477      0.694 0.000 0.000 0.312 0.688
#&gt; SRR801426     4  0.4331      0.722 0.000 0.000 0.288 0.712
#&gt; SRR801427     4  0.1798      0.710 0.040 0.000 0.016 0.944
#&gt; SRR801428     4  0.1406      0.730 0.024 0.000 0.016 0.960
#&gt; SRR801429     4  0.4331      0.722 0.000 0.000 0.288 0.712
#&gt; SRR801430     4  0.1406      0.730 0.024 0.000 0.016 0.960
#&gt; SRR801431     4  0.4331      0.722 0.000 0.000 0.288 0.712
#&gt; SRR801432     4  0.4331      0.722 0.000 0.000 0.288 0.712
#&gt; SRR801433     4  0.1406      0.730 0.024 0.000 0.016 0.960
#&gt; SRR825135     3  0.0000      0.979 0.000 0.000 1.000 0.000
#&gt; SRR825136     1  0.4103      0.995 0.744 0.000 0.000 0.256
#&gt; SRR825137     3  0.0000      0.979 0.000 0.000 1.000 0.000
#&gt; SRR825139     1  0.4103      0.995 0.744 0.000 0.000 0.256
#&gt; SRR825140     1  0.4103      0.995 0.744 0.000 0.000 0.256
#&gt; SRR825141     3  0.0000      0.979 0.000 0.000 1.000 0.000
#&gt; SRR825143     1  0.4103      0.995 0.744 0.000 0.000 0.256
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-3-a').click(function(){
  $('#tab-MAD-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-4'>
<p><a id='tab-MAD-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR547975     5  0.0609      0.815 0.000 0.020 0.000 0.000 0.980
#&gt; SRR547973     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547968     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547980     5  0.2929      0.820 0.000 0.180 0.000 0.000 0.820
#&gt; SRR545058     3  0.0000      0.944 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546225     3  0.3073      0.888 0.004 0.000 0.868 0.076 0.052
#&gt; SRR546226     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.0000      0.944 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546229     3  0.3424      0.649 0.000 0.000 0.760 0.240 0.000
#&gt; SRR546230     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.1638      0.921 0.004 0.000 0.932 0.064 0.000
#&gt; SRR546232     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546234     3  0.2694      0.899 0.004 0.000 0.888 0.076 0.032
#&gt; SRR546235     3  0.0000      0.944 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546236     3  0.1478      0.923 0.000 0.000 0.936 0.064 0.000
#&gt; SRR546237     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546238     3  0.0000      0.944 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546239     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546240     1  0.0880      0.963 0.968 0.000 0.000 0.000 0.032
#&gt; SRR547969     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547970     5  0.0000      0.804 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547971     5  0.2280      0.834 0.000 0.120 0.000 0.000 0.880
#&gt; SRR547972     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547974     5  0.2377      0.834 0.000 0.128 0.000 0.000 0.872
#&gt; SRR547976     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547978     5  0.3508      0.779 0.000 0.252 0.000 0.000 0.748
#&gt; SRR547979     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547981     5  0.0000      0.804 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547982     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547983     5  0.4273      0.497 0.000 0.448 0.000 0.000 0.552
#&gt; SRR547989     5  0.4278      0.488 0.000 0.452 0.000 0.000 0.548
#&gt; SRR547990     5  0.0880      0.819 0.000 0.032 0.000 0.000 0.968
#&gt; SRR547991     5  0.3395      0.791 0.000 0.236 0.000 0.000 0.764
#&gt; SRR547992     2  0.0000      1.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR801424     4  0.2179      0.849 0.112 0.000 0.000 0.888 0.000
#&gt; SRR801425     4  0.2929      0.800 0.000 0.000 0.180 0.820 0.000
#&gt; SRR801426     4  0.2020      0.837 0.000 0.000 0.100 0.900 0.000
#&gt; SRR801427     4  0.3999      0.539 0.344 0.000 0.000 0.656 0.000
#&gt; SRR801428     4  0.2179      0.849 0.112 0.000 0.000 0.888 0.000
#&gt; SRR801429     4  0.2020      0.837 0.000 0.000 0.100 0.900 0.000
#&gt; SRR801430     4  0.2179      0.849 0.112 0.000 0.000 0.888 0.000
#&gt; SRR801431     4  0.2020      0.837 0.000 0.000 0.100 0.900 0.000
#&gt; SRR801432     4  0.2020      0.837 0.000 0.000 0.100 0.900 0.000
#&gt; SRR801433     4  0.2179      0.849 0.112 0.000 0.000 0.888 0.000
#&gt; SRR825135     3  0.0000      0.944 0.000 0.000 1.000 0.000 0.000
#&gt; SRR825136     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825137     3  0.0000      0.944 0.000 0.000 1.000 0.000 0.000
#&gt; SRR825139     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825140     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0000      0.944 0.000 0.000 1.000 0.000 0.000
#&gt; SRR825143     1  0.0000      0.997 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-4-a').click(function(){
  $('#tab-MAD-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-mclust-get-classes-5'>
<p><a id='tab-MAD-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR547975     5  0.1007     0.9433 0.000 0.044 0.000 0.000 0.956 0.000
#&gt; SRR547973     2  0.0000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547968     2  0.0000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547980     5  0.1141     0.9453 0.000 0.052 0.000 0.000 0.948 0.000
#&gt; SRR545058     3  0.0000     0.9188 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546225     1  0.5111     0.0541 0.492 0.020 0.448 0.000 0.040 0.000
#&gt; SRR546226     1  0.0713     0.8935 0.972 0.000 0.000 0.000 0.000 0.028
#&gt; SRR546227     1  0.0000     0.8901 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.0000     0.9188 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546229     3  0.1957     0.8034 0.000 0.000 0.888 0.112 0.000 0.000
#&gt; SRR546230     1  0.0713     0.8935 0.972 0.000 0.000 0.000 0.000 0.028
#&gt; SRR546231     3  0.0632     0.9015 0.024 0.000 0.976 0.000 0.000 0.000
#&gt; SRR546232     1  0.0000     0.8901 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.2697     0.8088 0.812 0.000 0.000 0.000 0.000 0.188
#&gt; SRR546234     3  0.4179    -0.0528 0.472 0.000 0.516 0.000 0.012 0.000
#&gt; SRR546235     3  0.0000     0.9188 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546236     3  0.0000     0.9188 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546237     1  0.1957     0.8546 0.888 0.000 0.000 0.000 0.000 0.112
#&gt; SRR546238     3  0.0000     0.9188 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR546239     1  0.1957     0.8546 0.888 0.000 0.000 0.000 0.000 0.112
#&gt; SRR546240     1  0.1957     0.8546 0.888 0.000 0.000 0.000 0.000 0.112
#&gt; SRR547969     2  0.0000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547970     5  0.0000     0.9222 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547971     5  0.1141     0.9453 0.000 0.052 0.000 0.000 0.948 0.000
#&gt; SRR547972     2  0.0000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547974     5  0.1141     0.9453 0.000 0.052 0.000 0.000 0.948 0.000
#&gt; SRR547976     2  0.0000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547978     5  0.1141     0.9453 0.000 0.052 0.000 0.000 0.948 0.000
#&gt; SRR547979     2  0.0000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547981     5  0.0000     0.9222 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547982     2  0.0000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547983     5  0.2823     0.8201 0.000 0.204 0.000 0.000 0.796 0.000
#&gt; SRR547989     5  0.2823     0.8201 0.000 0.204 0.000 0.000 0.796 0.000
#&gt; SRR547990     5  0.0000     0.9222 0.000 0.000 0.000 0.000 1.000 0.000
#&gt; SRR547991     5  0.1327     0.9400 0.000 0.064 0.000 0.000 0.936 0.000
#&gt; SRR547992     2  0.0000     1.0000 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR801424     6  0.0000     0.9698 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR801425     4  0.3409     0.5527 0.000 0.000 0.300 0.700 0.000 0.000
#&gt; SRR801426     4  0.0146     0.9000 0.000 0.000 0.004 0.996 0.000 0.000
#&gt; SRR801427     6  0.1663     0.8774 0.088 0.000 0.000 0.000 0.000 0.912
#&gt; SRR801428     6  0.0000     0.9698 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR801429     4  0.0000     0.9016 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR801430     6  0.0000     0.9698 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR801431     4  0.0000     0.9016 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR801432     4  0.0000     0.9016 0.000 0.000 0.000 1.000 0.000 0.000
#&gt; SRR801433     6  0.0000     0.9698 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR825135     3  0.0000     0.9188 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR825136     1  0.1327     0.8798 0.936 0.000 0.000 0.000 0.000 0.064
#&gt; SRR825137     3  0.0000     0.9188 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR825139     1  0.0937     0.8905 0.960 0.000 0.000 0.000 0.000 0.040
#&gt; SRR825140     1  0.0000     0.8901 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0000     0.9188 0.000 0.000 1.000 0.000 0.000 0.000
#&gt; SRR825143     1  0.0713     0.8935 0.972 0.000 0.000 0.000 0.000 0.028
</code></pre>

<script>
$('#tab-MAD-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-mclust-get-classes-5-a').click(function(){
  $('#tab-MAD-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-signatures'>
<ul>
<li><a href='#tab-MAD-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-1-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-1"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-2-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-2"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-3-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-3"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-4-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-4"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-5-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-mclust-signature_compare](figure_cola/MAD-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-mclust-collect-classes](figure_cola/MAD-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### MAD:NMF**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["MAD", "NMF"]
# you can also extract it by
# res = res_list["MAD:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'MAD' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk MAD-NMF-collect-plots](figure_cola/MAD-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk MAD-NMF-select-partition-number](figure_cola/MAD-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.958           0.940       0.976         0.4872 0.512   0.512
#> 3 3 0.556           0.631       0.730         0.2816 0.920   0.844
#> 4 4 0.697           0.706       0.788         0.1742 0.798   0.543
#> 5 5 0.819           0.776       0.863         0.0867 0.871   0.546
#> 6 6 0.783           0.761       0.864         0.0343 0.959   0.794
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-MAD-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-classes'>
<ul>
<li><a href='#tab-MAD-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-MAD-NMF-get-classes-1'>
<p><a id='tab-MAD-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR547975     2   0.000     0.9704 0.000 1.000
#&gt; SRR547973     2   0.000     0.9704 0.000 1.000
#&gt; SRR547968     2   0.000     0.9704 0.000 1.000
#&gt; SRR547980     2   0.000     0.9704 0.000 1.000
#&gt; SRR545058     1   0.000     0.9768 1.000 0.000
#&gt; SRR546225     2   0.443     0.8763 0.092 0.908
#&gt; SRR546226     1   0.000     0.9768 1.000 0.000
#&gt; SRR546227     1   0.000     0.9768 1.000 0.000
#&gt; SRR546228     1   0.000     0.9768 1.000 0.000
#&gt; SRR546229     1   0.000     0.9768 1.000 0.000
#&gt; SRR546230     1   0.000     0.9768 1.000 0.000
#&gt; SRR546231     1   0.000     0.9768 1.000 0.000
#&gt; SRR546232     1   0.000     0.9768 1.000 0.000
#&gt; SRR546233     1   0.000     0.9768 1.000 0.000
#&gt; SRR546234     1   0.000     0.9768 1.000 0.000
#&gt; SRR546235     1   0.000     0.9768 1.000 0.000
#&gt; SRR546236     1   0.000     0.9768 1.000 0.000
#&gt; SRR546237     1   0.000     0.9768 1.000 0.000
#&gt; SRR546238     1   0.118     0.9641 0.984 0.016
#&gt; SRR546239     1   0.000     0.9768 1.000 0.000
#&gt; SRR546240     1   0.000     0.9768 1.000 0.000
#&gt; SRR547969     2   0.000     0.9704 0.000 1.000
#&gt; SRR547970     2   0.000     0.9704 0.000 1.000
#&gt; SRR547971     2   0.000     0.9704 0.000 1.000
#&gt; SRR547972     2   0.000     0.9704 0.000 1.000
#&gt; SRR547974     2   0.000     0.9704 0.000 1.000
#&gt; SRR547976     2   0.000     0.9704 0.000 1.000
#&gt; SRR547978     2   0.000     0.9704 0.000 1.000
#&gt; SRR547979     2   0.000     0.9704 0.000 1.000
#&gt; SRR547981     2   0.000     0.9704 0.000 1.000
#&gt; SRR547982     2   0.000     0.9704 0.000 1.000
#&gt; SRR547983     2   0.000     0.9704 0.000 1.000
#&gt; SRR547989     2   0.000     0.9704 0.000 1.000
#&gt; SRR547990     2   0.000     0.9704 0.000 1.000
#&gt; SRR547991     2   0.000     0.9704 0.000 1.000
#&gt; SRR547992     2   0.000     0.9704 0.000 1.000
#&gt; SRR801424     1   0.000     0.9768 1.000 0.000
#&gt; SRR801425     1   0.697     0.7708 0.812 0.188
#&gt; SRR801426     1   0.886     0.5690 0.696 0.304
#&gt; SRR801427     1   0.000     0.9768 1.000 0.000
#&gt; SRR801428     1   0.000     0.9768 1.000 0.000
#&gt; SRR801429     1   0.605     0.8245 0.852 0.148
#&gt; SRR801430     1   0.000     0.9768 1.000 0.000
#&gt; SRR801431     1   0.204     0.9502 0.968 0.032
#&gt; SRR801432     2   0.998     0.0563 0.472 0.528
#&gt; SRR801433     1   0.000     0.9768 1.000 0.000
#&gt; SRR825135     1   0.000     0.9768 1.000 0.000
#&gt; SRR825136     1   0.000     0.9768 1.000 0.000
#&gt; SRR825137     1   0.000     0.9768 1.000 0.000
#&gt; SRR825139     1   0.000     0.9768 1.000 0.000
#&gt; SRR825140     1   0.000     0.9768 1.000 0.000
#&gt; SRR825141     1   0.000     0.9768 1.000 0.000
#&gt; SRR825143     1   0.000     0.9768 1.000 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-1-a').click(function(){
  $('#tab-MAD-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-2'>
<p><a id='tab-MAD-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     2  0.6267     0.8266 0.000 0.548 0.452
#&gt; SRR547973     3  0.0237     0.6653 0.000 0.004 0.996
#&gt; SRR547968     3  0.0237     0.6653 0.000 0.004 0.996
#&gt; SRR547980     2  0.6267     0.8266 0.000 0.548 0.452
#&gt; SRR545058     1  0.5560     0.7525 0.700 0.300 0.000
#&gt; SRR546225     2  0.9642    -0.1250 0.344 0.440 0.216
#&gt; SRR546226     1  0.0424     0.7814 0.992 0.008 0.000
#&gt; SRR546227     1  0.0000     0.7805 1.000 0.000 0.000
#&gt; SRR546228     1  0.5560     0.7525 0.700 0.300 0.000
#&gt; SRR546229     1  0.5560     0.7525 0.700 0.300 0.000
#&gt; SRR546230     1  0.0237     0.7800 0.996 0.004 0.000
#&gt; SRR546231     1  0.5560     0.7525 0.700 0.300 0.000
#&gt; SRR546232     1  0.0747     0.7820 0.984 0.016 0.000
#&gt; SRR546233     1  0.2711     0.7527 0.912 0.088 0.000
#&gt; SRR546234     1  0.5785     0.7504 0.696 0.300 0.004
#&gt; SRR546235     1  0.5560     0.7525 0.700 0.300 0.000
#&gt; SRR546236     1  0.5560     0.7525 0.700 0.300 0.000
#&gt; SRR546237     1  0.2356     0.7806 0.928 0.072 0.000
#&gt; SRR546238     1  0.6799     0.6056 0.532 0.456 0.012
#&gt; SRR546239     1  0.0592     0.7818 0.988 0.012 0.000
#&gt; SRR546240     1  0.4452     0.7689 0.808 0.192 0.000
#&gt; SRR547969     3  0.1289     0.6477 0.000 0.032 0.968
#&gt; SRR547970     2  0.6267     0.8266 0.000 0.548 0.452
#&gt; SRR547971     2  0.6267     0.8266 0.000 0.548 0.452
#&gt; SRR547972     3  0.0000     0.6656 0.000 0.000 1.000
#&gt; SRR547974     2  0.6280     0.8119 0.000 0.540 0.460
#&gt; SRR547976     3  0.5291     0.0200 0.000 0.268 0.732
#&gt; SRR547978     2  0.6267     0.8266 0.000 0.548 0.452
#&gt; SRR547979     3  0.1031     0.6556 0.000 0.024 0.976
#&gt; SRR547981     2  0.6267     0.8266 0.000 0.548 0.452
#&gt; SRR547982     3  0.0592     0.6626 0.000 0.012 0.988
#&gt; SRR547983     3  0.6140    -0.4828 0.000 0.404 0.596
#&gt; SRR547989     3  0.6140    -0.4828 0.000 0.404 0.596
#&gt; SRR547990     2  0.6274     0.8203 0.000 0.544 0.456
#&gt; SRR547991     2  0.6267     0.8266 0.000 0.548 0.452
#&gt; SRR547992     3  0.0237     0.6653 0.000 0.004 0.996
#&gt; SRR801424     1  0.4539     0.7144 0.836 0.148 0.016
#&gt; SRR801425     1  0.8135     0.6602 0.484 0.448 0.068
#&gt; SRR801426     1  0.9963     0.3202 0.376 0.316 0.308
#&gt; SRR801427     1  0.4228     0.7191 0.844 0.148 0.008
#&gt; SRR801428     1  0.6546     0.6549 0.756 0.148 0.096
#&gt; SRR801429     1  0.9234     0.1937 0.476 0.160 0.364
#&gt; SRR801430     1  0.6968     0.6324 0.732 0.148 0.120
#&gt; SRR801431     1  0.9588     0.4585 0.476 0.284 0.240
#&gt; SRR801432     3  0.9306     0.0331 0.348 0.172 0.480
#&gt; SRR801433     1  0.6834     0.6402 0.740 0.148 0.112
#&gt; SRR825135     1  0.5560     0.7525 0.700 0.300 0.000
#&gt; SRR825136     1  0.0892     0.7763 0.980 0.020 0.000
#&gt; SRR825137     1  0.5560     0.7525 0.700 0.300 0.000
#&gt; SRR825139     1  0.0237     0.7800 0.996 0.004 0.000
#&gt; SRR825140     1  0.0237     0.7809 0.996 0.004 0.000
#&gt; SRR825141     1  0.5560     0.7525 0.700 0.300 0.000
#&gt; SRR825143     1  0.0237     0.7800 0.996 0.004 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-2-a').click(function(){
  $('#tab-MAD-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-3'>
<p><a id='tab-MAD-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     2  0.0469    0.98007 0.000 0.988 0.000 0.012
#&gt; SRR547973     4  0.2319    0.79024 0.000 0.040 0.036 0.924
#&gt; SRR547968     4  0.2124    0.79321 0.000 0.040 0.028 0.932
#&gt; SRR547980     2  0.0895    0.97720 0.000 0.976 0.004 0.020
#&gt; SRR545058     3  0.4585    0.74615 0.332 0.000 0.668 0.000
#&gt; SRR546225     3  0.8612   -0.00916 0.068 0.148 0.440 0.344
#&gt; SRR546226     1  0.0817    0.77022 0.976 0.000 0.024 0.000
#&gt; SRR546227     1  0.0188    0.78260 0.996 0.000 0.004 0.000
#&gt; SRR546228     3  0.4585    0.74615 0.332 0.000 0.668 0.000
#&gt; SRR546229     3  0.4883    0.72908 0.288 0.000 0.696 0.016
#&gt; SRR546230     1  0.0336    0.78342 0.992 0.000 0.008 0.000
#&gt; SRR546231     3  0.4699    0.74946 0.320 0.000 0.676 0.004
#&gt; SRR546232     1  0.1557    0.74360 0.944 0.000 0.056 0.000
#&gt; SRR546233     1  0.1474    0.76563 0.948 0.000 0.052 0.000
#&gt; SRR546234     3  0.5174    0.70356 0.368 0.000 0.620 0.012
#&gt; SRR546235     3  0.4543    0.74971 0.324 0.000 0.676 0.000
#&gt; SRR546236     3  0.4837    0.73196 0.348 0.000 0.648 0.004
#&gt; SRR546237     1  0.1716    0.73679 0.936 0.000 0.064 0.000
#&gt; SRR546238     3  0.5732    0.73681 0.292 0.032 0.664 0.012
#&gt; SRR546239     1  0.1637    0.74051 0.940 0.000 0.060 0.000
#&gt; SRR546240     1  0.3688    0.48340 0.792 0.000 0.208 0.000
#&gt; SRR547969     4  0.2921    0.80209 0.000 0.140 0.000 0.860
#&gt; SRR547970     2  0.0469    0.97081 0.000 0.988 0.012 0.000
#&gt; SRR547971     2  0.0469    0.98007 0.000 0.988 0.000 0.012
#&gt; SRR547972     4  0.2647    0.80944 0.000 0.120 0.000 0.880
#&gt; SRR547974     2  0.0592    0.97932 0.000 0.984 0.000 0.016
#&gt; SRR547976     4  0.4175    0.75038 0.000 0.212 0.012 0.776
#&gt; SRR547978     2  0.0895    0.97764 0.000 0.976 0.004 0.020
#&gt; SRR547979     4  0.3217    0.80848 0.000 0.128 0.012 0.860
#&gt; SRR547981     2  0.0707    0.96728 0.000 0.980 0.020 0.000
#&gt; SRR547982     4  0.1867    0.80928 0.000 0.072 0.000 0.928
#&gt; SRR547983     4  0.4916    0.44856 0.000 0.424 0.000 0.576
#&gt; SRR547989     4  0.4916    0.44856 0.000 0.424 0.000 0.576
#&gt; SRR547990     2  0.0921    0.96169 0.000 0.972 0.028 0.000
#&gt; SRR547991     2  0.1256    0.96921 0.000 0.964 0.008 0.028
#&gt; SRR547992     4  0.1637    0.80666 0.000 0.060 0.000 0.940
#&gt; SRR801424     1  0.5698    0.54655 0.608 0.000 0.356 0.036
#&gt; SRR801425     3  0.4250    0.52105 0.052 0.064 0.848 0.036
#&gt; SRR801426     3  0.4724    0.44936 0.088 0.004 0.800 0.108
#&gt; SRR801427     1  0.5890    0.59437 0.660 0.000 0.268 0.072
#&gt; SRR801428     1  0.6495    0.56001 0.608 0.000 0.284 0.108
#&gt; SRR801429     3  0.7026   -0.16089 0.120 0.000 0.476 0.404
#&gt; SRR801430     1  0.6394    0.55094 0.596 0.000 0.316 0.088
#&gt; SRR801431     3  0.4346    0.47743 0.096 0.004 0.824 0.076
#&gt; SRR801432     4  0.6542    0.20925 0.076 0.000 0.428 0.496
#&gt; SRR801433     1  0.6558    0.54903 0.596 0.000 0.296 0.108
#&gt; SRR825135     3  0.4699    0.75051 0.320 0.000 0.676 0.004
#&gt; SRR825136     1  0.0469    0.78262 0.988 0.000 0.012 0.000
#&gt; SRR825137     3  0.4677    0.75051 0.316 0.000 0.680 0.004
#&gt; SRR825139     1  0.0000    0.78367 1.000 0.000 0.000 0.000
#&gt; SRR825140     1  0.0188    0.78260 0.996 0.000 0.004 0.000
#&gt; SRR825141     3  0.4585    0.74738 0.332 0.000 0.668 0.000
#&gt; SRR825143     1  0.0000    0.78367 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-3-a').click(function(){
  $('#tab-MAD-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-4'>
<p><a id='tab-MAD-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR547975     5  0.0290      0.977 0.000 0.000 0.000 0.008 0.992
#&gt; SRR547973     2  0.2329      0.821 0.000 0.876 0.000 0.124 0.000
#&gt; SRR547968     2  0.1544      0.863 0.000 0.932 0.000 0.068 0.000
#&gt; SRR547980     5  0.1012      0.971 0.012 0.000 0.000 0.020 0.968
#&gt; SRR545058     3  0.0000      0.889 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546225     2  0.4548      0.731 0.000 0.748 0.156 0.096 0.000
#&gt; SRR546226     1  0.0880      0.907 0.968 0.000 0.032 0.000 0.000
#&gt; SRR546227     1  0.0880      0.907 0.968 0.000 0.032 0.000 0.000
#&gt; SRR546228     3  0.0451      0.888 0.000 0.008 0.988 0.004 0.000
#&gt; SRR546229     3  0.3730      0.540 0.000 0.000 0.712 0.288 0.000
#&gt; SRR546230     1  0.1041      0.905 0.964 0.000 0.032 0.004 0.000
#&gt; SRR546231     3  0.0000      0.889 0.000 0.000 1.000 0.000 0.000
#&gt; SRR546232     1  0.0880      0.907 0.968 0.000 0.032 0.000 0.000
#&gt; SRR546233     1  0.1106      0.896 0.964 0.000 0.024 0.012 0.000
#&gt; SRR546234     3  0.3244      0.789 0.008 0.084 0.860 0.048 0.000
#&gt; SRR546235     3  0.0290      0.889 0.000 0.000 0.992 0.008 0.000
#&gt; SRR546236     3  0.0451      0.885 0.008 0.000 0.988 0.004 0.000
#&gt; SRR546237     1  0.3333      0.690 0.788 0.000 0.208 0.004 0.000
#&gt; SRR546238     3  0.2300      0.849 0.000 0.024 0.904 0.072 0.000
#&gt; SRR546239     1  0.1908      0.848 0.908 0.000 0.092 0.000 0.000
#&gt; SRR546240     3  0.5425      0.351 0.320 0.000 0.600 0.080 0.000
#&gt; SRR547969     2  0.1393      0.878 0.012 0.956 0.000 0.024 0.008
#&gt; SRR547970     5  0.0000      0.977 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547971     5  0.0451      0.976 0.008 0.000 0.000 0.004 0.988
#&gt; SRR547972     2  0.0671      0.880 0.004 0.980 0.000 0.016 0.000
#&gt; SRR547974     5  0.0000      0.977 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547976     2  0.2054      0.870 0.000 0.920 0.000 0.028 0.052
#&gt; SRR547978     5  0.2067      0.946 0.032 0.000 0.000 0.048 0.920
#&gt; SRR547979     2  0.0992      0.881 0.000 0.968 0.000 0.024 0.008
#&gt; SRR547981     5  0.0000      0.977 0.000 0.000 0.000 0.000 1.000
#&gt; SRR547982     2  0.0162      0.881 0.004 0.996 0.000 0.000 0.000
#&gt; SRR547983     2  0.5237      0.643 0.032 0.684 0.000 0.040 0.244
#&gt; SRR547989     2  0.5237      0.643 0.032 0.684 0.000 0.040 0.244
#&gt; SRR547990     5  0.0162      0.976 0.000 0.000 0.000 0.004 0.996
#&gt; SRR547991     5  0.2562      0.933 0.032 0.008 0.000 0.060 0.900
#&gt; SRR547992     2  0.0404      0.881 0.000 0.988 0.000 0.012 0.000
#&gt; SRR801424     4  0.4835      0.470 0.380 0.000 0.028 0.592 0.000
#&gt; SRR801425     4  0.4045      0.433 0.000 0.000 0.356 0.644 0.000
#&gt; SRR801426     4  0.3424      0.599 0.000 0.000 0.240 0.760 0.000
#&gt; SRR801427     1  0.4300     -0.295 0.524 0.000 0.000 0.476 0.000
#&gt; SRR801428     4  0.4302      0.284 0.480 0.000 0.000 0.520 0.000
#&gt; SRR801429     4  0.4000      0.631 0.016 0.020 0.180 0.784 0.000
#&gt; SRR801430     4  0.4235      0.406 0.424 0.000 0.000 0.576 0.000
#&gt; SRR801431     4  0.3508      0.588 0.000 0.000 0.252 0.748 0.000
#&gt; SRR801432     4  0.3687      0.622 0.000 0.028 0.180 0.792 0.000
#&gt; SRR801433     4  0.4256      0.386 0.436 0.000 0.000 0.564 0.000
#&gt; SRR825135     3  0.1197      0.871 0.000 0.000 0.952 0.048 0.000
#&gt; SRR825136     1  0.0880      0.907 0.968 0.000 0.032 0.000 0.000
#&gt; SRR825137     3  0.0162      0.889 0.000 0.000 0.996 0.004 0.000
#&gt; SRR825139     1  0.0880      0.907 0.968 0.000 0.032 0.000 0.000
#&gt; SRR825140     1  0.0880      0.907 0.968 0.000 0.032 0.000 0.000
#&gt; SRR825141     3  0.0794      0.882 0.000 0.000 0.972 0.028 0.000
#&gt; SRR825143     1  0.0880      0.907 0.968 0.000 0.032 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-4-a').click(function(){
  $('#tab-MAD-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-MAD-NMF-get-classes-5'>
<p><a id='tab-MAD-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR547975     5  0.2362     0.7454 0.000 0.000 0.000 0.004 0.860 0.136
#&gt; SRR547973     2  0.1657     0.7886 0.000 0.928 0.000 0.056 0.000 0.016
#&gt; SRR547968     2  0.0363     0.8205 0.000 0.988 0.000 0.000 0.000 0.012
#&gt; SRR547980     5  0.3993     0.0819 0.000 0.000 0.000 0.004 0.520 0.476
#&gt; SRR545058     3  0.0603     0.8913 0.004 0.000 0.980 0.016 0.000 0.000
#&gt; SRR546225     2  0.4895     0.3754 0.004 0.584 0.364 0.040 0.004 0.004
#&gt; SRR546226     1  0.0146     0.9358 0.996 0.000 0.004 0.000 0.000 0.000
#&gt; SRR546227     1  0.0146     0.9358 0.996 0.000 0.004 0.000 0.000 0.000
#&gt; SRR546228     3  0.0862     0.8909 0.004 0.008 0.972 0.016 0.000 0.000
#&gt; SRR546229     3  0.3795     0.4949 0.004 0.000 0.632 0.364 0.000 0.000
#&gt; SRR546230     1  0.0146     0.9358 0.996 0.000 0.004 0.000 0.000 0.000
#&gt; SRR546231     3  0.0260     0.8868 0.008 0.000 0.992 0.000 0.000 0.000
#&gt; SRR546232     1  0.0547     0.9245 0.980 0.000 0.020 0.000 0.000 0.000
#&gt; SRR546233     1  0.0146     0.9308 0.996 0.000 0.000 0.004 0.000 0.000
#&gt; SRR546234     3  0.2615     0.7976 0.004 0.104 0.872 0.012 0.000 0.008
#&gt; SRR546235     3  0.0858     0.8907 0.004 0.000 0.968 0.028 0.000 0.000
#&gt; SRR546236     3  0.0912     0.8783 0.004 0.008 0.972 0.012 0.000 0.004
#&gt; SRR546237     1  0.2941     0.7174 0.780 0.000 0.220 0.000 0.000 0.000
#&gt; SRR546238     3  0.2212     0.8457 0.000 0.008 0.880 0.112 0.000 0.000
#&gt; SRR546239     1  0.3163     0.6925 0.764 0.000 0.232 0.004 0.000 0.000
#&gt; SRR546240     3  0.4483     0.4992 0.284 0.000 0.668 0.032 0.000 0.016
#&gt; SRR547969     2  0.3684     0.6497 0.000 0.692 0.004 0.004 0.000 0.300
#&gt; SRR547970     5  0.0260     0.7745 0.000 0.000 0.000 0.000 0.992 0.008
#&gt; SRR547971     5  0.3578     0.4538 0.000 0.000 0.000 0.000 0.660 0.340
#&gt; SRR547972     2  0.2416     0.8114 0.000 0.844 0.000 0.000 0.000 0.156
#&gt; SRR547974     5  0.1814     0.7669 0.000 0.000 0.000 0.000 0.900 0.100
#&gt; SRR547976     2  0.1958     0.7879 0.000 0.896 0.000 0.000 0.100 0.004
#&gt; SRR547978     6  0.3476     0.6846 0.000 0.004 0.000 0.004 0.260 0.732
#&gt; SRR547979     2  0.1444     0.8385 0.000 0.928 0.000 0.000 0.000 0.072
#&gt; SRR547981     5  0.0458     0.7610 0.000 0.000 0.000 0.000 0.984 0.016
#&gt; SRR547982     2  0.1957     0.8306 0.000 0.888 0.000 0.000 0.000 0.112
#&gt; SRR547983     6  0.3455     0.7856 0.000 0.092 0.004 0.004 0.076 0.824
#&gt; SRR547989     6  0.3455     0.7856 0.000 0.092 0.004 0.004 0.076 0.824
#&gt; SRR547990     5  0.0547     0.7766 0.000 0.000 0.000 0.000 0.980 0.020
#&gt; SRR547991     6  0.3276     0.7362 0.000 0.004 0.000 0.004 0.228 0.764
#&gt; SRR547992     2  0.1444     0.8388 0.000 0.928 0.000 0.000 0.000 0.072
#&gt; SRR801424     4  0.3337     0.7154 0.260 0.000 0.004 0.736 0.000 0.000
#&gt; SRR801425     4  0.2854     0.5850 0.000 0.000 0.208 0.792 0.000 0.000
#&gt; SRR801426     4  0.1267     0.7226 0.000 0.000 0.060 0.940 0.000 0.000
#&gt; SRR801427     4  0.3810     0.5270 0.428 0.000 0.000 0.572 0.000 0.000
#&gt; SRR801428     4  0.3672     0.6287 0.368 0.000 0.000 0.632 0.000 0.000
#&gt; SRR801429     4  0.1364     0.7258 0.004 0.004 0.048 0.944 0.000 0.000
#&gt; SRR801430     4  0.3547     0.6724 0.332 0.000 0.000 0.668 0.000 0.000
#&gt; SRR801431     4  0.1444     0.7173 0.000 0.000 0.072 0.928 0.000 0.000
#&gt; SRR801432     4  0.1297     0.7222 0.000 0.012 0.040 0.948 0.000 0.000
#&gt; SRR801433     4  0.3515     0.6801 0.324 0.000 0.000 0.676 0.000 0.000
#&gt; SRR825135     3  0.1588     0.8754 0.004 0.000 0.924 0.072 0.000 0.000
#&gt; SRR825136     1  0.0146     0.9358 0.996 0.000 0.004 0.000 0.000 0.000
#&gt; SRR825137     3  0.0508     0.8906 0.004 0.000 0.984 0.012 0.000 0.000
#&gt; SRR825139     1  0.0146     0.9358 0.996 0.000 0.004 0.000 0.000 0.000
#&gt; SRR825140     1  0.0146     0.9358 0.996 0.000 0.004 0.000 0.000 0.000
#&gt; SRR825141     3  0.1349     0.8830 0.004 0.000 0.940 0.056 0.000 0.000
#&gt; SRR825143     1  0.0146     0.9358 0.996 0.000 0.004 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-MAD-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-MAD-NMF-get-classes-5-a').click(function(){
  $('#tab-MAD-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-MAD-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-MAD-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-MAD-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-MAD-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-MAD-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-MAD-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-MAD-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-MAD-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-MAD-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-signatures'>
<ul>
<li><a href='#tab-MAD-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-1-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-1"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-2-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-2"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-3-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-3"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-4-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-4"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-5-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-MAD-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-MAD-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-MAD-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk MAD-NMF-signature_compare](figure_cola/MAD-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-MAD-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-MAD-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-MAD-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-MAD-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-MAD-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-MAD-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-MAD-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-MAD-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk MAD-NMF-collect-classes](figure_cola/MAD-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:hclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "hclust"]
# you can also extract it by
# res = res_list["ATC:hclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'hclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-hclust-collect-plots](figure_cola/ATC-hclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-hclust-select-partition-number](figure_cola/ATC-hclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.713           0.915       0.951         0.4979 0.495   0.495
#> 3 3 0.771           0.846       0.920         0.3180 0.852   0.701
#> 4 4 0.820           0.874       0.896         0.1006 0.931   0.801
#> 5 5 0.933           0.952       0.950         0.0610 0.948   0.812
#> 6 6 0.985           0.922       0.970         0.0304 0.987   0.942
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 5
```

There is also optional best $k$ = 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-hclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-classes'>
<ul>
<li><a href='#tab-ATC-hclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-hclust-get-classes-1'>
<p><a id='tab-ATC-hclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR547975     2   0.000      1.000 0.000 1.000
#&gt; SRR547973     2   0.000      1.000 0.000 1.000
#&gt; SRR547968     2   0.000      1.000 0.000 1.000
#&gt; SRR547980     2   0.000      1.000 0.000 1.000
#&gt; SRR545058     1   0.000      0.901 1.000 0.000
#&gt; SRR546225     1   0.000      0.901 1.000 0.000
#&gt; SRR546226     1   0.000      0.901 1.000 0.000
#&gt; SRR546227     1   0.000      0.901 1.000 0.000
#&gt; SRR546228     1   0.000      0.901 1.000 0.000
#&gt; SRR546229     1   0.204      0.886 0.968 0.032
#&gt; SRR546230     1   0.000      0.901 1.000 0.000
#&gt; SRR546231     1   0.861      0.719 0.716 0.284
#&gt; SRR546232     1   0.000      0.901 1.000 0.000
#&gt; SRR546233     1   0.000      0.901 1.000 0.000
#&gt; SRR546234     1   0.000      0.901 1.000 0.000
#&gt; SRR546235     1   0.861      0.719 0.716 0.284
#&gt; SRR546236     1   0.000      0.901 1.000 0.000
#&gt; SRR546237     1   0.000      0.901 1.000 0.000
#&gt; SRR546238     1   0.000      0.901 1.000 0.000
#&gt; SRR546239     1   0.000      0.901 1.000 0.000
#&gt; SRR546240     1   0.000      0.901 1.000 0.000
#&gt; SRR547969     2   0.000      1.000 0.000 1.000
#&gt; SRR547970     2   0.000      1.000 0.000 1.000
#&gt; SRR547971     2   0.000      1.000 0.000 1.000
#&gt; SRR547972     2   0.000      1.000 0.000 1.000
#&gt; SRR547974     2   0.000      1.000 0.000 1.000
#&gt; SRR547976     2   0.000      1.000 0.000 1.000
#&gt; SRR547978     2   0.000      1.000 0.000 1.000
#&gt; SRR547979     2   0.000      1.000 0.000 1.000
#&gt; SRR547981     2   0.000      1.000 0.000 1.000
#&gt; SRR547982     2   0.000      1.000 0.000 1.000
#&gt; SRR547983     2   0.000      1.000 0.000 1.000
#&gt; SRR547989     2   0.000      1.000 0.000 1.000
#&gt; SRR547990     2   0.000      1.000 0.000 1.000
#&gt; SRR547991     2   0.000      1.000 0.000 1.000
#&gt; SRR547992     2   0.000      1.000 0.000 1.000
#&gt; SRR801424     1   0.861      0.719 0.716 0.284
#&gt; SRR801425     2   0.000      1.000 0.000 1.000
#&gt; SRR801426     2   0.000      1.000 0.000 1.000
#&gt; SRR801427     1   0.861      0.719 0.716 0.284
#&gt; SRR801428     1   0.861      0.719 0.716 0.284
#&gt; SRR801429     2   0.000      1.000 0.000 1.000
#&gt; SRR801430     1   0.861      0.719 0.716 0.284
#&gt; SRR801431     2   0.000      1.000 0.000 1.000
#&gt; SRR801432     2   0.000      1.000 0.000 1.000
#&gt; SRR801433     1   0.861      0.719 0.716 0.284
#&gt; SRR825135     1   0.000      0.901 1.000 0.000
#&gt; SRR825136     1   0.000      0.901 1.000 0.000
#&gt; SRR825137     1   0.861      0.719 0.716 0.284
#&gt; SRR825139     1   0.000      0.901 1.000 0.000
#&gt; SRR825140     1   0.000      0.901 1.000 0.000
#&gt; SRR825141     1   0.861      0.719 0.716 0.284
#&gt; SRR825143     1   0.000      0.901 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-1-a').click(function(){
  $('#tab-ATC-hclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-2'>
<p><a id='tab-ATC-hclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     2   0.000      0.938 0.000 1.000 0.000
#&gt; SRR547973     2   0.000      0.938 0.000 1.000 0.000
#&gt; SRR547968     2   0.000      0.938 0.000 1.000 0.000
#&gt; SRR547980     2   0.000      0.938 0.000 1.000 0.000
#&gt; SRR545058     3   0.543      0.732 0.284 0.000 0.716
#&gt; SRR546225     3   0.543      0.732 0.284 0.000 0.716
#&gt; SRR546226     1   0.000      0.934 1.000 0.000 0.000
#&gt; SRR546227     1   0.000      0.934 1.000 0.000 0.000
#&gt; SRR546228     3   0.543      0.732 0.284 0.000 0.716
#&gt; SRR546229     3   0.514      0.747 0.252 0.000 0.748
#&gt; SRR546230     1   0.000      0.934 1.000 0.000 0.000
#&gt; SRR546231     3   0.000      0.816 0.000 0.000 1.000
#&gt; SRR546232     1   0.000      0.934 1.000 0.000 0.000
#&gt; SRR546233     1   0.608      0.167 0.612 0.000 0.388
#&gt; SRR546234     3   0.543      0.732 0.284 0.000 0.716
#&gt; SRR546235     3   0.000      0.816 0.000 0.000 1.000
#&gt; SRR546236     3   0.543      0.732 0.284 0.000 0.716
#&gt; SRR546237     1   0.000      0.934 1.000 0.000 0.000
#&gt; SRR546238     3   0.543      0.732 0.284 0.000 0.716
#&gt; SRR546239     1   0.000      0.934 1.000 0.000 0.000
#&gt; SRR546240     1   0.000      0.934 1.000 0.000 0.000
#&gt; SRR547969     2   0.000      0.938 0.000 1.000 0.000
#&gt; SRR547970     2   0.000      0.938 0.000 1.000 0.000
#&gt; SRR547971     2   0.000      0.938 0.000 1.000 0.000
#&gt; SRR547972     2   0.000      0.938 0.000 1.000 0.000
#&gt; SRR547974     2   0.000      0.938 0.000 1.000 0.000
#&gt; SRR547976     2   0.000      0.938 0.000 1.000 0.000
#&gt; SRR547978     2   0.000      0.938 0.000 1.000 0.000
#&gt; SRR547979     2   0.000      0.938 0.000 1.000 0.000
#&gt; SRR547981     2   0.000      0.938 0.000 1.000 0.000
#&gt; SRR547982     2   0.000      0.938 0.000 1.000 0.000
#&gt; SRR547983     2   0.000      0.938 0.000 1.000 0.000
#&gt; SRR547989     2   0.000      0.938 0.000 1.000 0.000
#&gt; SRR547990     2   0.000      0.938 0.000 1.000 0.000
#&gt; SRR547991     2   0.000      0.938 0.000 1.000 0.000
#&gt; SRR547992     2   0.000      0.938 0.000 1.000 0.000
#&gt; SRR801424     3   0.000      0.816 0.000 0.000 1.000
#&gt; SRR801425     2   0.543      0.721 0.000 0.716 0.284
#&gt; SRR801426     2   0.543      0.721 0.000 0.716 0.284
#&gt; SRR801427     3   0.000      0.816 0.000 0.000 1.000
#&gt; SRR801428     3   0.000      0.816 0.000 0.000 1.000
#&gt; SRR801429     2   0.543      0.721 0.000 0.716 0.284
#&gt; SRR801430     3   0.000      0.816 0.000 0.000 1.000
#&gt; SRR801431     2   0.543      0.721 0.000 0.716 0.284
#&gt; SRR801432     2   0.543      0.721 0.000 0.716 0.284
#&gt; SRR801433     3   0.000      0.816 0.000 0.000 1.000
#&gt; SRR825135     3   0.543      0.732 0.284 0.000 0.716
#&gt; SRR825136     1   0.435      0.701 0.816 0.000 0.184
#&gt; SRR825137     3   0.000      0.816 0.000 0.000 1.000
#&gt; SRR825139     1   0.000      0.934 1.000 0.000 0.000
#&gt; SRR825140     1   0.000      0.934 1.000 0.000 0.000
#&gt; SRR825141     3   0.000      0.816 0.000 0.000 1.000
#&gt; SRR825143     1   0.000      0.934 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-2-a').click(function(){
  $('#tab-ATC-hclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-3'>
<p><a id='tab-ATC-hclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     2  0.0000      0.988 0.000 1.000 0.000 0.000
#&gt; SRR547973     2  0.3610      0.727 0.000 0.800 0.000 0.200
#&gt; SRR547968     2  0.0000      0.988 0.000 1.000 0.000 0.000
#&gt; SRR547980     2  0.0000      0.988 0.000 1.000 0.000 0.000
#&gt; SRR545058     3  0.4877      0.734 0.000 0.000 0.592 0.408
#&gt; SRR546225     3  0.4877      0.734 0.000 0.000 0.592 0.408
#&gt; SRR546226     1  0.0000      0.934 1.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000      0.934 1.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.4877      0.734 0.000 0.000 0.592 0.408
#&gt; SRR546229     3  0.4776      0.735 0.000 0.000 0.624 0.376
#&gt; SRR546230     1  0.0000      0.934 1.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.0000      0.730 0.000 0.000 1.000 0.000
#&gt; SRR546232     1  0.0000      0.934 1.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.4817      0.318 0.612 0.000 0.388 0.000
#&gt; SRR546234     3  0.4877      0.734 0.000 0.000 0.592 0.408
#&gt; SRR546235     3  0.0188      0.730 0.000 0.000 0.996 0.004
#&gt; SRR546236     3  0.4877      0.734 0.000 0.000 0.592 0.408
#&gt; SRR546237     1  0.0000      0.934 1.000 0.000 0.000 0.000
#&gt; SRR546238     3  0.4877      0.734 0.000 0.000 0.592 0.408
#&gt; SRR546239     1  0.0000      0.934 1.000 0.000 0.000 0.000
#&gt; SRR546240     1  0.0000      0.934 1.000 0.000 0.000 0.000
#&gt; SRR547969     2  0.0000      0.988 0.000 1.000 0.000 0.000
#&gt; SRR547970     2  0.0000      0.988 0.000 1.000 0.000 0.000
#&gt; SRR547971     2  0.0000      0.988 0.000 1.000 0.000 0.000
#&gt; SRR547972     2  0.0000      0.988 0.000 1.000 0.000 0.000
#&gt; SRR547974     2  0.0000      0.988 0.000 1.000 0.000 0.000
#&gt; SRR547976     2  0.0000      0.988 0.000 1.000 0.000 0.000
#&gt; SRR547978     2  0.0000      0.988 0.000 1.000 0.000 0.000
#&gt; SRR547979     2  0.0000      0.988 0.000 1.000 0.000 0.000
#&gt; SRR547981     2  0.0000      0.988 0.000 1.000 0.000 0.000
#&gt; SRR547982     2  0.0000      0.988 0.000 1.000 0.000 0.000
#&gt; SRR547983     2  0.0000      0.988 0.000 1.000 0.000 0.000
#&gt; SRR547989     2  0.0000      0.988 0.000 1.000 0.000 0.000
#&gt; SRR547990     2  0.0000      0.988 0.000 1.000 0.000 0.000
#&gt; SRR547991     2  0.0000      0.988 0.000 1.000 0.000 0.000
#&gt; SRR547992     2  0.0000      0.988 0.000 1.000 0.000 0.000
#&gt; SRR801424     3  0.0000      0.730 0.000 0.000 1.000 0.000
#&gt; SRR801425     4  0.7118      1.000 0.000 0.168 0.284 0.548
#&gt; SRR801426     4  0.7118      1.000 0.000 0.168 0.284 0.548
#&gt; SRR801427     3  0.0000      0.730 0.000 0.000 1.000 0.000
#&gt; SRR801428     3  0.0000      0.730 0.000 0.000 1.000 0.000
#&gt; SRR801429     4  0.7118      1.000 0.000 0.168 0.284 0.548
#&gt; SRR801430     3  0.0000      0.730 0.000 0.000 1.000 0.000
#&gt; SRR801431     4  0.7118      1.000 0.000 0.168 0.284 0.548
#&gt; SRR801432     4  0.7118      1.000 0.000 0.168 0.284 0.548
#&gt; SRR801433     3  0.0000      0.730 0.000 0.000 1.000 0.000
#&gt; SRR825135     3  0.4877      0.734 0.000 0.000 0.592 0.408
#&gt; SRR825136     1  0.3444      0.736 0.816 0.000 0.184 0.000
#&gt; SRR825137     3  0.0000      0.730 0.000 0.000 1.000 0.000
#&gt; SRR825139     1  0.0000      0.934 1.000 0.000 0.000 0.000
#&gt; SRR825140     1  0.0000      0.934 1.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0000      0.730 0.000 0.000 1.000 0.000
#&gt; SRR825143     1  0.0000      0.934 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-3-a').click(function(){
  $('#tab-ATC-hclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-4'>
<p><a id='tab-ATC-hclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1  p2    p3    p4 p5
#&gt; SRR547975     2   0.000      0.990 0.000 1.0 0.000 0.000  0
#&gt; SRR547973     2   0.311      0.792 0.000 0.8 0.000 0.200  0
#&gt; SRR547968     2   0.000      0.990 0.000 1.0 0.000 0.000  0
#&gt; SRR547980     2   0.000      0.990 0.000 1.0 0.000 0.000  0
#&gt; SRR545058     3   0.000      0.994 0.000 0.0 1.000 0.000  0
#&gt; SRR546225     3   0.000      0.994 0.000 0.0 1.000 0.000  0
#&gt; SRR546226     1   0.000      0.941 1.000 0.0 0.000 0.000  0
#&gt; SRR546227     1   0.000      0.941 1.000 0.0 0.000 0.000  0
#&gt; SRR546228     3   0.000      0.994 0.000 0.0 1.000 0.000  0
#&gt; SRR546229     3   0.088      0.956 0.000 0.0 0.968 0.032  0
#&gt; SRR546230     1   0.000      0.941 1.000 0.0 0.000 0.000  0
#&gt; SRR546231     4   0.318      0.960 0.000 0.0 0.208 0.792  0
#&gt; SRR546232     1   0.000      0.941 1.000 0.0 0.000 0.000  0
#&gt; SRR546233     1   0.581      0.381 0.612 0.0 0.208 0.180  0
#&gt; SRR546234     3   0.000      0.994 0.000 0.0 1.000 0.000  0
#&gt; SRR546235     4   0.418      0.656 0.000 0.0 0.400 0.600  0
#&gt; SRR546236     3   0.000      0.994 0.000 0.0 1.000 0.000  0
#&gt; SRR546237     1   0.000      0.941 1.000 0.0 0.000 0.000  0
#&gt; SRR546238     3   0.000      0.994 0.000 0.0 1.000 0.000  0
#&gt; SRR546239     1   0.000      0.941 1.000 0.0 0.000 0.000  0
#&gt; SRR546240     1   0.000      0.941 1.000 0.0 0.000 0.000  0
#&gt; SRR547969     2   0.000      0.990 0.000 1.0 0.000 0.000  0
#&gt; SRR547970     2   0.000      0.990 0.000 1.0 0.000 0.000  0
#&gt; SRR547971     2   0.000      0.990 0.000 1.0 0.000 0.000  0
#&gt; SRR547972     2   0.000      0.990 0.000 1.0 0.000 0.000  0
#&gt; SRR547974     2   0.000      0.990 0.000 1.0 0.000 0.000  0
#&gt; SRR547976     2   0.000      0.990 0.000 1.0 0.000 0.000  0
#&gt; SRR547978     2   0.000      0.990 0.000 1.0 0.000 0.000  0
#&gt; SRR547979     2   0.000      0.990 0.000 1.0 0.000 0.000  0
#&gt; SRR547981     2   0.000      0.990 0.000 1.0 0.000 0.000  0
#&gt; SRR547982     2   0.000      0.990 0.000 1.0 0.000 0.000  0
#&gt; SRR547983     2   0.000      0.990 0.000 1.0 0.000 0.000  0
#&gt; SRR547989     2   0.000      0.990 0.000 1.0 0.000 0.000  0
#&gt; SRR547990     2   0.000      0.990 0.000 1.0 0.000 0.000  0
#&gt; SRR547991     2   0.000      0.990 0.000 1.0 0.000 0.000  0
#&gt; SRR547992     2   0.000      0.990 0.000 1.0 0.000 0.000  0
#&gt; SRR801424     4   0.311      0.963 0.000 0.0 0.200 0.800  0
#&gt; SRR801425     5   0.000      1.000 0.000 0.0 0.000 0.000  1
#&gt; SRR801426     5   0.000      1.000 0.000 0.0 0.000 0.000  1
#&gt; SRR801427     4   0.311      0.963 0.000 0.0 0.200 0.800  0
#&gt; SRR801428     4   0.311      0.963 0.000 0.0 0.200 0.800  0
#&gt; SRR801429     5   0.000      1.000 0.000 0.0 0.000 0.000  1
#&gt; SRR801430     4   0.311      0.963 0.000 0.0 0.200 0.800  0
#&gt; SRR801431     5   0.000      1.000 0.000 0.0 0.000 0.000  1
#&gt; SRR801432     5   0.000      1.000 0.000 0.0 0.000 0.000  1
#&gt; SRR801433     4   0.311      0.963 0.000 0.0 0.200 0.800  0
#&gt; SRR825135     3   0.000      0.994 0.000 0.0 1.000 0.000  0
#&gt; SRR825136     1   0.317      0.772 0.816 0.0 0.008 0.176  0
#&gt; SRR825137     4   0.318      0.960 0.000 0.0 0.208 0.792  0
#&gt; SRR825139     1   0.000      0.941 1.000 0.0 0.000 0.000  0
#&gt; SRR825140     1   0.000      0.941 1.000 0.0 0.000 0.000  0
#&gt; SRR825141     4   0.318      0.960 0.000 0.0 0.208 0.792  0
#&gt; SRR825143     1   0.000      0.941 1.000 0.0 0.000 0.000  0
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-4-a').click(function(){
  $('#tab-ATC-hclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-hclust-get-classes-5'>
<p><a id='tab-ATC-hclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3 p4    p5    p6
#&gt; SRR547975     5  0.0000      0.996 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR547973     2  0.1610      0.000 0.000 0.916 0.000  0 0.084 0.000
#&gt; SRR547968     5  0.0146      0.995 0.000 0.004 0.000  0 0.996 0.000
#&gt; SRR547980     5  0.0000      0.996 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR545058     3  0.0000      0.994 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR546225     3  0.0000      0.994 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR546226     1  0.0000      0.939 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR546227     1  0.0000      0.939 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR546228     3  0.0000      0.994 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR546229     3  0.0790      0.956 0.000 0.000 0.968  0 0.000 0.032
#&gt; SRR546230     1  0.0000      0.939 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR546231     6  0.1610      0.877 0.000 0.084 0.000  0 0.000 0.916
#&gt; SRR546232     1  0.0000      0.939 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR546233     1  0.4859      0.435 0.612 0.084 0.000  0 0.000 0.304
#&gt; SRR546234     3  0.0000      0.994 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR546235     6  0.3747      0.348 0.000 0.000 0.396  0 0.000 0.604
#&gt; SRR546236     3  0.0000      0.994 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR546237     1  0.0000      0.939 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR546238     3  0.0000      0.994 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR546239     1  0.0000      0.939 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR546240     1  0.0000      0.939 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR547969     5  0.0000      0.996 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR547970     5  0.0000      0.996 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR547971     5  0.0000      0.996 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR547972     5  0.0146      0.995 0.000 0.004 0.000  0 0.996 0.000
#&gt; SRR547974     5  0.0146      0.995 0.000 0.004 0.000  0 0.996 0.000
#&gt; SRR547976     5  0.0146      0.995 0.000 0.004 0.000  0 0.996 0.000
#&gt; SRR547978     5  0.0000      0.996 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR547979     5  0.0000      0.996 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR547981     5  0.0937      0.958 0.000 0.040 0.000  0 0.960 0.000
#&gt; SRR547982     5  0.0146      0.995 0.000 0.004 0.000  0 0.996 0.000
#&gt; SRR547983     5  0.0000      0.996 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR547989     5  0.0000      0.996 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR547990     5  0.0000      0.996 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR547991     5  0.0000      0.996 0.000 0.000 0.000  0 1.000 0.000
#&gt; SRR547992     5  0.0146      0.995 0.000 0.004 0.000  0 0.996 0.000
#&gt; SRR801424     6  0.0000      0.900 0.000 0.000 0.000  0 0.000 1.000
#&gt; SRR801425     4  0.0000      1.000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR801426     4  0.0000      1.000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR801427     6  0.0000      0.900 0.000 0.000 0.000  0 0.000 1.000
#&gt; SRR801428     6  0.0000      0.900 0.000 0.000 0.000  0 0.000 1.000
#&gt; SRR801429     4  0.0000      1.000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR801430     6  0.0000      0.900 0.000 0.000 0.000  0 0.000 1.000
#&gt; SRR801431     4  0.0000      1.000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR801432     4  0.0000      1.000 0.000 0.000 0.000  1 0.000 0.000
#&gt; SRR801433     6  0.0000      0.900 0.000 0.000 0.000  0 0.000 1.000
#&gt; SRR825135     3  0.0000      0.994 0.000 0.000 1.000  0 0.000 0.000
#&gt; SRR825136     1  0.3372      0.754 0.816 0.084 0.000  0 0.000 0.100
#&gt; SRR825137     6  0.1610      0.877 0.000 0.084 0.000  0 0.000 0.916
#&gt; SRR825139     1  0.0000      0.939 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR825140     1  0.0000      0.939 1.000 0.000 0.000  0 0.000 0.000
#&gt; SRR825141     6  0.1610      0.877 0.000 0.084 0.000  0 0.000 0.916
#&gt; SRR825143     1  0.0000      0.939 1.000 0.000 0.000  0 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-hclust-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-hclust-get-classes-5-a').click(function(){
  $('#tab-ATC-hclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-hclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-hclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-hclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-hclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-hclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-hclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-hclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-hclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-hclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-signatures'>
<ul>
<li><a href='#tab-ATC-hclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-1-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-1"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-2-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-2"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-3-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-3"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-4-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-4"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-5-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-hclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-hclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-hclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-hclust-signature_compare](figure_cola/ATC-hclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-hclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-hclust-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-hclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-hclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-hclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-hclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-hclust-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-hclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-hclust-collect-classes](figure_cola/ATC-hclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:kmeans**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "kmeans"]
# you can also extract it by
# res = res_list["ATC:kmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'kmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 2.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-kmeans-collect-plots](figure_cola/ATC-kmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-kmeans-select-partition-number](figure_cola/ATC-kmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           0.995       0.993         0.5028 0.495   0.495
#> 3 3 0.710           0.662       0.755         0.2755 0.747   0.528
#> 4 4 0.774           0.872       0.890         0.1318 0.905   0.718
#> 5 5 0.832           0.854       0.827         0.0662 0.973   0.896
#> 6 6 0.785           0.760       0.755         0.0464 0.922   0.675
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 2
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-classes'>
<ul>
<li><a href='#tab-ATC-kmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-kmeans-get-classes-1'>
<p><a id='tab-ATC-kmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR547975     2  0.1184      0.996 0.016 0.984
#&gt; SRR547973     2  0.1184      0.996 0.016 0.984
#&gt; SRR547968     2  0.1184      0.996 0.016 0.984
#&gt; SRR547980     2  0.1184      0.996 0.016 0.984
#&gt; SRR545058     1  0.0000      0.997 1.000 0.000
#&gt; SRR546225     1  0.0000      0.997 1.000 0.000
#&gt; SRR546226     1  0.0000      0.997 1.000 0.000
#&gt; SRR546227     1  0.0000      0.997 1.000 0.000
#&gt; SRR546228     1  0.0000      0.997 1.000 0.000
#&gt; SRR546229     1  0.0000      0.997 1.000 0.000
#&gt; SRR546230     1  0.0000      0.997 1.000 0.000
#&gt; SRR546231     1  0.0672      0.992 0.992 0.008
#&gt; SRR546232     1  0.0000      0.997 1.000 0.000
#&gt; SRR546233     1  0.0000      0.997 1.000 0.000
#&gt; SRR546234     1  0.0000      0.997 1.000 0.000
#&gt; SRR546235     1  0.0000      0.997 1.000 0.000
#&gt; SRR546236     1  0.0000      0.997 1.000 0.000
#&gt; SRR546237     1  0.0000      0.997 1.000 0.000
#&gt; SRR546238     1  0.0000      0.997 1.000 0.000
#&gt; SRR546239     1  0.0000      0.997 1.000 0.000
#&gt; SRR546240     1  0.0000      0.997 1.000 0.000
#&gt; SRR547969     2  0.1184      0.996 0.016 0.984
#&gt; SRR547970     2  0.1184      0.996 0.016 0.984
#&gt; SRR547971     2  0.1184      0.996 0.016 0.984
#&gt; SRR547972     2  0.1184      0.996 0.016 0.984
#&gt; SRR547974     2  0.1184      0.996 0.016 0.984
#&gt; SRR547976     2  0.1184      0.996 0.016 0.984
#&gt; SRR547978     2  0.1184      0.996 0.016 0.984
#&gt; SRR547979     2  0.1184      0.996 0.016 0.984
#&gt; SRR547981     2  0.1184      0.996 0.016 0.984
#&gt; SRR547982     2  0.1184      0.996 0.016 0.984
#&gt; SRR547983     2  0.1184      0.996 0.016 0.984
#&gt; SRR547989     2  0.1184      0.996 0.016 0.984
#&gt; SRR547990     2  0.1184      0.996 0.016 0.984
#&gt; SRR547991     2  0.1184      0.996 0.016 0.984
#&gt; SRR547992     2  0.1184      0.996 0.016 0.984
#&gt; SRR801424     1  0.1184      0.986 0.984 0.016
#&gt; SRR801425     2  0.0000      0.987 0.000 1.000
#&gt; SRR801426     2  0.0000      0.987 0.000 1.000
#&gt; SRR801427     1  0.1184      0.986 0.984 0.016
#&gt; SRR801428     1  0.1184      0.986 0.984 0.016
#&gt; SRR801429     2  0.0000      0.987 0.000 1.000
#&gt; SRR801430     1  0.1184      0.986 0.984 0.016
#&gt; SRR801431     2  0.0000      0.987 0.000 1.000
#&gt; SRR801432     2  0.0000      0.987 0.000 1.000
#&gt; SRR801433     1  0.1184      0.986 0.984 0.016
#&gt; SRR825135     1  0.0000      0.997 1.000 0.000
#&gt; SRR825136     1  0.0000      0.997 1.000 0.000
#&gt; SRR825137     1  0.0000      0.997 1.000 0.000
#&gt; SRR825139     1  0.0000      0.997 1.000 0.000
#&gt; SRR825140     1  0.0000      0.997 1.000 0.000
#&gt; SRR825141     1  0.0000      0.997 1.000 0.000
#&gt; SRR825143     1  0.0000      0.997 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-1-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-2'>
<p><a id='tab-ATC-kmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     2  0.0000     1.0000 0.000 1.000 0.000
#&gt; SRR547973     2  0.0000     1.0000 0.000 1.000 0.000
#&gt; SRR547968     2  0.0000     1.0000 0.000 1.000 0.000
#&gt; SRR547980     2  0.0000     1.0000 0.000 1.000 0.000
#&gt; SRR545058     3  0.0747     0.7333 0.016 0.000 0.984
#&gt; SRR546225     3  0.3038     0.6255 0.104 0.000 0.896
#&gt; SRR546226     1  0.6308     0.4342 0.508 0.000 0.492
#&gt; SRR546227     1  0.6308     0.4342 0.508 0.000 0.492
#&gt; SRR546228     3  0.2448     0.6663 0.076 0.000 0.924
#&gt; SRR546229     3  0.1031     0.7384 0.024 0.000 0.976
#&gt; SRR546230     1  0.6308     0.4342 0.508 0.000 0.492
#&gt; SRR546231     3  0.0592     0.7385 0.012 0.000 0.988
#&gt; SRR546232     1  0.6308     0.4342 0.508 0.000 0.492
#&gt; SRR546233     3  0.4002     0.5365 0.160 0.000 0.840
#&gt; SRR546234     3  0.3816     0.5478 0.148 0.000 0.852
#&gt; SRR546235     3  0.0000     0.7423 0.000 0.000 1.000
#&gt; SRR546236     3  0.0000     0.7423 0.000 0.000 1.000
#&gt; SRR546237     1  0.6308     0.4342 0.508 0.000 0.492
#&gt; SRR546238     3  0.0747     0.7413 0.016 0.000 0.984
#&gt; SRR546239     1  0.6308     0.4342 0.508 0.000 0.492
#&gt; SRR546240     1  0.6308     0.4342 0.508 0.000 0.492
#&gt; SRR547969     2  0.0000     1.0000 0.000 1.000 0.000
#&gt; SRR547970     2  0.0000     1.0000 0.000 1.000 0.000
#&gt; SRR547971     2  0.0000     1.0000 0.000 1.000 0.000
#&gt; SRR547972     2  0.0000     1.0000 0.000 1.000 0.000
#&gt; SRR547974     2  0.0000     1.0000 0.000 1.000 0.000
#&gt; SRR547976     2  0.0000     1.0000 0.000 1.000 0.000
#&gt; SRR547978     2  0.0000     1.0000 0.000 1.000 0.000
#&gt; SRR547979     2  0.0000     1.0000 0.000 1.000 0.000
#&gt; SRR547981     2  0.0000     1.0000 0.000 1.000 0.000
#&gt; SRR547982     2  0.0000     1.0000 0.000 1.000 0.000
#&gt; SRR547983     2  0.0000     1.0000 0.000 1.000 0.000
#&gt; SRR547989     2  0.0000     1.0000 0.000 1.000 0.000
#&gt; SRR547990     2  0.0000     1.0000 0.000 1.000 0.000
#&gt; SRR547991     2  0.0000     1.0000 0.000 1.000 0.000
#&gt; SRR547992     2  0.0000     1.0000 0.000 1.000 0.000
#&gt; SRR801424     3  0.6079     0.4848 0.388 0.000 0.612
#&gt; SRR801425     1  0.8957    -0.0473 0.492 0.376 0.132
#&gt; SRR801426     1  0.8957    -0.0473 0.492 0.376 0.132
#&gt; SRR801427     3  0.5621     0.5428 0.308 0.000 0.692
#&gt; SRR801428     3  0.6079     0.4848 0.388 0.000 0.612
#&gt; SRR801429     1  0.9098    -0.0202 0.492 0.360 0.148
#&gt; SRR801430     3  0.6079     0.4848 0.388 0.000 0.612
#&gt; SRR801431     1  0.9098    -0.0202 0.492 0.360 0.148
#&gt; SRR801432     1  0.8957    -0.0473 0.492 0.376 0.132
#&gt; SRR801433     3  0.6079     0.4848 0.388 0.000 0.612
#&gt; SRR825135     3  0.0892     0.7402 0.020 0.000 0.980
#&gt; SRR825136     1  0.6308     0.4342 0.508 0.000 0.492
#&gt; SRR825137     3  0.0000     0.7423 0.000 0.000 1.000
#&gt; SRR825139     1  0.6308     0.4342 0.508 0.000 0.492
#&gt; SRR825140     1  0.6308     0.4342 0.508 0.000 0.492
#&gt; SRR825141     3  0.0747     0.7333 0.016 0.000 0.984
#&gt; SRR825143     1  0.6308     0.4342 0.508 0.000 0.492
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-2-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-3'>
<p><a id='tab-ATC-kmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     2  0.0895      0.942 0.020 0.976 0.000 0.004
#&gt; SRR547973     2  0.2593      0.937 0.104 0.892 0.000 0.004
#&gt; SRR547968     2  0.2593      0.937 0.104 0.892 0.000 0.004
#&gt; SRR547980     2  0.0895      0.942 0.020 0.976 0.000 0.004
#&gt; SRR545058     3  0.0592      0.906 0.016 0.000 0.984 0.000
#&gt; SRR546225     3  0.0592      0.906 0.016 0.000 0.984 0.000
#&gt; SRR546226     1  0.2921      0.988 0.860 0.000 0.140 0.000
#&gt; SRR546227     1  0.3812      0.986 0.832 0.000 0.140 0.028
#&gt; SRR546228     3  0.0592      0.906 0.016 0.000 0.984 0.000
#&gt; SRR546229     3  0.0592      0.891 0.000 0.000 0.984 0.016
#&gt; SRR546230     1  0.2921      0.988 0.860 0.000 0.140 0.000
#&gt; SRR546231     3  0.1792      0.851 0.000 0.000 0.932 0.068
#&gt; SRR546232     1  0.2921      0.988 0.860 0.000 0.140 0.000
#&gt; SRR546233     3  0.4500      0.446 0.316 0.000 0.684 0.000
#&gt; SRR546234     3  0.1118      0.890 0.036 0.000 0.964 0.000
#&gt; SRR546235     3  0.0336      0.907 0.008 0.000 0.992 0.000
#&gt; SRR546236     3  0.0336      0.907 0.008 0.000 0.992 0.000
#&gt; SRR546237     1  0.3812      0.986 0.832 0.000 0.140 0.028
#&gt; SRR546238     3  0.0804      0.901 0.008 0.000 0.980 0.012
#&gt; SRR546239     1  0.3812      0.986 0.832 0.000 0.140 0.028
#&gt; SRR546240     1  0.3812      0.986 0.832 0.000 0.140 0.028
#&gt; SRR547969     2  0.2530      0.938 0.100 0.896 0.000 0.004
#&gt; SRR547970     2  0.0895      0.942 0.020 0.976 0.000 0.004
#&gt; SRR547971     2  0.0524      0.944 0.008 0.988 0.000 0.004
#&gt; SRR547972     2  0.2466      0.938 0.096 0.900 0.000 0.004
#&gt; SRR547974     2  0.2466      0.940 0.096 0.900 0.000 0.004
#&gt; SRR547976     2  0.2334      0.940 0.088 0.908 0.000 0.004
#&gt; SRR547978     2  0.0895      0.942 0.020 0.976 0.000 0.004
#&gt; SRR547979     2  0.0336      0.945 0.008 0.992 0.000 0.000
#&gt; SRR547981     2  0.2593      0.937 0.104 0.892 0.000 0.004
#&gt; SRR547982     2  0.2593      0.937 0.104 0.892 0.000 0.004
#&gt; SRR547983     2  0.0779      0.943 0.016 0.980 0.000 0.004
#&gt; SRR547989     2  0.0779      0.943 0.016 0.980 0.000 0.004
#&gt; SRR547990     2  0.0895      0.942 0.020 0.976 0.000 0.004
#&gt; SRR547991     2  0.1004      0.942 0.024 0.972 0.000 0.004
#&gt; SRR547992     2  0.2466      0.938 0.096 0.900 0.000 0.004
#&gt; SRR801424     4  0.5149      0.602 0.016 0.000 0.336 0.648
#&gt; SRR801425     4  0.2611      0.776 0.000 0.096 0.008 0.896
#&gt; SRR801426     4  0.2611      0.776 0.000 0.096 0.008 0.896
#&gt; SRR801427     3  0.5444     -0.032 0.016 0.000 0.560 0.424
#&gt; SRR801428     4  0.5149      0.602 0.016 0.000 0.336 0.648
#&gt; SRR801429     4  0.2611      0.776 0.000 0.096 0.008 0.896
#&gt; SRR801430     4  0.5149      0.602 0.016 0.000 0.336 0.648
#&gt; SRR801431     4  0.2611      0.776 0.000 0.096 0.008 0.896
#&gt; SRR801432     4  0.2611      0.776 0.000 0.096 0.008 0.896
#&gt; SRR801433     4  0.5149      0.602 0.016 0.000 0.336 0.648
#&gt; SRR825135     3  0.0927      0.897 0.008 0.000 0.976 0.016
#&gt; SRR825136     1  0.3812      0.986 0.832 0.000 0.140 0.028
#&gt; SRR825137     3  0.0336      0.907 0.008 0.000 0.992 0.000
#&gt; SRR825139     1  0.2921      0.988 0.860 0.000 0.140 0.000
#&gt; SRR825140     1  0.2921      0.988 0.860 0.000 0.140 0.000
#&gt; SRR825141     3  0.0592      0.906 0.016 0.000 0.984 0.000
#&gt; SRR825143     1  0.2921      0.988 0.860 0.000 0.140 0.000
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-3-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-4'>
<p><a id='tab-ATC-kmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR547975     2  0.3438     0.8458 0.000 0.808 0.020 0.000 0.172
#&gt; SRR547973     2  0.4685     0.7410 0.000 0.768 0.028 0.140 0.064
#&gt; SRR547968     2  0.4430     0.7509 0.000 0.784 0.024 0.136 0.056
#&gt; SRR547980     2  0.3438     0.8458 0.000 0.808 0.020 0.000 0.172
#&gt; SRR545058     3  0.1357     0.8794 0.048 0.000 0.948 0.000 0.004
#&gt; SRR546225     3  0.1893     0.8751 0.048 0.000 0.928 0.000 0.024
#&gt; SRR546226     1  0.0000     0.9455 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.3146     0.9224 0.856 0.000 0.000 0.052 0.092
#&gt; SRR546228     3  0.1701     0.8778 0.048 0.000 0.936 0.000 0.016
#&gt; SRR546229     3  0.2788     0.8614 0.040 0.000 0.888 0.008 0.064
#&gt; SRR546230     1  0.0000     0.9455 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.6940    -0.0243 0.040 0.000 0.476 0.352 0.132
#&gt; SRR546232     1  0.0162     0.9451 0.996 0.000 0.000 0.004 0.000
#&gt; SRR546233     3  0.6156     0.4280 0.308 0.000 0.556 0.008 0.128
#&gt; SRR546234     3  0.2321     0.8663 0.056 0.000 0.912 0.008 0.024
#&gt; SRR546235     3  0.2588     0.8671 0.048 0.000 0.892 0.000 0.060
#&gt; SRR546236     3  0.1197     0.8797 0.048 0.000 0.952 0.000 0.000
#&gt; SRR546237     1  0.3146     0.9224 0.856 0.000 0.000 0.052 0.092
#&gt; SRR546238     3  0.1357     0.8795 0.048 0.000 0.948 0.000 0.004
#&gt; SRR546239     1  0.3146     0.9224 0.856 0.000 0.000 0.052 0.092
#&gt; SRR546240     1  0.3146     0.9224 0.856 0.000 0.000 0.052 0.092
#&gt; SRR547969     2  0.2673     0.8100 0.000 0.892 0.016 0.076 0.016
#&gt; SRR547970     2  0.3438     0.8458 0.000 0.808 0.020 0.000 0.172
#&gt; SRR547971     2  0.3123     0.8495 0.000 0.828 0.012 0.000 0.160
#&gt; SRR547972     2  0.1921     0.8234 0.000 0.932 0.012 0.044 0.012
#&gt; SRR547974     2  0.1483     0.8321 0.000 0.952 0.012 0.028 0.008
#&gt; SRR547976     2  0.1356     0.8315 0.000 0.956 0.012 0.028 0.004
#&gt; SRR547978     2  0.3419     0.8449 0.000 0.804 0.016 0.000 0.180
#&gt; SRR547979     2  0.2583     0.8494 0.000 0.864 0.004 0.000 0.132
#&gt; SRR547981     2  0.4538     0.7451 0.000 0.776 0.024 0.140 0.060
#&gt; SRR547982     2  0.4474     0.7481 0.000 0.780 0.024 0.140 0.056
#&gt; SRR547983     2  0.3476     0.8467 0.000 0.804 0.020 0.000 0.176
#&gt; SRR547989     2  0.3476     0.8467 0.000 0.804 0.020 0.000 0.176
#&gt; SRR547990     2  0.3438     0.8458 0.000 0.808 0.020 0.000 0.172
#&gt; SRR547991     2  0.3550     0.8449 0.000 0.796 0.020 0.000 0.184
#&gt; SRR547992     2  0.1921     0.8234 0.000 0.932 0.012 0.044 0.012
#&gt; SRR801424     4  0.3109     0.9300 0.000 0.000 0.200 0.800 0.000
#&gt; SRR801425     5  0.4958     0.9840 0.000 0.036 0.000 0.372 0.592
#&gt; SRR801426     5  0.4958     0.9840 0.000 0.036 0.000 0.372 0.592
#&gt; SRR801427     4  0.4797     0.7539 0.000 0.000 0.296 0.660 0.044
#&gt; SRR801428     4  0.3109     0.9300 0.000 0.000 0.200 0.800 0.000
#&gt; SRR801429     5  0.4856     0.9757 0.000 0.028 0.000 0.388 0.584
#&gt; SRR801430     4  0.3109     0.9300 0.000 0.000 0.200 0.800 0.000
#&gt; SRR801431     5  0.4856     0.9757 0.000 0.028 0.000 0.388 0.584
#&gt; SRR801432     5  0.4958     0.9840 0.000 0.036 0.000 0.372 0.592
#&gt; SRR801433     4  0.3109     0.9300 0.000 0.000 0.200 0.800 0.000
#&gt; SRR825135     3  0.1357     0.8795 0.048 0.000 0.948 0.000 0.004
#&gt; SRR825136     1  0.2067     0.9362 0.920 0.000 0.000 0.048 0.032
#&gt; SRR825137     3  0.2588     0.8671 0.048 0.000 0.892 0.000 0.060
#&gt; SRR825139     1  0.0000     0.9455 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825140     1  0.0000     0.9455 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.2782     0.8661 0.048 0.000 0.880 0.000 0.072
#&gt; SRR825143     1  0.0000     0.9455 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-4-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-kmeans-get-classes-5'>
<p><a id='tab-ATC-kmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR547975     5  0.4144      0.905 0.000 0.360 0.000 0.000 0.620 0.020
#&gt; SRR547973     2  0.3200      0.531 0.000 0.844 0.024 0.004 0.020 0.108
#&gt; SRR547968     2  0.0547      0.661 0.000 0.980 0.000 0.000 0.020 0.000
#&gt; SRR547980     5  0.4144      0.905 0.000 0.360 0.000 0.000 0.620 0.020
#&gt; SRR545058     3  0.1829      0.810 0.008 0.000 0.928 0.000 0.036 0.028
#&gt; SRR546225     3  0.3067      0.779 0.012 0.000 0.860 0.004 0.064 0.060
#&gt; SRR546226     1  0.0291      0.896 0.992 0.000 0.004 0.000 0.000 0.004
#&gt; SRR546227     1  0.3946      0.861 0.752 0.000 0.004 0.000 0.192 0.052
#&gt; SRR546228     3  0.2420      0.812 0.008 0.000 0.900 0.008 0.056 0.028
#&gt; SRR546229     3  0.3334      0.771 0.000 0.000 0.820 0.004 0.052 0.124
#&gt; SRR546230     1  0.0146      0.897 0.996 0.000 0.004 0.000 0.000 0.000
#&gt; SRR546231     6  0.5631      0.124 0.000 0.000 0.344 0.008 0.128 0.520
#&gt; SRR546232     1  0.0405      0.896 0.988 0.000 0.004 0.000 0.000 0.008
#&gt; SRR546233     3  0.7396      0.270 0.272 0.000 0.416 0.008 0.180 0.124
#&gt; SRR546234     3  0.3012      0.801 0.012 0.000 0.864 0.008 0.080 0.036
#&gt; SRR546235     3  0.4161      0.761 0.008 0.000 0.768 0.008 0.068 0.148
#&gt; SRR546236     3  0.0405      0.820 0.008 0.000 0.988 0.000 0.000 0.004
#&gt; SRR546237     1  0.3974      0.861 0.752 0.000 0.004 0.000 0.188 0.056
#&gt; SRR546238     3  0.0767      0.817 0.008 0.000 0.976 0.004 0.012 0.000
#&gt; SRR546239     1  0.4064      0.856 0.740 0.000 0.004 0.000 0.200 0.056
#&gt; SRR546240     1  0.4092      0.856 0.740 0.000 0.004 0.000 0.196 0.060
#&gt; SRR547969     2  0.2473      0.646 0.000 0.856 0.000 0.000 0.136 0.008
#&gt; SRR547970     5  0.4144      0.905 0.000 0.360 0.000 0.000 0.620 0.020
#&gt; SRR547971     5  0.4525      0.717 0.004 0.448 0.008 0.000 0.528 0.012
#&gt; SRR547972     2  0.3192      0.597 0.004 0.776 0.004 0.000 0.216 0.000
#&gt; SRR547974     2  0.4004      0.403 0.004 0.684 0.004 0.000 0.296 0.012
#&gt; SRR547976     2  0.3512      0.471 0.000 0.720 0.000 0.000 0.272 0.008
#&gt; SRR547978     5  0.4353      0.898 0.000 0.360 0.004 0.000 0.612 0.024
#&gt; SRR547979     2  0.4594     -0.462 0.000 0.560 0.004 0.000 0.404 0.032
#&gt; SRR547981     2  0.1109      0.652 0.004 0.964 0.004 0.000 0.016 0.012
#&gt; SRR547982     2  0.0146      0.650 0.000 0.996 0.000 0.000 0.000 0.004
#&gt; SRR547983     5  0.4093      0.877 0.000 0.404 0.000 0.000 0.584 0.012
#&gt; SRR547989     5  0.4093      0.877 0.000 0.404 0.000 0.000 0.584 0.012
#&gt; SRR547990     5  0.4435      0.900 0.004 0.364 0.000 0.000 0.604 0.028
#&gt; SRR547991     5  0.4562      0.877 0.000 0.388 0.004 0.000 0.576 0.032
#&gt; SRR547992     2  0.2979      0.628 0.004 0.804 0.004 0.000 0.188 0.000
#&gt; SRR801424     6  0.5238      0.807 0.000 0.000 0.128 0.292 0.000 0.580
#&gt; SRR801425     4  0.1353      0.975 0.000 0.012 0.000 0.952 0.024 0.012
#&gt; SRR801426     4  0.0984      0.982 0.000 0.012 0.000 0.968 0.012 0.008
#&gt; SRR801427     6  0.4638      0.731 0.000 0.000 0.152 0.156 0.000 0.692
#&gt; SRR801428     6  0.5238      0.807 0.000 0.000 0.128 0.292 0.000 0.580
#&gt; SRR801429     4  0.0363      0.980 0.000 0.012 0.000 0.988 0.000 0.000
#&gt; SRR801430     6  0.5238      0.807 0.000 0.000 0.128 0.292 0.000 0.580
#&gt; SRR801431     4  0.0363      0.980 0.000 0.012 0.000 0.988 0.000 0.000
#&gt; SRR801432     4  0.0725      0.982 0.000 0.012 0.000 0.976 0.012 0.000
#&gt; SRR801433     6  0.5238      0.807 0.000 0.000 0.128 0.292 0.000 0.580
#&gt; SRR825135     3  0.0912      0.817 0.008 0.000 0.972 0.004 0.012 0.004
#&gt; SRR825136     1  0.3242      0.876 0.816 0.000 0.004 0.000 0.148 0.032
#&gt; SRR825137     3  0.4161      0.761 0.008 0.000 0.768 0.008 0.068 0.148
#&gt; SRR825139     1  0.0146      0.897 0.996 0.000 0.004 0.000 0.000 0.000
#&gt; SRR825140     1  0.0291      0.897 0.992 0.000 0.004 0.000 0.000 0.004
#&gt; SRR825141     3  0.4266      0.756 0.008 0.000 0.760 0.008 0.076 0.148
#&gt; SRR825143     1  0.0291      0.896 0.992 0.000 0.004 0.000 0.000 0.004
</code></pre>

<script>
$('#tab-ATC-kmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-kmeans-get-classes-5-a').click(function(){
  $('#tab-ATC-kmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-kmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-kmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-kmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-kmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-kmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-kmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-kmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-signatures'>
<ul>
<li><a href='#tab-ATC-kmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-1-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-1"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-2-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-2"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-3-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-3"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-4-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-4"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-5-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-kmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-kmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-kmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-kmeans-signature_compare](figure_cola/ATC-kmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-kmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-kmeans-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-kmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-kmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-kmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-kmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-kmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-kmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-kmeans-collect-classes](figure_cola/ATC-kmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:skmeans*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "skmeans"]
# you can also extract it by
# res = res_list["ATC:skmeans"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'skmeans' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-skmeans-collect-plots](figure_cola/ATC-skmeans-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-skmeans-select-partition-number](figure_cola/ATC-skmeans-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5056 0.495   0.495
#> 3 3 0.902           0.952       0.963         0.2479 0.826   0.661
#> 4 4 0.848           0.714       0.856         0.1208 0.931   0.807
#> 5 5 0.894           0.813       0.902         0.0576 0.924   0.753
#> 6 6 0.904           0.872       0.909         0.0361 0.931   0.740
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 3
```

There is also optional best $k$ = 2 3 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-classes'>
<ul>
<li><a href='#tab-ATC-skmeans-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-skmeans-get-classes-1'>
<p><a id='tab-ATC-skmeans-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1 p2
#&gt; SRR547975     2       0          1  0  1
#&gt; SRR547973     2       0          1  0  1
#&gt; SRR547968     2       0          1  0  1
#&gt; SRR547980     2       0          1  0  1
#&gt; SRR545058     1       0          1  1  0
#&gt; SRR546225     1       0          1  1  0
#&gt; SRR546226     1       0          1  1  0
#&gt; SRR546227     1       0          1  1  0
#&gt; SRR546228     1       0          1  1  0
#&gt; SRR546229     1       0          1  1  0
#&gt; SRR546230     1       0          1  1  0
#&gt; SRR546231     1       0          1  1  0
#&gt; SRR546232     1       0          1  1  0
#&gt; SRR546233     1       0          1  1  0
#&gt; SRR546234     1       0          1  1  0
#&gt; SRR546235     1       0          1  1  0
#&gt; SRR546236     1       0          1  1  0
#&gt; SRR546237     1       0          1  1  0
#&gt; SRR546238     1       0          1  1  0
#&gt; SRR546239     1       0          1  1  0
#&gt; SRR546240     1       0          1  1  0
#&gt; SRR547969     2       0          1  0  1
#&gt; SRR547970     2       0          1  0  1
#&gt; SRR547971     2       0          1  0  1
#&gt; SRR547972     2       0          1  0  1
#&gt; SRR547974     2       0          1  0  1
#&gt; SRR547976     2       0          1  0  1
#&gt; SRR547978     2       0          1  0  1
#&gt; SRR547979     2       0          1  0  1
#&gt; SRR547981     2       0          1  0  1
#&gt; SRR547982     2       0          1  0  1
#&gt; SRR547983     2       0          1  0  1
#&gt; SRR547989     2       0          1  0  1
#&gt; SRR547990     2       0          1  0  1
#&gt; SRR547991     2       0          1  0  1
#&gt; SRR547992     2       0          1  0  1
#&gt; SRR801424     1       0          1  1  0
#&gt; SRR801425     2       0          1  0  1
#&gt; SRR801426     2       0          1  0  1
#&gt; SRR801427     1       0          1  1  0
#&gt; SRR801428     1       0          1  1  0
#&gt; SRR801429     2       0          1  0  1
#&gt; SRR801430     1       0          1  1  0
#&gt; SRR801431     2       0          1  0  1
#&gt; SRR801432     2       0          1  0  1
#&gt; SRR801433     1       0          1  1  0
#&gt; SRR825135     1       0          1  1  0
#&gt; SRR825136     1       0          1  1  0
#&gt; SRR825137     1       0          1  1  0
#&gt; SRR825139     1       0          1  1  0
#&gt; SRR825140     1       0          1  1  0
#&gt; SRR825141     1       0          1  1  0
#&gt; SRR825143     1       0          1  1  0
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-1-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-2'>
<p><a id='tab-ATC-skmeans-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR547973     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR547968     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR547980     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR545058     1   0.103      0.978 0.976 0.000 0.024
#&gt; SRR546225     1   0.103      0.978 0.976 0.000 0.024
#&gt; SRR546226     1   0.000      0.986 1.000 0.000 0.000
#&gt; SRR546227     1   0.000      0.986 1.000 0.000 0.000
#&gt; SRR546228     1   0.103      0.978 0.976 0.000 0.024
#&gt; SRR546229     1   0.296      0.920 0.900 0.000 0.100
#&gt; SRR546230     1   0.000      0.986 1.000 0.000 0.000
#&gt; SRR546231     1   0.216      0.934 0.936 0.000 0.064
#&gt; SRR546232     1   0.000      0.986 1.000 0.000 0.000
#&gt; SRR546233     1   0.000      0.986 1.000 0.000 0.000
#&gt; SRR546234     1   0.103      0.978 0.976 0.000 0.024
#&gt; SRR546235     1   0.000      0.986 1.000 0.000 0.000
#&gt; SRR546236     1   0.116      0.976 0.972 0.000 0.028
#&gt; SRR546237     1   0.000      0.986 1.000 0.000 0.000
#&gt; SRR546238     1   0.116      0.976 0.972 0.000 0.028
#&gt; SRR546239     1   0.000      0.986 1.000 0.000 0.000
#&gt; SRR546240     1   0.000      0.986 1.000 0.000 0.000
#&gt; SRR547969     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR547970     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR547971     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR547972     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR547974     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR547976     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR547978     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR547979     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR547981     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR547982     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR547983     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR547989     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR547990     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR547991     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR547992     2   0.000      1.000 0.000 1.000 0.000
#&gt; SRR801424     3   0.116      0.823 0.028 0.000 0.972
#&gt; SRR801425     3   0.525      0.790 0.000 0.264 0.736
#&gt; SRR801426     3   0.525      0.790 0.000 0.264 0.736
#&gt; SRR801427     3   0.406      0.716 0.164 0.000 0.836
#&gt; SRR801428     3   0.116      0.823 0.028 0.000 0.972
#&gt; SRR801429     3   0.525      0.790 0.000 0.264 0.736
#&gt; SRR801430     3   0.116      0.823 0.028 0.000 0.972
#&gt; SRR801431     3   0.525      0.790 0.000 0.264 0.736
#&gt; SRR801432     3   0.525      0.790 0.000 0.264 0.736
#&gt; SRR801433     3   0.116      0.823 0.028 0.000 0.972
#&gt; SRR825135     1   0.116      0.976 0.972 0.000 0.028
#&gt; SRR825136     1   0.000      0.986 1.000 0.000 0.000
#&gt; SRR825137     1   0.000      0.986 1.000 0.000 0.000
#&gt; SRR825139     1   0.000      0.986 1.000 0.000 0.000
#&gt; SRR825140     1   0.000      0.986 1.000 0.000 0.000
#&gt; SRR825141     1   0.000      0.986 1.000 0.000 0.000
#&gt; SRR825143     1   0.000      0.986 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-2-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-3'>
<p><a id='tab-ATC-skmeans-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR547973     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR547968     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR547980     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR545058     1   0.499     -0.452 0.520 0.000 0.480 0.000
#&gt; SRR546225     1   0.276      0.619 0.872 0.000 0.128 0.000
#&gt; SRR546226     1   0.000      0.767 1.000 0.000 0.000 0.000
#&gt; SRR546227     1   0.000      0.767 1.000 0.000 0.000 0.000
#&gt; SRR546228     1   0.498     -0.406 0.536 0.000 0.464 0.000
#&gt; SRR546229     3   0.310      0.544 0.140 0.000 0.856 0.004
#&gt; SRR546230     1   0.000      0.767 1.000 0.000 0.000 0.000
#&gt; SRR546231     3   0.476      0.467 0.372 0.000 0.628 0.000
#&gt; SRR546232     1   0.000      0.767 1.000 0.000 0.000 0.000
#&gt; SRR546233     1   0.000      0.767 1.000 0.000 0.000 0.000
#&gt; SRR546234     1   0.253      0.641 0.888 0.000 0.112 0.000
#&gt; SRR546235     1   0.499     -0.460 0.524 0.000 0.476 0.000
#&gt; SRR546236     3   0.493      0.593 0.432 0.000 0.568 0.000
#&gt; SRR546237     1   0.000      0.767 1.000 0.000 0.000 0.000
#&gt; SRR546238     3   0.485      0.646 0.400 0.000 0.600 0.000
#&gt; SRR546239     1   0.000      0.767 1.000 0.000 0.000 0.000
#&gt; SRR546240     1   0.000      0.767 1.000 0.000 0.000 0.000
#&gt; SRR547969     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR547970     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR547971     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR547972     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR547974     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR547976     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR547978     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR547979     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR547981     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR547982     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR547983     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR547989     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR547990     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR547991     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR547992     2   0.000      1.000 0.000 1.000 0.000 0.000
#&gt; SRR801424     4   0.503      0.723 0.004 0.000 0.400 0.596
#&gt; SRR801425     4   0.228      0.749 0.000 0.096 0.000 0.904
#&gt; SRR801426     4   0.228      0.749 0.000 0.096 0.000 0.904
#&gt; SRR801427     4   0.680      0.625 0.100 0.000 0.400 0.500
#&gt; SRR801428     4   0.503      0.723 0.004 0.000 0.400 0.596
#&gt; SRR801429     4   0.228      0.749 0.000 0.096 0.000 0.904
#&gt; SRR801430     4   0.503      0.723 0.004 0.000 0.400 0.596
#&gt; SRR801431     4   0.228      0.749 0.000 0.096 0.000 0.904
#&gt; SRR801432     4   0.228      0.749 0.000 0.096 0.000 0.904
#&gt; SRR801433     4   0.503      0.723 0.004 0.000 0.400 0.596
#&gt; SRR825135     3   0.487      0.644 0.404 0.000 0.596 0.000
#&gt; SRR825136     1   0.000      0.767 1.000 0.000 0.000 0.000
#&gt; SRR825137     1   0.484     -0.239 0.604 0.000 0.396 0.000
#&gt; SRR825139     1   0.000      0.767 1.000 0.000 0.000 0.000
#&gt; SRR825140     1   0.000      0.767 1.000 0.000 0.000 0.000
#&gt; SRR825141     1   0.482     -0.215 0.612 0.000 0.388 0.000
#&gt; SRR825143     1   0.000      0.767 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-3-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-4'>
<p><a id='tab-ATC-skmeans-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5
#&gt; SRR547975     2  0.0000     0.9998 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547973     2  0.0162     0.9964 0.000 0.996 0.004 0.000 0.000
#&gt; SRR547968     2  0.0000     0.9998 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547980     2  0.0000     0.9998 0.000 1.000 0.000 0.000 0.000
#&gt; SRR545058     3  0.6521     0.4268 0.372 0.000 0.476 0.140 0.012
#&gt; SRR546225     1  0.5727     0.3481 0.656 0.000 0.192 0.140 0.012
#&gt; SRR546226     1  0.0000     0.8246 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000     0.8246 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.6460     0.3643 0.404 0.000 0.448 0.140 0.008
#&gt; SRR546229     3  0.2414     0.5866 0.012 0.000 0.900 0.080 0.008
#&gt; SRR546230     1  0.0000     0.8246 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     1  0.6616    -0.0356 0.456 0.000 0.252 0.292 0.000
#&gt; SRR546232     1  0.0000     0.8246 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.0000     0.8246 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546234     1  0.5203     0.4532 0.708 0.000 0.144 0.140 0.008
#&gt; SRR546235     3  0.4949     0.3854 0.368 0.000 0.600 0.028 0.004
#&gt; SRR546236     3  0.4594     0.6818 0.116 0.000 0.764 0.112 0.008
#&gt; SRR546237     1  0.0000     0.8246 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546238     3  0.2741     0.6270 0.004 0.000 0.860 0.132 0.004
#&gt; SRR546239     1  0.0000     0.8246 1.000 0.000 0.000 0.000 0.000
#&gt; SRR546240     1  0.0000     0.8246 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547969     2  0.0000     0.9998 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547970     2  0.0000     0.9998 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547971     2  0.0000     0.9998 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547972     2  0.0000     0.9998 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547974     2  0.0000     0.9998 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547976     2  0.0000     0.9998 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547978     2  0.0000     0.9998 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547979     2  0.0000     0.9998 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547981     2  0.0000     0.9998 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547982     2  0.0000     0.9998 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547983     2  0.0000     0.9998 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547989     2  0.0000     0.9998 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547990     2  0.0000     0.9998 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547991     2  0.0000     0.9998 0.000 1.000 0.000 0.000 0.000
#&gt; SRR547992     2  0.0000     0.9998 0.000 1.000 0.000 0.000 0.000
#&gt; SRR801424     4  0.2891     0.9928 0.000 0.000 0.000 0.824 0.176
#&gt; SRR801425     5  0.0510     1.0000 0.000 0.016 0.000 0.000 0.984
#&gt; SRR801426     5  0.0510     1.0000 0.000 0.016 0.000 0.000 0.984
#&gt; SRR801427     4  0.3224     0.9714 0.016 0.000 0.000 0.824 0.160
#&gt; SRR801428     4  0.2891     0.9928 0.000 0.000 0.000 0.824 0.176
#&gt; SRR801429     5  0.0510     1.0000 0.000 0.016 0.000 0.000 0.984
#&gt; SRR801430     4  0.2891     0.9928 0.000 0.000 0.000 0.824 0.176
#&gt; SRR801431     5  0.0510     1.0000 0.000 0.016 0.000 0.000 0.984
#&gt; SRR801432     5  0.0510     1.0000 0.000 0.016 0.000 0.000 0.984
#&gt; SRR801433     4  0.2891     0.9928 0.000 0.000 0.000 0.824 0.176
#&gt; SRR825135     3  0.1106     0.6377 0.012 0.000 0.964 0.024 0.000
#&gt; SRR825136     1  0.0000     0.8246 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825137     1  0.4905    -0.1574 0.500 0.000 0.476 0.024 0.000
#&gt; SRR825139     1  0.0000     0.8246 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825140     1  0.0000     0.8246 1.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     1  0.4886    -0.0642 0.528 0.000 0.448 0.024 0.000
#&gt; SRR825143     1  0.0000     0.8246 1.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-4-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-skmeans-get-classes-5'>
<p><a id='tab-ATC-skmeans-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5    p6
#&gt; SRR547975     2  0.0000     0.9925 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547973     2  0.0922     0.9823 0.000 0.968 0.024 0.004 0.004 0.000
#&gt; SRR547968     2  0.0603     0.9893 0.000 0.980 0.016 0.000 0.004 0.000
#&gt; SRR547980     2  0.0000     0.9925 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR545058     3  0.4153     0.6160 0.148 0.000 0.752 0.004 0.096 0.000
#&gt; SRR546225     3  0.2996     0.5965 0.228 0.000 0.772 0.000 0.000 0.000
#&gt; SRR546226     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.4252     0.6146 0.188 0.000 0.724 0.000 0.088 0.000
#&gt; SRR546229     5  0.3314     0.2478 0.004 0.000 0.100 0.040 0.840 0.016
#&gt; SRR546230     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546231     5  0.4700     0.6115 0.340 0.000 0.000 0.000 0.600 0.060
#&gt; SRR546232     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546234     3  0.3727     0.4653 0.388 0.000 0.612 0.000 0.000 0.000
#&gt; SRR546235     5  0.4299     0.6177 0.308 0.000 0.040 0.000 0.652 0.000
#&gt; SRR546236     3  0.5048     0.2239 0.036 0.000 0.504 0.020 0.440 0.000
#&gt; SRR546237     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546238     3  0.4857     0.2227 0.000 0.000 0.532 0.060 0.408 0.000
#&gt; SRR546239     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR546240     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR547969     2  0.0146     0.9922 0.000 0.996 0.004 0.000 0.000 0.000
#&gt; SRR547970     2  0.0000     0.9925 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547971     2  0.0000     0.9925 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547972     2  0.0508     0.9897 0.000 0.984 0.012 0.000 0.004 0.000
#&gt; SRR547974     2  0.0405     0.9908 0.000 0.988 0.008 0.000 0.004 0.000
#&gt; SRR547976     2  0.0508     0.9897 0.000 0.984 0.012 0.000 0.004 0.000
#&gt; SRR547978     2  0.0000     0.9925 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547979     2  0.0146     0.9922 0.000 0.996 0.004 0.000 0.000 0.000
#&gt; SRR547981     2  0.0508     0.9898 0.000 0.984 0.012 0.000 0.004 0.000
#&gt; SRR547982     2  0.0603     0.9893 0.000 0.980 0.016 0.000 0.004 0.000
#&gt; SRR547983     2  0.0146     0.9922 0.000 0.996 0.004 0.000 0.000 0.000
#&gt; SRR547989     2  0.0146     0.9922 0.000 0.996 0.004 0.000 0.000 0.000
#&gt; SRR547990     2  0.0000     0.9925 0.000 1.000 0.000 0.000 0.000 0.000
#&gt; SRR547991     2  0.0146     0.9922 0.000 0.996 0.004 0.000 0.000 0.000
#&gt; SRR547992     2  0.0508     0.9897 0.000 0.984 0.012 0.000 0.004 0.000
#&gt; SRR801424     6  0.0000     1.0000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR801425     4  0.1444     1.0000 0.000 0.000 0.000 0.928 0.000 0.072
#&gt; SRR801426     4  0.1444     1.0000 0.000 0.000 0.000 0.928 0.000 0.072
#&gt; SRR801427     6  0.0000     1.0000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR801428     6  0.0000     1.0000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR801429     4  0.1444     1.0000 0.000 0.000 0.000 0.928 0.000 0.072
#&gt; SRR801430     6  0.0000     1.0000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR801431     4  0.1444     1.0000 0.000 0.000 0.000 0.928 0.000 0.072
#&gt; SRR801432     4  0.1444     1.0000 0.000 0.000 0.000 0.928 0.000 0.072
#&gt; SRR801433     6  0.0000     1.0000 0.000 0.000 0.000 0.000 0.000 1.000
#&gt; SRR825135     5  0.4806    -0.0812 0.000 0.000 0.380 0.060 0.560 0.000
#&gt; SRR825136     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR825137     5  0.3847     0.6343 0.348 0.000 0.008 0.000 0.644 0.000
#&gt; SRR825139     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR825140     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
#&gt; SRR825141     5  0.3769     0.6297 0.356 0.000 0.004 0.000 0.640 0.000
#&gt; SRR825143     1  0.0000     1.0000 1.000 0.000 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-skmeans-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-skmeans-get-classes-5-a').click(function(){
  $('#tab-ATC-skmeans-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-skmeans-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-skmeans-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-skmeans-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-skmeans-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-skmeans-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-skmeans-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-skmeans-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-signatures'>
<ul>
<li><a href='#tab-ATC-skmeans-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-1-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-1"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-2-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-2"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-3-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-3"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-4-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-4"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-5-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-skmeans-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-skmeans-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-skmeans-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-skmeans-signature_compare](figure_cola/ATC-skmeans-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-skmeans-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-skmeans-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-skmeans-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-skmeans-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-skmeans-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-skmeans-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-skmeans-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-skmeans-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-skmeans-collect-classes](figure_cola/ATC-skmeans-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:pam**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "pam"]
# you can also extract it by
# res = res_list["ATC:pam"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'pam' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 6.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-pam-collect-plots](figure_cola/ATC-pam-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-pam-select-partition-number](figure_cola/ATC-pam-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.5056 0.495   0.495
#> 3 3 0.779           0.806       0.911         0.3103 0.728   0.501
#> 4 4 0.919           0.884       0.945         0.1154 0.889   0.677
#> 5 5 1.000           0.961       0.985         0.0429 0.970   0.884
#> 6 6 0.969           0.928       0.972         0.0741 0.939   0.735
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 6
#> attr(,"optional")
#> [1] 2 4 5
```

There is also optional best $k$ = 2 4 5 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-pam-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-classes'>
<ul>
<li><a href='#tab-ATC-pam-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-pam-get-classes-1'>
<p><a id='tab-ATC-pam-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette p1 p2
#&gt; SRR547975     2       0          1  0  1
#&gt; SRR547973     2       0          1  0  1
#&gt; SRR547968     2       0          1  0  1
#&gt; SRR547980     2       0          1  0  1
#&gt; SRR545058     1       0          1  1  0
#&gt; SRR546225     1       0          1  1  0
#&gt; SRR546226     1       0          1  1  0
#&gt; SRR546227     1       0          1  1  0
#&gt; SRR546228     1       0          1  1  0
#&gt; SRR546229     1       0          1  1  0
#&gt; SRR546230     1       0          1  1  0
#&gt; SRR546231     1       0          1  1  0
#&gt; SRR546232     1       0          1  1  0
#&gt; SRR546233     1       0          1  1  0
#&gt; SRR546234     1       0          1  1  0
#&gt; SRR546235     1       0          1  1  0
#&gt; SRR546236     1       0          1  1  0
#&gt; SRR546237     1       0          1  1  0
#&gt; SRR546238     1       0          1  1  0
#&gt; SRR546239     1       0          1  1  0
#&gt; SRR546240     1       0          1  1  0
#&gt; SRR547969     2       0          1  0  1
#&gt; SRR547970     2       0          1  0  1
#&gt; SRR547971     2       0          1  0  1
#&gt; SRR547972     2       0          1  0  1
#&gt; SRR547974     2       0          1  0  1
#&gt; SRR547976     2       0          1  0  1
#&gt; SRR547978     2       0          1  0  1
#&gt; SRR547979     2       0          1  0  1
#&gt; SRR547981     2       0          1  0  1
#&gt; SRR547982     2       0          1  0  1
#&gt; SRR547983     2       0          1  0  1
#&gt; SRR547989     2       0          1  0  1
#&gt; SRR547990     2       0          1  0  1
#&gt; SRR547991     2       0          1  0  1
#&gt; SRR547992     2       0          1  0  1
#&gt; SRR801424     1       0          1  1  0
#&gt; SRR801425     2       0          1  0  1
#&gt; SRR801426     2       0          1  0  1
#&gt; SRR801427     1       0          1  1  0
#&gt; SRR801428     1       0          1  1  0
#&gt; SRR801429     2       0          1  0  1
#&gt; SRR801430     1       0          1  1  0
#&gt; SRR801431     2       0          1  0  1
#&gt; SRR801432     2       0          1  0  1
#&gt; SRR801433     1       0          1  1  0
#&gt; SRR825135     1       0          1  1  0
#&gt; SRR825136     1       0          1  1  0
#&gt; SRR825137     1       0          1  1  0
#&gt; SRR825139     1       0          1  1  0
#&gt; SRR825140     1       0          1  1  0
#&gt; SRR825141     1       0          1  1  0
#&gt; SRR825143     1       0          1  1  0
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-1-a').click(function(){
  $('#tab-ATC-pam-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-2'>
<p><a id='tab-ATC-pam-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547973     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547968     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547980     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR545058     3  0.6126      0.385 0.400 0.000 0.600
#&gt; SRR546225     1  0.6111      0.280 0.604 0.000 0.396
#&gt; SRR546226     1  0.0000      0.905 1.000 0.000 0.000
#&gt; SRR546227     1  0.0000      0.905 1.000 0.000 0.000
#&gt; SRR546228     1  0.6126      0.268 0.600 0.000 0.400
#&gt; SRR546229     3  0.5138      0.681 0.252 0.000 0.748
#&gt; SRR546230     1  0.0000      0.905 1.000 0.000 0.000
#&gt; SRR546231     3  0.5138      0.681 0.252 0.000 0.748
#&gt; SRR546232     1  0.0000      0.905 1.000 0.000 0.000
#&gt; SRR546233     1  0.4555      0.690 0.800 0.000 0.200
#&gt; SRR546234     1  0.2165      0.854 0.936 0.000 0.064
#&gt; SRR546235     3  0.5138      0.681 0.252 0.000 0.748
#&gt; SRR546236     3  0.5138      0.681 0.252 0.000 0.748
#&gt; SRR546237     1  0.0000      0.905 1.000 0.000 0.000
#&gt; SRR546238     3  0.5138      0.681 0.252 0.000 0.748
#&gt; SRR546239     1  0.0000      0.905 1.000 0.000 0.000
#&gt; SRR546240     1  0.0000      0.905 1.000 0.000 0.000
#&gt; SRR547969     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547970     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547971     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547972     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547974     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547976     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547978     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547979     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547981     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547982     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547983     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547989     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547990     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547991     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR547992     2  0.0000      1.000 0.000 1.000 0.000
#&gt; SRR801424     3  0.0000      0.730 0.000 0.000 1.000
#&gt; SRR801425     3  0.6126      0.239 0.000 0.400 0.600
#&gt; SRR801426     3  0.6126      0.239 0.000 0.400 0.600
#&gt; SRR801427     3  0.0000      0.730 0.000 0.000 1.000
#&gt; SRR801428     3  0.0000      0.730 0.000 0.000 1.000
#&gt; SRR801429     3  0.0747      0.725 0.000 0.016 0.984
#&gt; SRR801430     3  0.0000      0.730 0.000 0.000 1.000
#&gt; SRR801431     3  0.0747      0.725 0.000 0.016 0.984
#&gt; SRR801432     3  0.6062      0.279 0.000 0.384 0.616
#&gt; SRR801433     3  0.0000      0.730 0.000 0.000 1.000
#&gt; SRR825135     3  0.5138      0.681 0.252 0.000 0.748
#&gt; SRR825136     1  0.0000      0.905 1.000 0.000 0.000
#&gt; SRR825137     3  0.5138      0.681 0.252 0.000 0.748
#&gt; SRR825139     1  0.0000      0.905 1.000 0.000 0.000
#&gt; SRR825140     1  0.0000      0.905 1.000 0.000 0.000
#&gt; SRR825141     3  0.5138      0.681 0.252 0.000 0.748
#&gt; SRR825143     1  0.0000      0.905 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-2-a').click(function(){
  $('#tab-ATC-pam-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-3'>
<p><a id='tab-ATC-pam-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     2  0.0000     0.9878 0.000 1.000 0.000 0.000
#&gt; SRR547973     2  0.3610     0.7797 0.000 0.800 0.000 0.200
#&gt; SRR547968     2  0.1022     0.9614 0.000 0.968 0.000 0.032
#&gt; SRR547980     2  0.0000     0.9878 0.000 1.000 0.000 0.000
#&gt; SRR545058     3  0.0000     0.9500 0.000 0.000 1.000 0.000
#&gt; SRR546225     3  0.0000     0.9500 0.000 0.000 1.000 0.000
#&gt; SRR546226     1  0.0000     0.9699 1.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000     0.9699 1.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.0000     0.9500 0.000 0.000 1.000 0.000
#&gt; SRR546229     3  0.0000     0.9500 0.000 0.000 1.000 0.000
#&gt; SRR546230     1  0.0000     0.9699 1.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.4790     0.0206 0.000 0.000 0.620 0.380
#&gt; SRR546232     1  0.0000     0.9699 1.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.4222     0.5817 0.728 0.000 0.272 0.000
#&gt; SRR546234     3  0.0592     0.9290 0.016 0.000 0.984 0.000
#&gt; SRR546235     3  0.0000     0.9500 0.000 0.000 1.000 0.000
#&gt; SRR546236     3  0.0000     0.9500 0.000 0.000 1.000 0.000
#&gt; SRR546237     1  0.0000     0.9699 1.000 0.000 0.000 0.000
#&gt; SRR546238     3  0.0000     0.9500 0.000 0.000 1.000 0.000
#&gt; SRR546239     1  0.0000     0.9699 1.000 0.000 0.000 0.000
#&gt; SRR546240     1  0.0000     0.9699 1.000 0.000 0.000 0.000
#&gt; SRR547969     2  0.0000     0.9878 0.000 1.000 0.000 0.000
#&gt; SRR547970     2  0.0000     0.9878 0.000 1.000 0.000 0.000
#&gt; SRR547971     2  0.0000     0.9878 0.000 1.000 0.000 0.000
#&gt; SRR547972     2  0.0000     0.9878 0.000 1.000 0.000 0.000
#&gt; SRR547974     2  0.0000     0.9878 0.000 1.000 0.000 0.000
#&gt; SRR547976     2  0.0000     0.9878 0.000 1.000 0.000 0.000
#&gt; SRR547978     2  0.0000     0.9878 0.000 1.000 0.000 0.000
#&gt; SRR547979     2  0.0000     0.9878 0.000 1.000 0.000 0.000
#&gt; SRR547981     2  0.0000     0.9878 0.000 1.000 0.000 0.000
#&gt; SRR547982     2  0.0000     0.9878 0.000 1.000 0.000 0.000
#&gt; SRR547983     2  0.0000     0.9878 0.000 1.000 0.000 0.000
#&gt; SRR547989     2  0.0000     0.9878 0.000 1.000 0.000 0.000
#&gt; SRR547990     2  0.0000     0.9878 0.000 1.000 0.000 0.000
#&gt; SRR547991     2  0.0000     0.9878 0.000 1.000 0.000 0.000
#&gt; SRR547992     2  0.0000     0.9878 0.000 1.000 0.000 0.000
#&gt; SRR801424     4  0.4855     0.5948 0.000 0.000 0.400 0.600
#&gt; SRR801425     4  0.0000     0.7303 0.000 0.000 0.000 1.000
#&gt; SRR801426     4  0.0000     0.7303 0.000 0.000 0.000 1.000
#&gt; SRR801427     4  0.4855     0.5948 0.000 0.000 0.400 0.600
#&gt; SRR801428     4  0.4855     0.5948 0.000 0.000 0.400 0.600
#&gt; SRR801429     4  0.0000     0.7303 0.000 0.000 0.000 1.000
#&gt; SRR801430     4  0.4855     0.5948 0.000 0.000 0.400 0.600
#&gt; SRR801431     4  0.0000     0.7303 0.000 0.000 0.000 1.000
#&gt; SRR801432     4  0.0000     0.7303 0.000 0.000 0.000 1.000
#&gt; SRR801433     4  0.4855     0.5948 0.000 0.000 0.400 0.600
#&gt; SRR825135     3  0.0000     0.9500 0.000 0.000 1.000 0.000
#&gt; SRR825136     1  0.0000     0.9699 1.000 0.000 0.000 0.000
#&gt; SRR825137     3  0.0000     0.9500 0.000 0.000 1.000 0.000
#&gt; SRR825139     1  0.0000     0.9699 1.000 0.000 0.000 0.000
#&gt; SRR825140     1  0.0000     0.9699 1.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0000     0.9500 0.000 0.000 1.000 0.000
#&gt; SRR825143     1  0.0000     0.9699 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-3-a').click(function(){
  $('#tab-ATC-pam-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-4'>
<p><a id='tab-ATC-pam-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette  p1    p2    p3    p4    p5
#&gt; SRR547975     2   0.000      0.987 0.0 1.000 0.000 0.000 0.000
#&gt; SRR547973     2   0.351      0.761 0.0 0.800 0.020 0.000 0.180
#&gt; SRR547968     2   0.088      0.959 0.0 0.968 0.000 0.000 0.032
#&gt; SRR547980     2   0.000      0.987 0.0 1.000 0.000 0.000 0.000
#&gt; SRR545058     3   0.000      1.000 0.0 0.000 1.000 0.000 0.000
#&gt; SRR546225     3   0.000      1.000 0.0 0.000 1.000 0.000 0.000
#&gt; SRR546226     1   0.000      0.979 1.0 0.000 0.000 0.000 0.000
#&gt; SRR546227     1   0.000      0.979 1.0 0.000 0.000 0.000 0.000
#&gt; SRR546228     3   0.000      1.000 0.0 0.000 1.000 0.000 0.000
#&gt; SRR546229     3   0.000      1.000 0.0 0.000 1.000 0.000 0.000
#&gt; SRR546230     1   0.000      0.979 1.0 0.000 0.000 0.000 0.000
#&gt; SRR546231     4   0.409      0.415 0.0 0.000 0.368 0.632 0.000
#&gt; SRR546232     1   0.000      0.979 1.0 0.000 0.000 0.000 0.000
#&gt; SRR546233     1   0.323      0.735 0.8 0.000 0.196 0.004 0.000
#&gt; SRR546234     3   0.000      1.000 0.0 0.000 1.000 0.000 0.000
#&gt; SRR546235     3   0.000      1.000 0.0 0.000 1.000 0.000 0.000
#&gt; SRR546236     3   0.000      1.000 0.0 0.000 1.000 0.000 0.000
#&gt; SRR546237     1   0.000      0.979 1.0 0.000 0.000 0.000 0.000
#&gt; SRR546238     3   0.000      1.000 0.0 0.000 1.000 0.000 0.000
#&gt; SRR546239     1   0.000      0.979 1.0 0.000 0.000 0.000 0.000
#&gt; SRR546240     1   0.000      0.979 1.0 0.000 0.000 0.000 0.000
#&gt; SRR547969     2   0.000      0.987 0.0 1.000 0.000 0.000 0.000
#&gt; SRR547970     2   0.000      0.987 0.0 1.000 0.000 0.000 0.000
#&gt; SRR547971     2   0.000      0.987 0.0 1.000 0.000 0.000 0.000
#&gt; SRR547972     2   0.000      0.987 0.0 1.000 0.000 0.000 0.000
#&gt; SRR547974     2   0.000      0.987 0.0 1.000 0.000 0.000 0.000
#&gt; SRR547976     2   0.000      0.987 0.0 1.000 0.000 0.000 0.000
#&gt; SRR547978     2   0.000      0.987 0.0 1.000 0.000 0.000 0.000
#&gt; SRR547979     2   0.000      0.987 0.0 1.000 0.000 0.000 0.000
#&gt; SRR547981     2   0.000      0.987 0.0 1.000 0.000 0.000 0.000
#&gt; SRR547982     2   0.000      0.987 0.0 1.000 0.000 0.000 0.000
#&gt; SRR547983     2   0.000      0.987 0.0 1.000 0.000 0.000 0.000
#&gt; SRR547989     2   0.000      0.987 0.0 1.000 0.000 0.000 0.000
#&gt; SRR547990     2   0.000      0.987 0.0 1.000 0.000 0.000 0.000
#&gt; SRR547991     2   0.000      0.987 0.0 1.000 0.000 0.000 0.000
#&gt; SRR547992     2   0.000      0.987 0.0 1.000 0.000 0.000 0.000
#&gt; SRR801424     4   0.000      0.906 0.0 0.000 0.000 1.000 0.000
#&gt; SRR801425     5   0.000      1.000 0.0 0.000 0.000 0.000 1.000
#&gt; SRR801426     5   0.000      1.000 0.0 0.000 0.000 0.000 1.000
#&gt; SRR801427     4   0.000      0.906 0.0 0.000 0.000 1.000 0.000
#&gt; SRR801428     4   0.000      0.906 0.0 0.000 0.000 1.000 0.000
#&gt; SRR801429     5   0.000      1.000 0.0 0.000 0.000 0.000 1.000
#&gt; SRR801430     4   0.000      0.906 0.0 0.000 0.000 1.000 0.000
#&gt; SRR801431     5   0.000      1.000 0.0 0.000 0.000 0.000 1.000
#&gt; SRR801432     5   0.000      1.000 0.0 0.000 0.000 0.000 1.000
#&gt; SRR801433     4   0.000      0.906 0.0 0.000 0.000 1.000 0.000
#&gt; SRR825135     3   0.000      1.000 0.0 0.000 1.000 0.000 0.000
#&gt; SRR825136     1   0.000      0.979 1.0 0.000 0.000 0.000 0.000
#&gt; SRR825137     3   0.000      1.000 0.0 0.000 1.000 0.000 0.000
#&gt; SRR825139     1   0.000      0.979 1.0 0.000 0.000 0.000 0.000
#&gt; SRR825140     1   0.000      0.979 1.0 0.000 0.000 0.000 0.000
#&gt; SRR825141     3   0.000      1.000 0.0 0.000 1.000 0.000 0.000
#&gt; SRR825143     1   0.000      0.979 1.0 0.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-4-a').click(function(){
  $('#tab-ATC-pam-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-pam-get-classes-5'>
<p><a id='tab-ATC-pam-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette  p1    p2    p3 p4    p5    p6
#&gt; SRR547975     5   0.000      0.964 0.0 0.000 0.000  0 1.000 0.000
#&gt; SRR547973     2   0.000      0.884 0.0 1.000 0.000  0 0.000 0.000
#&gt; SRR547968     2   0.000      0.884 0.0 1.000 0.000  0 0.000 0.000
#&gt; SRR547980     5   0.000      0.964 0.0 0.000 0.000  0 1.000 0.000
#&gt; SRR545058     3   0.000      1.000 0.0 0.000 1.000  0 0.000 0.000
#&gt; SRR546225     3   0.000      1.000 0.0 0.000 1.000  0 0.000 0.000
#&gt; SRR546226     1   0.000      0.979 1.0 0.000 0.000  0 0.000 0.000
#&gt; SRR546227     1   0.000      0.979 1.0 0.000 0.000  0 0.000 0.000
#&gt; SRR546228     3   0.000      1.000 0.0 0.000 1.000  0 0.000 0.000
#&gt; SRR546229     3   0.000      1.000 0.0 0.000 1.000  0 0.000 0.000
#&gt; SRR546230     1   0.000      0.979 1.0 0.000 0.000  0 0.000 0.000
#&gt; SRR546231     6   0.368      0.405 0.0 0.000 0.372  0 0.000 0.628
#&gt; SRR546232     1   0.000      0.979 1.0 0.000 0.000  0 0.000 0.000
#&gt; SRR546233     1   0.290      0.734 0.8 0.000 0.196  0 0.000 0.004
#&gt; SRR546234     3   0.000      1.000 0.0 0.000 1.000  0 0.000 0.000
#&gt; SRR546235     3   0.000      1.000 0.0 0.000 1.000  0 0.000 0.000
#&gt; SRR546236     3   0.000      1.000 0.0 0.000 1.000  0 0.000 0.000
#&gt; SRR546237     1   0.000      0.979 1.0 0.000 0.000  0 0.000 0.000
#&gt; SRR546238     3   0.000      1.000 0.0 0.000 1.000  0 0.000 0.000
#&gt; SRR546239     1   0.000      0.979 1.0 0.000 0.000  0 0.000 0.000
#&gt; SRR546240     1   0.000      0.979 1.0 0.000 0.000  0 0.000 0.000
#&gt; SRR547969     5   0.150      0.892 0.0 0.076 0.000  0 0.924 0.000
#&gt; SRR547970     5   0.000      0.964 0.0 0.000 0.000  0 1.000 0.000
#&gt; SRR547971     5   0.000      0.964 0.0 0.000 0.000  0 1.000 0.000
#&gt; SRR547972     2   0.279      0.741 0.0 0.800 0.000  0 0.200 0.000
#&gt; SRR547974     2   0.359      0.500 0.0 0.656 0.000  0 0.344 0.000
#&gt; SRR547976     5   0.324      0.591 0.0 0.268 0.000  0 0.732 0.000
#&gt; SRR547978     5   0.000      0.964 0.0 0.000 0.000  0 1.000 0.000
#&gt; SRR547979     5   0.000      0.964 0.0 0.000 0.000  0 1.000 0.000
#&gt; SRR547981     2   0.000      0.884 0.0 1.000 0.000  0 0.000 0.000
#&gt; SRR547982     2   0.000      0.884 0.0 1.000 0.000  0 0.000 0.000
#&gt; SRR547983     5   0.000      0.964 0.0 0.000 0.000  0 1.000 0.000
#&gt; SRR547989     5   0.000      0.964 0.0 0.000 0.000  0 1.000 0.000
#&gt; SRR547990     5   0.000      0.964 0.0 0.000 0.000  0 1.000 0.000
#&gt; SRR547991     5   0.000      0.964 0.0 0.000 0.000  0 1.000 0.000
#&gt; SRR547992     2   0.000      0.884 0.0 1.000 0.000  0 0.000 0.000
#&gt; SRR801424     6   0.000      0.904 0.0 0.000 0.000  0 0.000 1.000
#&gt; SRR801425     4   0.000      1.000 0.0 0.000 0.000  1 0.000 0.000
#&gt; SRR801426     4   0.000      1.000 0.0 0.000 0.000  1 0.000 0.000
#&gt; SRR801427     6   0.000      0.904 0.0 0.000 0.000  0 0.000 1.000
#&gt; SRR801428     6   0.000      0.904 0.0 0.000 0.000  0 0.000 1.000
#&gt; SRR801429     4   0.000      1.000 0.0 0.000 0.000  1 0.000 0.000
#&gt; SRR801430     6   0.000      0.904 0.0 0.000 0.000  0 0.000 1.000
#&gt; SRR801431     4   0.000      1.000 0.0 0.000 0.000  1 0.000 0.000
#&gt; SRR801432     4   0.000      1.000 0.0 0.000 0.000  1 0.000 0.000
#&gt; SRR801433     6   0.000      0.904 0.0 0.000 0.000  0 0.000 1.000
#&gt; SRR825135     3   0.000      1.000 0.0 0.000 1.000  0 0.000 0.000
#&gt; SRR825136     1   0.000      0.979 1.0 0.000 0.000  0 0.000 0.000
#&gt; SRR825137     3   0.000      1.000 0.0 0.000 1.000  0 0.000 0.000
#&gt; SRR825139     1   0.000      0.979 1.0 0.000 0.000  0 0.000 0.000
#&gt; SRR825140     1   0.000      0.979 1.0 0.000 0.000  0 0.000 0.000
#&gt; SRR825141     3   0.000      1.000 0.0 0.000 1.000  0 0.000 0.000
#&gt; SRR825143     1   0.000      0.979 1.0 0.000 0.000  0 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-pam-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-pam-get-classes-5-a').click(function(){
  $('#tab-ATC-pam-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-pam-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-pam-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-pam-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-pam-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-pam-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-pam-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-pam-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-pam-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-pam-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-signatures'>
<ul>
<li><a href='#tab-ATC-pam-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-1-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-1"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-2-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-2"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-3-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-3"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-4-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-4"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-5-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-pam-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-pam-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-pam-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-pam-signature_compare](figure_cola/ATC-pam-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-pam-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-pam-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-pam-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-pam-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-pam-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-pam-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-pam-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-pam-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-pam-collect-classes](figure_cola/ATC-pam-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:mclust**






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "mclust"]
# you can also extract it by
# res = res_list["ATC:mclust"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'mclust' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 4.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-mclust-collect-plots](figure_cola/ATC-mclust-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-mclust-select-partition-number](figure_cola/ATC-mclust-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 1.000           1.000       1.000         0.4694 0.531   0.531
#> 3 3 0.793           0.879       0.885         0.3550 0.826   0.672
#> 4 4 0.976           0.920       0.969         0.1729 0.898   0.715
#> 5 5 0.839           0.883       0.897         0.0435 1.000   1.000
#> 6 6 0.850           0.829       0.885         0.0289 0.936   0.770
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 4
#> attr(,"optional")
#> [1] 2
```

There is also optional best $k$ = 2 that is worth to check.

Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-mclust-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-classes'>
<ul>
<li><a href='#tab-ATC-mclust-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-mclust-get-classes-1'>
<p><a id='tab-ATC-mclust-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR547975     2  0.0000      1.000 0.000 1.000
#&gt; SRR547973     2  0.0000      1.000 0.000 1.000
#&gt; SRR547968     2  0.0000      1.000 0.000 1.000
#&gt; SRR547980     2  0.0000      1.000 0.000 1.000
#&gt; SRR545058     1  0.0000      1.000 1.000 0.000
#&gt; SRR546225     1  0.0376      0.996 0.996 0.004
#&gt; SRR546226     1  0.0000      1.000 1.000 0.000
#&gt; SRR546227     1  0.0000      1.000 1.000 0.000
#&gt; SRR546228     1  0.0000      1.000 1.000 0.000
#&gt; SRR546229     1  0.0000      1.000 1.000 0.000
#&gt; SRR546230     1  0.0000      1.000 1.000 0.000
#&gt; SRR546231     1  0.0000      1.000 1.000 0.000
#&gt; SRR546232     1  0.0000      1.000 1.000 0.000
#&gt; SRR546233     1  0.0000      1.000 1.000 0.000
#&gt; SRR546234     1  0.0000      1.000 1.000 0.000
#&gt; SRR546235     1  0.0000      1.000 1.000 0.000
#&gt; SRR546236     1  0.0000      1.000 1.000 0.000
#&gt; SRR546237     1  0.0000      1.000 1.000 0.000
#&gt; SRR546238     1  0.0000      1.000 1.000 0.000
#&gt; SRR546239     1  0.0000      1.000 1.000 0.000
#&gt; SRR546240     1  0.0000      1.000 1.000 0.000
#&gt; SRR547969     2  0.0000      1.000 0.000 1.000
#&gt; SRR547970     2  0.0000      1.000 0.000 1.000
#&gt; SRR547971     2  0.0000      1.000 0.000 1.000
#&gt; SRR547972     2  0.0000      1.000 0.000 1.000
#&gt; SRR547974     2  0.0000      1.000 0.000 1.000
#&gt; SRR547976     2  0.0000      1.000 0.000 1.000
#&gt; SRR547978     2  0.0000      1.000 0.000 1.000
#&gt; SRR547979     2  0.0000      1.000 0.000 1.000
#&gt; SRR547981     2  0.0000      1.000 0.000 1.000
#&gt; SRR547982     2  0.0000      1.000 0.000 1.000
#&gt; SRR547983     2  0.0000      1.000 0.000 1.000
#&gt; SRR547989     2  0.0000      1.000 0.000 1.000
#&gt; SRR547990     2  0.0000      1.000 0.000 1.000
#&gt; SRR547991     2  0.0000      1.000 0.000 1.000
#&gt; SRR547992     2  0.0000      1.000 0.000 1.000
#&gt; SRR801424     1  0.0000      1.000 1.000 0.000
#&gt; SRR801425     1  0.0000      1.000 1.000 0.000
#&gt; SRR801426     1  0.0000      1.000 1.000 0.000
#&gt; SRR801427     1  0.0000      1.000 1.000 0.000
#&gt; SRR801428     1  0.0000      1.000 1.000 0.000
#&gt; SRR801429     1  0.0000      1.000 1.000 0.000
#&gt; SRR801430     1  0.0000      1.000 1.000 0.000
#&gt; SRR801431     1  0.0000      1.000 1.000 0.000
#&gt; SRR801432     1  0.0000      1.000 1.000 0.000
#&gt; SRR801433     1  0.0000      1.000 1.000 0.000
#&gt; SRR825135     1  0.0000      1.000 1.000 0.000
#&gt; SRR825136     1  0.0000      1.000 1.000 0.000
#&gt; SRR825137     1  0.0000      1.000 1.000 0.000
#&gt; SRR825139     1  0.0000      1.000 1.000 0.000
#&gt; SRR825140     1  0.0000      1.000 1.000 0.000
#&gt; SRR825141     1  0.0000      1.000 1.000 0.000
#&gt; SRR825143     1  0.0000      1.000 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-1-a').click(function(){
  $('#tab-ATC-mclust-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-2'>
<p><a id='tab-ATC-mclust-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547973     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547968     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547980     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR545058     1  0.6095      0.743 0.608 0.000 0.392
#&gt; SRR546225     1  0.5678      0.759 0.684 0.000 0.316
#&gt; SRR546226     1  0.0424      0.708 0.992 0.000 0.008
#&gt; SRR546227     1  0.0424      0.708 0.992 0.000 0.008
#&gt; SRR546228     1  0.6095      0.743 0.608 0.000 0.392
#&gt; SRR546229     1  0.5678      0.759 0.684 0.000 0.316
#&gt; SRR546230     1  0.0424      0.708 0.992 0.000 0.008
#&gt; SRR546231     1  0.5706      0.758 0.680 0.000 0.320
#&gt; SRR546232     1  0.0424      0.708 0.992 0.000 0.008
#&gt; SRR546233     1  0.5733      0.755 0.676 0.000 0.324
#&gt; SRR546234     1  0.6095      0.743 0.608 0.000 0.392
#&gt; SRR546235     1  0.5678      0.759 0.684 0.000 0.316
#&gt; SRR546236     1  0.6095      0.743 0.608 0.000 0.392
#&gt; SRR546237     1  0.5706      0.758 0.680 0.000 0.320
#&gt; SRR546238     1  0.6095      0.743 0.608 0.000 0.392
#&gt; SRR546239     1  0.0424      0.708 0.992 0.000 0.008
#&gt; SRR546240     1  0.5706      0.758 0.680 0.000 0.320
#&gt; SRR547969     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547970     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547971     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547972     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547974     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547976     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547978     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547979     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547981     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547982     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547983     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547989     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547990     2  0.1267      0.967 0.004 0.972 0.024
#&gt; SRR547991     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR547992     2  0.0000      0.998 0.000 1.000 0.000
#&gt; SRR801424     3  0.2448      1.000 0.076 0.000 0.924
#&gt; SRR801425     3  0.2448      1.000 0.076 0.000 0.924
#&gt; SRR801426     3  0.2448      1.000 0.076 0.000 0.924
#&gt; SRR801427     3  0.2448      1.000 0.076 0.000 0.924
#&gt; SRR801428     3  0.2448      1.000 0.076 0.000 0.924
#&gt; SRR801429     3  0.2448      1.000 0.076 0.000 0.924
#&gt; SRR801430     3  0.2448      1.000 0.076 0.000 0.924
#&gt; SRR801431     3  0.2448      1.000 0.076 0.000 0.924
#&gt; SRR801432     3  0.2448      1.000 0.076 0.000 0.924
#&gt; SRR801433     3  0.2448      1.000 0.076 0.000 0.924
#&gt; SRR825135     1  0.6095      0.743 0.608 0.000 0.392
#&gt; SRR825136     1  0.0424      0.708 0.992 0.000 0.008
#&gt; SRR825137     1  0.5678      0.759 0.684 0.000 0.316
#&gt; SRR825139     1  0.0424      0.708 0.992 0.000 0.008
#&gt; SRR825140     1  0.0424      0.708 0.992 0.000 0.008
#&gt; SRR825141     1  0.5678      0.759 0.684 0.000 0.316
#&gt; SRR825143     1  0.0424      0.708 0.992 0.000 0.008
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-2-a').click(function(){
  $('#tab-ATC-mclust-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-3'>
<p><a id='tab-ATC-mclust-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR547973     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR547968     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR547980     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR545058     3  0.0000      0.924 0.000 0.000 1.000 0.000
#&gt; SRR546225     3  0.0000      0.924 0.000 0.000 1.000 0.000
#&gt; SRR546226     1  0.0000      0.960 1.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0000      0.960 1.000 0.000 0.000 0.000
#&gt; SRR546228     3  0.0000      0.924 0.000 0.000 1.000 0.000
#&gt; SRR546229     3  0.0000      0.924 0.000 0.000 1.000 0.000
#&gt; SRR546230     1  0.0000      0.960 1.000 0.000 0.000 0.000
#&gt; SRR546231     3  0.1975      0.876 0.016 0.000 0.936 0.048
#&gt; SRR546232     1  0.0000      0.960 1.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.4585      0.461 0.668 0.000 0.332 0.000
#&gt; SRR546234     3  0.0000      0.924 0.000 0.000 1.000 0.000
#&gt; SRR546235     3  0.0000      0.924 0.000 0.000 1.000 0.000
#&gt; SRR546236     3  0.0000      0.924 0.000 0.000 1.000 0.000
#&gt; SRR546237     3  0.4933      0.272 0.432 0.000 0.568 0.000
#&gt; SRR546238     3  0.0000      0.924 0.000 0.000 1.000 0.000
#&gt; SRR546239     1  0.0000      0.960 1.000 0.000 0.000 0.000
#&gt; SRR546240     3  0.4933      0.272 0.432 0.000 0.568 0.000
#&gt; SRR547969     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR547970     2  0.0469      0.970 0.000 0.988 0.012 0.000
#&gt; SRR547971     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR547972     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR547974     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR547976     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR547978     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR547979     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR547981     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR547982     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR547983     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR547989     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR547990     2  0.4431      0.548 0.000 0.696 0.304 0.000
#&gt; SRR547991     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR547992     2  0.0000      0.981 0.000 1.000 0.000 0.000
#&gt; SRR801424     4  0.0000      0.994 0.000 0.000 0.000 1.000
#&gt; SRR801425     4  0.1118      0.959 0.000 0.000 0.036 0.964
#&gt; SRR801426     4  0.0000      0.994 0.000 0.000 0.000 1.000
#&gt; SRR801427     4  0.0469      0.984 0.012 0.000 0.000 0.988
#&gt; SRR801428     4  0.0000      0.994 0.000 0.000 0.000 1.000
#&gt; SRR801429     4  0.0000      0.994 0.000 0.000 0.000 1.000
#&gt; SRR801430     4  0.0000      0.994 0.000 0.000 0.000 1.000
#&gt; SRR801431     4  0.0000      0.994 0.000 0.000 0.000 1.000
#&gt; SRR801432     4  0.0000      0.994 0.000 0.000 0.000 1.000
#&gt; SRR801433     4  0.0000      0.994 0.000 0.000 0.000 1.000
#&gt; SRR825135     3  0.0000      0.924 0.000 0.000 1.000 0.000
#&gt; SRR825136     1  0.0000      0.960 1.000 0.000 0.000 0.000
#&gt; SRR825137     3  0.0000      0.924 0.000 0.000 1.000 0.000
#&gt; SRR825139     1  0.0000      0.960 1.000 0.000 0.000 0.000
#&gt; SRR825140     1  0.0000      0.960 1.000 0.000 0.000 0.000
#&gt; SRR825141     3  0.0000      0.924 0.000 0.000 1.000 0.000
#&gt; SRR825143     1  0.0000      0.960 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-3-a').click(function(){
  $('#tab-ATC-mclust-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-4'>
<p><a id='tab-ATC-mclust-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4 p5
#&gt; SRR547975     2  0.2605      0.871 0.000 0.852 0.000 0.000 NA
#&gt; SRR547973     2  0.2690      0.842 0.000 0.844 0.000 0.000 NA
#&gt; SRR547968     2  0.0963      0.887 0.000 0.964 0.000 0.000 NA
#&gt; SRR547980     2  0.0510      0.894 0.000 0.984 0.000 0.000 NA
#&gt; SRR545058     3  0.1638      0.899 0.004 0.000 0.932 0.000 NA
#&gt; SRR546225     3  0.3689      0.835 0.004 0.000 0.740 0.000 NA
#&gt; SRR546226     1  0.0162      0.962 0.996 0.000 0.000 0.000 NA
#&gt; SRR546227     1  0.0404      0.960 0.988 0.000 0.012 0.000 NA
#&gt; SRR546228     3  0.1704      0.898 0.004 0.000 0.928 0.000 NA
#&gt; SRR546229     3  0.2077      0.902 0.040 0.000 0.920 0.000 NA
#&gt; SRR546230     1  0.0000      0.963 1.000 0.000 0.000 0.000 NA
#&gt; SRR546231     3  0.3299      0.853 0.108 0.000 0.848 0.040 NA
#&gt; SRR546232     1  0.0000      0.963 1.000 0.000 0.000 0.000 NA
#&gt; SRR546233     1  0.3684      0.611 0.720 0.000 0.280 0.000 NA
#&gt; SRR546234     3  0.3550      0.845 0.004 0.000 0.760 0.000 NA
#&gt; SRR546235     3  0.1043      0.899 0.040 0.000 0.960 0.000 NA
#&gt; SRR546236     3  0.0798      0.903 0.008 0.000 0.976 0.000 NA
#&gt; SRR546237     3  0.4845      0.784 0.128 0.000 0.724 0.000 NA
#&gt; SRR546238     3  0.1357      0.901 0.004 0.000 0.948 0.000 NA
#&gt; SRR546239     1  0.0404      0.960 0.988 0.000 0.012 0.000 NA
#&gt; SRR546240     3  0.4845      0.784 0.128 0.000 0.724 0.000 NA
#&gt; SRR547969     2  0.0404      0.894 0.000 0.988 0.000 0.000 NA
#&gt; SRR547970     2  0.4088      0.721 0.000 0.632 0.000 0.000 NA
#&gt; SRR547971     2  0.2561      0.872 0.000 0.856 0.000 0.000 NA
#&gt; SRR547972     2  0.4101      0.747 0.000 0.628 0.000 0.000 NA
#&gt; SRR547974     2  0.2690      0.871 0.000 0.844 0.000 0.000 NA
#&gt; SRR547976     2  0.0162      0.893 0.000 0.996 0.000 0.000 NA
#&gt; SRR547978     2  0.0609      0.893 0.000 0.980 0.000 0.000 NA
#&gt; SRR547979     2  0.1197      0.884 0.000 0.952 0.000 0.000 NA
#&gt; SRR547981     2  0.3336      0.850 0.000 0.772 0.000 0.000 NA
#&gt; SRR547982     2  0.1478      0.892 0.000 0.936 0.000 0.000 NA
#&gt; SRR547983     2  0.0404      0.893 0.000 0.988 0.000 0.000 NA
#&gt; SRR547989     2  0.0404      0.893 0.000 0.988 0.000 0.000 NA
#&gt; SRR547990     2  0.5853      0.560 0.000 0.472 0.096 0.000 NA
#&gt; SRR547991     2  0.1197      0.884 0.000 0.952 0.000 0.000 NA
#&gt; SRR547992     2  0.2929      0.864 0.000 0.820 0.000 0.000 NA
#&gt; SRR801424     4  0.2852      0.922 0.000 0.000 0.000 0.828 NA
#&gt; SRR801425     4  0.0162      0.924 0.000 0.000 0.004 0.996 NA
#&gt; SRR801426     4  0.0000      0.926 0.000 0.000 0.000 1.000 NA
#&gt; SRR801427     4  0.3921      0.895 0.044 0.000 0.000 0.784 NA
#&gt; SRR801428     4  0.2852      0.922 0.000 0.000 0.000 0.828 NA
#&gt; SRR801429     4  0.0000      0.926 0.000 0.000 0.000 1.000 NA
#&gt; SRR801430     4  0.2852      0.922 0.000 0.000 0.000 0.828 NA
#&gt; SRR801431     4  0.0000      0.926 0.000 0.000 0.000 1.000 NA
#&gt; SRR801432     4  0.0000      0.926 0.000 0.000 0.000 1.000 NA
#&gt; SRR801433     4  0.2852      0.922 0.000 0.000 0.000 0.828 NA
#&gt; SRR825135     3  0.1704      0.898 0.004 0.000 0.928 0.000 NA
#&gt; SRR825136     1  0.0290      0.961 0.992 0.000 0.008 0.000 NA
#&gt; SRR825137     3  0.1043      0.899 0.040 0.000 0.960 0.000 NA
#&gt; SRR825139     1  0.0000      0.963 1.000 0.000 0.000 0.000 NA
#&gt; SRR825140     1  0.0162      0.963 0.996 0.000 0.004 0.000 NA
#&gt; SRR825141     3  0.1043      0.899 0.040 0.000 0.960 0.000 NA
#&gt; SRR825143     1  0.0162      0.962 0.996 0.000 0.000 0.000 NA
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-4-a').click(function(){
  $('#tab-ATC-mclust-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-mclust-get-classes-5'>
<p><a id='tab-ATC-mclust-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5 p6
#&gt; SRR547975     2  0.1501     0.8589 0.000 0.924 0.000 0.000 0.000 NA
#&gt; SRR547973     2  0.3862     0.5135 0.000 0.524 0.000 0.000 0.000 NA
#&gt; SRR547968     2  0.2340     0.8263 0.000 0.852 0.000 0.000 0.000 NA
#&gt; SRR547980     2  0.1910     0.8471 0.000 0.892 0.000 0.000 0.000 NA
#&gt; SRR545058     3  0.0000     0.8794 0.000 0.000 1.000 0.000 0.000 NA
#&gt; SRR546225     3  0.1951     0.8456 0.000 0.000 0.908 0.016 0.000 NA
#&gt; SRR546226     1  0.0000     0.8942 1.000 0.000 0.000 0.000 0.000 NA
#&gt; SRR546227     1  0.0146     0.8931 0.996 0.000 0.000 0.000 0.000 NA
#&gt; SRR546228     3  0.0000     0.8794 0.000 0.000 1.000 0.000 0.000 NA
#&gt; SRR546229     3  0.2164     0.8669 0.000 0.000 0.900 0.068 0.000 NA
#&gt; SRR546230     1  0.0000     0.8942 1.000 0.000 0.000 0.000 0.000 NA
#&gt; SRR546231     3  0.5497     0.5673 0.012 0.000 0.632 0.068 0.256 NA
#&gt; SRR546232     1  0.0000     0.8942 1.000 0.000 0.000 0.000 0.000 NA
#&gt; SRR546233     3  0.5447     0.0655 0.452 0.000 0.468 0.020 0.004 NA
#&gt; SRR546234     3  0.1951     0.8456 0.000 0.000 0.908 0.016 0.000 NA
#&gt; SRR546235     3  0.2350     0.8655 0.000 0.000 0.888 0.076 0.000 NA
#&gt; SRR546236     3  0.0291     0.8797 0.000 0.000 0.992 0.004 0.000 NA
#&gt; SRR546237     1  0.5778     0.3128 0.552 0.000 0.320 0.088 0.000 NA
#&gt; SRR546238     3  0.0405     0.8796 0.000 0.000 0.988 0.004 0.000 NA
#&gt; SRR546239     1  0.0146     0.8931 0.996 0.000 0.000 0.000 0.000 NA
#&gt; SRR546240     1  0.6269     0.2546 0.512 0.000 0.320 0.088 0.000 NA
#&gt; SRR547969     2  0.1714     0.8429 0.000 0.908 0.000 0.000 0.000 NA
#&gt; SRR547970     2  0.3747     0.6357 0.000 0.604 0.000 0.000 0.000 NA
#&gt; SRR547971     2  0.1007     0.8593 0.000 0.956 0.000 0.000 0.000 NA
#&gt; SRR547972     2  0.2048     0.8398 0.000 0.880 0.000 0.000 0.000 NA
#&gt; SRR547974     2  0.1007     0.8598 0.000 0.956 0.000 0.000 0.000 NA
#&gt; SRR547976     2  0.0000     0.8603 0.000 1.000 0.000 0.000 0.000 NA
#&gt; SRR547978     2  0.2048     0.8438 0.000 0.880 0.000 0.000 0.000 NA
#&gt; SRR547979     2  0.1007     0.8588 0.000 0.956 0.000 0.000 0.000 NA
#&gt; SRR547981     2  0.3482     0.7146 0.000 0.684 0.000 0.000 0.000 NA
#&gt; SRR547982     2  0.3266     0.7255 0.000 0.728 0.000 0.000 0.000 NA
#&gt; SRR547983     2  0.2003     0.8447 0.000 0.884 0.000 0.000 0.000 NA
#&gt; SRR547989     2  0.2003     0.8447 0.000 0.884 0.000 0.000 0.000 NA
#&gt; SRR547990     2  0.3684     0.6536 0.000 0.628 0.000 0.000 0.000 NA
#&gt; SRR547991     2  0.1007     0.8590 0.000 0.956 0.000 0.000 0.000 NA
#&gt; SRR547992     2  0.1075     0.8594 0.000 0.952 0.000 0.000 0.000 NA
#&gt; SRR801424     5  0.0000     0.9971 0.000 0.000 0.000 0.000 1.000 NA
#&gt; SRR801425     4  0.1714     1.0000 0.000 0.000 0.000 0.908 0.092 NA
#&gt; SRR801426     4  0.1714     1.0000 0.000 0.000 0.000 0.908 0.092 NA
#&gt; SRR801427     5  0.0260     0.9882 0.000 0.000 0.008 0.000 0.992 NA
#&gt; SRR801428     5  0.0000     0.9971 0.000 0.000 0.000 0.000 1.000 NA
#&gt; SRR801429     4  0.1714     1.0000 0.000 0.000 0.000 0.908 0.092 NA
#&gt; SRR801430     5  0.0000     0.9971 0.000 0.000 0.000 0.000 1.000 NA
#&gt; SRR801431     4  0.1714     1.0000 0.000 0.000 0.000 0.908 0.092 NA
#&gt; SRR801432     4  0.1714     1.0000 0.000 0.000 0.000 0.908 0.092 NA
#&gt; SRR801433     5  0.0000     0.9971 0.000 0.000 0.000 0.000 1.000 NA
#&gt; SRR825135     3  0.0000     0.8794 0.000 0.000 1.000 0.000 0.000 NA
#&gt; SRR825136     1  0.0291     0.8911 0.992 0.000 0.004 0.000 0.000 NA
#&gt; SRR825137     3  0.2350     0.8655 0.000 0.000 0.888 0.076 0.000 NA
#&gt; SRR825139     1  0.0000     0.8942 1.000 0.000 0.000 0.000 0.000 NA
#&gt; SRR825140     1  0.0000     0.8942 1.000 0.000 0.000 0.000 0.000 NA
#&gt; SRR825141     3  0.2350     0.8655 0.000 0.000 0.888 0.076 0.000 NA
#&gt; SRR825143     1  0.0000     0.8942 1.000 0.000 0.000 0.000 0.000 NA
</code></pre>

<script>
$('#tab-ATC-mclust-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-mclust-get-classes-5-a').click(function(){
  $('#tab-ATC-mclust-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-mclust-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-mclust-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-mclust-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-mclust-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-mclust-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-mclust-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-mclust-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-mclust-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-mclust-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-signatures'>
<ul>
<li><a href='#tab-ATC-mclust-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-1-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-1"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-2-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-2"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-3-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-3"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-4-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-4"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-5-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-mclust-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-mclust-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-mclust-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-mclust-signature_compare](figure_cola/ATC-mclust-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-mclust-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-mclust-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-mclust-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-mclust-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-mclust-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-mclust-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-mclust-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-mclust-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-mclust-collect-classes](figure_cola/ATC-mclust-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

---------------------------------------------------




### ATC:NMF*






The object with results only for a single top-value method and a single partition method 
can be extracted as:

```r
res = res_list["ATC", "NMF"]
# you can also extract it by
# res = res_list["ATC:NMF"]
```

A summary of `res` and all the functions that can be applied to it:

```r
res
```

```
#> A 'ConsensusPartition' object with k = 2, 3, 4, 5, 6.
#>   On a matrix with 16748 rows and 53 columns.
#>   Top rows (1000, 2000, 3000, 4000, 5000) are extracted by 'ATC' method.
#>   Subgroups are detected by 'NMF' method.
#>   Performed in total 1250 partitions by row resampling.
#>   Best k for subgroups seems to be 3.
#> 
#> Following methods can be applied to this 'ConsensusPartition' object:
#>  [1] "cola_report"             "collect_classes"         "collect_plots"          
#>  [4] "collect_stats"           "colnames"                "compare_signatures"     
#>  [7] "consensus_heatmap"       "dimension_reduction"     "functional_enrichment"  
#> [10] "get_anno_col"            "get_anno"                "get_classes"            
#> [13] "get_consensus"           "get_matrix"              "get_membership"         
#> [16] "get_param"               "get_signatures"          "get_stats"              
#> [19] "is_best_k"               "is_stable_k"             "membership_heatmap"     
#> [22] "ncol"                    "nrow"                    "plot_ecdf"              
#> [25] "rownames"                "select_partition_number" "show"                   
#> [28] "suggest_best_k"          "test_to_known_factors"
```

`collect_plots()` function collects all the plots made from `res` for all `k` (number of partitions)
into one single page to provide an easy and fast comparison between different `k`.

```r
collect_plots(res)
```

![plot of chunk ATC-NMF-collect-plots](figure_cola/ATC-NMF-collect-plots-1.png)

The plots are:

- The first row: a plot of the ECDF (empirical cumulative distribution
  function) curves of the consensus matrix for each `k` and the heatmap of
  predicted classes for each `k`.
- The second row: heatmaps of the consensus matrix for each `k`.
- The third row: heatmaps of the membership matrix for each `k`.
- The fouth row: heatmaps of the signatures for each `k`.

All the plots in panels can be made by individual functions and they are
plotted later in this section.

`select_partition_number()` produces several plots showing different
statistics for choosing "optimized" `k`. There are following statistics:

- ECDF curves of the consensus matrix for each `k`;
- 1-PAC. [The PAC
  score](https://en.wikipedia.org/wiki/Consensus_clustering#Over-interpretation_potential_of_consensus_clustering)
  measures the proportion of the ambiguous subgrouping.
- Mean silhouette score.
- Concordance. The mean probability of fiting the consensus class ids in all
  partitions.
- Area increased. Denote $A_k$ as the area under the ECDF curve for current
  `k`, the area increased is defined as $A_k - A_{k-1}$.
- Rand index. The percent of pairs of samples that are both in a same cluster
  or both are not in a same cluster in the partition of k and k-1.
- Jaccard index. The ratio of pairs of samples are both in a same cluster in
  the partition of k and k-1 and the pairs of samples are both in a same
  cluster in the partition k or k-1.

The detailed explanations of these statistics can be found in [the _cola_
vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/cola.html#toc_13).

Generally speaking, lower PAC score, higher mean silhouette score or higher
concordance corresponds to better partition. Rand index and Jaccard index
measure how similar the current partition is compared to partition with `k-1`.
If they are too similar, we won't accept `k` is better than `k-1`.

```r
select_partition_number(res)
```

![plot of chunk ATC-NMF-select-partition-number](figure_cola/ATC-NMF-select-partition-number-1.png)

The numeric values for all these statistics can be obtained by `get_stats()`.

```r
get_stats(res)
```

```
#>   k 1-PAC mean_silhouette concordance area_increased  Rand Jaccard
#> 2 2 0.778           0.901       0.951         0.4654 0.512   0.512
#> 3 3 0.922           0.940       0.974         0.3488 0.826   0.672
#> 4 4 0.713           0.787       0.864         0.1653 0.873   0.666
#> 5 5 0.749           0.806       0.846         0.0598 0.954   0.836
#> 6 6 0.774           0.746       0.825         0.0358 0.971   0.886
```

`suggest_best_k()` suggests the best $k$ based on these statistics. The rules are as follows:

- All $k$ with Jaccard index larger than 0.95 are removed because increasing
  $k$ does not provide enough extra information. If all $k$ are removed, it is
  marked as no subgroup is detected.
- For all $k$ with 1-PAC score larger than 0.9, the maximal $k$ is taken as
  the best $k$, and other $k$ are marked as optional $k$.
- If it does not fit the second rule. The $k$ with the maximal vote of the
  highest 1-PAC score, highest mean silhouette, and highest concordance is
  taken as the best $k$.

```r
suggest_best_k(res)
```

```
#> [1] 3
```


Following shows the table of the partitions (You need to click the **show/hide
code output** link to see it). The membership matrix (columns with name `p*`)
is inferred by
[`clue::cl_consensus()`](https://www.rdocumentation.org/link/cl_consensus?package=clue)
function with the `SE` method. Basically the value in the membership matrix
represents the probability to belong to a certain group. The finall class
label for an item is determined with the group with highest probability it
belongs to.

In `get_classes()` function, the entropy is calculated from the membership
matrix and the silhouette score is calculated from the consensus matrix.



<script>
$( function() {
	$( '#tabs-ATC-NMF-get-classes' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-classes'>
<ul>
<li><a href='#tab-ATC-NMF-get-classes-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-classes-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-classes-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-classes-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-classes-5'>k = 6</a></li>
</ul>

<div id='tab-ATC-NMF-get-classes-1'>
<p><a id='tab-ATC-NMF-get-classes-1-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 2), get_membership(res, k = 2))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2
#&gt; SRR547975     2   0.000      0.978 0.000 1.000
#&gt; SRR547973     2   0.000      0.978 0.000 1.000
#&gt; SRR547968     2   0.000      0.978 0.000 1.000
#&gt; SRR547980     2   0.000      0.978 0.000 1.000
#&gt; SRR545058     2   0.000      0.978 0.000 1.000
#&gt; SRR546225     2   0.000      0.978 0.000 1.000
#&gt; SRR546226     1   0.000      0.892 1.000 0.000
#&gt; SRR546227     1   0.000      0.892 1.000 0.000
#&gt; SRR546228     2   0.388      0.898 0.076 0.924
#&gt; SRR546229     2   0.295      0.927 0.052 0.948
#&gt; SRR546230     1   0.000      0.892 1.000 0.000
#&gt; SRR546231     1   0.000      0.892 1.000 0.000
#&gt; SRR546232     1   0.000      0.892 1.000 0.000
#&gt; SRR546233     1   0.388      0.870 0.924 0.076
#&gt; SRR546234     2   0.969      0.191 0.396 0.604
#&gt; SRR546235     1   0.900      0.656 0.684 0.316
#&gt; SRR546236     2   0.295      0.927 0.052 0.948
#&gt; SRR546237     1   0.000      0.892 1.000 0.000
#&gt; SRR546238     2   0.000      0.978 0.000 1.000
#&gt; SRR546239     1   0.000      0.892 1.000 0.000
#&gt; SRR546240     1   0.000      0.892 1.000 0.000
#&gt; SRR547969     2   0.000      0.978 0.000 1.000
#&gt; SRR547970     2   0.000      0.978 0.000 1.000
#&gt; SRR547971     2   0.000      0.978 0.000 1.000
#&gt; SRR547972     2   0.000      0.978 0.000 1.000
#&gt; SRR547974     2   0.000      0.978 0.000 1.000
#&gt; SRR547976     2   0.000      0.978 0.000 1.000
#&gt; SRR547978     2   0.000      0.978 0.000 1.000
#&gt; SRR547979     2   0.000      0.978 0.000 1.000
#&gt; SRR547981     2   0.000      0.978 0.000 1.000
#&gt; SRR547982     2   0.000      0.978 0.000 1.000
#&gt; SRR547983     2   0.000      0.978 0.000 1.000
#&gt; SRR547989     2   0.000      0.978 0.000 1.000
#&gt; SRR547990     2   0.000      0.978 0.000 1.000
#&gt; SRR547991     2   0.000      0.978 0.000 1.000
#&gt; SRR547992     2   0.000      0.978 0.000 1.000
#&gt; SRR801424     1   0.886      0.675 0.696 0.304
#&gt; SRR801425     2   0.000      0.978 0.000 1.000
#&gt; SRR801426     2   0.000      0.978 0.000 1.000
#&gt; SRR801427     1   0.541      0.849 0.876 0.124
#&gt; SRR801428     1   0.671      0.817 0.824 0.176
#&gt; SRR801429     2   0.000      0.978 0.000 1.000
#&gt; SRR801430     1   0.781      0.765 0.768 0.232
#&gt; SRR801431     2   0.000      0.978 0.000 1.000
#&gt; SRR801432     2   0.000      0.978 0.000 1.000
#&gt; SRR801433     1   0.855      0.709 0.720 0.280
#&gt; SRR825135     2   0.000      0.978 0.000 1.000
#&gt; SRR825136     1   0.000      0.892 1.000 0.000
#&gt; SRR825137     1   0.949      0.555 0.632 0.368
#&gt; SRR825139     1   0.000      0.892 1.000 0.000
#&gt; SRR825140     1   0.000      0.892 1.000 0.000
#&gt; SRR825141     1   0.644      0.825 0.836 0.164
#&gt; SRR825143     1   0.000      0.892 1.000 0.000
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-1-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-1-a').click(function(){
  $('#tab-ATC-NMF-get-classes-1-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-2'>
<p><a id='tab-ATC-NMF-get-classes-2-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 3), get_membership(res, k = 3))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3
#&gt; SRR547975     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR547973     2  0.0747      0.961 0.000 0.984 0.016
#&gt; SRR547968     2  0.0237      0.968 0.000 0.996 0.004
#&gt; SRR547980     2  0.0237      0.968 0.000 0.996 0.004
#&gt; SRR545058     2  0.0237      0.968 0.000 0.996 0.004
#&gt; SRR546225     2  0.0237      0.968 0.000 0.996 0.004
#&gt; SRR546226     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR546227     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR546228     2  0.2200      0.924 0.056 0.940 0.004
#&gt; SRR546229     2  0.7940      0.113 0.416 0.524 0.060
#&gt; SRR546230     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR546231     1  0.3482      0.840 0.872 0.000 0.128
#&gt; SRR546232     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR546233     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR546234     2  0.3349      0.868 0.108 0.888 0.004
#&gt; SRR546235     1  0.4110      0.814 0.844 0.152 0.004
#&gt; SRR546236     2  0.2096      0.928 0.052 0.944 0.004
#&gt; SRR546237     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR546238     2  0.0237      0.968 0.000 0.996 0.004
#&gt; SRR546239     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR546240     1  0.0237      0.952 0.996 0.000 0.004
#&gt; SRR547969     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR547970     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR547971     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR547972     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR547974     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR547976     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR547978     2  0.0237      0.968 0.000 0.996 0.004
#&gt; SRR547979     2  0.0747      0.961 0.000 0.984 0.016
#&gt; SRR547981     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR547982     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR547983     2  0.0237      0.968 0.000 0.996 0.004
#&gt; SRR547989     2  0.0237      0.968 0.000 0.996 0.004
#&gt; SRR547990     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR547991     2  0.0237      0.968 0.000 0.996 0.004
#&gt; SRR547992     2  0.0000      0.969 0.000 1.000 0.000
#&gt; SRR801424     3  0.0237      0.997 0.004 0.000 0.996
#&gt; SRR801425     3  0.0237      0.997 0.000 0.004 0.996
#&gt; SRR801426     3  0.0237      0.997 0.000 0.004 0.996
#&gt; SRR801427     3  0.0424      0.993 0.008 0.000 0.992
#&gt; SRR801428     3  0.0237      0.997 0.004 0.000 0.996
#&gt; SRR801429     3  0.0237      0.997 0.000 0.004 0.996
#&gt; SRR801430     3  0.0237      0.997 0.004 0.000 0.996
#&gt; SRR801431     3  0.0237      0.997 0.000 0.004 0.996
#&gt; SRR801432     3  0.0237      0.997 0.000 0.004 0.996
#&gt; SRR801433     3  0.0237      0.997 0.004 0.000 0.996
#&gt; SRR825135     2  0.0424      0.967 0.000 0.992 0.008
#&gt; SRR825136     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR825137     1  0.4741      0.804 0.828 0.152 0.020
#&gt; SRR825139     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR825140     1  0.0000      0.954 1.000 0.000 0.000
#&gt; SRR825141     1  0.3349      0.861 0.888 0.108 0.004
#&gt; SRR825143     1  0.0000      0.954 1.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-2-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-2-a').click(function(){
  $('#tab-ATC-NMF-get-classes-2-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-3'>
<p><a id='tab-ATC-NMF-get-classes-3-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 4), get_membership(res, k = 4))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4
#&gt; SRR547975     2  0.2469     0.8389 0.000 0.892 0.108 0.000
#&gt; SRR547973     2  0.3037     0.8208 0.000 0.880 0.100 0.020
#&gt; SRR547968     2  0.1520     0.8329 0.000 0.956 0.020 0.024
#&gt; SRR547980     2  0.0657     0.8419 0.000 0.984 0.012 0.004
#&gt; SRR545058     3  0.4104     0.7535 0.000 0.164 0.808 0.028
#&gt; SRR546225     3  0.4936     0.5237 0.000 0.340 0.652 0.008
#&gt; SRR546226     1  0.0000     0.8877 1.000 0.000 0.000 0.000
#&gt; SRR546227     1  0.0188     0.8862 0.996 0.000 0.000 0.004
#&gt; SRR546228     3  0.3949     0.7514 0.012 0.140 0.832 0.016
#&gt; SRR546229     3  0.8012     0.3797 0.024 0.164 0.460 0.352
#&gt; SRR546230     1  0.0000     0.8877 1.000 0.000 0.000 0.000
#&gt; SRR546231     1  0.7285     0.3702 0.520 0.000 0.180 0.300
#&gt; SRR546232     1  0.0000     0.8877 1.000 0.000 0.000 0.000
#&gt; SRR546233     1  0.1247     0.8701 0.968 0.016 0.012 0.004
#&gt; SRR546234     3  0.3978     0.7253 0.012 0.192 0.796 0.000
#&gt; SRR546235     3  0.8924     0.2790 0.312 0.124 0.444 0.120
#&gt; SRR546236     3  0.6052     0.7211 0.092 0.224 0.680 0.004
#&gt; SRR546237     1  0.0188     0.8866 0.996 0.000 0.004 0.000
#&gt; SRR546238     3  0.4567     0.7232 0.000 0.244 0.740 0.016
#&gt; SRR546239     1  0.1388     0.8686 0.960 0.000 0.012 0.028
#&gt; SRR546240     1  0.1022     0.8753 0.968 0.000 0.032 0.000
#&gt; SRR547969     2  0.1474     0.8489 0.000 0.948 0.052 0.000
#&gt; SRR547970     2  0.1637     0.8369 0.000 0.940 0.060 0.000
#&gt; SRR547971     2  0.3873     0.7459 0.000 0.772 0.228 0.000
#&gt; SRR547972     2  0.4661     0.5741 0.000 0.652 0.348 0.000
#&gt; SRR547974     2  0.3801     0.7466 0.000 0.780 0.220 0.000
#&gt; SRR547976     2  0.2011     0.8462 0.000 0.920 0.080 0.000
#&gt; SRR547978     2  0.0657     0.8411 0.000 0.984 0.012 0.004
#&gt; SRR547979     2  0.2670     0.7952 0.000 0.908 0.040 0.052
#&gt; SRR547981     2  0.3486     0.8060 0.000 0.812 0.188 0.000
#&gt; SRR547982     2  0.3356     0.8210 0.000 0.824 0.176 0.000
#&gt; SRR547983     2  0.2081     0.8280 0.000 0.916 0.084 0.000
#&gt; SRR547989     2  0.2011     0.8305 0.000 0.920 0.080 0.000
#&gt; SRR547990     2  0.3726     0.7656 0.000 0.788 0.212 0.000
#&gt; SRR547991     2  0.1406     0.8274 0.000 0.960 0.024 0.016
#&gt; SRR547992     2  0.4277     0.6720 0.000 0.720 0.280 0.000
#&gt; SRR801424     4  0.0469     0.9723 0.000 0.000 0.012 0.988
#&gt; SRR801425     4  0.3182     0.8686 0.000 0.028 0.096 0.876
#&gt; SRR801426     4  0.0524     0.9740 0.000 0.008 0.004 0.988
#&gt; SRR801427     4  0.0376     0.9743 0.004 0.004 0.000 0.992
#&gt; SRR801428     4  0.0592     0.9691 0.000 0.000 0.016 0.984
#&gt; SRR801429     4  0.0524     0.9740 0.000 0.008 0.004 0.988
#&gt; SRR801430     4  0.0592     0.9691 0.000 0.000 0.016 0.984
#&gt; SRR801431     4  0.0779     0.9711 0.000 0.004 0.016 0.980
#&gt; SRR801432     4  0.0804     0.9702 0.000 0.012 0.008 0.980
#&gt; SRR801433     4  0.0188     0.9734 0.000 0.000 0.004 0.996
#&gt; SRR825135     3  0.4936     0.6964 0.000 0.280 0.700 0.020
#&gt; SRR825136     1  0.0000     0.8877 1.000 0.000 0.000 0.000
#&gt; SRR825137     1  0.7329     0.0835 0.456 0.120 0.416 0.008
#&gt; SRR825139     1  0.0000     0.8877 1.000 0.000 0.000 0.000
#&gt; SRR825140     1  0.0000     0.8877 1.000 0.000 0.000 0.000
#&gt; SRR825141     1  0.5441     0.3751 0.588 0.012 0.396 0.004
#&gt; SRR825143     1  0.0000     0.8877 1.000 0.000 0.000 0.000
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-3-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-3-a').click(function(){
  $('#tab-ATC-NMF-get-classes-3-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-4'>
<p><a id='tab-ATC-NMF-get-classes-4-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 5), get_membership(res, k = 5))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4 p5
#&gt; SRR547975     2  0.1597      0.864 0.000 0.940 0.012 0.000 NA
#&gt; SRR547973     2  0.5889      0.562 0.000 0.576 0.112 0.004 NA
#&gt; SRR547968     2  0.2907      0.854 0.000 0.864 0.012 0.008 NA
#&gt; SRR547980     2  0.1043      0.865 0.000 0.960 0.000 0.000 NA
#&gt; SRR545058     3  0.3218      0.704 0.000 0.016 0.848 0.012 NA
#&gt; SRR546225     3  0.5747      0.519 0.000 0.088 0.504 0.000 NA
#&gt; SRR546226     1  0.0000      0.951 1.000 0.000 0.000 0.000 NA
#&gt; SRR546227     1  0.0162      0.949 0.996 0.000 0.004 0.000 NA
#&gt; SRR546228     3  0.3320      0.712 0.016 0.016 0.844 0.000 NA
#&gt; SRR546229     3  0.6136      0.532 0.008 0.040 0.632 0.252 NA
#&gt; SRR546230     1  0.0000      0.951 1.000 0.000 0.000 0.000 NA
#&gt; SRR546231     3  0.7973      0.266 0.204 0.000 0.368 0.332 NA
#&gt; SRR546232     1  0.0000      0.951 1.000 0.000 0.000 0.000 NA
#&gt; SRR546233     1  0.0162      0.949 0.996 0.004 0.000 0.000 NA
#&gt; SRR546234     3  0.5126      0.603 0.000 0.040 0.600 0.004 NA
#&gt; SRR546235     3  0.5546      0.687 0.072 0.032 0.752 0.068 NA
#&gt; SRR546236     3  0.4919      0.713 0.084 0.056 0.768 0.000 NA
#&gt; SRR546237     1  0.0510      0.942 0.984 0.000 0.016 0.000 NA
#&gt; SRR546238     3  0.4519      0.690 0.000 0.100 0.752 0.000 NA
#&gt; SRR546239     1  0.1547      0.912 0.948 0.000 0.004 0.032 NA
#&gt; SRR546240     1  0.5213      0.354 0.628 0.004 0.312 0.000 NA
#&gt; SRR547969     2  0.1597      0.868 0.000 0.940 0.012 0.000 NA
#&gt; SRR547970     2  0.2482      0.851 0.000 0.892 0.024 0.000 NA
#&gt; SRR547971     2  0.3321      0.845 0.000 0.832 0.032 0.000 NA
#&gt; SRR547972     2  0.6091      0.580 0.000 0.560 0.172 0.000 NA
#&gt; SRR547974     2  0.3958      0.823 0.000 0.776 0.040 0.000 NA
#&gt; SRR547976     2  0.2561      0.863 0.000 0.884 0.020 0.000 NA
#&gt; SRR547978     2  0.1484      0.866 0.000 0.944 0.008 0.000 NA
#&gt; SRR547979     2  0.3096      0.844 0.000 0.860 0.008 0.024 NA
#&gt; SRR547981     2  0.3608      0.837 0.000 0.824 0.064 0.000 NA
#&gt; SRR547982     2  0.3477      0.847 0.000 0.824 0.040 0.000 NA
#&gt; SRR547983     2  0.1952      0.852 0.000 0.912 0.004 0.000 NA
#&gt; SRR547989     2  0.1831      0.853 0.000 0.920 0.004 0.000 NA
#&gt; SRR547990     2  0.3767      0.830 0.000 0.812 0.068 0.000 NA
#&gt; SRR547991     2  0.1608      0.856 0.000 0.928 0.000 0.000 NA
#&gt; SRR547992     2  0.5264      0.713 0.000 0.652 0.092 0.000 NA
#&gt; SRR801424     4  0.0693      0.967 0.000 0.000 0.008 0.980 NA
#&gt; SRR801425     4  0.2331      0.902 0.000 0.000 0.080 0.900 NA
#&gt; SRR801426     4  0.1012      0.966 0.000 0.000 0.012 0.968 NA
#&gt; SRR801427     4  0.0613      0.967 0.008 0.000 0.004 0.984 NA
#&gt; SRR801428     4  0.0703      0.962 0.000 0.000 0.000 0.976 NA
#&gt; SRR801429     4  0.1331      0.960 0.000 0.000 0.008 0.952 NA
#&gt; SRR801430     4  0.0703      0.962 0.000 0.000 0.000 0.976 NA
#&gt; SRR801431     4  0.0579      0.968 0.000 0.000 0.008 0.984 NA
#&gt; SRR801432     4  0.1408      0.958 0.000 0.000 0.008 0.948 NA
#&gt; SRR801433     4  0.0162      0.968 0.000 0.000 0.000 0.996 NA
#&gt; SRR825135     3  0.4879      0.632 0.004 0.168 0.740 0.008 NA
#&gt; SRR825136     1  0.0771      0.937 0.976 0.000 0.004 0.000 NA
#&gt; SRR825137     3  0.7636      0.519 0.216 0.172 0.520 0.012 NA
#&gt; SRR825139     1  0.0000      0.951 1.000 0.000 0.000 0.000 NA
#&gt; SRR825140     1  0.0000      0.951 1.000 0.000 0.000 0.000 NA
#&gt; SRR825141     3  0.5864      0.315 0.368 0.004 0.536 0.000 NA
#&gt; SRR825143     1  0.0000      0.951 1.000 0.000 0.000 0.000 NA
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-4-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-4-a').click(function(){
  $('#tab-ATC-NMF-get-classes-4-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>

<div id='tab-ATC-NMF-get-classes-5'>
<p><a id='tab-ATC-NMF-get-classes-5-a' style='color:#0366d6' href='#'>show/hide code output</a></p>
<pre><code class="r">cbind(get_classes(res, k = 6), get_membership(res, k = 6))
</code></pre>

<pre><code>#&gt;           class entropy silhouette    p1    p2    p3    p4    p5 p6
#&gt; SRR547975     5  0.2879     0.8044 0.000 0.044 0.016 0.000 0.868 NA
#&gt; SRR547973     2  0.7339     0.3870 0.000 0.352 0.092 0.008 0.200 NA
#&gt; SRR547968     5  0.4634     0.7121 0.000 0.064 0.004 0.016 0.712 NA
#&gt; SRR547980     5  0.2001     0.8106 0.000 0.012 0.008 0.000 0.912 NA
#&gt; SRR545058     3  0.3304     0.5155 0.000 0.168 0.804 0.008 0.000 NA
#&gt; SRR546225     2  0.5163     0.5465 0.000 0.636 0.272 0.000 0.048 NA
#&gt; SRR546226     1  0.0000     0.9183 1.000 0.000 0.000 0.000 0.000 NA
#&gt; SRR546227     1  0.0363     0.9139 0.988 0.000 0.000 0.000 0.000 NA
#&gt; SRR546228     3  0.3025     0.5692 0.008 0.164 0.820 0.000 0.004 NA
#&gt; SRR546229     3  0.5326     0.5515 0.016 0.020 0.712 0.164 0.032 NA
#&gt; SRR546230     1  0.0000     0.9183 1.000 0.000 0.000 0.000 0.000 NA
#&gt; SRR546231     3  0.7013     0.3912 0.144 0.004 0.492 0.224 0.000 NA
#&gt; SRR546232     1  0.0000     0.9183 1.000 0.000 0.000 0.000 0.000 NA
#&gt; SRR546233     1  0.2044     0.8732 0.920 0.008 0.040 0.004 0.000 NA
#&gt; SRR546234     2  0.4393     0.4566 0.000 0.628 0.340 0.000 0.024 NA
#&gt; SRR546235     3  0.3389     0.6348 0.048 0.016 0.860 0.024 0.008 NA
#&gt; SRR546236     3  0.3666     0.5882 0.028 0.112 0.820 0.000 0.008 NA
#&gt; SRR546237     1  0.0363     0.9127 0.988 0.000 0.012 0.000 0.000 NA
#&gt; SRR546238     3  0.4511     0.5784 0.000 0.116 0.768 0.016 0.072 NA
#&gt; SRR546239     1  0.1737     0.8789 0.932 0.008 0.000 0.020 0.000 NA
#&gt; SRR546240     1  0.5581    -0.0985 0.492 0.008 0.408 0.000 0.008 NA
#&gt; SRR547969     5  0.2231     0.8083 0.000 0.028 0.004 0.000 0.900 NA
#&gt; SRR547970     5  0.3005     0.7993 0.000 0.036 0.008 0.000 0.848 NA
#&gt; SRR547971     5  0.3203     0.7963 0.000 0.064 0.028 0.000 0.852 NA
#&gt; SRR547972     5  0.5991     0.4054 0.000 0.348 0.060 0.000 0.516 NA
#&gt; SRR547974     5  0.4578     0.7714 0.000 0.084 0.040 0.004 0.756 NA
#&gt; SRR547976     5  0.3208     0.7965 0.000 0.068 0.012 0.000 0.844 NA
#&gt; SRR547978     5  0.2068     0.8093 0.000 0.008 0.008 0.000 0.904 NA
#&gt; SRR547979     5  0.3889     0.7620 0.000 0.028 0.004 0.016 0.772 NA
#&gt; SRR547981     5  0.4798     0.7409 0.000 0.052 0.076 0.000 0.728 NA
#&gt; SRR547982     5  0.4324     0.7355 0.000 0.192 0.004 0.000 0.724 NA
#&gt; SRR547983     5  0.2679     0.7859 0.000 0.040 0.000 0.000 0.864 NA
#&gt; SRR547989     5  0.2579     0.7870 0.000 0.040 0.000 0.000 0.872 NA
#&gt; SRR547990     5  0.4280     0.7721 0.000 0.052 0.064 0.000 0.776 NA
#&gt; SRR547991     5  0.3742     0.7569 0.000 0.056 0.000 0.004 0.780 NA
#&gt; SRR547992     5  0.5734     0.5549 0.000 0.284 0.052 0.000 0.584 NA
#&gt; SRR801424     4  0.1152     0.9572 0.000 0.000 0.004 0.952 0.000 NA
#&gt; SRR801425     4  0.1793     0.9255 0.000 0.004 0.040 0.932 0.008 NA
#&gt; SRR801426     4  0.0405     0.9602 0.000 0.000 0.004 0.988 0.000 NA
#&gt; SRR801427     4  0.0717     0.9606 0.008 0.000 0.000 0.976 0.000 NA
#&gt; SRR801428     4  0.1588     0.9441 0.000 0.004 0.000 0.924 0.000 NA
#&gt; SRR801429     4  0.0405     0.9608 0.000 0.000 0.004 0.988 0.000 NA
#&gt; SRR801430     4  0.1812     0.9374 0.000 0.008 0.000 0.912 0.000 NA
#&gt; SRR801431     4  0.0291     0.9610 0.000 0.000 0.004 0.992 0.000 NA
#&gt; SRR801432     4  0.0748     0.9571 0.000 0.004 0.004 0.976 0.000 NA
#&gt; SRR801433     4  0.1152     0.9562 0.000 0.004 0.000 0.952 0.000 NA
#&gt; SRR825135     3  0.5200     0.5555 0.004 0.052 0.732 0.020 0.088 NA
#&gt; SRR825136     1  0.3100     0.8051 0.840 0.024 0.008 0.000 0.004 NA
#&gt; SRR825137     3  0.6226     0.5404 0.128 0.008 0.620 0.004 0.080 NA
#&gt; SRR825139     1  0.0000     0.9183 1.000 0.000 0.000 0.000 0.000 NA
#&gt; SRR825140     1  0.0000     0.9183 1.000 0.000 0.000 0.000 0.000 NA
#&gt; SRR825141     3  0.5290     0.4904 0.272 0.020 0.636 0.000 0.016 NA
#&gt; SRR825143     1  0.0000     0.9183 1.000 0.000 0.000 0.000 0.000 NA
</code></pre>

<script>
$('#tab-ATC-NMF-get-classes-5-a').parent().next().next().hide();
$('#tab-ATC-NMF-get-classes-5-a').click(function(){
  $('#tab-ATC-NMF-get-classes-5-a').parent().next().next().toggle();
  return(false);
});
</script>
</div>
</div>

Heatmaps for the consensus matrix. It visualizes the probability of two
samples to be in a same group.



<script>
$( function() {
	$( '#tabs-ATC-NMF-consensus-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-consensus-heatmap'>
<ul>
<li><a href='#tab-ATC-NMF-consensus-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-consensus-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-consensus-heatmap-1'>
<pre><code class="r">consensus_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-1-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-1"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-2'>
<pre><code class="r">consensus_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-2-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-2"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-3'>
<pre><code class="r">consensus_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-3-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-3"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-4'>
<pre><code class="r">consensus_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-4-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-4"/></p>

</div>
<div id='tab-ATC-NMF-consensus-heatmap-5'>
<pre><code class="r">consensus_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-consensus-heatmap-5-1.png" alt="plot of chunk tab-ATC-NMF-consensus-heatmap-5"/></p>

</div>
</div>

Heatmaps for the membership of samples in all partitions to see how consistent they are:




<script>
$( function() {
	$( '#tabs-ATC-NMF-membership-heatmap' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-membership-heatmap'>
<ul>
<li><a href='#tab-ATC-NMF-membership-heatmap-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-membership-heatmap-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-membership-heatmap-1'>
<pre><code class="r">membership_heatmap(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-1-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-1"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-2'>
<pre><code class="r">membership_heatmap(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-2-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-2"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-3'>
<pre><code class="r">membership_heatmap(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-3-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-3"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-4'>
<pre><code class="r">membership_heatmap(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-4-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-4"/></p>

</div>
<div id='tab-ATC-NMF-membership-heatmap-5'>
<pre><code class="r">membership_heatmap(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-membership-heatmap-5-1.png" alt="plot of chunk tab-ATC-NMF-membership-heatmap-5"/></p>

</div>
</div>

As soon as we have had the classes for columns, we can look for signatures
which are significantly different between classes which can be candidate marks
for certain classes. Following are the heatmaps for signatures.



Signature heatmaps where rows are scaled:



<script>
$( function() {
	$( '#tabs-ATC-NMF-get-signatures' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-signatures'>
<ul>
<li><a href='#tab-ATC-NMF-get-signatures-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-get-signatures-1'>
<pre><code class="r">get_signatures(res, k = 2)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-1-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-1"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-2'>
<pre><code class="r">get_signatures(res, k = 3)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-2-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-2"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-3'>
<pre><code class="r">get_signatures(res, k = 4)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-3-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-3"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-4'>
<pre><code class="r">get_signatures(res, k = 5)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-4-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-4"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-5'>
<pre><code class="r">get_signatures(res, k = 6)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-5-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-5"/></p>

</div>
</div>



Signature heatmaps where rows are not scaled:


<script>
$( function() {
	$( '#tabs-ATC-NMF-get-signatures-no-scale' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-get-signatures-no-scale'>
<ul>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-get-signatures-no-scale-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-get-signatures-no-scale-1'>
<pre><code class="r">get_signatures(res, k = 2, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-1-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-1"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-2'>
<pre><code class="r">get_signatures(res, k = 3, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-2-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-2"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-3'>
<pre><code class="r">get_signatures(res, k = 4, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-3-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-3"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-4'>
<pre><code class="r">get_signatures(res, k = 5, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-4-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-4"/></p>

</div>
<div id='tab-ATC-NMF-get-signatures-no-scale-5'>
<pre><code class="r">get_signatures(res, k = 6, scale_rows = FALSE)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-get-signatures-no-scale-5-1.png" alt="plot of chunk tab-ATC-NMF-get-signatures-no-scale-5"/></p>

</div>
</div>



Compare the overlap of signatures from different k:

```r
compare_signatures(res)
```

![plot of chunk ATC-NMF-signature_compare](figure_cola/ATC-NMF-signature_compare-1.png)

`get_signature()` returns a data frame invisibly. TO get the list of signatures, the function
call should be assigned to a variable explicitly. In following code, if `plot` argument is set
to `FALSE`, no heatmap is plotted while only the differential analysis is performed.

```r
# code only for demonstration
tb = get_signature(res, k = ..., plot = FALSE)
```

An example of the output of `tb` is:

```
#>   which_row         fdr    mean_1    mean_2 scaled_mean_1 scaled_mean_2 km
#> 1        38 0.042760348  8.373488  9.131774    -0.5533452     0.5164555  1
#> 2        40 0.018707592  7.106213  8.469186    -0.6173731     0.5762149  1
#> 3        55 0.019134737 10.221463 11.207825    -0.6159697     0.5749050  1
#> 4        59 0.006059896  5.921854  7.869574    -0.6899429     0.6439467  1
#> 5        60 0.018055526  8.928898 10.211722    -0.6204761     0.5791110  1
#> 6        98 0.009384629 15.714769 14.887706     0.6635654    -0.6193277  2
...
```

The columns in `tb` are:

1. `which_row`: row indices corresponding to the input matrix.
2. `fdr`: FDR for the differential test. 
3. `mean_x`: The mean value in group x.
4. `scaled_mean_x`: The mean value in group x after rows are scaled.
5. `km`: Row groups if k-means clustering is applied to rows.



UMAP plot which shows how samples are separated.


<script>
$( function() {
	$( '#tabs-ATC-NMF-dimension-reduction' ).tabs();
} );
</script>
<div id='tabs-ATC-NMF-dimension-reduction'>
<ul>
<li><a href='#tab-ATC-NMF-dimension-reduction-1'>k = 2</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-2'>k = 3</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-3'>k = 4</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-4'>k = 5</a></li>
<li><a href='#tab-ATC-NMF-dimension-reduction-5'>k = 6</a></li>
</ul>
<div id='tab-ATC-NMF-dimension-reduction-1'>
<pre><code class="r">dimension_reduction(res, k = 2, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-1-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-1"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-2'>
<pre><code class="r">dimension_reduction(res, k = 3, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-2-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-2"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-3'>
<pre><code class="r">dimension_reduction(res, k = 4, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-3-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-3"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-4'>
<pre><code class="r">dimension_reduction(res, k = 5, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-4-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-4"/></p>

</div>
<div id='tab-ATC-NMF-dimension-reduction-5'>
<pre><code class="r">dimension_reduction(res, k = 6, method = &quot;UMAP&quot;)
</code></pre>

<p><img src="figure_cola/tab-ATC-NMF-dimension-reduction-5-1.png" alt="plot of chunk tab-ATC-NMF-dimension-reduction-5"/></p>

</div>
</div>


Following heatmap shows how subgroups are split when increasing `k`:

```r
collect_classes(res)
```

![plot of chunk ATC-NMF-collect-classes](figure_cola/ATC-NMF-collect-classes-1.png)


If matrix rows can be associated to genes, consider to use `functional_enrichment(res,
...)` to perform function enrichment for the signature genes. See [this vignette](http://bioconductor.org/packages/devel/bioc/vignettes/cola/inst/doc/functional_enrichment.html) for more detailed explanations.


 

## Session info


```r
sessionInfo()
```

```
#> R version 3.6.0 (2019-04-26)
#> Platform: x86_64-pc-linux-gnu (64-bit)
#> Running under: CentOS Linux 7 (Core)
#> 
#> Matrix products: default
#> BLAS:   /usr/lib64/libblas.so.3.4.2
#> LAPACK: /usr/lib64/liblapack.so.3.4.2
#> 
#> locale:
#>  [1] LC_CTYPE=en_GB.UTF-8       LC_NUMERIC=C               LC_TIME=en_GB.UTF-8       
#>  [4] LC_COLLATE=en_GB.UTF-8     LC_MONETARY=en_GB.UTF-8    LC_MESSAGES=en_GB.UTF-8   
#>  [7] LC_PAPER=en_GB.UTF-8       LC_NAME=C                  LC_ADDRESS=C              
#> [10] LC_TELEPHONE=C             LC_MEASUREMENT=en_GB.UTF-8 LC_IDENTIFICATION=C       
#> 
#> attached base packages:
#> [1] grid      stats     graphics  grDevices utils     datasets  methods   base     
#> 
#> other attached packages:
#> [1] genefilter_1.66.0    ComplexHeatmap_2.3.1 markdown_1.1         knitr_1.26          
#> [5] GetoptLong_0.1.7     cola_1.3.2          
#> 
#> loaded via a namespace (and not attached):
#>  [1] circlize_0.4.8       shape_1.4.4          xfun_0.11            slam_0.1-46         
#>  [5] lattice_0.20-38      splines_3.6.0        colorspace_1.4-1     vctrs_0.2.0         
#>  [9] stats4_3.6.0         blob_1.2.0           XML_3.98-1.20        survival_2.44-1.1   
#> [13] rlang_0.4.2          pillar_1.4.2         DBI_1.0.0            BiocGenerics_0.30.0 
#> [17] bit64_0.9-7          RColorBrewer_1.1-2   matrixStats_0.55.0   stringr_1.4.0       
#> [21] GlobalOptions_0.1.1  evaluate_0.14        memoise_1.1.0        Biobase_2.44.0      
#> [25] IRanges_2.18.3       parallel_3.6.0       AnnotationDbi_1.46.1 highr_0.8           
#> [29] Rcpp_1.0.3           xtable_1.8-4         backports_1.1.5      S4Vectors_0.22.1    
#> [33] annotate_1.62.0      skmeans_0.2-11       bit_1.1-14           microbenchmark_1.4-7
#> [37] brew_1.0-6           impute_1.58.0        rjson_0.2.20         png_0.1-7           
#> [41] digest_0.6.23        stringi_1.4.3        polyclip_1.10-0      clue_0.3-57         
#> [45] tools_3.6.0          bitops_1.0-6         magrittr_1.5         eulerr_6.0.0        
#> [49] RCurl_1.95-4.12      RSQLite_2.1.4        tibble_2.1.3         cluster_2.1.0       
#> [53] crayon_1.3.4         pkgconfig_2.0.3      zeallot_0.1.0        Matrix_1.2-17       
#> [57] xml2_1.2.2           httr_1.4.1           R6_2.4.1             mclust_5.4.5        
#> [61] compiler_3.6.0
```


