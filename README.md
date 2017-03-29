# OO LESS
Create your own Object Oriented LESS Grid System
- Media Querie Support
- Based on css calc
- Possible use of % or PX values
- 12, 16, 24, .... columns
- Nested rows!

### Version
1.0.0

### Requires

* [LESS]

## FINAL RESULT
```sh
  <div class="row">
    <div class="col-4 tablet-col-6 mobile-col-12">
      <h2 class="mb50 tablet-mb-20 mobile-mb-10"></h2>
      <img src="..." class="tablet-w80 mobile-w60" />
    </div>
    <div class="col-4 tablet-col-6 mobile-col-12"></div>
  </div>
```

## OO GRID
#### 1. Variables
```sh
    @gridWidth: 1280px;
    @columnCount: 12;
    @columnSpace: 20px;
    @columnWidth: 100 - @columnSpace;
```
#### 2. Define Rows and Columns
```sh
    .column(@count) {
        @thisColumnWidth: 100% / @columnCount * @count;
        @thisColumnSpace: @columnSpace / 2;
        box-sizing: border-box;
        float: left;
        margin-left: @thisColumnSpace;
        margin-right: @thisColumnSpace;
        min-height: 1px; // for empty cols
        width: calc(~"@{thisColumnWidth} - @{thisColumnSpace} * 2");
    }

    .row {
        margin-left: auto;
        margin-right: auto;
        max-width: @gridWidth;
        position: relative;
        &:after { // clearfix
            clear: both;
            content: "";
            display: table;
        }
        .row {
            margin-left: -(@columnSpace / 2);
            margin-right: -(@columnSpace / 2);
            max-width: none;
        }
    }
```
#### 3. Create Media Querie Supported Classes
```sh
    // only mobile
    .cols(@columnCount);
    .cols(@n, @i: 1) when (@i =< @n) { .col-@{i} { .column(@i) } .cols(@n, (@i + 1)) }

    // only mobile
    @media (min-width: 0) and (max-width: 650px) {
        .mobile-cols(@columnCount);
        .mobile-cols(@n, @i: 1) when (@i =< @n) { .mobile-col-@{i} { .column(@i) } .mobile-cols(@n, (@i + 1)) }
    }

    ...


```
#### 4. Voilà
```sh
    .col-1 {
      box-sizing: border-box;
      float: left;
      margin-left: 10px;
      margin-right: 10px;
      min-height: 1px;
      width: calc(8.333333333333334% - 10px * 2);
    }
    .col-2 {
      box-sizing: border-box;
      float: left;
      margin-left: 10px;
      margin-right: 10px;
      min-height: 1px;
      width: calc(16.666666666666668% - 10px * 2);
    }

    ...

    @media (min-width: 0) and (max-width: 650px) {
      .mobile-col-1 {
        box-sizing: border-box;
        float: left;
        margin-left: 10px;
        margin-right: 10px;
        min-height: 1px;
        width: calc(8.333333333333334% - 10px * 2);
      }
      .mobile-col-2 {
        box-sizing: border-box;
        float: left;
        margin-left: 10px;
        margin-right: 10px;
        min-height: 1px;
        width: calc(16.666666666666668% - 10px * 2);
      }

      ...
    }
```

## OO Classes Example
#### 1. Define your desired classes

```sh
    .@{prefix}w10    { width: 10%               }
    .@{prefix}w20    { width: 20%               }
    .@{prefix}w25    { width: 25%               }

    ...
```
#### 2. Create object oriented classes 
```sh
    // global
    @prefix: ;
    @import "object_oriented.less";

    // only mobile
    @media (min-width: 0) and (max-width: 650px) {
        @prefix: mobile-;
        @import (multiple) "object_oriented.less";
    }

    ...
```
#### 3. Voilà
```sh
    .w10 {
      width: 10%;
    }
    .w20 {
      width: 20%;
    }
    .w25 {
      width: 25%;
    }

    ...

    @media (min-width: 0) and (max-width: 650px) {
      .mobile-w10 {
        width: 10%;
      }
      .mobile-w20 {
        width: 20%;
      }
      .mobile-w25 {
        width: 25%;
      }

      ...
    }
```