# Операторно-параметрические схемы модели ремонта "Прибор-Мастер"

## Схема блока ПРИБОР

```mermaid
%%{init: {'theme': 'base', 'themeVariables': {
  'primaryColor': '#ffcc00',
  'primaryTextColor': '#000',
  'primaryBorderColor': '#7C0000',
  'lineColor': '#F8B229',
  'secondaryColor': '#006100',
  'tertiaryColor': '#fff'
}}}%%
flowchart LR
    title[<em>Блок ПРИБОР</em>]
    
    h1(["ВРЕМЯ=ТСЛОМ"]) ==> h2["сост:=<br>сломан"]
    h2 ==> h3(["режим:=<br>работа"])
    h3 ==> h5["мастер:=занят<br>Трем:=func(x)"]
    h5 ==> h6(["ВРЕМЯ=Трем"])
    h6 ==> h7["сост:=рабочий<br>мастер:=своб<br>Тслом:=func(x)"]
    h7 ==> h1
    
    h2 -.- par3((сост))
    h7 -.- par3
    par1((режим)) -.- h3
    par2((мастер)) -.- h5
    h7 -.- par2
    h5 -.- par4((Трем))
    par4 -.- h6
    Ini@{shape: braces, label: "I::"} -.- h1
    HTf@{shape: braces, label: "I::Tclom = 100"}
    
    h2 e11@==> h3
    h5 e20@==> h6
    h7 e10@==> h1
    e10@{ curve: linear}
    e11@{ curve: natural}
    e20@{ curve: stepAfter}
    
    classDef cond fill:#bee,stroke:#aaa,stroke-width:1px;
    classDef state fill:#9e8,stroke:#333,stroke-width:1px;
    class h5,h2,h7 state;
    class h1,h3,h6 cond;
    style title fill:yellow,stroke:red;
    style par1 fill:#fcc,stroke:#111,stroke-width:2px;
    style par2 fill:#fae,stroke:#bbb,stroke-width:2px;
    style par4 fill:#ccc,stroke:#555,stroke-width:2px;
    
    click par2 href "https://iu5.bmstu.ru" "переход для Мастера" _blank;
    click par4 href "https://mermaid.js.org" "информация о параметре Трем" _blank;



