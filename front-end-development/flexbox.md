# CSS Flexbox Guide (Internet Applications)
## 1. What is Flexbox?
Flexbox (Flexible Box Layout) is a CSS layout system used to arrange elements in a row or column. It is especially useful for creating responsive layouts and aligning items easily.
## 2. Flex Container vs Flex Items
To use Flexbox, you define a container and its child elements become flex items.
Example:
```
HTML:
<div class='container'>
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
</div>
CSS:
.container {
  display: flex;
}
```
## 3. Flex Direction
Controls the direction of items inside the container.  
row (default): items go left to right  
column: items go top to bottom  
```
.container {
  display: flex;
  flex-direction: row;
}
```
## 4. Justify Content (Horizontal Alignment)
Controls alignment along the main axis (usually horizontal).
Values:
flex-start
center
flex-end
space-between
space-around
```
.container {
  display: flex;
  justify-content: center;
}
```
## 5. Align Items (Vertical Alignment)
Controls alignment along the cross axis (usually vertical).
Values:
flex-start
center
flex-end
stretch
```
.container {
  display: flex;
  align-items: center;
}
```
## 6. Gap Between Items
Adds space between flex items without using margin.
```
.container {
  display: flex;
  gap: 10px;
}
```
## 7. Flex Wrap (Responsive Layout)
Allows items to wrap onto a new line when there is not enough space.
```
.container {
  display: flex;
  flex-wrap: wrap;
}
```
## 8. Common Layout Example (Navigation Bar)
```
HTML:
<nav class='nav'>
  <a href='#'>Home</a>
  <a href='#'>About</a>
  <a href='#'>Contact</a>
</nav>
CSS:
.nav {
  display: flex;
  justify-content: space-between;
  background-color: #333;
}
.nav a {
  color: white;
  padding: 10px;
  text-decoration: none;
}
```
