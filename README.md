## vex

Dialogs for the 21st century.

### How To Use Vex

#### Basics of Opening and Passing Content

To open a dialog, call `vex.open`.

```coffeescript
vex.open
    content: '<div>Content</div>'
    afterOpen: ($vexContent) ->
        # console.log $vexContent.data().vex
        $vexContent.append $el
    afterClose: ->
        console.log 'vexClose'
```

In addition, you can wait to append your content until after the dialog has opened. (Visually, it will be perceived the same way.)

```coffeescript
vex.open
    afterOpen: ($vexContent) ->
        # console.log $vexContent.data()
        $vexContent.append $el
    afterClose: ->
        console.log 'vexClose'
```

Instead of using callbacks, you can choose to chain off the open call and bind to vexOpen and vexClose events. For example:

```coffeescript
vex
    .open()
    .bind('vexOpen', (options) ->
        options.$vexContent.append $el
    )
    .bind('vexClose', ->
        console.log 'vexClose'
    )
```

Also, since opening/closing is synchronous, you don't even have to wait for the vexOpen event. Just append right away!

```coffeescript
vex.open().append($el).bind('vexClose', -> console.log 'vexClose')
```

You can also close vex dialogs by id:
```coffeescript
$vexContent = vex.open()
vex.close($vexContent.data().vex.id)
```


#### Options

When calling `vex.open()` you can pass a number of options to handle styling and certain behaviors.

Here are the defaults:

```coffeescript
defaultOptions:
    content: ''
    showCloseButton: true
    overlayClosesOnClick: true
    appendLocation: 'body'
    className: ''
    css: {}
    overlayClassName: ''
    overlayCSS: {}
    closeClassName: ''
    closeCSS: {}
```

There are some class names in `vex.sass` you can use for the `className` property:

- Use `vex-content-auto` when making a simple dialog.
- Use `vex-content-tall` when you want to support something with a scrollable middle.
- Use `vex-content-tall-and-wide` or `fullscreen` when you want to take up most or all of the screen, respectively.