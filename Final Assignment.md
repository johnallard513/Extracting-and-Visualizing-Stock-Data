<center>
    <img src="https://s3-api.us-geo.objectstorage.softlayer.net/cf-courses-data/CognitiveClass/Logos/organization_logo/organization_logo.png" width="300" alt="cognitiveclass.ai logo"  />
</center>


<h1>Extracting and Visualizing Stock Data</h1>
<h2>Description</h2>


Extracting essential data from a dataset and displaying it is a necessary part of data science; therefore individuals can make correct decisions based on the data. In this assignment, you will extract some stock data, you will then display this data in a graph.


<h2>Table of Contents</h2>
<div class="alert alert-block alert-info" style="margin-top: 20px">
    <ul>
        <li>Define a Function that Makes a Graph</li>
        <li>Question 1: Use yfinance to Extract Stock Data</li>
        <li>Question 2: Use Webscraping to Extract Tesla Revenue Data</li>
        <li>Question 3: Use yfinance to Extract Stock Data</li>
        <li>Question 4: Use Webscraping to Extract GME Revenue Data</li>
        <li>Question 5: Plot Tesla Stock Graph</li>
        <li>Question 6: Plot GameStop Stock Graph</li>
    </ul>
<p>
    Estimated Time Needed: <strong>30 min</strong></p>
</div>

<hr>



```python
!pip install yfinance==0.1.67
#!pip install pandas==1.3.3
#!pip install requests==2.26.0
!mamba install bs4==4.10.0 -y
#!pip install plotly==5.3.1
!pip install bs4
```

    Collecting yfinance==0.1.67
      Downloading yfinance-0.1.67-py2.py3-none-any.whl (25 kB)
    Requirement already satisfied: pandas>=0.24 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from yfinance==0.1.67) (1.3.5)
    Requirement already satisfied: requests>=2.20 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from yfinance==0.1.67) (2.28.1)
    Requirement already satisfied: lxml>=4.5.1 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from yfinance==0.1.67) (4.9.1)
    Collecting multitasking>=0.0.7
      Downloading multitasking-0.0.11-py3-none-any.whl (8.5 kB)
    Requirement already satisfied: numpy>=1.15 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from yfinance==0.1.67) (1.21.6)
    Requirement already satisfied: python-dateutil>=2.7.3 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from pandas>=0.24->yfinance==0.1.67) (2.8.2)
    Requirement already satisfied: pytz>=2017.3 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from pandas>=0.24->yfinance==0.1.67) (2022.6)
    Requirement already satisfied: charset-normalizer<3,>=2 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from requests>=2.20->yfinance==0.1.67) (2.1.1)
    Requirement already satisfied: certifi>=2017.4.17 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from requests>=2.20->yfinance==0.1.67) (2022.9.24)
    Requirement already satisfied: urllib3<1.27,>=1.21.1 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from requests>=2.20->yfinance==0.1.67) (1.26.11)
    Requirement already satisfied: idna<4,>=2.5 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from requests>=2.20->yfinance==0.1.67) (3.4)
    Requirement already satisfied: six>=1.5 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from python-dateutil>=2.7.3->pandas>=0.24->yfinance==0.1.67) (1.16.0)
    Installing collected packages: multitasking, yfinance
    Successfully installed multitasking-0.0.11 yfinance-0.1.67
    
                      __    __    __    __
                     /  \  /  \  /  \  /  \
                    /    \/    \/    \/    \
    ███████████████/  /██/  /██/  /██/  /████████████████████████
                  /  / \   / \   / \   / \  \____
                 /  /   \_/   \_/   \_/   \    o \__,
                / _/                       \_____/  `
                |/
            ███╗   ███╗ █████╗ ███╗   ███╗██████╗  █████╗
            ████╗ ████║██╔══██╗████╗ ████║██╔══██╗██╔══██╗
            ██╔████╔██║███████║██╔████╔██║██████╔╝███████║
            ██║╚██╔╝██║██╔══██║██║╚██╔╝██║██╔══██╗██╔══██║
            ██║ ╚═╝ ██║██║  ██║██║ ╚═╝ ██║██████╔╝██║  ██║
            ╚═╝     ╚═╝╚═╝  ╚═╝╚═╝     ╚═╝╚═════╝ ╚═╝  ╚═╝
    
            mamba (0.15.3) supported by @QuantStack
    
            GitHub:  https://github.com/mamba-org/mamba
            Twitter: https://twitter.com/QuantStack
    
    █████████████████████████████████████████████████████████████
    
    
    Looking for: ['bs4==4.10.0']
    
    pkgs/main/linux-64       [<=>                 ] (00m:00s) 
    pkgs/main/linux-64       [=>                ] (00m:00s) 10 KB / ?? (65.51 KB/s)
    pkgs/main/linux-64       [=>                ] (00m:00s) 10 KB / ?? (65.51 KB/s)
    pkgs/main/noarch         [<=>                 ] (00m:00s) 
    pkgs/main/linux-64       [=>                ] (00m:00s) 10 KB / ?? (65.51 KB/s)
    pkgs/main/noarch         [=>               ] (00m:00s) 40 KB / ?? (266.10 KB/s)
    pkgs/main/linux-64       [<=>               ] (00m:00s) 10 KB / ?? (65.51 KB/s)
    pkgs/main/noarch         [=>               ] (00m:00s) 40 KB / ?? (266.10 KB/s)
    pkgs/main/linux-64       [<=>               ] (00m:00s) 792 KB / ?? (2.56 MB/s)
    pkgs/main/noarch         [=>               ] (00m:00s) 40 KB / ?? (266.10 KB/s)
    pkgs/main/linux-64       [<=>               ] (00m:00s) 792 KB / ?? (2.56 MB/s)
    pkgs/main/noarch         [<=>              ] (00m:00s) 40 KB / ?? (266.10 KB/s)
    pkgs/main/linux-64       [<=>               ] (00m:00s) 792 KB / ?? (2.56 MB/s)
    pkgs/main/noarch         [<=>               ] (00m:00s) 732 KB / ?? (2.36 MB/s)
    pkgs/main/linux-64       [<=>               ] (00m:00s) 792 KB / ?? (2.56 MB/s)
    pkgs/main/noarch         [<=>               ] (00m:00s) 732 KB / ?? (2.36 MB/s)
    pkgs/r/linux-64          [<=>                 ] (00m:00s) 
    pkgs/main/linux-64       [<=>               ] (00m:00s) 792 KB / ?? (2.56 MB/s)
    pkgs/main/noarch         [<=>               ] (00m:00s) 732 KB / ?? (2.36 MB/s)
    pkgs/r/linux-64          [=>                ] (00m:00s) 652 KB / ?? (2.10 MB/s)
    pkgs/main/linux-64       [<=>               ] (00m:00s) 792 KB / ?? (2.56 MB/s)
    pkgs/main/noarch         [<=>               ] (00m:00s) 732 KB / ?? (2.36 MB/s)
    pkgs/r/linux-64          [=>                ] (00m:00s) 652 KB / ?? (2.10 MB/s)
    pkgs/r/noarch            [<=>                 ] (00m:00s) 
    pkgs/main/linux-64       [<=>               ] (00m:00s) 792 KB / ?? (2.56 MB/s)
    pkgs/main/noarch         [<=>               ] (00m:00s) 732 KB / ?? (2.36 MB/s)
    pkgs/r/linux-64          [=>                ] (00m:00s) 652 KB / ?? (2.10 MB/s)
    pkgs/r/noarch            [=>                ] (00m:00s) 432 KB / ?? (1.39 MB/s)
    pkgs/main/linux-64       [<=>               ] (00m:00s) 792 KB / ?? (2.56 MB/s)
    pkgs/main/noarch         [ <=>                ] (00m:00s) Finalizing...
    pkgs/r/linux-64          [=>                ] (00m:00s) 652 KB / ?? (2.10 MB/s)
    pkgs/r/noarch            [=>                ] (00m:00s) 432 KB / ?? (1.39 MB/s)
    pkgs/main/linux-64       [<=>               ] (00m:00s) 792 KB / ?? (2.56 MB/s)
    pkgs/main/noarch         [ <=>                ] (00m:00s) Done
    pkgs/r/linux-64          [=>                ] (00m:00s) 652 KB / ?? (2.10 MB/s)
    pkgs/r/noarch            [=>                ] (00m:00s) 432 KB / ?? (1.39 MB/s)
    pkgs/main/noarch         [====================] (00m:00s) Done
    pkgs/main/linux-64       [<=>               ] (00m:00s) 792 KB / ?? (2.56 MB/s)
    pkgs/r/linux-64          [=>                ] (00m:00s) 652 KB / ?? (2.10 MB/s)
    pkgs/r/noarch            [=>                ] (00m:00s) 432 KB / ?? (1.39 MB/s)
    pkgs/main/linux-64       [ <=>              ] (00m:00s) 792 KB / ?? (2.56 MB/s)
    pkgs/r/linux-64          [=>                ] (00m:00s) 652 KB / ?? (2.10 MB/s)
    pkgs/r/noarch            [=>                ] (00m:00s) 432 KB / ?? (1.39 MB/s)
    pkgs/main/linux-64       [  <=>               ] (00m:00s) 1 MB / ?? (3.31 MB/s)
    pkgs/r/linux-64          [=>                ] (00m:00s) 652 KB / ?? (2.10 MB/s)
    pkgs/r/noarch            [=>                ] (00m:00s) 432 KB / ?? (1.39 MB/s)
    pkgs/main/linux-64       [  <=>               ] (00m:00s) 1 MB / ?? (3.31 MB/s)
    pkgs/r/linux-64          [<=>               ] (00m:00s) 652 KB / ?? (2.10 MB/s)
    pkgs/r/noarch            [=>                ] (00m:00s) 432 KB / ?? (1.39 MB/s)
    pkgs/main/linux-64       [  <=>               ] (00m:00s) 1 MB / ?? (3.31 MB/s)
    pkgs/r/linux-64          [ <=>                ] (00m:00s) 1 MB / ?? (2.85 MB/s)
    pkgs/r/noarch            [=>                ] (00m:00s) 432 KB / ?? (1.39 MB/s)
    pkgs/main/linux-64       [  <=>               ] (00m:00s) 1 MB / ?? (3.31 MB/s)
    pkgs/r/linux-64          [ <=>                ] (00m:00s) 1 MB / ?? (2.85 MB/s)
    pkgs/r/noarch            [<=>               ] (00m:00s) 432 KB / ?? (1.39 MB/s)
    pkgs/main/linux-64       [  <=>               ] (00m:00s) 1 MB / ?? (3.31 MB/s)
    pkgs/r/linux-64          [ <=>                ] (00m:00s) 1 MB / ?? (2.85 MB/s)
    pkgs/r/noarch            [<=>               ] (00m:00s) 856 KB / ?? (1.84 MB/s)
    pkgs/main/linux-64       [  <=>               ] (00m:00s) 1 MB / ?? (3.31 MB/s)
    pkgs/r/linux-64          [ <=>                ] (00m:00s) Finalizing...
    pkgs/r/noarch            [<=>               ] (00m:00s) 856 KB / ?? (1.84 MB/s)
    pkgs/main/linux-64       [  <=>               ] (00m:00s) 1 MB / ?? (3.31 MB/s)
    pkgs/r/linux-64          [ <=>                ] (00m:00s) Done
    pkgs/r/noarch            [<=>               ] (00m:00s) 856 KB / ?? (1.84 MB/s)
    pkgs/r/linux-64          [====================] (00m:00s) Done
    pkgs/main/linux-64       [  <=>               ] (00m:00s) 1 MB / ?? (3.31 MB/s)
    pkgs/r/noarch            [<=>               ] (00m:00s) 856 KB / ?? (1.84 MB/s)
    pkgs/main/linux-64       [   <=>              ] (00m:00s) 1 MB / ?? (3.31 MB/s)
    pkgs/r/noarch            [<=>               ] (00m:00s) 856 KB / ?? (1.84 MB/s)
    pkgs/main/linux-64       [   <=>              ] (00m:00s) 2 MB / ?? (3.68 MB/s)
    pkgs/r/noarch            [<=>               ] (00m:00s) 856 KB / ?? (1.84 MB/s)
    pkgs/main/linux-64       [   <=>              ] (00m:00s) 2 MB / ?? (3.68 MB/s)
    pkgs/r/noarch            [ <=>              ] (00m:00s) 856 KB / ?? (1.84 MB/s)
    pkgs/main/linux-64       [   <=>              ] (00m:00s) 2 MB / ?? (3.68 MB/s)
    pkgs/r/noarch            [  <=>               ] (00m:00s) 1 MB / ?? (2.01 MB/s)
    pkgs/main/linux-64       [   <=>              ] (00m:00s) 2 MB / ?? (3.68 MB/s)
    pkgs/r/noarch            [  <=>               ] (00m:00s) Finalizing...
    pkgs/main/linux-64       [   <=>              ] (00m:00s) 2 MB / ?? (3.68 MB/s)
    pkgs/r/noarch            [  <=>               ] (00m:00s) Done
    pkgs/r/noarch            [====================] (00m:00s) Done
    pkgs/main/linux-64       [   <=>              ] (00m:00s) 2 MB / ?? (3.68 MB/s)
    pkgs/main/linux-64       [    <=>             ] (00m:00s) 2 MB / ?? (3.68 MB/s)
    pkgs/main/linux-64       [    <=>             ] (00m:00s) 3 MB / ?? (3.78 MB/s)
    pkgs/main/linux-64       [     <=>            ] (00m:00s) 3 MB / ?? (3.78 MB/s)
    pkgs/main/linux-64       [     <=>            ] (00m:00s) 4 MB / ?? (3.92 MB/s)
    pkgs/main/linux-64       [      <=>           ] (00m:00s) 4 MB / ?? (3.92 MB/s)
    pkgs/main/linux-64       [      <=>           ] (00m:00s) 4 MB / ?? (4.05 MB/s)
    pkgs/main/linux-64       [      <=>           ] (00m:01s) Finalizing...
    pkgs/main/linux-64       [      <=>           ] (00m:01s) Done
    pkgs/main/linux-64       [====================] (00m:01s) Done
    
    Pinned packages:
      - python 3.7.*
    
    
    Transaction
    
      Prefix: /home/jupyterlab/conda/envs/python
    
      Updating specs:
    
       - bs4==4.10.0
       - ca-certificates
       - certifi
       - openssl
    
    
      Package               Version  Build           Channel                  Size
    ────────────────────────────────────────────────────────────────────────────────
      Install:
    ────────────────────────────────────────────────────────────────────────────────
    
    [32m  + bs4            [00m      4.10.0  hd3eb1b0_0      pkgs/main/noarch        10 KB
    
      Change:
    ────────────────────────────────────────────────────────────────────────────────
    
    [31m  - certifi        [00m   2022.9.24  pyhd8ed1ab_0    installed                    
    [32m  + certifi        [00m   2022.9.24  py37h06a4308_0  pkgs/main/linux-64     154 KB
    [31m  - openssl        [00m      1.1.1s  h166bdaf_0      installed                    
    [32m  + openssl        [00m      1.1.1s  h7f8727e_0      pkgs/main/linux-64       4 MB
    
      Upgrade:
    ────────────────────────────────────────────────────────────────────────────────
    
    [31m  - ca-certificates[00m   2022.9.24  ha878542_0      installed                    
    [32m  + ca-certificates[00m  2022.10.11  h06a4308_0      pkgs/main/linux-64     124 KB
    
      Downgrade:
    ────────────────────────────────────────────────────────────────────────────────
    
    [31m  - beautifulsoup4 [00m      4.11.1  pyha770c72_0    installed                    
    [32m  + beautifulsoup4 [00m      4.10.0  pyh06a4308_0    pkgs/main/noarch        85 KB
    
      Summary:
    
      Install: 1 packages
      Change: 2 packages
      Upgrade: 1 packages
      Downgrade: 1 packages
    
      Total download: 4 MB
    
    ────────────────────────────────────────────────────────────────────────────────
    
    Downloading  [>                                        ] (00m:00s)  556.09 KB/s
    Extracting   [>                                                      ] (--:--) 
    [2A[0KFinished beautifulsoup4                       (00m:00s)              85 KB    555 KB/s
    Downloading  [>                                        ] (00m:00s)  556.09 KB/s
    Extracting   [>                                                      ] (--:--) 
    Downloading  [>                                        ] (00m:00s)  556.09 KB/s
    Extracting   [>                                                      ] (--:--) 
    Downloading  [>                                        ] (00m:00s)  556.09 KB/s
    Extracting   [>                                                      ] (--:--) 
    Downloading  [=====>                                   ] (00m:00s)    3.55 MB/s
    Extracting   [>                                                      ] (--:--) 
    Downloading  [=====>                                   ] (00m:00s)    3.55 MB/s
    Extracting   [>                                                      ] (--:--) 
    Downloading  [=====>                                   ] (00m:00s)    3.55 MB/s
    Extracting   [>                                                      ] (--:--) 
    [2A[0KFinished bs4                                  (00m:00s)              10 KB     65 KB/s
    Downloading  [=====>                                   ] (00m:00s)    3.55 MB/s
    Extracting   [>                                                      ] (--:--) 
    Downloading  [=====>                                   ] (00m:00s)    3.55 MB/s
    Extracting   [>                                                      ] (--:--) 
    Downloading  [======>                                  ] (00m:00s)    4.18 MB/s
    Extracting   [>                                                      ] (--:--) 
    Downloading  [========>                                ] (00m:00s)    5.04 MB/s
    Extracting   [>                                                      ] (--:--) 
    [2A[0KFinished ca-certificates                      (00m:00s)             124 KB    782 KB/s
    Downloading  [========>                                ] (00m:00s)    5.04 MB/s
    Extracting   [========>                                ] (00m:00s)        1 / 5
    Downloading  [========>                                ] (00m:00s)    5.04 MB/s
    Extracting   [========>                                ] (00m:00s)        1 / 5
    Downloading  [========>                                ] (00m:00s)    5.04 MB/s
    Extracting   [========>                                ] (00m:00s)        1 / 5
    Downloading  [========>                                ] (00m:00s)    5.04 MB/s
    Extracting   [========>                                ] (00m:00s)        1 / 5
    [2A[0KFinished certifi                              (00m:00s)             154 KB    954 KB/s
    Downloading  [========>                                ] (00m:00s)    5.04 MB/s
    Extracting   [========>                                ] (00m:00s)        1 / 5
    Downloading  [========>                                ] (00m:00s)    5.04 MB/s
    Extracting   [========>                                ] (00m:00s)        1 / 5
    Downloading  [=========================================] (00m:00s)   21.50 MB/s
    Extracting   [========>                                ] (00m:00s)        1 / 5
    Downloading  [=========================================] (00m:00s)   21.50 MB/s
    Extracting   [================>                        ] (00m:00s)        2 / 5
    Downloading  [=========================================] (00m:00s)   21.50 MB/s
    Extracting   [================>                        ] (00m:00s)        2 / 5
    Downloading  [=========================================] (00m:00s)   21.50 MB/s
    Extracting   [========================>                ] (00m:00s)        3 / 5
    Downloading  [=========================================] (00m:00s)   21.50 MB/s
    Extracting   [========================>                ] (00m:00s)        3 / 5
    [2A[0KFinished openssl                              (00m:00s)               4 MB     21 MB/s
    Downloading  [=========================================] (00m:00s)   21.50 MB/s
    Extracting   [========================>                ] (00m:00s)        3 / 5
    Downloading  [=========================================] (00m:00s)   21.50 MB/s
    Extracting   [========================>                ] (00m:00s)        3 / 5
    Downloading  [=========================================] (00m:00s)   21.50 MB/s
    Extracting   [================================>        ] (00m:00s)        4 / 5
    Downloading  [=========================================] (00m:00s)   21.50 MB/s
    Extracting   [================================>        ] (00m:00s)        4 / 5
    Downloading  [=========================================] (00m:00s)   21.50 MB/s
    Extracting   [=========================================] (00m:00s)        5 / 5
    Preparing transaction: done
    Verifying transaction: done
    Executing transaction: done
    Collecting bs4
      Downloading bs4-0.0.1.tar.gz (1.1 kB)
      Preparing metadata (setup.py) ... [?25ldone
    [?25hRequirement already satisfied: beautifulsoup4 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from bs4) (4.10.0)
    Requirement already satisfied: soupsieve>1.2 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from beautifulsoup4->bs4) (2.3.2.post1)
    Building wheels for collected packages: bs4
      Building wheel for bs4 (setup.py) ... [?25ldone
    [?25h  Created wheel for bs4: filename=bs4-0.0.1-py3-none-any.whl size=1256 sha256=57c780d5ea2546918d4202f4f0b187bf3b1fea0cb367ca80876dbbd854583dac
      Stored in directory: /home/jupyterlab/.cache/pip/wheels/77/8a/04/7b1a8ce5de6555a18e09370d3d4fde48be9571ac07a623071e
    Successfully built bs4
    Installing collected packages: bs4
    Successfully installed bs4-0.0.1



```python
import yfinance as yf
import pandas as pd
import requests
from bs4 import BeautifulSoup
import plotly.graph_objects as go
from plotly.subplots import make_subplots
```

## Define Graphing Function


In this section, we define the function `make_graph`. You don't have to know how the function works, you should only care about the inputs. It takes a dataframe with stock data (dataframe must contain Date and Close columns), a dataframe with revenue data (dataframe must contain Date and Revenue columns), and the name of the stock.



```python
def make_graph(stock_data, revenue_data, stock):
    fig = make_subplots(rows=2, cols=1, shared_xaxes=True, subplot_titles=("Historical Share Price", "Historical Revenue"), vertical_spacing = .3)
    stock_data_specific = stock_data[stock_data.Date <= '2021--06-14']
    revenue_data_specific = revenue_data[revenue_data.Date <= '2021-04-30']
    fig.add_trace(go.Scatter(x=pd.to_datetime(stock_data_specific.Date, infer_datetime_format=True), y=stock_data_specific.Close.astype("float"), name="Share Price"), row=1, col=1)
    fig.add_trace(go.Scatter(x=pd.to_datetime(revenue_data_specific.Date, infer_datetime_format=True), y=revenue_data_specific.Revenue.astype("float"), name="Revenue"), row=2, col=1)
    fig.update_xaxes(title_text="Date", row=1, col=1)
    fig.update_xaxes(title_text="Date", row=2, col=1)
    fig.update_yaxes(title_text="Price ($US)", row=1, col=1)
    fig.update_yaxes(title_text="Revenue ($US Millions)", row=2, col=1)
    fig.update_layout(showlegend=False,
    height=900,
    title=stock,
    xaxis_rangeslider_visible=True)
    fig.show()
```

## Question 1: Use yfinance to Extract Stock Data


Using the `Ticker` function enter the ticker symbol of the stock we want to extract data on to create a ticker object. The stock is Tesla and its ticker symbol is `TSLA`.



```python
Tesla = yf.Ticker("TSLA")
```

Using the ticker object and the function `history` extract stock information and save it in a dataframe named `tesla_data`. Set the `period` parameter to `max` so we get information for the maximum amount of time.



```python
tesla_data = Tesla.history(period="max")
```

**Reset the index** using the `reset_index(inplace=True)` function on the tesla_data DataFrame and display the first five rows of the `tesla_data` dataframe using the `head` function. Take a screenshot of the results and code from the beginning of Question 1 to the results below.



```python
tesla_data.reset_index(inplace=True)
tesla_data.head()
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
      <th>Date</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Dividends</th>
      <th>Stock Splits</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010-06-29</td>
      <td>1.266667</td>
      <td>1.666667</td>
      <td>1.169333</td>
      <td>1.592667</td>
      <td>281494500</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2010-06-30</td>
      <td>1.719333</td>
      <td>2.028000</td>
      <td>1.553333</td>
      <td>1.588667</td>
      <td>257806500</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2010-07-01</td>
      <td>1.666667</td>
      <td>1.728000</td>
      <td>1.351333</td>
      <td>1.464000</td>
      <td>123282000</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2010-07-02</td>
      <td>1.533333</td>
      <td>1.540000</td>
      <td>1.247333</td>
      <td>1.280000</td>
      <td>77097000</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2010-07-06</td>
      <td>1.333333</td>
      <td>1.333333</td>
      <td>1.055333</td>
      <td>1.074000</td>
      <td>103003500</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>



## Question 2: Use Webscraping to Extract Tesla Revenue Data


Use the `requests` library to download the webpage [https://www.macrotrends.net/stocks/charts/TSLA/tesla/revenue](https://www.macrotrends.net/stocks/charts/TSLA/tesla/revenue?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkPY0220ENSkillsNetwork23455606-2022-01-01). Save the text of the response as a variable named `html_data`.



```python
url = "https://www.macrotrends.net/stocks/charts/TSLA/tesla/revenue"

html_data  = requests.get(url).text
```

Parse the html data using `beautiful_soup`.



```python

soup = BeautifulSoup(html_data, 'html.parser')

```

Using `BeautifulSoup` or the `read_html` function extract the table with `Tesla Quarterly Revenue` and store it into a dataframe named `tesla_revenue`. The dataframe should have columns `Date` and `Revenue`.


<details><summary>Click here if you need help locating the table</summary>

```
    
Below is the code to isolate the table, you will now need to loop through the rows and columns like in the previous lab
    
soup.find_all("tbody")[1]
    
If you want to use the read_html function the table is located at index 1


```

</details>



```python
tesla_tables = soup.find_all('table')

for index,table in enumerate(tesla_tables):
    if ("Tesla Quarterly Revenue" in str(table)):
        tesla_table_index = index

tesla_revenue = pd.DataFrame(columns=["Date", "Revenue"])

for row in tesla_tables[tesla_table_index].tbody.find_all("tr"):
    col = row.find_all("td")
    if (col !=[]):
        date = col[0].text
        revenue = col[1].text.replace("$", "").replace(",", "")
        tesla_revenue = tesla_revenue.append({"Date" : date, "Revenue" : revenue}, ignore_index=True)
```

Execute the following line to remove the comma and dollar sign from the `Revenue` column.



```python
tesla_revenue['Revenue'] = tesla_revenue['Revenue'].str.replace('[,$]',"",regex=True)
```

Execute the following lines to remove an null or empty strings in the Revenue column.

tesla_revenue.dropna(inplace=True)

tesla_revenue = tesla_revenue[tesla_revenue['Revenue'] != ""]
Display the last 5 row of the `tesla_revenue` dataframe using the `tail` function. Take a screenshot of the results.



```python
tesla_revenue.tail()
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
      <th>Date</th>
      <th>Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>49</th>
      <td>2010-06-30</td>
      <td>28</td>
    </tr>
    <tr>
      <th>50</th>
      <td>2010-03-31</td>
      <td>21</td>
    </tr>
    <tr>
      <th>51</th>
      <td>2009-12-31</td>
      <td></td>
    </tr>
    <tr>
      <th>52</th>
      <td>2009-09-30</td>
      <td>46</td>
    </tr>
    <tr>
      <th>53</th>
      <td>2009-06-30</td>
      <td>27</td>
    </tr>
  </tbody>
</table>
</div>



## Question 3: Use yfinance to Extract Stock Data


Using the `Ticker` function enter the ticker symbol of the stock we want to extract data on to create a ticker object. The stock is GameStop and its ticker symbol is `GME`.



```python

Gamestop = yf.Ticker("GME")
```

Using the ticker object and the function `history` extract stock information and save it in a dataframe named `gme_data`. Set the `period` parameter to `max` so we get information for the maximum amount of time.



```python
gme_data = Gamestop.history(period="max")
```

**Reset the index** using the `reset_index(inplace=True)` function on the gme_data DataFrame and display the first five rows of the `gme_data` dataframe using the `head` function. Take a screenshot of the results and code from the beginning of Question 3 to the results below.



```python
gme_data.reset_index(inplace=True)
gme_data.head()
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
      <th>Date</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Dividends</th>
      <th>Stock Splits</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2002-02-13</td>
      <td>1.620128</td>
      <td>1.693350</td>
      <td>1.603296</td>
      <td>1.691667</td>
      <td>76216000</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2002-02-14</td>
      <td>1.712707</td>
      <td>1.716073</td>
      <td>1.670626</td>
      <td>1.683250</td>
      <td>11021600</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2002-02-15</td>
      <td>1.683250</td>
      <td>1.687458</td>
      <td>1.658002</td>
      <td>1.674834</td>
      <td>8389600</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2002-02-19</td>
      <td>1.666418</td>
      <td>1.666418</td>
      <td>1.578047</td>
      <td>1.607504</td>
      <td>7410400</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2002-02-20</td>
      <td>1.615920</td>
      <td>1.662209</td>
      <td>1.603295</td>
      <td>1.662209</td>
      <td>6892800</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>



## Question 4: Use Webscraping to Extract GME Revenue Data


Use the `requests` library to download the webpage <https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html>. Save the text of the response as a variable named `html_data`.



```python
url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html"


html_data = requests.get(url).text
```

Parse the html data using `beautiful_soup`.



```python
soup = BeautifulSoup(html_data, 'html.parser')
```

Using `BeautifulSoup` or the `read_html` function extract the table with `GameStop Quarterly Revenue` and store it into a dataframe named `gme_revenue`. The dataframe should have columns `Date` and `Revenue`. Make sure the comma and dollar sign is removed from the `Revenue` column using a method similar to what you did in Question 2.


<details><summary>Click here if you need help locating the table</summary>

```
    
Below is the code to isolate the table, you will now need to loop through the rows and columns like in the previous lab
    
soup.find_all("tbody")[1]
    
If you want to use the read_html function the table is located at index 1


```

</details>



```python
gme_revenue = pd.DataFrame(columns=["Date", "Revenue"])
for table in soup.find_all('table'):
    if table.find('th').getText().startswith("Tesla Quarterly Revenue"):
        for row in table.find("tbody").find_all('tr'):
            col = row.find_all('td')
            date = col[0].text
            revenue = col[1].text
            gme_revenue = gme_revenue.append({"Date" : date, "Revenue" : revenue}, ignore_index= True)

        
```

Display the last five rows of the `gme_revenue` dataframe using the `tail` function. Take a screenshot of the results.



```python

gme_revenue.tail()

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
      <th>Date</th>
      <th>Revenue</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>



## Question 5: Plot Tesla Stock Graph


Use the `make_graph` function to graph the Tesla Stock Data, also provide a title for the graph. The structure to call the `make_graph` function is `make_graph(tesla_data, tesla_revenue, 'Tesla')`. Note the graph will only show data upto June 2021.



```python

```

## Question 6: Plot GameStop Stock Graph


Use the `make_graph` function to graph the GameStop Stock Data, also provide a title for the graph. The structure to call the `make_graph` function is `make_graph(gme_data, gme_revenue, 'GameStop')`. Note the graph will only show data upto June 2021.



```python

```

<h2>About the Authors:</h2> 

<a href="https://www.linkedin.com/in/joseph-s-50398b136/?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkPY0220ENSkillsNetwork23455606-2022-01-01">Joseph Santarcangelo</a> has a PhD in Electrical Engineering, his research focused on using machine learning, signal processing, and computer vision to determine how videos impact human cognition. Joseph has been working for IBM since he completed his PhD.

Azim Hirjani


## Change Log

| Date (YYYY-MM-DD) | Version | Changed By    | Change Description          |
| ----------------- | ------- | ------------- | --------------------------- |
| 2022-02-28        | 1.2     | Lakshmi Holla | Changed the URL of GameStop |
| 2020-11-10        | 1.1     | Malika Singla | Deleted the Optional part   |
| 2020-08-27        | 1.0     | Malika Singla | Added lab to GitLab         |

<hr>

## <h3 align="center"> © IBM Corporation 2020. All rights reserved. <h3/>

<p>

