# backtest
Calculate historical performance of portfolios

```import pandas as pd
import datetime as dt
import backtest as bt
import matplotlib
matplotlib.style.use('ggplot')
%pylab inline

for date in bt.get_datelist(dt.date(2014,12,1),dt.date.today(),months=[1,2,3,4,5,6,7,8,9,10,11,12]):
    df_comp = pd.DataFrame({'Symbol':['FRESX','SPY','LUTAX'],'Weight':[0.3,0.4,0.3]})
    df_comp.to_csv('backtest/test/FUNDS_'+dt.date.strftime(date,'%Y%m%d')+'.csv',sep=',',index=False)
    
df = bt.calculate('backtest/test','FUNDS')

bm = bt.externaldata.yahoo.get_timeseries_gross_return('SPY',dt.date(2014,11,1),dt.date.today())

df = df.join(bm)
df = df / df.iloc[0] * 100

df.plot()```