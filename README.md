# stater
The state setting Sass mixin

#### Required Sass version: 3.4+

### Usage
###### Input
```scss
.parent-sel {
  color: CornflowerBlue;
  
  // Set one or more states on parent-sel directly
  @include stater(("hover", "active")) {
    color: Tomato;
  }
  
  // Set one or more states on parent-sel if body contains state
  @include stater("modal-is-active", "body") {
    color: MediumAquaMarine;
  }
  
  .child-sel {
    color: LightSkyBlue;
    
    // Set one or more states with arguments on child-sel if it is nested in
    // the nth-child parent-sel
    @include stater("nth-child(2)", ".parent-sel") {
      color: Khaki;
    }
    
    // Sets a state on both parent-sel and grandparent-el
    @include stater("is-disabled", (".parent-sel", ".grandparent-el")) {
      color: BlanchedAlmond;
    }
    
    &::before {
      color: SandyBrown;
      
      // 
      @include stater("is-active", ".parent-sel") {
        color: MistyRose;
      }
    }
  }
}
```

###### Output
```css
.parent-sel {
  color: CornflowerBlue;
}
.parent-sel:hover, .parent-sel:active {
  color: Tomato;
}
body.modal-is-active .parent-sel {
  color: MediumAquaMarine;
}
.parent-sel .child-sel {
  color: LightSkyBlue;
}
.parent-sel:nth-child(2) .child-sel {
  color: Khaki;
}
.parent-sel.is-disabled .child-sel, .grandparent-el.is-disabled .parent-sel .child-sel {
  color: BlanchedAlmond;
}
.parent-sel .child-sel::before {
  color: SandyBrown;
}
.parent-sel.is-active .child-sel::before {
  color: MistyRose;
}
```
