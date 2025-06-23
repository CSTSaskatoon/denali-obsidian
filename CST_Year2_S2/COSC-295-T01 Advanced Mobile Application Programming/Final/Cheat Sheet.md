# Cheat Sheet
## Table of Contents
- [Layouts](#Layouts)
	- [Layout Types](#Layout%20Types)
	- [Layout Options](#Layout%20Options)
		- [Layout Guide](#Layout%20Guide)
	- [Layout Code Examples](#Layout%20Code%20Examples)
- [Navigation](#Navigation)
	- [Navigation Methods](#Navigation%20Methods)
	- [Navigation Code Examples](#Navigation%20Code%20Examples)
- [List Views](#List%20Views)
	- [List View Code Examples](#List%20View%20Code%20Examples)
- [Sliders](#Sliders)
	- [Sliders Code Examples](#Sliders%20Code%20Examples)
- [Persistent Storage](#Persistent%20Storage)
	- [Persistent Storage Code Examples](#Persistent%20Storage%20Code%20Examples)

## Layouts
- [Table of Contents](#Table%20of%20Contents)

### Layout Types
- [Table of Contents](#Table%20of%20Contents)
- *`StackLayout`* - Linearly, either horizontal or vertical
- *`AbsoluteLayout`* - setting coordinates
- *`RelativeLayout`* - setting constraints based on parents dimensions and position
- *`Grid`* - rows and columns with either absolute values or ratios
- *`ScrollView`* - Provides scrolling when a view can't fit within the bounds of the screen

### Layout Options
- [Table of Contents](#Table%20of%20Contents)
- *`HorizontalOptions`* and *`VerticalOptions`* are type `LayoutOptions`

#### Layout Guide
- [Table of Contents](#Table%20of%20Contents)
![](Pasted%20image%2020250427192403.png)

### Layout Code Examples
- [Table of Contents](#Table%20of%20Contents)
- [Examples](Code%20Examples.md#Layouts)

## Navigation
- [Table of Contents](#Table%20of%20Contents)
- **Need to do `MainPage = new NavigationPage(new MainPage());` in `app.xaml.cs` if you are using `Navigation.PushAsync()`**

### Navigation Methods
- [Table of Contents](#Table%20of%20Contents)
- *`PopAsync`*
- *`PushModalAsync`*
- *`PopModalAsync`*
- *`PopToRootAsync`* - close all but root page, all other pages removed from stack
- App will crash if you do `PopModalAsync` on a normal page, or do `PopAsync` on a modal page
- Can only do `PopToRootAsync` on a normal page

### Navigation Code Examples
- [Table of Contents](#Table%20of%20Contents)
- [Examples](Code%20Examples.md#Navigation)

## List Views
- [Table of Contents](#Table%20of%20Contents)

### List View Code Examples
- [Table of Contents](#Table%20of%20Contents)
- [Examples](Code%20Examples.md#List%20Views)

## Sliders
- [Table of Contents](#Table%20of%20Contents)

### Sliders Code Examples
- [Table of Contents](#Table%20of%20Contents)
- [Examples](Code%20Examples.md#Sliders)

## Persistent Storage
- [Table of Contents](#Table%20of%20Contents)

### Persistent Storage Code Examples
- [Table of Contents](#Table%20of%20Contents)
- [Examples](Code%20Examples.md#Persistent%20Storage)
- [Database Query Example](Code%20Examples.md#Database%20SQL%20Query%20Example)

## BindingContext
- [Table of Contents](#Table%20of%20Contents)

### BindingContext Code Examples
- [Table of Contents](#Table%20of%20Contents)
- [Examples](Code%20Examples.md#BindingContext)
- [OnBindingContextChanged](Code%20Examples.md#OnBindingContextChanged)
