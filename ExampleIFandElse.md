if [Valor Principal] < 50 
                then "a) Até R$ 50"
else if [Valor Principal] >= 50 
    and [Valor Principal] < 100
                then "b) R$ 50 à R$ 100"
else if [Valor Principal] >= 100 
     and [Valor Principal] < 150
                then "c) R$ 100 à R$ 150"
else if [Valor Principal] >= 150 
     and [Valor Principal] < 200
                then "d) R$ 150 à R$ 200"
else if [Valor Principal] >= 250 
     and [Valor Principal] < 300
                then "e) R$ 250 à R$ 300"
else if [Valor Principal] >= 300 
     and [Valor Principal] < 400
                then "f) R$ 300 à R$ 400"
                else "g) Acima de R$ 400"
