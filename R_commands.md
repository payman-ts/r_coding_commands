*1- Raw String Literals::* 

```r 
>path <- r"(C:\Users\Administrator\Downloads)"
```
- Use **r\"()\"** to write strings without escaping backslashes.

- Ideal for Windows file paths.
  
---
  
*2- Grouped Data as List-Columns*
- dplyr:: **group_nest()**
- data.table:: dt[, **.(data = list(.SD))**, by = ...]
```r
> iris |> dplyr::group_nest(Species)
# A tibble: 3 × 2
  Species                  data
  <fct>      <list<tibble[,4]>>
1 setosa               [50 × 4]
2 versicolor           [50 × 4]
3 virginica            [50 × 4]


>iris |>
  as.data.table() |>
  (\(dt) dt[, .(data = list(.SD)), by = Species])()
      Species               data
       <fctr>             <list>
1:     setosa <data.table[50x4]>
2: versicolor <data.table[50x4]>
3:  virginica <data.table[50x4]>

```
