2025-11-29 | 15:03  
**Status:** #alpha 
**Tags:** #Design #Figma

# Grids and Columns
Rows are used for vertical axis. They're used for consistency when working with the 8-pt grid system. It could be any number, but you should be sticking to the amount of rows. When using the 8-pt grid system, often the size and gutter are set to 8 to keep in line with the layout system.

> In Figma, this is created through the Layout Guide when a frame is selected. Additionally, a Layout Guide can be transformed into style to be applied in project-wide frames.


# 12 Column Layout
Web standard applies a horizontal layout with 12 segments. 12 Is easily divisible, allowing for division by 2, 3, 4, and 6. Typically, the world of web-design revolves around a centered approach. Here, the screen exists of 12 columns which have a fixed width and ignore scaling. From the tablet downwards, a stretch approach is used with less columns. Here, the width of the columns scale based on the width of the screen.

20px gutter, count is 12, type stretch, margin depends on the size of the container.

| **Container Size** | **Margin** |
| -------------- | ------ |
| 1140px         | 30     |
| 960px          | 120    |
The Column Layout serves as a guide and can be broken. However, if done, this should be done with clear intention and by design, not on accident. Sticking to the Column Layout guarantees consistency, while stepping away could shake things up and make it look more interesting.

## Making Responsive Columns
When designing websites, we often use a different number of columns for different resolutions. Designers often apply the 12 / 8 / 4 rule, maintaining 12 columns for desktop designs, 8 for tablet designs and 4 for mobile designs. The gutter and margin also vary on the resolution of the screen as shown in the earlier table. 


| **Resolution Type** | **Count** | **Gutter** | **Type** | **Margin**           |
| ------------------- | --------- | ---------- | -------- | -------------------- |
| Desktop             | 12        | 20px       | Stretch  | Depends on container |
| Tablet              | 8         | 16px       | Stretch  | 32px                 |
| Mobile              | 4         | 12px       | Stretch  | 12px                 |


## References
[Master Responsive Grids (Rows & Columns) in Figma](https://www.youtube.com/watch?v=sybtdc4dYzE)
