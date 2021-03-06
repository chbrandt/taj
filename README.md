Tables As JSON
-------

TAJ is a specification for *Pandas DataFrames* as a JSON structure including
not only the data and table's metadata but also visual parameters to visualize
it in a uniform way.

The JSON structure is composed by four sections:
* columns : name of the columns
* index : table index values
* data : list of values disposed rowwise
* meta : metadata section for general visual aspects

```
{
    "columns": [
        <If 'columns:type' is "Simple", this is a simple list of column names>
        <If 'columns:type' is "MultiIndex", this a list of lists with column names>
    ],
    "index": [
        <If 'index:type' is "Simple", this is a simple list of index values>
        <If 'index:type' is "MultiIndex", this a list of lists with index values>
    ],
    "data": [
        <List of lists of values, that are represented row-wise; i.e, each list of values is a row from the dataframe>
    ],
    "meta": {
        "tableType": < "Simple" or "MultiIndex" > ,
        "colors": {
            "bg": <String: #RGB value> ,
            "fg": <String: #RGB value>
        },
        "filterFields": <List of strings: column names flagged to be filtered>,
        "index": {
            "type": <"Simple" or "MultiIndex"> ,
            "name": <String, List of strings (if MultiIndex) or 'null'>
        },
        "columns": {
            "type": <"Simple" or "MultiIndex"> ,
            "name": <String, List of strings (if MultiIndex) or 'null'>,
            "bins": {
                <String: a column name set to be coloured after bins/intervals>: {
                    "edges": <List of values for the interval limits>,
                    "colors": {
                        "bg": <List of #RGB values>,
                        "fg": <List of #RGB values>
                    }
                }
            }
        },
    }
}
```


## Example of tables

### Nested Rows & Columns
#### *With* columns/cell colouring *and* "filter-fields"
```json
{
  "columns": [
    [
      "sepal_length",
      "min"
    ],
    [
      "sepal_length",
      "max"
    ],
    [
      "sepal_width",
      "min"
    ],
    [
      "sepal_width",
      "max"
    ],
    [
      "petal_length",
      "min"
    ],
    [
      "petal_length",
      "max"
    ],
    [
      "petal_width",
      "min"
    ],
    [
      "petal_width",
      "max"
    ]
  ],
  "index": [
    [
      "setosa",
      "north"
    ],
    [
      "versicolor",
      "north"
    ],
    [
      "virginica",
      "north"
    ]
  ],
  "data": [
    [
      4.4,
      5.7,
      2.9,
      4.4,
      1.3,
      1.6,
      0.2,
      0.6
    ],
    [
      5.5,
      5.7,
      2.4,
      2.8,
      3.8,
      4.5,
      1.1,
      1.3
    ],
    [
      5.8,
      7.7,
      2.8,
      3.2,
      4.8,
      6.7,
      1.6,
      2.4
    ]
  ],
  "meta": {
    "tableType": "MultiIndex",
    "colors": {
      "bg": "#FFFFFF",
      "fg": "#000000"
    },
    "filterFields": [
      "sepal_length|min"
    ],
    "columns": {
      "type": "MultiIndex",
      "name": [
        null,
        null
      ],
      "bins": {
        "sepal_length|min": {
          "colors": {
            "bg": [
              "#006d2c",
              "#31a354",
              "#74c476",
              "#bae4b3",
              "#edf8e9"
            ],
            "fg": [
              "#6d0041",
              "#a33180",
              "#c474c2",
              "#ddb3e4",
              "#f4e9f8"
            ]
          },
          "edges": [
            4.398,
            4.68,
            4.96,
            5.24,
            5.52,
            5.8
          ]
        }
      }
    },
    "index": {
      "type": "MultiIndex",
      "name": [
        "species",
        "location"
      ]
    }
  }
}
```


#### **3-levels** of nested columns and usual (2-levels) nested rows
```json
{
  "columns": [
    [
      "petal_length",
      1514764800000,
      "min"
    ],
    [
      "petal_length",
      1514764800000,
      "max"
    ],
    [
      "petal_length",
      1517443200000,
      "min"
    ],
    [
      "petal_length",
      1517443200000,
      "max"
    ],
    [
      "petal_length",
      1519862400000,
      "min"
    ],
    [
      "petal_length",
      1519862400000,
      "max"
    ],
    [
      "petal_width",
      1514764800000,
      "min"
    ],
    [
      "petal_width",
      1514764800000,
      "max"
    ],
    [
      "petal_width",
      1517443200000,
      "min"
    ],
    [
      "petal_width",
      1517443200000,
      "max"
    ],
    [
      "petal_width",
      1519862400000,
      "min"
    ],
    [
      "petal_width",
      1519862400000,
      "max"
    ],
    [
      "sepal_length",
      1514764800000,
      "min"
    ],
    [
      "sepal_length",
      1514764800000,
      "max"
    ],
    [
      "sepal_length",
      1517443200000,
      "min"
    ],
    [
      "sepal_length",
      1517443200000,
      "max"
    ],
    [
      "sepal_length",
      1519862400000,
      "min"
    ],
    [
      "sepal_length",
      1519862400000,
      "max"
    ],
    [
      "sepal_width",
      1514764800000,
      "min"
    ],
    [
      "sepal_width",
      1514764800000,
      "max"
    ],
    [
      "sepal_width",
      1517443200000,
      "min"
    ],
    [
      "sepal_width",
      1517443200000,
      "max"
    ],
    [
      "sepal_width",
      1519862400000,
      "min"
    ],
    [
      "sepal_width",
      1519862400000,
      "max"
    ]
  ],
  "index": [
    [
      "setosa",
      "north"
    ],
    [
      "setosa",
      "south"
    ],
    [
      "versicolor",
      "north"
    ],
    [
      "versicolor",
      "south"
    ],
    [
      "virginica",
      "north"
    ],
    [
      "virginica",
      "south"
    ]
  ],
  "data": [
    [
      1.3,
      1.5,
      1.3,
      0.1,
      0.2,
      0.1,
      4.4,
      4.9,
      4.5,
      3.0,
      3.0,
      2.3,
      1.7,
      1.6,
      1.5,
      0.3,
      0.4,
      0.4,
      5.4,
      5.1,
      5.7,
      3.5,
      3.8,
      4.4
    ],
    [
      1.1,
      1.0,
      1.2,
      0.1,
      0.1,
      0.2,
      4.3,
      4.6,
      4.4,
      3.0,
      3.0,
      2.9,
      1.9,
      1.9,
      1.7,
      0.5,
      0.6,
      0.4,
      5.8,
      5.7,
      5.4,
      4.1,
      4.2,
      3.9
    ],
    [
      3.5,
      4.0,
      3.7,
      1.0,
      1.0,
      1.0,
      5.2,
      5.6,
      5.4,
      2.4,
      2.2,
      2.3,
      4.7,
      5.0,
      5.1,
      1.6,
      1.7,
      1.6,
      6.4,
      6.8,
      6.3,
      3.3,
      3.4,
      3.0
    ],
    [
      3.0,
      3.3,
      3.3,
      1.0,
      1.0,
      1.0,
      5.0,
      4.9,
      5.0,
      2.0,
      2.4,
      2.2,
      4.0,
      4.7,
      4.9,
      1.2,
      1.5,
      1.8,
      5.8,
      7.0,
      6.9,
      2.6,
      3.2,
      3.2
    ],
    [
      4.5,
      4.9,
      4.8,
      1.4,
      1.5,
      1.8,
      4.9,
      5.8,
      6.0,
      2.5,
      2.5,
      2.5,
      5.8,
      6.7,
      6.3,
      2.4,
      2.5,
      2.5,
      6.8,
      7.7,
      7.3,
      3.4,
      3.8,
      3.3
    ],
    [
      5.1,
      5.0,
      4.9,
      1.8,
      1.5,
      1.8,
      5.8,
      5.7,
      5.6,
      2.7,
      2.2,
      2.8,
      6.7,
      6.9,
      6.4,
      2.4,
      2.5,
      2.3,
      7.7,
      7.7,
      7.9,
      3.2,
      3.6,
      3.8
    ]
  ],
  "meta": {
    "tableType": "MultiIndex",
    "colors": {
      "bg": "#FFFFFF",
      "fg": "#000000"
    },
    "filterFields": null,
    "columns": {
      "type": "MultiIndex",
      "name": [
        "variable",
        "date",
        "stats"
      ],
      "bins": {}
    },
    "index": {
      "type": "MultiIndex",
      "name": [
        "species",
        "location"
      ]
    }
  }
}
```


CellOps
-----
Coming in the future

Specification for tabular data:

- Visual operations at cell, column, row, table levels

- Column Operations
  - Binning:

- Simple Table

- Nested Columns

- Nested Rows

- Cell Symbology: cells may be [draw](https://github.com/brendancol/react-taj) with different colors, for instance, based on their values, corresponding column or index.
  - 'style':
  - 'breaks':
  - 'palette': colors to use for drawing
  - 'colorMethod': background, text, fontsize
  - 'binMethod': Equal Interval, Natural Breaks, Quantile,
