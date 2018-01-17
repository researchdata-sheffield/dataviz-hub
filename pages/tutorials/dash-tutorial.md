---
title: Visualising data on the web with Python and Dash
---

[Dash](https://plot.ly/dash/) is a user interface library for creating analytical web applications. Those who use [Python](https://python.org) for data analysis, data exploration, visualization, modelling, instrument control, and reporting will find immediate use for Dash.

[Read the full documentation for Dash](https://plot.ly/dash/)

------------------------------------------------------------------------------

**Contents**

[TOC]

## 1. Installation

In order to run Dash app in a Flask server install the following libraries.

Make sure you have installed **Python** (https://www.python.org/downloads/) and **pip** (https://pip.pypa.io/en/stable/installing/)
{: .alert .alert-block .alert-warning }


```sh
pip install dash==0.19.0  # The core dash backend
pip install dash-renderer==0.11.1  # The dash front-end
pip install dash-html-components==0.8.0  # HTML components
pip install dash-core-components==0.15.2  # Supercharged components
pip install plotly --upgrade  # Latest Plotly graphing library
```

## 2. About this example

In this example we are going to build a graph that shows life expectancy in comparison to GDP per capita based in all countries around the World.

## 3. First step

Besides Dash, we are using __Pandas__ for extract and manipulate data and __Plotly__ to render the output into a Graph. In order to use those libraries you first need to import them:


```python
import dash
import dash_core_components as dcc
import dash_html_components as html

import plotly.graph_objs as go

import pandas as pd
```

## 4. Download and read a CSV file

Use Panda's `read_csv` function to download and extract your dataset. When you read a CSV, you get a `DataFrame`, which is made up of rows and columns. You access columns in a DataFrame the same way you access elements of a dictionary.


```python
df = pd.read_csv('https://ndownloader.figsh.com/files/8261349')
```

## 5. Preview Dataset

Function `head()` gives you a preview of the downloaded dataset.

```python
df.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>country</th>
      <th>continent</th>
      <th>population</th>
      <th>life expectancy</th>
      <th>gdp per capita</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>11</td>
      <td>Afghanistan</td>
      <td>Asia</td>
      <td>31889923.0</td>
      <td>43.828</td>
      <td>974.580338</td>
    </tr>
    <tr>
      <th>1</th>
      <td>23</td>
      <td>Albania</td>
      <td>Europe</td>
      <td>3600523.0</td>
      <td>76.423</td>
      <td>5937.029526</td>
    </tr>
    <tr>
      <th>2</th>
      <td>35</td>
      <td>Algeria</td>
      <td>Africa</td>
      <td>33333216.0</td>
      <td>72.301</td>
      <td>6223.367465</td>
    </tr>
    <tr>
      <th>3</th>
      <td>47</td>
      <td>Angola</td>
      <td>Africa</td>
      <td>12420476.0</td>
      <td>42.731</td>
      <td>4797.231267</td>
    </tr>
    <tr>
      <th>4</th>
      <td>59</td>
      <td>Argentina</td>
      <td>Americas</td>
      <td>40301927.0</td>
      <td>75.320</td>
      <td>12779.379640</td>
    </tr>
  </tbody>
</table>
</div>



## 6. Layout
Dash apps are composed of two parts: __Layout__ and __Interactivity__.
The first part is the "layout" of the app and it describes what the application looks like.

In this example we are going to create two kinds of filter:

1. Countries: Multiple selection combo box with a list of all countries included on the Dataset
2. Life Expectancy: Slider with a range of ages (min and max)

<!-- ![filter.PNG](attachment:filter.PNG) -->


```python
countries = df['country'].unique()

app = dash.Dash()

app.layout = html.Div([

    html.Div([
        html.Label('Country'),
        dcc.Dropdown(
            id='country',
            options=[{'label': i, 'value': i} for i in countries],
            value='',
            placeholder='Select...',
            multi=True
        )
    ],    
    style={'width': '20%', 'display': 'inline-block', 'margin-bottom': '20px'}),    

    html.Div([
        html.Label('Life Expectancy'),
        dcc.Slider(
            id='expectancy-slider',
            min=30,
            max=80,
            value=30,
            step=None,
            marks={'30':'>30', '40':'>40', '50':'>50', '60':'>60', '70':'>70', '80':'>80'}
        ),
    ],
    style={'width': '20%', 'display': 'inline-block', 'margin-bottom': '20px', 'margin-left': '20px'}),

    html.Div([
        dcc.Graph(id='life-exp-vs-gdp'),
    ],
    style={'width': '70%'}),
])
```

## 7. Interactivity

Dash provides a simple reactive decorator for binding your custom data analysis code to your Dash user interface.  
When an input element changes (e.g. when you select an item in the dropdown or drag the slider), Dash’s decorator provides your Python code with the new value of the input.  
In this example we are calling the `update_graph` function each time either a country is selected or a life expectancy range is set.


```python
@app.callback(
    dash.dependencies.Output('life-exp-vs-gdp', 'figure'),
    [
        dash.dependencies.Input('expectancy-slider', 'value'),
        dash.dependencies.Input('country', 'value')
    ])
def update_graph(expectancy, country):
    
    filtered_df = df.loc[df["life expectancy"] > expectancy]

    if (country != '' and country is not None):
        filtered_df = filtered_df[df.country.str.contains('|'.join(country))]

    traces = []
    for i in filtered_df.continent.unique():
        df_by_continent = filtered_df[filtered_df['continent'] == i]
        traces.append(go.Scatter(
            x=df_by_continent['gdp per capita'],
            y=df_by_continent['life expectancy'],
            text=df_by_continent['country'],
            mode='markers',
            opacity=0.7,
            marker={
                'size': 15,
                'line': {'width': 0.5, 'color': 'white'}
            },
            name=i
        ))

    return {
        'data': traces,
        'layout': go.Layout(
            xaxis={'title': 'GDP Per Capita', 'titlefont': dict(size=18, color='darkgrey'), 'zeroline': False, 'ticks': 'outside' },
            yaxis={'title': 'Life Expectancy', 'titlefont': dict(size=18, color='darkgrey'), 'range': [30, 90], 'ticks': 'outside'},
            margin={'l': 60, 'b': 60, 't': 30, 'r': 20},
            legend={'x': 1, 'y': 1},
            hovermode='closest'
        )
    }
```

## 8. Style

Every aesthetic element of the app is customisable: The sizing, the positioning, the colors, the fonts. Dash apps are built and published in the Web, so the full power of CSS is available. 

Use `app.css.append_css` in order to set an external CSS file


```python
app.css.append_css({
    "external_url": "https://codepen.io/chriddyp/pen/bWLwgP.css"
})
```

## 9. Running Application

Dash apps are web applications. Dash uses Flask as the web framework. The underlying Flask app is available at app.server, and for the purpose of running the application you should call `run_server` function in your python code as you can see below.

```python
if __name__ == '__main__':
    app.run_server(debug=True)
```

If it all works correctly, your app should be running and accessible in your web browser; the default address is <http://127.0.0.1:8050/>. It should look something like this:

<iframe src="https://dash-tutorial.herokuapp.com/" style="height: 600px; width: 100%;" frameBorder="0"></iframe>

------------------------------------------------------------------------------

**Related technologies:**

 - [Pandas](https://pandas.pydata.org/)
 - [Plotly](https://plot.ly/)
 - [React.js](https://reactjs.org/)
 - [Flask](http://flask.pocoo.org/)
