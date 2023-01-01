# Global temperature anomalies compared to baseline, 1880 to 2020


[This is the link to the finished project](https://karanxhagiulia.github.io/Global_Temperatures/)

  
  ![github](https://user-images.githubusercontent.com/96819403/210184386-8a93d7ac-54ab-4003-98c2-ce25a29c26f6.png)


Data provided by NASA.

  

_Tools: Python, Plotly. Learning viz with Plotly!_
  
### Cleaning the data


I know I have some nulls, I can just remove them this time.

  

![](https://t9008005499.p.clickup-attachments.com/t9008005499/aadb3291-1faf-4cf6-8a40-a706fcba0a0e/image.png)

I only want the "Global" data, so I will use a condition to filter the data I want:

```python
df = df[df['Hemisphere']=='Global'] #condition
```

I will create the yearly mean:

  

```python
df['Yearly Mean'] = df[['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul',        'Aug', 'Sep', 'Oct', 'Nov', 'Dec']].mean(axis=1) #creating a new column with the yearly mean
```

and round it for the visualization.

```python
df1['Yearly Average above/below baseline °C']= df1['Yearly Mean'].round(decimals=3) 
```

  

### Visualization

  

Creating the visualization with Plotly:

  

```python
import plotly.express as px
fig = px.bar_polar(df1, r='Yearly Average above/below baseline °C', template="plotly_dark",color='Yearly Average above/below baseline °C',hover_name='Year',
                   color_discrete_sequence= px.colors.sequential.Plasma_r,start_angle = 90, log_r = False,title ='Global temperature anomalies compared to baseline, from 1880 to 2020',width=1620, height=800)
fig.show()
```

  

```python
fig.update_layout(
    polar = dict(
      angularaxis = dict(
            tickvals=[7, 45, 90, 135, 180, 225, 270, 315, 356],
            ticktext=["1880", "1898", "1915", "1933", "1951", "1969", "1986", "2003","2020"],
            showgrid=False, showline=False, showticklabels=True, layer='below traces',
            color="antiquewhite",ticks=""
            ),
    radialaxis = dict(showgrid=True, showline=True,showticklabels=True, linecolor="#3c3b54",gridcolor="#3c3b54",color='antiquewhite',side='clockwise',tickangle=0,type='-',ticks="outside")
    ))
```
