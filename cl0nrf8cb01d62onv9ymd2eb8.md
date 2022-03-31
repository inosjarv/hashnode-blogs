## Python in Day To Day Life

#### Problem Statement

I was assigned a task to compare two tables schemas and add missing columns from new table schema to old table. So as a normal developer I automated that task using **Python**'s **Pandas** library.

#### Sample Schema of Two Tables
| Old Columns | New Columns |
| :----               |    :-----------: |
| Columns 1     | Column 1         |
| Columns 2     | Column 2         |
| Columns 3     | Column 5         |
| Columns 6     | Column 7         |

So on and so forth ....

#### Code To Compare Two Columns

``` python
import pandas as pd

def compare_columns(fileName):
    dataframe = pd.read_csv(fileName)
    
    # .dropna() will remove missing data in columns if any
    oldColumns = dataframe["Old Columns"].dropna().tolist()
    newColumns  =dataframe["New Columns"].dropna().tolist()
   
    # difference of set will provide new columns
    differentColumns = list(set(newColumns) - set(oldColumns))
    return differentColumns

def query_builder(columns):
    # \r \t \n will do magic of indentation in query string 
    query = "ALTER TABLE TABLE_NAME ADD \r\n"
    
    for column in columns:
        query += "\r\t{0} nvarchar(200), \r\n".format(column)
    
    return query
``` 

Output for the above code will be:

```sql
ALTER TABLE TABLE_NAME ADD
    MISSING_COLUMN1 nvarchar(200),
    MISSING_COLUMN2 nvarchar(200),
    MISSING_COLUMN3 nvarchar(200),
    MISSING_COLUMN4 nvarchar(200),
    ....
``` 
**Note**: Mind you, above solution is not perfect since I have considered all columns' datatype nvarchar only.

#### Bonus Meme:

![20220217_215747.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1647083315114/IDLZCzHqo.jpg)

