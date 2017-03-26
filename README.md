# OO LESS
Create your own Object Oriented LESS Classes with Media Querie Support

### Version
1.0.0

### Requires

* [LESS]

## Example
#### 1. Define your desired classes
```sh
    .@{prefix}tac    { text-align: center       }
    .@{prefix}tal    { text-align: left         }
    .@{prefix}tar    { text-align: right        }

    .@{prefix}m0     { margin: 0px              }
    .@{prefix}m5     { margin: 5px              }
    .@{prefix}m10    { margin: 10px             }

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

    // only tablet
    @media (min-width: 650px) and (max-width: 990px) {
        @prefix: tablet-;
        @import (multiple) "object_oriented.less";
    }

    // only desktop
    @media (min-width: 990px) {
        @prefix: desktop-;
        @import (multiple) "object_oriented.less";
    }
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
    }
```