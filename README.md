[![Build Status](https://travis-ci.org/drcmda/react-spring-numerical.svg?branch=master)](https://travis-ci.org/drcmda/react-spring-numerical) [![npm version](https://badge.fury.io/js/react-spring-numerical.svg)](https://badge.fury.io/js/react-spring-numerical)

# Installation 🖥

    npm install react-spring-numerical

# What is it? 🤔

A barebones 3-4kb implementation of [react-spring](https://github.com/drcmda/react-spring). It contains the spring mathematics, the Spring primitive, and support for raw, numerical values or arrays. It will not understand colors, paths, strings, units, etc. Use this for applications that can get away with numerical animations (which you can still interpolate into anything you like) and basics springs.

#### Use it like always

```jsx
import React from 'react'
import ReactDOM from 'react-dom'
import { Spring } from 'react-spring-numerical'

ReactDOM.render(
  <Spring from={{ opacity: 0 }} to={{ opacity: 1 }}>
    {props => <div style={props}>hello</div>}
  </Spring>,
  document.getElementById('root')
)
```

#### Native

The `createAnimatedComponent` may seem unfamiliar, react-spring has that as well, but for convenience it ships with a collection of html-elements that are already transformed - the downside is that it takes more bytes.

```jsx
import { Spring, createAnimatedComponent } from 'react-spring-numerical'

const AnimatedDiv = createAnimatedComponent('div')

<Spring native from={{ opacity: 0 }} to={{ opacity: 1 }}>
  {props => <AnimatedDiv style={props}>hello</AnimatedDiv>}
</Spring>,
```

#### Custom interpolators

Either call interpolators on the animated value itself or use the slightly more flexible `interpolate` function which takes an array or animated values and a function that receives their actual, numerical values and returns the interplated result.

```jsx
import { Spring, createAnimatedComponent, interpolate } from 'react-spring-numerical'

const AnimatedDiv = createAnimatedComponent('div')

<Spring native from={{ opacity: 0, vec: [0, 0] }} to={{ opacity: 1, vec: [100, 150] }}>
  {({ opacity, vec }) => (
    <AnimatedDiv
      opacity={opacity.interpolate(o => o / 2)}
      style={{ transform: interpolate(vec, (x, y) => `translate(${y}px, ${y}px)`)}}>
      hello
    </AnimatedDiv>
  )}
</Spring>,
```
