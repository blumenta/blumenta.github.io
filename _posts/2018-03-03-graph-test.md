

```python
import numpy as np
import scipy.stats as st
import ipywidgets as widgets
import plotly as pl
import plotly.graph_objs as go

pl.offline.init_notebook_mode(connected=True)
```


<script>requirejs.config({paths: { 'plotly': ['https://cdn.plot.ly/plotly-latest.min']},});if(!window.Plotly) {{require(['plotly'],function(plotly) {window.Plotly=plotly;});}}</script>



```python
x = np.linspace(0, 1 , 1000)
M = 20
pdfs = [[st.beta.pdf(x,a,b) for b in range(1,M+1)] for a in range(1,M+1)]
```


```python
import pandas as pd
#pd.DataFrame('x':)
```


```python
layout = go.Layout(
    title='Beta distribution density',
    yaxis = dict(
        title='f(x,a,b)'
    ),
    xaxis = dict(
        title='x'
    )
)

def update_plot(a, b):
    trace = go.Scatter(
                x = x,
                y = pdfs[a-1][b-1],#st.beta.pdf(x,a,b),
                mode='lines', #'markers'
                name = 'Beta(%.1f,%.1f)'%(a,b),
                line = dict(
                    shape = 'spline'
                )
            )
    fig = go.Figure(data=[trace], layout=layout)
    pl.offline.iplot(fig)

#signals = widgets.SelectMultiple(options = list(range(6)), value = (0,), description = 'Bessel order')
a = widgets.IntSlider(min=1, max=M, value=1, description='a')
b = widgets.IntSlider(min=1, max=M, value=1, description='b')
widgets.interactive(update_plot, a=a, b=b)
```


<p>Failed to display Jupyter Widget of type <code>interactive</code>.</p>
<p>
  If you're reading this message in the Jupyter Notebook or JupyterLab Notebook, it may mean
  that the widgets JavaScript is still loading. If this message persists, it
  likely means that the widgets JavaScript library is either not installed or
  not enabled. See the <a href="https://ipywidgets.readthedocs.io/en/stable/user_install.html">Jupyter
  Widgets Documentation</a> for setup instructions.
</p>
<p>
  If you're reading this message in another frontend (for example, a static
  rendering on GitHub or <a href="https://nbviewer.jupyter.org/">NBViewer</a>),
  it may mean that your frontend doesn't currently support widgets.
</p>



* Ok, cool. But to put it in a blog I would need to precompute the pdfs for predefined values of a,b and store them.
* Why does the legend not pop up?
* can it do latex labels?
