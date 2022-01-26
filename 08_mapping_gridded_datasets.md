# Mapping Gridded Datasets

https://cds.climate.copernicus.eu/cdsapp#!/dataset/ecv-for-climate-change?tab=overview


```python
import os
from matplotlib import pyplot as plt
import cartopy
import cartopy.crs as ccrs
import xarray as xr
```


```python
data_pkg_path = 'data'
file_path = os.path.join(data_pkg_path, 'gistemp','gistemp1200_GHCNv4_ERSSTv5.nc')

ds = xr.open_dataset(file_path)
```


```python
ds
```




<div><svg style="position: absolute; width: 0; height: 0; overflow: hidden">
<defs>
<symbol id="icon-database" viewBox="0 0 32 32">
<path d="M16 0c-8.837 0-16 2.239-16 5v4c0 2.761 7.163 5 16 5s16-2.239 16-5v-4c0-2.761-7.163-5-16-5z"></path>
<path d="M16 17c-8.837 0-16-2.239-16-5v6c0 2.761 7.163 5 16 5s16-2.239 16-5v-6c0 2.761-7.163 5-16 5z"></path>
<path d="M16 26c-8.837 0-16-2.239-16-5v6c0 2.761 7.163 5 16 5s16-2.239 16-5v-6c0 2.761-7.163 5-16 5z"></path>
</symbol>
<symbol id="icon-file-text2" viewBox="0 0 32 32">
<path d="M28.681 7.159c-0.694-0.947-1.662-2.053-2.724-3.116s-2.169-2.030-3.116-2.724c-1.612-1.182-2.393-1.319-2.841-1.319h-15.5c-1.378 0-2.5 1.121-2.5 2.5v27c0 1.378 1.122 2.5 2.5 2.5h23c1.378 0 2.5-1.122 2.5-2.5v-19.5c0-0.448-0.137-1.23-1.319-2.841zM24.543 5.457c0.959 0.959 1.712 1.825 2.268 2.543h-4.811v-4.811c0.718 0.556 1.584 1.309 2.543 2.268zM28 29.5c0 0.271-0.229 0.5-0.5 0.5h-23c-0.271 0-0.5-0.229-0.5-0.5v-27c0-0.271 0.229-0.5 0.5-0.5 0 0 15.499-0 15.5 0v7c0 0.552 0.448 1 1 1h7v19.5z"></path>
<path d="M23 26h-14c-0.552 0-1-0.448-1-1s0.448-1 1-1h14c0.552 0 1 0.448 1 1s-0.448 1-1 1z"></path>
<path d="M23 22h-14c-0.552 0-1-0.448-1-1s0.448-1 1-1h14c0.552 0 1 0.448 1 1s-0.448 1-1 1z"></path>
<path d="M23 18h-14c-0.552 0-1-0.448-1-1s0.448-1 1-1h14c0.552 0 1 0.448 1 1s-0.448 1-1 1z"></path>
</symbol>
</defs>
</svg>
<style>/* CSS stylesheet for displaying xarray objects in jupyterlab.
 *
 */

:root {
  --xr-font-color0: var(--jp-content-font-color0, rgba(0, 0, 0, 1));
  --xr-font-color2: var(--jp-content-font-color2, rgba(0, 0, 0, 0.54));
  --xr-font-color3: var(--jp-content-font-color3, rgba(0, 0, 0, 0.38));
  --xr-border-color: var(--jp-border-color2, #e0e0e0);
  --xr-disabled-color: var(--jp-layout-color3, #bdbdbd);
  --xr-background-color: var(--jp-layout-color0, white);
  --xr-background-color-row-even: var(--jp-layout-color1, white);
  --xr-background-color-row-odd: var(--jp-layout-color2, #eeeeee);
}

html[theme=dark],
body.vscode-dark {
  --xr-font-color0: rgba(255, 255, 255, 1);
  --xr-font-color2: rgba(255, 255, 255, 0.54);
  --xr-font-color3: rgba(255, 255, 255, 0.38);
  --xr-border-color: #1F1F1F;
  --xr-disabled-color: #515151;
  --xr-background-color: #111111;
  --xr-background-color-row-even: #111111;
  --xr-background-color-row-odd: #313131;
}

.xr-wrap {
  display: block !important;
  min-width: 300px;
  max-width: 700px;
}

.xr-text-repr-fallback {
  /* fallback to plain text repr when CSS is not injected (untrusted notebook) */
  display: none;
}

.xr-header {
  padding-top: 6px;
  padding-bottom: 6px;
  margin-bottom: 4px;
  border-bottom: solid 1px var(--xr-border-color);
}

.xr-header > div,
.xr-header > ul {
  display: inline;
  margin-top: 0;
  margin-bottom: 0;
}

.xr-obj-type,
.xr-array-name {
  margin-left: 2px;
  margin-right: 10px;
}

.xr-obj-type {
  color: var(--xr-font-color2);
}

.xr-sections {
  padding-left: 0 !important;
  display: grid;
  grid-template-columns: 150px auto auto 1fr 20px 20px;
}

.xr-section-item {
  display: contents;
}

.xr-section-item input {
  display: none;
}

.xr-section-item input + label {
  color: var(--xr-disabled-color);
}

.xr-section-item input:enabled + label {
  cursor: pointer;
  color: var(--xr-font-color2);
}

.xr-section-item input:enabled + label:hover {
  color: var(--xr-font-color0);
}

.xr-section-summary {
  grid-column: 1;
  color: var(--xr-font-color2);
  font-weight: 500;
}

.xr-section-summary > span {
  display: inline-block;
  padding-left: 0.5em;
}

.xr-section-summary-in:disabled + label {
  color: var(--xr-font-color2);
}

.xr-section-summary-in + label:before {
  display: inline-block;
  content: '►';
  font-size: 11px;
  width: 15px;
  text-align: center;
}

.xr-section-summary-in:disabled + label:before {
  color: var(--xr-disabled-color);
}

.xr-section-summary-in:checked + label:before {
  content: '▼';
}

.xr-section-summary-in:checked + label > span {
  display: none;
}

.xr-section-summary,
.xr-section-inline-details {
  padding-top: 4px;
  padding-bottom: 4px;
}

.xr-section-inline-details {
  grid-column: 2 / -1;
}

.xr-section-details {
  display: none;
  grid-column: 1 / -1;
  margin-bottom: 5px;
}

.xr-section-summary-in:checked ~ .xr-section-details {
  display: contents;
}

.xr-array-wrap {
  grid-column: 1 / -1;
  display: grid;
  grid-template-columns: 20px auto;
}

.xr-array-wrap > label {
  grid-column: 1;
  vertical-align: top;
}

.xr-preview {
  color: var(--xr-font-color3);
}

.xr-array-preview,
.xr-array-data {
  padding: 0 5px !important;
  grid-column: 2;
}

.xr-array-data,
.xr-array-in:checked ~ .xr-array-preview {
  display: none;
}

.xr-array-in:checked ~ .xr-array-data,
.xr-array-preview {
  display: inline-block;
}

.xr-dim-list {
  display: inline-block !important;
  list-style: none;
  padding: 0 !important;
  margin: 0;
}

.xr-dim-list li {
  display: inline-block;
  padding: 0;
  margin: 0;
}

.xr-dim-list:before {
  content: '(';
}

.xr-dim-list:after {
  content: ')';
}

.xr-dim-list li:not(:last-child):after {
  content: ',';
  padding-right: 5px;
}

.xr-has-index {
  font-weight: bold;
}

.xr-var-list,
.xr-var-item {
  display: contents;
}

.xr-var-item > div,
.xr-var-item label,
.xr-var-item > .xr-var-name span {
  background-color: var(--xr-background-color-row-even);
  margin-bottom: 0;
}

.xr-var-item > .xr-var-name:hover span {
  padding-right: 5px;
}

.xr-var-list > li:nth-child(odd) > div,
.xr-var-list > li:nth-child(odd) > label,
.xr-var-list > li:nth-child(odd) > .xr-var-name span {
  background-color: var(--xr-background-color-row-odd);
}

.xr-var-name {
  grid-column: 1;
}

.xr-var-dims {
  grid-column: 2;
}

.xr-var-dtype {
  grid-column: 3;
  text-align: right;
  color: var(--xr-font-color2);
}

.xr-var-preview {
  grid-column: 4;
}

.xr-var-name,
.xr-var-dims,
.xr-var-dtype,
.xr-preview,
.xr-attrs dt {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  padding-right: 10px;
}

.xr-var-name:hover,
.xr-var-dims:hover,
.xr-var-dtype:hover,
.xr-attrs dt:hover {
  overflow: visible;
  width: auto;
  z-index: 1;
}

.xr-var-attrs,
.xr-var-data {
  display: none;
  background-color: var(--xr-background-color) !important;
  padding-bottom: 5px !important;
}

.xr-var-attrs-in:checked ~ .xr-var-attrs,
.xr-var-data-in:checked ~ .xr-var-data {
  display: block;
}

.xr-var-data > table {
  float: right;
}

.xr-var-name span,
.xr-var-data,
.xr-attrs {
  padding-left: 25px !important;
}

.xr-attrs,
.xr-var-attrs,
.xr-var-data {
  grid-column: 1 / -1;
}

dl.xr-attrs {
  padding: 0;
  margin: 0;
  display: grid;
  grid-template-columns: 125px auto;
}

.xr-attrs dt,
.xr-attrs dd {
  padding: 0;
  margin: 0;
  float: left;
  padding-right: 10px;
  width: auto;
}

.xr-attrs dt {
  font-weight: normal;
  grid-column: 1;
}

.xr-attrs dt:hover span {
  display: inline-block;
  background: var(--xr-background-color);
  padding-right: 10px;
}

.xr-attrs dd {
  grid-column: 2;
  white-space: pre-wrap;
  word-break: break-all;
}

.xr-icon-database,
.xr-icon-file-text2 {
  display: inline-block;
  vertical-align: middle;
  width: 1em;
  height: 1.5em !important;
  stroke-width: 0;
  stroke: currentColor;
  fill: currentColor;
}
</style><pre class='xr-text-repr-fallback'>&lt;xarray.Dataset&gt;
Dimensions:      (lat: 90, lon: 180, time: 1704, nv: 2)
Coordinates:
  * lat          (lat) float32 -89.0 -87.0 -85.0 -83.0 ... 83.0 85.0 87.0 89.0
  * lon          (lon) float32 -179.0 -177.0 -175.0 -173.0 ... 175.0 177.0 179.0
  * time         (time) datetime64[ns] 1880-01-15 1880-02-15 ... 2021-12-15
Dimensions without coordinates: nv
Data variables:
    time_bnds    (time, nv) datetime64[ns] 1880-01-01 1880-02-01 ... 2022-01-01
    tempanomaly  (time, lat, lon) float32 ...
Attributes:
    title:        GISTEMP Surface Temperature Analysis
    institution:  NASA Goddard Institute for Space Studies
    source:       http://data.giss.nasa.gov/gistemp/
    Conventions:  CF-1.6
    history:      Created 2022-01-11 09:09:58 by SBBX_to_nc 2.0 - ILAND=1200,...</pre><div class='xr-wrap' style='display:none'><div class='xr-header'><div class='xr-obj-type'>xarray.Dataset</div></div><ul class='xr-sections'><li class='xr-section-item'><input id='section-a4631026-e527-4434-9d39-ca2a9e618930' class='xr-section-summary-in' type='checkbox' disabled ><label for='section-a4631026-e527-4434-9d39-ca2a9e618930' class='xr-section-summary'  title='Expand/collapse section'>Dimensions:</label><div class='xr-section-inline-details'><ul class='xr-dim-list'><li><span class='xr-has-index'>lat</span>: 90</li><li><span class='xr-has-index'>lon</span>: 180</li><li><span class='xr-has-index'>time</span>: 1704</li><li><span>nv</span>: 2</li></ul></div><div class='xr-section-details'></div></li><li class='xr-section-item'><input id='section-7f4423e2-9523-4443-bda0-d998439cbbfd' class='xr-section-summary-in' type='checkbox'  checked><label for='section-7f4423e2-9523-4443-bda0-d998439cbbfd' class='xr-section-summary' >Coordinates: <span>(3)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><ul class='xr-var-list'><li class='xr-var-item'><div class='xr-var-name'><span class='xr-has-index'>lat</span></div><div class='xr-var-dims'>(lat)</div><div class='xr-var-dtype'>float32</div><div class='xr-var-preview xr-preview'>-89.0 -87.0 -85.0 ... 87.0 89.0</div><input id='attrs-bf716a4e-fb74-4bf0-995d-c25deca24d0c' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-bf716a4e-fb74-4bf0-995d-c25deca24d0c' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-378c1cd1-efd1-46fb-94f9-746dc26048bf' class='xr-var-data-in' type='checkbox'><label for='data-378c1cd1-efd1-46fb-94f9-746dc26048bf' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>standard_name :</span></dt><dd>latitude</dd><dt><span>long_name :</span></dt><dd>Latitude</dd><dt><span>units :</span></dt><dd>degrees_north</dd></dl></div><div class='xr-var-data'><pre>array([-89., -87., -85., -83., -81., -79., -77., -75., -73., -71., -69., -67.,
       -65., -63., -61., -59., -57., -55., -53., -51., -49., -47., -45., -43.,
       -41., -39., -37., -35., -33., -31., -29., -27., -25., -23., -21., -19.,
       -17., -15., -13., -11.,  -9.,  -7.,  -5.,  -3.,  -1.,   1.,   3.,   5.,
         7.,   9.,  11.,  13.,  15.,  17.,  19.,  21.,  23.,  25.,  27.,  29.,
        31.,  33.,  35.,  37.,  39.,  41.,  43.,  45.,  47.,  49.,  51.,  53.,
        55.,  57.,  59.,  61.,  63.,  65.,  67.,  69.,  71.,  73.,  75.,  77.,
        79.,  81.,  83.,  85.,  87.,  89.], dtype=float32)</pre></div></li><li class='xr-var-item'><div class='xr-var-name'><span class='xr-has-index'>lon</span></div><div class='xr-var-dims'>(lon)</div><div class='xr-var-dtype'>float32</div><div class='xr-var-preview xr-preview'>-179.0 -177.0 ... 177.0 179.0</div><input id='attrs-21952b2a-281c-40eb-926d-ef0db9257471' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-21952b2a-281c-40eb-926d-ef0db9257471' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-2bed47ba-eeaf-40f5-8bf0-d8d7f8df3926' class='xr-var-data-in' type='checkbox'><label for='data-2bed47ba-eeaf-40f5-8bf0-d8d7f8df3926' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>standard_name :</span></dt><dd>longitude</dd><dt><span>long_name :</span></dt><dd>Longitude</dd><dt><span>units :</span></dt><dd>degrees_east</dd></dl></div><div class='xr-var-data'><pre>array([-179., -177., -175., -173., -171., -169., -167., -165., -163., -161.,
       -159., -157., -155., -153., -151., -149., -147., -145., -143., -141.,
       -139., -137., -135., -133., -131., -129., -127., -125., -123., -121.,
       -119., -117., -115., -113., -111., -109., -107., -105., -103., -101.,
        -99.,  -97.,  -95.,  -93.,  -91.,  -89.,  -87.,  -85.,  -83.,  -81.,
        -79.,  -77.,  -75.,  -73.,  -71.,  -69.,  -67.,  -65.,  -63.,  -61.,
        -59.,  -57.,  -55.,  -53.,  -51.,  -49.,  -47.,  -45.,  -43.,  -41.,
        -39.,  -37.,  -35.,  -33.,  -31.,  -29.,  -27.,  -25.,  -23.,  -21.,
        -19.,  -17.,  -15.,  -13.,  -11.,   -9.,   -7.,   -5.,   -3.,   -1.,
          1.,    3.,    5.,    7.,    9.,   11.,   13.,   15.,   17.,   19.,
         21.,   23.,   25.,   27.,   29.,   31.,   33.,   35.,   37.,   39.,
         41.,   43.,   45.,   47.,   49.,   51.,   53.,   55.,   57.,   59.,
         61.,   63.,   65.,   67.,   69.,   71.,   73.,   75.,   77.,   79.,
         81.,   83.,   85.,   87.,   89.,   91.,   93.,   95.,   97.,   99.,
        101.,  103.,  105.,  107.,  109.,  111.,  113.,  115.,  117.,  119.,
        121.,  123.,  125.,  127.,  129.,  131.,  133.,  135.,  137.,  139.,
        141.,  143.,  145.,  147.,  149.,  151.,  153.,  155.,  157.,  159.,
        161.,  163.,  165.,  167.,  169.,  171.,  173.,  175.,  177.,  179.],
      dtype=float32)</pre></div></li><li class='xr-var-item'><div class='xr-var-name'><span class='xr-has-index'>time</span></div><div class='xr-var-dims'>(time)</div><div class='xr-var-dtype'>datetime64[ns]</div><div class='xr-var-preview xr-preview'>1880-01-15 ... 2021-12-15</div><input id='attrs-6d2d30ff-3ae7-4fec-a81b-0b0153846e4b' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-6d2d30ff-3ae7-4fec-a81b-0b0153846e4b' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-ae8b45bc-8b4f-4c2e-9b88-7445c85f7c64' class='xr-var-data-in' type='checkbox'><label for='data-ae8b45bc-8b4f-4c2e-9b88-7445c85f7c64' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>long_name :</span></dt><dd>time</dd><dt><span>bounds :</span></dt><dd>time_bnds</dd></dl></div><div class='xr-var-data'><pre>array([&#x27;1880-01-15T00:00:00.000000000&#x27;, &#x27;1880-02-15T00:00:00.000000000&#x27;,
       &#x27;1880-03-15T00:00:00.000000000&#x27;, ..., &#x27;2021-10-15T00:00:00.000000000&#x27;,
       &#x27;2021-11-15T00:00:00.000000000&#x27;, &#x27;2021-12-15T00:00:00.000000000&#x27;],
      dtype=&#x27;datetime64[ns]&#x27;)</pre></div></li></ul></div></li><li class='xr-section-item'><input id='section-2807910d-d932-46a5-8ed2-a0f66f703101' class='xr-section-summary-in' type='checkbox'  checked><label for='section-2807910d-d932-46a5-8ed2-a0f66f703101' class='xr-section-summary' >Data variables: <span>(2)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><ul class='xr-var-list'><li class='xr-var-item'><div class='xr-var-name'><span>time_bnds</span></div><div class='xr-var-dims'>(time, nv)</div><div class='xr-var-dtype'>datetime64[ns]</div><div class='xr-var-preview xr-preview'>...</div><input id='attrs-54260cd4-6f77-45c2-b8ad-e1306ddf9f6c' class='xr-var-attrs-in' type='checkbox' disabled><label for='attrs-54260cd4-6f77-45c2-b8ad-e1306ddf9f6c' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-d7d9c08c-4538-4c17-b9ca-49f84ef7df6e' class='xr-var-data-in' type='checkbox'><label for='data-d7d9c08c-4538-4c17-b9ca-49f84ef7df6e' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'></dl></div><div class='xr-var-data'><pre>array([[&#x27;1880-01-01T00:00:00.000000000&#x27;, &#x27;1880-02-01T00:00:00.000000000&#x27;],
       [&#x27;1880-02-01T00:00:00.000000000&#x27;, &#x27;1880-03-01T00:00:00.000000000&#x27;],
       [&#x27;1880-03-01T00:00:00.000000000&#x27;, &#x27;1880-04-01T00:00:00.000000000&#x27;],
       ...,
       [&#x27;2021-10-01T00:00:00.000000000&#x27;, &#x27;2021-11-01T00:00:00.000000000&#x27;],
       [&#x27;2021-11-01T00:00:00.000000000&#x27;, &#x27;2021-12-01T00:00:00.000000000&#x27;],
       [&#x27;2021-12-01T00:00:00.000000000&#x27;, &#x27;2022-01-01T00:00:00.000000000&#x27;]],
      dtype=&#x27;datetime64[ns]&#x27;)</pre></div></li><li class='xr-var-item'><div class='xr-var-name'><span>tempanomaly</span></div><div class='xr-var-dims'>(time, lat, lon)</div><div class='xr-var-dtype'>float32</div><div class='xr-var-preview xr-preview'>...</div><input id='attrs-b88f90cb-8952-4426-9c10-d06f66929b84' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-b88f90cb-8952-4426-9c10-d06f66929b84' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-7e38b1cc-43eb-47a3-9b68-d616c23fb122' class='xr-var-data-in' type='checkbox'><label for='data-7e38b1cc-43eb-47a3-9b68-d616c23fb122' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>long_name :</span></dt><dd>Surface temperature anomaly</dd><dt><span>units :</span></dt><dd>K</dd><dt><span>cell_methods :</span></dt><dd>time: mean</dd></dl></div><div class='xr-var-data'><pre>[27604800 values with dtype=float32]</pre></div></li></ul></div></li><li class='xr-section-item'><input id='section-a39c8885-db9a-43d0-807f-1438b21dd3de' class='xr-section-summary-in' type='checkbox'  checked><label for='section-a39c8885-db9a-43d0-807f-1438b21dd3de' class='xr-section-summary' >Attributes: <span>(5)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><dl class='xr-attrs'><dt><span>title :</span></dt><dd>GISTEMP Surface Temperature Analysis</dd><dt><span>institution :</span></dt><dd>NASA Goddard Institute for Space Studies</dd><dt><span>source :</span></dt><dd>http://data.giss.nasa.gov/gistemp/</dd><dt><span>Conventions :</span></dt><dd>CF-1.6</dd><dt><span>history :</span></dt><dd>Created 2022-01-11 09:09:58 by SBBX_to_nc 2.0 - ILAND=1200, IOCEAN=NCDC/ER5, Base: 1951-1980</dd></dl></div></li></ul></div></div>




```python
yearly = ds.resample(time='Y').mean()
yearly
```




<div><svg style="position: absolute; width: 0; height: 0; overflow: hidden">
<defs>
<symbol id="icon-database" viewBox="0 0 32 32">
<path d="M16 0c-8.837 0-16 2.239-16 5v4c0 2.761 7.163 5 16 5s16-2.239 16-5v-4c0-2.761-7.163-5-16-5z"></path>
<path d="M16 17c-8.837 0-16-2.239-16-5v6c0 2.761 7.163 5 16 5s16-2.239 16-5v-6c0 2.761-7.163 5-16 5z"></path>
<path d="M16 26c-8.837 0-16-2.239-16-5v6c0 2.761 7.163 5 16 5s16-2.239 16-5v-6c0 2.761-7.163 5-16 5z"></path>
</symbol>
<symbol id="icon-file-text2" viewBox="0 0 32 32">
<path d="M28.681 7.159c-0.694-0.947-1.662-2.053-2.724-3.116s-2.169-2.030-3.116-2.724c-1.612-1.182-2.393-1.319-2.841-1.319h-15.5c-1.378 0-2.5 1.121-2.5 2.5v27c0 1.378 1.122 2.5 2.5 2.5h23c1.378 0 2.5-1.122 2.5-2.5v-19.5c0-0.448-0.137-1.23-1.319-2.841zM24.543 5.457c0.959 0.959 1.712 1.825 2.268 2.543h-4.811v-4.811c0.718 0.556 1.584 1.309 2.543 2.268zM28 29.5c0 0.271-0.229 0.5-0.5 0.5h-23c-0.271 0-0.5-0.229-0.5-0.5v-27c0-0.271 0.229-0.5 0.5-0.5 0 0 15.499-0 15.5 0v7c0 0.552 0.448 1 1 1h7v19.5z"></path>
<path d="M23 26h-14c-0.552 0-1-0.448-1-1s0.448-1 1-1h14c0.552 0 1 0.448 1 1s-0.448 1-1 1z"></path>
<path d="M23 22h-14c-0.552 0-1-0.448-1-1s0.448-1 1-1h14c0.552 0 1 0.448 1 1s-0.448 1-1 1z"></path>
<path d="M23 18h-14c-0.552 0-1-0.448-1-1s0.448-1 1-1h14c0.552 0 1 0.448 1 1s-0.448 1-1 1z"></path>
</symbol>
</defs>
</svg>
<style>/* CSS stylesheet for displaying xarray objects in jupyterlab.
 *
 */

:root {
  --xr-font-color0: var(--jp-content-font-color0, rgba(0, 0, 0, 1));
  --xr-font-color2: var(--jp-content-font-color2, rgba(0, 0, 0, 0.54));
  --xr-font-color3: var(--jp-content-font-color3, rgba(0, 0, 0, 0.38));
  --xr-border-color: var(--jp-border-color2, #e0e0e0);
  --xr-disabled-color: var(--jp-layout-color3, #bdbdbd);
  --xr-background-color: var(--jp-layout-color0, white);
  --xr-background-color-row-even: var(--jp-layout-color1, white);
  --xr-background-color-row-odd: var(--jp-layout-color2, #eeeeee);
}

html[theme=dark],
body.vscode-dark {
  --xr-font-color0: rgba(255, 255, 255, 1);
  --xr-font-color2: rgba(255, 255, 255, 0.54);
  --xr-font-color3: rgba(255, 255, 255, 0.38);
  --xr-border-color: #1F1F1F;
  --xr-disabled-color: #515151;
  --xr-background-color: #111111;
  --xr-background-color-row-even: #111111;
  --xr-background-color-row-odd: #313131;
}

.xr-wrap {
  display: block !important;
  min-width: 300px;
  max-width: 700px;
}

.xr-text-repr-fallback {
  /* fallback to plain text repr when CSS is not injected (untrusted notebook) */
  display: none;
}

.xr-header {
  padding-top: 6px;
  padding-bottom: 6px;
  margin-bottom: 4px;
  border-bottom: solid 1px var(--xr-border-color);
}

.xr-header > div,
.xr-header > ul {
  display: inline;
  margin-top: 0;
  margin-bottom: 0;
}

.xr-obj-type,
.xr-array-name {
  margin-left: 2px;
  margin-right: 10px;
}

.xr-obj-type {
  color: var(--xr-font-color2);
}

.xr-sections {
  padding-left: 0 !important;
  display: grid;
  grid-template-columns: 150px auto auto 1fr 20px 20px;
}

.xr-section-item {
  display: contents;
}

.xr-section-item input {
  display: none;
}

.xr-section-item input + label {
  color: var(--xr-disabled-color);
}

.xr-section-item input:enabled + label {
  cursor: pointer;
  color: var(--xr-font-color2);
}

.xr-section-item input:enabled + label:hover {
  color: var(--xr-font-color0);
}

.xr-section-summary {
  grid-column: 1;
  color: var(--xr-font-color2);
  font-weight: 500;
}

.xr-section-summary > span {
  display: inline-block;
  padding-left: 0.5em;
}

.xr-section-summary-in:disabled + label {
  color: var(--xr-font-color2);
}

.xr-section-summary-in + label:before {
  display: inline-block;
  content: '►';
  font-size: 11px;
  width: 15px;
  text-align: center;
}

.xr-section-summary-in:disabled + label:before {
  color: var(--xr-disabled-color);
}

.xr-section-summary-in:checked + label:before {
  content: '▼';
}

.xr-section-summary-in:checked + label > span {
  display: none;
}

.xr-section-summary,
.xr-section-inline-details {
  padding-top: 4px;
  padding-bottom: 4px;
}

.xr-section-inline-details {
  grid-column: 2 / -1;
}

.xr-section-details {
  display: none;
  grid-column: 1 / -1;
  margin-bottom: 5px;
}

.xr-section-summary-in:checked ~ .xr-section-details {
  display: contents;
}

.xr-array-wrap {
  grid-column: 1 / -1;
  display: grid;
  grid-template-columns: 20px auto;
}

.xr-array-wrap > label {
  grid-column: 1;
  vertical-align: top;
}

.xr-preview {
  color: var(--xr-font-color3);
}

.xr-array-preview,
.xr-array-data {
  padding: 0 5px !important;
  grid-column: 2;
}

.xr-array-data,
.xr-array-in:checked ~ .xr-array-preview {
  display: none;
}

.xr-array-in:checked ~ .xr-array-data,
.xr-array-preview {
  display: inline-block;
}

.xr-dim-list {
  display: inline-block !important;
  list-style: none;
  padding: 0 !important;
  margin: 0;
}

.xr-dim-list li {
  display: inline-block;
  padding: 0;
  margin: 0;
}

.xr-dim-list:before {
  content: '(';
}

.xr-dim-list:after {
  content: ')';
}

.xr-dim-list li:not(:last-child):after {
  content: ',';
  padding-right: 5px;
}

.xr-has-index {
  font-weight: bold;
}

.xr-var-list,
.xr-var-item {
  display: contents;
}

.xr-var-item > div,
.xr-var-item label,
.xr-var-item > .xr-var-name span {
  background-color: var(--xr-background-color-row-even);
  margin-bottom: 0;
}

.xr-var-item > .xr-var-name:hover span {
  padding-right: 5px;
}

.xr-var-list > li:nth-child(odd) > div,
.xr-var-list > li:nth-child(odd) > label,
.xr-var-list > li:nth-child(odd) > .xr-var-name span {
  background-color: var(--xr-background-color-row-odd);
}

.xr-var-name {
  grid-column: 1;
}

.xr-var-dims {
  grid-column: 2;
}

.xr-var-dtype {
  grid-column: 3;
  text-align: right;
  color: var(--xr-font-color2);
}

.xr-var-preview {
  grid-column: 4;
}

.xr-var-name,
.xr-var-dims,
.xr-var-dtype,
.xr-preview,
.xr-attrs dt {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  padding-right: 10px;
}

.xr-var-name:hover,
.xr-var-dims:hover,
.xr-var-dtype:hover,
.xr-attrs dt:hover {
  overflow: visible;
  width: auto;
  z-index: 1;
}

.xr-var-attrs,
.xr-var-data {
  display: none;
  background-color: var(--xr-background-color) !important;
  padding-bottom: 5px !important;
}

.xr-var-attrs-in:checked ~ .xr-var-attrs,
.xr-var-data-in:checked ~ .xr-var-data {
  display: block;
}

.xr-var-data > table {
  float: right;
}

.xr-var-name span,
.xr-var-data,
.xr-attrs {
  padding-left: 25px !important;
}

.xr-attrs,
.xr-var-attrs,
.xr-var-data {
  grid-column: 1 / -1;
}

dl.xr-attrs {
  padding: 0;
  margin: 0;
  display: grid;
  grid-template-columns: 125px auto;
}

.xr-attrs dt,
.xr-attrs dd {
  padding: 0;
  margin: 0;
  float: left;
  padding-right: 10px;
  width: auto;
}

.xr-attrs dt {
  font-weight: normal;
  grid-column: 1;
}

.xr-attrs dt:hover span {
  display: inline-block;
  background: var(--xr-background-color);
  padding-right: 10px;
}

.xr-attrs dd {
  grid-column: 2;
  white-space: pre-wrap;
  word-break: break-all;
}

.xr-icon-database,
.xr-icon-file-text2 {
  display: inline-block;
  vertical-align: middle;
  width: 1em;
  height: 1.5em !important;
  stroke-width: 0;
  stroke: currentColor;
  fill: currentColor;
}
</style><pre class='xr-text-repr-fallback'>&lt;xarray.Dataset&gt;
Dimensions:      (time: 142, lat: 90, lon: 180)
Coordinates:
  * time         (time) datetime64[ns] 1880-12-31 1881-12-31 ... 2021-12-31
  * lat          (lat) float32 -89.0 -87.0 -85.0 -83.0 ... 83.0 85.0 87.0 89.0
  * lon          (lon) float32 -179.0 -177.0 -175.0 -173.0 ... 175.0 177.0 179.0
Data variables:
    tempanomaly  (time, lat, lon) float32 nan nan nan nan ... 3.729 3.729 3.729</pre><div class='xr-wrap' style='display:none'><div class='xr-header'><div class='xr-obj-type'>xarray.Dataset</div></div><ul class='xr-sections'><li class='xr-section-item'><input id='section-6b6b38fd-1516-49b4-8af0-43e53ec379fb' class='xr-section-summary-in' type='checkbox' disabled ><label for='section-6b6b38fd-1516-49b4-8af0-43e53ec379fb' class='xr-section-summary'  title='Expand/collapse section'>Dimensions:</label><div class='xr-section-inline-details'><ul class='xr-dim-list'><li><span class='xr-has-index'>time</span>: 142</li><li><span class='xr-has-index'>lat</span>: 90</li><li><span class='xr-has-index'>lon</span>: 180</li></ul></div><div class='xr-section-details'></div></li><li class='xr-section-item'><input id='section-f64c7886-7c97-4cd6-a0aa-ba17359822f8' class='xr-section-summary-in' type='checkbox'  checked><label for='section-f64c7886-7c97-4cd6-a0aa-ba17359822f8' class='xr-section-summary' >Coordinates: <span>(3)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><ul class='xr-var-list'><li class='xr-var-item'><div class='xr-var-name'><span class='xr-has-index'>time</span></div><div class='xr-var-dims'>(time)</div><div class='xr-var-dtype'>datetime64[ns]</div><div class='xr-var-preview xr-preview'>1880-12-31 ... 2021-12-31</div><input id='attrs-295d3215-a7c5-463a-b6f7-333c925af72d' class='xr-var-attrs-in' type='checkbox' disabled><label for='attrs-295d3215-a7c5-463a-b6f7-333c925af72d' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-fab1b55c-f21f-4f11-afa1-e66d012d3080' class='xr-var-data-in' type='checkbox'><label for='data-fab1b55c-f21f-4f11-afa1-e66d012d3080' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'></dl></div><div class='xr-var-data'><pre>array([&#x27;1880-12-31T00:00:00.000000000&#x27;, &#x27;1881-12-31T00:00:00.000000000&#x27;,
       &#x27;1882-12-31T00:00:00.000000000&#x27;, &#x27;1883-12-31T00:00:00.000000000&#x27;,
       &#x27;1884-12-31T00:00:00.000000000&#x27;, &#x27;1885-12-31T00:00:00.000000000&#x27;,
       &#x27;1886-12-31T00:00:00.000000000&#x27;, &#x27;1887-12-31T00:00:00.000000000&#x27;,
       &#x27;1888-12-31T00:00:00.000000000&#x27;, &#x27;1889-12-31T00:00:00.000000000&#x27;,
       &#x27;1890-12-31T00:00:00.000000000&#x27;, &#x27;1891-12-31T00:00:00.000000000&#x27;,
       &#x27;1892-12-31T00:00:00.000000000&#x27;, &#x27;1893-12-31T00:00:00.000000000&#x27;,
       &#x27;1894-12-31T00:00:00.000000000&#x27;, &#x27;1895-12-31T00:00:00.000000000&#x27;,
       &#x27;1896-12-31T00:00:00.000000000&#x27;, &#x27;1897-12-31T00:00:00.000000000&#x27;,
       &#x27;1898-12-31T00:00:00.000000000&#x27;, &#x27;1899-12-31T00:00:00.000000000&#x27;,
       &#x27;1900-12-31T00:00:00.000000000&#x27;, &#x27;1901-12-31T00:00:00.000000000&#x27;,
       &#x27;1902-12-31T00:00:00.000000000&#x27;, &#x27;1903-12-31T00:00:00.000000000&#x27;,
       &#x27;1904-12-31T00:00:00.000000000&#x27;, &#x27;1905-12-31T00:00:00.000000000&#x27;,
       &#x27;1906-12-31T00:00:00.000000000&#x27;, &#x27;1907-12-31T00:00:00.000000000&#x27;,
       &#x27;1908-12-31T00:00:00.000000000&#x27;, &#x27;1909-12-31T00:00:00.000000000&#x27;,
       &#x27;1910-12-31T00:00:00.000000000&#x27;, &#x27;1911-12-31T00:00:00.000000000&#x27;,
       &#x27;1912-12-31T00:00:00.000000000&#x27;, &#x27;1913-12-31T00:00:00.000000000&#x27;,
       &#x27;1914-12-31T00:00:00.000000000&#x27;, &#x27;1915-12-31T00:00:00.000000000&#x27;,
       &#x27;1916-12-31T00:00:00.000000000&#x27;, &#x27;1917-12-31T00:00:00.000000000&#x27;,
       &#x27;1918-12-31T00:00:00.000000000&#x27;, &#x27;1919-12-31T00:00:00.000000000&#x27;,
       &#x27;1920-12-31T00:00:00.000000000&#x27;, &#x27;1921-12-31T00:00:00.000000000&#x27;,
       &#x27;1922-12-31T00:00:00.000000000&#x27;, &#x27;1923-12-31T00:00:00.000000000&#x27;,
       &#x27;1924-12-31T00:00:00.000000000&#x27;, &#x27;1925-12-31T00:00:00.000000000&#x27;,
       &#x27;1926-12-31T00:00:00.000000000&#x27;, &#x27;1927-12-31T00:00:00.000000000&#x27;,
       &#x27;1928-12-31T00:00:00.000000000&#x27;, &#x27;1929-12-31T00:00:00.000000000&#x27;,
       &#x27;1930-12-31T00:00:00.000000000&#x27;, &#x27;1931-12-31T00:00:00.000000000&#x27;,
       &#x27;1932-12-31T00:00:00.000000000&#x27;, &#x27;1933-12-31T00:00:00.000000000&#x27;,
       &#x27;1934-12-31T00:00:00.000000000&#x27;, &#x27;1935-12-31T00:00:00.000000000&#x27;,
       &#x27;1936-12-31T00:00:00.000000000&#x27;, &#x27;1937-12-31T00:00:00.000000000&#x27;,
       &#x27;1938-12-31T00:00:00.000000000&#x27;, &#x27;1939-12-31T00:00:00.000000000&#x27;,
       &#x27;1940-12-31T00:00:00.000000000&#x27;, &#x27;1941-12-31T00:00:00.000000000&#x27;,
       &#x27;1942-12-31T00:00:00.000000000&#x27;, &#x27;1943-12-31T00:00:00.000000000&#x27;,
       &#x27;1944-12-31T00:00:00.000000000&#x27;, &#x27;1945-12-31T00:00:00.000000000&#x27;,
       &#x27;1946-12-31T00:00:00.000000000&#x27;, &#x27;1947-12-31T00:00:00.000000000&#x27;,
       &#x27;1948-12-31T00:00:00.000000000&#x27;, &#x27;1949-12-31T00:00:00.000000000&#x27;,
       &#x27;1950-12-31T00:00:00.000000000&#x27;, &#x27;1951-12-31T00:00:00.000000000&#x27;,
       &#x27;1952-12-31T00:00:00.000000000&#x27;, &#x27;1953-12-31T00:00:00.000000000&#x27;,
       &#x27;1954-12-31T00:00:00.000000000&#x27;, &#x27;1955-12-31T00:00:00.000000000&#x27;,
       &#x27;1956-12-31T00:00:00.000000000&#x27;, &#x27;1957-12-31T00:00:00.000000000&#x27;,
       &#x27;1958-12-31T00:00:00.000000000&#x27;, &#x27;1959-12-31T00:00:00.000000000&#x27;,
       &#x27;1960-12-31T00:00:00.000000000&#x27;, &#x27;1961-12-31T00:00:00.000000000&#x27;,
       &#x27;1962-12-31T00:00:00.000000000&#x27;, &#x27;1963-12-31T00:00:00.000000000&#x27;,
       &#x27;1964-12-31T00:00:00.000000000&#x27;, &#x27;1965-12-31T00:00:00.000000000&#x27;,
       &#x27;1966-12-31T00:00:00.000000000&#x27;, &#x27;1967-12-31T00:00:00.000000000&#x27;,
       &#x27;1968-12-31T00:00:00.000000000&#x27;, &#x27;1969-12-31T00:00:00.000000000&#x27;,
       &#x27;1970-12-31T00:00:00.000000000&#x27;, &#x27;1971-12-31T00:00:00.000000000&#x27;,
       &#x27;1972-12-31T00:00:00.000000000&#x27;, &#x27;1973-12-31T00:00:00.000000000&#x27;,
       &#x27;1974-12-31T00:00:00.000000000&#x27;, &#x27;1975-12-31T00:00:00.000000000&#x27;,
       &#x27;1976-12-31T00:00:00.000000000&#x27;, &#x27;1977-12-31T00:00:00.000000000&#x27;,
       &#x27;1978-12-31T00:00:00.000000000&#x27;, &#x27;1979-12-31T00:00:00.000000000&#x27;,
       &#x27;1980-12-31T00:00:00.000000000&#x27;, &#x27;1981-12-31T00:00:00.000000000&#x27;,
       &#x27;1982-12-31T00:00:00.000000000&#x27;, &#x27;1983-12-31T00:00:00.000000000&#x27;,
       &#x27;1984-12-31T00:00:00.000000000&#x27;, &#x27;1985-12-31T00:00:00.000000000&#x27;,
       &#x27;1986-12-31T00:00:00.000000000&#x27;, &#x27;1987-12-31T00:00:00.000000000&#x27;,
       &#x27;1988-12-31T00:00:00.000000000&#x27;, &#x27;1989-12-31T00:00:00.000000000&#x27;,
       &#x27;1990-12-31T00:00:00.000000000&#x27;, &#x27;1991-12-31T00:00:00.000000000&#x27;,
       &#x27;1992-12-31T00:00:00.000000000&#x27;, &#x27;1993-12-31T00:00:00.000000000&#x27;,
       &#x27;1994-12-31T00:00:00.000000000&#x27;, &#x27;1995-12-31T00:00:00.000000000&#x27;,
       &#x27;1996-12-31T00:00:00.000000000&#x27;, &#x27;1997-12-31T00:00:00.000000000&#x27;,
       &#x27;1998-12-31T00:00:00.000000000&#x27;, &#x27;1999-12-31T00:00:00.000000000&#x27;,
       &#x27;2000-12-31T00:00:00.000000000&#x27;, &#x27;2001-12-31T00:00:00.000000000&#x27;,
       &#x27;2002-12-31T00:00:00.000000000&#x27;, &#x27;2003-12-31T00:00:00.000000000&#x27;,
       &#x27;2004-12-31T00:00:00.000000000&#x27;, &#x27;2005-12-31T00:00:00.000000000&#x27;,
       &#x27;2006-12-31T00:00:00.000000000&#x27;, &#x27;2007-12-31T00:00:00.000000000&#x27;,
       &#x27;2008-12-31T00:00:00.000000000&#x27;, &#x27;2009-12-31T00:00:00.000000000&#x27;,
       &#x27;2010-12-31T00:00:00.000000000&#x27;, &#x27;2011-12-31T00:00:00.000000000&#x27;,
       &#x27;2012-12-31T00:00:00.000000000&#x27;, &#x27;2013-12-31T00:00:00.000000000&#x27;,
       &#x27;2014-12-31T00:00:00.000000000&#x27;, &#x27;2015-12-31T00:00:00.000000000&#x27;,
       &#x27;2016-12-31T00:00:00.000000000&#x27;, &#x27;2017-12-31T00:00:00.000000000&#x27;,
       &#x27;2018-12-31T00:00:00.000000000&#x27;, &#x27;2019-12-31T00:00:00.000000000&#x27;,
       &#x27;2020-12-31T00:00:00.000000000&#x27;, &#x27;2021-12-31T00:00:00.000000000&#x27;],
      dtype=&#x27;datetime64[ns]&#x27;)</pre></div></li><li class='xr-var-item'><div class='xr-var-name'><span class='xr-has-index'>lat</span></div><div class='xr-var-dims'>(lat)</div><div class='xr-var-dtype'>float32</div><div class='xr-var-preview xr-preview'>-89.0 -87.0 -85.0 ... 87.0 89.0</div><input id='attrs-649aac71-a9df-45cd-b74f-b677f88de690' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-649aac71-a9df-45cd-b74f-b677f88de690' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-6f668209-22cd-437a-9d98-d12638e04416' class='xr-var-data-in' type='checkbox'><label for='data-6f668209-22cd-437a-9d98-d12638e04416' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>standard_name :</span></dt><dd>latitude</dd><dt><span>long_name :</span></dt><dd>Latitude</dd><dt><span>units :</span></dt><dd>degrees_north</dd></dl></div><div class='xr-var-data'><pre>array([-89., -87., -85., -83., -81., -79., -77., -75., -73., -71., -69., -67.,
       -65., -63., -61., -59., -57., -55., -53., -51., -49., -47., -45., -43.,
       -41., -39., -37., -35., -33., -31., -29., -27., -25., -23., -21., -19.,
       -17., -15., -13., -11.,  -9.,  -7.,  -5.,  -3.,  -1.,   1.,   3.,   5.,
         7.,   9.,  11.,  13.,  15.,  17.,  19.,  21.,  23.,  25.,  27.,  29.,
        31.,  33.,  35.,  37.,  39.,  41.,  43.,  45.,  47.,  49.,  51.,  53.,
        55.,  57.,  59.,  61.,  63.,  65.,  67.,  69.,  71.,  73.,  75.,  77.,
        79.,  81.,  83.,  85.,  87.,  89.], dtype=float32)</pre></div></li><li class='xr-var-item'><div class='xr-var-name'><span class='xr-has-index'>lon</span></div><div class='xr-var-dims'>(lon)</div><div class='xr-var-dtype'>float32</div><div class='xr-var-preview xr-preview'>-179.0 -177.0 ... 177.0 179.0</div><input id='attrs-17ef01ff-9bb3-4407-97b5-cacd9300ad24' class='xr-var-attrs-in' type='checkbox' ><label for='attrs-17ef01ff-9bb3-4407-97b5-cacd9300ad24' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-65fe4905-a3d2-4f57-8507-e40688a2619c' class='xr-var-data-in' type='checkbox'><label for='data-65fe4905-a3d2-4f57-8507-e40688a2619c' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'><dt><span>standard_name :</span></dt><dd>longitude</dd><dt><span>long_name :</span></dt><dd>Longitude</dd><dt><span>units :</span></dt><dd>degrees_east</dd></dl></div><div class='xr-var-data'><pre>array([-179., -177., -175., -173., -171., -169., -167., -165., -163., -161.,
       -159., -157., -155., -153., -151., -149., -147., -145., -143., -141.,
       -139., -137., -135., -133., -131., -129., -127., -125., -123., -121.,
       -119., -117., -115., -113., -111., -109., -107., -105., -103., -101.,
        -99.,  -97.,  -95.,  -93.,  -91.,  -89.,  -87.,  -85.,  -83.,  -81.,
        -79.,  -77.,  -75.,  -73.,  -71.,  -69.,  -67.,  -65.,  -63.,  -61.,
        -59.,  -57.,  -55.,  -53.,  -51.,  -49.,  -47.,  -45.,  -43.,  -41.,
        -39.,  -37.,  -35.,  -33.,  -31.,  -29.,  -27.,  -25.,  -23.,  -21.,
        -19.,  -17.,  -15.,  -13.,  -11.,   -9.,   -7.,   -5.,   -3.,   -1.,
          1.,    3.,    5.,    7.,    9.,   11.,   13.,   15.,   17.,   19.,
         21.,   23.,   25.,   27.,   29.,   31.,   33.,   35.,   37.,   39.,
         41.,   43.,   45.,   47.,   49.,   51.,   53.,   55.,   57.,   59.,
         61.,   63.,   65.,   67.,   69.,   71.,   73.,   75.,   77.,   79.,
         81.,   83.,   85.,   87.,   89.,   91.,   93.,   95.,   97.,   99.,
        101.,  103.,  105.,  107.,  109.,  111.,  113.,  115.,  117.,  119.,
        121.,  123.,  125.,  127.,  129.,  131.,  133.,  135.,  137.,  139.,
        141.,  143.,  145.,  147.,  149.,  151.,  153.,  155.,  157.,  159.,
        161.,  163.,  165.,  167.,  169.,  171.,  173.,  175.,  177.,  179.],
      dtype=float32)</pre></div></li></ul></div></li><li class='xr-section-item'><input id='section-53f063c9-ab6f-43ca-ba47-8584c50fd134' class='xr-section-summary-in' type='checkbox'  checked><label for='section-53f063c9-ab6f-43ca-ba47-8584c50fd134' class='xr-section-summary' >Data variables: <span>(1)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><ul class='xr-var-list'><li class='xr-var-item'><div class='xr-var-name'><span>tempanomaly</span></div><div class='xr-var-dims'>(time, lat, lon)</div><div class='xr-var-dtype'>float32</div><div class='xr-var-preview xr-preview'>nan nan nan ... 3.729 3.729 3.729</div><input id='attrs-7e6da35a-01fe-4b85-9ec9-56985f88ca5c' class='xr-var-attrs-in' type='checkbox' disabled><label for='attrs-7e6da35a-01fe-4b85-9ec9-56985f88ca5c' title='Show/Hide attributes'><svg class='icon xr-icon-file-text2'><use xlink:href='#icon-file-text2'></use></svg></label><input id='data-abd4c6e7-7688-4e60-a660-c9288a81b652' class='xr-var-data-in' type='checkbox'><label for='data-abd4c6e7-7688-4e60-a660-c9288a81b652' title='Show/Hide data repr'><svg class='icon xr-icon-database'><use xlink:href='#icon-database'></use></svg></label><div class='xr-var-attrs'><dl class='xr-attrs'></dl></div><div class='xr-var-data'><pre>array([[[        nan,         nan,         nan, ...,         nan,
                 nan,         nan],
        [        nan,         nan,         nan, ...,         nan,
                 nan,         nan],
        [        nan,         nan,         nan, ...,         nan,
                 nan,         nan],
        ...,
        [        nan,         nan,         nan, ...,         nan,
                 nan,         nan],
        [        nan,         nan,         nan, ...,         nan,
                 nan,         nan],
        [        nan,         nan,         nan, ...,         nan,
                 nan,         nan]],

       [[        nan,         nan,         nan, ...,         nan,
                 nan,         nan],
        [        nan,         nan,         nan, ...,         nan,
                 nan,         nan],
        [        nan,         nan,         nan, ...,         nan,
                 nan,         nan],
...
        [ 3.7966664 ,  3.7966664 ,  3.7966664 , ...,  3.7966664 ,
          3.7966664 ,  3.7966664 ],
        [ 3.7966664 ,  3.7966664 ,  3.7966664 , ...,  3.7966664 ,
          3.7966664 ,  3.7966664 ],
        [ 3.7966664 ,  3.7966664 ,  3.7966664 , ...,  3.7966664 ,
          3.7966664 ,  3.7966664 ]],

       [[-1.0675001 , -1.0675001 , -1.0675001 , ..., -1.0675001 ,
         -1.0675001 , -1.0675001 ],
        [-1.0675001 , -1.0675001 , -1.0675001 , ..., -1.0675001 ,
         -1.0675001 , -1.0675001 ],
        [-1.0675001 , -1.0675001 , -1.0675001 , ..., -1.0675001 ,
         -1.0675001 , -1.0675001 ],
        ...,
        [ 3.7291667 ,  3.7291667 ,  3.7291667 , ...,  3.7291667 ,
          3.7291667 ,  3.7291667 ],
        [ 3.7291667 ,  3.7291667 ,  3.7291667 , ...,  3.7291667 ,
          3.7291667 ,  3.7291667 ],
        [ 3.7291667 ,  3.7291667 ,  3.7291667 , ...,  3.7291667 ,
          3.7291667 ,  3.7291667 ]]], dtype=float32)</pre></div></li></ul></div></li><li class='xr-section-item'><input id='section-7dd20d7b-acea-4cd5-95a8-a6067e48f0e6' class='xr-section-summary-in' type='checkbox' disabled ><label for='section-7dd20d7b-acea-4cd5-95a8-a6067e48f0e6' class='xr-section-summary'  title='Expand/collapse section'>Attributes: <span>(0)</span></label><div class='xr-section-inline-details'></div><div class='xr-section-details'><dl class='xr-attrs'></dl></div></li></ul></div></div>




```python
anomaly = yearly['tempanomaly']
anomaly2021 = anomaly.isel(time=-1)
```


```python
from xarray.plot import imshow
imshow(anomaly2021)
```




    <matplotlib.image.AxesImage at 0x17acff070>




    
![](08_mapping_gridded_datasets_files/08_mapping_gridded_datasets_7_1.png)
    



```python
ax = plt.axes(projection=ccrs.Orthographic(0, 40))
ax.coastlines()
fig = plt.gcf()
fig.set_size_inches(5,5)
plt.show()
```


    
![](08_mapping_gridded_datasets_files/08_mapping_gridded_datasets_8_0.png)
    



```python
ax = plt.axes(projection=ccrs.Orthographic(0, 30))
ax.coastlines()
anomaly2021.plot.imshow(ax=ax,
    vmin=-4, vmax=4, cmap='coolwarm',
    transform=ccrs.PlateCarree())

fig = plt.gcf()
fig.set_size_inches(5,5)
plt.tight_layout()
plt.show()
```


    
![](08_mapping_gridded_datasets_files/08_mapping_gridded_datasets_9_0.png)
    


https://matplotlib.org/stable/api/_as_gen/matplotlib.pyplot.colorbar.html


```python
cbar_kwargs = {
    'orientation':'horizontal',
    'location': 'bottom',
    'fraction': 0.025,
    'pad': 0.05,
    'extend':'neither'
}

ax = plt.axes(projection=ccrs.Orthographic(0, 30))
ax.coastlines()
anomaly2021.plot.imshow(
    ax=ax,
    vmin=-4, vmax=4, cmap='coolwarm',
    transform=ccrs.PlateCarree(),
    add_labels=False,
    cbar_kwargs=cbar_kwargs)

fig = plt.gcf()
fig.set_size_inches(10,10)
plt.title('Temprature Anomaly in 2021 (°C)', fontsize = 14)

output_folder = 'output'
output_path = os.path.join(output_folder, 'anomaly.jpg')
plt.savefig(output_path, dpi=300)
plt.show()
```


    
![](08_mapping_gridded_datasets_files/08_mapping_gridded_datasets_11_0.png)
    



```python

```