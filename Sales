# Import libraries
import pandas as pd
import plotly.express as px

# Load data
df = pd.read_csv('/content/Sales Data - New - sales_data_sample.csv')
df

# Cek Data
df.isnull().sum()
df.info()

# Keep status = shipped, resolved
print(df['STATUS'].unique())

values_to_drop = ['Cancelled', 'On Hold', 'Disputed', 'In Process']
df = df[~df['STATUS'].isin(values_to_drop)]

# Product line with highest and lowest
agg_product_line = df.groupby('PRODUCTLINE')['QUANTITYORDERED'].sum().reset_index()
agg_product_line

fig = px.bar(
    agg_product_line,
    x='PRODUCTLINE',
    y='QUANTITYORDERED',
    color_discrete_sequence=['darkblue']      
)

fig.update_traces(
    width=0.5,
    texttemplate='%{y:,.0f}',
    textposition='outside',
)

fig.update_layout(
    width=1000,
    height=800,
    xaxis={'categoryorder': 'total descending'},
    xaxis_title='',
    yaxis={'visible': False},
    title_text='PRODUCT LINE',
    title_x=0.5,
    font=dict(
        family='Arial',
        size=16,
        color='black'
    ),
    title_font=dict(
        family='Arial',
        size=26,
        color='black',
        weight='bold'
    ),
    paper_bgcolor='white',
    plot_bgcolor='white'
)

fig.show()


# Sales performance
# QUANTITY groupby ORDERDATE
df['ORDERDATE'] = pd.to_datetime(df['ORDERDATE'])
df['MONTH'] = df['ORDERDATE'].dt.strftime('%Y %m')

# Variable baru bulanan
agg_sales = df.groupby('MONTH')['QUANTITYORDERED'].sum().reset_index()
agg_sales

fig = px.line(
    agg_sales,
    x='MONTH',
    y='QUANTITYORDERED',
    color_discrete_sequence=['darkblue']     
)

fig.update_layout(
    xaxis_title='',
    yaxis_title='Quantity',
    title_text='SALES PERFORMANCE',
    title_x=0.5,
    font=dict(
        family='Arial',
        size=14,
        color='black'
    ),
    title_font=dict(
        family='Arial',
        size=26,
        color='black',
        weight='bold'
    ),
    paper_bgcolor='white',
    plot_bgcolor='white'
)

fig.show()

# Contribution deal size with total total sales?
agg_dealsize = df.groupby('DEALSIZE')['QUANTITYORDERED'].sum().reset_index()
agg_dealsize

fig = px.pie(
    agg_dealsize, 
    values='QUANTITYORDERED', 
    names='DEALSIZE', 
    color_discrete_sequence=px.colors.sequential.Cividis
)
fig.update_layout(
    width=1100,
    height=700,
    title_text='TOTAL SALES BY DEAL SIZE',
    title_x=0.5,
    font=dict(
        family='Arial',
        size=20,
        color='black'
    ),
    title_font=dict(
        family='Arial',
        size=26,
        color='black',
        weight='bold'
    ),
    legend=dict(
        orientation='v',
        yanchor='middle',
        y=0.5,
        xanchor='center',
        x=+0.9
    )
)
fig.show()
