# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_270517.jpg
## adasind_271039.jpg
- L1+R7 mid WRONG_CLASS
- L5+R5 center BOX_GEOMETRY
- L7+R8 center DUPLICATE
- L8 center SPURIOUS
- R4 edge MISSING
- R6 mid MISSING
- R9 edge MISSING
- R10 center MISSING
## adasind_295948.jpg
- L1 mid IGNORE_SCOPE
- L4 center IGNORE_SCOPE
- L3+R1 center WRONG_CLASS
- L5+R3 mid WRONG_CLASS

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 12 | 9 | 3 | 4 |
| mid | 5 | 2 | 3 | 2 |
| edge | 3 | 1 | 2 | 0 |
