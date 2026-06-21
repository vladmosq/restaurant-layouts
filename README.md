# Restaurant Website Layout - Task Report

## Overview

This project demonstrates four different layout approaches for a fictional restaurant website called Vladimirs Restaurant . Each layout approach is implemented in a separate HTML file: fixed.html, fluid.html, adaptive.html, and responsive.html. Every page includes the same structure: a header, a navigation menu, a main content area with a menu section and a specials section, and a footer.


## Fixed Layout (fixed.html)

In the fixed layout, all dimensions are set in absolute pixel values. The main container has a fixed width of 960px, the navigation links have a fixed width of 150px each, and the two main columns are set at 600px and 320px respectively.

Behavior on different screen sizes:

-On a desktop with a large monitor, the layout appears centered. The content fits comfortably within the 960px container and the two-column structure is clearly visible.

-On a tablet with a viewport narrower than 960px, the container starts to overflow the visible area. The user is forced to scroll horizontally to see the full content. Part of the specials column gets cut off on the right side of the screen.

-On a smartphone, the problem becomes more severe. The 960px container is significantly wider than the screen, so you can see only the left portion of the layout and must scroll horizontally to access the rest. This is a very poor user experience.

Issues encountered:

During the development of the fixed layout, one issue I encountered was the footer overlapping with the two-column content area. The footer was rendering on top of the menu and specials sections instead of appearing below them. This happened because the two columns were using float: left and float: right, and the footer did not know where these floated elements ended. The solution was to create a clearfix class on the wrapper div. By adding a ::after pseudo-element with clear: both and display: table, the wrapper correctly calculated its height to include the floated children, and the footer dropped to its proper position below them.

Advantages: Simple to implement. The layout looks exactly as designed on the target screen size.

Disadvantages: Very poor usability on mobile devices. Content gets cut off and horizontal scrolling is required.


## Fluid Layout (fluid.html)

In the fluid layout, all dimensions are defined as percentages relative to the viewport width. The main container is set to 90% of the viewport width, the navigation links are 24% each, and the two columns are 70% and 30% of the container.

Behavior on different screen sizes:

-On a desktop, the container fills 90% of the screen and scales proportionally as the window is resized. The two-column structure is maintained and the content scales smoothly.

-On a tablet, the layout continues to scale down proportionally. There is no horizontal scrollbar, which is an improvement over the fixed layout. However, both columns simply shrink, making the specials column quite narrow.

-On a smartphone, the biggest problem appears. Both columns remain side by side but they become extremely narrow. The text in each column wraps tightly and becomes very difficult to read. There is no horizontal scrolling, but the readability and usability are poor because the content is too squished.

Effectiveness evaluation:

The fluid layout is more accessible than the fixed layout because it eliminates horizontal scrolling. However, it does not intelligently adapt the structure of the page to the screen size. It simply compresses everything proportionally, which fails on very small screens where two columns side by side are not practical.

Advantages: No horizontal scrolling. Content always fits within the viewport. Relatively simple to implement.

Disadvantages: Text becomes too squished on small screens. The two-column structure is maintained even when it no longer makes sense for the screen size.

---

## Adaptive Layout (adaptive.html)

The adaptive layout uses several predefined fixed layouts that activate at specific breakpoints using CSS media queries. Three states are defined: a desktop state at 960px, a tablet state at 720px (activated at max-width: 992px), and a mobile state at 320px (activated at max-width: 768px).

Behavior and transitions between states:

On desktop screens wider than 992px, the layout uses the default 960px container with a two-column structure and horizontal navigation links.

When the viewport crosses 992px, the layout snaps to a 720px container. The columns shrink to 450px and 240px and the navigation links become 120px wide. The transition is abrupt and visible as a sudden jump rather than a smooth scale.

When the viewport crosses 768px, the layout snaps to a 320px mobile container. The two columns stop floating and stack vertically one below the other, and the navigation links display as a vertical list.

Impact on user experience:

The adaptive layout significantly improves mobile usability compared to fixed and fluid layouts because the structure changes according to the device. On mobile, the single-column layout makes the content fully readable without squishing or scrolling.

However, the experience on screen sizes between breakpoints can be poor. For example, on a screen that is 500px wide, the mobile state activates and the 320px container sits in the center of the screen with large empty margins on both sides.

New knowledge: During this task I learned about the @media rule in CSS. The @media query allows you to apply different CSS rules depending on the characteristics of the device or viewport, most commonly the screen width. Using max-width inside a media query means the styles inside it will apply only when the viewport is at or below that specified width. This is the key tool that makes both adaptive and responsive layouts possible.

Advantages: Good control over specific device states. Mobile version is fully readable.

Disadvantages: Abrupt visual snapping between states. Poor display on screen sizes that fall between defined breakpoints. Requires defining and maintaining multiple layout states.

---

## Responsive Layout (responsive.html)

The responsive layout combines the fluid scaling of percentages with the structural flexibility of media queries. The container width is set to 90% with a max-width of 1100px. The two-column layout is built using CSS Flexbox where the menu section takes flex: 2 and the specials section takes flex: 1. At a breakpoint of 768px, flex-direction changes to column, stacking both sections vertically.

How this approach enhances flexibility and usability:

Between breakpoints, the content scales fluidly and proportionally just like in the fluid layout. There is no horizontal scrolling and the text remains readable because the flexbox proportions are maintained gracefully across a wide range of widths.

At the 768px breakpoint, the layout intelligently restructures itself. Both the main content columns and the navigation links switch from horizontal to vertical alignment. This structural change means that on a smartphone the entire layout is presented as a single readable column that does not squish any content.

The combination of fluid scaling and structural breakpoints means the layout performs well at every screen size, not just at a few fixed target widths.

How responsive design accommodates various devices:

-On a large desktop, the content fills a comfortable portion of the screen up to 1100px. 
-On a medium laptop, it scales down proportionally. 
-On a tablet near the breakpoint, the transition is smooth and the layout restructures clearly. 
-On a smartphone, the single-column layout is easy to scroll and read.

Advantages: Best user experience across all screen sizes. Smooth scaling between breakpoints. No content is cut off, squished, or hidden. Modern approach using Flexbox.

Disadvantages: More complex CSS to write and maintain compared to fixed or fluid layouts. Requires testing across many different screen sizes.


## Advantages and Disadvantages Summary

Fixed Layout: Easy to build and visually predictable on the target screen. However it is completely unusable on mobile devices due to horizontal scrolling and cut-off content.

Fluid Layout: Eliminates horizontal scrolling and scales to any screen size. However it does not restructure the layout for small screens, resulting in squished and unreadable content on smartphones.

Adaptive Layout: Provides good usability on targeted device sizes and restructures the layout for mobile. However the transitions between states are abrupt and the layout can look poor on screen sizes that fall between defined breakpoints.

Responsive Layout: Provides smooth fluid scaling at all sizes combined with intelligent structural restructuring at breakpoints. It is the most flexible and usable approach across all devices.

---

## Which Layout is Most Appropriate for a Restaurant Website?

The responsive layout is the most appropriate choice for a restaurant website. Restaurant customers frequently access websites on mobile devices while looking for menus, opening hours, or directions. A fixed layout forces mobile users to scroll horizontally and zoom in, making the experience frustrating. A fluid layout removes the scrollbar but squishes menu text to an unreadable width. An adaptive layout helps but leaves poor experiences between breakpoints.

The responsive layout solves all of these problems. It scales smoothly on every screen, restructures the content for small devices, and ensures that menu items, prices, and specials are always easy to read regardless of whether the visitor is using a desktop, tablet, or smartphone. For these reasons, the responsive approach is the professional standard for modern restaurant websites.
