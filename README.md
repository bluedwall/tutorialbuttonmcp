##Name : How to create custom button
##Author : @⛧' BlueWall#9376 (me)
#Description : how to create a button with custom textures / color / rectangles

Lets start !
First create a class that extends GuiButton ( `net.minecraft.client.gui` )
```java
public class GuiCustomButton extends GuiButton
{
    public GuiCustomButton(int buttonId, int x, int y, String buttonText)
    {
        super(buttonId, x, y, 200, 20, buttonText);
    }

    public GuiCustomButton(int buttonId, int x, int y, int widthIn, int heightIn, String buttonText)
    {
        super(buttonId, x, y, widthIn, heightIn, buttonText);
    }
}
```
Next, create a override function named drawButton
```java
    @Override
    public void drawButton(Minecraft mc, int mouseX, int mouseY)
    {
        
    }
```
Now put in the function the code below (default minecraft drawButton func)
```java
        if (this.visible)
        {
            FontRenderer fontrenderer = mc.fontRendererObj;
            mc.getTextureManager().bindTexture(buttonTextures);
            GlStateManager.color(1.0F, 1.0F, 1.0F, 1.0F);
            this.hovered = mouseX >= this.xPosition&&mouseY>=this.yPosition&&mouseX<this.xPosition+this.width&&mouseY<this.yPosition+this.height;
            int i = this.getHoverState(this.hovered);
            GlStateManager.enableBlend();
            GlStateManager.tryBlendFuncSeparate(770, 771, 1, 0);
            GlStateManager.blendFunc(770, 771);
            // THIS IS THE LINE YOU WANNA MODIFY TO CREATE A CUSTOM BUTTON
            this.drawTexturedModalRect(this.xPosition, this.yPosition, 0, 46 + i * 20, this.width / 2, this.height);
            this.drawTexturedModalRect(this.xPosition + this.width / 2, this.yPosition, 200 - this.width / 2, 46 + i*20,this.width/2,this.height);
            this.mouseDragged(mc, mouseX, mouseY);
            int j = 14737632;

            if (!this.enabled)
            {
                j = 10526880;
            }
            else if (this.hovered)
            {
                j = 16777120;
            }

            this.drawCenteredString(fontrenderer, this.displayString, this.xPosition + this.width / 2, this.yPosition + (this.height - 8) / 2, j);
        }
```
Those are the lines you wana modify :
```java

            this.drawTexturedModalRect(this.xPosition, this.yPosition, 0, 46 + i * 20, this.width / 2, this.height);
            this.drawTexturedModalRect(this.xPosition + this.width / 2, this.yPosition, 200 - this.width / 2, 46 + i*20,this.width/2,this.height);
```
To call the button :
this.buttonList.add(new GuiCustomButton(args));
