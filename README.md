# Example Tinted Model
An example of a custom Minecraft item model that makes use of the new tint system.

To get an item that has this model, use a command like
```
/give @s minecraft:stick[item_model="custom_tint:thingy",custom_model_data={colors:[[1,0,0], [0,0,1]]}]
```

You'll get a staff with an orb on the end. The orb's color is controlled by the first `custom_model_data` color
(red in the provided command), the grip's color is controlled by the second  `custom_model_data` color (blue in
the provided command), and the pommel's color is controlled by the team color of the player currently holding it.

You can test changing the pommel color by setting up some colored teams and joining them:
```
/team add green_team "Green"
/team modify green_team color green
/team add red_team "Red"
/team modify red_team color red

/team join green_team @s
/team join red_team @s
```

And you can test changing the orb color and grip color by modifying the item's custom model data:
```
# Update the orb color and grip color at the same time:
/item modify entity @a weapon.mainhand {function:"set_custom_model_data",colors:{mode:"replace_section",offset:0,values:[[1.0,0.5,0.0], [0.0,1.0,0.5]]}}

# Update just the orb color:
/item modify entity @a weapon.mainhand {function:"set_custom_model_data",colors:{mode:"replace_section",offset:0,values:[[0.0,0.5,0.5]]}}

# Update just the grip color:
/item modify entity @a weapon.mainhand {function:"set_custom_model_data",colors:{mode:"replace_section",offset:1,values:[[1.0,0.8,0.0]]}}

# Set the orb color to a scoreboard value:
# (The scoreboard value is calculated as (((R * 256) + G) * 256) + B, where RGB are all integers in the range 0 - 255.)
/item modify entity @a weapon.mainhand {function:"set_custom_model_data",colors:{mode:"replace_section",offset:0,values:[{type:"score",target:"this",score:"tintRGB"}]}}
```
