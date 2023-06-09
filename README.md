The purpose of this repo is just for myself to documenting a few common templates that I use for reference. Feel free to use/copy any of it if you find it useful. 

# General
- Types of diagram
    - `flowchart`
    - `classDiagram` [UML]: focus more on what each class can do. Typically used to show the structure of program.
    - `erDiagram`: focus more on relationship between concepts, less on what each concept can do. Typically used to show the structure of database
    - `sequenceDiagram` [UML]: for multiple participants interaction sequence such as Client and Server

- Shared syntax
    - `%%`: comments

# Mermaid flowchart template
### For decision flow
- Nodes
    - `[]`: facts?
    - `()`: action point
    - `{}`: decision point
- Relationships
    - `-->`: directed arrow
    - `||`: annotation on link

```mermaid

flowchart LR
    s[Start] --> email(Enter your email)
    email --> user{Existing User?}
    user -->|no| name(Enter name)
    user -->|yes| link(Send email with magic link)
    name --> condition{Except condition?}
    condition --> |no| email
    condition --> |yes| link
    link --> e[End]
 ```
### For data flow
```mermaid
flowchart LR
    %% source
    table2[(project3.dataset2.table2)]
    table3[(project2.dataset3.table3)]

    %% output
    table1(project1.dataset1.table1)
    view1{{project1.dataset1.view1}}
    table4(project1.dataset1.table4)
    
    subgraph Recent Redeem Value
    direction LR
    table2 --> table1
    end

    subgraph Redeem Value
    table3 --> view1
    end

    subgraph Final Table
    table1 --> table4
    view1 --> table4
    end

    subgraph Legend
    s[(source table/view)]
    t(table)
    v{{view}}
    end
```
# Class diagram template
- Attribute symbol
    - `<<>>`: notation usually used to declare <<abstract>>
    - `+`: public
    - `#`: protected
    - `-`: private
- Relationships
    - `-->`: directed association
    - `--`: association
    - `--|>`: inheritance
    - `o--`: aggregation
    - `*--`: Composition


```mermaid
classDiagram
    class Champion{
        <<abstract>>
        +Int HP
        +Int Mana/Energy
        +q()
        +w()
        +e()
        +r()
    }
    class Summonor{
        + d()
        + f()
    }
    class Yasuo{
        +q()
        +w()
        +e()
        +r()
    }
    class Fizz{
        +q()
        +w()
        +e()
        +r()
    }
    class Match{
        +List Champions
    }
    %% enumeration
    class Status{
        <<enumeration>>
        DEAD
        ALIVE
    }
    Champion <|-- Yasuo : inherit
    Champion <|-- Fizz : inherit
    Match *--o Champion %% campaign cannot spawn without a match game but a match can be created without having any campaign

```


# erDiagram
- Relationships
    - `|o`, `o|`: zero or 1
    - `||`, `||`: exactly one
    - `}o`, `o{`: zero or more
    - `}|`, `|{`: one or more

```mermaid
erDiagram
    %% one customer can place 0 or more orders
    Customer ||--o{ Order : places
    %% one order contains 1 or more lineitems
    Order ||--|{ LineItem : contains 

    Customer {
        String id
        String name
    }
```

# Reference/useful links
- [Arjancode - Mermaid JS: Finally There's A Great UML & Diagram Drawing Tool](https://www.youtube.com/watch?v=JiQmpA474BY)
- [Mermaid official doc](https://mermaid.js.org/intro/)
- [Mermaid live editor](https://mermaid.live/)
