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


## Схема блока МАСТЕР

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
    title_m[<em>Блок МАСТЕР</em>]
    
    h10(["ВРЕМЯ=Тцикл"]) ==> h11["мастер:=своб"]
    h11 ==> h12{"заявка<br>есть?"}
    h12 ==>|"да"| h13["мастер:=занят"]
    h13 ==> h14(["ВРЕМЯ=Траб"])
    h14 ==> h15{"мастер<br>=>..."}
    h15 ==>|"...= занят"| h16["Трем:=Трем:+<br>Траб-ВРЕМЯ"]
    h15 ==>|"...= свобод"| h11
    h16 ==> h10
    h12 ==>|"нет"| h10
    
    h11 -.- par_m1((сост_мастера))
    h13 -.- par_m1
    h15 -.- par_m2((мастер))
    
    classDef navig fill:#eda,stroke:#333,stroke-width:1px;
    classDef cond fill:#bee,stroke:#aaa,stroke-width:1px;
    classDef state fill:#9e8,stroke:#333,stroke-width:1px;
    class h11,h13,h16 state;
    class h10,h14 cond;
    class h12,h15 navig;
    style title_m fill:yellow,stroke:red;

