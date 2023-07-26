# Grid Core <!-- omit in toc -->

- [Features](#features)
- [Documentation With Examples](#documentation-with-examples)
- [Disclaimer](#disclaimer)
- [Quick Start](#quick-start)
- [Grid Classes](#grid-classes)
  - [Grids](#grids)
  - [Grid Items](#grid-items)
  - [Subgrid](#subgrid)
  - [Others](#others)
- [Customization](#customization)
  - [Container](#container)
  - [Items](#items)
- [Responsive](#responsive)
- [Basic Example](#basic-example)


## Features

- easy/intuitive grid system
- pure css
- customizable
- no unnecessary css you need to override
- __subgrids__


## Documentation With Examples

For more details and examples look [here](https://gridcore.jonas-stumpf.de).


## Disclaimer

I don't guarantee that this works flawlessly (or at all) in all browsers.  
I use this myself so most cases should work, but don't forget to double check your stuff in different browsers!

## Quick Start

1. Add css to your page

```
<link rel="stylesheet" href="grid-core.min.css">
```

2. Add a [grid class](#grid-classes) to your container element

3. Adjust columns, gap, column span
- `--columns: 12;`
- `--gap: 0px;`
- `--col-span: 1;`

4. [Responsive](#responsive) mobile first adjustments
- `sm` - `md` - `lg` - `xl` - `xxl`
- e.g. `--columns: 1; --columns-md: 3;`



## Grid Classes

`General:` classes with _grid-_ are for containing elements and classes with _grid__item_ are for grid elements

There are 2 classes for setting up a grid, and a few others for positioning or subgrids.  
_...don't name your classes starting with __grid__ if you want to be safe for future updates_

Set a [grid class](#grids) on the containing element to setup a grid.
Customize your grid via [custom properties](#customization).

### Grids

These classes setup the grid, they are necessary.

_`Note`: every class starting with __grid-__ gets the grid setup (custom properties, ...), dont name your classes __grid-...__ unless you want to create your own grid._

Creating your own grid: define `grid-template-columns` in your grid class and you're ready to go.

`.grid-default`
> basic grid with equally sized columns, nothing special


`.grid-content`
> as the name suggest, this grid stays within a content width you set
>> `--content-width` - the maximum with your content is supposed to take  
>> `--content-padding` - the padding your content has (mobile)
> 
> a grid with 2 additional columns - left and right  
> these spacer columns grow when the desired width is reached and shrink to the content padding  
> the content part is a basic grid, equally sized columns  
>> useful if content is supposed to flow out of your content width on 1 side (e.g. an image)

### Grid Items

These classes allow you to position your items (horizontally) in your grid.  
Without these, items line up normally.

`.grid__item--l`
> position your item from the left
>> `--col-start: 1;` - the item starts on the far left

`.grid__item--r`
> position your item from the right
>> `--col-start: 1;` - the item starts on the far right

### Subgrid

Getting bored? Wanna be fancy?  
Here you go, no need to wait for browser support.

`.subgrid`
> Set this class on a nested grid and the child grid will adapt its columns and gaps accordingly to it's parent grid gaps and the columns it takes up in the grid
> (you still need to define your grid class)  
> You can still change the gaps, e.g. different row gaps  
> Example:
> ```
> <div class="grid-content">
>   <div class="grid__item--l subgrid grid-default"></div>
> </div>
> ```

2 grid classes for subgrids (feel free to use them as normal grids)
to adjust to content-grids spacers on the sites:  
_Spacer on both sides? use content-grid ...._

`.grid-content--l`
> spacer on the left

`.grid-content--r`
> spacer on the right

### Others

Nice to have, irrelevant for grid layouts.  
_...might add more in the future like center all items or position item at the bottom_

`.grid__rows--equal-height`
> equally sized rows

`.grid__item--center`
> centers the item


## Customization

All of the following `custom variables` are [responsive](#responsive).  
There is no check for the values you put in there, inspect the mess you make ... counting isn't so hard after all. 

There are other variables you can play around with, they aren't responsive and changing them can break your grid. Look at the [documentation](#documentation-with-examples) and the [examples](#documentation-with-examples) for further explanation.


### Container

`--columns`
> sets the number of columns of your grid, default: 12  

`--gap`
> sets the x and y gap

`--gap-x`
> sets the x gap, overrides `--gap`

`--gap-y`
> sets the y gap, overrides `--gap`

### Items

`--col-span`
> sets the amount of columns the item takes up

`--col-start`
> sets the starting column of the item, used with `grid__item--l` and `grid__item--r`

`--row-span`
> sets the amount of rows the item takes up

`--row-start`
> sets the starting row of the item, usefull to force items in the same row or push items above others


## Responsive

Add the breakpoint suffix behind the variable:  
`--variable-sm` / `--variable-lg`

Mobile first with bootstraps breakpoints.  
Available breakpoints:
- `sm` >= 576px
- `md` >= 768px
- `lg` >= 992px
- `xl` >= 1200px
- `xxl` >= 1400px
   


## Basic Example

Copy&Paste example. For more examples look [here](#documentation-with-examples).

```
<style>
    * {box-sizing: border-box;}body{margin:0}

    /* Set content width and padding - overrides grid core defaults */
    :root {
        --content-width: 1000px;
        --content-padding: 15px;
    }
    /* class for content width */
    .content-width {
        max-width: calc(var(--content-width) + var(--content-padding) * 2);
        padding-left: var(--content-padding);
        padding-right: var(--content-padding);
        margin: 0 auto;
    }
    /* item styles for demo purposes */
    .item {
        background: #1a1a1a;
        color: white;
        display: flex;
        justify-content: center;
        align-items: center;
        border-radius: 20px;
        height: 100px;
    }

    /* -- Grid Settings -- */
    /* Default Grid */
    .grid-default {
        --columns: 1;
        --columns-sm: 2;
        --columns-lg: 3;
        --gap: 15px;
        --gap-y: 30px;
        --gap-md: 50px;
    }
    .item--large {
        --col-span-sm: 2;
    }
    
    /* Content Grid */
    .grid-content {
        --gap-y: 30px;
    }
    .grid__item--l {
        --col-start: 2;
        --col-span: 10;
        --col-span-md: 5;
    }
    .grid__item--r {
        --col-start: 1;
        --col-span: 11;
        --col-span-md: 7;
        --row-start: 1;
    }
</style>

<div class="grid-default content-width">
    <div class="item item--large">Content</div>
    <div class="item">Content</div>
    <div class="item">Content</div>
    <div class="item">Content</div>
    <div class="item">Content</div>
</div>

<div class="grid-content">
    <div class="item grid__item--l">Content Left</div>
    <div class="item grid__item--r">Content Right</div>
</div>
```

