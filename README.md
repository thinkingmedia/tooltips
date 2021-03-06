# ToolTips - [ToolTips](https://angular-demos.github.io/tooltips/)

This is a demonstration on how to create tool tips with Angular 5.

This demo is divided into three modules:

- *Main* handles the bootstrapping of the demo application.
- *Demo* handles the tooltip demonstration.
- *ToolTip* handles the UI components for tooltips.

# Demo

View this demo in action at [https://angular-demos.github.io/tooltips/](https://angular-demos.github.io/tooltips/)

# Dependencies

This application was built with these key dependencies

- Angular (tested with 5.2.1)
- Bootstrap 4 (tested with 4.0.0-beta.3)

# Installation

You need [NodeJS](https://nodejs.org/en/) installed to build and run this demo. Afterwards these two CLI commands will start a local server, where by you can access the demo at `http://localhost:4200/`

```
npm install
npm start
```

# Overview

This demo shows how to create tool tips in Angular without having to compile web components at *run-time*. Usually 
a tool tip component is appended to the DOM body and compiled when it is needed. This demo uses a different
approach where a `<tooltips>` component is used as a wrapper around the body contents. This allows the `<tooltips>`
component to create tool tips by using `*ngFor`.

An example usage:

```
<body>
    <tooltips>
          <button class="btn" [tooltip]="message"></button>
    </tooltips>
</body>
```

This approach allows the `[tooltip]` directive to easily notify the parent `<tooltips>` when and how to
display a tool tip.

## Accessibility

This demo provides accessibility features by adding the `aria-describedby` attribute to
DOM elements when a tool tip is displayed. This attribute points to the tool tip element
which contains the `role="tooltip"` attribute. 

## Design

This demo was designed to make it easier to test different aspects of tool tips:

- You can adjust the number of buttons displayed.
- Test window edge collision by aligning buttons to left or right of the page.
- Extra long page allows you to test the scrolling of tool tips off the top.
- Extra buttons at the bottom of the page to test scrolling off the bottom.
- You can control which side of a button the tool tip appears on (top, bottom, left, right)

## Architectural

This demo follows a common Angular feature module approach. Where by, routes define scopes for
features and those feature modules can be lazy loaded based upon demand.

Modules are described as follows:

- Main is the bootstrap module that starts the demo.
- Demo module handles the tooltip demonstration.
- ToolTip module handles the UI components for tooltips.

## How It Works

Tool tip support is added by inserting the `<tooltips>` component in the `BodyComponent` 
located in the *Main* module. This `ToolTipsComponent` acts like a global service as 
it is *injected* via the dependency injector into child `[tooltip]` directives.

### ToolTipsComponent

This component handles the displaying of tool tips by using a `*ngFor` on a 
collection of `ToolTipPlacement` objects. This makes it easy to support either a
single tool tip or multiple at once.

### ToolTipDirective

The `ToolTipDirective` handles the click events and calls the `add()` and `remove()` 
methods on `ToolTipsComponent` which is injected via the constructor.

### ToolTipPlacement

This is an *immutable* object that describes where a tool tip should be displayed, and
what the tool tip message is. 

### ToolTipMessageComponent

This is the component that displays a single tool tip message. It contains the logic
for edge collisions with the browser.

## CSS and UX

The styles used to color the tooltip and create the tooltip arrows were taken from the Bootstrap 4 SASS
source code. No other functionality was copied from the BootStrap project or other source.
