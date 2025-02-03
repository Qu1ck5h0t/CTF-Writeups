## I especially liked this one because I once took a class on boolean logic gates and I was good at it. Or so I say.
![image](https://github.com/user-attachments/assets/2221e3e7-cd92-482a-a075-ab8613c4a07f)
The description is much, much more intimidating than the problem is. 
The solution for this is extremely simple, as long as you know how boolean logic gates work.
![image](https://github.com/user-attachments/assets/30c508fb-b7ef-42cd-ad72-8d8cc5cdb14a)
I drew lines to represent the boolean variables, with red = false and blue = true. Since the input was [0,1,0,1,0], the lines on the diagram from top to bottom would be [red, blue, red, blue, red]. Following that, all I needed to do was to not mess up the gate handling, which I did a decent job of.

The lines in the end are [red, blue, red, blue, red, blue, blue], so end output is [0,1,0,1,0,1,1]. Therefore, we get the flag
```
ectf{0101011}
```
