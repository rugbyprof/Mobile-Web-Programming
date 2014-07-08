### ViewPort

`<meta name="viewport" content="width=960px">`

`<meta name="viewport" content="width=device-width">`

- `initial-scale`
- `maximum-scale`
- `user-scalabale=no`

### Fluid Layout

- Use percentages or viewport units
- Test while resizing
<br><br>
- reflow to use all space on the screen
- make sure you adapt to different screens


### Css Flex

display:flex
display:flex-inline


### Media Queries


#### Scenarios for responsive design:

- Phone 
- Tablet 
- Desktop

#### Device Pixel Ratio

`window.devicePixelRatio` = approximate number of device pixels for every "formatting pixel"

```css
display: flex;
flex-wrap: wrap;
flex-direction: row;

a {
	flex: 0 46%;
	position: relative;
}


@media (min-width: 500) {
    a {
        flex: 0 24%;
    }
}  
```

#### Responsive Images


#### Links

- http://dev.opera.com/articles/an-introduction-to-meta-viewport-and-viewport/
- http://dev.w3.org/csswg/css-device-adapt/#the-lsquouser-zoomrsquo-property
- https://developers.google.com/webmasters/smartphone-sites/details
