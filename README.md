

## Usage

### terms Engine

```py
from terms import terms, Engine

portfolio = Engine(
    start_date = "2018-06-09", 
    portfolio = ["BABA", "PDD", "KO", "AMD","^IXIC"], 
    weights = [0.2, 0.2, 0.2, 0.2, 0.2],  # equal weighting is set by default
    benchmark = ["SPY"]  # SPY is set by default
)

terms(portfolio)
```

### Calendar Rebalancing
A portfolio can be rebalanced for either a specific time period or for specific dates using the ```rebalance``` option.

#### Rebalance for Time Period
Time periods available for rebalancing are 
 ```2y```, ```1y```, ```6mo```, ```quarterly```, ```monthly```  

```py
from terms import terms, Engine

portfolio = Engine(
    start_date = "2018-06-09", 
    portfolio = ["BABA", "PDD", "KO", "AMD","^IXIC"], 
    weights = [0.2, 0.2, 0.2, 0.2, 0.2],  # equal weighting is set by default
    benchmark = ["SPY"],  # SPY is set by default
    rebalance = "1y"
)

terms(portfolio)
```

#### Rebalance for Custom Dates
You can rebalance a portfolio by specifying a list of custom dates.  
⚠️ When using custom dates, the first date of the list must correspond with the ```start_date``` and the last element should correspond to the ```end_date``` which is **today's date** by default.

```py
from terms import terms, Engine

portfolio = Engine(
    start_date = "2018-06-09", 
    portfolio = ["BABA", "PDD", "KO", "AMD","^IXIC"], 
    weights = [0.2, 0.2, 0.2, 0.2, 0.2],  # equal weighting is set by default
    benchmark = ["SPY"],  # SPY is set by default
    rebalance = ["2018-06-09", "2019-01-01", "2020-01-01", "2021-01-01"]
)

terms(portfolio)
```

### Optimizer
The default optimizer is **equal weighting**. You can specify custom weights, if desired.

```py
from terms import terms, Engine

portfolio = Engine(
    start_date = "2018-01-01",
    portfolio = ["BABA", "PDD", "KO", "AMD","^IXIC"], 
    weights = [0.1, 0.3, 0.15, 0.25, 0.2],   # custom weights
    rebalance = "1y"  # rebalance every year
)

terms(portfolio)
```

You can also use the **built-in optimizers**. There are 4 optimizers available:  

- ```"EF"```: **Global Efficient Frontier**  [Example](https://terms.gitbook.io/terms/optimization/global-efficient-frontier)
- ```"MEANVAR"```: **Mean-Variance**  [Example](https://terms.gitbook.io/terms/optimization/mean-variance)
- ```"HRP"```: **Hierarchical Risk Parity**  [Example](https://terms.gitbook.io/terms/optimization/hierarchical-risk-parity)
- ```"MINVAR"```: **Minimum-Variance**  [Example](https://terms.gitbook.io/terms/optimization/minimum-variance)


```py
from terms import terms, Engine

portfolio = Engine(
    start_date = "2018-01-01",
    portfolio = ["BABA", "PDD", "KO", "AMD","^IXIC"],
    optimizer = "EF",
    rebalance = "1y"  # rebalance every year
)

portfolio.weights
```

> Output:

```
[0.0, 0.0, 0.0348, 0.9652, 0.0]
```  
We can see that the allocation has been optimized.

### Risk Manager
3 Risk Managers are available:

- **Max Drawdown**: ```{"Max Drawdown" : -0.3}```  [Example](https://terms.gitbook.io/terms/risk-management/max-drawdown)
- **Take Profit**: ```{"Take Profit" : 0.4}```  [Example](https://terms.gitbook.io/terms/risk-management/take-profit)
- **Stop Loss**: ```{"Stop Loss" : -0.2}```  [Example](https://terms.gitbook.io/terms/risk-management/stop-loss)

```py
from terms import terms, Engine

portfolio = Engine(
    start_date = "2018-01-01",
    portfolio= ["BABA", "PDD", "KO", "AMD","^IXIC"], 
    optimizer = "EF",
    rebalance = "1y",  # rebalance every year
    risk_manager = {"Max Drawdown" : -0.2}  # Stop the investment when the drawdown becomes superior to -20%
)

terms(portfolio)
``` 

### terms Outputs

<div align="center">

![image](https://user-images.githubusercontent.com/61618641/126879140-ea03ff17-a7c6-481a-bb3e-61c055b31267.png)
![image](https://user-images.githubusercontent.com/61618641/126879203-4390813c-a4f2-41b9-916b-e03dd8bafffb.png)
![image](https://user-images.githubusercontent.com/61618641/128025087-04afed7e-96ab-4730-9bd8-98f5491b2b5d.png)
![image](https://user-images.githubusercontent.com/61618641/126879204-01fe1eca-00b8-438e-b489-0213535dd31b.png)
![image](https://user-images.githubusercontent.com/61618641/126879210-9fd61e2b-01ab-4bfd-b679-3b1867d9302d.png)
![image](https://user-images.githubusercontent.com/61618641/126879215-e24c929a-55be-4912-8e2c-043e31ff2a95.png)
![image](https://user-images.githubusercontent.com/61618641/126879221-455b8ffa-c958-4ac9-ae98-d15b4c5f0826.png)
![image](https://user-images.githubusercontent.com/61618641/126879222-08906643-16db-441e-a099-7ac3b00bdbd7.png)
![image](https://user-images.githubusercontent.com/61618641/126879223-f1116dc3-cceb-493c-93b3-2d3810cae789.png)
![image](https://user-images.githubusercontent.com/61618641/126879225-dc879b71-2070-46ed-a8ad-e90880050be8.png)
![image](https://user-images.githubusercontent.com/61618641/126879297-cb78743a-6d43-465b-8021-d4b62a659828.png)

</div>

## Download the Tearsheet
You can use the ```get_report()``` function of terms to generate a tearsheet, and then download this as a PDF document.

```py
from terms import get_report, Engine

portfolio = Engine(
      start_date = "2018-01-01",
      portfolio = ["BABA", "PDD", "KO", "AMD","^IXIC"],
      optimizer = "EF",
      rebalance = "1y", #rebalance every year
      risk_manager = {"Stop Loss" : -0.2}
)

get_report(portfolio)
``` 

> Output:

![image](https://user-images.githubusercontent.com/61618641/126879406-3ff8eb14-e08b-4103-b46d-02597634d469.png)


## Stargazers over time

<div align="center">
	
![追星族的时间](https://starchart.cc/ssantoshp/terms.svg)
	
</div>

## Contribution and Issues
terms uses GitHub to host its source code.  *Learn more about the [Github flow](https://docs.github.com/en/get-started/quickstart/github-flow).*  

For larger changes (e.g., new feature request, large refactoring), please open an issue to discuss first.  

* If you wish to create a new Issue, then [click here to create a new issue](https://github.com/ssantoshp/terms/issues/new/choose).  

Smaller improvements (e.g., document improvements, bugfixes) can be handled by the Pull Request process of GitHub: [pull requests](https://github.com/ssantoshp/terms/pulls).  

* To contribute to the code, you will need to do the following:  

 * [Fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo#forking-a-repository) [terms](https://github.com/ssantoshp/terms) - Click the **Fork** button at the upper right corner of this page. 
 * [Clone your own fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo#cloning-your-forked-repository).  E.g., ```git clone https://github.com/ssantoshp/terms.git```  
  *If your fork is out of date, then will you need to manually sync your fork: [Synchronization method](https://help.github.com/articles/syncing-a-fork/)*
 * [Create a Pull Request](https://github.com/ssantoshp/terms/pulls) using **your fork** as the `compare head repository`. 

You contributions will be reviewed, potentially modified, and hopefully merged into terms.  

## Contributors

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

[![All Contributors](https://img.shields.io/badge/all_contributors-11-orange.svg?style=flat-square)](#contributors-)

<table>
  <tr>
    <td align="center"><a href="https://github.com/BrendanGlancy"><img src="https://avatars.githubusercontent.com/u/61941978?v=4" width="100px;" alt=""/><br /><sub><b>Brendan Glancy</b></sub></a><br /><a title="Code">💻</a> <a title="Bug report">🐛</a></td>
    <td align="center"><a href="https://github.com/rslopes"><img src="https://avatars.githubusercontent.com/u/24928343?v=4" width="100px;" alt=""/><br /><sub><b>Renan Lopes</b></sub></a><br /><a title="Code">💻</a> <a title="Bug report">🐛</a></td>
    <td align="center"><a href="https://github.com/markthebault"><img src="https://avatars.githubusercontent.com/u/3846664?v=4" width="100px;" alt=""/><br /><sub><b>Mark Thebault</b></sub></a><br /><a title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/diegodalvarez"><img src="https://avatars.githubusercontent.com/u/48641554?v=4" width="100px;" alt=""/><br /><sub><b>Diego Alvarez</b></sub></a><br /><a title="Code">💻🐛</a></td>
    <td align="center"><a href="https://github.com/rakeshbhat9"><img src="https://avatars.githubusercontent.com/u/11472305?v=4" width="100px;" alt=""/><br /><sub><b>Rakesh Bhat</b></sub></a><br /><a title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/Haizzz"><img src="https://avatars.githubusercontent.com/u/5275680?v=4" width="100px;" alt=""/><br /><sub><b>Anh Le</b></sub></a><br /><a title="Bug report">🐛</a></td>
    <td align="center"><a href="https://github.com/TonyZhangkz"><img src="https://avatars.githubusercontent.com/u/65281213?v=4" width="100px;" alt=""/><br /><sub><b>Tony Zhang</b></sub></a><br /><a title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/eltociear"><img src="https://avatars.githubusercontent.com/u/22633385?v=4" width="100px;" alt=""/><br /><sub><b>Ikko Ashimine</b></sub></a><br /><a title="Code">✒️</a></td>
    <td align="center"><a href="https://www.youtube.com/watch?v=-4qx3tbtTgs"><img src="https://avatars.githubusercontent.com/u/50767660?v=4" width="100px;" alt=""/><br /><sub><b>QuantNomad</b></sub></a><br /><a title="Code">📹</a></td>
    <td align="center"><a href="https://github.com/buckleyc"><img src="https://avatars.githubusercontent.com/u/4175900?v=4" width="100px;" alt=""/><br /><sub><b>Buckley</b></sub></a><br /><a title="Code">✒️💻</a></td>
    <td align="center"><a href="https://github.com/agn35"><img src="https://lh3.googleusercontent.com/a-/AOh14GhXGFHHpVQTL2r23oEXFssH0f7RyoGDihrS_HmT=s48" width="100px;" alt=""/><br /><sub><b>Adam Nelsson</b></sub></a><br /><a title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/rgleavenworth"><img src="https://avatars.githubusercontent.com/u/87843950?v=4" width="100px;" alt=""/><br /><sub><b>Ranjan Grover</b></sub></a><br /><a title="Code">🐛💻</a></td>
  </tr>
</table>

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. **Contributions of any kind are welcome!**

## Credit

This library has also been made possible because of the work of these incredible people:
- [**Ran Aroussi**](https://github.com/ranaroussi) for the [**Quantstats library**](https://github.com/ranaroussi/quantstats) 
- [**Robert Martin**](https://github.com/robertmartin8) for the [**PyPortfolioOpt**](https://github.com/robertmartin8/PyPortfolioOpt) 

## Contact

You are welcome to contact us by email at **santoshpassoubady@gmail.com** or in terms's [discussion space](https://github.com/ssantoshp/terms/discussions)

## License

MIT
