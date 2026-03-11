<div align="center">
  <img src="https://cdn.discordapp.com/attachments/1476728915522224138/1478833401208373389/AddText_03-05-01.07.38.jpg?ex=69b2682e&is=69b116ae&hm=362b1b1f064a7e6cb6cc8768970d8c5b5158899950e53b2970c6778f3e592f99&" width="100%" alt="Asteroid Banner">
  <h1>Discord.py Components V2 Master Guide</h1>
  <p><b>An In-depth Technical Documentation by 🆁︎🅸︎🆈︎🅰︎🅳︎ && Asteroid Development</b></p>
  <hr>
</div>

## Overview of Components V2

Discord Components V2 introduces a structured layout system that moves away from simple button rows. It allows for rich, nested UI elements that live directly in the message body rather than just inside embeds.

---

## 1. Core Layout Structure

### LayoutView
The base class for all V2-enabled views. Unlike the standard `ui.View`, `LayoutView` is designed to handle hierarchical components like Containers.

### Container
The top-level wrapper. Every V2 component **must** be placed inside a Container to render properly. It acts as a vertical stack for Sections, TextDisplays, and ActionRows.

### ActionRow
Used to group interactive elements (Buttons, Select Menus) within a Container. In V2, ActionRows allow for more precise placement of interactive components relative to text.

```python
import discord
from discord import ui

class CoreLayout(ui.LayoutView):
    def __init__(self):
        super().__init__(timeout=None)
        
        self.add_item(ui.Container(
            ui.TextDisplay(content="# V2 Structure"),
            ui.ActionRow(
                ui.Button(label="Action 1", style=discord.ButtonStyle.primary),
                ui.Button(label="Action 2", style=discord.ButtonStyle.secondary)
            )
        ))

2. Content & Media Elements
Section
The most versatile component. A Section can hold a primary string of text, a Thumbnail, and an accessory (like a single button or select menu).
Thumbnail
A dedicated image component. When used inside a Section, it automatically aligns to the side of the text.
MediaGallery & MediaGalleryItem
Allows for a grid of images (up to 4). MediaGalleryItem is used to define the specific properties of each image in the gallery.
class MediaExample(ui.LayoutView):
    def __init__(self):
        super().__init__()
        
        gallery = ui.MediaGallery(
            discord.MediaGalleryItem(media="[https://example.com/img1.png](https://example.com/img1.png)"),
            discord.MediaGalleryItem(media="[https://example.com/img2.png](https://example.com/img2.png)")
        )
        
        section = ui.Section(
            text="## User Profile",
            thumbnail=ui.Thumbnail(media="[https://example.com/avatar.png](https://example.com/avatar.png)")
        )

        self.add_item(ui.Container(section, gallery))

3. Formatting Components
TextDisplay
A block-level text component. It supports full markdown and is preferred over standard message content for structured data.
Separator
A horizontal line used to create visual distinction between content blocks. Use visible=True to render the line.
class FormattingExample(ui.LayoutView):
    def __init__(self):
        super().__init__()
        
        self.add_item(ui.Container(
            ui.TextDisplay(content="### Top Section"),
            ui.Separator(visible=True),
            ui.TextDisplay(content="### Bottom Section")
        ))

4. Interactive Components & Styles
Select Menus
V2 supports all standard select menus (String, User, Role, Mentionable, Channel) but allows them to be tucked inside ActionRows or as accessories in a Section.
New Button Styles
V2 utilizes the expanded discord.ButtonStyle enum, including:
 * .primary (Blurple)
 * .secondary (Grey)
 * .success (Green)
 * .danger (Red)
 * .link (Grey with redirect icon)
 * .premium (For monetization/SKU integration)
<!-- end list -->
class InteractionExample(ui.LayoutView):
    def __init__(self):
        super().__init__()
        
        select = ui.Select(
            placeholder="Choose an option...",
            options=[discord.SelectOption(label="Option A", value="a")]
        )
        
        self.add_item(ui.Container(
            ui.ActionRow(select),
            ui.ActionRow(
                ui.Button(label="Premium Feature", style=discord.ButtonStyle.premium)
            )
        ))

Component Reference Table
| Component | Description | Best Use Case |
|---|---|---|
| LayoutView | Parent View class | The foundation of any V2 UI. |
| Container | Vertical Wrapper | Organizing sections and rows. |
| Section | Text + Image row | Profiles, headers, or item listings. |
| Separator | Visual Divider | Splitting different categories of info. |
| MediaGallery | Image Grid | Showcasing multiple screenshots or items. |
<div align="center">
<p><b>Documentation provided by Asteroid Development</b></p>
<p><a href="https://dsc.gg/Asteroidhq">Support</a> | <a href="https://Asteroid-bot.ddns.net">Website</a></p>
</div>
