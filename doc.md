# ATTENTION HERE!
STILL UNDER COLLECTING,SOME PROPERTIES I HAVEN"T CHECKED MYSELF. 

---

#### Elements

```js
const {
	Surface,
	Shape,
	Group,
	Text,
	Path,
	ClippingRectangle,
	LinearGradient,
	RadialGradient,
	Pattern,
	Transform
} = React.ART
```

##### Surface
Container for all other ART components.

```js
render(){
	return (
		<Surface>
			{ all other componnets }
		</Surface>
	)
}
```
Property | Type | Must | tag
:-:|:-:|:-:|:-:
width| string | false | width of target surface
height|string|false|height of target surface
visible |boolean|false|visible or invisible


##### Group
To combine shapes or other groups into hierarchies that can be transformed as a set.

```js
render(){
	return (
		<Surface>
			{ this.getContainer() }
			<Shape/>
		</Surface>
	)
}

getContainer = () => {
	return (
		<Group>
			<Shape>
			<Shape>
		</Group>
	)
}
```

##### Shape
Used to draw arbitrary vector shapes from Path.
Shape implements Transform as a mixin which means it has all transform methods available for moving, scaling and rotating a shape.

```js
render(){
	return (
		<Surface>
			<Shape/>
		</Surface>
	)
}
```

Property | Type | Must | tag
:-:|:-:|:-:|:-:
width | Number | false | width of Shape
height | Number | false | height of Shape
d| String | false | container of path
fill|String|false|fill style of Shape.Any color object module will be support
stroke | String |false|stroke color of paths it contains
strokeWidth | String |false|stroke width of paths it contains
strokeDash | Object | false | demo followed.
strokeCap | String | false | cap style of path end. oneOf([0,1,2])
strokeJoin | String | false | path join point style. oneOf([0,1,2])

```js
render(){
	return (
		<Surface>
			<Shape
				d = "..."
				fill = '#000000'
				stroke = '#FFFFFF'
				strokeWidth = 12
				// strokeDash Demo
				strokeDash = {{
					count:12, // StrokeDash array length,
					strokeDash:[
						10,20,20
					]
				}}
				strokeCap:0 // 0:butt 1:round(default) 2:square
				strokeJoin:0 // 0:miter 1:round(default) 2:square
			/>
		</Surface>
	)
}
```


##### Text
Text component creates a shape based on text content using native text rendering.

```js
render(){
	return (
		<Surface>
			<Text
			
				font={`13px "Helvetica Neue", "Helvetica", Arial`}
				/*
				 * Another way to define font property
				 * font = {{
				 * 		fontFamily:'Helvetica,Neue Helvetica,Arial',
				 * 		fontSize:23
				 * 	 	fontWeight:"bold" // or normal
				 * 	   fontStyle:"italic" // or normal
				 * }
				**/
				
				fill = "#000000"
			>
				Hello World
			</Text>
		</Surface>
	)
}
```

`ART module` in React Native supplies Text component different from sebmarkbage's `art` repo that that mix `Text` and `Font` up.So `font` property is necessary,or your device will crash.And in fact, ART makes `Text` with `Path`, so just try methods what `Shape` has.

Property | Type | Must | tag
:-:|:-:|:-:|:-:
font | String or Object | true | font name and font size for text content
fill | String | false | fill color


#### APIs

```js
redner(){
	return (
		<Surface>
			<Shape
				d={ this.getPaths() }
			/>
		</Surface>
	)
}
```

##### Path
###### Path.move

```js
getPaths = () => {
	return	(
		new Path()
		.move(10,20)
		
		// This means move ctx form current point to relative right 10px bottom 20px
		// for example ctx now at (20,20) point
		// after move(10,20) the point will change to (30,40)
	)
}
```

###### Path.moveTo

```js
getPaths = () => {
	return	(
		new Path()
		.moveTo(10,20)
		
		// This means move ctx to absolute coordinate (10,20)
		// for example ctx now at (20,20) point
		// after moveTo(10,20) the point will change to (10,20)
	)
}
```

###### Path.line

```js
getPaths = () => {
	return	(
		new Path()
		.line(10,20)
		
		// This means draw a line from current position to relative right 10px bottom 20px
		// for example ctx now at (20,20) point
		// after line(10,20) you will get a line from (20,20) to (30.40)
	)
}
```

###### Path.lineTo

```js
getPaths = () => {
	return	(
		new Path()
		.lineTo(10,20)
		
		// This means draw a line from current position to absolute coordinate (10,20)
		// for example ctx now at (20,20) point
		// after lineTo(10,20) you will get a line from (20,20) to (10.20)
	)
}
```
###### Path.arc
Draw an arc with specific arguments.

```
arc(xPosition, xPosition, xRadius, yRadius[,outer,counterClockWise,rotation])
```

```js
path.arc(10,10,30,40,true,false,1)
```

###### Path.arcTo
Just like arc,instead of passing relative position,`arcTo` accept an absolute point coorid to be the arc end.
```
arcTo(xPosition, xPosition, xRadius, yRadius[,outer,counterClockWise,rotation])
```

```js
path.arcTo(60,90,30,40,true,false,1)
```

###### Path.counterArc

Same as arc,opposite clockwise.

###### Path.counterArcTo

Same as arcTo,opposite clockwise.

###### Path.curve
draw a bezier curve to relative position.

```
curve(ControlPoint1.x,ControlPoint1.y,ControlPoint2.x,ControlPoint2.y,deltaX,deltaY)
```

```js
path.curve(10,20,30,40,12,32);
```
###### Path.curveTo
draw a bezier curve to absolute position.

```
curve(ControlPoint1.x,ControlPoint1.y,ControlPoint2.x,ControlPoint2.y,endPoint.x,endPoint.y)
```

```js
path.curve(10,20,30,40,12,32);
```



###### Path.reset

###### Path.close
Draws a line to the first point in the current sub-path and begins a new sub-path.

```js
Path.close();
// It returns the current Path instance.
```

###### Path.toJson


##### Patten

##### Transform

##### ClippingRectangle

##### Morph
